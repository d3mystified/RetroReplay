# RetroReplay

[![Hippocratic License HL3-BDS-ECO-EXTR-FFD-LAW-MIL](https://img.shields.io/static/v1?label=Hippocratic%20License&message=HL3-BDS-ECO-EXTR-FFD-LAW-MIL&labelColor=5e2751&color=bc8c3d)](https://firstdonoharm.dev/version/3/0/bds-eco-extr-ffd-law-mil.html)

Highlight your Plex media that originally aired in the past during the current week or month.

![](https://i.imgur.com/akwExaK.png)

The script updates lists on TMDb after filtering out low-rated content against MDBList. These lists are intended to be used with Kometa to create collections on Plex.

*Inspired by https://github.com/InsertDisc/pattrmm.*

## How to use

### Configure

Create `config.yml`:

```yaml
libraries:
  Movies:
    imdb_min_rating: 70
    imdb_min_votes: 50000
    range: week  # can be "day", "week", "month
    starting_year: 1990
    tmdb_list_id: 12345  # Create a list in your profile then copy the ID here
  TV Shows:
    imdb_min_rating: 70
    imdb_min_votes: 50000
    range: week  # can be "day", "week", "month
    starting_year: 2000
    tmdb_list_id: 12345  # Create a list in your profile then copy the ID here
mdblist:
  api_key: abc123  # Required
plex:
  token: abc123  # Required
  url: https://1234.com  # Required
tmdb:
  access_token: reallylongstring  # Get from https://www.themoviedb.org/settings/api
  api_key: abc123  # Get from https://www.themoviedb.org/settings/api
healthchecks:
  base_url: https://hc-ping.com/12345678-1234-1234-1234-123456789012
```

### Docker Compose

```yaml
  retroreplay:
    image: ghcr.io/d3mystified/retroreplay:main
    container_name: retroreplay
    environment:
      - PUID=1000
      - GUID=1000
      - TZ=America/Los_Angeles
      - CONFIG_FILE=/config/config.yml
      - RUN_AT=13:51  # Run at 1:51pm
    volumes:
      - /path/to/retroreplay:/config
    restart: always
```

After the container is created, you can also manually run the script with:

```bash
docker exec -it retroreplay python /app/main.py --run
```

### Configure Kometa

```yaml
collections:
  Released This Month In History:
    tmdb_list: 12345  # ID from above
    sync_mode: sync
    collection_order: random
    url_poster: https://raw.githubusercontent.com/Kometa-Team/Default-Images/refs/heads/master/chart/This%20Week%20in%20History.jpg
```
