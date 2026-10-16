# Module 10: Detailed Routing, DRC and TritonRoute

## Contents

1. Introduction to Maze Routing – Lee's Algorithm
2. Lee's Algorithm – Conclusion
3. Design Rule Check (DRC)
4. Basics of Global and Detailed Routing & Configuring TritonRoute
5. TritonRoute Feature 1 – Honors Pre-processed Route Guides
6. TritonRoute Features 2 & 3 – Inter-guide Connectivity and Intra- & Inter-layer Routing
7. TritonRoute Method to Handle Connectivity
8. Routing Topology Algorithm

---

## 1. Introduction to Maze Routing – Lee's Algorithm

Lee's algorithm is a grid-based routing algorithm used to find a path between two points while avoiding obstacles. It uses a wavefront expansion method based on Breadth-First Search (BFS).

### Working Principle

1. The routing area is divided into a grid.
2. The source pin is selected as the starting point.
3. The neighbouring grid cells are explored and labelled according to their distance from the source.
4. The wavefront continues expanding until the destination pin is reached.
5. The shortest path is traced backward from the destination to the source by following decreasing labels.

### Key Points

- Finds the shortest path in terms of grid steps when a legal path exists.
- Avoids obstacles during path searching.
- Can be used for maze routing in integrated circuits.
- Requires considerable memory and computation for large routing grids.

---

## 2. Lee's Algorithm – Conclusion

Lee's algorithm provides a reliable method for finding a legal path between pins while avoiding obstacles.

- **Shortest Path:** Finds the minimum-length path in an unweighted routing grid.
- **Obstacle Avoidance:** Explores only reachable grid cells.
- **Limitation:** Its memory and computational requirements increase with the size of the routing grid.
- **Modern Routing:** Advanced routers use optimisations such as route guides, heuristic searches, and rip-up-and-reroute techniques to improve routing efficiency.

The basic principle of exploring available paths and finding a connection remains important in modern detailed routing.

---

## 3. Design Rule Check (DRC)

Design Rule Check (DRC) verifies whether the physical layout satisfies the manufacturing rules specified by the foundry. These rules define the minimum dimensions and spacing required for metal wires, vias, and other layout structures.

### Important Design Rules

1. **Wire Width:** The minimum permitted width of a metal wire.
2. **Wire Spacing:** The minimum distance between neighbouring wires on the same layer.
3. **Wire Pitch:** The distance between corresponding points of adjacent routing tracks, generally measured from centre to centre.
4. **Via Width:** The required dimensions of a via used to connect different metal layers.

### Types of DRC Violations

- **Signal Short:** Two electrically different nets become unintentionally connected.
- **Width Violation:** A wire is narrower than the permitted minimum width.
- **Spacing Violation:** Two shapes are placed closer than the minimum allowed distance.
- **Via Violation:** A via or its surrounding metal enclosure does not satisfy the required rules.

### Importance of DRC

- Ensures the layout follows fabrication constraints.
- Prevents shorts and other manufacturing-related defects.
- Improves the reliability of the physical design.
- Helps ensure that the final layout is suitable for fabrication.

A DRC-clean layout satisfies the applicable geometric design rules checked by the verification tool.

---

## 4. Basics of Global and Detailed Routing & Configuring TritonRoute

Routing connects the pins of standard cells and macros using metal wires and vias.

### Global Routing

Global routing determines the approximate paths that nets should follow through the chip.

- Divides the routing region into larger grid regions called GCells.
- Generates route guides for individual nets.
- Estimates wirelength and identifies congestion.
- Does not determine the complete, exact metal geometry.

### Detailed Routing

Detailed routing converts the global routing guides into actual metal wires and vias.

- Selects legal routing tracks.
- Connects the required pins.
- Inserts vias when connections must move between metal layers.
- Observes the manufacturing rules specified by the PDK.
- Resolves local routing conflicts and DRC violations.

### TritonRoute

TritonRoute is the detailed routing engine used in the OpenROAD flow.

Its routing process uses global-route guides and technology information to construct legal connections between pins.

Important routing configurations include:

- Available metal layers and their preferred directions.
- Routing tracks and via definitions.
- Pin-access locations.
- Design rules and spacing constraints.
- Congestion handling and DRC-repair operations.

**Routing Flow:**

Global Routing → Route Guides → Detailed Routing → DRC Checking → Parasitic Extraction

---

## 5. TritonRoute Feature 1 – Honors Pre-processed Route Guides

Route guides specify the approximate regions in which a net should be routed. TritonRoute uses these guides to direct detailed routing.

Before routing, the guides may require preprocessing to make them suitable for the routing engine.

### Pre-processing of Route Guides

1. **Initial Route Guides:** The original guides indicate the approximate paths between pins.
2. **Splitting:** Long or complex guides are divided into smaller segments.
3. **Merging:** Compatible guide segments are combined where necessary.
4. **Bridging:** Additional guide segments are introduced to connect separated portions of a route.
5. **Pre-processed Guides:** The resulting guides are arranged to support legal routing.

### Requirements of Pre-processed Guides

- Guides should have the required unit width for the routing representation.
- Guides should follow the preferred direction of their metal layer.
- Guide segments should provide sufficient coverage for the required connections.

For example, a technology may prefer vertical routing on one metal layer and horizontal routing on another. The actual directions depend on the PDK and routing configuration.

TritonRoute attempts to follow the guides while resolving pin access, connectivity, and design-rule constraints.

---

## 6. TritonRoute Features 2 & 3 – Inter-guide Connectivity and Intra- & Inter-layer Routing

### Inter-guide Connectivity

A net may have multiple route guides that do not directly form a continuous connection.

TritonRoute must connect these guide segments to ensure that all required terminals belong to the same electrical net.

This involves finding legal connections between separate guide regions while considering available routing tracks and design rules.

### Intra-layer Routing

Intra-layer routing connects points using wires on the same metal layer.

- Avoids unnecessary layer changes.
- Can reduce via usage.
- Uses available tracks on the selected metal layer.

### Inter-layer Routing

Inter-layer routing connects different metal layers using vias.

- Used when the required path cannot be completed efficiently on one layer.
- Helps overcome congestion and routing obstacles.
- Provides connectivity between horizontal and vertical routing resources.

The combination of intra-layer and inter-layer routing allows TritonRoute to complete connections across the routing grid.

---

## 7. TritonRoute Method to Handle Connectivity

TritonRoute must establish electrical connectivity between all terminals belonging to a net.

### Main Steps

1. **Pin Access:** Identifies suitable access points through which wires can connect to cell and macro pins.
2. **Routing Graph:** Represents available routing resources across positions and metal layers.
3. **Path Search:** Finds legal paths between the required terminals.
4. **Via Insertion:** Adds vias when a connection requires a change of metal layer.
5. **Connectivity Completion:** Connects all terminals belonging to the net.
6. **DRC Repair:** Adjusts routes to remove geometric violations while maintaining connectivity.

### Rip-up-and-reroute

When a route causes congestion or design-rule violations, the router may remove an existing route and search for an alternative path.

This process helps resolve conflicts and improve the overall routing solution.

The final objective is to connect every required terminal while satisfying the routing and manufacturing constraints.

---

## 8. Routing Topology Algorithm

Routing topology describes the overall structure of connections between the terminals of a net before the final metal geometry is generated.

For a two-terminal net, the topology defines a path between the source and destination. For a multi-terminal net, it defines how the terminals are interconnected.

### Common Routing Approaches

- **Maze Routing:** Searches through available grid cells to find a legal path.
- **Pattern Routing:** Uses predefined path shapes, such as L-shaped and Z-shaped routes, where suitable.
- **Steiner-Tree-Based Routing:** Finds a connection structure for multiple terminals, potentially using intermediate branching points to reduce total wirelength.
- **Rip-up-and-reroute:** Reconstructs parts of the routing topology to resolve congestion and design-rule violations.

### Routing Topology in Detailed Routing

1. Determines how the terminals of a net should be connected.
2. Provides an initial structure for path searching.
3. Considers routing resources, obstacles, and available metal layers.
4. Is refined during detailed routing to satisfy connectivity and DRC constraints.

The selected topology acts as the structural plan for producing the final metal wires and vias.

---

## Summary

- Lee's algorithm demonstrates how shortest legal paths can be found using grid-based wavefront expansion.
- DRC verifies that physical layouts satisfy manufacturing constraints such as wire width, spacing, pitch, and via dimensions.
- Global routing generates approximate route guides, while detailed routing creates actual metal connections.
- TritonRoute uses pre-processed route guides, pin access, layer transitions, and routing optimisation to complete nets.
- Routing topology determines the overall connection structure, and parasitic extraction estimates the resistance and capacitance of the completed interconnects for further timing analysis.
