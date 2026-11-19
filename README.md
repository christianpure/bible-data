<p align="center">
  <a href="https://christianpure.com/">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/christianpure/.github/main/assets/christianpure-logo-on-navy.png">
      <img src="https://raw.githubusercontent.com/christianpure/.github/main/assets/christianpure-logo-light.png" alt="Christian Pure" width="240">
    </picture>
  </a>
</p>

# Bible data from Christian Pure

This repository holds six sets of data that [Christian Pure](https://christianpure.com/) built for its free Bible and church tools, released so that anyone can use them: app builders, teachers, researchers and anyone who simply likes a good table. Each set is a folder of plain files (spreadsheets you can open in Excel or Google Sheets, JSON and, for the map, GeoJSON) with a README that says what is in it, how it was made, where it falls short and how to cite it.

| Folder | What it holds | Size | License | It powers |
| --- | --- | --- | --- | --- |
| [`pauls-journeys`](pauls-journeys/) | Paul's three missionary journeys and his voyage to Rome: every stop with its coordinates and verse in Acts, every leg with its distance by Roman road and by sea, and the places matched to OpenBible.info, Pleiades and Wikidata. | 4 journeys, 69 stops, 65 legs, 48 places | CC BY 4.0 | [Paul's missionary journeys map](https://christianpure.com/pauls-missionary-journeys/) |
| [`saints`](saints/) | 378 saints with their feast days in the Western and Orthodox calendars, patronages and sources. | 378 saints, 1,090 sources | CC BY 4.0 | [Saint finder](https://christianpure.com/saint-finder/) |
| [`denominations`](denominations/) | 22 churches and traditions, and Protestants in general, on 55 questions, each answered from the church's own documents, with the passage named and linked. | 23 churches, 55 questions, 1,265 answers | CC BY 4.0 | [Compare Christian Denominations](https://christianpure.com/compare-denominations/) |
| [`bible-places`](bible-places/) | Every place named in the four Gospels and Acts: its location, how sure that location is, the verses that name it, and its name as the Bible in each of 11 languages prints it. | 151 places, 11 languages | CC BY 4.0 | [Bible places map](https://christianpure.com/bible-places-map/) |
| [`topical-bible`](topical-bible/) | 6,699 Bible subjects and the verses on each, from the OpenBible.info Topical Bible and our own pages, as references only. | 79,134 rows | CC BY 4.0 | [What does the Bible say about…?](https://christianpure.com/what-does-the-bible-say-about/) |
| [`easter-dates`](easter-dates/) | Western and Orthodox Easter, with Lent, Palm Sunday, Good Friday, Ascension and Pentecost, for every year from 1900 to 2099. | 200 years | CC0 (no conditions) | [When is Easter?](https://christianpure.com/when-is-easter/) |

## Using the data

You may copy, change, share and build on all of it, for any purpose, commercial or not. The Easter dates aside, every folder is released under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which asks only that you name Christian Pure as the source. A plain-text credit is enough, such as "Saints data by Christian Pure, CC BY 4.0". The Easter dates are dedicated to the public domain under [CC0](https://creativecommons.org/publicdomain/zero/1.0/) and carry no conditions at all.

If you use the data, we'd be grateful for a credit link to the page it comes from, which is named in each folder's README. That is a request, not a condition: a credit without a link is fine, and any link may carry nofollow.

Some of what the data draws on belongs to others, and the folder READMEs say what. The places on both maps come from OpenBible.info and Pleiades, and Paul's roads from the Itiner-e atlas of Roman roads; the subjects in the topic table come from OpenBible.info's Topical Bible. Their licenses ask you to keep their credits. The Bible verses are from the World English Bible, which is in the public domain. The churches' own words are not included in the denominations data, because they belong to the churches; it names and links each passage instead. No pictures are included.

## Formats

Every CSV file is UTF-8, comma separated, with a header row. Lists inside a cell are separated by a semicolon and a space. Dates are `YYYY-MM-DD`, and feast days without a year are `MM-DD`. Coordinates are WGS 84 decimal degrees.

Each folder also has a `datapackage.json` in the [Frictionless Data](https://specs.frictionlessdata.io/data-package/) format, which describes every file and field, its type and the keys that join the tables, so that tools such as the Frictionless Framework, pandas or R can load the data with the right types. For example, with Python:

```python
import pandas as pd

stops = pd.read_csv("pauls-journeys/stops.csv")
easter = pd.read_csv("easter-dates/easter-dates.csv", parse_dates=["western_easter", "orthodox_easter"])
```

## Citing

[`CITATION.cff`](CITATION.cff) gives the citation in a form GitHub and reference managers read; GitHub shows it under "Cite this repository". In short:

> Christian Pure. *Bible Data from Christian Pure*. Version 1.1.0, 19 November 2026. https://github.com/christianpure/bible-data.

## Versions and corrections

This is version 1.1.0, released on 19 November 2026, and it matches what the six tools showed that day. [`CHANGELOG.md`](CHANGELOG.md) says what changed in each version. When the tools change, a new version will follow, and older versions stay available in the repository's history.

If you find a mistake, please [open an issue](https://github.com/christianpure/bible-data/issues). We fix the tools and the data together, and corrections to our pages are logged on [our editorial standards page](https://christianpure.com/editorial-standards/).

The data was prepared by the Christian Pure editorial team.
