This document introduces the basic syntax and examples of geospatial functions.

## Geospatial Concepts

Geospatial functions support geometries in Well-Known Text (WKT) format.

| Geometry     | WKT Format                                   |
| ------------ | ------------------------------------------------------------ |
| Point           | POINT (0 0)                                                  |
| LineString         | LINESTRING (0 0, 1 1, 1 2)                                   |
| Polygon       | POLYGON ((0 0, 4 0, 4 4, 0 4, 0 0), (1 1, 2 1, 2 2, 1 2, 1 1)) |
| MultiPoint         | MULTIPOINT (0 0, 1 2)                                        |
| MultiLineString       | MULTILINESTRING ((0 0, 1 1, 1 2), (2 3, 3 2, 5 4))           |
| MultiPolygon   | MULTIPOLYGON (((0 0, 4 0, 4 4, 0 4, 0 0), (1 1, 2 1, 2 2, 1 2, 1 1)), ((-1 -1, -1 -2, -2 -2, -2 -1, -1 -1))) |
| GeometryCollection | GEOMETRYCOLLECTION (POINT(2 3), LINESTRING (2 3, 3 4))       |



## Constructors

| Function                                            | Description                                                         |
| --------------------------------------- | --------------------------------- |
| ST_Point(double, double) → Point        | Constructs a point.                      |
| ST_LineFromText(varchar) → LineString   | Constructs a LineString based on WKT text.   |
| ST_Polygon(varchar) → Polygon           | Constructs a polygon based on WKT text. |
| ST_GeometryFromText(varchar) → Geometry | Constructs a geometry based on WKT text. |
| ST_AsText(Geometry) → varchar           | Converts a geometry into WKT format. |



## Operators

| Function                                            | Description                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| ST_Boundary(Geometry) → Geometry                | Returns the boundary (closure) of a geometry.                                         |
| ST_Buffer(Geometry, distance) → Geometry        | Returns a geometric object that represents the union of all points whose distance from a geometry is less than or equal to a specified value. |
| ST_Difference(Geometry, Geometry) → Geometry    | Returns the geometry value that represents the point set difference of the two given geometries.                           |
| ST_Envelope(Geometry) → Geometry                | Returns the bounding rectangular polygon of the geometry.                                   |
| ST_ExteriorRing(Geometry) → Geometry            | Returns the exterior ring of the input polygon.                                         |
| ST_Intersection(Geometry, Geometry) → Geometry  | Returns the geometry value that represents the point set intersection of two given geometries.                                   |
| ST_SymDifference(Geometry, Geometry) → Geometry | Returns the geometry value that represents the point set symmetric difference of two geometries. |



### Relationship Tests

| Function                                            | Description                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| ST_Contains(Geometry, Geometry) → boolean   | Returns `true` if and only if no points of the second geometry lie in the exterior of the first geometry, and at least one point of the interior of the first geometry lies in the interior of the second geometry. Returns `false` if the second geometry lies exactly on the boundary of the first geometry. |
| ST_Crosses(Geometry, Geometry) → boolean    | Returns `true` if the given geometries have some, but not all, interior points in common.                         |
| ST_Disjoint(Geometry, Geometry) → boolean   | Returns `true` if the given geometries do not spatially intersect.                         |
| ST_Equals(Geometry, Geometry) → boolean     | Returns `true` if the given geometries represent the same geometry.                             |
| ST_Intersects(Geometry, Geometry) → boolean | Returns `true` if the given geometries spatially intersect in two dimensions.                     |
| ST_Overlaps(Geometry, Geometry) → boolean   | Returns `true` if the given geometries are of the same dimension, but are not completely contained by each other.           |
| ST_Relate(Geometry, Geometry) → boolean     | Returns `true` if the first geometry is spatially related to the second geometry.                                 |
| ST_Touches(Geometry, Geometry) → boolean    | Returns `true` if a geometry spatially touches another geometry, but their interiors do not intersect.       |
| ST_Within(Geometry, Geometry) → boolean     | Returns `true` if first geometry is completely inside the second geometry. Return `false` if their boundaries intersect. |



### Accessors

| Function                                     | Description                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| ST_Area(Geometry) → double               | Calculates the area of a polygon projected on a two dimensional plane using Euclidean measurement.       |
| ST_Centroid(Geometry) → Geometry         | Returns the point value that is the mathematical centroid of a geometry.                                       |
| ST_CoordDim(Geometry) → bigint           | Returns the coordinate dimension of a geometry.                                     |
| ST_Dimension(Geometry) → bigint          | Returns the inherent dimension of this geometry, which must be less than or equal to the coordinate dimension.             |
| ST_Distance(Geometry, Geometry) → double | Returns the minimum distance between two geometries.                                 |
| ST_IsClosed(Geometry) → boolean          | Returns `true` if the start and end points of the given geometry are the same.                           |
| ST_IsEmpty(Geometry) → boolean           | Returns `true` if the geometry is an empty GeometryCollection, polygon, point etc.   |
| ST_IsRing(Geometry) → boolean            | Returns `true` if and only if the geometry is a closed and simple line.           |
| ST_Length(Geometry) → double             | Returns the length of a LineString or Multi-LineString using Euclidean measurement on a 2D plane (based on spatial reference) in projected units. |
| ST_XMax(Geometry) → double               | Returns the maximum X-coordinate value of the bounding box of the geometry.                                    |
| ST_YMax(Geometry) → double               | Returns the maximum Y-coordinate value of the bounding box of the geometry.                                    |
| T_XMin(Geometry) → double               | Returns the minimum X-coordinate value of the bounding box of the geometry.                                    |
| ST_YMin(Geometry) → double               | Returns the minimum Y-coordinate value of the bounding box of the geometry.                                    |
| ST_StartPoint(Geometry) → point          | Returns the first point of a LineString geometry.                               |
| ST_EndPoint(Geometry) → point          | Returns the last point of a LineString geometry.                               |
| ST_X(Point) → double                     | Returns the X coordinate of a point.                                            |
| ST_Y(Point) → double                     | Returns the Y coordinate of a point.                                            |
| ST_NumPoints(Geometry) → bigint          | Returns the number of points in a geometry.                                     |
| ST_NumInteriorRing(Geometry) → bigint    | Returns the number of the interior rings of a polygon.                                   |

