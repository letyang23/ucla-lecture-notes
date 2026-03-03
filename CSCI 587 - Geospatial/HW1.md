# CSCI 587 • Geospatial Data Analysis Homework 1

# 1 Overview of the Assignment

**Expected Outcome** The goal of this assignment is to explore and compare different methods for executing spatial queries. You will implement three approaches: a brute-force linear search, a space-driven grid index, and a data-driven KD-Tree index. By evaluating their performance on *k* -Nearest Neighbors (KNN) and range queries, you will learn how different indexing techniques can impact query efficiency and understand the trade-offs between them in terms of speed and adaptability to different data distributions.

Distance Metric and Coordinate Space For computational simplicity, treat longitude as the *x* - coordinate and latitude as the *y* -coordinate. The distance between two points shall be computed using the standard Euclidean distance formula in a 2D Cartesian plane:

$$ d = \sqrt {\left(x _ {2} - x _ {1}\right) ^ {2} + \left(y _ {2} - y _ {1}\right) ^ {2}} $$

where *x* := longitude and *y* := latitude. Note: All calculations, including search radii and distance thresholds, should be handled in decimal degrees without converting to metric units.

# 2 Programming Requirements and Environment Settings

While this assignment is designed for Python, you have the option to implement the indexes in C++. Please adhere to the following requirements for your chosen programming language:

• Python: Use Python version 3.6 or higher. Include a requirements.txt file with your submission that lists all the necessary libraries and dependencies (such as scipy, numpy, matplotlib, etc.). To do so, you can use the following commands:

```
pip install pipreqs pipreqs /path/to/project 
```

• C++: Use standard *C* + +11 or higher for your implementation. Include a README file that describes the compilation instructions and any dependencies required for running your code.

Whichever language you choose, ensure your code is well-documented and includes clear instructions for compilation (if using C++) and execution.

# 3 Dataset

This assignment utilizes Points of Interest (POI) data surrounding USC, sourced from OpenStreetMap (OSM) [1]. To retrieve this data, you will use Overpass Turbo [2], a web-based mining tool designed for querying and exporting custom OSM datasets. Details are provided in the following section.

1

# 4 Deliverables and Tasks

# 4.1 Part A: Data Download and Preprocessing (10 pts)

In this part of the assignment, you will download and preprocess a dataset of Points of Interest (POIs) obtained from OpenStreetMap (OSM). The goal is to prepare a clean dataset that can be used for further analysis in subsequent parts of the assignment:

Data Acquisition To obtain the POI data, you will need to follow these steps:

1. Access Overpass Turbo: Go to the Overpass Turbo dashboard at https://overpass-turbo.eu/.

1. Input the Query: Copy and paste the following code into the editor. Clean up this query: remove the extra spaces between the quotation marks caused by copying from a PDF. To prevent the browser from hanging due to the large dataset, do not click Run.

```
// Format output as CSV with POI ID, latitude, longitude, and name [out:csv(:, :, lat, :, lon, "name"; true; "", ]) [timeout:3000]; // Target all named nodes within a 500km radius of USC node (around:500000, 34.0224, -118.2851) ["name"]; out; 
```

1. Export the Data: Click the Export button in the top menu, navigate to the Data section, and select raw data directly from Overpass API. This will trigger an immediate download of the results as a CSV file.

Data Cleansing Clean the dataset by removing entries with missing data or malformed identifiers. Ensure the unique identifier (@id) is numeric and unique.

# 4.2 Part B: Query Implementation: Brute Force Approach (30 pts)

In this part, you will implement two fundamental spatial queries– *k* -nearest neighbors (kNN) and range queries—using a brute force linear search approach. This method involves sequentially checking each entry in the dataset to find the results.

1. *k* -Nearest Neighbors (kNN) Query Using Linear Search: Implement a function to find the *k* closest POIs to a target POI using linear search.
   - Write a helper function, euclidean_distance(point_x, point_y), to compute the Euclidean distance between two POIs.
   - Create a function, knn_linear_search(dataset, target_id, k), that:
     - Takes as input the dataset, a target POI ID, and the number of neighbors (k).
     - Finds the target POI and computes its distance to all other POIs.
     - Returns a list of the *k* -nearest neighbors and their distances.
   - Test your function by randomly selecting target IDs and varying *k* and dataset sizes ( *N* ): *k* ∈ {1, 5, 10, 50, 100, 500} , *N* ∈ {1 000, 10 000, 100 000, Full Dataset}
   - Plot the query execution times and write your observations.

2. Range Query Using Linear Search: Implement a function to find all POIs within a specified distance *r* from a target POI using linear search.

   - Create a function, range_query_linear_search(dataset, target_id, r), that:
     - Takes as input the dataset, a target POI ID, and a radius *r*
     - Returns a list of POIs within the radius r from the target.
   - Test your function by randomly selecting target IDs and varying *r* and dataset sizes (N): r

   - Plot the query execution times and write your observations.

# 4.3 Part C: Implementing Spatial Indexes: Grid Index and KD-Tree (60 pts)

In this part, you will implement two types of spatial indexes — a grid index and a KD-Tree index — to optimize the performance of k-nearest neighbors (kNN) and range queries. After implementing these indexes, you will run the same queries as in the brute force approach, compare the performance of these methods, and analyze the results. You should not use built-in implementations of these indexes such as scipy.spatial.KDTree!

1. Implement a Grid Index: A grid index divides the space into uniform cells and assigns each point to a cell based on its coordinates, restricting the search to relevant cells near the target point.

• Implement a function, build_grid_index(dataset, cell_size), that:

– Takes as input the dataset of POIs and the size of each cell (cell_size).

– Assigns each POI to the appropriate grid cell based on its latitude and longitude.

– Returns the grid index.

• Experiment with different cell sizes (cell_size ∈ {0.01, 0.05, 0.1, 0.2}) and evaluate their impact on query performance.

1. Implement a KD-Tree Index: A KD-Tree is a binary search tree that recursively partitions the space into half-spaces, adapting to the data distribution.

• Implement a function, build_kd_tree(dataset), that:

– Takes as input the dataset of POIs.

– Constructs a KD-Tree from scratch using the coordinates (latitude, longitude) of the POIs.

– Returns the root node of the constructed KD-Tree.

• Use your KD-Tree implementation to perform spatial queries by traversing the tree and comparing distances to find the nearest neighbors or points within a specified range.

# 3. Run Queries and Compare Performance:

• Use your implemented Grid Index and KD-Tree to run the same *k* NN and range queries with the same configurations (values of *k* , *r* , and dataset sizes) as in the brute force approach.

• Verify the correctness of your results by comparing the outcomes from the brute force approach with those from the indexing methods.

• Measure and report the query execution times for each indexing method.

3

• Compare the performance of the Grid Index and KD-Tree against each other and against the brute force approach.

• Provide observations on the impact of different indexing methods on query performance, including any differences observed with varying data distributions, grid cell sizes, and dataset sizes.

# 5 Submission Guidelines

You should submit a single zip file named YourName_USC ID.zip on Brightspace. This file must contain a folder with your code, a README file with clear instructions on how to run your code, and a PDF file named Results that includes your plots, comparisons, and observations.

# References

[1] OpenStreetMap contributors. Openstreetmap. https://www.openstreetmap.org/, 2026. A free, editable map of the whole world that is being built by volunteers.

[2] Martin Raifer. overpass-turbo. https://overpass-turbo.eu/, 2025. A web-based data mining tool for OpenStreetMap.

4