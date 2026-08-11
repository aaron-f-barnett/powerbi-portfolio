# Renamed & Cleaned R8 2011-2020

Harmonized series of BLS Table R8 (incidence rates for nonfatal occupational injuries and illnesses involving days away from work, per 10,000 full-time workers, private industry), healthcare scope, 2011-2020. 2021-2024 excluded by design (COVID distortion and dual-year tables).

Every file contains the identical 23 categories in the same order: the all-private-industry benchmark row, the Health care and social assistance sector row (NAICS 62), and the full Ambulatory (621), Hospitals (622), and Nursing and residential care (623) branches. Category labels are harmonized across all ten years — see RENAMING_LOG.md for every rename and the argument for it.

## Sources and file structure

2011-2015 were transcribed from the BLS PDF tables (event/exposure columns from screenshots, totals and NAICS codes extracted directly from the PDF text layer). They carry the columns: Year, NAICS code, Industry, Total cases, and the 12 event/exposure categories from overexertion through all-other-events. The contact-with-objects and falls/slips/trips column groups were not transcribed for these years.

2016-2020 are cleaned copies of the workbooks sliced from the BLS source files; they retain their original column layout, including the contact-with-objects and falls/slips/trips groups that the 2011-2015 files lack. Column sets therefore differ between the two eras; the columns they share are identical in meaning.

## Cleaning operations applied

Duplicate removal. BLS prints "Offices of physicians" twice in every 2016-2020 source table (NAICS 6211 and 62111 - the same category at two hierarchy levels, identical values). The second occurrence was removed from each 2016-2020 file after verifying the two rows' values were identical. The 2011-2015 files were built deduplicated from the start (the PDFs triple-print this category at NAICS 6211/62111/621111 levels; 621111 "except mental health specialists" is a genuinely distinct child and was kept).

Backfilled category rows ("-" in every data cell). BLS did not publish these categories in these years; the rows were added so every vintage has the same 23 categories:

| Year | Category backfilled | Reason |
|---|---|---|
| 2011 | Offices of other health practitioners | Not published in the 2011 PDF |
| 2013 | Offices of physicians, mental health specialists | Not published in the 2013 PDF |
| 2017 | Offices of physicians (except mental health specialists) | Not in the 2017 BLS source workbook |
| 2017 | Offices of dentists | Not in the 2017 BLS source workbook |
| 2018 | Offices of other health practitioners | Not in the 2018 BLS source workbook |

All five gaps were verified against the original BLS documents (not slicing artifacts).

Dash convention. "-" (or the en dash "–" in the 2017-2020 files, matching each file's existing convention) means BLS did not publish the value: either the source shows a dash (does not meet publication criteria / too small to display) or a "data too small to be displayed" footnote marker sat in place of the value. In the 2011-2015 files this includes the fires-and-explosions cells on sector rows where the PDF prints a footnote reference instead of a number. Backfilled rows use the same convention. Treat all dashes as null when importing; do not treat as zero.

NAICS codes. A NAICS code column was added to 2011-2015, with codes taken from the PDFs' own NAICS column. Verification across all ten vintages: no code was re-used or re-indexed for a different category during 2011-2020 within this scope. The span crosses NAICS 2007 (2011-2013), NAICS 2012 (2014-2018), and NAICS 2017 (2019-2020) revisions, but in sector 62 these revisions changed only label wording, never the code-to-category mapping. Two cosmetic differences to be aware of when joining on code: the 2017-2020 sources zero-pad codes to six digits (621100 vs 6211) and store them as text, and the removed duplicate means 6211 appears once per file. Given the padding inconsistency, name-based joins on the harmonized labels are the recommended key, with codes as a secondary check — consistent with the decision to prefer nomenclature over numeric indexing.

The benchmark row ("Private industry (all industries)") intentionally has no NAICS code. It is the aggregate rate for all private employers - (N/EH) x 20,000,000 across the whole private economy - not an average of industry rates. Use it for baseline comparisons; exclude it from any visual that sums or ranks industries.

## Scope decisions (recorded, not applied)

The Social assistance branch (NAICS 624) is excluded from this series by decision, for all ten years. It exists in every source document 2011-2020, so it can be added later if wanted. Findings recorded for that branch in case it is ever brought in: "Other individual and family services" (62419) was not published 2014-2016; the 62423 "Emergency and other relief services" child row is missing from the 2019 source; in the 2016-2018 sources the NAICS 6242 parent ("Community food and housing, and emergency and other relief services") is mislabeled as "Emergency and other relief services," colliding with its own 62423 child; and "Services for the elderly and disabled" (2016-2018) is the same category as "Services for the elderly and persons with disabilities" (62412).

## Provenance chain

PDF/source workbooks from BLS -> healthcare rows sliced (2016-2020 by hand; 2011-2015 transcribed) -> this cleaned folder. Cleaning performed 2026-08-09.
