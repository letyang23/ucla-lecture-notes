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



