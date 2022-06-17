This document introduces the basic syntax and examples of geospatial functions.

## Concepts

Geospatial functions support Well-Known Text (WKT) and Well-Known Binary (WKB) forms of geometries. For related concepts, see [Well-known text representation of geometry - Wikipedia](https://en.wikipedia.org/wiki/Well-known_text_representation_of_geometry).

| Geometry     | WKT Format                                   |
| ------------ | ------------------------------------------------------------ |
| Point           | POINT (0 0)                                                  |
| LineString         | LINESTRING (0 0, 1 1, 1 2)                                   |
| Polygon       | POLYGON ((0 0, 4 0, 4 4, 0 4, 0 0), (1 1, 2 1, 2 2, 1 2, 1 1)) |
| MultiPoint         | MULTIPOINT (0 0, 1 2)                                        |
| MultiLineString       | MULTILINESTRING ((0 0, 1 1, 1 2), (2 3, 3 2, 5 4))           |
| MultiPolygon   | MULTIPOLYGON (((0 0, 4 0, 4 4, 0 4, 0 0), (1 1, 2 1, 2 2, 1 2, 1 1)), ((-1 -1, -1 -2, -2 -2, -2 -1, -1 -1))) |
| GeometryCollection | GEOMETRYCOLLECTION (POINT(2 3), LINESTRING (2 3, 3 4))       |

Geometries default to plane geometries, in which the shortest distance between two points is a straight line. Geometries also support spherical geometries, where the shortest distance between two points is a great circle arc. You can use `to_spherical_geography()` to convert a plane geometry into a spherical geometry.
For example:
`ST_Distance(ST_Point(-71.0882, 42.3607), ST_Point(-74.1197, 40.6976))` calculates the distance between two points on a plane, and the result is 3.4577.
`ST_Distance(to_spherical_geography(ST_Point(-71.0882, 42.3607)), to_spherical_geography(ST_Point(-74.1197, 40.6976)))` calculates the distance between two points on a sphere, and the result is 312822.179.

When a length is calculated (for example, `ST_Distance()` and `ST_Length()`), the unit is meter. When an area is calculated (for example, `ST_Area()`), the unit is square meter.



## Constructing a Geometry

| Function                            | Return Value Type         | Description                                |
| -------------------------------- | ------------------ | ----------------------------------- |
| ST_Point(double, double) | Point        | Constructs a point.                      |
| ST_LineFromText(varchar) | LineString   | Constructs a LineString based on WKT text.   |
| ST_Polygon(varchar) | Polygon           | Constructs a polygon based on WKT text. |
| ST_GeometryFromText(varchar) | Geometry | Constructs a geometry based on WKT text. |
| ST_GeomFromBinary(varbinary)     | Geometry           | Constructs a geometry based on WKB representation.         |
| ST_AsText(Geometry) | varchar           | Converts a geometry into WKT format. |
| to_spherical_geography(Geometry) | SphericalGeography | Converts a plane geometry into a spherical geometry.  |
| to_geometry(SphericalGeography)  | Geometry           | Converts a spherical geometry into a plane geometry.  |



## Relationship Tests

| Function                              | Return Value Type | Description                                                         |
| --------------------------------- | ---------- | ------------------------------------------------------------ |
| ST_Contains(Geometry, Geometry) | boolean   | Returns `true` if and only if no points of the second geometry lie in the exterior of the first geometry, and at least one point of the interior of the first geometry lies in the interior of the second geometry. Returns `false` if the second geometry lies exactly on the boundary of the first geometry. |
| ST_Crosses(Geometry, Geometry) | boolean    | Returns `true` if the given geometries have some, but not all, interior points in common.                         |
| ST_Disjoint(Geometry, Geometry) | boolean   | Returns `true` if the given geometries do not spatially intersect.                         |
| ST_Equals(Geometry, Geometry) | boolean     | Returns `true` if the given geometries represent the same geometry.                             |
| ST_Intersects(Geometry, Geometry) | boolean | Returns `true` if the given geometries spatially intersect in two dimensions.                     |
| ST_Overlaps(Geometry, Geometry) | boolean   | Returns `true` if the given geometries are of the same dimension, but are not completely contained by each other.           |
| ST_Relate(Geometry, Geometry) | boolean     | Returns `true` if the first geometry is spatially related to the second geometry.                                 |
| ST_Touches(Geometry, Geometry) | boolean    | Returns `true` if a geometry spatially touches another geometry, but their interiors do not intersect.       |
| ST_Within(Geometry, Geometry) | boolean     | Returns `true` if first geometry is completely inside the second geometry. Return `false` if their boundaries intersect. |



## Operations

| Function                                        | Return Value Type        | Description                                                         |
| ------------------------------------------- | ----------------- | ------------------------------------------------------------ |
| geometry_nearest_points(Geometry, Geometry) | row(Point, Point) | Returns the two closest points between two geometries.                         |
| geometry_union(array(Geometry))             | Geometry          | Combines multiple geometries into one.                           |
| ST_Boundary(Geometry) | Geometry                | Returns the boundary (closure) of a geometry.                                         |
| ST_Buffer(Geometry, distance) | Geometry        | Returns a geometric object that represents the union of all points whose distance from a geometry is less than or equal to a specified value. |
| ST_Difference(Geometry, Geometry) | Geometry    | Returns the geometry value that represents the point set difference of the two given geometries.                           |
| ST_Envelope(Geometry) | Geometry                | Returns the bounding rectangular polygon of the geometry.                                   |
| ST_ExteriorRing(Geometry) | Geometry            | Returns the exterior ring of the input polygon.                                         |
| ST_Intersection(Geometry, Geometry) | Geometry  | Returns the geometry value that represents the point set intersection of two given geometries.                                   |
| ST_SymDifference(Geometry, Geometry) | Geometry | Returns the geometry value that represents the point set symmetric difference of two geometries. |



## Accessors

| Function                                        | Return Value Type        | Description                                                         |
| --------------------------------------------------- | ---------- | ----------------------------------------------------------- |
| ST_Area(Geometry)                                   | double     | Returns the area of a polygon in a plane geometry.                                |
| ST_Area(SphericalGeography)                         | double     | Returns the area of a polygon in a spherical geometry.                                |
| ST_Centroid(Geometry)                               | Geometry   | Returns the point value that is the mathematical centroid of a geometry.                                      |
| ST_CoordDim(Geometry)                               | bigint     | Returns the coordinate dimension of the geometry.                                    |
| ST_Dimension(Geometry) | bigint          | Returns the inherent dimension of this geometry, which must be less than or equal to the coordinate dimension.             |
| ST_Distance(Geometry, Geometry) | double | Returns the minimum distance between two geometries.                                 |
| ST_Distance(SphericalGeography, SphericalGeography) | double     | Returns the smallest distance between two spherical geographies.                      |
| ST_IsClosed(Geometry) | boolean          | Returns `true` if the start and end points of the given geometry are the same.                           |
| ST_IsEmpty(Geometry) | boolean           | Returns `true` if the geometry is an empty GeometryCollection, polygon, point etc.   |
| ST_IsRing(Geometry) | boolean            | Returns `true` if and only if the geometry is a closed and simple line.           |
| ST_Length(Geometry)                                 | double     | Returns the length of a LineString or MultiLineString on a plane geometry.              |
| ST_Length(SphericalGeography)                       | double     | Returns the length of a LineString or MultiLineString on a spherical geometry.              |
| ST_XMax(Geometry)                                   | double     | Returns the X maxima of a bounding box of a geometry.                                 |
| ST_YMax(Geometry)                                   | double     | Returns the Y maxima of a bounding box of a geometry.                                 |
| ST_XMin(Geometry)                                    | double     | Returns the X minima of a bounding box of a geometry.                                 |
| ST_YMin(Geometry)                                   | double     | Returns the Y minima of a bounding box of a geometry.                                 |
| ST_StartPoint(Geometry)                             | point      | Returns the first point of a LineString geometry.                               |
| ST_EndPoint(Geometry)                             | point      | Returns the last point of a LineString geometry.                               |
| ST_X(Point)                                         | double     | Returns the X coordinate of the point.                                         |
| ST_Y(Point)                                         | double     | Returns the Y coordinate of the point.                                         |
| ST_NumPoints(Geometry)                              | bigint     | Returns the number of points in a geometry.                                    |
| ST_NumInteriorRing(Geometry) | bigint    | Returns the number of the interior rings of a polygon.                                   |
