# DataLoader (Minimal Design)

## Scope

This module provides a minimal dataloader for STT training.

---

## Data Source

- S3-compatible storage (Cloudflare R2)
- Access via:
  - endpoint_url
  - bucket
  - prefix

- Credentials are NOT handled here (use environment / SDK)

---

## Output Contract

The dataloader MUST return standardized sample objects:

```python
{
    "sample_id": str,
    "audio_uri": str,
    "transcript": str,
    "duration_sec": float | None,
    "speaker_id": str | None,
    "metadata": dict
}
```

Rules:

* sample_id, audio_uri, transcript are required
* metadata must always exist (default {})

---

Responsibilities

The dataloader:

* reads dataset metadata from S3
* constructs standardized samples
* provides iterable / indexable dataset

---

Non-Responsibilities

The dataloader MUST NOT:

* decode audio
* load waveform
* resample audio
* tokenize text
* generate model inputs
* handle training logic

---

S3 Structure

To be decided here
