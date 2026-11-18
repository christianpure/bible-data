# Paul's missionary journeys: stops, legs and places

These files trace Paul's three missionary journeys and his voyage to Rome, stop by stop, as the Acts of the Apostles tells them. Each stop has its coordinates and the verse that puts Paul there, and each leg between two stops has its distance by Roman road and by sea, how far the road climbs, and the days Acts gives where it gives any. It is the data behind our map at [christianpure.com/pauls-missionary-journeys](https://christianpure.com/pauls-missionary-journeys/).

The four journeys come to 69 stops, 65 legs and 48 places, and about 15,070 km (9,365 miles) in all: 7,149 km by road, 32 km of short connecting lines and 7,891 km by sea.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `journeys.csv` | 4 | One row per journey, with its chapters in Acts, its approximate years and its total distances. |
| `stops.csv` | 69 | Every stop in order, with coordinates, its verse in the World English Bible, our note, and any line from Paul's letters that recalls the visit. |
| `stop-verses.csv` | 120 | Every verse quoted for a stop, one per row, with its text. |
| `legs.csv` | 65 | Every leg between two stops: kilometres by road, connecting line and sea; days on foot; climb, descent and highest point; how much of the road the Itiner-e atlas grades certain or conjectured; and the days Acts gives. |
| `places.csv` | 48 | Every place, with the OpenBible.info record its point comes from and the Pleiades and Wikidata records matched to it. |
| `stops.geojson` | 69 points | The stops, with the fields of `stops.csv` and their other verses. |
| `legs.geojson` | 65 lines | The legs as drawn on the map, one MultiLineString each (one line per road or sea part), with the fields of `legs.csv`. |
| `datapackage.json` | | The same description in [Frictionless Data](https://specs.frictionlessdata.io/data-package/) form: every field, its type and the keys that join the tables. |

The CSV files are UTF-8 with a header row, comma separated, and lists inside a cell are separated by a semicolon and a space. Coordinates are WGS 84 decimal degrees; GeoJSON gives them in its usual order, longitude first. A journey's stops and legs are joined by `journey_id` and their order: leg 3 runs from stop 3 to stop 4.

## Fields

### journeys.csv

<!-- fields: journeys -->
| Field | Type | What it holds |
| --- | --- | --- |
| `journey_id` | string (required) | Short id of the journey: first, second, third or rome. |
| `journey_order` | integer (required) | Order of the journey, 1 to 4. |
| `name` | string (required) | Name of the journey. |
| `bible_refs` | string (required) | The chapters of Acts the journey covers. |
| `bible_refs_osis` | string (required) | The same range in OSIS notation. |
| `years` | string (required) | Approximate years, as scholars reconstruct them. |
| `stop_count` | integer (required) | Number of stops (rows in stops.csv). |
| `leg_count` | integer (required) | Number of legs (rows in legs.csv). |
| `road_km` | integer (required) | Kilometres on Roman roads (Itiner-e network), all legs. |
| `drawn_km` | integer (required) | Kilometres of straight line drawn where a place lies off the road network. |
| `sea_km` | integer (required) | Kilometres by sea, all legs. |
| `total_km` | integer (required) | road_km + drawn_km + sea_km. |
<!-- /fields -->

### stops.csv

<!-- fields: stops -->
| Field | Type | What it holds |
| --- | --- | --- |
| `journey_id` | string (required) | Journey (journeys.csv). |
| `stop_order` | integer (required) | Order of the stop within its journey, from 1. |
| `stop_id` | string (required) | Id of the stop, unique within its journey. A place visited twice has a suffix such as -2. |
| `place_id` | string (required) | Place (places.csv). |
| `label` | string (required) | Name shown on the map. Where Acts names a region, the region. |
| `kind` | string (required) | stop: Acts has Paul stop or work here. pass: passed or touched on the way. reading: Acts names a region or leaves the place open, and the place is our reading. |
| `latitude` | number (required) | WGS 84 latitude of the place. |
| `longitude` | number (required) | WGS 84 longitude of the place. |
| `bible_ref` | string (required) | The verse in Acts (or a letter) that puts Paul here. |
| `bible_ref_osis` | string (required) | The same verse in OSIS notation. |
| `verse_text` | string (required) | Text of bible_ref in the World English Bible (public domain). |
| `note` | string | Our one-line note on what happens here. Empty for some passing stops. |
| `also_refs` | string | Other verses for this stop, separated by "; ". Their texts are in stop-verses.csv. |
| `letter_ref` | string | A verse from one of Paul’s letters that recalls this visit, if any. |
| `letter_ref_osis` | string | The same verse in OSIS notation. |
| `letter_text` | string | Text of letter_ref in the World English Bible. |
| `letter_why` | string | Our note on how the letter connects to the visit. |
| `letter_is_reading` | boolean | true where the link between letter and visit rests on a disputed reading. |
<!-- /fields -->

### stop-verses.csv

<!-- fields: stop-verses -->
| Field | Type | What it holds |
| --- | --- | --- |
| `journey_id` | string (required) | Journey (journeys.csv). |
| `stop_order` | integer (required) | Stop (stops.csv), by its order in the journey. |
| `stop_id` | string (required) | Id of the stop. |
| `role` | string (required) | main: the stop’s own verse. also: another verse for the stop. letter: a verse from a letter. |
| `bible_ref` | string (required) | Bible reference. |
| `bible_ref_osis` | string (required) | The same reference in OSIS notation. |
| `text` | string (required) | Text in the World English Bible (public domain). Some are part of a verse. |
<!-- /fields -->

### legs.csv

<!-- fields: legs -->
| Field | Type | What it holds |
| --- | --- | --- |
| `journey_id` | string (required) | Journey (journeys.csv). |
| `leg_order` | integer (required) | Order of the leg within its journey, from 1. Leg n runs from stop n to stop n+1. |
| `from_stop_id` | string (required) | Stop the leg starts from. |
| `to_stop_id` | string (required) | Stop the leg ends at. |
| `from_place_id` | string (required) | Place the leg starts from. |
| `to_place_id` | string (required) | Place the leg ends at. |
| `from_label` | string (required) | Name of the start. |
| `to_label` | string (required) | Name of the end. |
| `mode` | string (required) | How the leg is travelled: road, sea, or foot (Acts 20:13, where Paul walks while the ship sails round). A sea leg may begin or end with a short road part. |
| `road_km` | integer (required) | Kilometres on the Itiner-e Roman road network. |
| `drawn_km` | integer (required) | Kilometres of straight line joining a place to the network. |
| `sea_km` | integer (required) | Kilometres of our drawn sea line. |
| `total_km` | integer (required) | road_km + drawn_km + sea_km. |
| `days_on_foot` | number | Land kilometres divided by 29.6 km a day (20 Roman miles, Vegetius 1.9). Empty for legs wholly at sea. An assumption, not a record. |
| `climb_m` | integer | Metres climbed on the land part. |
| `descent_m` | integer | Metres descended on the land part. |
| `highest_m` | integer | Highest point of the land part, in metres. |
| `road_certain_km` | integer | Road kilometres that Itiner-e grades certain. Empty where the leg has no road. |
| `road_conjectured_km` | integer | Road kilometres that Itiner-e grades conjectured. |
| `road_hypothetical_km` | integer | Road kilometres that Itiner-e grades hypothetical. |
| `itinere_roads` | string | Names of the Itiner-e road segments used, in order, separated by "; ". |
| `acts_days` | integer | Days Acts itself gives for this stretch, if any. |
| `acts_days_approximate` | boolean | true where the days are not a stated journey time (the storm before Malta). |
| `acts_days_from_stop_id` | string | Where the days in Acts are counted from, which can be an earlier stop. |
| `acts_ref` | string | The verse that gives the days. |
| `acts_ref_osis` | string | The same verse in OSIS notation. |
| `acts_quote` | string | That verse in the World English Bible. |
<!-- /fields -->

### places.csv

<!-- fields: places -->
| Field | Type | What it holds |
| --- | --- | --- |
| `place_id` | string (required) | Id of the place. |
| `name` | string (required) | Name of the place as first labelled on the map. |
| `on_route` | boolean (required) | false for Tarsus, Paul’s home city, which the map marks but no journey stops at. |
| `latitude` | number (required) | WGS 84 latitude, from OpenBible.info. |
| `longitude` | number (required) | WGS 84 longitude, from OpenBible.info. |
| `openbible_id` | string (required) | Id of the OpenBible.info ancient place record the point comes from. |
| `openbible_name` | string (required) | Name of that OpenBible.info record. |
| `openbible_identification` | string (required) | The modern site OpenBible.info identifies the place with. |
| `openbible_other_candidate_sites` | integer (required) | How many other candidate sites OpenBible.info lists. |
| `wikidata_id` | string | Wikidata item, from OpenBible.info. |
| `pleiades_id` | string | Pleiades place matched to the point, if one lies near. Empty where none matched. |
| `pleiades_title` | string | Title of the Pleiades place. |
| `pleiades_offset_km` | number | Kilometres between the OpenBible.info point and the Pleiades point. |
| `pleiades_url` | string | Address of the Pleiades place. |
<!-- /fields -->

## How it was made

We wrote the journeys by hand from Acts: each stop, the verse that names it, a one-line note, and where it helps, a line from one of Paul's letters. The verses are quoted from the World English Bible, and every reference and quotation in these files has been checked against that translation's text.

Each place takes its point from the OpenBible.info Bible Geocoding Data, which identifies each biblical place with a modern site and says how many other candidate sites there are. We then matched each point to the nearest Pleiades place, where one lies close, and kept the distance between the two so you can judge the match.

Road legs follow the shortest path between the two places on the Roman road network of Itiner-e, the digital atlas of ancient roads. Where a place lies off that network, a short straight line joins it, and its length is counted in `drawn_km`. Sea legs are our own lines: the shortest open water between the two places, kept off the coast and passing the places Acts says the ship passed. Four points shape the sea lines for that reason: off Pieria, where Acts 17:14 sends Paul "to the sea" from Berea; south of Cyprus, which they left "on the left hand" (Acts 21:3); and north of Cyprus and along the coast of Cilicia and Pamphylia on the voyage to Rome (Acts 27:4–5). Islands and silted harbours are reached by sea, never overland.

Days on foot divide the land kilometres by 29.6 km, the 20 Roman miles that Vegetius (*Epitoma rei militaris* 1.9) says recruits had to march in five summer hours. It is our assumption, not a record of how fast Paul walked. Heights come from the Terrain Tiles on AWS (SRTM, GMTED2010, ETOPO1 and the Copernicus EU-DEM) at a coarse resolution, so climbs and descents are approximate, and the highest point of a road leg comes from the heights Itiner-e stores.

The years are a reconstruction, and every one says "about". Their fixed point is Gallio, who was proconsul of Achaia while Paul was in Corinth (Acts 18:12) and whom an inscription at Delphi dates to about AD 52.

## Known gaps

- **The routes are reconstructions.** Acts names where Paul went, seldom how. The road lines take the shortest Roman road we know of, and Itiner-e grades only 1,128 of their 7,149 km as certain; the rest is conjectured. The sea lines are drawn by us.
- **Six stops are our reading,** marked `reading` in `kind`, because Acts names a region or leaves the place open: "Phrygia and Galatia" (Acts 16:6) and "Galatia and Phrygia" (Acts 18:23), drawn through Antioch in Pisidia; "went up and greeted the assembly" (Acts 18:22), which most read as Jerusalem; Troas on the third journey, which comes from 2 Corinthians 2:12; "Macedonia" (Acts 20:1), drawn to Philippi; and "Greece" (Acts 20:2–3), which most read as Corinth.
- **Two letter lines rest on a disputed reading** (`letter_is_reading`): Galatians 4:13 at Antioch in Pisidia, which holds if "Galatians" means the southern towns, and Romans 16:23 at Corinth.
- **Eight places have no Pleiades match** near the OpenBible.info point: Seleucia, Berea, Cnidus, Salmone, Cauda, Malta, Syracuse and Rhegium. For Samothrace the nearest Pleiades place is 7.2 km away.
- **Two places have other candidate sites** in OpenBible.info: Derbe (two others) and Rhodes (one). We use OpenBible.info's first identification.
- **Tarsus is listed but not visited.** The map marks Paul's home city, so it is in `places.csv` with `on_route` false; no journey stops there.
- `road_hypothetical_km` is 0 on every leg, because no road we use is graded hypothetical. We kept the column so the three grades always add up to the road distance, give or take a kilometre of rounding.

## Sources and their licenses

When you reuse these files, please keep the credits of the sources they draw on, which their licenses ask for:

- **OpenBible.info**, Bible Geocoding Data, [openbible.info/geo](https://www.openbible.info/geo/), CC BY 4.0: the place points and their identifications.
- **Pleiades**, [pleiades.stoa.org](https://pleiades.stoa.org/), CC BY 3.0: the matched places.
- **Itiner-e**: "Itiner-e: the digital atlas of ancient roads © 2024 by Brughmans, Pažout, de Soto and Bjerregaard Vahlstrup is licensed under CC BY 4.0", [doi.org/10.5281/zenodo.17122148](https://doi.org/10.5281/zenodo.17122148): the road network, its names and certainty grades, and road heights.
- **World English Bible**, [ebible.org](https://ebible.org/find/details.php?id=eng-web), public domain: every verse quoted.
- **Terrain Tiles on AWS**, [registry.opendata.aws/terrain-tiles](https://registry.opendata.aws/terrain-tiles/): heights, from SRTM and GMTED2010 (U.S. Geological Survey), ETOPO1 (U.S. National Oceanic and Atmospheric Administration) and the EU-DEM (produced using Copernicus data and information funded by the European Union).

## License and credit

Our journeys, notes, route lines, distances and the way these tables are put together are released under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0); the full text is in `LICENSE`. You may copy, change and build on them for any purpose, commercial or not. The license asks you to name Christian Pure as the source, and a plain-text credit is enough, for example:

> Paul's journeys data by Christian Pure, CC BY 4.0, building on OpenBible.info, Pleiades and Itiner-e.

If you use this, we'd be grateful for a credit link to [https://christianpure.com/pauls-missionary-journeys/](https://christianpure.com/pauls-missionary-journeys/), where the map is. That is a request, not a condition: a credit without a link is fine, and any link may carry nofollow.

To cite the data in a paper, see `CITATION.cff` at the top of this repository, or use:

> Christian Pure. "Paul's Missionary Journeys: Stops, Legs and Places." Version 1.0.0, 18 November 2026. https://christianpure.com/pauls-missionary-journeys/.

Found a mistake? Please open an issue in this repository. Corrections to our pages are logged on [our editorial standards page](https://christianpure.com/editorial-standards/).
