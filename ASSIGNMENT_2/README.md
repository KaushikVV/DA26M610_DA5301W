# Assignment 2

This folder is organized into two parts: `InClass` and `TakeHome`. Each part keeps its data files and source notebook in separate subfolders.

## Folder structure

```text
ASSIGNMENT_2/
├── InClass/
│   ├── data/
│   │   ├── OL.cedge
│   │   └── OL.cnode
│   └── src/
│       └── assignment_2_in_class.ipynb
└── TakeHome/
    ├── data/
    │   ├── facebook_combined.txt
    │   └── facebook_combined.txt.gz
    └── src/
        └── social_astar_takehome.ipynb
```

## Contents

- **`InClass/`** — In-class assignment files.
  - **`data/`** — `OL.cedge` and `OL.cnode` data files.
  - **`src/`** — The `assignment_2_in_class.ipynb` notebook.
- **`TakeHome/`** — Take-home assignment files.
  - **`data/`** — The Facebook network data in plain-text and compressed (`.gz`) formats.
  - **`src/`** — The `social_astar_takehome.ipynb` notebook.

## Environment setup

The notebooks use Python, NumPy, and NetworkX. The in-class notebook also uses Matplotlib to visualize the graphs. To create and activate the Conda environment from this folder, run:

```bash
conda env create -f environment.yml
conda activate assignment-2
```

Alternatively, the Conda package list is in `requirements.txt` and can be used with:

```bash
conda create --name assignment-2 --file requirements.txt
```

After activating the environment, open either notebook in Jupyter. The take-home notebook can download the SNAP dataset if the text file is missing; the in-class notebook can download its road-network files if they are missing.

## How I solved the assignment

### InClass

I first used the provided small, fixed graph to implement Breadth-First Search (BFS) and Depth-First Search (DFS) myself. Both algorithms keep track of visited nodes and parent links so that I can reconstruct a path from the source to the destination. I considered neighbors in increasing node order to make the traversal results consistent, then recorded the paths and expansion orders and visualized each route.

For the road-network exercise, I loaded the node coordinates and weighted edges from `OL.cnode` and `OL.cedge`, built a NetworkX graph, and kept its largest connected component. I then implemented Dijkstra's algorithm using a priority queue and edge lengths to find the shortest route from node 100 to node 6000. I checked the computed route length against NetworkX and plotted the route with its endpoints highlighted.

### TakeHome

I loaded the SNAP Facebook edge list into an undirected adjacency structure and checked the network statistics. For the two assigned node pairs, I implemented BFS and DFS, tracking the path and the number of expanded nodes. I sorted the neighbors so that the search order was deterministic.

For the weighted search, I calculated the Jaccard similarity between the neighbor sets of each connected pair, then converted each similarity into an integer friction weight. I used these weights in an A* search implementation with a priority queue, path reconstruction, and expansion counting, and ran it on the two benchmark pairs. This exercise compares unweighted searches, which find paths by hop count, with A*, which searches using the assigned friction costs.
