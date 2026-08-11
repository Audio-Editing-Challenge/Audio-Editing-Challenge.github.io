---
layout: page
title: Leaderboard
permalink: /leaderboard/
---

<!-- The registration form and leaderboard URLs will be added after they are confirmed. -->

## Benchmark and Evaluation Protocol

### Benchmark

During the development and leaderboard stages, both tracks use the public **MMAE benchmark**, comprising **2,000 examples** and **17,741 atomic rubrics** and available on [Hugging Face](https://huggingface.co/datasets/BoJack/MMAE). The final stage introduces **450 previously unreleased examples** constructed through the same MMAE pipeline and manually annotated and verified.

### Submission Format

For each test item, participants submit the edited audio file and a JSONL record that maps the sample ID to its relative audio path:

```json
{"id": "<sample_id>", "audio_path": "audio/<sample_id>.wav"}
```

The audio files and JSONL manifest are packaged together and uploaded to the challenge leaderboard. The two tracks are ranked independently.

### Evaluation Metrics

1. **Instruction Following Rate (IFR):** the average score over rubrics that verify whether the requested edits were correctly executed.
2. **Consistency Rate (CR):** the average score over rubrics that verify whether unrelated audio content and quality were preserved.
3. **Exact Match Rate (EMR):** the proportion of samples for which all instruction-following and consistency rubrics are satisfied.

Systems are ranked primarily by **Overall EMR**, with ties broken first by Overall IFR and then by Overall CR.

## Competition Timeline

| Event | Date |
|-------|------|
| Participant Registration Opens | September 1, 2026 |
| Challenge Announcement, Detailed Rules, and Data Release | October 1, 2026 |
| Leaderboard Opens for Submissions | November 1, 2026 |
| Leaderboard Submission Deadline | December 1, 2026 |
| Submission Verification, Final Rankings, and Winner Announcement | December 8, 2026 |
| Invited Two-Page ICASSP Paper Submission Deadline | January 7, 2027 |

After December 1, 2026, the leaderboard will remain open, but later submissions will not be considered for the official challenge rankings. The timeline is tentative and subject to change in accordance with the ICASSP 2027 conference schedule.
