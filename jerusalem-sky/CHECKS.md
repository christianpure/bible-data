# Checks

Run on 2026-11-23, before release. 23 of 23 checks pass.


## Easter moons

- **Pass:** Western and Orthodox Easter, 1900-2099, match the published easter-dates table (the /when-is-easter/ tool) exactly. 200 years compared, 0 differ
- **Pass:** AE4: 2025 gives Easter on 20 April in both tables and by the real moon. western 2025-04-20, orthodox 2025-04-20, astronomical (Aleppo) 2025-04-20
- **Pass:** Every Orthodox Easter, AD 325-2100, matches Gauss's Julian Easter formula. 1776 years, 0 differ
- **Pass:** Every Western Easter, 1583-2100, matches Gauss's Gregorian Easter formula. 518 years, 0 differ
- **Pass:** Before 1583 Western and Orthodox Easter are the same day (one Julian table). 0 differ
- **Pass:** Every Easter (Western, Orthodox, astronomical) falls on a Sunday by its day number. 0 not Sunday
- **Pass:** AD 325: Easter on 18 April (Julian calendar). table gives 0325-04-18

## Months and Passover

- **Pass:** Every month under the likely rule runs 29 or 30 days. 14038 months, lengths found: [29, 30]
- **Pass:** Every month under the earliest rule runs 29 or 30 days. 14038 months, lengths found: [29, 30]
- **Pass:** Every year from 1000 BC (-999) to AD 135 has one Passover row. 1135 rows, -999 to 135
- **Pass:** Every Passover day number matches its Julian date, and its weekday matches the day number. 0 mismatches in 1135 rows
- **Pass:** Humphreys and Waddington (Nature 306, 1983): 14 Nisan on Friday 7 April AD 30 and Friday 3 April AD 33. AD 30: 0030-04-07 Friday; AD 33: 0033-04-03 Friday (likely rule; the earliest rule gives 0030-04-06 and 0033-04-03)

## Live page /the-day-jesus-died/

- **Pass:** The page's Passover table (every year, 1000 BC to AD 135) matches passover-years.csv. 1135 years compared, 0 differ
- **Pass:** AD 33 Passover on the page: 14 Nisan Friday 3 April. release: 0033-04-03 Friday
- **Pass:** AD 33 lunar eclipse on the page matches the eclipse table (magnitude, times, minutes seen). page {"magnitude": 0.575, "start": "15:46", "greatest": "17:11", "end": "18:36", "minutes_seen": [26, 18, 9]}; release {"magnitude": 0.575, "start": "15:46", "greatest": "17:11", "end": "18:36", "minutes_seen": [26, 18, 9]}
- **Pass:** Sunset and moonrise on the page for AD 30 and AD 33 appear in named-nights.json. AD 30 sunset 18:21 moonrise 19:14; AD 33 sunset 18:19 moonrise 18:18

## NASA catalogues

- **Pass:** New moons, 1000 BC to 901 BC, against NASA's Five Millennium Catalog of Moon Phases. 1236 new moons; ours minus NASA's: median +18.0 min, largest 19.0 min. The gap is mostly the two estimates of Delta T (NASA uses Morrison and Stephenson 2004; Skyfield the 2016/2021 values).
- **Pass:** New moons, AD 1 to 100, against NASA's Five Millennium Catalog of Moon Phases. 1237 new moons; ours minus NASA's: median +7.4 min, largest 8.1 min. The gap is mostly the two estimates of Delta T (NASA uses Morrison and Stephenson 2004; Skyfield the 2016/2021 values).
- **Pass:** New moons, AD 101 to 135, against NASA's Five Millennium Catalog of Moon Phases. 433 new moons; ours minus NASA's: median +7.4 min, largest 8.1 min. The gap is mostly the two estimates of Delta T (NASA uses Morrison and Stephenson 2004; Skyfield the 2016/2021 values).
- **Pass:** Lunar eclipses, 800 BC to 701 BC, against NASA's Five Millennium Canon of Lunar Eclipses. 239 eclipses in NASA's list, 0 missing from ours, apart from 1 graze of the outer shadow that the engine does not list: -0780 Dec 13 (penumbral magnitude 0.0004); umbral magnitude differs by at most 0.0036 (median 0.0005); greatest eclipse, ours minus NASA's: median +4.3 min, largest 4.9 min (Delta T estimates differ).
- **Pass:** Lunar eclipses, AD 1 to 100, against NASA's Five Millennium Canon of Lunar Eclipses. 251 eclipses in NASA's list, 0 missing from ours; umbral magnitude differs by at most 0.0092 (median 0.0009); greatest eclipse, ours minus NASA's: median +2.5 min, largest 3.3 min (Delta T estimates differ).
- **Pass:** 3 April AD 33: umbral magnitude 0.575 against NASA's 0.5764. ours 0.575

## bible-natural-events (version 1.3.0)

- **Pass:** Eclipses the 1.3.0 ledger shares with this table: same eclipse, same place, magnitude within 0.03. 24 ledger rows at Jerusalem, Samaria or Nineveh; 0 not in this table; largest magnitude gap 0.000 (e-joshua-sun-stands, Samaria, -1206-10-30). Both tables come from the same calculation, so they must agree.

## Not checked here

- Solar eclipses against NASA's solar canon across the whole table. Only the solar eclipses that the natural-events ledger uses (15 June 763 BC among them) are compared above, and only with the ledger.
- The crescent grades. Yallop's test is a published model, not an observation, and no outside list of first sightings for ancient Jerusalem exists to check it against.
