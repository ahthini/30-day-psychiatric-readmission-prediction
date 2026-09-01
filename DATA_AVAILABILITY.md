# Data Availability

This project uses MIMIC-IV v3.1, a credentialed electronic health record dataset available through PhysioNet. The raw data are not included in this repository and must not be redistributed.

To reproduce the analysis, obtain access through the official MIMIC-IV credentialing process and place the local data folder at:

```text
mimic-iv-3.1/
  hosp/
  icu/
```

Generated admission-level datasets, hourly sequence datasets, processed matrices, model files and patient-level outputs are also excluded from the repository because they may contain derived clinical information and can be regenerated from the notebooks by authorised users with local data access.

The repository therefore contains code, documentation, dissertation source files and non-sensitive report assets only.
