osmpoly
=======

Polygons for OSM extracts

Based on the TIGER 2012 State Boundary shapefile.

Load shapefile into a PostGIS database:

    shp2pgsql -s 4326 -I -W LATIN1 tl_2012_us_state.shp states12 > tl_2012_us_state.sql
    psql -U osm -d tiger -f tl_2012_us_state.sql

Extract the buffered dissolved polygon:

    pgsql2shp -f /osm/us_buf01.poly -u osm -P osm tiger "SELECT sum(aland), ST_Simplify(ST_Buffer(ST_Union(geom),0.1),0.1) from states12;"

Load into JOSM and save as POLY

That's the POLY file in this repo. 
