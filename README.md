# verify-data

Adaptive data verification that thinks before it checks.

## What It Does

Verifies any dataset by first assessing what checks actually matter for THIS data in THIS context, then running only those. Works with CSV, JSON, SQL results, Google Sheets, API outputs, LLM-generated research — anything. Produces a severity-rated report with actionable fixes and a clear verdict.

Unlike rigid checklists, this skill adapts: it reads the data, considers its origin, understands the project context, and designs a custom verification plan. LLM-generated research gets fact-checked against the web. Database exports get structural integrity checks. Manual entry gets consistency checks. Nothing runs unnecessarily.

## Who It's For

Anyone who needs to trust data before using it. Especially useful after LLM research pipelines where hallucinated facts, fabricated entities, and unsourced statistics are common failure modes.

## Usage

```
/verify-data
```

Best used in the same conversation where data was produced — the skill uses conversation context to skip discovery questions and jump straight to assessment.

## How It Works

```
Phase 1: Assessment
    Read data + context → decide what checks matter → present plan
    ↓
Phase 2: Execute
    Run only the relevant checks from the toolkit
    ↓
Phase 3: Report
    Findings by severity + health score + go-deeper option
    ↓
Phase 4: Verdict
    CLEAN / CLEAN WITH CAVEATS / NEEDS FIXES / UNVERIFIED
```

## Check Toolkit (used adaptively)

- **Structural Integrity** — schema, types, encoding, IDs
- **Completeness** — missing values, coverage gaps, truncation
- **Consistency** — duplicates, naming variations, format mismatches
- **Outliers & Anomalies** — statistical outliers, impossible values
- **Cross-Reference Validation** — multi-source agreement
- **Evidence & Citation Integrity** — source traceability
- **Factual Accuracy** — web-verified fact-checking
- **LLM Hallucination Detection** — fabricated entities, unsourced claims, templated text

## Key Principles

- Think first, check second — design a plan before running checks
- Use conversation context — don't re-ask what you already know
- Skip what doesn't apply — irrelevant checks bury real issues
- Web-verify LLM claims — "sounds right" is not verification
- One clear verdict — actionable, not a wall of caveats

## When NOT to Use

- Data cleaning/transformation (use `/survey-normalize`)
- Code review (use `/review`)
- Schema design

## Related Skills

- `/survey-normalize` — Clean and categorize verified survey data
- `/research-pipeline` — Build research pipelines (verify outputs with this skill)
- `/present` — Turn verified data into presentations

## License

MIT
