# Bible subjects and their verses

This table lists over 6,500 Bible subjects, from "10 commandments" to "zoroastrian priests", and the verses on each: 79,134 rows, one for each subject, verse and source. It joins the rankings of the OpenBible.info Topical Bible with the verses that Christian Pure's own pages on 418 of those subjects quote, and links each subject to our page where we have one. It is the data behind our search page [What does the Bible say about…?](https://christianpure.com/what-does-the-bible-say-about/)

The table holds verse references only, no Bible text, so you can pair it with any translation you are free to use.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `topical-bible.csv` | 79,134 | One row per subject, verse and source. |

The CSV file is UTF-8 with a header row, comma separated. Each row has the reference twice: as people write it (`Philippians 4:6–7`) and in OSIS form (`Phil.4.6-Phil.4.7`), which most Bible software reads. A subject, a verse and a source together pick out one row.

## Fields

<!-- fields: topical-bible -->
| Field | Type | What it holds |
| --- | --- | --- |
| `topic` | string (required) | The subject, as OpenBible.info names it (names that differ only in spaces or hyphens are joined). |
| `topic_key` | string (required) | A web-safe key for the subject. |
| `reference` | string (required) | The verse or passage in English numbering, for example "Philippians 4:6–7". |
| `osis` | string (required) | The same reference in OSIS form, for example "Phil.4.6-Phil.4.7". |
| `source` | string (required) | "OpenBible.info" for a verse in its Topical Bible; "Christian Pure" for a verse our page on the subject quotes. |
| `openbible_score` | integer | OpenBible.info's helpfulness score for the verse on that subject (higher is more helpful). Empty for our picks. |
| `christianpure_page` | string | Our page of verses on the subject, where we have one. |
<!-- /fields -->

## How it was made

The subjects and their ranked verses come from the OpenBible.info Topical Bible, downloaded on 18 November 2026. OpenBible.info ranks each verse on each subject by readers' votes, and `openbible_score` keeps that score; the 71,349 rows with `source` "OpenBible.info" are its verses. We joined subject names that differ only in spaces or hyphens.

For the 418 subjects on which Christian Pure has a page of Bible verses, we added the verses that page quotes, 7,785 rows with `source` "Christian Pure" and no score. A verse that both sources list appears twice, once for each, so you can keep either set or both. Every row of those 418 subjects carries the link to our page in `christianpure_page`.

## Known gaps

- **English numbering.** References follow the verse numbering of English Bibles. Some Hebrew and Greek editions, and Bibles in other languages, number a few chapters differently. Even among English Bibles there are differences: five rows end at Romans 16:27 or 3 John 15, verses the World English Bible numbers otherwise (it prints the end of Romans as 14:24–26 and gives 3 John 14 verses).
- **Subjects as people searched for them.** OpenBible.info's subjects come from what people searched for on the web, so they include odd ones and near-duplicates, such as "anxiety" and "worry". We kept them as they are.
- **Scores change.** OpenBible.info's votes keep coming in; these scores are as downloaded on 18 November 2026.

## Sources and their licenses

- **OpenBible.info**, Topical Bible, [openbible.info/topics](https://www.openbible.info/topics/), CC BY 4.0: the subjects, their verses and their scores. Please keep its credit when you reuse the table.

## License and credit

The combined table is released under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0); the full text is in `LICENSE`. You may copy, change and build on it for any purpose, commercial or not. Please credit both sources; a plain-text credit is enough, for example:

> Topical Bible data from OpenBible.info and Christian Pure, CC BY 4.0.

If you use this, we'd be grateful for a credit link to [https://christianpure.com/what-does-the-bible-say-about/](https://christianpure.com/what-does-the-bible-say-about/). That is a request, not a condition: a credit without a link is fine, and any link may carry nofollow.

To cite the data in a paper, see `CITATION.cff` at the top of this repository, or use:

> Christian Pure. "Bible Subjects and Their Verses." Version 1.4.1, 23 November 2026. https://christianpure.com/what-does-the-bible-say-about/.

Found a mistake? Please open an issue in this repository. Corrections to our pages are logged on [our editorial standards page](https://christianpure.com/editorial-standards/).
