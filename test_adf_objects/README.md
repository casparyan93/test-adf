# Test ADF Objects

Self‑contained minimal Azure Data Factory artifact set for deployment script testing. Copy the entire `test_adf_objects` folder contents into a clean repo root to simulate a new ADF codebase.

## Contents

- factory/Factory.json – Factory definition placeholder
- linkedService/LS_RawBlob.json – Sample Azure Blob Storage linked service (non‑secret placeholder)
- dataset/DS_Raw_SampleCsv.json – Source CSV dataset
- dataset/DS_Processed_SampleCsv.json – Sink CSV dataset
- pipeline/PL_Copy_SampleCsv.json – Simple Copy pipeline (source -> sink)
- dataflow/DF_PassThrough_Sample.json – Pass‑through mapping data flow (optional reference object)
- trigger/TR_Hourly.json – Hourly schedule trigger (disabled by default)
- integrationRuntime/IR_Auto.json – Managed (AutoResolve) IR sample
- publish_config.json – Minimal publish config placeholders

## Notes / Placeholders

- Replace `youraccount` in the linked service with a real storage account or parameterize via Key Vault/ARM before real deployment.
- No secrets are included; connection string is intentionally incomplete.
- All names kept short and unique to reduce collision risk.
- Artifacts use simplest viable schemas to exercise deployment (create/update/validate) paths.

## Typical Deployment Script Expectations

Your script should:

1. Enumerate artifact subfolders (dataset, linkedService, pipeline, dataflow, trigger, integrationRuntime, factory).
2. Deploy each JSON via ARM/REST in dependency order (linkedService -> dataset -> dataflow -> pipeline -> trigger) or rely on ADF publish method if scripted.
3. Skip enabling triggers until after pipelines are published (trigger property `runtimeState` intentionally omitted; provide `"properties": {"type": "ScheduleTrigger", ...}` only).

## Parameterization (Optional Extension)

You can introduce parameter files (e.g. `arm-template-parameters-definition.json`) later to map environment specifics. This starter set keeps focus on structural deployment testing.

---
Generated for deployment script testing.
