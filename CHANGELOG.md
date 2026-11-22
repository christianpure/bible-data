# Changes

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
