<p align="center">
  <a href="https://christianpure.com/">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/christianpure/.github/main/assets/christianpure-logo-on-navy.png">
      <img src="https://raw.githubusercontent.com/christianpure/.github/main/assets/christianpure-logo-light.png" alt="Christian Pure" width="240">
    </picture>
  </a>
</p>

<p align="center"><a href="https://doi.org/10.5281/zenodo.24396556"><img src="https://zenodo.org/badge/DOI/10.5281/zenodo.24396556.svg" alt="DOI 10.5281/zenodo.24396556"></a></p>

# Bible data from Christian Pure

This repository holds nine sets of data that [Christian Pure](https://christianpure.com/) built for its free Bible and church tools, released so that anyone can use them: app builders, teachers, researchers and anyone who simply likes a good table. Each set is a folder of plain files (spreadsheets you can open in Excel or Google Sheets, JSON and, for the map, GeoJSON) with a README that says what is in it, how it was made, where it falls short and how to cite it.

| Folder | What it holds | Size | License | It powers |
| --- | --- | --- | --- | --- |
| [`pauls-journeys`](pauls-journeys/) | Paul's three missionary journeys and his voyage to Rome: every stop with its coordinates and verse in Acts, every leg with its distance by Roman road and by sea, and the places matched to OpenBible.info, Pleiades and Wikidata. | 4 journeys, 69 stops, 65 legs, 48 places | CC BY 4.0 | [Paul's missionary journeys map](https://christianpure.com/pauls-missionary-journeys/) |
| [`saints`](saints/) | 378 saints with their feast days in the Western and Orthodox calendars, patronages and sources. | 378 saints, 1,090 sources | CC BY 4.0 | [Saint finder](https://christianpure.com/saint-finder/) |
| [`denominations`](denominations/) | 22 churches and traditions, and Protestants in general, on 55 questions, each answered from the church's own documents, with the passage named and linked. | 23 churches, 55 questions, 1,265 answers | CC BY 4.0 | [Compare Christian Denominations](https://christianpure.com/compare-denominations/) |
| [`bible-places`](bible-places/) | Every place the Bible names that can be put on a map, from Genesis to Revelation: its location, how sure that location is, the verses that name it, and its name as the Bible in each of 11 languages prints it. | 1,247 places, 11 languages | CC BY 4.0 | [Bible places map](https://christianpure.com/bible-places-map/) |
| [`topical-bible`](topical-bible/) | Over 6,500 Bible subjects and the verses on each, from the OpenBible.info Topical Bible and our own pages, as references only. | 79,134 rows | CC BY 4.0 | [What does the Bible say about…?](https://christianpure.com/what-does-the-bible-say-about/) |
| [`bible-natural-events`](bible-natural-events/) | 25 earthquakes, eclipses, famines and droughts from the Bible and the early church, each set against earthquake catalogues, eclipse calculations, climate records and ancient historians and given one of four grades, with its sources. Events with no match stay in. | 25 events, 218 sources | CC BY-SA 4.0 | [Earthquakes, eclipses and famines in the Bible](https://christianpure.com/bible-earthquakes-eclipses-famines/) |
| [`jerusalem-sky`](jerusalem-sky/) | The sky over Jerusalem from the sun's and moon's positions: when each Hebrew month most likely began, by crescent sighting, and the date and weekday of Passover in every year from 1000 BC to AD 135; every eclipse seen from Jerusalem, Samaria or Nineveh from 1999 BC to AD 500; and the sky on named nights, such as the Star of Bethlehem candidates and 3 April AD 33. Every row carries its margin of doubt. | 14,038 months, 1,135 years, 21,137 eclipse rows | CC0 (no conditions) | [When did Jesus die?](https://christianpure.com/the-day-jesus-died/) |
| [`easter-moons`](easter-moons/) | The full moon the church's Easter tables use beside the real full moon over Jerusalem, for every year from AD 325 to 2100, with Western, Orthodox and astronomical Easter: why the two Easters differ. | 1,776 years | CC0 (no conditions) | Background for [When is Easter?](https://christianpure.com/when-is-easter/) |
| [`easter-dates`](easter-dates/) | Western and Orthodox Easter, with Lent, Palm Sunday, Good Friday, Ascension and Pentecost, for every year from 1900 to 2099. | 200 years | CC0 (no conditions) | [When is Easter?](https://christianpure.com/when-is-easter/) |

## Using the data

You may copy, change, share and build on all of it, for any purpose, commercial or not. The Easter dates, the two sky tables and the natural events aside, every folder is released under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which asks only that you name Christian Pure as the source. A plain-text credit is enough, such as "Saints data by Christian Pure, CC BY 4.0". The Easter dates, `jerusalem-sky` and `easter-moons` are calculations, dedicated to the public domain under [CC0](https://creativecommons.org/publicdomain/zero/1.0/), and carry no conditions at all. The natural events folder is under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/), because the fault map it draws on is share-alike: what you build from that folder must carry the same licence.

If you use the data, we'd be grateful for a credit link to the page it comes from, which is named in each folder's README. That is a request, not a condition: a credit without a link is fine, and any link may carry nofollow.

Some of what the data draws on belongs to others, and the folder READMEs say what. The places on both maps come from OpenBible.info and Pleiades, and Paul's roads from the Itiner-e atlas of Roman roads; the subjects in the topic table come from OpenBible.info's Topical Bible. Their licenses ask you to keep their credits. The Bible verses are from the World English Bible, which is in the public domain. The churches' own words are not included in the denominations data, because they belong to the churches; it names and links each passage instead. No pictures are included.

## Formats

Every CSV file is UTF-8, comma separated, with a header row. Lists inside a cell are separated by a semicolon and a space. Dates are `YYYY-MM-DD`, and feast days without a year are `MM-DD`. The two sky tables reach back before AD 1, so they write years as astronomers do (1 BC is `0000`, 2 BC is `-0001`), use the Julian calendar before 15 October 1582, and give each date's Julian Day Number beside it. Coordinates are WGS 84 decimal degrees.

Each folder also has a `datapackage.json` in the [Frictionless Data](https://specs.frictionlessdata.io/data-package/) format, which describes every file and field, its type and the keys that join the tables, so that tools such as the Frictionless Framework, pandas or R can load the data with the right types. For example, with Python:

```python
import pandas as pd

stops = pd.read_csv("pauls-journeys/stops.csv")
easter = pd.read_csv("easter-dates/easter-dates.csv", parse_dates=["western_easter", "orthodox_easter"])
```

## Citing

[`CITATION.cff`](CITATION.cff) gives the citation in a form GitHub and reference managers read; GitHub shows it under "Cite this repository". In short:

> Christian Pure. *Bible Data from Christian Pure*. Version 1.4.0, 23 November 2026. https://doi.org/10.5281/zenodo.24396556.

The DOI always points to the latest version on [Zenodo](https://doi.org/10.5281/zenodo.24396556), which keeps a permanent copy of every release; each version also has its own DOI there.

## Versions and corrections

This is version 1.4.0, released on 23 November 2026, and it matches what our tools and pages showed that day. [`CHANGELOG.md`](CHANGELOG.md) says what changed in each version. When the tools change, a new version will follow, and older versions stay available in the repository's history.

If you find a mistake, please [open an issue](https://github.com/christianpure/bible-data/issues). We fix the tools and the data together, and corrections to our pages are logged on [our editorial standards page](https://christianpure.com/editorial-standards/).

The data was prepared by the Christian Pure editorial team.
