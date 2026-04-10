# Verification Checklists by Data Type

Use the appropriate checklist based on the dataset format and purpose. Check all applicable items before declaring data clean.

---

## Universal Checklist (all data types)

### Structural Integrity
- [ ] File/source is readable and not corrupted
- [ ] Row/record count matches expectations (or is plausible)
- [ ] All expected columns/fields are present
- [ ] Column/field names are spelled correctly and match spec (if provided)
- [ ] No empty rows/records mixed into data
- [ ] No encoding issues (garbled characters, BOM markers)

### Completeness
- [ ] Required fields have values in all rows
- [ ] No unexpected null/blank patterns (entire columns empty, blocks of missing data)
- [ ] Expected date range is fully covered (no gaps in time series)
- [ ] Expected categories/entities are all represented
- [ ] No truncated values (strings cut off mid-word)

### Consistency
- [ ] No exact duplicate rows (unless expected)
- [ ] Categorical fields use consistent naming (no "USA" vs "US" vs "United States")
- [ ] Date/time formats are consistent within each column
- [ ] Numeric formats are consistent (decimal separators, thousands separators)
- [ ] Case is consistent in text fields (no mixed Title Case / lowercase)

### Logical Validity
- [ ] No impossible values (negative ages, future dates in historical data, percentages > 100)
- [ ] Start dates precede end dates
- [ ] Parent-child relationships are valid (no orphan children)
- [ ] Calculated/derived fields match when recomputed
- [ ] No contradictory values across columns in the same row

### Outliers & Anomalies
- [ ] No extreme statistical outliers without explanation
- [ ] No suspicious placeholder values ("test", "TBD", "N/A", "xxx")
- [ ] No default/sentinel values masquerading as real data (0, -1, 9999, 1970-01-01)
- [ ] Distribution looks reasonable (no unexpected spikes or flatlines)

---

## CSV-Specific Checklist

- [ ] Delimiter is consistent (comma, semicolon, tab)
- [ ] Quoted fields handle embedded delimiters correctly
- [ ] Header row is present and matches expected columns
- [ ] No trailing commas creating phantom columns
- [ ] Line endings are consistent (no mixed \r\n and \n)
- [ ] Number of fields per row is consistent (no ragged rows)
- [ ] UTF-8 encoding (or declared encoding matches content)

## JSON-Specific Checklist

- [ ] Valid JSON (parseable without errors)
- [ ] Consistent schema across all records/objects
- [ ] No unexpected null vs missing-key inconsistencies
- [ ] Nested structures are consistently shaped
- [ ] Array fields have consistent element types
- [ ] No circular references
- [ ] String values don't contain unescaped special characters

## SQL Query Results Checklist

- [ ] Query returned expected number of rows
- [ ] JOIN conditions didn't create unexpected duplicates (1:many explosion)
- [ ] NULL handling is correct (NULL != 0, NULL != empty string)
- [ ] Aggregations match when cross-checked (SUM of parts = total)
- [ ] Date/timezone handling is consistent
- [ ] No implicit type coercions affecting results
- [ ] WHERE clause didn't accidentally filter too much/too little

## Google Sheets Checklist

- [ ] No merged cells affecting data extraction
- [ ] No hidden rows or columns containing data
- [ ] Formulas are resolved (no #REF!, #N/A, #VALUE! errors)
- [ ] Number formatting hasn't changed underlying values (dates stored as text, etc.)
- [ ] No conditional formatting masking data issues
- [ ] Sheet tab names are correct (if multiple tabs referenced)
- [ ] Data validation rules are in place where expected

## API Response Checklist

- [ ] HTTP status code was 200/success
- [ ] Response schema matches API documentation
- [ ] Pagination was handled correctly (all pages fetched, no duplicates)
- [ ] Rate limiting didn't cause missing data
- [ ] Timestamps are in expected timezone (usually UTC)
- [ ] No stale/cached responses
- [ ] Error responses were caught and logged, not mixed into data

## Survey Data Checklist

- [ ] Response count matches expected sample size
- [ ] No bot/spam responses (identical answers, impossible completion times)
- [ ] Skip logic was applied correctly (no answers to questions that should have been skipped)
- [ ] Scale values are within expected range (1-5, 1-10, etc.)
- [ ] Free-text responses are actually free text (not pasted HTML, URLs, etc.)
- [ ] Demographic distributions are plausible
- [ ] No duplicate respondent IDs

## Time Series Checklist

- [ ] Timestamps are sorted chronologically
- [ ] Interval is consistent (no missing periods)
- [ ] No duplicate timestamps
- [ ] Timezone is consistent across all records
- [ ] No data from before the system existed
- [ ] Daylight saving time transitions handled correctly
- [ ] Aggregation windows align as expected (daily = midnight to midnight)

## Cross-Reference Checklist (when validating against another source)

- [ ] Key columns exist in both datasets
- [ ] Key values in source exist in reference (no orphans)
- [ ] Shared fields agree on values (within acceptable tolerance)
- [ ] Both sources cover the same time period / entity set
- [ ] Aggregate totals match between sources
- [ ] Reference data is current (not outdated version)

## LLM-Generated / AI-Enriched Data Checklist

### Factual Accuracy (web-verify a sample)
- [ ] Company names exist and are spelled correctly
- [ ] Product names and features match official sources
- [ ] Founding dates, launch dates, acquisition dates are correct
- [ ] Pricing/revenue/market size numbers match published sources
- [ ] Person names + titles match LinkedIn/company pages
- [ ] Cited URLs resolve to real, relevant pages (not 404s or unrelated content)
- [ ] Geographic claims are accurate (HQ locations, operating countries)
- [ ] Partnership/integration claims are verifiable

### LLM Hallucination Signals
- [ ] No "too perfect" data — real-world data always has gaps, unknowns, and edge cases
- [ ] No templated text patterns (identical sentence structures with swapped nouns across rows)
- [ ] No unsourced specific statistics (exact percentages, market sizes, growth rates without citations)
- [ ] No entities that sound plausible but don't exist (fake companies, fake studies, fake tools)
- [ ] No confidently stated "industry standards" or "best practices" without evidence
- [ ] No suspiciously comprehensive coverage (every field filled, no "unknown" or "N/A" where real data would have gaps)
- [ ] No outdated facts presented as current (check if "current" info reflects LLM knowledge cutoff, not today)

### LLM Assumption Detection
- [ ] Universal claims are qualified ("all", "every", "always", "never" — verify or flag)
- [ ] Causal claims have evidence (not just correlation or LLM reasoning)
- [ ] Rankings/comparisons are sourced (not LLM opinion presented as fact)
- [ ] Predictions/forecasts are labeled as such (not stated as facts)
- [ ] "According to" citations actually exist and say what's claimed
- [ ] Category labels reflect real taxonomy, not LLM-invented groupings
- [ ] Relationships between entities (acquired, partnered, integrated) are verified
