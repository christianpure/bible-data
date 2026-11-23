# Saints with their feast days in the Western and Orthodox calendars

This is a list of 378 saints, each with the day the Western (Roman Catholic) calendar keeps their feast, the day the Orthodox calendar keeps it, what they are patrons of, a line on what they are known for, and the sources we drew it from. It is the data behind our saint finder at [christianpure.com/saint-finder](https://christianpure.com/saint-finder/), where a reader types a first name, a need or a date and meets the saint.

Between them the 378 saints cover every day of the year, 29 February included. 171 have a feast in both calendars, 162 in the Western calendar only and 45 in the Orthodox calendar only.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `saints.csv` | 378 | One row per saint. |
| `saint-sources.csv` | 1,090 | The sources for each saint, in order, with their addresses. |
| `saints.json` | 378 | The same saints as JSON, each with its sources inside. |
| `datapackage.json` | | The same description in [Frictionless Data](https://specs.frictionlessdata.io/data-package/) form: every field, its type and the keys that join the tables. |

The CSV files are UTF-8 with a header row, comma separated, and lists inside a cell (patronages, titles, name forms) are separated by a semicolon and a space. Feast days are written `MM-DD`, so `12-06` is 6 December.

## Fields

### saints.csv

<!-- fields: saints -->
| Field | Type | What it holds |
| --- | --- | --- |
| `saint_id` | string (required) | Id of the saint, as in the finder’s addresses (?saint=<id>). |
| `name` | string (required) | Name of the saint. |
| `western_feast` | string | Feast day in the Western (Roman Catholic) calendar, as MM-DD. Empty where the West keeps no feast. |
| `western_feast_note` | string | Note on the Western date, such as the calendar that keeps it. |
| `orthodox_feast` | string | Feast day in the Orthodox calendar, as MM-DD on the civil (Gregorian) calendar, as new-calendar churches keep it. Empty where no Orthodox feast was found. |
| `orthodox_feast_note` | string | Note on the Orthodox date, or why there is none. |
| `orthodox_old_calendar_also` | boolean | true where the old-calendar churches (Russian, Serbian, Jerusalem, Mount Athos) also keep the feast, 13 days later on the civil calendar. false where only new-calendar churches keep it, or it could not be told. |
| `orthodox_old_calendar_date` | string | The civil date (MM-DD) on which old-calendar churches keep the feast: orthodox_feast plus 13 days, counted in a common year. |
| `patron_of` | string | Patronages, separated by "; ". Empty where none was sourced. |
| `titles` | string | Titles and traditional descriptions, separated by "; ". |
| `name_forms` | string | First names the finder matches to this saint, lower case, separated by "; ". |
| `known_for` | string (required) | One line on what the saint is known for. Our words. |
| `source_count` | integer (required) | Number of sources (saint-sources.csv). |
| `finder_url` | string (required) | The saint’s page in the Christian Pure saint finder. |
<!-- /fields -->

### saint-sources.csv

<!-- fields: saint-sources -->
| Field | Type | What it holds |
| --- | --- | --- |
| `saint_id` | string (required) | Saint (saints.csv). |
| `source_order` | integer (required) | Order of the source for the saint, from 1. |
| `title` | string (required) | Title of the source. |
| `url` | string (required) | Address of the source. |
<!-- /fields -->

## How it was made

We chose the saints in two ways. Most are the saints people look for, ranked by how often their names are searched for, and the rest were added so that a search for any date of the year finds at least one saint.

Each entry was written by our editorial team from its sources and then read a second time, line by line, against saved copies of those sources, by someone who had not written it. Every date, patronage and title had to be in a source, and anything a source did not support was changed or taken out. The known-for lines and the choice of saints are our own work. The finder also shows a short life of each saint, which is not part of this release.

Western dates follow the General Roman Calendar and, for saints who are not on it, the Roman Martyrology of 2004. Orthodox dates are the days on which the Orthodox Church in America, which uses the new calendar, keeps the feast, as its lives of the saints give them, so they are civil (Gregorian) dates. Churches that keep the old Julian calendar, among them the Russian and Serbian churches, Jerusalem and Mount Athos, keep the same feast 13 days later on the civil calendar; where they do, `orthodox_old_calendar_also` is true and `orthodox_old_calendar_date` gives that later date.

## Known gaps

- **Many saints have no patronage.** 205 of the 378 have nothing in `patron_of`, because we list a patronage only where a source names it, and for many saints none does.
- **An empty feast means we found none, not that none exists.** 162 saints have no Orthodox date and 45 no Western date in these files. A local or national calendar may keep a feast we did not find.
- **National calendars can differ.** Where we know of a well-known difference, the feast note says so (Saint Kateri Tekakwitha, for example, is kept on 14 July in the United States), but we have not checked every country's calendar.
- **Old-calendar dates near the end of February shift in leap years.** We add 13 days as if in a common year, as the finder does. For the nine saints whose Orthodox feast falls between 16 and 29 February (Polycarp, Leo the Great, Pamphilus of Caesarea, Philemon, Leo of Catania, Tarasius, Porphyrius of Gaza, Marana and Kyra, and John Cassian), the old-calendar civil date is one day earlier in a leap year.
- **38 saints have an Orthodox feast that only new-calendar churches keep**, or where we could not tell, such as Saint Patrick in the Orthodox Church in America; for these `orthodox_old_calendar_also` is false.
- **Older sources.** 257 saints cite the Catholic Encyclopedia of 1911, which is out of copyright and freely readable but a century old. The Western dates come from the current calendar and the 2004 Martyrology, not from the encyclopedia, and every saint but one, Anthony of Padua, has at least one other source as well.
- **No pictures.** The finder shows a painting for many saints, but paintings and their photographs carry rights of their own, so none are included here.
- `name_forms` are the first names the finder matches to each saint, such as "nick" and "colin" for Saint Nicholas. They help people find a name saint; they are not an etymology.

## License and credit

The list of saints, the known-for lines and the way these tables are put together are released under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0); the full text is in `LICENSE`. Feast dates and patronages are facts that anyone may use. You may copy, change and build on all of it for any purpose, commercial or not. The license asks you to name Christian Pure as the source, and a plain-text credit is enough, for example:

> Saints data by Christian Pure, CC BY 4.0.

If you use this, we'd be grateful for a credit link to [https://christianpure.com/saint-finder/](https://christianpure.com/saint-finder/), or to one saint's own page there (its `finder_url`). That is a request, not a condition: a credit without a link is fine, and any link may carry nofollow.

The sources we link to belong to their publishers, and their own terms apply if you copy from them.

To cite the data in a paper, see `CITATION.cff` at the top of this repository, or use:

> Christian Pure. "Saints with Their Feast Days in the Western and Orthodox Calendars." Version 1.3.0, 23 November 2026. https://christianpure.com/saint-finder/.

Found a mistake? Please open an issue in this repository. Corrections to our pages are logged on [our editorial standards page](https://christianpure.com/editorial-standards/).
