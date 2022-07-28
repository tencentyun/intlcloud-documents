The database supports geometric types of point, box, lseg, line, path, polygon, and circle, so it also provides a series of geometric functions as listed below:

## Geometric Operators

| Operator | Description | Example | Result |
| ------ | ------------------------------------ | ---------------------------------------------------- | ------------- |
| +      |  Translation                             | box   '((0,0),(1,1))' + point '(2.0,0)'              | (3,1),(2,0)   |
| -      |  Translation                             | box '((0,0),(1,1))'   - point '(2.0,0)'              | (-1,1),(-2,0) |
| *      | Scaling/Rotation                            | box   '((0,0),(1,1))' * point '(2.0,0)'              | (2,2),(0,0)   |
| /      | Scaling/Rotation                            | box   '((0,0),(2,2))' / point '(2.0,0)'              | (1,1),(0,0)   |
| #      | Point or box of intersection                       | box   '((1,-1),(-1,1))' # box '((1,1),(-1,-1))'      | (1,1),(-1,-1) |
| @-@    | Length or circumference                   | @-@ path   '((0,0),(1,0))'                           | 2             |
| @@     | Center                                 | @@   circle '((0,0),10)'                             | (0,0)         |
| ##     | Closest point to the first operand on the second operand       | point   '(0,0)' ## lseg '((2,0),(0,2))'              | (1,1)         |
| <->    | Distance between                       | circle   '((0,0),2)' <-> circle '((4,0),1)'          | 1             |
| &&     | Overlaps?                     | box   '((0,0),(1,2))' && box '((0,0),(2,3))'         | t             |
| <<     | Is strictly left of?          | circle   '((0,0),1)' << circle '((5,0),1)'           | t             |
| >>     | Is strictly right of?          | circle   '((5,0),1)' >> circle '((0,0),1)'           | t             |
| &<     | Does not extend to the right of? | box   '((0,0),(1,1))' &< box '((0,0),(2,2))'         | t             |
| &>     | Does not extend to the left of? | box   '((0,0),(3,3))' &> box '((0,0),(2,2))'         | t             |
| <<\|   | Is strictly below?            | box   '((0,0),(2,2))' <<\| box '((4,5),(6,6))'       | t             |
| \|>>   | Is strictly above?            | box '((5,6),(7,7))'   \|>> box '((0,0),(4,4))'       | t             |
| <^     | Is below (allows touching)?        | box '((5,6),(7,7))'    <^ box '((0,0),(4,4))'        | f             |
| >^     | Is above (allows touching)?      | box '((5,6),(7,7))'    >^ box '((0,0),(4,4))'        | t             |
| ?#     | Intersects?                                 | lseg   '((-1,0),(1,0))' ?# box '((-2,-2),(2,2))'     | t             |
| ?-     | Is horizontal?                             | ?- lseg   '((-1,0),(1,0))'                           | t             |
| ?-     | Are horizontally aligned?                     | point   '(1,0)' ?- point '(0,0)'                     | t             |
| ?\|    | Is vertical?                             | ?\| lseg   '((-1,0),(1,0))'                          | f             |
| ?\|    | Are vertically aligned?                 | point   '(1,2)' ?\| point '(1,1)'                    | t             |
| ?-\|   | Is perpendicular?                       | lseg '((0,0),(0,1))'   ?-\| lseg '((0,0),(1,0))'     | t             |
| ?\|\|  | Are parallel?                       | lseg   '((-1,0),(1,0))' ?\|\| lseg '((-1,2),(1,2))'  | t             |
| @>     | Contains?                   | circle   '((0,0),2)' @> circle '((0,0),1)''          | t             |
| <@     | Contained in or on?                 | point   '(1,1)' <@ circle '((0,0),2)'                | t             |
| ~=     | Same as?                             | polygon   '((0,0),(1,1))' ~= polygon '((1,1),(0,0))' | t             |



## Geometric Functions

| Function | Return Type | Description | Example | Result |
| ---------------- | ------------------ | ------------ | -------------------------------------- | ------- |
| area(object)     | double   precision | Area         | area(box   '((0,0),(1,2))')            | 2       |
| center(object)   | point              | Center       | center(box   '((0,0),(1,2))')          | (0.5,1) |
| diameter(circle) | double   precision | Diameter of circle     | diameter(circle   '((0,0),2.0)')       | 4       |
| height(box)      | double   precision | Vertical size of box           | height(box   '((0,0),(2,3))')          | 3       |
| isclosed(path)   | boolean            | A closed path? | isclosed(path   '((0,0),(1,1),(2,0))') | t       |
| isopen(path)     | boolean            | An open path? | isopen(path   '[(0,0),(1,1),(2,0)]')   | t       |
| length(object)   | double   precision | Length   | length(path   '((-1,0),(1,0))')        | 2       |
| npoints(path)    | int                | Number of points | npoints(path   '[(0,0),(1,1),(2,0)]')  | 3       |
| npoints(polygon) | int                | Number of points | npoints(polygon   '((1,1),(0,0))')     | 2       |
| radius(circle)   | double   precision | Radius of circle     | radius(circle   '((0,0),2.0)')         | 2       |
| width(box)       | double   precision | Horizontal size of box     | width(box   '((0,0),(3,2))')           | 3       |

## Geometric Type Conversion Functions

| Function | Return Type | Description | Example | Return Value |
| ------------------- | ---------- | ---------------------- | ------------------------- | ----------------------------- |
| box(circle)                                 | box        | Circle to box             | box(circle   '((0,0),3.0)')             | (2.12132034355964,2.12132034355964),(-2.12132034355964,-2.12132034355964)   (1 row) |
| box(point, point)    | box        | Points to box            | box(point   '(0,0)', point '(2,2)')     | (2,2),(0,0)        |
| box(polygon)      | box        | Polygon to box         | box(polygon   '((0,0),(1,1),(2,0))')    | (2,1),(0,0)             |
| circle(box)   | circle     | Box to circle             | circle(box   '((0,0),(2,2))')           | <(1,1),1.4142135623731>           |
| circle(point, double   precision)    | circle     | Center and radius to circle       | circle(point   '(0,0)', 3.0)            | <(0,0),3>             |
| circle(polygon)      | circle     | Polygon to circle  | circle(polygon   '((0,0),(1,1),(2,0))') | <(1,0.333333333333333),0.924950591148529>     |
| lseg(box)    | lseg       | Box diagonal to line segment           | lseg(box'((-1,0),(1,0))')               | [(1,0),(-1,0)]                |
| lseg(point, point)     | lseg       | Points to line segment           | lseg(point   '(-1,0)', point '(1,0)')   | [(-1,0),(1,0)]          |
| path(polygon)    | path       | Polygon to path      | path(polygon   '((0,0),(1,1),(2,0))')   | ((0,0),(1,1),(2,0))             |
| point(double   precision, double precision) | point      | Construct point      | point(23.4,   -44.5)                    | (23.4,-44.5)         |
| point(box)                                  | point      | Center of box               | point(box   '((-1,0),(1,0))')           | (0,0)         |
| point(circle)                               | point      | Center of circle               | point(circle   '((0,0),2.0)')           | (0,0)            |
| point(lseg)                                 | point      | Center of line segment             | point(lseg   '((-2,0),(2,0))')          | (0,0)   |
| point(polygon)                              | point      | Center of polygon           | point(polygon   '((0,0),(1,1),(2,0))')  | (1,0.333333333333333)     |
| polygon(box)                                | polygon    | Box to 4-point polygon | polygon(box   '((0,0),(1,1))')          | ((0,0),(0,1),(1,1),(1,0))       |
| polygon(circle)                             | polygon    | Circle to 12-point polygon | polygon(circle   '((0,0),2.0)')         |    -         |
| polygon(npts, circle)                       | polygon    | Circle to n-point polygon  | polygon(12,   circle '((0,0),2.0)')     | ((-2,0),(-0.618033988749895,1.90211303259031),(1.61803398874989,1.17557050458495),(1.6180339887499,-1.17557050458495),(-0.618033988749894,-1.90211303259031)) |
| polygon(path)                               | polygon    | Path to polygon         | polygon(path   '((0,0),(1,1),(2,0))')   | ((0,0),(1,1),(2,0))       |

