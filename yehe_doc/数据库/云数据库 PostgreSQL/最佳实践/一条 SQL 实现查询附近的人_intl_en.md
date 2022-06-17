PostGIS is an extension of the PostgreSQL relational database. It follows the specifications of OpenGIS and provides the following spatial information service features: spatial objects, indexes, operation functions, and operators.

PostGIS supports all spatial data types, including POINT, LINESTRING, POLYGON, MULTIPOINT, MULTILINESTRING, MULTIPOLYGON, and GEOMETRYCOLLECTION.

PostGIS is also the most comprehensive and powerful spatial and geographic database engine in the industry. Many business use cases nowadays require the "XXX nearby" feature. PostGIS and PostgreSQL can work together to implement this feature quickly.

This document describes how to implement the "objects nearby" feature with PostGIS.

## Prerequisites
- You have a PostgreSQL instance.
- This instance supports the PostGIS extension.

## Step 1. Create the extension
Log in to the business database instance and run the following commands. For the login methods, see [Connecting to TencentDB for PostgreSQL Instance](https://intl.cloud.tencent.com/document/product/409/34626).
```
\c test
CREATE EXTENSION postgis;
CREATE EXTENSION postgis_topology;
```

## Step 2. Create a test table and an index
Run the following commands in the business database. You can customize the name after `TABLE`.
```
CREATE TABLE t_user(uid int PRIMARY KEY,name varchar(20),location geometry);
CREATE INDEX t_user_location on t_user USING GIST(location);
```

## Step 3. Insert test data
```
## Create an automatic name generation function
create or replace function random_string(length integer) returns text as
$$
declare
chars text[] := '{0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z,a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z}';
result text := '';
i integer := 0;
length2 integer := (select trunc(random() * length + 1));
begin
if length2 < 0 then
raise exception 'Given length cannot be less than 0';
end if;
for i in 1..length2 loop
result := result || chars[1+random()*(array_length(chars, 1)-1)];
end loop;
return result;
end;
$$ language plpgsql;

## Insert ten million rows of test data
insert into t_user select generate_series(1,10000000), random_string(20),st_setsrid(st_makepoint(150-random()*100, 90-random()*100), 4326);
```

## Step 4. Query people nearby
1. Select a random coordinate [here](http://api.map.baidu.com/lbsapi/getpoint/). The coordinate of Tiananmen Square (116.404177,39.909652) is used as an example.
2. Use it as the coordinate for query to find the five objects closest to it in the database, and then output the distances of these objects from it (in 00' km).
>?WGS 84 is the most popular geographic coordinate system. Internationally, each coordinate system is assigned an EPSG code, which is 4326 for WGS 84. GPS is based on WGS 84, so the coordinate data obtained is usually in WGS 84 and generally stored as WGS 84.
>
Run the following command:
```
select uid, name, ST_AsText(location), ST_Distance(ST_GeomFromText('POINT(116.404177 39.909652)',4326), location) from t_user order by location <-> 'SRID=4326;POINT(116.404177 39.909652)'::geometry limit 5;
```
3. View all objects within 1000 meters of this coordinate object and their distances.
```
select uid, name, ST_AsText(location),ST_Distance(ST_GeomFromText('POINT(116.404177 39.909652)',4326), location) from t_user where ST_DWithin(location::geography, ST_GeographyFromText('POINT(116.404177 39.909652)'), 1000.0);
```
