# Changes

## 1.3.0, 23 November 2026

A new folder:

- `bible-natural-events`: 25 earthquakes, eclipses, famines and droughts from the Bible and the early church, from the earthquake of Amos 1:1 to the Galilee earthquake of AD 363. Each is set against earthquake catalogues (NOAA, CFTI5Med), eclipse calculations for Jerusalem, Samaria, Nineveh and Gibeon, climate records and ancient historians, and given one of four grades: strong match (2), possible match (7), no match found (3) and beyond the records (13). Events with no match stay in. Every source is listed, with the nearest active fault and how common such events were. It is the data behind [Earthquakes, eclipses and famines in the Bible](https://christianpure.com/bible-earthquakes-eclipses-famines/). This folder is CC BY-SA 4.0, because the fault map it draws on is share-alike.

Changes in one other folder, following the live [Compare Christian Denominations](https://christianpure.com/compare-denominations/) page:

- `denominations`: seven Anabaptist answers now cite Mennonite Church USA's current documents in place of the 1963 Mennonite Confession and the Keystone Mennonite Fellowship's 1998 supplement, and the Anabaptist answer on remarriage is now `no_official_statement`. The read-more links point to newer articles that answer each question more closely: 1,129 answers have one, up from 714.

The other four folders have not changed apart from their version number.

## 1.2.1, 22 November 2026

- `bible-places`: Seba is now its own place, `cp-seba`, with Isaiah 43:3 and Psalm 72:10. OpenBible.info files it under Sheba (`a81ab85`), but the Bible names the two apart (Psalm 72:10, Genesis 10:7). Sheba keeps its point in Yemen and loses Isaiah 43:3. Seba's point, Meroë in Sudan, is ours, and it has no OpenBible.info score. 1,247 places. Thanks to Robert Rouse of Theographic, who found it ([issue 1](https://github.com/christianpure/bible-data/issues/1)).
- `id` may now be `cp-` plus a name for a place that OpenBible.info does not list on its own, and `openbible_score` may be empty for one.

The other five folders have not changed apart from their version number.

## 1.2.0, 19 November 2026

- `bible-places` now covers the whole Bible: 1,246 places from Genesis to Revelation (was 151 from the Gospels and Acts), as the [Bible places map](https://christianpure.com/bible-places-map/) now does. The column `gospels_acts_verses` is renamed `verses`, and `books` can name any book of the Bible. The 151 places of 1.1.0 are all still here.
- The description of `openbible_score` is corrected: it is OpenBible.info's time-weighted score, which a few places carry below 0 or above 1000.

The other five folders have not changed apart from their version number.

## 1.1.0, 19 November 2026

Two new folders:

- `bible-places`: the 151 places named in the four Gospels and Acts, with their locations, how sure each location is, the verses that name them and their names in 11 languages, as CSV and GeoJSON. It is the data behind the [Bible places map](https://christianpure.com/bible-places-map/).
- `topical-bible`: over 6,500 Bible subjects and the verses on each, 79,134 rows, from the OpenBible.info Topical Bible and the verses our own pages quote. It is the data behind [What does the Bible say about…?](https://christianpure.com/what-does-the-bible-say-about/)

The four existing folders have not changed apart from their version number.

## 1.0.0, 18 November 2026

First release: Paul's journeys, saints, denominations and Easter dates.
