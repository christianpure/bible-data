# Western and Orthodox Easter dates, 1900 to 2099

This table gives the date of Easter in the Western churches (Catholic and Protestant) and in the Eastern Orthodox churches for every year from 1900 to 2099, with the days that move with it: the start of Lent, Palm Sunday, Good Friday, Ascension and Pentecost in both traditions, and the first Sunday of Advent in the West. The dates are the ones our page [christianpure.com/when-is-easter](https://christianpure.com/when-is-easter/) works out, from the same code.

The dates are arithmetic, so they come with no conditions at all. They are dedicated to the public domain under CC0: copy them, change them and use them for anything, with no need to say where they came from.

Over the 200 years the two Easters fall on the same day 57 times, a week apart 91 times, four weeks apart 9 times and five weeks apart 43 times.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `easter-dates.csv` | 200 | One row per year. |
| `easter-dates.json` | 200 | The same rows as JSON. |
| `datapackage.json` | | The same description in [Frictionless Data](https://specs.frictionlessdata.io/data-package/) form: every field and its type. |

Dates are written `YYYY-MM-DD` on the civil (Gregorian) calendar, the one on a wall calendar, for both traditions.

## Fields

<!-- fields: easter-dates -->
| Field | Type | What it holds |
| --- | --- | --- |
| `year` | integer (required) | Year. |
| `western_easter` | date (required) | Easter Sunday in Catholic and Protestant churches (Gregorian computus). |
| `orthodox_easter` | date (required) | Easter (Pascha) in Eastern Orthodox churches (Julian computus), as a civil (Gregorian) date. |
| `same_day` | boolean (required) | true when both fall on the same day. |
| `days_apart` | integer (required) | Days from Western to Orthodox Easter: 0, 7, 28 or 35. |
| `western_ash_wednesday` | date (required) | Ash Wednesday, the first day of Lent: Easter minus 46 days. |
| `western_palm_sunday` | date (required) | Palm Sunday: Easter minus 7 days. |
| `western_good_friday` | date (required) | Good Friday: Easter minus 2 days. |
| `western_ascension` | date (required) | Ascension Day: Easter plus 39 days (a Thursday). Some places move it to the next Sunday. |
| `western_pentecost` | date (required) | Pentecost: Easter plus 49 days. |
| `western_advent_sunday` | date (required) | First Sunday of Advent: the fourth Sunday before Christmas. |
| `orthodox_clean_monday` | date (required) | Clean Monday, the first day of Great Lent: Pascha minus 48 days. |
| `orthodox_palm_sunday` | date (required) | Palm Sunday: Pascha minus 7 days. |
| `orthodox_holy_friday` | date (required) | Holy Friday: Pascha minus 2 days. |
| `orthodox_ascension` | date (required) | Ascension: Pascha plus 39 days. |
| `orthodox_pentecost` | date (required) | Pentecost (Trinity Sunday): Pascha plus 49 days. |
<!-- /fields -->

## How it was worked out

Both churches keep Easter on the Sunday after the first full moon of spring, but they reckon that moon and that spring by different calendars. Western Easter follows the Gregorian rule, computed here by the method that Jean Meeus gives in *Astronomical Algorithms* (chapter 8). Orthodox Easter follows the older Julian rule, computed by Meeus's Julian method and then moved to the civil calendar by adding the 13 days by which the Julian calendar runs behind it throughout these two centuries. The other days are counted from Easter: Ash Wednesday 46 days before, the Orthodox Clean Monday 48 days before, Palm Sunday 7, Good Friday 2, Ascension 39 days after and Pentecost 49 days after. The first Sunday of Advent is the fourth Sunday before Christmas.

We checked every year by working both Easters out a second way, with Gauss's algorithm for each calendar, and all 200 years agree. We also checked that every Easter is a Sunday between 22 March and 25 April (Western) or 4 April and 8 May (Orthodox), and that every other day falls on its weekday, and we compared sample years with the live page.

## Known gaps

- **Not every Orthodox church keeps the Orthodox date.** The Orthodox Church of Finland keeps Easter on the Western date, so for Finland use `western_easter`.
- **Ascension is sometimes moved.** Many Catholic dioceses, among them most of those in the United States, keep it on the following Sunday, 42 days after Easter, instead of the Thursday given here.
- **The Orthodox Nativity Fast and Christmas are left out** because they fall on fixed days: 15 November and 25 December for churches on the new calendar, and 28 November and 7 January for those on the old.
- **The table stops at 2099,** as the page does. From 1 March 2100 the Julian calendar runs 14 days behind the civil one, not 13, so later Orthodox dates need one more day.

## License

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/): no rights reserved, no conditions, no credit needed. The full text is in `LICENSE`. If you would like to point people to a page that shows these dates for any year, ours is [https://christianpure.com/when-is-easter/](https://christianpure.com/when-is-easter/), but you need not.
