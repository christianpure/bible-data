# What Christian churches teach: 55 questions, answered from their own documents

These files set 22 Christian churches and traditions, and Protestants in general, against 55 questions of belief and practice, from the Trinity and baptism to divorce and military service. For each church and question they name the passage of the church's own documents that answers it, with a link to that passage, or say plainly that we found no official statement. It is the data behind our tool Compare Christian Denominations at [christianpure.com/compare-denominations](https://christianpure.com/compare-denominations/), which shows the passages side by side.

The table has 23 columns and 55 questions, so 1,265 answers. 1,232 are answered, 23 say that we found no official statement, and 10 are still blank.

## What is and is not in these files

The tool quotes each church's words. Those words belong to the churches that wrote them, so the quotations are not part of this release, as the tool's own page says of its download. What you get is our work: which passage answers which question, whether it answers it directly or is only the closest statement, the notes where churches of one tradition differ, and the links. Follow `source_url` to read each passage where the church publishes it.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `churches.csv` | 23 | The churches and traditions, with the main document their answers come from. |
| `questions.csv` | 55 | The questions, in eight groups. |
| `answers.csv` | 1,265 | One row for every church and question, answered or not. |
| `church-pair-articles.csv` | 54 | Our articles that compare two of the churches. |
| `denominations.json` | | All of the above in one JSON file. |
| `datapackage.json` | | The same description in [Frictionless Data](https://specs.frictionlessdata.io/data-package/) form: every field, its type and the keys that join the tables. |

The CSV files are UTF-8 with a header row and comma separated. `answers.csv` joins to `churches.csv` by `church_id` and to `questions.csv` by `question_id`.

## Fields

### churches.csv

<!-- fields: churches -->
| Field | Type | What it holds |
| --- | --- | --- |
| `church_id` | string (required) | Id of the church or tradition. |
| `church_order` | integer (required) | Order in the tool. |
| `name` | string (required) | Name of the church or tradition. |
| `short_name` | string (required) | Shorter name used in menus and tables. |
| `members` | string (required) | What its members are called, as used in a sentence. |
| `main_document` | string | The document most answers quote. Empty for "Protestant (in general)", which quotes several. |
| `main_document_url` | string | Address of that document. |
<!-- /fields -->

### questions.csv

<!-- fields: questions -->
| Field | Type | What it holds |
| --- | --- | --- |
| `question_id` | string (required) | Id of the question. |
| `question_order` | integer (required) | Order in the tool. |
| `name` | string (required) | Short name of the question. |
| `about` | string (required) | What the question asks about, as used in a sentence. |
| `group_id` | string (required) | Group the question belongs to. |
| `group_name` | string (required) | Name of the group. |
<!-- /fields -->

### answers.csv

<!-- fields: answers -->
| Field | Type | What it holds |
| --- | --- | --- |
| `church_id` | string (required) | Church (churches.csv). |
| `question_id` | string (required) | Question (questions.csv). |
| `status` | string (required) | answered: the tool answers with the passage named in source_title. no_official_statement: we looked and found no official statement. blank: not yet settled, no answer. |
| `closest_only` | boolean | true where the church has no teaching on this exact question and the passage is the closest statement. |
| `source_kind` | string | church_document: the church’s own document. christianpure_article: a Christian Pure article, where no document of the church was used. |
| `source_title` | string | The document and passage that answers the question. |
| `source_url` | string | Address of the passage. |
| `branch` | string | Where churches of the tradition differ, the body the passage comes from. |
| `branch_note` | string | Our note on how the other bodies differ. |
| `read_more_title` | string | A Christian Pure article on the subject, if any. |
| `read_more_url` | string | Address of that article. |
<!-- /fields -->

### church-pair-articles.csv

<!-- fields: church-pair-articles -->
| Field | Type | What it holds |
| --- | --- | --- |
| `church_a` | string (required) | First church (churches.csv). |
| `church_b` | string (required) | Second church. |
| `article_title` | string (required) | Title of the Christian Pure article comparing the two. |
| `article_url` | string (required) | Address of the article. |
<!-- /fields -->

## How it was made

We answered every question from what each church says of itself: its catechism or confession of faith where it has one, and otherwise the statement of beliefs it publishes, such as the Statement of Fundamental Truths of the Assemblies of God or the 28 Fundamental Beliefs of the Seventh-day Adventists. `churches.csv` names each church's main document, and every answer names its own passage, by paragraph or article number where the document has them.

Some traditions have no single voice. For the Eastern Orthodox we use Fr. Thomas Hopko's *The Orthodox Faith*, published by the Orthodox Church in America; for the Coptic Orthodox, Pope Shenouda III's *Comparative Theology*; for nondenominational and evangelical churches, the Statement of Faith of the National Association of Evangelicals; and for the Churches of Christ, which have no creed, Batsell Barrett Baxter's account of their beliefs, *Who are the churches of Christ and what do they believe?* "Protestant (in general)" draws on several documents and so has no main document. Where bodies within one tradition differ, as Lutherans and Presbyterians do on women's ordination, the answer names the body it comes from in `branch` and says how the others differ in `branch_note`.

Where a church has no teaching on the exact question but says something close, the answer gives that closest passage and `closest_only` is true. Where we looked and found no official statement at all, `status` is `no_official_statement`, and we wrote nothing in its place. For the Amish, who publish little doctrine beyond the Dordrecht Confession of 1632, five answers point to a Christian Pure article instead of a church document, and `source_kind` says so.

## Known gaps

- **Ten answers are still blank,** because we have not yet settled what passage answers them: Protestant (in general) on alcohol; The Salvation Army on blood transfusions; Nondenominational and Evangelical on head coverings and on remarriage; Church of Christ on war and military service; Pentecostal on icons and images; Oneness Pentecostal on who takes Communion, on the sacraments, and on icons and images; and Quaker on how the Bible was kept.
- **23 answers say we found no official statement:** Catholic on head coverings; Protestant (in general) on speaking in tongues, spiritual gifts today, contraception and blood transfusions; Lutheran on icons and images; Baptist on worship music; Nondenominational and Evangelical on who takes Communion, Communion bread and wine, leadership and worship music; Disciples of Christ on losing salvation and on Mary; Pentecostal on praying to saints; and nine churches on whether Mary was without sin: Lutheran, United Church of Christ, Methodist, Church of the Nazarene, The Salvation Army, Disciples of Christ, Pentecostal, Oneness Pentecostal and Quaker.
- **268 answers are the closest statement** rather than a direct answer (`closest_only` true). Read those as the nearest thing the church has said.
- **Churches revise their documents.** Some answers come from documents that change, such as the PC(USA) Book of Order 2025–2027, so a link may in time point to a newer edition. The table was last built on 9 November 2026.
- **A church's documents are not every member's belief.** The answers say what a church teaches officially, which many members hold in their own way.

## License and credit

Our selection of which passage answers which question, the statuses and flags, the notes, the ids and the way these tables are put together are released under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0); the full text is in `LICENSE`. You may copy, change and build on them for any purpose, commercial or not. The churches' documents are not ours and are not covered by that license; if you quote from them, their own terms apply. The license asks you to name Christian Pure as the source, and a plain-text credit is enough, for example:

> Denominations data by Christian Pure, CC BY 4.0.

If you use this, we'd be grateful for a credit link to [https://christianpure.com/compare-denominations/](https://christianpure.com/compare-denominations/). That is a request, not a condition: a credit without a link is fine, and any link may carry nofollow.

To cite the data in a paper, see `CITATION.cff` at the top of this repository, or use:

> Christian Pure. "What Christian Churches Teach: 55 Questions, Answered from Their Own Documents." Version 1.2.0, 19 November 2026. https://christianpure.com/compare-denominations/.

An error in this table is seen first by the church it describes, so please tell us. Open an issue in this repository; corrections to our pages are logged on [our editorial standards page](https://christianpure.com/editorial-standards/).
