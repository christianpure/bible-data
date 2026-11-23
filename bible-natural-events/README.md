# Earthquakes, eclipses and famines in the Bible, set against the scientific record

These files take every natural event the Bible names that the scientific record could speak to (earthquakes, eclipses and darkness, famines and droughts), add two from early church writers, and look for each one in earthquake catalogues, NASA's eclipse canons and climate records. Each event gets one of four grades, the record that comes closest, how common such events were at that place and time, the nearest active fault for earthquakes, and every source consulted.

Rows with no match stay in. A table that keeps its misses lets you judge its matches.

Version 1.0.0 holds 25 events: 2 strong matches, 6 possible matches, 4 with no match found, and 13 beyond the records.

## The four grades

| Grade | What it means |
| --- | --- |
| **Strong match** | An independently dated record places an event of this kind at or near the place the passage names, and the record's date range lies inside the passage's. |
| **Possible match** | A record overlaps the passage in date and lies in the same region, but its date range is wider than the passage's, it shows only regional effects, or its date is disputed. |
| **No match found** | The records reach this time and place and hold nothing that fits. |
| **Beyond the records** | No record reaches this time or place closely enough to show a single event. |

Three rules sit on top of these:

- Where scholars disagree about a date or a reading, the row says so and takes the more cautious grade.
- A catalogue entry whose only source is the passage itself, or later writers retelling it, is not an independent record. It cannot lift a grade above *possible match*, and the row names it. Several catalogues list earthquakes at Jerusalem in AD 33 and at Philippi in the 50s that trace back to Matthew and Acts.
- A grade describes the record, not the passage. A strong match does not show that an event had a natural cause, and *no match found* does not show that it did not happen. Where a passage presents an event as an act of God, the row says what the record shows and stops there.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `natural-events.csv` | 25 | One row per event: place, the passage's date range, grade, reason, best match, how common, nearest fault. |
| `natural-events.geojson` | 25 points | The same rows as map points. |
| `natural-events-sources.csv` | 218 | Every source consulted, numbered per event, with a link or DOI. |
| `earthquake-candidates.csv` | 20 | Every catalogue earthquake near each earthquake row in place and time, with the catalogue's own warnings. |
| `eclipse-visibility.csv` | 72 | What each proposed eclipse looked like from Jerusalem, Samaria and Nineveh, worked out three ways. |
| `eclipse-counts.csv` | 5 | Every eclipse visible from the place in each eclipse row's date range. |
| `grade-log.csv` | 0 | Every change to a grade after release, with its date and reason. |
| `place-additions.csv` | 2 | Two places used here that are not in our Bible places list (Nicaea and Shunem). |
| `datapackage.json` | | The same description in [Frictionless Data](https://specs.frictionlessdata.io/data-package/) form. |

The CSV files are UTF-8 with a header row. Coordinates are WGS 84 decimal degrees. In `natural-events.csv` and `earthquake-candidates.csv`, negative years are BC: -760 is 760 BC. The eclipse files give dates as NASA's canon does (astronomical years, where -762 is 763 BC) and say so in each field.

## How the matching was done

**Earthquakes.** A candidate is any earthquake in NOAA's significant-earthquake database or CFTI5Med within 200 km of the row's place and within 25 years either side of the passage's date range. 200 km is wide because ancient epicentres are often just the city that reported the damage; it is the distance that catches the AD 363 earthquake, which NOAA places at Karak. Entries CFTI5Med marks as false are left out; entries marked as resting on no observations are kept and flagged. How common: the number of catalogue earthquakes within 200 km in the 100 years around the passage, and the rate per century across 2150 BC to AD 500. Nearest fault: the shortest distance from the place to any line in the GEM Global Active Faults file.

Dead Sea lake-bed layers (seismites) are not in a downloadable catalogue. Where a row rests on one, the reason names the study.

**Eclipses.** The figures come from the Christian Pure sky engine, which works out every solar and lunar eclipse from 2000 BC to AD 500 for a given place from the JPL DE441 ephemeris through Skyfield. Each proposed eclipse is also listed with its number in NASA's Five Millennium Canons. The big unknown before AD 1 is Delta T, the slowing of Earth's spin, which shifts where an eclipse's shadow fell. Each eclipse was worked out at the engine's central value and at two standard errors either side (Morrison and Stephenson 2004, stated for 1000 BC to AD 1200; the Joshua candidates fall outside that range and say so). Dates are Julian calendar. Normal bending of light near the horizon is counted, which matters for the moonrise eclipse of AD 33.

The count of how common eclipses were includes every solar eclipse in the passage's date range that covered at least half the sun's width at greatest eclipse with the sun up at the row's place, or for the lunar row, every lunar eclipse whose shadow (umbral) phase could be seen with the moon up.

Version 1.1.0 (23 November 2026) switched the eclipse figures from this project's own calculation (NASA's canons with DE422) to the sky engine. No grade changed. Magnitudes moved by up to 0.015, the AD 33 moonrise eclipse is now in shadow for about 18 minutes after rising rather than 12 (bending of light is now counted), Samaria's count for Jeroboam II's reign rose from 6 to 7 (an eclipse of 16 July 755 BC that covered just half the sun), and Gibeon's count for 1500 to 1050 BC fell from 85 to 80.

**Famines and droughts.** No record used here counts famines year by year. The climate records near the Levant are the Soreq Cave stalagmite (samples every one to two years from about 190 BC to AD 1056, but with ages uncertain by decades), lower-resolution cave and lake records, and the Old World Drought Atlas, whose grid cells over Judea start only in AD 1083. So most famine rows are *beyond the records*, and the two that grade higher rest on ancient writers: Josephus for the famine under Claudius, Menander of Tyre for Elijah's drought.

**Grades.** Scripts propose candidates; a person reads each research note and sets the grade. Grades will be read again by a second reviewer before release.

## Gaps

- **EMME14**, the Earthquake Model of the Middle East catalogue, offers no bulk download. Rows cite its entries only through the published literature.
- All 218 source links were checked. Every DOI is registered. Four other links refuse automated checks and still need opening by hand before release: two news articles on the Joshua eclipse, a Cambridge journal page and a Tübingen library record for Hezekiah.
- The places are those of the Christian Pure Bible places list; where a passage names a region (Canaan, Egypt), the point is the region's middle, and distances from it mean little.

## Fields

<!-- fields -->
### natural-events.csv

One row per natural event named in the Bible or early church writings, with its place, the passage's date, the grade and the best match in the scientific record.

| Field | Type | What it holds |
| --- | --- | --- |
| `id` | string (required) | Short id of the event. Starts with e- (eclipse or darkness), f- (famine or drought) or q- (earthquake). |
| `kind` | string (required) | earthquake, eclipse, darkness, famine or drought. |
| `event` | string (required) | Short title of the event. |
| `passages` | string (required) | Where the event is told: Bible references, or the ancient writer for the two rows outside the Bible. |
| `place` | string (required) | The place used for matching: where the passage puts the event, or the nearest place it names. |
| `place_id` | string (required) | Id of the place in the Christian Pure Bible places list, or add-… for the two places added here (see place-additions.csv). |
| `latitude` | number (required) | WGS 84 latitude of the place. |
| `longitude` | number (required) | WGS 84 longitude of the place. |
| `passage_date_from` | integer (required) | Earliest year scholars give for the passage. Negative years are BC: -760 is 760 BC (there is no year 0). |
| `passage_date_to` | integer (required) | Latest year scholars give for the passage, same numbering. |
| `passage_date` | string (required) | The same range in words, for example 766 BC to 751 BC. |
| `date_note` | string (required) | Where the date range comes from and where scholars disagree. |
| `grade` | string (required) | One of four: strong match, possible match, no match found, beyond the records. See the README for what each means. |
| `reason` | string (required) | Why the row has its grade, naming the record it rests on. |
| `best_match` | string | The record that comes closest. Empty where nothing comes close; starts with None. where the nearest candidate does not fit. |
| `best_match_catalogue` | string | The catalogue or writer that holds the best match. |
| `best_match_entry` | string | The entry's number in that catalogue, where it has one. |
| `best_match_year` | integer | Year of the best match, same numbering as passage_date_from. |
| `how_common` | string (required) | How often events of this kind happened at this place in the same period, counted from the same records (earthquakes within 200 km; eclipses visible from the place). |
| `nearest_fault_km` | number | Earthquake rows: distance in km from the place to the nearest mapped active fault (GEM Global Active Faults). |
| `nearest_fault` | string | Earthquake rows: that fault's type and slip rate. Most faults in this region have no name in the source. |
| `nearest_fault_gem_id` | string | Earthquake rows: the fault's id in the GEM file (catalogue name and id). |
| `graded_on` | string (required) | Date the grade was last set, YYYY-MM-DD. |

### natural-events-sources.csv

Every source consulted for each event, numbered as in the research notes.

| Field | Type | What it holds |
| --- | --- | --- |
| `event_id` | string (required) | Event (natural-events.csv). |
| `n` | integer (required) | Number of the source within its event. |
| `citation` | string (required) | The citation, with a note where the source was not opened or is cited only to show a claim exists. |
| `url` | string | Link or DOI for the source, where there is one. |

### earthquake-candidates.csv

Every catalogue earthquake within 200 km of an earthquake row's place and within 25 years either side of its date range. An event with no candidates has one row with the catalogue fields empty.

| Field | Type | What it holds |
| --- | --- | --- |
| `event_id` | string (required) | Event (natural-events.csv). |
| `catalogue` | string | NOAA NCEI significant earthquakes, NOAA NCEI tsunamis, or CFTI5Med. |
| `entry` | string | Entry number in that catalogue. CFTI5Med notes in brackets: N = no observations behind the entry, S = a single data point, D = doubtful. |
| `year` | integer | Year the catalogue gives, same numbering as natural-events.csv. |
| `where` | string | Place name the catalogue gives. |
| `size` | string | Magnitude (M, Mw) or intensity (I0) where the catalogue gives one. |
| `distance_km` | integer | Distance in km from the event's place to the catalogue's epicentre. |
| `catalogue_flag` | string | Where the catalogue itself marks the entry as doubtful or as resting on no observations. |
| `base_count_100y` | integer (required) | Catalogue earthquakes within 200 km in the 50 years either side of the middle of the passage's range. |
| `base_rate_per_century` | number (required) | Catalogue earthquakes within 200 km per century, 2150 BC to AD 500. |

### eclipse-visibility.csv

What each proposed eclipse looked like from Jerusalem, Samaria and Nineveh, from the Christian Pure sky engine (JPL DE441), worked out three times: at the engine's central value for the slowing of Earth's spin (Delta T) and at two standard errors either side.

| Field | Type | What it holds |
| --- | --- | --- |
| `event` | string (required) | Event (natural-events.csv). |
| `kind` | string (required) | solar or lunar. |
| `nasa_catalogue_number` | string (required) | Number of the same eclipse in NASA's Five Millennium Canon, for reference. |
| `date_julian` | string (required) | Date (Universal Time) in the Julian calendar, astronomical year first: -762 Jun 15 is 15 June 763 BC. |
| `nasa_type` | string (required) | NASA's type for the eclipse as a whole: T total, A annular, H hybrid, P partial. |
| `local_type` | string (required) | The eclipse as seen from the place at the central Delta T: Total, Annular or Partial (lunar: the eclipse's own type). |
| `delta_t_case` | string (required) | central, minus_2sigma or plus_2sigma. |
| `delta_t_s` | integer (required) | Delta T used, in seconds. |
| `delta_t_2sigma_s` | integer (required) | Two standard errors of Delta T, in seconds (Morrison and Stephenson 2004, 0.8 t^2 s; stretched before 1000 BC). |
| `place_id` | string (required) | Place id. |
| `place` | string (required) | Jerusalem, Samaria or Nineveh. |
| `visible` | string (required) | yes or no. Solar: the sun was up while partly covered. Lunar: the moon was up during the shadow (umbral) phase. Normal bending of light at the horizon is counted. |
| `magnitude` | number (required) | Solar: fraction of the sun's width covered at greatest eclipse at the place. Lunar: umbral magnitude. |
| `altitude_deg` | number (required) | Height of the sun (solar) or moon (lunar) above the horizon at greatest eclipse, degrees. Negative means below the horizon. |
| `minutes_visible` | integer (required) | Minutes the eclipse (solar) or its umbral phase (lunar) could be seen with the sun or moon up. |
| `local_start` | string | Central Delta T only: local mean time the eclipse (solar) or umbral phase (lunar) began, HH:MM. |
| `local_greatest` | string | Central Delta T only: local mean time of greatest eclipse, HH:MM. |
| `local_end` | string | Central Delta T only: local mean time the eclipse or umbral phase ended, HH:MM. |
| `ut_greatest` | string | Central Delta T only: Universal Time of greatest eclipse, HH:MM. |
| `first_seen_local` | string | Central Delta T only: local mean time the eclipse could first be seen, HH:MM. |
| `note` | string | Warnings, for example where the Delta T error formula is used outside its stated range. |

### eclipse-counts.csv

For each eclipse or darkness row, every eclipse in the sky engine's table inside the passage's date range that was visible from the row's place at the central Delta T: how common eclipses were.

| Field | Type | What it holds |
| --- | --- | --- |
| `event_id` | string (required) | Event (natural-events.csv). |
| `place` | string (required) | Place the eclipses were worked out for. |
| `range` | string (required) | The passage's date range. |
| `kind_counted` | string (required) | What was counted: solar eclipses covering half the sun or more at greatest eclipse with the sun up, or lunar eclipses with the moon up during the shadow (umbral) phase. |
| `visible_count` | integer (required) | How many eclipses were counted. |
| `per_century` | number (required) | visible_count per hundred years. |
| `visible_list` | string | The counted eclipses, separated by "; ": date (Julian calendar) and fraction of the sun covered, or minutes of the lunar shadow phase with the moon up. |

### grade-log.csv

Every change to a grade after first release, with its date and reason. Empty until a grade changes.

| Field | Type | What it holds |
| --- | --- | --- |
| `event_id` | string (required) | Event (natural-events.csv). |
| `date` | string (required) | Date of the change, YYYY-MM-DD. |
| `old_grade` | string (required) | Grade before. |
| `new_grade` | string (required) | Grade after. |
| `why` | string (required) | What changed: a new study, a corrected figure, or a reviewer's reading. |

### place-additions.csv

Places used here that are not in the Christian Pure Bible places list.

| Field | Type | What it holds |
| --- | --- | --- |
| `id` | string (required) | Id used in natural-events.csv place_id. |
| `name` | string (required) | Name. |
| `lat` | number (required) | WGS 84 latitude. |
| `lon` | number (required) | WGS 84 longitude. |
| `source` | string (required) | Where the point comes from. |

<!-- /fields -->

## Sources and credit

- NOAA National Centers for Environmental Information, NCEI/WDS Global Significant Earthquake Database, doi:10.7289/V5TD9V7K, and Global Historical Tsunami Database, doi:10.7289/V5PN93H7 (public domain).
- Guidoboni, E., et al. 2018. CFTI5Med, Catalogue of Strong Earthquakes in Italy (461 BC to 1997) and Mediterranean Area (760 BC to 1500). PANGAEA, doi:10.1594/PANGAEA.896750; Scientific Data 6:80 (2019). CC BY 4.0.
- Styron, R., and Pagani, M. 2020. The GEM Global Active Faults Database. Earthquake Spectra 36(1_suppl), doi:10.1177/8755293020944182. CC BY-SA 4.0.
- Eclipse Predictions by Fred Espenak and Jean Meeus (NASA's GSFC): Five Millennium Canon of Solar Eclipses (NASA TP-2006-214141) and of Lunar Eclipses (NASA/TP-2009-214173).
- JPL planetary ephemeris DE441 (Park et al. 2021, The JPL Planetary and Lunar Ephemerides DE440 and DE441, Astronomical Journal 161:105), read with Skyfield (Rhodes).
- Morrison, L. V., and Stephenson, F. R. 2004. Historical values of the Earth's clock error ΔT. Journal for the History of Astronomy 35: 327-336.
- Christian Pure Bible places list (CC BY 4.0), built on OpenBible.info and Pleiades.
- The studies, catalogues and ancient writers behind each row are in `natural-events-sources.csv`.

## Licence

CC BY-SA 4.0 (see `LICENSE`). This folder is share-alike, unlike our other datasets, because the GEM fault file it draws on is share-alike. Credit Christian Pure and keep the credits above. If you use the table, we would be glad of a link to the page it was made for, [Earthquakes, eclipses and famines in the Bible](https://christianpure.com/bible-earthquakes-eclipses-famines/); that is a request, not a condition.

## How to cite

Christian Pure. 2026. *Earthquakes, eclipses and famines in the Bible, set against the scientific record*, version 1.1.0. https://christianpure.com/bible-earthquakes-eclipses-famines/
