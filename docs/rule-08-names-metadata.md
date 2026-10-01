# Rule 8: Standardize data names, formats, and metadata

The checklist below covers typical naming and documentation decisions. It should be completed once at the start of a project, revisited when a new data source is added, and stored in `docs/data_dictionary.md` alongside the schema it describes.

## Minimum standardization checklist

- [ ] Subject IDs follow one convention.
- [ ] Task names follow one convention.
- [ ] Run labels follow one convention.
- [ ] Event names are canonical.
- [ ] Column names are consistent across files.
- [ ] Variable meanings are documented.
- [ ] Derived variables are identified.
- [ ] Allowed values and units are recorded.
- [ ] Metadata files travel with the data.
- [ ] Analysis scripts use dictionaries/configs instead of hard-coded special cases.

## Example canonical naming table

| Concept | Use this | Avoid |
|---|---|---|
| Participant ID | `sub-000` | `S001`, `participant_0` |
| Task name | `task-obslearn` | `OL`, `observationLearning`, `obs` |
| Run label | `run-01` | `run1`, `Run1`, `first` |
| Trial type | `play_choice` | `choice`, `selfChoice`, `choice_trial` |
| Response time | `response_time` | `RT`, `rt_sec`, `reactionTime` |
| Missed response | `missed_response` | `no_key`, `blank`, `fail` |

## Example `events.tsv` convention

| onset | duration | trial_type | response_time | missed_response |
|---:|---:|---|---:|---:|
| 12.40 | 2.00 | `observe_stimulus` | n/a | 0 |
| 18.75 | 3.50 | `play_choice` | 1.24 | 0 |
| 25.10 | 1.00 | `feedback` | n/a | 0 |

## Lab boilerplates

Storing mappings and conventions in configuration files rather than inside scripts means that a naming change or updated variable definition requires editing one file rather than every script that references it. The structure below separates task-specific configuration from analysis logic, which is the practical implementation of the interface principle in Rule 8.

```text
config/
├── schema.json             # task-specific variable definitions
├── event_mapping.yaml      # raw event names -> canonical trial_type labels
├── subject_list.tsv        # participants to process
└── model_config.yaml       # analysis-specific options

scripts/
├── build_events.py         # reads event_mapping.yaml
├── preprocess_behavior.py  # reads schema.json and subject_list.tsv
├── qc_report.py            # reads schema.json and subject_list.tsv
├── run_analysis.py         # reads event_mapping.yaml, subject_list.tsv, model_config.yaml
└── generate_report.py      # uses model_config.yaml
```
