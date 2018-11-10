---
layout: post
title: OSRM build quickstart
---

I've been working with OSRM data lately and find I'm constantly rebuilding my environment. So, here's my copy-paste source to do this easier for WA state.

Back end data download and setup
```bash
cd
mkdir osrm && cd osrm
curl -O https://download.geofabrik.de/north-america/us/washington-latest.osm.pbf
docker run -t -v $(pwd):/data osrm/osrm-backend osrm-extract -p /opt/foot.lua /data/washington-latest.osm.pbf
docker run -t -v $(pwd):/data osrm/osrm-backend osrm-partition /data/washington-latest.osrm
docker run -t -v $(pwd):/data osrm/osrm-backend osrm-customize /data/washington-latest.osrm
docker run -t -i -p 5000:5000 -v $(pwd):/data osrm/osrm-backend osrm-routed --algorithm mld /data/washington-latest.osrm
```

Front end setup
```bash
docker run -p 9966:9966 osrm/osrm-frontend
```

Voila, you've got a routing front end at http://localhost:9966

Source: https://hub.docker.com/r/osrm/osrm-backend/
