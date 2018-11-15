---
layout: post
title: OSM Data Import
---

Requirements

```bash
brew install postgresql postgis osm2pgsql
```

PostgreSQL setup

```bash
createuser osm -l -P
createdb -O osm osm_wa
psql -c "create extension postgis; create extension hstore;" osm_wa

# You don't need to do the following, but it can help when this role is used for other services
psql -c "ALTER TABLE geometry_columns OWNER TO osm;
ALTER TABLE geography_columns OWNER TO osm;
ALTER TABLE raster_columns OWNER TO osm;
ALTER TABLE raster_overviews OWNER TO osm;
ALTER TABLE spatial_ref_sys OWNER TO osm;" osm_wa
```

Data download and import

```bash
cd
mkdir osm && cd osm
curl -O https://download.geofabrik.de/north-america/us/washington-latest.osm.pbf
osm2pgsql -c -d osm_wa -U osm washington-latest.osm.pbf
```

Viewing data in QGIS3 can be done by manually adding the PostgreSQL data source, adding any of `planet_osm_[point|line|polygon]` then filtering on some attribute. You can also accomplish this programmatically in the python console:

```python
tablename = "planet_osm_polygon"
geometrycol = "way"

from qgis.core import QgsVectorLayer, QgsDataSourceUri
uri = QgsDataSourceUri()
uri.setConnection("localhost", "5432", "osm_wa", "osm", "password")
uri.setDataSource ("public", tablename, geometrycol, "leisure = 'park'")
vlayer=QgsVectorLayer (uri .uri(False), tablename, "postgres")
QgsProject.instance().addMapLayer(vlayer)
```
