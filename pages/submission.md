---
layout: page
title: Submission Guide
permalink: /submission/
---

Submit your inference results in three steps: **prepare your files → upload with the SDK → start evaluation on the website**.

An **Upload** stores your result files. A **Submission** starts an evaluation of a selected Upload. **Uploading alone does not start evaluation.**

Use the evaluation URL and track-specific Secret Key provided privately by the organizers. If you have not received them, contact [Zhikang Niu](mailto:zhikangniu@sjtu.edu.cn).

## 1. Prepare your inference results

For your chosen track, generate one edited audio file for each of the **500 challenge test samples**. Place the audio files and a UTF-8 `submission.jsonl` in a results directory:

```text
my_submission/
├── submission.jsonl
└── audio/
    ├── sample-001.wav
    ├── sample-002.wav
    └── ...
```

Each nonempty JSONL line must contain exactly these two string fields:

```json
{"id": "<official sample ID>", "audio_path": "audio/sample-001.wav"}
```

Replace the placeholder with an official ID from your track. Include all 500 IDs exactly once, with a distinct audio path for each sample. Paths are relative to `my_submission/` and use `/`; use regular files, without symlinks or paths outside that directory.

| Requirement | Value |
| --- | --- |
| Audio format | WAV, 16 kHz, mono, 16-bit integer PCM |
| Audio duration | Greater than 0 and at most 300 seconds per file |
| Total archive size | At most 2 GiB, including tar headers and padding |

The SDK fetches the current upload requirements from the system and validates your results before packaging. It does not convert audio; prepare the required format before uploading.

## 2. Upload with the SDK

Install the [Audio Editing Challenge SDK](https://github.com/Audio-Editing-Challenge/Audio-Editing-Challenge-SDK) with Python 3.11 or later:

```bash
git clone https://github.com/Audio-Editing-Challenge/Audio-Editing-Challenge-SDK.git
cd Audio-Editing-Challenge-SDK
pip install -e .
```

Run the upload example from the SDK directory, replacing `/path/to/my_submission` with your results directory:

```bash
python examples/upload.py /path/to/my_submission \
  --competition aec_single_model \
  --archive ./result.tar \
  --name my-run-v1
```

Choose the competition ID that matches your results and Secret Key:

| Track | `--competition` |
| --- | --- |
| Track 1: Single Model | `aec_single_model` |
| Track 2: Agent | `aec_agent` |

The script prompts for your evaluation URL and Secret Key with hidden input. Enter the platform base URL supplied by the organizers, without an `/upload` suffix.

The SDK validates the files, creates an uncompressed tar archive, uploads it, and prints a **Ready Upload ID**. Keep this ID to identify the files on the website. See the [SDK README](https://github.com/Audio-Editing-Challenge/Audio-Editing-Challenge-SDK#readme) for Python usage and automation.

## 3. Start evaluation and view results

1. Open the evaluation website provided by the organizers and select the same competition used for the SDK upload.
2. Enter the same **Secret Key** and click **Confirm**. This loads your Ready Uploads, Submissions, and remaining daily quotas. If the page was already open when you uploaded, click **Refresh**.
3. Under **Submit an Upload**, select your **Ready Upload**, then click **Start evaluation**. This creates a Submission with its own ID.
4. Follow its status under **Track your Submission**. Evaluation runs asynchronously; you may close the page and return later using the same competition and Secret Key. Refresh to check for updates.

A `queued` Submission is waiting to run; `evaluating` means evaluation is in progress. A `succeeded` Submission shows its scores. For a `failed` Submission, contact the organizers with its Submission ID and the displayed error message.

## Daily limits and troubleshooting

**Each Secret Key allows 1 successful upload and 1 evaluation submission per day for its track.** Quotas reset at **00:00 UTC**. Confirm your Secret Key on the evaluation website to see your remaining allowances. Failed evaluation submissions count toward the daily limit.

- **Validation fails:** correct the reported IDs, paths, audio format, duration, or archive size before retrying.
- **An upload request times out or loses its connection:** check Ready Uploads on the website before uploading again; the system may already have accepted the files.
- **Your Upload is missing:** confirm that the website uses the same competition and Secret Key as the SDK, then refresh.
- **Start evaluation is unavailable:** check that your Secret Key is confirmed, a Ready Upload is selected, the submission window is open, and you have remaining submission quota.

Keep the evaluation URL and your Secret Key private; do not include them in public code, screenshots, logs, or issues. Do not share them with non-participants or other contestants. Do not abuse the evaluation system or exploit its bugs; report issues privately to the organizers. Violations will result in disqualification.
