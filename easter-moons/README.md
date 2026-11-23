# The Easter moon and the real moon, AD 325 to 2100

Easter falls on the Sunday after the first full moon of spring, but the churches never looked at the sky to find it. They used tables. This table sets the full moon the tables give beside the real full moon, as seen from Jerusalem, for every year from AD 325 to 2100, with the Easter each one produces.

It shows why Western and Orthodox Easter so often fall on different days. The Orthodox churches still use the old Julian tables, whose moon has drifted: it now runs about four days behind the real one. The Western churches have used the Gregorian tables since 1583, which stay within a day or two. The table also gives the Easter of the 1997 Aleppo proposal of the World Council of Churches: the same rule applied to the real moon and equinox at Jerusalem.

It is calculation, so it comes with no conditions: it is dedicated to the public domain under CC0.

## What the table shows

- **The Julian tables' moon has drifted.** In 325–600 it ran about a day early. Since 2001 it has run about four days late. In 32 of the 100 years from 2001 to 2100 the tables pick the next month's moon altogether, and in those years Orthodox Easter falls four or five weeks after Western Easter.
- **Neither church matches the real sky every year.** From 2001 to 2100, Orthodox Easter is the astronomical Easter in 27% of years and Western Easter in 90%.
- **Where Western Easter misses,** the Gregorian tables run a day or two off the real moon, or fix the equinox at 21 March when the real one falls earlier. 2019 is the best-known case; 2038, 2045 and 2049 come next.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `easter-moons-325-2100.csv` | 1,776 | One row per year, AD 325 to 2100. |
| `easter-moons-325-2100.json` | 1,776 | The same rows as JSON. |
| `datapackage.json` | | Every field described in [Frictionless Data](https://specs.frictionlessdata.io/data-package/) form. |
| `CHECKS.md`, `checks.json` | | The checks run before release and their results. |

## Dates

Civil dates are written as people wrote them at the time: in the Julian calendar to 1582, and in the Gregorian calendar from 1583. The `calendar` column names which one a row uses. Each date column has a partner column ending in `_jdn` that holds its Julian Day Number, a count of days with no calendar to doubt. Two extra columns give the Julian tables' full moon and Orthodox Easter in the Julian calendar in every year, since that is the calendar those tables run in.

The real equinox and full moon are reckoned in Jerusalem local mean time, 2 hours 21 minutes ahead of Universal Time.

## How it was worked out

- **The tables' full moon and Easter** follow the Julian (Alexandrian) reckoning in every year and the Gregorian reckoning from 1583. Before 1583 the Western church also used the Julian tables, so its Easter is the same.
- **The real equinox and full moon** come from NASA's JPL DE441 ephemeris, read with the Skyfield library, version 1.55. The full moon is the first on or after the real March equinox.
- **The Aleppo Easter** is the Sunday after that real full moon, counted at Jerusalem's meridian, as the 1997 proposal asks.
- **Days from real** count from the real full moon's date to the tables' full moon; a positive number means the tables run late.

## Fields

<!-- fields: easter-moons -->
| Field | Type | What it holds |
| --- | --- | --- |
| `year` | integer (required) | Year AD (astronomers' numbering is the same for AD years). |
| `calendar` | string (required) | Calendar of the civil dates in this row: Julian to 1582, Gregorian from 1583 (the Gregorian calendar began on 15 October 1582). |
| `real_equinox` | string (required) | The real spring (March) equinox, Jerusalem local time. Civil date written YYYY-MM-DD, in the calendar named in `calendar`. |
| `real_equinox_jdn` | integer | Julian Day Number of `real_equinox` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `real_full_moon` | string (required) | The first real full moon on or after that equinox, Jerusalem local time. Civil date written YYYY-MM-DD, in the calendar named in `calendar`. |
| `real_full_moon_jdn` | integer | Julian Day Number of `real_full_moon` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `real_full_moon_time_jerusalem` | string (required) | Time of that full moon, Jerusalem local mean time, HH:MM. |
| `aleppo_easter` | string (required) | Easter by the 1997 Aleppo proposal: the Sunday after the real full moon, reckoned at Jerusalem's meridian. Civil date written YYYY-MM-DD, in the calendar named in `calendar`. |
| `aleppo_easter_jdn` | integer | Julian Day Number of `aleppo_easter` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `julian_tables_full_moon` | string (required) | The Easter full moon of the Julian (Alexandrian) tables, which the Orthodox churches still use. Civil date written YYYY-MM-DD, in the calendar named in `calendar`. |
| `julian_tables_full_moon_jdn` | integer | Julian Day Number of `julian_tables_full_moon` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `julian_tables_full_moon_julian_calendar` | string (required) | The same full moon in the Julian calendar, the calendar the tables run in. |
| `julian_tables_days_from_real` | integer (required) | Days from the real full moon to the Julian tables' full moon (positive: the tables run late). |
| `orthodox_easter` | string (required) | Easter by the Julian tables: Orthodox Easter (and every church's Easter before 1583). Civil date written YYYY-MM-DD, in the calendar named in `calendar`. |
| `orthodox_easter_jdn` | integer | Julian Day Number of `orthodox_easter` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `orthodox_easter_julian_calendar` | string (required) | The same Easter in the Julian calendar. |
| `gregorian_tables_full_moon` | string | From 1583: the Easter full moon of the Gregorian tables. Empty before 1583. Civil date written YYYY-MM-DD, in the calendar named in `calendar`. |
| `gregorian_tables_full_moon_jdn` | integer | Julian Day Number of `gregorian_tables_full_moon` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `gregorian_tables_days_from_real` | integer | From 1583: days from the real full moon to the Gregorian tables' full moon. |
| `western_easter` | string (required) | Western Easter: by the Gregorian tables from 1583, by the Julian tables before. Civil date written YYYY-MM-DD, in the calendar named in `calendar`. |
| `western_easter_jdn` | integer | Julian Day Number of `western_easter` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `western_matches_aleppo` | string (required) | yes when Western Easter falls on the Aleppo (astronomical) date. |
| `orthodox_matches_aleppo` | string (required) | yes when Orthodox Easter falls on the Aleppo date. |
| `western_orthodox_weeks_apart` | integer (required) | Weeks from Western to Orthodox Easter: 0, 1, 4 or 5. |
<!-- /fields -->

## Checks

Every check in `CHECKS.md` passed before release. In short:

- **Western and Orthodox Easter for 1900 to 2099** match the `easter-dates` folder of this repository, and our [When is Easter?](https://christianpure.com/when-is-easter/) tool, in all 200 years.
- **2025** gives Easter on 20 April in both churches, which is also the astronomical date.
- **Every Orthodox Easter** from 325 to 2100, and every Western Easter from 1583, matches Gauss's Easter formula, worked out separately.
- **Every Easter** falls on a Sunday, and AD 325 gives 18 April (Julian calendar).

## Known gaps

- **Not every Orthodox church keeps the Julian Easter.** The Orthodox Church of Finland keeps the Western date.
- **The 1997 Aleppo proposal was never adopted.** Its Easter is given to show what the sky itself would give, not a date any church keeps.
- **Old reckonings are simplified.** Before the Julian tables settled, churches in Rome and Alexandria sometimes kept Easter on different days. This table gives the Alexandrian reckoning throughout.

## Sources

- Park, R. S., Folkner, W. M., Williams, J. G., and Boggs, D. H. 2021. "The JPL Planetary and Lunar Ephemerides DE440 and DE441." *Astronomical Journal* 161:105. doi:10.3847/1538-3881/abd414.
- Rhodes, B. Skyfield, version 1.55. Astrophysics Source Code Library ascl:1907.024. https://rhodesmill.org/skyfield/
- Meeus, J. 1998. *Astronomical Algorithms*, 2nd ed., chapter 8, "Date of Easter" (for the check against Gauss's formula).
- World Council of Churches and Middle East Council of Churches. 1997. *Towards a Common Date for Easter* (the Aleppo consultation, 5–10 March 1997).

## How to cite

> Christian Pure. *The Easter moon and the real moon, AD 325 to 2100.* In *Bible Data from Christian Pure*, version 1.4.0, 23 November 2026. https://doi.org/10.5281/zenodo.24396556.

That DOI always points to the latest version. To cite this version and no other, use https://doi.org/10.5281/zenodo.24468741.

## License

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/): no rights reserved, no conditions, no credit needed. The full text is in `LICENSE`. A credit is welcome but never required; our page that shows Easter for any year is [https://christianpure.com/when-is-easter/](https://christianpure.com/when-is-easter/).
