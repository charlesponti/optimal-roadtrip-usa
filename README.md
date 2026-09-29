# The restored optimal road trip maps

These are the interactive maps from the "optimal road trip" projects that Randal S. Olson published between 2015 and 2018. They were restored in 2026 and work again.

The site is served with GitHub Pages at <https://rhiever.github.io/optimal-roadtrip-usa/>. Every map keeps its original URL, so old links, blog embeds and bookmarks land on a working page. Start at [`index.html`](index.html), which lists every map.

## Why the maps broke

The original pages drew each route live in the browser by calling the Google Maps JavaScript API's Directions service, without an API key. Google later required a key and a billing account for every request. From then on each request came back `REQUEST_DENIED`, and the pages showed an empty map with no route.

## How they were restored

Nothing here calls Google or any other outside service. Each page loads only files from this repository.

1. The ordered stop list was parsed out of each original page. Every stop was re-verified against Wikidata, Wikipedia, the National Park Service and OpenStreetMap, and given a coordinate for the landmark itself and a separate "drive point" where a car can actually arrive (a parking lot, a visitor center or a ferry terminal). The stops and their order are exactly as originally published. Nothing was re-optimized.
2. Each leg was routed on [OpenStreetMap](https://www.openstreetmap.org/) road data with [OSRM](https://project-osrm.org/) (car profile for road trips, foot profile for the walking tours), using a pinned OSM snapshot recorded in each page's `trip.json`. Legs that cannot be driven, such as the flights in the South America trip, are drawn as dashed straight lines labeled "flight or ferry". Where a stop's drive point is more than about 1 km from the landmark (Santorini is reached from the port of Piraeus, the Statue of Liberty from the Battery), a dotted line joins them, and the stop's popup says how it is reached.
3. The basemap is a [Protomaps](https://protomaps.com/) vector tile extract in a single PMTiles file, drawn with [MapLibre GL JS](https://maplibre.org/). The lower 48 states go down to zoom 8 (a 51 MB file) and the world basemap, used where no regional extract covers a route, to zoom 5. You can zoom in further; the route line stays sharp because it is vector data, but the basemap shows less detail past those levels. Fonts and map icons are served from this repository too.
4. Every map offers GPX, KML and GeoJSON files, plus links that open the route in Google Maps or Apple Maps. Those links split long routes into parts, because both apps take only a limited number of stops per link.

Distances and driving times are recomputed on today's road data, so they can differ from the figures quoted in the original posts.

### Embedding a map

Add `?embed=1` to any map URL for a map-only view with a small title card, suitable for an iframe. Scrolling over an embedded map scrolls the page: hold Ctrl (or Cmd) while scrolling to zoom the map, and use two fingers to move it on a touch screen.

## What is in this repository

| Path | Contents |
|---|---|
| `index.html` | List of every restored map |
| `<map>.html` | One page per map, at its original filename |
| `images/`, `*-google.md` | Unused by the restored pages; kept for compatibility with old links |
| `data/<map>/` | Per-map data: `trip.json` (stops, totals, build info), `route.geojson`, `route.gpx`, `route.kml` |
| `assets/` | Page script and styles, MapLibre, fonts, map icons and the `.pmtiles` basemaps |

The pages are built from a separate, private build pipeline. This repository holds only the static output.

The 47 state-capitol Pareto-front maps from the 2016 post "Computing optimal road trips on a limited budget" are a separate project with their own repository: [optimized-us-capitol-road-trip](https://github.com/rhiever/optimized-us-capitol-road-trip), served at <https://rhiever.github.io/optimized-us-capitol-road-trip/road-trip-maps/>.

## Licenses

- Code (the HTML pages and `assets/app.js`, `assets/style.css`): MIT License, the same license as the original project. See [`LICENSE`](LICENSE).
- Route and stop data (everything under `data/`, including the GPX, KML and GeoJSON downloads): derived from OpenStreetMap, so it is available under the [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/). If you reuse it, credit "© OpenStreetMap contributors" and share any adapted database under the ODbL.
- Basemap tiles (`assets/basemaps/*.pmtiles`): built by Protomaps from OpenStreetMap (ODbL) and Natural Earth (public domain).
- Written content of the original project (titles and descriptions): CC BY 4.0, by Randal S. Olson.

Third-party components shipped in `assets/`, each under its own license:

| Component | License |
|---|---|
| [MapLibre GL JS](https://github.com/maplibre/maplibre-gl-js) | BSD-3-Clause (`assets/vendor/maplibre/LICENSE.txt`) |
| [PMTiles](https://github.com/protomaps/PMTiles) JavaScript library | BSD-3-Clause (bundled in `assets/app.js`) |
| [@protomaps/basemaps](https://github.com/protomaps/basemaps) map style | BSD-3-Clause (bundled in `assets/app.js`) |
| Noto Sans glyphs from [protomaps/basemaps-assets](https://github.com/protomaps/basemaps-assets) | SIL Open Font License 1.1 (`assets/fonts/OFL.txt`) |
| Map icons from protomaps/basemaps-assets | MIT, derived from [tangrams/icons](https://github.com/tangrams/icons) |

## Attribution

- Map and route data © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), under the ODbL.
- Basemap by [Protomaps](https://protomaps.com/).
- Rendering by [MapLibre](https://maplibre.org/). Routing by [OSRM](https://project-osrm.org/).
- Original road trips, code and writing by [Randal S. Olson](https://www.randalolson.com/).
