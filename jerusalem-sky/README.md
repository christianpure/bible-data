# The sky over Jerusalem: months, Passover and eclipses, 1000 BC to AD 135

These tables work out, from the positions of the sun and moon, when each Hebrew month most likely began in Jerusalem and on which day and weekday Passover fell, for every year from 1000 BC to AD 135. They also list every eclipse that could be seen from Jerusalem, Samaria or Nineveh from 1999 BC to AD 500, and describe the sky on a few nights that writers link to the Bible: the Star of Bethlehem candidates, the two proposed dates of the crucifixion, the eclipse of 763 BC and the autumn of Paul's shipwreck.

The ancient calendar began each month when the thin crescent moon was first seen after sunset, so a table of new moons is not enough. These tables test, evening by evening, whether that crescent could have been seen from the Temple Mount. Where the answer is unsure, they give both possible evenings and say why, rather than pick one.

They are the data behind our page [When did Jesus die?](https://christianpure.com/the-day-jesus-died/). They are calculations, so they come with no conditions: they are dedicated to the public domain under CC0.

## Files

| File | Rows | What it holds |
| --- | --- | --- |
| `jerusalem-months.csv` | 14,038 | One row for each lunar month from 1000 BC to AD 135: the new moon, the first three evenings after it with the crescent's grade, and the two possible start evenings. |
| `passover-years.csv` | 1,135 | One row for each year: the spring equinox, the new moon that began Nisan, and 14 and 15 Nisan with their weekdays under both start rules, and the 14th of the month before and after. |
| `eclipses-jerusalem-samaria-nineveh.csv` | 21,137 | One row for each eclipse at each of the three places, 1999 BC to AD 500: 6,010 lunar eclipses, and every solar eclipse that touched one of the places while the sun was up. |
| `named-nights.json` | | The sky on the named nights listed below. |
| `*.json` | | Each CSV table again as JSON, with the same rows. |
| `datapackage.json` | | Every file and field described in [Frictionless Data](https://specs.frictionlessdata.io/data-package/) form. |
| `CHECKS.md`, `checks.json` | | The checks run before release and their results. |

## Dates and years

Every date is in the Julian calendar, the one historians use for dates before 15 October 1582. Years use astronomers' numbering, in which 1 BC is year 0 and 2 BC is year −1, so a date such as `-0999-04-13` is 13 April 1000 BC. The `year_label` column gives the same year as BC or AD.

Each date column has a partner column ending in `_jdn`. It holds the Julian Day Number: a count of days used by astronomers, with no calendar to doubt. 3 April AD 33 is day 1733204. Weekdays follow from it: the day number plus one, divided by seven, leaves 0 for Sunday, 1 for Monday and so on.

Times are local mean time at the place (Jerusalem is 2 hours 21 minutes ahead of Universal Time), except columns marked UT.

## How it was worked out

- **The sun and moon** come from NASA's JPL DE441 ephemeris, read with the Skyfield library, version 1.55.
- **The place** is the Temple Mount, at 31.7781° N, 35.2354° E, 740 metres up.
- **The crescent test** is Yallop's (NAO Technical Note 69, 1997), worked out at his "best time" for a sighting: four-ninths of the way from sunset to moonset. His grades run from A (easily seen) to F (not visible). Grades A and B mean the crescent could be seen by eye in good conditions; grade C means it could only just be seen.
- **Two start evenings** are given for each month. The *likely* one is the first evening graded A or B. The *earliest* is the first evening graded C or better. A month begins at sunset on its start evening, so its first full day is the next daylight day, and no month runs past 30 days. In 6 months the start came from that 30-day rule rather than a sighting, and the margin column says so.
- **Nisan** is taken to be the month whose 14th day is the first to fall on or after the spring equinox. Nobody knows how the extra thirteenth month was added in a given year, so the 14th of the month before and of the month after are given too.
- **Passover dates** (14 Nisan) are the daylight day. The Jewish day began at sunset, so 14 Nisan began on the evening before the date in the table.
- **Earth's clock (Delta T).** Earth's spin has slowed unevenly, so the gap between clock time and the sun's time in ancient years is known only within a margin. Delta T itself is Skyfield's: Morrison, Stephenson, Hohenkerk and Zawilski (2021) for 720 BC to AD 2015, and the long-term curve of Stephenson, Morrison and Hohenkerk (2016) before that. Its margin, one standard error, is 0.8 t² seconds, where t is centuries from 1820 (Morrison and Stephenson 2004, as NASA uses it). A month's margin column is filled in when moving Delta T by twice that error could move its start by a night. That happens in 318 of the 14,038 months under the likely rule.
- **Eclipses** are worked out three times at each place: with the usual Delta T, and with Delta T moved by twice its standard error each way. The columns ending `_dt_low`, `_dt_mid` and `_dt_high` show whether that changes the answer. Places and their IDs come from the `bible-places` folder in this repository.
- **Bright stars are not included.** The one star in the data, Regulus, is entered from its published Hipparcos position (ESA 1997) for its meetings with Jupiter.

## Named nights

`named-nights.json` records:

- **Star of Bethlehem candidates.** Jupiter met Saturn three times in Pisces in 7 BC (29 May, 30 September and 5 December). Jupiter came within 0.07° of Venus on 12 August 3 BC and within 0.007° on 17 June 2 BC. It passed Regulus on 14 September 3 BC, 17 February 2 BC and 9 May 2 BC. Its turning points are listed too; one falls on 27 December 2 BC. A planet stands almost still for days around a turning point, so that exact day is soft.
- **AD 30 and AD 33.** Sunset, moonrise and moonset, and where the sun, moon and planets stood an hour after sunset. On Friday 3 April AD 33 the moon rose at 18:18 local time, already in eclipse, and the sun set at 18:19.
- **15 June 763 BC.** The sky over Jerusalem at greatest eclipse. Linking this eclipse to Amos 8:9 is a proposal that goes back to Cowell (1906); the `bible-natural-events` folder grades it.
- **Paul's voyage (Acts 27).** The Fast (10 Tishri) in AD 59 and AD 60, and the moon's phases at Malta for 75 days after it. The Fast falls on 7 October AD 59 and 25 September AD 60. Ramsay put it on 5 October AD 59, using a different reconstruction of the calendar.

## Fields

### `jerusalem-months.csv`

<!-- fields: jerusalem-months -->
| Field | Type | What it holds |
| --- | --- | --- |
| `year` | integer (required) | Year in astronomers' numbering: 1 BC is 0, 2 BC is -1, AD 1 is 1. |
| `year_label` | string (required) | The same year written for readers, BC or AD. |
| `new_moon_jd_ut` | number (required) | Moment of the true new moon (sun and moon at the same ecliptic longitude) as a Julian Date in Universal Time. |
| `new_moon_date_local` | string (required) | Date of the new moon in Jerusalem local mean time (UT + 2 h 21 min). Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `new_moon_date_local_jdn` | integer | Julian Day Number of `new_moon_date_local` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `new_moon_time_local` | string (required) | Time of the new moon, local mean time, HH:MM. |
| `delta_t_s` | integer (required) | Delta T used (TT minus UT), in seconds, as Skyfield gives it. |
| `delta_t_sigma_s` | integer (required) | Standard error of Delta T in seconds, 0.8 t^2 with t in centuries from 1820 (Morrison and Stephenson 2004). |
| `eve1_date` | string (required) | Evening 1 after the new moon: its date. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `eve1_date_jdn` | integer | Julian Day Number of `eve1_date` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `eve1_moon_age_h` | number | Moon's age at sunset on that evening, in hours from the new moon. |
| `eve1_lag_min` | integer | Minutes from sunset to moonset that evening (negative when the moon set first). |
| `eve1_q` | number | Yallop's q value at his best time for sighting (sunset plus four-ninths of the lag). |
| `eve1_grade` | string | Yallop's visibility grade: A easily seen by eye, B seen by eye in perfect conditions, C may need optical aid to find, then seen by eye, D needs optical aid, E not visible with a telescope, F not visible (the moon sets before the sun or is below Danjon's limit). |
| `eve2_date` | string (required) | Evening 2 after the new moon: its date. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `eve2_date_jdn` | integer | Julian Day Number of `eve2_date` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `eve2_moon_age_h` | number | Moon's age at sunset on that evening, in hours from the new moon. |
| `eve2_lag_min` | integer | Minutes from sunset to moonset that evening (negative when the moon set first). |
| `eve2_q` | number | Yallop's q value at his best time for sighting (sunset plus four-ninths of the lag). |
| `eve2_grade` | string | Yallop's visibility grade: A easily seen by eye, B seen by eye in perfect conditions, C may need optical aid to find, then seen by eye, D needs optical aid, E not visible with a telescope, F not visible (the moon sets before the sun or is below Danjon's limit). |
| `eve3_date` | string (required) | Evening 3 after the new moon: its date. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `eve3_date_jdn` | integer | Julian Day Number of `eve3_date` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `eve3_moon_age_h` | number | Moon's age at sunset on that evening, in hours from the new moon. |
| `eve3_lag_min` | integer | Minutes from sunset to moonset that evening (negative when the moon set first). |
| `eve3_q` | number | Yallop's q value at his best time for sighting (sunset plus four-ninths of the lag). |
| `eve3_grade` | string | Yallop's visibility grade: A easily seen by eye, B seen by eye in perfect conditions, C may need optical aid to find, then seen by eye, D needs optical aid, E not visible with a telescope, F not visible (the moon sets before the sun or is below Danjon's limit). |
| `likely_start_evening` | string (required) | Likely start: the first evening graded A or B. The month begins at sunset that evening, so day 1 is the next daylight day. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `likely_start_evening_jdn` | integer | Julian Day Number of `likely_start_evening` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `likely_margin` | string | Empty when the likely start is firm. Otherwise says in words why it could move a night: moving Delta T by twice its standard error, or the 30-day rule. |
| `earliest_start_evening` | string (required) | Earliest start: the first evening graded C or better. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `earliest_start_evening_jdn` | integer | Julian Day Number of `earliest_start_evening` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `earliest_margin` | string | As likely_margin, for the earliest start. |
<!-- /fields -->

### `passover-years.csv`

<!-- fields: passover-years -->
| Field | Type | What it holds |
| --- | --- | --- |
| `year` | integer (required) | Year in astronomers' numbering: 1 BC is 0, 2 BC is -1, AD 1 is 1. |
| `year_label` | string (required) | The same year written for readers, BC or AD. |
| `spring_equinox` | string (required) | Date of the spring (March) equinox in Jerusalem local mean time. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `spring_equinox_jdn` | integer | Julian Day Number of `spring_equinox` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `nisan_new_moon` | string (required) | Date of the true new moon that began Nisan, local mean time. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `nisan_new_moon_jdn` | integer | Julian Day Number of `nisan_new_moon` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `nisan14_likely` | string (required) | 14 Nisan (Passover) under the likely start: the daylight day. The Jewish day began at sunset the evening before. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `nisan14_likely_jdn` | integer | Julian Day Number of `nisan14_likely` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `nisan14_likely_weekday` | string (required) | Weekday of `nisan14_likely`. |
| `nisan15_likely` | string (required) | 15 Nisan under the likely start: the daylight day. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `nisan15_likely_jdn` | integer | Julian Day Number of `nisan15_likely` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `nisan15_likely_weekday` | string (required) | Weekday of `nisan15_likely`. |
| `likely_margin` | string | Empty when firm; otherwise why 14 Nisan could move a day under the likely rule. |
| `nisan14_earliest` | string (required) | 14 Nisan under the earliest start: the daylight day. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `nisan14_earliest_jdn` | integer | Julian Day Number of `nisan14_earliest` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `nisan14_earliest_weekday` | string (required) | Weekday of `nisan14_earliest`. |
| `nisan15_earliest` | string (required) | 15 Nisan under the earliest start: the daylight day. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `nisan15_earliest_jdn` | integer | Julian Day Number of `nisan15_earliest` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `nisan15_earliest_weekday` | string (required) | Weekday of `nisan15_earliest`. |
| `earliest_margin` | string | Empty when firm; otherwise why 14 Nisan could move a day under the earliest rule. |
| `nisan14_if_month_before` | string (required) | 14th day of the month before, likely start: Passover if Nisan was a month earlier. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `nisan14_if_month_before_jdn` | integer | Julian Day Number of `nisan14_if_month_before` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `nisan14_if_month_before_weekday` | string (required) | Weekday of `nisan14_if_month_before`. |
| `nisan14_if_month_after` | string (required) | 14th day of the month after, likely start: Passover if a thirteenth month was added. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `nisan14_if_month_after_jdn` | integer | Julian Day Number of `nisan14_if_month_after` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `nisan14_if_month_after_weekday` | string (required) | Weekday of `nisan14_if_month_after`. |
<!-- /fields -->

### `eclipses-jerusalem-samaria-nineveh.csv`

<!-- fields: eclipses -->
| Field | Type | What it holds |
| --- | --- | --- |
| `kind` | string (required) | solar or lunar. |
| `type` | string (required) | Type of eclipse: for lunar, Total, Partial or Penumbral as seen from Earth; for solar, the type seen at this place (Total, Annular, Partial). |
| `year` | integer (required) | Year in astronomers' numbering: 1 BC is 0, 2 BC is -1, AD 1 is 1. |
| `year_label` | string (required) | The same year written for readers, BC or AD. |
| `greatest_ut_date` | string (required) | Date of greatest eclipse in Universal Time. Civil date, Julian calendar, astronomers' year numbering (1 BC is 0000, 2 BC is -0001), written YYYY-MM-DD. |
| `greatest_ut_date_jdn` | integer | Julian Day Number of `greatest_ut_date` (the day that begins at noon UT on that date): one count of days with no calendar to doubt. |
| `greatest_ut` | string (required) | Time of greatest eclipse, UT, HH:MM. For a solar eclipse, greatest as seen at this place. |
| `greatest_jd_ut` | number (required) | Greatest eclipse as a Julian Date in UT. |
| `delta_t_s` | integer (required) | Delta T used, seconds. |
| `delta_t_2sigma_s` | integer (required) | Twice the standard error of Delta T, seconds: the margin each way. |
| `place_id` | string (required) | Place ID in the bible-places folder of this repository. |
| `place` | string (required) | Place name: Jerusalem, Samaria or Nineveh. |
| `greatest_local` | string | Greatest eclipse at the place. Local mean time at the place, Julian calendar, astronomers' years: YYYY-MM-DD HH:MM. |
| `phase_start_local` | string | Start of the umbral phase (lunar) or first contact (solar). Local mean time at the place, Julian calendar, astronomers' years: YYYY-MM-DD HH:MM. |
| `phase_end_local` | string | End of the umbral phase (lunar) or last contact (solar). Local mean time at the place, Julian calendar, astronomers' years: YYYY-MM-DD HH:MM. |
| `magnitude` | number | Lunar: umbral magnitude (share of the moon's diameter inside Earth's dark shadow; 1 or more is total; negative for penumbral eclipses). Solar: share of the sun's diameter covered at this place. |
| `penumbral_magnitude` | number | Lunar only: penumbral magnitude. |
| `magnitude_dt_low` | number | Solar only: magnitude at the place with Delta T moved down by twice its standard error. |
| `magnitude_dt_high` | number | Solar only: magnitude with Delta T moved up by twice its standard error. |
| `body_alt_at_greatest_dt_low` | number | Height of the moon (lunar) or sun (solar) above the horizon at greatest, degrees, Delta T low. |
| `body_alt_at_greatest_dt_mid` | number | The same with the usual Delta T. |
| `body_alt_at_greatest_dt_high` | number | The same with Delta T high. |
| `visible_dt_low` | string | yes if any of the eclipse could be seen from the place, Delta T low. |
| `visible_dt_mid` | string | The same with the usual Delta T. |
| `visible_dt_high` | string | The same with Delta T high. |
| `minutes_visible_dt_low` | integer | Minutes of the eclipse with the body above the horizon (lunar: umbral phase, moon up and sun down), Delta T low. |
| `minutes_visible_dt_mid` | integer | The same with the usual Delta T. |
| `minutes_visible_dt_high` | integer | The same with Delta T high. |
| `first_seen_local` | string | When the eclipse could first be seen, usual Delta T. Local mean time at the place, Julian calendar, astronomers' years: YYYY-MM-DD HH:MM. |
| `sun_alt_when_first_seen` | number | Height of the sun at that moment, degrees (lunar: shows whether the sky was still light). |
<!-- /fields -->

## Checks

Every check in `CHECKS.md` passed before release. In short:

- **AD 30 and AD 33** match Humphreys and Waddington (*Nature* 306, 1983): under the likely rule, 14 Nisan falls on Friday 7 April AD 30 and Friday 3 April AD 33.
- **New moons** fall within 8 minutes of NASA's Five Millennium Catalog of Moon Phases for AD 1 to 135, and within 19 minutes for 1000 to 901 BC. The gap comes from the two estimates of Delta T: NASA uses Morrison and Stephenson's 2004 values.
- **Lunar eclipses** match NASA's Five Millennium Canon for 800 to 701 BC and AD 1 to 100. The share of the moon covered differs by at most 0.009, and the time of greatest eclipse by at most 5 minutes. One grazing eclipse of the outer shadow in 780 BC, covering 0.0004 of the moon's width, is in NASA's list but not ours; nobody could have seen it. For 3 April AD 33 our 0.575 compares with NASA's 0.5764.
- **Every month** runs 29 or 30 days, and every year has one Passover row.
- **The live page** [When did Jesus die?](https://christianpure.com/the-day-jesus-died/) shows the same Passover dates for every year and the same AD 33 eclipse.

## Known gaps

- **The crescent test is a model.** Yallop's grades predict what an observer could see on a clear evening. Dust, cloud or a missed watch could delay a sighting by a night, and no list of actual first sightings from ancient Jerusalem survives to test against. That is why two start evenings are given.
- **Nobody knows when the extra month was added.** The Nisan rule here is one reasonable rule, not a record. Use the month-before and month-after columns when it matters.
- **The calendar of the time may not have followed sighting at all** in every period. Some writers argue for calculated calendars in parts of this span. These tables answer only what the sky allowed.
- **Solar eclipses** were not compared with NASA's solar canon across the whole table; only those the `bible-natural-events` folder uses were compared.
- **The Delta T margin grows the further back a row goes.** Twice the standard error is about 9 minutes in AD 1, 21 minutes in 1000 BC and 39 minutes in 2000 BC, so times in the oldest rows are less sure. The margin columns say where it changes an answer.

## Sources

- Park, R. S., Folkner, W. M., Williams, J. G., and Boggs, D. H. 2021. "The JPL Planetary and Lunar Ephemerides DE440 and DE441." *Astronomical Journal* 161:105. doi:10.3847/1538-3881/abd414.
- Rhodes, B. Skyfield, version 1.55. Astrophysics Source Code Library ascl:1907.024. https://rhodesmill.org/skyfield/
- Yallop, B. D. 1997. *A Method for Predicting the First Sighting of the New Crescent Moon.* NAO Technical Note 69. HM Nautical Almanac Office.
- Morrison, L. V., and Stephenson, F. R. 2004. "Historical values of the Earth's clock error ΔT and the calculation of eclipses." *Journal for the History of Astronomy* 35:327–336. doi:10.1177/002182860403500305.
- Stephenson, F. R., Morrison, L. V., and Hohenkerk, C. Y. 2016. "Measurement of the Earth's rotation: 720 BC to AD 2015." *Proceedings of the Royal Society A* 472:20160404. doi:10.1098/rspa.2016.0404.
- Morrison, L. V., Stephenson, F. R., Hohenkerk, C. Y., and Zawilski, M. 2021. "Addendum 2020 to 'Measurement of the Earth's rotation: 720 BC to AD 2015'." *Proceedings of the Royal Society A* 477:20200776. doi:10.1098/rspa.2020.0776.
- Espenak, F., and Meeus, J. *Five Millennium Canon of Lunar Eclipses* and *Five Millennium Catalog of Moon Phases.* NASA. https://eclipse.gsfc.nasa.gov/
- Humphreys, C. J., and Waddington, W. G. 1983. "Dating the Crucifixion." *Nature* 306:743–746. doi:10.1038/306743a0.
- ESA 1997. *The Hipparcos and Tycho Catalogues.* ESA SP-1200 (Regulus, HIP 49669).

## How to cite

> Christian Pure. *The sky over Jerusalem: months, Passover and eclipses, 1000 BC to AD 135.* In *Bible Data from Christian Pure*, version 1.4.0, 23 November 2026. https://doi.org/10.5281/zenodo.24396556.

## License

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/): no rights reserved, no conditions, no credit needed. The full text is in `LICENSE`. A credit is welcome but never required; if you would like to point people to a page that lets them explore these dates, ours is [https://christianpure.com/the-day-jesus-died/](https://christianpure.com/the-day-jesus-died/).
