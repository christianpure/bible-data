# Places in the Bible, with their names in 11 languages

This table lists every place the Bible names that can be put on a map, from Genesis to Revelation: where it is, how sure scholars are of that, every verse that names it, and its name as the Bible in each of 11 languages prints it. It is the data behind our [Bible places map](https://christianpure.com/bible-places-map/), which shows the same places on real terrain in all 11 languages.

There are 1,247 places, named in 61 of the Bible's 66 books. For 194 the site is known, for 493 it is probable, for 396 it is disputed, and 164 are regions rather than single sites, such as Galilee or Edom. 1,073 are named only in the Old Testament and 128 only in the New.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `places.csv` | 1,247 | One row per place. |
| `places.geojson` | 1,247 | The same places as GeoJSON points, with the names, certainty and verses as properties. |

The CSV file is UTF-8 with a header row, comma separated, and lists inside a cell are separated by a semicolon and a space. Coordinates are WGS 84 decimal degrees; GeoJSON gives them in its usual order, longitude first. Verse references are in OSIS form, for example `Luke.2.4`, and follow the verse numbering of English Bibles. The `id` is OpenBible.info's own id for the ancient place, so each row joins with its Bible Geocoding Data, and `pauls_journeys` joins with `pauls-journeys/stops.csv` in this repository.

## Fields

<!-- fields: places -->
| Field | Type | What it holds |
| --- | --- | --- |
| `id` | string (required) | OpenBible.info ancient-place id; join with its Bible Geocoding Data. One place OpenBible.info files under another has our own id: cp-seba (Seba, filed under Sheba, a81ab85). |
| `name_en` | string (required) | Name in English, as the Berean Standard Bible prints it. |
| `name_ar` | string | Name in Arabic, as the Van Dyck Bible (1865) prints it. Empty where that Bible does not print the name. |
| `name_de` | string | Name in German, as the Lutherbibel 1912 prints it. Empty where that Bible does not print the name. |
| `name_es` | string | Name in Spanish, as the Reina-Valera 1909 prints it. Empty where that Bible does not print the name. |
| `name_fr` | string | Name in French, as the Louis Segond 1910 prints it. Empty where that Bible does not print the name. |
| `name_it` | string | Name in Italian, as the Riveduta 1927 prints it. Empty where that Bible does not print the name. |
| `name_nl` | string | Name in Dutch, as the De Heilige Schrift 1917 prints it. Empty where that Bible does not print the name. |
| `name_pt` | string | Name in Portuguese, as the Bíblia Livre (CC BY 4.0) prints it. Empty where that Bible does not print the name. |
| `name_ru` | string | Name in Russian, as the Synodal translation prints it. Empty where that Bible does not print the name. |
| `name_zh` | string | Name in Chinese, as the Chinese Union Version prints it. Empty where that Bible does not print the name. |
| `name_ja` | string | Name in Japanese, as the Colloquial Japanese Bible (1955) prints it. Empty where that Bible does not print the name. |
| `name_kjv` | string | Name as the King James Version prints it, where it differs or for reference. |
| `lat` | number (required) | Latitude of the point, WGS 84 (OpenBible.info; ours for cp-seba). |
| `lon` | number (required) | Longitude of the point, WGS 84 (OpenBible.info; ours for cp-seba). |
| `label_lat` | number | For a region: latitude where the map prints its name. Empty for other places. |
| `label_lon` | number | For a region: longitude where the map prints its name. Empty for other places. |
| `site_today` | string (required) | The modern place or site the point stands for. |
| `openbible_score` | integer | OpenBible.info confidence in the identification (its time-weighted score, time_total): read it as thousandths, where 1000 is very high confidence. It is a trend line, so a few run below 0 or above 1000. Empty for cp-seba, which OpenBible.info does not list. |
| `certainty` | string (required) | Our reading of how sure the location is: sure, likely, unsure, or region (an area, not a point). |
| `certainty_note` | string (required) | One sentence on why, as the map shows it. |
| `other_proposed_sites` | string | Other sites proposed for it, separated by "; ". |
| `sources_surveyed` | integer (required) | Reference works OpenBible.info surveyed for this place (0 for cp-seba). |
| `verses` | string (required) | Every verse in the Bible that names it, in English verse numbering, OSIS references separated by "; ". |
| `books` | string (required) | The books of the Bible that name it, in Bible order, OSIS codes separated by "; ". |
| `pleiades` | string | Pleiades gazetteer page, where one matches. |
| `wikidata` | string | Wikidata item, where one matches. |
| `openbible_url` | string (required) | The place on OpenBible.info (for cp-seba, the Sheba page it is filed under). |
| `pauls_journeys` | string | Where Paul stops here on our Paul map: journey_id:stop_order pairs, separated by "; ", matching pauls-journeys/stops.csv. |
<!-- /fields -->

## How it was made

We started from the OpenBible.info Bible Geocoding Data, which identifies every place in the Protestant Bible with its possible modern sites, the reference works that propose each one, and a confidence score. OpenBible.info lists 1,285 places. We left out 39: the 32 that its own data cannot put on a map (such as the Garden of Eden, the land of Nod and Azazel), and seven entries that are directions or words rather than places the verses name (the Nile, North, East, South three times, and the Holy Place). That leaves 1,246.

One place is our own addition. OpenBible.info files Seba under Sheba (`a81ab85`), but the Bible names them apart: Psalm 72:10 has "the kings of Sheba and Seba", Genesis 10:7 gives them different fathers, and Isaiah 43:3 names "Cush and Seba". So Sheba keeps its point in Yemen, and Seba has its own row, `cp-seba`, with Isaiah 43:3 and Psalm 72:10. Its point is ours, not OpenBible.info's: Meroë in Sudan, where Josephus places it, with Yemen as the other proposed site. It has no OpenBible.info score, and its `openbible_url` goes to the Sheba page. Robert Rouse of Theographic pointed this out ([issue 1](https://github.com/christianpure/bible-data/issues/1)). That makes 1,247 places.

For each place we kept OpenBible.info's most likely point and its score, and wrote one sentence on how sure the location is, naming the number of sources OpenBible.info surveyed. We sorted each place into four groups: `sure` where the site is not in doubt, `likely` where most sources agree, `unsure` where they divide, and `region` for an area rather than a site. The other sites that OpenBible.info lists are in `other_proposed_sites`.

The names in other languages are taken from the verses that name each place, in a Bible in the public domain or under an open license for each language. Each name was read against the verse it comes from and checked by machine; no native speaker has read them all. Where a Bible does not print the name in those verses, the cell is empty: 1,155 places have a name in all ten other languages.

We matched each place to Pleiades and to Wikidata where a match was clear: 201 places have a Pleiades link and 608 a Wikidata link.

## Known gaps

- **Disputed sites keep one point.** For the 396 `unsure` places, the point is OpenBible.info's first choice, not a settled answer; read `certainty_note` and `other_proposed_sites` before you rely on it.
- **A region has one point.** For the 164 regions the point is a rough centre, and `label_lat` and `label_lon` give where our map prints the region's name for 36 of them.
- **Some descriptions are OpenBible.info's English notes.** Where OpenBible.info identifies a place only by a note, such as "another name for Ur 2", `site_today` and `other_proposed_sites` keep that note in English.
- **English verse numbering.** References follow English Bibles. Hebrew editions and some Bibles in other languages number a few chapters differently (our map shows each Bible's own numbering).
- **The names have not all been read by a native speaker,** as noted above.

## Sources and their licenses

When you reuse these files, please keep the credits of the sources they draw on, which their licenses ask for:

- **OpenBible.info**, Bible Geocoding Data, [github.com/openbibleinfo/Bible-Geocoding-Data](https://github.com/openbibleinfo/Bible-Geocoding-Data), CC BY 4.0: the places, their points, scores, candidate sites and source counts.
- **Pleiades**, [pleiades.stoa.org](https://pleiades.stoa.org/), CC BY 3.0: the matched places.
- **Wikidata**, [wikidata.org](https://www.wikidata.org/), CC0: the matched items.
- **The Bibles the names come from:** the Berean Standard Bible (English) and the King James Version, the Van Dyck Bible (Arabic), the Lutherbibel 1912 (German), the Reina-Valera 1909 (Spanish), the Louis Segond 1910 (French), the Riveduta 1927 (Italian), De Heilige Schrift 1917 (Dutch), the Synodal translation (Russian) and the Colloquial Japanese Bible of 1955 (Japanese), all in the public domain; the Chinese Union Version (Chinese), whose 1919 text is in the public domain, with the names as its New Punctuation edition prints them; and the Bíblia Livre (Portuguese), CC BY 4.0. Only the names are taken, never verse text.

## License and credit

Our certainty readings, notes, matches and the way this table is put together are released under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0); the full text is in `LICENSE`. You may copy, change and build on them for any purpose, commercial or not. The license asks you to name the sources, and a plain-text credit is enough, for example:

> Bible places data by Christian Pure, CC BY 4.0, building on OpenBible.info Bible Geocoding Data (CC BY 4.0).

If you use this, we'd be grateful for a credit link to [https://christianpure.com/bible-places-map/](https://christianpure.com/bible-places-map/), where the map is. That is a request, not a condition: a credit without a link is fine, and any link may carry nofollow.

To cite the data in a paper, see `CITATION.cff` at the top of this repository, or use:

> Christian Pure. "Bible Places Map: Places in the Bible, Map and Data." Version 1.3.0, 23 November 2026. https://christianpure.com/bible-places-map/.

Found a mistake? Please open an issue in this repository. Corrections to our pages are logged on [our editorial standards page](https://christianpure.com/editorial-standards/).
