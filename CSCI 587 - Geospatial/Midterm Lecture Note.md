## 1/12 Lecture 1 - **CSCI 587: Geospatial Data Analysis – Lecture 1 Cheat Sheet**

### **1. Course Logistics & Structure**

- **Course Evolution:** The course transitioned from "Geospatial Information Management" to "Geospatial Data Analysis," placing heavier emphasis on modern machine learning and deep learning applied to spatial data.
- **Part 1 (Data Management):** Focuses on the fundamentals and challenges of spatial data (indexing, query types). Taught with a deep dive into 1–2 research papers per lecture.
- **Part 2 (Data Analysis):** Focuses on modern AI/ML applications (e.g., traffic forecasting). Fast-paced, covering 3–4 papers per lecture.
- **Grading Breakdown:**
  - **Midterm 1:** First half of the course (Closed book).
  - **Midterm 2:** Second half of the course (Closed book).
  - **Homework (30% total):** 3 assignments, 10% each. HW3 involves training a deep learning model.
  - **Participation (10%):** In-class attendance and engagement. You are allowed 3 unexcused absences.

------

### **2. Database Fundamentals (The Baseline)**

To understand spatial databases, you must first understand traditional database management systems (DBMS).

- **Definition:** A structured collection of data. Unlike standard file systems, databases have specific semantics and structures (e.g., relational tables).
- **Core Operations:** Insert, Update, Delete, and **Querying** (using SQL).
- **The Ultimate Goal — Efficiency:** Databases exist to execute operations fast. This is achieved primarily through **indexing** (e.g., B-trees) rather than scanning every record sequentially.

------

### **3. The Shift to Spatial Data**

Standard relational databases handle numbers and strings well but fail at representing spatial shapes (2D or 3D objects) efficiently.

- **The Inefficiency Problem:** If you store a 2D polygon in a standard relational database, you have to break it down into coordinates stored across multiple tables connected via foreign keys. Querying the shape requires multiple expensive SQL `JOIN` operations.
- **The Solution:** Spatial Database Management Systems (SDMS) introduce new, native geometric data types and optimized spatial indexes to handle this data without heavy `JOIN` overhead.

#### **Core Spatial Data Types**

1. **Points:** Represent single coordinate locations (e.g., a restaurant, a city center).
2. **Lines / Polylines:** Represent continuous paths (e.g., roads, rivers).
3. **Polygons / Regions:** Represent enclosed areas (e.g., states, census blocks, lakes). Polygons can contain "holes."

- *Note: Other representations exist depending on the application, such as graphs/networks (for road networks) or point clouds (for 3D spaces).*

------

### **4. Spatial Relationships & Queries**

When querying spatial data, relationships fall into three main categories:

| **Type**        | **Description**                                              | **Examples**                                                 |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Topological** | Relationships that remain invariant (unchanged) under transformations like scaling, translation, or rotation. | Intersect, inside, adjacent, touch, disjoint, overlap, cover, equal. |
| **Metric**      | Relationships based on distance. These *change* if the map is scaled. | Distance within 10 miles. Calculated via formulas like Euclidean distance: $\sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$ |
| **Directional** | Relationships based on orientation. These *change* if the map is rotated. | North of, South of.                                          |

------

### **5. Spatial Indexing: "Filter and Refine"**

Determining the exact topological relationship between two complex polygons is highly computationally expensive. Spatial databases solve this using a two-step "Filter and Refine" indexing approach.

1. **Filter Phase (Fast but Approximate):**
   - The database draws a **Minimum Bounding Rectangle (MBR)** around every complex polygon.
   - It tests for overlaps using only the MBRs. Checking if two rectangles overlap is mathematically simple and computationally cheap.
   - This step quickly filters out all shapes that definitely do *not* overlap.
2. **Refine Phase (Slow but Exact):**
   - For the MBRs that *do* overlap, the database then runs the complex computational geometry algorithms on the actual underlying polygons to confirm if a true intersection exists.

------

### **6. Advanced Spatial Concepts**

- **Spatial Joins:** Joining two spatial tables based on a spatial predicate rather than matching strings/numbers.
  - *Classic Example:* Doing a spatial join on a `Roads` table (lines) and a `Rivers` table (lines) where they `Intersect` will yield the locations of **Bridges**.
- **Query Optimization:** Standard SQL optimizers rely heavily on "selectivity" (how many rows a filter removes). Spatial optimizers must also factor in the **computational cost** of the spatial operation itself, as checking exact polygon overlap is drastically more expensive than checking a simple integer threshold (e.g., Population > 500,000).
- **GIS vs. SDMS:**
  - **Geographical Information Systems (GIS):** Focuses on the user application, visualization, dashboards, and spatial analytics (e.g., ArcGIS, Palantir).
  - **Spatial DBMS:** The underlying infrastructure layer (in the middle of GIS and raw computational geometry) that focuses strictly on efficient storage, indexing, and retrieval.

------

### **7. System Landscape (Brief Overview)**

- **Open Source Standard:** **PostGIS** (an extension for PostgreSQL) remains the most common and robust open-source spatial database.
- **Commercial Standard:** Oracle Spatial.
- **Modern/Cloud-Scale:** Tools like Google BigQuery (now supports spatial), Apache Sedona, and GeoMesa are used for distributed, cloud-scale spatial computing.

------



# 1/21 Lecture 3 (Guest Lecture)

------

## **1. Core Concepts & Applications**

Computational geometry involves the scientific design, analysis, and implementation of algorithms solving geometric problems.

**Common Applications:**

- **Robotics:** Path planning and avoiding collisions as shapes move through space.
- **GIS (Geographic Information Systems):** Finding map intersections, overlaps, and routes.
- **Computer-Aided Graphics:** 3D modeling, rendering, and tessellation.
- **Scientific Computing:** Simulating car crashes (folding and collisions) and circuit layouts.

**Primitive Objects:**

- **2D:** Points, line segments, polygons, circles, ellipses, and Bezier curves.
- **3D:** Polyhedra, spheres, cylinders, and cones. Problems scale in complexity in 3D (e.g., finding the shortest path on a 3D folded surface requires unfolding it to a 2D plane).

------

## **2. Point Operations & Vector Math**

Points are the most primitive geometric objects. In algorithmic design, they are best treated as vectors originating from the origin $(0,0)$.

**Fundamental Operations:**

- **Vector Subtraction ($B - A$):** Yields a vector representing the distance and direction from point A to point B.
- **Vector Addition ($A + B$):** Yields the fourth vertex of a parallelogram where the other three vertices are the origin, A, and B.
- **Dot Product:** Yields a scalar value indicating alignment. Formula: $A \cdot B = |A||B|\cos(\theta)$. A result of $0$ means orthogonal, and a negative result means the angle is $> 90^\circ$.
- **Cross Product (2D):** Yields a scalar representing the area of a parallelogram and the left/right orientation. Formula: $x_1y_2 - y_1x_2$.

**The Left/Right Turn Test:**

To determine if point Q is to the left or right of a directed line segment from P1 to P2:

1. Create $V_1 = P_2 - P_1$
2. Create $V_2 = Q - P_1$
3. Calculate the cross product $V_1 \times V_2$.
4. A **negative** result means Q is to the **right**. A **positive** result means Q is to the **left**.

------

## **3. The Convex Hull**

The convex hull of a set of points is the smallest convex polygon that contains all points inside it or on its boundary. Think of it as snapping a rubber band around a set of nails on a board.

**Applications:**

- **Gaming / Collision Detection:** Tighter and more accurate than a simple rectangular bounding box, while still allowing linear time $O(n)$ intersection checks.
- **Linear Programming:** The simplex method searches the vertices of a convex polyhedra (the feasible region).

**Convex Hull Algorithms:**

| **Algorithm**        | **Time Complexity** | **Description**                                              |
| -------------------- | ------------------- | ------------------------------------------------------------ |
| **Brute Force**      | $O(n^3)$            | Check all pairs of points; verify if all other points fall on one side of the segment. |
| **Angle Search**     | $O(n^2)$            | Start at the lowest Y point. Find the point with the most acute angle to form an edge. Repeat. |
| **Graham Scan**      | $O(n \log n)$       | Sort points counter-clockwise by angle from the lowest point. Use a stack to track the hull, popping vertices if a "right turn" is detected. |
| **Divide & Conquer** | $O(n \log k)$       | Output-sensitive algorithm. Best when the number of points actually on the hull ($k$) is very small compared to the total points ($n$). |

------

## **4. Closest Pair of Points**

Finding the two points closest to each other on a 2D plane.

- **Brute Force:** $O(n^2)$ checking all pairs.
- **Divide & Conquer Approach ($O(n \log n)$):**
  1. Split the points in half by an X-coordinate.
  2. Recursively find the minimum distance on the left side ($\delta_1$) and the right side ($\delta_2$).
  3. Let $\delta = \min(\delta_1, \delta_2)$. The overall closest pair might cross the middle dividing line, but they *must* be within a distance of $\delta$ from that center line.
  4. Sort the points in this middle $2\delta$ band by their Y-coordinates.
  5. Because of the $\delta$ constraints, you only need to check a maximum of **6 neighboring points** on the other side for any given point, reducing the merge step to linear time.

------

## **5. Voronoi Diagrams & Delaunay Triangulation**

These two structures are mathematically dual to one another and unlock extremely fast spatial lookups.

**Voronoi Diagram ($O(n \log n)$):**

- Partitions a plane into regions (polygons) based on the distance to a specific set of points.
- Any location inside a specific polygon is strictly closer to that polygon's core point than to any other point on the map.
- **Application:** Finding the nearest airport for an emergency landing, or the closest coffee shop based on GPS coordinates.

**Delaunay Triangulation ($O(n \log n)$):**

- Connects points to their nearest neighbors to form triangles. The edges of the Voronoi diagram act as perpendicular bisectors to the edges of the Delaunay triangulation.
- **Key Property:** It maximizes the minimum angle of all triangles. This prevents "flimsy" or sharp triangles, which is crucial for stability in finite element analysis and scientific simulations.
- **Euclidean Minimum Spanning Tree (EMST):** Can be found in $O(n \log n)$ time by first computing the Delaunay triangulation (which trims the graph from $n^2$ possible edges to a linear $O(n)$ edges), and then running a standard MST algorithm.

------

## **6. Triangulating Polygons**

Breaking down a complex polygon into a series of triangles for rendering or simulation.

| **Polygon Type**      | **Algorithm Complexity** | **Notes**                                                    |
| --------------------- | ------------------------ | ------------------------------------------------------------ |
| **Convex**            | $O(n)$                   | Easily triangulated by anchoring to one vertex. The number of possible triangulations is described by Catalan numbers. |
| **Monotone**          | $O(n)$                   | Solved using a greedy plane-sweep algorithm from left to right, utilizing a stack for deferred nodes. |
| **General / Concave** | $O(n \log n)$            | The complex polygon must first be broken into monotone pieces ($O(n \log n)$), which are then triangulated in linear time. |

------

## **7. Line Segment Intersection**

Finding intersections among a large set of $N$ line segments.

**Algorithm: Plane Sweep / Line Sweep**

- **Core Observation:** Segments must be adjacent in their Y-coordinates to intersect. You only need to check for intersections between immediate neighbors.
- **Data Structure 1 (Min-Heap):** Stores "Event Points" (start of a segment, end of a segment, and newly discovered intersections), keyed by the X-coordinate to process left to right.
- **Data Structure 2 (Balanced Binary Tree):** Stores the active line segments, keyed by their Y-coordinates.
- **Process:** As the vertical sweep line hits event points, segments are inserted, removed, or swapped in the binary tree. Whenever segments become adjacent due to an event, check them for intersection.
- **Time Complexity:** $O((n + m) \log n)$, where $m$ is the actual number of intersections. This is drastically faster than the brute force $O(n^2)$ when intersections are sparse.

------



# 1/26 Lecture 4

### Lecture Cheat Sheet: Spatial Indexing Techniques

#### 1. Course & Exam Logistics

- **Exam Structure:** Exams will consist of 7–9 questions.
  - 1–2 questions will be multiple-choice/fill-in-the-blank.
  - 6–7 questions will be problem-solving (math/algorithmic type).
  - No essay questions. No sample exams will be provided (examples given at the end of lectures will suffice).
- **Course Context:** The course builds on underlying database management and computational geometry techniques (e.g., Voronoi diagrams), but the focus is on *how* to build indexing techniques on top of them, not the geometry itself.
- **Core Assumption:** The course assumes data is massive and resides on **disk** (disk-based indexing), not in memory.

#### 2. Indexing Basics & The 2D Challenge

- **What is an index?** A list of pointers (like a Yellow Pages directory) that speeds up the search for specific data.
- **1D Indexing:** In 1D arrays, sorting allows for binary search, reducing search complexity from $O(n)$ to $O(\log n)$.
- **The 2D Problem:** You cannot simply sort 2D spatial data (X, Y / Latitude, Longitude).
  - Sorting by only X or only Y is inaccurate (e.g., it might group Los Angeles and New York together if only checking latitude).
  - Sorting by Euclidean distance to the origin reduces 2D to 1D, but destroys spatial proximity relationships (things close in real life might end up far apart in the index).
- **Disk Pages vs. Single Items:** In spatial databases, index pointers don't point to a single item; they point to a **disk page** that contains multiple items. The number of items a page can hold depends on the page size and item size.

#### 3. Grid Files

- **Concept:** Divide the 2D space into a grid where each cell points to a disk page.
- **Two-Disk Access Principle (Exact Match):**
  1. Read the index directory (if not in memory) to find the pointer.
  2. Read the actual data page from the disk.
- **Splitting Mechanism:** When a page reaches its capacity, the grid splits. In a standard Grid File, the split goes **all the way across** the X or Y axis.
- **Linear Scale:** An improvement over a basic grid. The X and Y axes don't have to be cut uniformly. The "scale" (which defines the grid boundaries) is kept in memory to avoid extra disk access.
- **Shortcomings of Grid Files:**
  - **Skewed Data:** Because splits go all the way across the space, dense data in one corner forces empty grid cells in other areas.
  - **Dimensionality Curse:** Storage grows exponentially with the number of dimensions.
  - **Range Queries:** A rectangular range query might overlap with many grid cells that contain no relevant data, causing expensive and unnecessary disk I/O.

#### 4. Space-Filling Curves (Dimension Reduction)

- **Goal:** Map a 2D space into a 1D sequence while keeping points that are close in 2D space as close as possible in the 1D index.
- **Row Order:** Ineffective. Points adjacent vertically are far apart in the index.
- **Z-Ordering (Morton Curve):**
  - Uses a hierarchical, recursive "Z" pattern to navigate quadrants (0, 1, 2, 3).
  - **The Shuffle Algorithm:** You don't have to manually count to find a coordinate's 1D value. You can take the binary bits of the X and Y coordinates and "shuffle" (interleave) them. Example: X = `01`, Y = `11` $\rightarrow$ Shuffled = `0111` (7).
  - *Flaw:* Still has occasional "jumps" where items close in 2D space are placed far apart in the 1D sequence.
- **Hilbert Curve:**
  - A smoother, continuous curve that navigates up, left, right, and down without the large diagonal jumps of the Z-curve.
  - **Advantage:** Superior for preserving spatial proximity and clustering objects. Translating between 2D coordinates and the 1D Hilbert value is done via a specific transformation function (the $L$ function).

#### 5. Quadtrees

- **Concept:** Solves the Grid File's skewness problem by splitting space **locally** rather than globally. When an area gets too dense, it subdivides into four equi-sized quadrants (NW, NE, SW, SE) only in that specific local area.
- **Types of Quadtrees:**
  1. **Region Quadtree (For Areas):**
     - Used to index regions (e.g., Water vs. Not Water).
     - If a cell is 100% water or 100% land, it stops splitting. If it contains a boundary, it splits into four.
     - *Applications:* Hyperspectral satellite imagery, containment queries.
  2. **Point Quadtree (For Coordinates):**
     - Splits locally when a cell exceeds its point capacity (e.g., only 1 city allowed per cell).
     - *Applications:* Nearest neighbor searches, fast counting (if a query rectangle fully covers a parent node, you just sum the population without checking the children), heat maps.
  3. **PM Quadtree (Polygonal Map - For Lines & Points):**
     - Used when your data has both vertices (points) and edges (lines).
     - *Core Intuition:* You do not want two distinct "features" in the same cell.
     - **PM1 Rules:** You must split the cell if it contains two points, OR a point and a separate line, OR two intersecting lines.
     - **PM2 & PM3:** Relax the strict PM1 rules to prevent the tree from splitting infinitely (which creates heavily imbalanced trees and bloats the node size).
     - *Applications:* Geocoding (e.g., an Amazon or Google maps query mapping an exact X,Y coordinate to the nearest named street for a mailing address).



# 1/28 Lecture 5 Cheat Sheet: Object-Based Spatial Indexing (R-Trees)

------

#### 1. Space-Based vs. Object-Based Indexing

To understand R-trees, you must first distinguish between the two primary ways to index spatial data.

- **Space-Based Indexing (e.g., Grid, Quadtree, Z-ordering):** Starts with the bounding box of the entire "world" or dataset space (e.g., the map of Los Angeles) and partitions that space. If you add a new city, you must recreate the bounding box and rebuild the index.
- **Object-Based Indexing (e.g., R-trees):** Indexes the actual objects in the database regardless of the "world" space. It builds the structure dynamically from the objects themselves, making it easier to scale without redefining the total global area.

------

#### 2. R-Tree Fundamentals

The R-tree (introduced in 1984) is a multi-dimensional extension of the B+ tree. Instead of 1D ranges, it uses multi-dimensional ranges represented as Minimum Bounding Rectangles (MBRs).

- **Node Capacity:** Each disk page (node) can hold a specific number of objects, governed by a maximum (M) and a minimum (m).
- **Maximum (M):** Determined by the disk page size divided by the item size (pointer + coordinates).
- **Minimum (m):** Usually set to half of M. This prevents underutilization of disk pages, which would result in deep trees and expensive disk I/O operations. The root node is exempt from this minimum.
- **Leaf Nodes:** Contain the MBR coordinates of the actual objects and a direct pointer to the database record.
- **Internal Nodes:** Contain the MBR that fully encloses all child MBRs below it, plus a pointer to the child node.

------

#### 3. R-Tree Construction (Insertion & Splitting)

R-trees are built by inserting one object at a time. The order of insertion directly changes the final shape of the tree!

**Step 1: Choose Leaf**

When inserting a new object, the tree must decide which existing MBR (box) should house it.

- **The Intuition:** Pick the box that requires the **minimum area extension** to completely cover the new object. You want to keep boxes as tight and compact as possible.

**Step 2: Quadratic Split (If a node is full)**

If the chosen node already contains the maximum M objects, it must split into two new groups.

- **Pick Seeds (The first two objects):** Look at all possible pairs of objects in the overflowing node. Pick the two objects that, if grouped together, would create the most "wasted area" (empty space). Put one in Group 1 and the other in Group 2.

  > pick 最远的两个object，form 两个group

- **Pick Next:** For the remaining objects, calculate how much Group 1 would grow if the object was added, versus how much Group 2 would grow. Find the object with the **maximum difference** between these two growth values and assign it to the group that requires the least growth.

  > d1 = k goes to g1, d2 = k goes to g2, d1-d2 is the largest number

------

#### 4. R-Tree Querying

Querying always starts at the root node and moves downward, bringing disk pages into memory one by one (I/O cost).

- **Exact Match Query:** Given a specific target coordinate, check which child MBRs overlap with the target.
- **Range/Overlap Query:** Given a search box, find all objects that overlap with it.
- **The Overlap Problem:** In R-trees, sibling MBRs are allowed to overlap. If your search target falls into an overlapping region between Box A and Box B, the algorithm does not know which box holds the actual object. You are forced to search down **both** paths, increasing disk I/O.

------

#### 5. Limitations of R-Trees & The R+ Tree Solution

Because overlapping MBRs cause inefficient search paths, the R+ tree was proposed as a fix.

- **The R+ Tree Concept:** It completely forbids overlapping MBRs. If an object falls across a boundary between two boxes, the object is duplicated and clipped into both boxes.
- **Drawbacks:** * Duplication wastes space and causes nodes to fill up faster, leading to taller trees (which means more I/O access time).
  - Aggregate queries (like counting) require extra filtering steps to remove the duplicated entries.
  - It awkwardly mixes space-based cell partitioning with object-based indexing. (Rarely used in commercial systems today).

------

#### 6. R* Trees (R-Star Trees) & Optimizations

Instead of forbidding overlap entirely like the R+ tree, the R* tree introduces aggressive optimization heuristics to naturally minimize overlap and improve structure.

**Key Optimizations:**

- **Minimize Perimeter (Margin):** Given the choice, the algorithm prefers MBRs that look more like squares than long, skinny rectangles. Squares tile space much more efficiently and are less likely to overlap.
- **New Split Algorithm:** Instead of the Quadratic Split, the R* tree sorts items along an axis (X or Y), splits them to minimize the perimeter, and then finalizes the split to minimize overlap.
- **Forced Reinsertion:** When a node overflows, do not split it immediately! Instead, temporarily delete 30% of the entries in that node (specifically, the ones that shrink the MBR the most). Reinsert those deleted items from the top of the tree. Because the tree now has a better established "map" of the data space, reinserting items usually leads to a much more compact, efficient tree layout.



# 2/2 Lecture **Cheat Sheet: Nearest Neighbor (NN) Search in Spatial Databases**

## **1. Introduction to Nearest Neighbor (NN) Queries**

- **Definition**: Given a query point $Q$ (e.g., a latitude/longitude coordinate), find the spatial object/point closest to $Q$.
- **Distance Metric**: Typically relies on **Euclidean distance**.
- **k-Nearest Neighbor (k-NN)**: A variation where the query asks for the $k$ closest objects (e.g., the 5 closest coffee shops).

## **2. The Naive Approach: Range Query Expansion**

Instead of a dedicated NN algorithm, one could guess a range and use standard range queries (which R-Trees already support well).

- **Method**:
  1. Draw a small bounding box/circle centered at $Q$.
  2. Query the R-Tree. If no objects are found, expand the radius and query again.
  3. Once an object $P$ is found, do one final range query with radius equal to the distance $Q \to P$ to guarantee no other object is closer.
- **Problem**: Highly inefficient. It requires guessing the radius and running multiple separate R-Tree queries, which leads to excessive disk I/O (opening too many nodes/boxes). In higher dimensions, almost all objects appear equidistant, generating massive candidate pools.

------

## **3. Direct R-Tree Search & Pruning Metrics**

*Goal: Traverse the R-Tree directly to find the NN without opening a node (disk page) unless absolutely necessary to minimize I/O.*

To decide whether to open a Minimum Bounding Rectangle (MBR) or discard it, we rely on two key distance metrics:

### **A. MINDIST (Minimum Distance)**

- **Definition**: The absolute shortest Euclidean distance between query point $Q$ and the boundary of the MBR.
- **Property**: It serves as the **strict lower bound**. No object *inside* that MBR can be closer to $Q$ than $MINDIST$.
- **Calculation**:
  - If $Q$ is aligned with the MBR's faces, it is the perpendicular distance to the closest edge.
  - If $Q$ is outside the parallel bounds of the faces, it is the distance to the closest vertex.
  - *Note:* If $Q$ is *inside* the MBR, $MINDIST = 0$.
- **Pruning Rule**: If $MINDIST(Q, MBR) >$ distance to our current best candidate object, **do not open the MBR** (prune it).

### **B. MINMAXDIST (Min-Max Distance)**

- **The "Face Property" of MBRs**: By definition, an MBR tightly bounds its objects. Therefore, *every face (edge) of the MBR must touch at least one point of the enclosed objects*.
- **Definition**: The smallest possible upper bound of the distances from $Q$ to an object in the MBR. It guarantees there is *at least one object* in the MBR at a distance $\le MINMAXDIST$.
- **Calculation**:
  1. For each dimension (X and Y), identify the face of the MBR that is *closest* to $Q$.
  2. Calculate the distance from $Q$ to the *farthest* point on that closest face.
  3. Take the **minimum** of these maximum distances across all dimensions.
- **Pruning Rule**: If $MINDIST(Q, MBR\_A) > MINMAXDIST(Q, MBR\_B)$, we can safely prune $MBR\_A$. Why? Because $MBR\_B$ is *guaranteed* to contain an object closer to $Q$ than anything inside $MBR\_A$.

------

## **4. NN Search Algorithms in R-Trees**

### **A. Depth-First Search (DFS)**

- **How it works**: Traverses down the tree branch by branch (e.g., going down the left-most nodes first). It calculates $MINDIST$ dynamically to establish a "current best" candidate, using it to prune other branches as it travels back up the tree.
- **Drawback**: It is not "I/O Optimal". If it searches a bad branch first, it will open many unnecessary nodes before finding a tight candidate distance to start pruning effectively.

### **B. Best-First Search (Global Priority Queue)**

- **How it works**: Maintains a single, global Priority Queue (Heap) of all visited MBRs, sorted strictly by $MINDIST$.
  1. Pop the MBR with the smallest $MINDIST$ from the queue.
  2. Open it, calculate $MINDIST$ for its children, and insert them into the queue.
  3. Stop when the element popped from the queue is an actual **object** (not an MBR).
- **Advantages**:
  - **I/O Optimal**: Mathematically proven to only open the absolute minimum number of nodes required.
  - **Incremental k-NN**: Easily adaptable to k-NN. Just keep popping from the heap to get the 2nd nearest, 3rd nearest, etc.
- **The Fatal Flaw (Memory)**: The priority queue grows massively. If the dataset is large, the heap exceeds RAM capacity, forcing the OS to swap memory to disk ("thrashing"). This entirely negates the I/O savings of the algorithm.

### **C. Branch and Bound Algorithm (Local Lists)**

- **How it works**: Uses a DFS approach, but instead of a massive global heap, it maintains a **small Active Branch List (ABL)** *per node* (which easily fits in memory).
- **Process**:
  1. At each node, evaluate all child MBRs.
  2. Sort the local MBRs using an ordering metric (either $MINDIST$ or $MINMAXDIST$).
  3. Aggressively apply pruning rules using both $MINDIST$ and $MINMAXDIST$ to drop MBRs from the local list.
  4. Visit the remaining MBRs in the sorted order.
- **Sorting Metric Dilemma**:
  - Sorting by $MINDIST$ is theoretically closer to I/O optimal.
  - Sorting by $MINMAXDIST$ prioritizes boxes guaranteed to have a close point, which can sometimes find a tight candidate faster in practice.
- **Advantage**: Fixes the memory/thrashing issue of Best-First Search while still aggressively minimizing disk I/O.

------

## **Summary Comparison**

| **Algorithm**      | **Traversal Style** | **Data Structure** | **Pruning / Metric Used** | **Pros & Cons**                                              |
| ------------------ | ------------------- | ------------------ | ------------------------- | ------------------------------------------------------------ |
| **Naive Range**    | Bounding Box        | None               | None                      | **Pros:** Simple. **Cons:** Horrible I/O, lots of guessing.  |
| **Basic DFS**      | Depth-First         | Call Stack         | $MINDIST$                 | **Pros:** Low memory. **Cons:** Not I/O optimal, order-dependent. |
| **Best-First**     | Global Best         | Global Min-Heap    | $MINDIST$                 | **Pros:** I/O Optimal, great for k-NN. **Cons:** Heap grows too large, causes disk thrashing. |
| **Branch & Bound** | Depth-First         | Local ABLs         | $MINDIST$ & $MINMAXDIST$  | **Pros:** Fits in memory, highly aggressive pruning. **Cons:** Technically not strictly I/O optimal. |

