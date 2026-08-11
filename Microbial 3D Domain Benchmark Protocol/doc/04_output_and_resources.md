# M3. Output Standardization, Resources and Coverage

## Execution Order

```bash
python progress/2-analyse/3-domain-level.py
python progress/2-analyse/A0-runtime-memory-analysis.py
python progress/2-analyse/A1b-tad-result-overview.py
python progress/2-analyse/A1c-tad-size-level-overview.py
```

The benchmark workbooks `summary.xlsx` and `time_memory-useage.xlsx` are provided under `progress/2-analyse/` for reproducing the recorded completion states, domain counts and resource records. They must be regenerated for new data rather than reused unchanged.

## Output Standardization

`3-domain-level.py` reads `progress/1-TAD-data/`, removes exact duplicate or invalid intervals, sorts by ascending start and descending end, and assigns hierarchy from coordinate containment. The outermost domain is level 1; a child domain receives its nearest parent level plus one. Intersecting intervals without containment do not form a parent-child relationship.

## Resource Summaries

`A0-runtime-memory-analysis.py` summarizes monitoring logs. Runtime and peak memory must retain their recorded units. When a wrapper processes multiple conditions, its total runtime must not be rewritten as a per-condition runtime.

## Coverage and Output Features

`A1b` records whether each chromosome-condition task contains at least one valid domain. `A1c` summarizes domain count, size, hierarchy, nesting and continuity. Coverage, zero output, timeout, OOM and unsupported input states must remain separate.

