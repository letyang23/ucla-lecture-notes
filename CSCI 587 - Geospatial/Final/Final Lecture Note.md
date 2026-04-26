# 3/9 Lecture: k-Nearest Neighbor (k-NN) in Road Networks & VN3 Algorithm

## 📌 Course Administration

- **Attendance Policy Update:** Maximum of 3 physical absences and 3 Zoom participations allowed. Beyond this, up to a 10% grade deduction may be applied based on lack of participation.
- **Exam 1 Reminder:** Takes place next class in the same room. Bring a pen and Student ID.
- **Content Warning:** The material covered in *this* lecture will **not** be on Exam 1, but it will be on Exam 2. However, it naturally includes a review of Exam 1 concepts (Voronoi Diagrams, k-NN).

------

## 1. The k-Nearest Neighbor (k-NN) Problem: Basics

- **Definition:** Given a set of objects $P$ and a query point $Q$, find the $k$ objects in $P$ that are closest to $Q$.
- **Naive Approach:** Calculate the distance to every point in the database ($O(N)$ complexity), which is highly inefficient.
- **Euclidean Space Solutions ($O(\log N)$):**
  - **Object-based indexing:** e.g., R-trees (indexes based on the data objects).
  - **Space-based indexing:** e.g., Grid, Quad-trees (partitions the space independent of the objects).

## 2. Euclidean Distance vs. Road Networks

- **The Problem:** Traditional spatial indexing assumes straight-line (Euclidean) distance. In reality, distance is constrained by road networks (shortest path or fastest time).
- **Data Evolution (Side Story):** Early map data (USGS Tiger) didn't accurately match real-world satellite imagery. Companies like Navteq physically drove streets to collect highly accurate graph data (vertices and edges) for early GPS navigation (like BMW).
- **Previous Network Approaches (e.g., INE - Incremental Network Expansion):**
  - Uses Dijkstra's algorithm to expand outward from $Q$ until it hits an object.
  - *Flaw:* Wastes computational resources expanding in directions moving away from the actual target.

------

## 3. Voronoi Diagrams (Exam 1 Review)

- **Concept:** Partitions a 2D space given a set of "generator" points. Every location inside a generator's polygon is closer to that generator than to any other.
- **Construction:** Created using perpendicular bisectors between neighboring points.
- **Key Properties:**
  - The diagram is unique for a given set of points.
  - Shared edges are equal distance from neighboring generators.
  - The 1st nearest neighbor is guaranteed to be an adjacent polygon.
  - *Complexity Bound:* The average number of edges per Voronoi polygon is **at most 6**. This bounds the complexity of nearest-neighbor searches to roughly $O(K)$.

------

## 4. The VN3 Algorithm: Network Voronoi Diagrams

The core of this lecture focuses on applying Voronoi concepts to network graphs rather than open 2D space.

- **Network Voronoi Diagram:** Partitions a road network graph. Instead of 2D Euclidean distance, the boundaries are based on **network distance** (shortest path on the graph).
- **Border Points:** Points on the graph edges where the network distance to two adjacent generators is exactly equal.

### Step 1: Offline Processing (Pre-computation)

This step is computationally heavy but done once in advance.

1. **Generate Polygons:** Expand out from generators to find all border points and connect them to form Network Voronoi cells.
2. **Create an Index:** (Initially done with an R-Tree—*see "The MBR Mistake" below for why this changed*).
3. **Pre-compute Distances (Table Generation):**
   - **Intra-network:** Distance from border points to the generator *inside* its own polygon.
   - **Inter-network:** Distance from the border points of one polygon to the border points of neighboring polygons.
   - *Result:* This creates a fast key-value store of pre-calculated shortest paths.

### Step 2: Online Processing (Query Time)

1. **Find 1st Nearest Neighbor:** Use the spatial index (R-tree/Quad-tree) to locate which polygon $Q$ is inside. Time complexity: $O(\log N)$.

2. **Find k-th Nearest Neighbor:** 

   - No need to run massive Dijkstra searches.

   - Calculate Dijkstra *only locally* from $Q$ to the border points of its containing polygon.
   - For the rest of the path, simply look up the distances in the pre-computed tables.

### Performance Evaluation

- **Speed:** VN3 is orders of magnitude faster than INE (e.g., finding $K=25$ took 25 seconds for VN3 vs. 430 seconds for INE).
- **Stability:** Pre-computation overhead is relatively fixed regardless of data density. Dense data (restaurants) creates many small polygons with few border points, while sparse data (hospitals) creates few large polygons with many border points. It balances out.
- **Impact:** The filtering efficiency of Network Voronoi diagrams was so good it inspired future research using Voronoi diagrams for pure Euclidean spaces (the Vor-tree).

------

## 5. The "MBR Mistake" & The Quad-tree Solution

- **The Original Flaw:** In the original 2004 paper, researchers grouped the Network Voronoi cells into Minimum Bounding Rectangles (MBRs) and indexed them using an **R-tree**.
- **Why it was terrible:**
  1. **Massive Overlap:** Because road networks snake around, MBRs heavily overlapped, making the R-tree highly inefficient.
  2. **Misclassification (False Negatives):** Connecting graph border points with straight lines creates artificial polygon boundaries in undefined space. If a query point fell into a dead-end street (cul-de-sac) near an artificial boundary, the R-tree might return the wrong nearest neighbor because the actual graph path required driving all the way out and around.
- **The Fix (Quad-tree):** Instead of drawing artificial polygons, use a **Quad-tree** to index the raw categorized edges.
  - Partition space into 4 squares. If a square contains roads belonging to different generators, partition it again.
  - *Result:* Low resolution (big boxes) in the center of a network region, and high resolution (tiny boxes) strictly along the borders. This cleanly separates the networks without overlap or false boundaries.

------

## 6. Disadvantages of the VN3 Approach

While VN3 was a massive leap forward, it has two major limitations:

1. **Class Segregation:** You must build a completely separate index for every class of object (one for hospitals, one for gas stations). It is difficult to run a combined query (e.g., "Find the nearest hospital *or* gas station").
2. **Dynamic Edge Weights:** Pre-computation relies on static graph distances. If edge weights change rapidly (e.g., real-time **traffic** causing travel times to fluctuate), the pre-computed tables become invalid. (Road closures/updates are fine because they are local, but systemic traffic breaks the model).



# 3/23 Lecture

## Exam 1 Review & Logistics

- The exam was statistically fair with no outliers.
- The median and mean were close to each other.
- The median was exactly 75 (the midpoint of the 50-100 curve).
- The maximum score achieved on each individual question matched the total possible score for that question (no impossible questions).
- The overall highest score was 100.
- Historically, students who skip class frequently fall below the median.

------

## Paper Overview: Shortest Path & KNN in Network Space

This lecture critiques a SIGMOD 2008 Best Paper that addresses shortest path and K-Nearest Neighbor (KNN) calculations in a road network without invoking Dijkstra's algorithm at query time. The professor notes the algorithm is "elegant" but highly impractical.

### Previous Work & Baselines

| **Approach**                   | **Space Complexity** | **Retrieval Complexity** | **Notes**                                                    |
| ------------------------------ | -------------------- | ------------------------ | ------------------------------------------------------------ |
| **Exhaustive Pre-computation** | $O(N^3)$             | $O(1)$                   | Stores the entire path between all node pairs. $N^2$ pairs $\times$ path length $N$. Completely unscalable. |
| **Dijkstra / A\***             | $O(N)$               | Depends on graph size    | Expands radially around the source, exploring many unnecessary nodes. |
| **INE / IER**                  | Varies               | Varies                   | VLDB 2003 papers. Slower, older baselines used in the paper. |
| **VN3**                        | Varies               | Varies                   | VLDB 2004 paper using Voronoi diagrams. State-of-the-art at the time, but completely ignored by the 2008 authors. |

------

## The "Next Hop" Concept

The paper attempts to reduce the shortest path problem into a series of database lookups using spatial coherence.

- **Spatial Coherence:** Nodes grouped in the same general direction share the same "first edge" (next hop) to get there.
- **Coloring:** For a given vertex, every other node in the entire network is colored based on which outgoing edge you must take to reach it.
- **Theoretical Space:** $O(N^2)$ (storing the next hop for every source-destination pair).
- **Theoretical Retrieval:** $O(P)$, where $P$ is the number of nodes in the path (requiring $P$ lookups).

### Using Quadtrees for Storage

To store these colored regions, the authors propose building a Quadtree for every single node in the network.

- A Quadtree groups spatial areas of the same color to save space.
- **Problem 1:** You need $N$ quadtrees (one for each vertex).
- **Problem 2:** The worst-case space complexity of a single quadtree is $O(N^2)$. Total space becomes $O(N^3)$, making it no better than exhaustive pre-computation.
- **Problem 3:** Querying the quadtree adds a logarithmic factor. Retrieval becomes $O(P \log N)$. This is slower than the theoretical $O(P)$.

------

## Reducing Space Complexity: The Monotonic Assumption

To fix the $O(N^3)$ space issue and make the paper look competitive, the authors reduce what they store.

- Instead of storing the full quadtree, they only store the **perimeters** (borders) of the colored regions.
- **The Assumption:** They assume all shape boundaries are *monotonic* (always increasing or decreasing in the X or Y dimension).
- Under the monotonic assumption, the perimeter size is reduced to $O(\sqrt{N})$.
- With $C$ colors (outgoing edges) per node, the space per quadtree is $C \times \sqrt{N}$.
- **Total Claimed Space Complexity:** $O(N^{1.5})$.

> **Professor's Critique:** While mathematically it brings the complexity down to $O(N^{1.5})$, writing code to traverse perimeters instead of standard quadtree boxes is effectively impossible to implement in a production environment.

------

## Extending to K-Nearest Neighbor (KNN)

Solving the shortest path is not enough; the original problem was finding the nearest neighbor (e.g., closest restaurant) based on network distance, not Euclidean distance.

### Lambda Multipliers ($\lambda$)

To avoid running Dijkstra for KNN, the paper adds pre-computed boundary metrics to every quadtree box.

- The algorithm calculates the network distance and Euclidean (spatial) distance from the source to every point in a quadtree box.
- It calculates the ratio: $\frac{\text{Network Distance}}{\text{Euclidean Distance}}$.
- It stores the minimum ($\lambda^-$) and maximum ($\lambda^+$) ratio for that box.
- **Network Distance Estimate:** The true network distance is bounded by $[\lambda^- \times \text{Euclidean}, \lambda^+ \times \text{Euclidean}]$.
- **Pre-computation Cost:** Finding these exact bounds requires the exhaustive $O(N^3)$ all-pairs shortest path calculation they were supposedly avoiding.

### The KNN Search Algorithm

The algorithm assumes the query point falls exactly on a node. If you are on an edge between two nodes, you must run the algorithm twice (once for each adjacent node) and pick the shorter result.

- Maintain two queues: `L` (sorted by maximum possible network distance) and `Q` (sorted by minimum possible network distance).
- Define $D_k$ as the maximum network distance of your current $k$-th best candidate.
- Expand quadtree boxes to find objects where the minimum possible distance is less than $D_k$.
- **Collisions:** A collision occurs when the $[\min, \max]$ distance range of Candidate A overlaps with the $[\min, \max]$ range of Candidate B. You cannot know which is truly closer.
- **Refinement:** To resolve collisions, the algorithm uses the "Next Hop" quadtree. It takes one hop closer to the target candidate, fetches the new $\lambda$ bounds from that next node, and tightens the estimate.
- Refinement repeats iteratively until the ranges no longer overlap and a winner is clear.

------

## Professor's Core Critiques of the Paper

- **Weak Baselines:** The paper compared its performance against 5-year-old algorithms (INE/IER) instead of the actual state-of-the-art VN3 algorithm published in 2004.
- **Hidden Costs:** The authors completely ignored the massive computational cost required to calculate $\lambda^-$ and $\lambda^+$ for every cell in every quadtree.
- **Flawed Assumptions:** The assumption that network shortest-path regions form monotonic boundaries is unsubstantiated and likely false in real-world road networks.
- **Implementation Nightmare:** Storing and querying monotonic perimeters inside a quadtree structure is far too complex for any practical database system.
- **Static Edge Weights:** The entire pre-computation model relies on static edge weights. It completely breaks down if edge weights are variable (e.g., introducing live traffic data).



# 3/25 Lecture: Time-Dependent Spatial Networks & Routing

## 1. Context & Data Collection

The lecture marks a shift in the course from fundamental single-paper concepts to advanced, multi-paper research on **Time-Dependent Spatial Networks** (specifically traffic and routing).

### Why Traffic Routing Matters

- **Economic & Time Impact:** Congestion wastes massive amounts of time and money (historically a $600B opportunity).
- **Psychological Flow:** Modern navigation apps help improve the psychological perception of traffic flow by preparing drivers with estimated arrival times.

### Data Sources & Evolution

- **Loop Detectors (Historical Method):** Sensors placed under asphalt (e.g., at traffic lights, freeways).
  - **Metrics Collected:** Volume (number of cars) and Occupancy (time spent over the sensor).
  - **Derivations:** Can calculate vehicle speed assuming standard car lengths based on inductance drop-off times.
  - **The RIITS Project:** A real-world LA project aggregating heterogeneous stream data (XML format, 30-sec/1-min intervals) from different transit agencies using Microsoft StreamInsight and Oracle Spatial databases.
- **The Shift to GPS (Current Method):** Loop detectors became obsolete because fixing them requires costly asphalt excavation. Modern traffic data is now sourced much more cheaply from **GPS logs** (smartphones, navigation systems, connected cars like Teslas).

------

## 2. Distance Computation: Static vs. Time-Dependent

Finding the "closest" point depends entirely on the spatial definition.

- **Euclidean Distance:** Straight line distance.
- **Network Distance:** Shortest path constrained by the road network (ignoring traffic).
- **Time-Dependent Space:** The *fastest* path. The shortest network path is not always the fastest due to variable traffic congestion.

### The Time-Dependent Problem Formulation

- **Variables:** Given a road network graph where edge weights (travel times) change based on the time of day.
- **Start Time Dependency:** The duration to travel an edge depends entirely on the exact time you *arrive* at that edge, requiring a composite function of time.
- **Why Pre-computation Fails:** Unlike static routing, you cannot pre-compute optimal routes for every possible departure time. Calculating the "lower envelope" (the optimal path composite function over time) has been proven to have **super-polynomial complexity**—it requires too much storage and time to be feasible.

------

## 3. Shortest Path Routing Approaches

### Legacy Approaches

- **Static Routing:** Dijkstra and A-Star (A*) algorithms. A* uses a heuristic (like Euclidean distance) to focus the search toward the destination. To guarantee an optimal path, the A* heuristic must *never overestimate* the cost.
- **Dreyfus Algorithm:** A time-dependent variant of Dijkstra that keeps track of arrival times at each node to calculate dynamic edge weights. Problem: It expands in all directions, scanning too much of the network.

### Flawed Heuristics for Time-Dependent A*

To make Dreyfus directional (like A*), a time-based heuristic is needed.

1. **Naive Heuristic:** `Euclidean Distance / Max Speed Limit`.
   - *Flaw:* The bound is too loose. It underestimates the time by so much that the algorithm behaves almost exactly like standard Dreyfus, offering no performance gain.
2. **Landmark Approach:** Pre-calculate distances to fixed map "landmarks" and use the triangle inequality to estimate travel time.
   - *Flaws:* Triangle inequality doesn't strictly hold for time-dependent traffic. Landmark selection is arbitrary, and it requires massive storage (e.g., 63MB for California).

### The Proposed Solution: Network Partitioning

Instead of arbitrary landmarks, the professor's research team developed a highly efficient, tight heuristic method.

1. **Partitioning:** Divide the road network into non-overlapping regions based on road hierarchy (e.g., separate freeways from arterials).
2. **Border Points:** Identify the exact "border nodes" where traffic enters and exits partitions.
3. **Lower Bound Graph:** Create a static graph representing the network at *maximum possible speeds* (no traffic).
4. **Pre-computation:** Pre-compute and store only the minimum travel times between border nodes on this lower-bound graph.

- **Why it works:** It mimics real driving behavior (finding the fastest way to a freeway, traveling the freeway, and exiting).
- **Performance:** Unlocks incredibly tight bounds, slashing query times to under 50 milliseconds (from 1000+ ms) and requiring only 8.5MB of storage.

------

## 4. Time-Dependent Nearest Neighbor Search

**Goal:** Find the nearest Point of Interest (POI), like a gas station, based on *future* dynamic traffic conditions, not just current distance.

To solve this without excessive computation, the algorithm generates two extreme network graphs:

- **Upper Bound Graph:** Assumes the *slowest* historical traffic speeds.
- **Lower Bound Graph:** Assumes the *fastest* possible speeds (speed limit).

### Tight Cells vs. Loose Cells

The network is divided into "cells" around each POI using these two bounds:

- **Tight Cells:** Calculated by traveling *as slow as possible* (upper bound) to the target POI, and *as fast as possible* (lower bound) to all other POIs.
  - *Rule:* If a driver is inside a POI's tight cell, that POI is definitively the fastest destination, regardless of real-time traffic variations.
- **Loose Cells:** Calculated by traveling *as fast as possible* (lower bound) to the target POI, and *as slow as possible* (upper bound) to all others.
  - *Rule:* If a driver is outside a POI's loose cell, that POI can be safely eliminated as a candidate.
- **Query Processing:** * If in a tight cell $\rightarrow$ Route immediately.
  - If in an overlapping area of loose cells $\rightarrow$ Run the exact Dreyfus algorithm *only* on the 2-3 overlapping candidates, drastically reducing computation.
  - *Indexing:* These cells are efficiently indexed using Quad Trees (corrected from earlier use of R-Trees).

------

## 5. Traffic Forecasting & Real-World Application

### The Forecasting Problem

Current navigation systems often route based on traffic *right now*. True predictive routing requires knowing what the traffic will be when you actually reach a specific segment in the future.

### AI & Deep Learning Evolution

The research group evolved their forecasting methods over time:

1. **Time Series Analysis:** Treating traffic purely sequentially.
2. **Causal/Matrix Tensors:** Mapping correlations between different freeways (e.g., if the 110 is blocked, the 710 behaves similarly).
3. **Graph Neural Networks (GNNs):** In 2017, the team successfully applied deep learning (Diffusion Models for GNNs) to traffic forecasting. This paper became a massive benchmark in the field (5,000+ citations).

### Tech Transfer & Startup Experience

- The team attempted to commercialize "predictive path planning" to beat Google Maps, which relied too heavily on sending users into incoming traffic bottlenecks.
- Pivoted from B2C (consumer apps) to B2B (logistics routing for companies like FedEx) leading to an eventual acquisition.
- The ultimate output of the lab's research was the students themselves, who went on to lead major systems at Apple, Google Gemini, and secure tenured university positions.



# 3/30 Lecture: Data-Driven Traffic Routing & Reachability

## 1. Traffic Data Sources: Loop Detectors vs. GPS

The foundation of modern traffic calculation relies on how data is collected. There are two primary sources, each with distinct characteristics.

### Data Source Comparison

| **Feature**     | **Loop Detectors**                                           | **GPS / Navigation Data (e.g., Waze, Tesla)**                |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Nature** | Aggregate counts (how many cars pass a point).               | Individual vehicle trajectories (sequence of locations).     |
| **Coverage**    | Limited strictly to installation locations (usually freeways). | Ubiquitous; covers arterial streets and anywhere a device travels. |
| **Accuracy**    | High spatial accuracy (exact location known).                | Subject to GPS noise and coordinate errors.                  |
| **Privacy**     | High privacy (anonymous, aggregate data).                    | Low privacy (tracks individual movements).                   |
| **Measurement** | Calculates volume and average speed via interval counts.     | Requires temporal and spatial aggregation to estimate traffic speed. |

> **Key Takeaway:** The industry is moving away from expensive, maintenance-heavy loop detectors toward ubiquitous GPS data, which benefits from the "network effect" (more users = exponentially better traffic accuracy).

------

## 2. The Traditional Navigation Pipeline (The "Cheat" Method)

Companies like Google and Apple use a heavily engineered, computationally expensive pipeline to turn raw GPS data into route recommendations.

### Standard Pipeline Steps

1. **Data Collection & Cleaning:** Ingesting noisy GPS data.
2. **Map Matching:** Computationally heavy process (often using Markov models) to snap erratic GPS points to actual road network segments.
3. **Speed Calculation & Forecasting:** Predicting speeds for road segments.
4. **Snapshot Graph Creation:** Building static, weighted road graphs for specific time intervals (e.g., 10:00 AM, 10:10 AM).
5. **Shortest Path Calculation:** Running algorithms like Dijkstra or Contraction Hierarchies on these snapshots.

### The "Cheating" Flaw

Traditional apps do not use true time-dependent routing. They route you based on a static snapshot of traffic at your departure time. If a route takes 30 minutes, the traffic data used for the end of your trip is outdated by the time you arrive. This is why navigation apps constantly say "rerouting to a faster path"—they are correcting their initial, flawed predictions.

------

## 3. Direct Trajectory Routing (The "Hitchhiking" Idea)

To bypass the expensive traditional pipeline (specifically map matching and snapshot graphs), the professor proposes a direct data-driven approach.

**The Core Concept:** Imagine you are hitchhiking. You hop into a car (a historical GPS trajectory) going your way. When that car turns off your desired path, you immediately hop into another car in the same location that is heading toward your destination.

### The Spatial-Temporal Index Structure

Instead of a roadmap, this method requires a highly updatable index structure to manage raw trajectory data.

- **Spatial Index:** A geographic grid. When a GPS coordinate is received, it instantly falls into a specific grid cell.
- **Temporal Index:** Within each grid cell, timestamps are indexed (e.g., using a 1D B-tree).
- **Query Logic:** Find trajectories that passed through your current grid cell within a similar time window (e.g., +/- 10 minutes) on historical days to ensure traffic patterns match your current trip.

### Routing & Cost Calculations

You traverse the grid by choosing to either stay on your current historical trajectory or hop to a new one. This forms a graph where standard algorithms (like A*) can be applied.

- **Staying on Trajectory Cost:** Time difference between point A and point B on the same trajectory.
- **Trajectory Switch Penalty:** A constant penalty added when hopping to a different trajectory in the same grid cell. This encourages route continuity and prevents chaotic zigzagging between historical trips.
- **Continuity Reward:** A reward (leveling off exponentially) applied to penalize over-switching and reward staying on a continuous, proven path.

### The Fallback Mechanism (New/Empty Roads)

What if you route into a grid cell with no historical GPS trajectories?

- **Solution:** Treat the underlying static road network as a permanent trajectory.
- **Road Cost:** Segment distance divided by the speed limit.
- **Road Penalty:** Speed limits assume zero traffic, no stoplights, and no turns. Therefore, a data-dependent penalty must be added to road costs so the algorithm doesn't default to empty roads just because they mathematically look faster than real, traffic-heavy trajectories.

------

## 4. Reachability & Isochrone Maps

Instead of going from Point A to Point B, urban planners and emergency services ask: "Where can I get to from Point A in 8 minutes?"

### Query Types

- **Reachability (Single Source):** Given a starting location and a time duration (e.g., 5 minutes), what is the coverage area?
- **Reverse Reachability (Single Target):** If an accident happens at a specific location, which hospitals can reach that point in 8 minutes?

### Direct Trajectory Solution

Using the same Spatial-Temporal Index, this problem becomes computationally simple:

1. Identify the starting grid cell and the departure time.
2. Find all historical trajectories that intersected that cell at that time.
3. Track those exact trajectories forward by the time limit (e.g., 5 minutes).
4. The endpoint grid cells dictate the reachability coverage.

### Visualization Methods

- **Convex Hull (Polygons):** Draws a boundary around all reachable endpoint coordinates. Easy to read, standard for Isochrone maps.
- **Grid Cells:** Highlights the specific spatial cells reached.
- **Buffers (Roads):** Renders the actual roads traveled to reach the limits. Slower to compute and render, but highly interpretable for real-world navigation.



# 4/1 Lecture

## Introduction to Spatial Crowdsourcing

Unlike traditional crowdsourcing (e.g., Amazon Mechanical Turk) where tasks can be done anywhere, **spatial crowdsourcing** requires a worker to be at a specific location at a specific time.

- **Enabling Technologies:** The rise of spatial crowdsourcing was driven by the convergence of advanced smartphones (GPS, accelerometers), high-quality mobile cameras, and improved mobile network bandwidth (3G/4G).
- **MediaQ Project (Early Example):** A system developed around 2011 that tracked not just GPS location, but the exact "field of view" of a mobile camera to verify if a user actually captured the requested task area.

------

## Paper 1: Task Assignment (Server-Assigned Tasks)

This paper focuses on how a central server matches $M$ spatial tasks to $K$ workers.

- **Core Problem:** Maximize the total number of assigned tasks over time, constrained by the workers' maximum task capacity and their localized working regions.
- **The "Clairvoyant" Challenge:** Because the system operates in real-time (online), future tasks and worker availability are unknown. An optimal assignment right now might be a poor decision long-term.
- **Greedy Strategy (Single Time Interval):** For an isolated moment in time, assignment can be solved optimally by modeling it as a **Bipartite Graph** and using a Max Flow algorithm (like Ford-Fulkerson). It connects workers to tasks they can geographically reach, capped by their task limit.
- **Location Entropy Priority (LEP) Strategy:** Outperforms the greedy strategy by 36% by prioritizing tasks in *low-entropy* locations. Low entropy means an area is rarely visited by diverse workers. If a task pops up there, it must be assigned immediately, whereas tasks in highly trafficked (high entropy) areas can wait for future workers.

------

## Paper 2: Task Scheduling (Worker-Selected Tasks)

This paper shifts the decision-making: the server broadcasts tasks, and individual workers select and schedule their own tasks.

- **Core Problem:** Given a worker's location and a set of tasks with locations and expiration deadlines, find the optimal sequence of tasks to maximize completion. This is an NP-hard problem.
- **Distance Metric:** The system assumes Manhattan distance for travel time calculations.

**Scheduling Algorithms Comparison**

| **Algorithm**                   | **Type**    | **Complexity**                                  | **Key Characteristics**                                      |
| ------------------------------- | ----------- | ----------------------------------------------- | ------------------------------------------------------------ |
| **Dynamic Programming**         | Exact       | $O(N^2 \cdot 2^N)$ time, $O(N \cdot 2^N)$ space | Solves subproblems recursively; very memory intensive.       |
| **Branch and Bound**            | Exact       | $O(N!)$ worst-case time                         | Prunes the search tree by calculating upper bounds; drops branches that cannot beat the current max reward. Extremely fast in practice despite worst-case complexity. |
| **Heuristics (Greedy/Nearest)** | Approximate | $O(N \log N)$ or $O(N^2)$ time                  | Selects closest task or least expiration time. Highly scalable but yields sub-optimal task volume. |
| **Progressive**                 | Hybrid      | Variable                                        | Uses a fast heuristic for the very first task to ensure a quick app response, then runs an optimal algorithm (like Branch and Bound) for the remaining route while the worker is traveling. |

------

## Paper 3: Combining Assignment and Scheduling

Real-world systems require both server-side global assignment and worker-side local scheduling.

- **Global Assignment & Local Scheduling (GALS):** The server assigns tasks globally, and workers schedule them locally. This requires an iterative feedback loop to fix scheduling conflicts (e.g., when a task is assigned to a worker who ends up unable to schedule it before expiration).
- **The Scaling Bottleneck:** Running GALS on massive flow networks (e.g., 25,000 tasks, 500K edges) is computationally heavy and too slow for real-time applications.
- **Naive Local Assignment (Naive LALS):** Spatially partitions the map and runs GALS on smaller clusters in parallel. However, this creates unbalanced workloads and leaves a large "residual" pool of border tasks.
- **Bisection-Based LALS:** Uses a top-down bisection method to create equally sized partitions and a bottom-up merge to handle residual tasks. This method is an order of magnitude faster than GALS while sacrificing less than 5% in schedule quality.

------

## Paper 4: Real-World Ride-Sharing (Auction-Based)

This paper scales spatial crowdsourcing to handle modern ride-sharing (e.g., UberPool) involving millions of concurrent users.

- **Core Problem:** The system must balance driver deviation limits, rider wait times, delays to existing passengers, and real-time traffic conditions.
- **Traditional Failure:** Standard Operations Research approaches (like "dial-a-ride") fail because they require all data in advance and take hours/days to compute.
- **The Auction Solution:** 1. A rider requests a trip.
  2. The server broadcasts the request to nearby drivers.
  3. Each driver's mobile app *locally* computes the detour time, traffic delays, and personal willingness to deviate.
  4. The driver's app submits a "bid" (price/time) to the server.
  5. The server simply ranks the bids and assigns the ride to the winner.
- **System Advantages:** Inherently handles dynamic availability (if a driver logs off, they simply don't bid), utilizes distributed computing power (calculations happen on the phones, not the server), and achieves sub-300 millisecond response times.



# 4/6 Lecture

------

### **Administrative Notes**

- **Final Exam:** April 29th.
- **Homework 3:** Due May 11th. No late days allowed due to a tight grading schedule. (The May 11th date is strictly for HW3, not an exam).

------

## **Topic: Spatial-Temporal Forecasting**

### **1. Spatiotemporal Data Fundamentals**

- **Definition:** Data that provides information about *where* (spatial) and *when* (temporal) an event happens.
- **Examples:** Traffic data (cars past an intersection over 30s), air quality, electricity consumption, seizure activity in the brain.
- **Key Characteristics:**
  - Massive amounts of high-frequency data.
  - Contains complex underlying patterns across both space and time.
  - Critical for decision-making (e.g., urban planning, predicting busy times on Google Maps).
- **Forecasting Goal:** Given a historical window of observations (length $W$), predict future values for a specific horizon (length $H$).

### **2. Modeling the Temporal Dimension**

- **Time Series:** A sequence of observations ordered by time.
  - **Multivariate Time Series:** Multiple sequences where the future value of one variable depends on its *own* past values AND the past values of *other* variables.
- **Requirements for Sequential Modeling:**
  - Handle variable-length sequences.
  - Maintain chronological order.
  - Track long-term dependencies (e.g., daily/weekly seasonality).
  - Share parameters across the entire sequence for consistency.

#### **Recurrent Neural Networks (RNNs)**

- **Mechanism:** Uses a loopback feed. Maintains a hidden/cell state ($h_t$) to track past observations.
- **Process:** $h_t$ is updated at every time step using the previous state ($h_{t-1}$) and current observation ($x_t$), transformed by a shared weight matrix ($W$).
- **The Flaw (Vanishing/Exploding Gradients):** During backpropagation over long sequences, gradients are multiplied many times. They either explode (overflow) or vanish to zero.
  - *Band-aid fixes:* Gradient clipping (capping max values) or using ReLU activations.
  - *Architectural fix:* Gated RNNs.

#### **Gated Recurrent Units (GRUs)**

- **Mechanism:** Uses "gates" to control how much information flows through the hidden state, preventing gradient issues.
- **Update Gate ($z_t$):** Controls which parts of the previous hidden state to keep and which to update.
- **Reset Gate ($r_t$):** Controls which parts of the previous hidden state to discard when computing new content.
- **Execution:** Computes a new candidate hidden state ($\tilde{h}_t$) and applies element-wise multiplication with the gates to finalize the current hidden state ($h_t$).

------

### **3. Modeling the Spatial Dimension (Graphs & GNNs)**

- **The Problem with treating Spatial Data purely as Time Series:** "Missed Inductive Bias." Feeding traffic data purely into a GRU discards critical spatial relationships (how roads connect and influence each other).

#### **Graph Neural Networks (GNNs)**

- **Components of a Graph:** Nodes (entities like sensors/roads) and Edges (relationships represented by an adjacency matrix).
- **Message Passing:** Nodes are informed of their local neighborhood to capture spatial dependencies.
  - **Message Function:** Transforms the features of a node.
  - **Aggregation Function:** Aggregates messages from neighbors (e.g., taking the mean).
  - **Update Function:** Updates the node's state using its own info and aggregated neighbor info.
- **Multi-hop layers:** 1 layer = immediate neighbors. 2 layers = two-hop neighbors.
- **Over-smoothing Hazard:** Doing message passing too many times causes all nodes to converge to the identical embedding, destroying node-level information. Keep graphs sparse.

#### **Comparisons:**

- **GNN vs. CNN:** CNNs assume a fixed, regular grid (position matters). GNNs handle irregular, general structures (permutation invariant).
- **GNN vs. Transformer:** Transformers act like a fully-connected graph learning attention weights on the fly. GNNs usually rely on predefined structural weights (like physical road distance) and multi-hop layers.

------

### **4. System 1: DCRNN (Diffusion Convolutional Recurrent Neural Network)**

- **Challenges Addressed:**
  - *Non-Euclidean Dependencies:* Roads physically close (opposite sides of a highway) may have entirely different traffic patterns.
  - *Non-linear Temporal Dynamics:* Traffic statistics change drastically over time.
  - *Long-horizon Prediction:* Errors compound over long predictions.
- **Graph Construction:** Builds a static graph based on **road-network distance** (not straight-line Euclidean). Connection weight is proportional to the inverse or exponential of distance. Edges below a threshold are cut to keep the graph sparse.
- **Diffusion Convolution:** Replaces standard matrix multiplication. Diffuses messages bidirectionally (using in-degree and out-degree matrices) to $K$-hop neighbors at each step.
- **Architecture:** Encoder-Decoder setup. Uses a DCGRU (a GRU modified with diffusion convolution).
  - *Teacher Forcing:* During decoding, ground truth values are sometimes substituted for predicted values to prevent small errors from compounding over time.

------

### **5. System 2: BSGN (Busyness Graph Neural Network)**

- **Limitation of DCRNN:** Assumes relationships between nodes are fixed. Real-world correlations are dynamic (e.g., a commercial road and residential road act similarly on weekdays but differently on weekends).
- **Goal:** Build a better, dynamic graph (the "Business Graph") rather than relying on complex message passing.
- **Multi-Context Correlations:**
  1. **Temporal:** Do two roads historically share similar traffic patterns? (Extracted via GRU with self-attention).
  2. **Semantic:** Do the roads share physical attributes? (e.g., speed limit, lanes). Attributes are converted to text and embedded using a pre-trained LLM, then compared via Cosine Similarity.
  3. **Spatial:** Geographic connectivity and road network distance.
  4. **Taxonomic:** High-level patterns between aggregated areas (e.g., grouping all sensors in a "stadium neighborhood" vs a "business district").
- **Graph Generation:**
  - Takes a weighted average of Spatial and Semantic similarities (Long-term relationships).
  - Uses Temporal similarity as a *gate* to adjust the combined score (Short-term/noisy relationships).
  - **Case Amplification:** To threshold the graph and keep it sparse, similarity scores (0 to 1) are raised to a power (e.g., $x^3$). This safely crushes smaller, noisy values closer to zero without heavily impacting strong connections.
- **Outcome:** Once this dynamic graph is built, BSGN achieves state-of-the-art results using very simple message passing, proving that a high-quality graph representation is more important than complex message passing algorithms.

------

### **6. Evaluation Metrics for Forecasting**

Because forecasting is a multi-node regression task, standard metrics include:

- **MAE (Mean Absolute Error):** The average absolute distance between predicted values and ground truth.
- **MAPE (Mean Absolute Percentage Error):** The MAE represented as a percentage.
- **RMSE (Root Mean Squared Error):** The square root of the average squared differences (penalizes larger errors more heavily).



# 4/8 Lecture

## Geo-Social Networks Lecture Cheat Sheet

> **Definition:** A geo-social network combines virtual social connections (graphs of people) with physical geographical data (locations and positioning). It powers queries like "find nearby friends."

### Architecture & Primitives

Early research proposed a Query Processing Module sitting between a separate **Social Module** and a **Geographical Module**.

**Pros of this Architecture:**

- Modules can be administered independently by different companies.
- Easy to integrate new underlying data structures (e.g., switching to a Quad-tree) without breaking the query layer.
- Highly flexible for creating new geo-social queries using basic primitives.

**Technical & Business Impediments:**

- **Technical:** Difficult to join data securely across separate entities without leaking unique IDs or inferring the other module's dataset.
- **Business:** Companies monetize their data; there is no incentive to share half of a data set with a competitor just to support a query.

**Atomic Primitives (Stateless Operations):**

- **Social:** `getFriends(U)`, `areFriends(Ui, Uj)`, `getDegree(U)`
- **Geographical:** `getUserLocation(U)`, `range(Q, R)` (find users within range $R$ of point $Q$), `nearestUsers(Q, K)` (find $K$ nearest neighbors to point $Q$)

------

### Query Execution Strategies

When combining primitives for a query like "Find friends of user U within range R of coffee shop Q," there are three main execution approaches:

| **Approach**          | **Methodology**                                              | **Best Used When...**                                      | **Disadvantages**                                            |
| --------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- | ------------------------------------------------------------ |
| **Social First**      | Find all friends of U $\rightarrow$ check if their locations fall within range R. | The user has a small number of friends (low degree).       | Very inefficient for dense social networks with thousands of friends. |
| **Spatial First**     | Find all users in range R $\rightarrow$ check if they are friends with U. | The geographic range is very small and sparsely populated. | Highly inefficient in dense, popular areas with thousands of check-ins. |
| **Serena's Approach** | Independently get all friends AND all users in range $\rightarrow$ find the intersection. | The underlying modules are optimized for bulk retrieval.   | Fails completely if both the friend list and the location check-ins are massive. |

------

### Nearest Star Group (NSG) Query

**Goal:** Find a group of $M$ socially connected users that minimizes the aggregate distance to a query point $Q$ (e.g., "Find 5 friends closest to this restaurant").

**Star Formation:** The group does not need to be fully connected. At least one user must be friends with the other $M-1$ users.

**NSG Algorithms:**

- **Eager:** A greedy heuristic. Finds the absolute nearest user to $Q$, builds a star with their closest friends, and uses that sum as the current "seen" budget/upper bound. It calculates a best-case "unseen" lower bound and loops until the unseen bound exceeds the current best.
- **Lazy:** Similar to Eager, but calculates the unseen budget using any visited users without strictly verifying their friendship status first. It generates a looser bound, requiring more loops but potentially less strict social querying upfront.
- **EagerStar:** Uses a highly aggressive calculation for the unseen bound. It loops fewer times but the initial result might not be perfectly accurate, requiring a secondary refinement step.

------

### Inferring Social Connections from Real-World Data

The core assumption validated by social scientists is that physical co-occurrences (two people in the same place at the same time) strongly imply a social connection.

**Challenges in Measurement:**

- **Richness/Diversity:** Meeting in many different locations implies a stronger bond than meeting in just one.
- **Frequency:** Meeting 10 times is a stronger signal than meeting once.
- **Coincidences:** Regular overlap at a specific time (e.g., Tuesday mornings at a coffee shop) might just be strangers with similar routines.
- **Location Popularity (Semantics):** Co-occurring at an unpopular, niche location is a much stronger signal of friendship than co-occurring at the Eiffel Tower.

**Mathematical Approaches to Co-occurrence:**

- **Shannon Entropy:** Captures both frequency and diversity. Calculated using the probability of a co-occurrence at a location: $p \times \ln(p)$. High entropy means low predictability, indicating the pair meets in highly diverse locations.
- **Rényi Entropy:** Adds a tuning parameter (order of diversity $q$) to control the weight of frequency versus diversity. Setting $q < 1$ gives more weight to low-frequency meetings, effectively filtering out high-frequency coincidences (like a shared daily commute).
- **Location Entropy:** Measures the popularity of a specific location independent of specific user pairs. High location entropy means a very diverse set of people visit it (e.g., highly popular tourist spots).
- **The Combined Model:** Weights Rényi entropy (co-occurrences) against Location entropy (popularity). This approach successfully handles data sparseness; even a single co-occurrence in a highly unpopular location yields a strong probability of friendship.

------

### Real-Time Multi-Criteria Social Graph Partitioning (RMGP)

**Goal:** Distribute a group of socially connected users to a set of locations (e.g., three different clubs) generated on the fly.

**Objectives:** Minimize travel distance AND minimize the loss of social connectivity (keep friends together).

**The Game Theoretic Solution:**

- **Initialization:** Users are assigned to locations completely at random.
- **Agent Behavior:** Each user acts selfishly to optimize their personal objective function (distance + keeping their specific friends).
- **Iteration:** Users "move" virtually to better locations based on where their friends are and how far the drive is.
- **Resolution:** The system eventually reaches a **Nash Equilibrium**, a state where no single user can improve their personal score by moving. The worst-case equilibrium is mathematically bounded to prevent terrible routing.

------

### The Two Sides of Geo-Privacy

When users interact with service providers, there is a fundamental tension in what data is shared versus what is inferred:

- **Scenario A (Navigation):** You willingly share your exact location to get driving directions, but you do *not* want the provider inferring your social network based on who you park next to.
- **Scenario B (Contact Tracing):** You willingly share your social/contact graph (who you stood near) to know if you were exposed to an illness, but you do *not* want the provider tracking the specific geographic locations you visited.



## 4/13 Lecture: Spatial Data Privacy: An Overview

**Context & Motivation**

- Location-based services (Uber, Google Maps) require users to share their location.
- **The Threat:** Unsecured connections, hacked servers, or companies monetizing/selling location data to third parties.
- **Why Pseudo-IDs Fail:** Hiding a user's explicit ID is insufficient. Knowing just 4 location points (e.g., where someone sleeps and works) is enough to identify 90% of people.
- **Sensitive Inferences:** Location data reveals religion (visiting a church), health conditions (visiting a cancer clinic), and real-world social networks (who you hang out with).

------

## 1. The Online Setting

Users are interacting with a location-based server they do not trust. There are two main architectures to handle this: the **Third-Party Architecture** and the **Client-Server Architecture**.

### Architecture A: Third-Party (The Anonymizer)

Users trust a middleman (anonymizer) to cloak their data before sending it to the untrusted server.

**Core Concept: K-Anonymity & Cloaking**

- **K-Anonymity:** A user's query must be indistinguishable from at least $K-1$ other users.
- **Cloaked Region (ASR):** Instead of exact coordinates, the user sends an "Anonymous Spatial Region" (e.g., a zip code or bounding box).
- **Trivial Solution 1 (Nearest Neighbors):** Find $K-1$ nearest people and send a query for all $K$.
  - *Flaw:* If all $K$ people are in the exact same room, the server still knows exactly where you are. It also overloads the server.
- **Trivial Solution 2 (Fixed Region):** User defines a fixed comfort area to report.
  - *Flaw:* If the user is in a sparse area (like a desert) with no one else around, they are the only logical sender.

**Hybrid Solutions**

- **Quad-tree Spatial Cloaking:** * Partitions space using a quad-tree.
  - Keeps dividing until a quadrant contains fewer than $K$ users.
  - It then steps back to the parent quadrant and uses that as the cloaked region.
- **Nearest Neighbor K-Anonymizer:**
  - Finds the user's $K-1$ nearest neighbors.
  - *Randomly selects* one user from that group and finds *their* $K-1$ nearest neighbors.
  - Creates a Minimum Bounding Rectangle (MBR) around this new group plus the original user. This ensures the user is not dead-center in the box.

**Handling Different K-Requirements (Personalized Privacy)**

What if User A wants $K=10$ but User B wants $K=2$?

- **Clique Cloak:** Connect users in a graph if they fall within each other's maximum acceptable cloak area. When a new user joins with a specific $K$, they connect to neighbors with a requirement $\leq K$ (to help those with stricter needs). The resulting "clique" shares the exact same MBR, confusing the server.
- **Hilbert Curve Cloaking:** * Pass a 1D Hilbert curve through 2D space to rank users (e.g., 0, 1, 2, 3).
  - Group users into rigid chunks based on a modulo operation (`Rank mod K`).
  - Users in the same chunk report the exact same start and end bounds, ensuring indistinguishability.

**The Trajectory Problem (Moving Users)**

- If a user sends queries over time, the server can track the intersection of their cloaked boxes. Over time, the other $K-1$ users will leave the box, isolating the target.
- *Fix:* Expand the box to always include the original $K$ users. *Trade-off:* This severely degrades utility/accuracy.

### Architecture B: Client-Server (Perturbation)

Users communicate directly with the server but add "noise" to their location.

- **Landmark Approach:** Create Voronoi diagrams around landmarks. Instead of your exact location, report the nearest landmark (e.g., report the Eiffel Tower and walk there when your Uber arrives).

**Geo-Indistinguishability (Differential Privacy for Location)**

A formal, mathematical approach to perturbation guaranteeing that a server cannot confidently distinguish between two nearby starting locations.

- **The Rule:** The probability of a mechanism generating noisy location $Z$ from true location $X$, compared to generating $Z$ from a nearby location $X'$, is bounded by distance and an $\epsilon$ privacy budget.
- **Epsilon ($\epsilon$) Privacy Budget:**
  - **Higher $\epsilon$:** Less privacy, pointier distribution (reported location is very close to true location). Higher utility.
  - **Lower $\epsilon$:** Higher privacy, fatter distribution (reported location could be far away). Lower utility.
- **Planar Laplace Mechanism:** Uses a 2D Laplace distribution to add noise. (Implementation note: must convert to polar coordinates to sample the radius and angle correctly; do not just sample $X$ and $Y$ independently).
- **Problems in Practice:** 1.  *Utility Loss:* Blindly adding math noise might put you in the middle of a river where no user could logically be.
  2. *Trajectories:* To maintain privacy over $N$ queries, the privacy budget multiplies ($N\epsilon$), rapidly degrading privacy guarantees over time.

------

## 2. The Offline Setting

Users trust the server (e.g., Google) to collect data, but the server wants to release aggregate models or histograms to the public without leaking user data (preventing Membership Inference Attacks).

**Differentially Private Histograms**

- The goal is to answer Range Count queries (e.g., "How many people are in this grid cell?") safely.
- To do this, servers add Laplace noise to the raw counts of a 2D grid.

**The Utility Challenge**

- A basic grid assumes data is uniformly distributed, which causes errors when queries only cover a fraction of a cell.
- Past research used complex KD-trees or Quad-trees to partition data based on density, but the tree structure itself could leak privacy.

**The Neural Network Solution (SNH / NeuroSketch)**

A modern approach to fixing noisy DP histograms without complex partitioning.

1. **Generate Noisy Data:** Create a basic 2D grid and add DP noise to every cell. (This data is fully private).
2. **Train a Model:** Train a small Neural Network (like a Multi-Layer Perceptron) to answer range queries *using only the noisy data as the ground truth*.
3. **The Result:** Querying the trained model yields a **more accurate** answer than querying the noisy histogram it was trained on.
4. **Why it works:** The neural network is kept deliberately small. It lacks the capacity to memorize the high-frequency random DP noise. Instead, it acts as a denoiser, learning only the underlying spatial patterns and distributions.

**Applying to Time-Series Data**

- For data that changes over time (e.g., foot traffic at 8 AM vs. 9 AM), the model uses **CNNs** (Convolutional Neural Networks) and **VAEs** (Variational Autoencoders).
- The CNN processes each time slice, and the VAE compresses it into a small embedding $Z$ before reconstructing it.
- The compression forces the model to learn the true spatial patterns while dropping the noise, resulting in highly accurate, fully private aggregate data releases.



# 4/15 Lecture Notes: Advanced Location Privacy & Spatial Crowdsourcing

## Part 1: Privacy-Preserving Task Assignment in Spatial Crowdsourcing

**Context:** Moving beyond simple location privacy (like range queries) to complex operations like task assignment (e.g., matching Uber drivers to riders) where both parties want to keep their exact locations private from the central server.

### Problem Definition & Threat Model

- **Goal:** Assign tasks (riders, $T$) to workers (drivers, $W$) in an online setting (tasks arrive dynamically and must be assigned immediately).
- **Challenge:** The server (Uber) traditionally needs exact locations of $W$ and $T$ to optimize dispatching. How can we do this if users submit "fake" (perturbed) locations?
- **Previous Work:** Mostly focused on hiding the worker's location. This approach hides **both** worker ($W$) and task ($T$) locations from the server.

### Core Privacy Concept: $\epsilon, R$-Geo-Indistinguishability

- An extension of standard $\epsilon$-geo-indistinguishability.
- **Parameters:**
  - **$\epsilon$ (Privacy Budget):** Determines the amount of noise added. Higher $\epsilon$ = less privacy.
  - **$R$ (Radius of Concern):** The distance within which privacy is guaranteed. Outside of distance $R$, the user does not care if their location is distinguishable.
- **Mechanism:** Users add noise to their true location sampled from a Planar Laplace distribution to generate a fake location ($W'$ or $T'$).

### The 3-Step Privacy Framework

Because the server only sees fake locations ($W', T'$), standard assignment algorithms fail (resulting in high travel costs or false hits where a driver is too far away). The proposed solution uses a 3-step decentralized negotiation:

1. **Server Candidate Selection:** Task $T$ requests a ride. The server uses fake locations ($W', T'$) to find a *superset* of candidate drivers and sends this list to $T$.
2. **Rider Selection:** Task $T$ (knowing their true location) evaluates the candidate list based on the drivers' fake locations ($W'$). $T$ picks the best driver and reveals their true location to that specific driver.
3. **Driver Acceptance/Rejection:** The chosen driver $W$ (knowing their true location) checks if $T$'s true location is within their reachable distance ($R_W$).
   - *Accept:* Match is made.
   - *Reject:* Privacy leak occurs ($T$'s location was revealed to a driver who didn't pick them up). $T$ must pick the next candidate.

### The Probabilistic Algorithm

To minimize privacy leaks and maximize utility, the system shouldn't blindly trust the fake locations (the "oblivious" approach). Instead, it reverse-engineers the probabilities.

- **The Math:** We know fake locations are generated via Planar Laplace noise. To simplify the math for reverse engineering, this is approximated using a **Bivariate Normal Distribution** (with zero covariance/independent variables to ensure circular symmetry).
- **Distance Estimation:** The distance between the true locations is modeled using a **Rice Distribution**.
  - *Server side:* Calculates the Probability Density Function (PDF) of the distance between true $W$ and true $T$ given fake $W'$ and fake $T'$. Filters candidates using threshold $\alpha$.
  - *Rider side:* Calculates the PDF of the distance between true $W$ and true $T$ given fake $W'$ and true $T$. Ranks drivers using threshold $\beta$.
- **Results:** At $\epsilon = 0.4$, the Probabilistic approach achieves almost the same utility (assigned tasks and travel cost) as the ground truth (knowing all locations), while reducing privacy leaks (false hits) from an average of 23 down to just 1.

------

## Part 2: Inferring Social Relationships from Location (Attack & Defense)

**Context:** If you know where people go, you can figure out who they hang out with. Originally viewed as a marketing tool (2008), this is now recognized as a privacy attack (2017).

### The Attack Model (2017 CCS Paper)

- **Goal:** Infer social links from mobility profiles (co-locations).
- **Mechanism:** Inspired by NLP (Word2Vec/Skip-gram).
  - Treats location movement sequences as "sentences" and User/Location IDs as "words".
  - Uses a neural network to generate vector embeddings for users.
  - Users with similar embeddings (high cosine similarity) are flagged as socially related (friends).

### The Defense: Hiding Co-Locations

If you can hide the basic primitive—a co-location—you break the attack. A co-location is defined by a spatial threshold ($\Delta S$) and temporal threshold ($\Delta T$).

- **The Trade-off:** Perturbing check-in data to hide co-locations introduces utility loss for legitimate Location-Based Services (LBS).
- **Metrics:**
  - *Utility Loss:* Spatial and temporal displacement of the perturbed check-in vs. the real check-in.
  - *Privacy Metric:* The drop in the attacker's inference accuracy.

### Comparison of Defense Techniques

1. **Gaussian Perturbation (Baseline):**
   - *How it works:* Adds 1D Gaussian noise to coordinates.
   - *Flaw:* Fails because co-location density is skewed. If you tune the noise for dense areas (city centers), it fails to protect users in sparse areas. If you tune it for sparse areas, it ruins LBS utility everywhere else.
2. **Adaptive $B$:**
   - *How it works:* Finds $B$ nearest check-ins to a co-location. Moves one of the co-located users to one of those $B$ locations uniformly at random.
   - *Pros:* Breaks the exact co-location with minimal distance displacement, preserving LBS utility well.
3. **K-Anonymity (for Co-locations):**
   - *How it works:* Instead of moving a co-located person away, it moves a nearby bystander *into* the co-location spot.
   - *Pros:* Highly efficient scaling. If 3 people are at a location, moving 1 more person in creates $C(4,2) = 6$ possible pairs, raising $k$ from 3 to 6 instantly. The server cannot guess which pair is the true social link.



# 4/20 Lecture Cheatsheet: Spatial Data Research & Mobility Analytics

## I. Course & Exam Administration

- **Course Phase:** Part 3 of the course focuses on current research in spatial data. It is fast-paced by design.
- **Learning Goal:** You are not expected to become an expert in machine learning or privacy. The goal is to understand the **current state of research**, unique challenges applied to spatial data, and high-level abstractions.
- **Exam Expectations:** 
  - Focus on conceptual understanding and problem-solving rather than memorizing dense formulas.
  - Expect to explain concepts rather than write long essays.
  - Rough curve: 50% of the exam should be answerable by everyone, the next 25% differentiates the middle, and the final 25% differentiates the top.

## II. Context: The Shift to Mobility Data

- **Evolution of the Field:** Euclidean Space $\rightarrow$ Road Networks $\rightarrow$ Real Traffic Data $\rightarrow$ Spatial Crowdsourcing/Privacy $\rightarrow$ **Mobility Data (GPS Trajectories)**.
- **Data Availability:** Industry releases GPS/mobility data. When traditional deep learning models fail to capture the nuances of spatial data, new research opportunities emerge (often published in SIGSPATIAL or ML conferences like ICML/ICLR).
- **Definition:** A trajectory is a sequence of latitude, longitude, and timestamp coordinates representing a moving object.

------

## III. Topic 1: Mobility Behavior Clustering

**Goal:** Group trajectories based on the *reason* for movement (e.g., commute, shopping, exercising) without manual human labeling, allowing for easier downstream classification.

### The Naive Approach & Its Failures

- **Idea:** Treat trajectories as time series and use Dynamic Time Warping (DTW) to measure similarity, then apply K-Means clustering.
- **Problem 1 (Multi-Scale Similarity):** The same behavior (e.g., a "commute") can look vastly different spatially and temporally. A 14-mile commute takes 50 minutes in traffic, 15 minutes without traffic, or 50 minutes on a bike covering a totally different distance. Shape-based distances fail here.
- **Problem 2 (Context Ignorance):** Moving behavior is determined by the *Places of Interest (POIs)* visited (e.g., home $\rightarrow$ coffee shop $\rightarrow$ work), not just the physical shape of the route.

### Paper 1: Two-Phase Context Clustering

- **Step 1: Context Extraction**
  - Find **Stay Points**: Locations where a user spends a significant amount of time (not just stuck in traffic).
  - Convert stay points into **Context Vectors**: Instead of identifying an exact POI (which is hard due to GPS inaccuracy), calculate the percentage of POI categories (e.g., 6% coffee shops, 20% residential) in a radius.
  - Trajectories become variable-length sequences of POI vectors.
- **Step 2: Sequence Embedding (RNN)**
  - Pass the sequence through an **RNN (Recurrent Neural Network)**.
  - Use self-supervised training to optimize for *reconstruction* (predicting the sequence). This outputs a fixed-size embedding.
- **Step 3: Refined Clustering (KL Divergence)**
  - Embeddings built for *reconstruction* are messy for *clustering*.
  - Added a second loss function using **KL Divergence** to make the distribution "pointier" (high confidence).
  - *Result:* Successfully separated clusters and naturally identified hidden behaviors (e.g., morning park joggers).

### Paper 2: VAMBC (One-Shot VAE Clustering)

- **Problem with Paper 1:** Alternating between reconstruction loss and clustering loss in two phases is suboptimal.
- **Solution:** Use a **Variational Autoencoder (VAE)** combined with an LSTM (to prevent vanishing gradients).
- **Architecture:**
  - Encoder outputs two things:
    1. $Z$: A continuous variable (standard embedding).
    2. $Y$: A discrete categorical variable representing the cluster.
  - **Gumbel-Softmax Trick:** Used to make the discrete cluster variable $Y$ differentiable so backpropagation can tune the clustering simultaneously with reconstruction.
  - *Result:* A one-shot model that is highly accurate for both reconstruction and cleanly separating behavioral clusters.

------

## IV. Topic 2: Synthetic Trajectory Generation

**Goal:** Take a small sample of real mobility data and generate a massive, realistic synthetic dataset for industry use, avoiding manual, human-tuned simulators like MATSim.

### Grid Representation & Base Model

- **Discretization:** The world is converted into a grid. A trajectory becomes a sequence of Grid IDs at fixed time intervals (e.g., every 5 minutes).
- **Base Model (SeqGAN):** * A Generative Adversarial Network tailored for sequences.
  - **Generator:** Makes the next "move" (like chess).
  - **Discriminator:** Tries to classify the trajectory as real or fake.
  - **Monte Carlo Search:** Used because you cannot evaluate a trajectory's realism until the entire sequence is complete.

### Paper 3: CSGAN (Modality-Aware Generation)

- **Problem with standard SeqGAN:** It ignores the *diversity* of modalities (walking vs. biking vs. driving). If it trains on diverse data, it might only output the most common modality.
- **Naive Fix (Fails):** Cluster the data first, then run a separate SeqGAN on each cluster. This fails because it prevents the models from learning shared sequential movement patterns across different modalities.
- **CSGAN Approach:**
  - Modify the Discriminator to classify into $K+1$ classes ($K$ real modalities + $1$ fake class).
  - The Generator is rewarded if it successfully fools the Discriminator into categorizing its output into *any* of the valid $K$ modalities.
  - *Key Finding:* Forcing the model to learn diversity actually **improved overall accuracy** (transition probabilities and spatial distributions).

### Paper 4: Context-Aware Generation (MPGail / Epicell)

- **Idea:** Expand CSGAN by including POI context, not just modality.
- **Contextual Grids:** Each grid cell is labeled with its majority POI type (e.g., business cell, residential cell).
- **Macro-Micro Model:** Treats trajectory generation like state transitions.
  1. **Context Transition:** Predicts the *type* of cell the person will go to next (e.g., moving from residential to business).
  2. **Location Prediction:** Standard GAN predicting the exact next grid cell.
  3. **Spatial Constraint:** Applies a Gaussian distribution around the current location to prevent unrealistic "teleportation" (borrowed from a model called MoveSim).
- **Dual Discriminators:** One discriminator verifies the validity of the *location* movements, while another verifies the validity of the *context* transitions.
- *Result:* State-of-the-art performance in both individual trajectory realism and aggregate distribution metrics.



# 4/22 Lecture: Geospatial Representation Learning & Location Encoding

**Lecturer:** Chen Chu (PhD Student, advised by Prof. Cyrus Shahabi)

**Core Topic:** Building the "wheels" (foundational models) for Geospatial AI.

> **Exam Hint:** The lecturer explicitly stated that midterm questions will focus on the **high-level ideas and intuitions** of *why* we need location encoding and *what* specific mathematical components achieve (e.g., granularity and direction), rather than asking you to memorize complex formulas.

------

## 1. Fundamentals of Representation Learning

Representation learning maps raw data (text, images, audio, etc.) into an $N$-dimensional mathematical feature space.

- **The Goal:** Enable deep learning models (MLPs, Transformers, CNNs) to directly use these feature vectors instead of struggling with raw, unstructured data.
- **Multimodality:** Modern AI merges different modalities (text, 3D signals, audio, geospatial coordinates) into a unified feature space so models can draw context from everything at once.

### Why Add Geospatial Data?

Location data provides critical context that standard features miss.

- **Example:** In an image classification task trying to distinguish an Arctic Fox from a Bat-eared Fox, visual features alone might struggle. However, if the model knows the image was taken in the Arctic versus South Africa (via embedded location data), it can easily make the correct prediction based on the spatial distribution of those species.

------

## 2. Point Data: The Foundation

Points are the easiest geospatial data type to model, requiring only $X$ and $Y$ coordinates. They are highly versatile; zooming out far enough allows even complex structures (like the USC campus or the city of Los Angeles) to be abstracted as a single point without losing relevant task data.

### The Problem with Raw Coordinates

Directly feeding raw $X$ and $Y$ coordinates into a machine learning model yields poor results because it lacks **inductive bias**.

- **Memorization over Generalization:** The model will only memorize specific coordinate-to-output mappings (e.g., "when $X = -10$, output 1"). It fails to understand broader spatial patterns, which is detrimental when trying to make predictions in regions with sparse data.
- **No Periodical Bias:** It cannot naturally learn that certain spatial phenomena repeat over distances.
- **No Frequency Awareness:** It cannot detect whether a spatial variation changes slowly or quickly.

### Injecting Inductive Bias using Location Encoding

To fix the raw coordinate problem, we encode the data using trigonometric functions before feeding it to the model.

- **Periodical Bias:** Instead of inputting $X$, inputting $\sin(X)$ forces the model to recognize repeating patterns.
- **Frequency/Granularity:** Changing the input to $\sin(AX)$ allows the model to capture the scale of the data. Tuning $A$ changes the frequency. High frequency captures discrete, localized phenomena, while low frequency captures broad, continuous phenomena.
- **Fourier Series Theorem:** A series of sine and cosine functions acts as a complete basis. If you use enough sine functions of different frequencies, you can represent *any* complex geospatial pattern. This converts a 1D coordinate into an N-dimensional vector.
- **Directionality:** In 2D space, multiplying the coordinates by different unit vectors enables the model to "think" along different geometric directions.

> **Exam Hint:** Know *why* the location encoding formula is used. You inject **direction** (by multiplying coordinates with unit vectors) and **granularity/scale** (by adjusting the frequency/lambda of the sine functions).

------

## 3. Beyond Points: Polylines and Polygons

While points are simple, complex AI tasks require representing shapes and boundaries.

- **Current Storage Limitations:** Polylines (roads, trajectories) and polygons (building footprints) are traditionally stored as discrete sequences of nodes/coordinates.
- **The Flaw:** If you feed a sequence of nodes into an LSTM or Graph Neural Network, the model loses the physical meaning of the data. It loses the topological "path" of a line, and it loses the "coverage" (interior vs. exterior) of a polygon.

### Previous Solution: Poly2Vec

Poly2Vec attempts to solve this by decomposing polygons and polylines into sets of triangles.

- **Mechanism:** It maps each data triangle to a predefined "unified" triangle using transformation functions (rotate, move).
- **Fourier Properties:** It leverages the rule that the Fourier transform of a whole object equals the sum of the Fourier transforms of its parts.
- **Limitation:** The resulting Fourier feature space is highly abstract and uninterpretable. It requires hundreds of sampling points to work effectively.

------

## 4. State-of-the-Art: Geo2Vec

Geo2Vec Abandons the discrete node sequence and the abstract Fourier space in favor of a continuous representation called a **Signed Distance Field (SDF)**.

### How Geo2Vec Works

A Signed Distance Field maps every point in a continuous space based on its distance to a boundary.

- **Boundaries:** Distance = 0
- **Interior (Polygons):** Distance is negative.
- **Exterior:** Distance is positive.
- **Training:** A Neural Network (similar to NERF in computer vision) is trained to approximate this ground-truth distance field. The model takes $X, Y$ as input and predicts the distance $D$. Part of the network's internal parameters are then extracted to serve as the unified representation vector for that specific shape.

### Key Advantages of Geo2Vec

1. **Unified Representation:** It provides a single mathematical framework for points, lines, and polygons. No more dealing with sequences of varying lengths.
2. **Scale-Preserving:** If you zoom out, the center of the distance field represents the absolute location. If you zoom in, the gradient of the field perfectly preserves the detailed shape.
3. **Highly Interpretable:** The representation maps directly to the actual geometric coordinate space, rather than an abstract Fourier space.
4. **High Efficiency:** Because it is interpretable, Geo2Vec requires drastically fewer sampling points (tens instead of hundreds) to achieve better performance than Poly2Vec in downstream tasks like predicting line lengths or polygon shapes.