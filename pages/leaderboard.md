---
layout: page
title: Leaderboard
permalink: /leaderboard/
---

The leaderboard will open for submissions on **November 10, 2026**, when the organizers will release the challenge test set and the submission software development kit (SDK). The submission link will be announced here.

## Benchmark and Evaluation Protocol

### Benchmark

**Before November 10, 2026**, participants may use the publicly available **MMAE test set**, comprising **2,000 examples** and **17,741 atomic rubrics** and available on [Hugging Face](https://huggingface.co/datasets/BoJack/MMAE), to develop and evaluate their models and agent systems.

**On November 10, 2026**, the organizers will release the **previously unreleased challenge test set** for leaderboard submissions. The Single Model Track and the Agent Track will each use **500 previously unreleased test examples**. The two tracks will be ranked independently. These examples are constructed through the same MMAE pipeline and manually annotated and verified. Test inputs and editing instructions will be provided for inference; evaluation rubrics will remain private until the official results are finalized.

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

## Team Membership

Before submissions open on **November 10, 2026**, the organizers will send a form to collect and confirm each team's final member list, **including supervisors and team leaders**. Except in special circumstances, **changes to team membership will not be permitted once submissions open**. **Each person may participate in both tracks, but may be listed on only one team per track.**

## Competition Timeline

| Event | Date |
|-------|------|
| Registration Opens and Challenge Guidelines Released | September 1, 2026 |
| Challenge Begins | October 1, 2026 |
| Registration Deadline (Extended) | October 8, 2026 |
| Challenge Test Set and Submission SDK Released; Leaderboard Opens | November 10, 2026 |
| Final Submission Deadline and Leaderboard Freeze | November 25, 2026 |
| Evaluation and Reproducibility Check Completed | December 7, 2026 |
| Final Rankings and Invited Teams Announced | December 8, 2026 |
| Invited Two-Page ICASSP Papers Due | January 7, 2027 |

**Note:** Registration and submission deadlines are at 11:59 PM on the respective day in U.S. Pacific Time. For the Agent Track, model versions and weights must have been publicly released **before November 1, 2026**. This tentative timeline is subject to change in accordance with the ICASSP 2027 conference schedule.
