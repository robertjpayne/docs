---
layout: api-command
language: Ruby
permalink: api/ruby/geojson/
command: geojson
related_commands:
    to_geojson: to_geojson/
---
# Command syntax #

{% apibody %}
r.geojson(geojson) &rarr; geometry
{% endapibody %}

# Description #

Convert a [GeoJSON](http://geojson.org) object to a ReQL geometry object.

RethinkDB only allows conversion of GeoJSON objects which have ReQL equivalents: Point, LineString, and Polygon. MultiPoint, MultiLineString, and MultiPolygon are not supported. (You could, however, store multiple points, lines and polygons in an array and use a geospatial multi index with them.)

Only longitude/latitude coordinates are supported. GeoJSON objects that use Cartesian coordinates, specify an altitude, or specify their own coordinate reference system will be rejected.

__Example:__ Convert a GeoJSON object to a ReQL geometry object.

```rb
geo_json = {
    :type => 'Point',
    :coordinates => [ -122.423246, 37.779388 ]
}
r.table('geo').insert({
    :id => 'sfo',
    :name => 'San Francisco',
    :location => r.geojson(geo_json)
}).run(conn)
```
