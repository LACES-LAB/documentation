---
title: SimModSuite
description: SimModSuite is a C++ and Python meshing library developed by Simmetrix.
weight: 1
---

SimModSuite Documentation and Tutorials can be found on the [SimModSuite Documentation Site](https://old-www.scorec.rpi.edu/~cwsmith/SCOREC/). This method may not be the most efficient way to walk the boundary nodes, but it is intuitive.


## Walk Along the Boundary of a Mesh
This tutorial shows how to open a mesh and a model using the SimModSuite API and extract the coordinates of the boundary nodes. This is an extract from the [DG2MeshwBoundary Repository](https://github.com/Fuad-HH/DG2MeshwBoundary/blob/16de0b449a0b88dbecdbe6d42ecde24c510eba78/DG2MeshwBoundary.cpp#L293-L354).

```cpp
std::vector<std::array<double, 2>> readWallFromSimMesh(const std::string &model_filename, const std::string &mesh_filename, pProgress progress) {
  const auto model = GM_load(model_filename.c_str(), NULL, progress);
  const auto mesh = M_load(mesh_filename.c_str(), model, progress);

  // find the leftmost mesh vertex to start searching for wall vertices
  VIter v_iter = M_vertexIter(mesh);
  pVertex leftmost_vertex = nullptr;
  pVertex current_vertex = nullptr;

  while (current_vertex = VIter_next(v_iter)) {
    if (!leftmost_vertex) {
      leftmost_vertex = current_vertex;
    } else {
      double current_coords[3];
      double leftmost_coords[3];
      V_coord(current_vertex, current_coords);
      V_coord(leftmost_vertex, leftmost_coords);
      if (current_coords[0] < leftmost_coords[0]) {
        leftmost_vertex = current_vertex;
      }
    }
  }
  VIter_delete(v_iter);

  // traverse the boundary edges to collect wall vertices
  std::vector<std::array<double, 2>> wall_points;
  current_vertex = leftmost_vertex;
  pEdge last_boundary_edge = nullptr;
  while (true) {
    pEdge current_boundary_edge = nullptr;
    const int n_adj_edges = V_numEdges(current_vertex);
    for ( int i = 0; i < n_adj_edges; ++i) {
      current_boundary_edge = V_edge(current_vertex, i);
      if (E_numFaces(current_boundary_edge) == 1 && current_boundary_edge != last_boundary_edge) {
        last_boundary_edge = current_boundary_edge;
        break;
      }
    }
    if (current_boundary_edge == nullptr) {
      double current_coords[3];
      V_coord(current_vertex, current_coords);
      printf("Error: For vertex at (%.6f, %.6f, %.6f), no boundary edge found but it has %d adjacent edges.\n",
             current_coords[0], current_coords[1], current_coords[2], n_adj_edges);
      std::abort();
    }

    // find the next vertex on the boundary edge
    current_vertex = E_otherVertex(current_boundary_edge, current_vertex);

    // store the vertex coordinates
    double coords[3];
    V_coord(current_vertex, coords);
    wall_points.push_back({coords[0], coords[1]});

    // complete the loop
    if (current_vertex == leftmost_vertex) {
      break; // completed the loop
    }
  }

  return wall_points;
}
```