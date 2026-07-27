# Microsoft Fabric Pipelines

This folder contains documentation and visual evidence for the Microsoft Fabric Data Factory orchestration layer.

The Fabric pipeline definition or exported metadata will be added where supported.

---

## Planned Pipeline

```text
pl_olist_end_to_end
```

Planned workflow:

```text
Ingest Source
     |
     v
Profile Source
     |
     v
Load Bronze
     |
     v
Transform Silver
     |
     v
Run Data-Quality Tests
     |
     v
Critical Quality Gate
   /       \
Pass       Fail
 |           |
 v           v
Build Gold  Stop Pipeline
 |
 v
Update Semantic Model
 |
 v
Write Audit Record
```

---

## Planned Activities

| Sequence | Activity | Purpose |
|---:|---|---|
| 1 | Ingestion notebook | Download or validate the source |
| 2 | Profiling notebook | Analyse source structure and quality |
| 3 | Bronze notebook | Load raw Delta tables |
| 4 | Silver core notebook | Transform primary business tables |
| 5 | Silver supporting notebook | Transform payments, reviews, sellers and location |
| 6 | Quality notebook | Execute automated checks |
| 7 | Conditional quality gate | Prevent invalid Gold updates |
| 8 | Gold notebook | Build facts and dimensions |
| 9 | Semantic-model action | Make transformed data available for reporting |
| 10 | Audit action | Record pipeline completion status |

---

## Pipeline Parameters

Planned parameters include:

```text
p_run_date
p_batch_id
p_load_source
p_fail_on_quality
p_environment
```

---

## Evidence

Pipeline screenshots should be saved under:

```text
screenshots/pipeline/
```

Recommended files:

```text
01-pipeline-design.png
02-successful-pipeline-run.png
03-quality-gate.png
04-failed-run-example.png
```

---

## Documentation Rule

Whenever the pipeline changes:

1. update the pipeline in Fabric;
2. update this README;
3. update the pipeline documentation under `docs`;
4. capture a new screenshot if the visual flow changes;
5. commit the related notebook or configuration changes.