---
title: Code Coupling
description: "Background on Code Coupling Techniques"
    
weight: 1
---

# PCMS
## Future PCMS Coupler Scheme

| Coupler (Conservative Transfer) | Coupler (Native Interpolation) | Coupler (Point Based) |
| :---                            | :---                           | :---                  |
| 1. Obtain mesh topology from apps | 1. Obtain mesh topology from apps | 1. Obtain mesh topology from apps |
| 2. Intersect meshes | 2. Obtain nodal coordinates from target side | 2. Get source eval at point locations |
| 3. Triangulate/determine I.P. | (3.) Perform localization with target | 3. Compute supports |
| 4. Perform point localization | 4. "Remote Eval" source at target points | 4. "Remote Eval" source points within each support radius |
| 5. "Remote Eval" <br>&emsp;- Coordinate transter <br>&emsp;- Send points to eval to client <br>&emsp;- Send point localization map to client (contains point -> element and parametric coordinates) | 5. Send evaluated data to target points | 5. Solve linear system for RBF. May be on client side for local RBF with MLS |
| 6. Get data back | | 6. Send values to target |
| 7. Solve linear system for conservative nodal values | | |
| 8. Send values back to application | | |

