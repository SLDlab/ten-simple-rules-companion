# Rule 9: Account for the data behind each analysis

The contents below represent the minimum that a quality check (QC) report should capture for a workflow run to be auditable. Reports do not need to be formatted documents; a structured text file or CSV that contains these fields is sufficient, provided it is stored in the `reports/` folder and committed alongside the outputs it describes.

## Recommended QC report contents

Each major run should report:

- Input dataset or participant list
- Preprocessing steps applied
- Parameters or thresholds used
- Exclusion criteria
- Excluded participants, runs, files, or trials
- QC warnings
- Summary plots or tables
- Output file locations
- Date, software version, and command used

## Example behavioral QC summary section for missed responses

The example below is for reporting missed responses on a task where type1 and type2 trials require different handling.

```text
QC category: missed responses

Task: Observational Learning
Rule: Count missed responses only on type1 trials.
Excluded from missed-response count: type2 trials.

Participant: sub-000
Run: run-01
Expected responses: 40
Missed responses: 2
Missed trial indices: 17 | 33
Flag: no

Participant: sub-005
Run: run-02
Expected responses: 40
Missed responses: 10
Missed trial indices: 2 | 5 | 9 | 11 | 17 | 21 | 24 | 30 | 33 | 39
Flag: yes                            # Flagging rule: missed response rate > 20%
```

## Example neuroimaging manual QC log

Tools such as fMRIPrep usually generate their own HTML report per participant, which covers motion statistics, registration quality, and preprocessing outputs automatically. The lab must then produce its own review decision based on those outputs. Below is a short example of a review log that records its decision across participants, based on specific criteria such as the number of volumes with motion defined as high.

`reports/qc_reports/fmriprep_review_log.tsv`

| subject | run | mean_fd | high_motion_vols | reviewed_by | decision | notes |
|---|---|---:|---:|---|---|---|
| sub-001 | task1_run-01 | 0.18 | 6 | VG | include | |
| sub-002 | task1_run-01 | 0.83 | 31 | VG | exclude | exceeds lab FD threshold (0.5mm) |
| sub-002 | task1_run-02 | 0.41 | 12 | VG | include | borderline; retained after visual check |
| sub-005 | task1_run-01 | 0.29 | 9 | VG | include | |
