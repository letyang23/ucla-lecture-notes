### 1/26 Lecture - Spatial Index Structures

# 1/28 Lecture - Spatial Index Structures (R-tree Family)

### Problem

- Given a collection of geometric objects (points, lines, polygons, ...) 

- organize them on disk, to answer spatial queries (range, nn, etc)

  <img src="Lecture.assets/Screenshot 2026-01-28 at 2.17.57 PM.png" alt="Screenshot 2026-01-28 at 2.17.57 PM" style="zoom:50%;" />

  

### R-trees

- [Guttman 84] Main idea: extend B+-tree to multi-dimensional spaces! 
  - (only deal with Minimum Bounding Rectangles - **MBR**s)

- A multi-way external memory tree 
- Index nodes and data (leaf) nodes 
- All leaf nodes appear on the same level 
- Every node contains between m and M entries 
- The root node has at least 2 entries (children)

### Example

- eg., w/ fanout 4: group nearby rectangles to parent MBRs; each group -> disk page

<img src="Lecture.assets/Screenshot 2026-01-28 at 2.27.45 PM.png" alt="Screenshot 2026-01-28 at 2.27.45 PM" style="zoom:50%;" />

- F=4

<img src="Lecture.assets/Screenshot 2026-01-28 at 2.28.47 PM.png" alt="Screenshot 2026-01-28 at 2.28.47 PM" style="zoom:50%;" />

<img src="Lecture.assets/Screenshot 2026-01-28 at 2.29.36 PM.png" alt="Screenshot 2026-01-28 at 2.29.36 PM" style="zoom:33%;" />

### R-trees - format of nodes 

- {(MBR; obj_ptr)} for leaf nodes

<img src="Lecture.assets/Screenshot 2026-01-28 at 2.33.03 PM.png" alt="Screenshot 2026-01-28 at 2.33.03 PM" style="zoom:50%;" />

