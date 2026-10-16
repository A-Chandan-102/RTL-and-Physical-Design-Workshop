# Module 10: Detailed Routing, DRC and TritonRoute

## Contents

1. Introduction to Maze Routing – Lee's Algorithm
2. Lee's Algorithm – Conclusion
3. Design Rule Check (DRC)
4. Basics of Global and Detailed Routing
5. TritonRoute Feature 1 – Pre-processed Route Guides
6. TritonRoute Features 2 & 3 – Inter-guide Connectivity and Intra- & Inter-layer Routing
7. TritonRoute Method to Handle Connectivity
8. Routing Topology Algorithm
9. Parasitic Extraction
10. Key Takeaways

---

## 1. Introduction to Maze Routing – Lee's Algorithm

Lee's algorithm is a grid-based maze-routing algorithm used to find a path between two pins while avoiding obstacles. It uses wavefront expansion, which is based on Breadth-First Search (BFS).

### Working Principle

1. The routing area is divided into a uniform grid.
2. The source pin is selected as the starting point.
3. The neighbouring grid cells are explored and labelled according to their distance from the source.
4. The wavefront continues expanding until the destination pin is reached.
5. The path is traced backward from the destination to the source by following decreasing labels.

### Example

Consider two pins, A and B, separated by obstacles.

- The algorithm starts at pin A and explores the available neighbouring cells.
- Each reachable cell is assigned a distance label.
- When pin B is reached, the algorithm traces the labels backward to identify the path.
- The selected path avoids obstacles and provides the shortest route in terms of grid steps.

### Key Points

- Finds the shortest path in terms of grid steps when a legal path exists.
- Avoids obstacles by exploring only reachable grid cells.
- Can be used to understand the fundamentals of routing in integrated circuits.
- Requires considerable memory and computation for large routing grids.

---

## 2. Lee's Algorithm – Conclusion

Lee's algorithm provides a reliable method for finding a legal path between two points in a routing grid.

### Advantages

- Guarantees a shortest path in an unweighted grid if a legal path exists.
- Naturally handles obstacles during path searching.
- Provides a systematic method for finding connections between pins.

### Limitations

- The search may explore many unnecessary grid cells.
- Memory and computational requirements increase with the size of the routing grid.
- Becomes inefficient for large VLSI designs containing millions of routing resources.

Modern detailed routers use optimisations such as route guides, pattern routing, heuristic searches, and rip-up-and-reroute techniques to improve routing efficiency.

The basic principle of exploring available paths while avoiding obstacles remains important in modern detailed routing.

---

## 3. Design Rule Check (DRC)

Design Rule Check (DRC) verifies whether the physical layout satisfies the manufacturing rules specified by the foundry.

These rules define the minimum dimensions, spacing, and connectivity-related geometric constraints required for metal wires, vias, and other layout structures.

### 3.1 Important Design Rules

#### 1. Wire Width

Wire width is the physical width of a metal conductor.

- Every metal layer has a minimum permitted wire width.
- A wire narrower than the permitted value causes a width violation.
- Wire width affects resistance, current-carrying capability, and routing density.

#### 2. Wire Spacing

Wire spacing is the minimum edge-to-edge distance between neighbouring metal shapes.

- Wires belonging to different nets must maintain the required spacing.
- Insufficient spacing can cause electrical shorts or manufacturing problems.
- The permitted spacing depends on the metal layer, wire geometry, and applicable technology rules.

#### 3. Wire Pitch

Wire pitch is the distance between corresponding points, usually the centre lines, of adjacent parallel routing tracks.

For equally sized parallel wires:

`Wire Pitch = Wire Width + Edge-to-edge Wire Spacing`

- Wire pitch determines the spacing between routing tracks.
- Smaller pitch can support denser routing.
- Minimum width and spacing constraints limit how closely wires can be placed.

#### 4. Via Width

A via provides an electrical connection between different metal layers.

- Via dimensions must satisfy the permitted cut-size rules.
- The surrounding metal must provide the required enclosure.
- Via placement must also satisfy applicable spacing and alignment rules.

### 3.2 Signal Short

A signal short occurs when two nets that should be electrically separate become unintentionally connected through overlapping or touching metal shapes.

For example, if a routing wire accidentally touches a wire belonging to another net, the two signals may become electrically connected.

**Correction:** The routing geometry must be changed to remove the short while maintaining the required connections.

### 3.3 DRC Clean

During detailed routing, the router checks the geometry of wires and vias against the applicable design rules.

The routing diagrams demonstrate how a violation can be identified and corrected by modifying the routing geometry. They also illustrate the importance of checking via dimensions and ensuring that the corrected layout has no unintended signal short.

A DRC-clean result means that the checks performed by the tool report no remaining violations within their configured scope.

### Importance of DRC

- Ensures the layout follows fabrication constraints.
- Prevents shorts and manufacturing-related defects.
- Improves the reliability of the physical design.
- Helps ensure that the layout is suitable for fabrication.

---

## 4. Basics of Global and Detailed Routing

Routing connects the pins of standard cells and macros using metal wires and vias.

The routing process is divided into two major stages: global routing and detailed routing.

### 4.1 Global Routing

Global routing determines the approximate paths that nets should follow through the chip.

- Divides the routing region into larger grid regions called GCells.
- Generates route guides for individual nets.
- Estimates wirelength and identifies routing congestion.
- Assigns approximate paths through available routing regions.
- Does not determine the complete, exact metal geometry.

### Route Guides

Route guides specify the approximate regions through which a net should travel.

They help the detailed router understand the intended routing path and reduce unnecessary exploration of the entire chip.

### 4.2 Detailed Routing

Detailed routing converts the global routing guides into actual metal wires and vias.

- Selects legal routing tracks.
- Connects the required pins.
- Inserts vias when connections must move between metal layers.
- Observes manufacturing rules specified by the PDK.
- Resolves local routing conflicts and DRC violations.
- Produces the final physical interconnections.

### Difference Between Global and Detailed Routing

| Global Routing | Detailed Routing |
|---|---|
| Determines approximate routing paths. | Determines exact wire and via geometry. |
| Uses GCells and route guides. | Uses actual routing tracks and layer information. |
| Estimates congestion and wirelength. | Resolves local congestion and geometric conflicts. |
| Does not generate the final detailed geometry. | Generates physical connections subject to design rules. |

### 4.3 TritonRoute

TritonRoute is the detailed-routing engine used in the OpenROAD flow.

It uses global-route guides and technology information to construct legal connections between pins.

Important routing considerations include:

- Available metal layers and their preferred directions.
- Routing tracks and via definitions.
- Pin-access locations.
- Wire width and spacing constraints.
- Congestion handling and DRC-repair operations.

### Routing Flow

`Global Routing → Route Guides → Detailed Routing → DRC Checking → Parasitic Extraction`

---

## 5. TritonRoute Feature 1 – Pre-processed Route Guides

Route guides specify the approximate regions in which a net should be routed. TritonRoute uses these guides to direct detailed routing.

The supplied diagram illustrates the preprocessing of route guides before they are used during detailed routing.

### 5.1 Pre-processing of Route Guides

#### 1. Initial Route Guides

The initial guides indicate the approximate path between the source and destination pins.

They provide the starting information for detailed routing.

#### 2. Splitting

A long or complex guide is divided into smaller segments.

This makes it easier to process individual guide regions and manage their geometry.

#### 3. Merging

Compatible guide segments are combined when necessary.

Merging helps simplify the routing representation and maintain continuity between connected sections.

#### 4. Bridging

Additional guide segments are introduced to connect separated portions of a route.

This helps create a usable routing path when the initial guide segments do not provide sufficient connectivity.

#### 5. Pre-processed Guides

The final preprocessed guides are arranged to support detailed routing while respecting the required geometry and preferred routing directions.

### 5.2 Requirements of Pre-processed Guides

As illustrated in the supplied diagram:

- Guides should have the required unit width for the routing representation.
- Guides should follow the preferred direction of their metal layer.
- Guide segments should provide sufficient coverage for the required connections.

For example, the diagram identifies **vertical routing as the preferred direction for M1** and **horizontal routing as the preferred direction for M2**.

The actual preferred directions depend on the technology and routing configuration.

### Importance

- Provides a structured starting point for detailed routing.
- Reduces unnecessary route searching.
- Helps manage the connection between separated guide segments.
- Encourages routing along preferred metal-layer directions.

TritonRoute uses the guides to direct routing while resolving pin-access, connectivity, congestion, and design-rule constraints.

---

## 6. TritonRoute Features 2 & 3 – Inter-guide Connectivity and Intra- & Inter-layer Routing

### 6.1 Inter-guide Connectivity

A net may have multiple route guides that do not directly form a continuous connection.

TritonRoute must connect these guide segments to ensure that all required terminals belong to the same electrical net.

This involves finding legal connections between separate guide regions while considering available routing tracks and design rules.

### 6.2 Intra-layer Routing

Intra-layer routing connects points using wires on the same metal layer.

- Avoids unnecessary layer changes.
- Can reduce via usage.
- Uses available tracks on the selected metal layer.
- Is suitable when the required connection can be completed legally on a single layer.

### 6.3 Inter-layer Routing

Inter-layer routing connects different metal layers using vias.

- Used when a connection must move from one metal layer to another.
- Helps overcome congestion and routing obstacles.
- Provides connectivity between different routing directions.
- Requires vias that satisfy the applicable manufacturing rules.

### 6.4 Routing Across Multiple Layers

The supplied routing-layer diagram illustrates routing performed across different metal layers and panels.

The routing process can be organised so that:

1. Routing is performed on the current panel of a metal layer.
2. Previously routed panels are considered while routing neighbouring regions.
3. Additional metal layers are used to complete connections and resolve conflicts.
4. Different panel groups can be processed in a planned order to manage interactions between routes.

This approach helps organise large routing problems and reduces conflicts between routing regions.

The combination of inter-guide connectivity, intra-layer routing, and inter-layer routing allows detailed routers to complete nets across the available routing resources.

---

## 7. TritonRoute Method to Handle Connectivity

TritonRoute must establish electrical connectivity between all terminals belonging to a net.

The supplied diagram shows a design containing multiple input pins, output pins, clock connections, standard cells, buffers, and pre-placed blocks.

The router must connect the required terminals while navigating around obstacles and avoiding conflicts with other nets.

### 7.1 Pin Access

Pin access identifies suitable locations through which wires can connect to standard-cell and macro pins.

Poor pin access can make routing difficult even when a global route guide exists.

### 7.2 Routing Graph

The available routing resources can be represented as a graph containing:

- Horizontal and vertical routing locations.
- Available routing tracks.
- Connections between metal layers.
- Obstacles and unavailable routing regions.

A three-dimensional representation can use the coordinates:

`(x, y, metal layer)`

A change in metal layer requires an appropriate via connection.

### 7.3 Path Search

The router searches for legal paths between the required terminals.

The search considers route guides, available tracks, obstacles, and applicable design rules.

### 7.4 Connectivity Completion

For a multi-terminal net, every required terminal must be connected to the same electrical network.

The routing topology may contain branches that connect multiple terminals using a shared path.

### 7.5 Rip-up-and-reroute

When a route causes congestion or design-rule violations, the router may remove an existing route and search for an alternative path.

The process can include:

1. Identifying a problematic route.
2. Removing or modifying the affected routing geometry.
3. Searching for an alternative legal path.
4. Reconnecting the required terminals.
5. Rechecking the resulting geometry.

This process helps resolve routing conflicts and improve the overall routing solution.

### Objective

The final objective is to connect every required terminal while satisfying connectivity, routing, and manufacturing constraints.

---

## 8. Routing Topology Algorithm

Routing topology describes the overall structure of connections between the terminals of a net before the final metal geometry is generated.

For a two-terminal net, the topology defines a path between the source and destination. For a multi-terminal net, it defines how the terminals are interconnected.

### Common Routing Approaches

#### 1. Maze Routing

Searches through available grid cells to find a legal path while avoiding obstacles.

#### 2. Pattern Routing

Uses predefined path shapes, such as L-shaped and Z-shaped routes, where suitable.

#### 3. Steiner-Tree-Based Routing

Finds a connection structure for multiple terminals, potentially using intermediate branching points to reduce total wirelength.

#### 4. Rip-up-and-reroute

Reconstructs parts of the routing solution to resolve congestion and design-rule violations.

### Routing Topology in Detailed Routing

1. Determines how the terminals of a net should be connected.
2. Provides an initial structure for path searching.
3. Considers routing resources, obstacles, and available metal layers.
4. Is refined during detailed routing to satisfy connectivity and DRC constraints.

The selected topology acts as the structural plan for producing the final metal wires and vias.

---

## 9. Parasitic Extraction

Parasitic extraction estimates the unwanted resistance and capacitance introduced by the physical interconnections of an integrated circuit.

The supplied diagram illustrates how the completed routing layout contains additional electrical effects that are absent from an ideal logical netlist.

### 9.1 Sources of Parasitics

#### Wire Resistance

Metal wires have finite resistance.

- Longer wires generally have greater resistance.
- Narrower wires generally have greater resistance for the same material and thickness.
- Resistance contributes to voltage drop and propagation delay.

#### Wire Capacitance

Metal wires have capacitance due to their surroundings.

- Capacitance exists between a wire and other conductors, including nearby wires and reference structures.
- Longer wires generally introduce more capacitance.
- Coupling capacitance can occur between neighbouring signal wires.

### 9.2 Extracted RC Network

After routing, the interconnections can be represented using parasitic resistors and capacitors.

- **R:** Represents the resistance of the interconnect.
- **C:** Represents the parasitic capacitance of the interconnect.

The extracted network provides a more realistic representation of the circuit than an ideal connection with zero resistance and capacitance.

### 9.3 Importance of Parasitic Extraction

- Improves the accuracy of timing analysis.
- Helps estimate interconnect delay.
- Helps evaluate signal transition times.
- Supports signal-integrity and power analysis.
- Identifies the effect of physical routing on circuit performance.

### Relationship with Static Timing Analysis

Parasitic extraction provides interconnect information required for accurate post-route timing analysis.

Long or highly capacitive interconnects can increase delay and worsen slew. The extracted parasitics are therefore used to evaluate the circuit under more realistic physical conditions.

---

## 10. Key Takeaways

- **Lee's Algorithm:** Uses grid-based wavefront expansion to find the shortest legal path between two pins in an unweighted grid.
- **Global Routing:** Generates approximate paths and route guides while considering wirelength and congestion.
- **Detailed Routing:** Converts route guides into actual metal wires and vias using available routing tracks.
- **Wire Width:** Defines the minimum permitted conductor width.
- **Wire Spacing:** Defines the minimum edge-to-edge distance between neighbouring metal shapes.
- **Wire Pitch:** Defines the distance between adjacent routing tracks, usually measured from centre to centre.
- **Via Rules:** Ensure that via dimensions and metal enclosures satisfy manufacturing constraints.
- **DRC Clean:** Confirms that the applicable geometric checks report no remaining violations.
- **Pre-processed Route Guides:** Use splitting, merging, and bridging to prepare guides for detailed routing.
- **Metal-Layer Directions:** Preferred routing directions help organise connections and reduce routing conflicts.
- **Inter-guide Connectivity:** Connects separated guide segments to establish complete net connectivity.
- **Intra-layer Routing:** Creates connections on the same metal layer.
- **Inter-layer Routing:** Uses vias to connect different metal layers.
- **Rip-up-and-reroute:** Removes and reconstructs problematic routes to resolve congestion or design-rule violations.
- **Routing Topology:** Defines the overall connection structure between the terminals of a net.
- **Parasitic Extraction:** Estimates the resistance and capacitance of physical interconnects, enabling more accurate post-route timing and signal analysis.

The detailed-routing stage transforms the approximate connections produced during global routing into physical inter
