---
layout: page
title: ""
---

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">

<div class="challenge-hero">
  <style>
    .challenge-hero { text-align: center; padding: 16px 0 8px; }
    .challenge-hero img {
      display: block;
      width: auto;
      max-width: 100%;
      max-height: 280px;
      height: auto;
      margin: 0 auto;
      object-fit: contain;
    }
    .challenge-hero .visually-hidden {
      position: absolute;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
      white-space: nowrap;
      border: 0;
    }
    @media (max-width: 600px) {
      .challenge-hero { padding: 8px 0 4px; }
      .challenge-hero img { max-height: 160px; }
    }
  </style>
  <img src="img/audio-editing-challenge-logo-hd-4k.png" alt="MMAE — ICASSP 2027 Audio Editing Challenge" width="3840" height="1341" loading="eager" fetchpriority="high">
  <h1 class="visually-hidden">Audio Editing Challenge</h1>
  <h2 class="visually-hidden">ICASSP 2027</h2>
</div>

<!-- News list: newest announcements first. -->
<div id="news" style="max-width: 980px; margin: 18px auto; padding: 12px 16px; border-radius: 8px; background: #fff; box-shadow: 0 1px 2px rgba(0,0,0,0.03);">
  <style>
    #news .header { font-family: 'Inter', sans-serif; font-weight: 600; font-size: 1.05em; margin-bottom: 8px; }
    #news ul { list-style: none; padding: 0; margin: 0; }
    #news li { display: flex; gap: 12px; align-items: baseline; padding: 8px 0; border-bottom: 1px solid rgba(0,0,0,0.04); }
    #news li:last-child { border-bottom: none; }
    #news .date { color: #999; font-size: 0.9em; width: 86px; flex-shrink: 0; }
    #news .item { font-size: 0.98em; }
    #news .item a { color: #0b66ff; text-decoration: none; }
    #news .item a:hover { text-decoration: underline; }
    @media (max-width: 520px) {
      #news li { flex-direction: column; align-items: flex-start; }
      #news .date { width: auto; margin-bottom: 4px; }
    }
  </style>

  <div class="header">News</div>
  <ul>
    <li>
      <div class="date">2026-08-17</div>
      <div class="item">Website goes live!</div>
    </li>
  </ul>
</div>

## Introduction

Imagine editing audio as naturally as editing text: remove audience applause while leaving the speaker and room acoustics untouched; replace a song lyric while preserving the singer's voice and accompaniment; or refine a recording through several dependent rounds of instructions. Recent generative audio models are beginning to make such interactions possible, moving audio production from specialized software pipelines toward an intelligent, natural-language interface.

Existing methods span domain-specific speech, music, and sound editing models, general-purpose systems that unify several editing operations and audio modalities, and planner-guided systems that decompose complex instructions into executable steps [1-13].

Current systems can often complete a simple edit in one domain, yet they remain unreliable when an instruction requires precise timing, multiple operations, mixed speech-music-sound content, multi-step reasoning, or multi-round interaction. Even when the requested change is successful, a model may alter speaker identity, musical structure, background ambience, or overall audio quality. On MMAE, existing systems achieve below 5% Exact Match Rate, revealing a wide gap between producing a plausible result and executing an edit completely and faithfully [14].

## Challenge Goals

The **Audio Editing Challenge at ICASSP 2027** studies how to build general-purpose audio editors that can accurately perceive and understand source audio, reason about potentially complex user instructions, and generate the requested modification while preserving everything that should remain unchanged.

The challenge features two complementary tracks:

1. **Single Model Track:** Build one end-to-end model that directly transforms the input audio according to the instruction. This track studies intrinsic, unified audio editing capability without external models or tools.
2. **Agent Track:** Build an autonomous editing system that may plan, invoke multiple locally deployed models or signal-processing tools, inspect intermediate results, and revise its output. This track studies orchestration, tool use, and self-correction.

<div style="text-align: center; margin: 40px 0;">
  <img src="img/example.png" alt="Representative MMAE audio editing examples" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
  <p style="margin-top: 12px; color: #666; font-size: 14px; font-style: italic;">Representative examples from the MMAE benchmark, illustrating diverse audio modalities, task complexity, editing granularity and operations, and rubric-based evaluation.</p>
</div>

## Timeline

| Event | Date |
|-------|------|
| Registration Opens and Challenge Guidelines Released | September 1, 2026 |
| Challenge Begins | October 1, 2026 |
| Data Released and Leaderboard Opens for Submissions | November 10, 2026 |
| Final Submission Deadline and Leaderboard Freeze | November 25, 2026 |
| Evaluation and Reproducibility Check Completed | December 7, 2026 |
| Final Rankings and Invited Teams Announced | December 8, 2026 |
| Invited Two-Page ICASSP Papers Due | January 7, 2027 |

**Note:** All deadlines are at 11:59 PM on the respective day in U.S. Pacific Time. This tentative timeline is subject to change in accordance with the ICASSP 2027 conference schedule.

## Challenge Tracks

### Track 1: Single Model Track

Participants build a **single, end-to-end audio editing model** that consumes one or more input recordings and a natural-language instruction and directly produces the edited audio. All learned components used to understand and execute the edit must belong to one model, without delegating to separately trained perception models, planners, editors, or external services.

[Learn more about Track 1](track1)

### Track 2: Agent Track

Participants build an **autonomous audio editing agent** that may orchestrate multiple open-source models and signal-processing tools, including ASR, captioning, source separation, acoustic analysis, planning, and iterative editing. An agent may maintain structured memory, inspect intermediate audio, and revise its output.

[Learn more about Track 2](track2)

## Benchmark and Evaluation Protocol

### Benchmark

During the development and leaderboard stages, both tracks use the public **MMAE benchmark**, comprising **2,000 examples** and **17,741 atomic rubrics**. The dataset is available on [Hugging Face](https://huggingface.co/datasets/BoJack/MMAE). The final stage introduces **450 previously unreleased examples** constructed through the same MMAE pipeline and manually annotated and verified. Test inputs and editing instructions will be provided for inference, while the rubrics remain private until the official results are finalized. The complete final set and its rubrics will be released after the competition.

### Submission Format

For each test item, participants submit the edited audio file and a JSONL record that maps the sample ID to its relative audio path:

```json
{"id": "<sample_id>", "audio_path": "audio/<sample_id>.wav"}
```

The audio files and JSONL manifest are packaged together and uploaded to the challenge leaderboard. The two tracks are ranked independently.

### Evaluation Metrics

Each rubric is evaluated three times by a frozen Qwen3-Omni model serving as the judge, with shuffled answer choices and majority voting [17]. The leaderboard reports:

1. **Instruction Following Rate (IFR):** the average score over rubrics that verify whether the requested edits were correctly executed.
2. **Consistency Rate (CR):** the average score over rubrics that verify whether unrelated audio content and quality were preserved.
3. **Exact Match Rate (EMR):** the proportion of samples for which all instruction-following and consistency rubrics are satisfied.

Systems are ranked primarily by **Overall EMR**, with ties broken first by Overall IFR and then by Overall CR.

## Registration and Leaderboard

<!-- Registration form and leaderboard URLs will be inserted after they are confirmed. -->

[Learn more about Leaderboard](leaderboard)

## Paper Submission

The top three teams in each track will be invited to submit a two-page ICASSP 2027 paper and present their work in the Grand Challenge session.

## Contact

For questions about the challenge, please contact
[Zhikang Niu](mailto:zhikangniu@sjtu.edu.cn) or
[Wenming Tu](mailto:tuwenming@sjtu.edu.cn).

## Organizers

<div id="organizers" style="max-width: 980px; margin: 24px auto 60px; padding: 0 16px;">
  <style>
    #organizers .grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 18px;
    }
    @media (min-width: 720px) {
      #organizers .grid {
        grid-template-columns: 1fr 1fr;
      }
    }
    #organizers .organizer {
      display: flex;
      align-items: center;
      gap: 14px;
      background: #fff;
      padding: 12px;
      border-radius: 8px;
      box-shadow: 0 1px 2px rgba(0,0,0,0.04);
    }
    #organizers .organizer img,
    #organizers .organizer .photo-placeholder {
      width: 88px;
      height: 88px;
      object-fit: cover;
      border-radius: 8px;
      flex-shrink: 0;
      background: #f2f2f2;
    }
    #organizers .organizer .meta {
      text-align: left;
    }
    #organizers .organizer .name {
      font-family: 'Inter', sans-serif;
      font-weight: 600;
      font-size: 1.2em;
      margin-bottom: 4px;
    }
    #organizers .organizer .affil {
      color: #666;
      font-size: 0.8em;
      line-height: 1.2;
    }
  </style>

  <div class="grid">
    <div class="organizer">
      <img src="img/organizers/zhikang-niu.jpg" alt="Zhikang Niu">
      <div class="meta">
        <div class="name">
          <a href="https://zhikangniu.github.io/" target="_blank" rel="noopener noreferrer">Zhikang Niu</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
        <div class="affil">Shanghai Innovation Institute</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/wenming-tu.jpg" alt="Wenming Tu">
      <div class="meta">
        <div class="name">
          <a href="https://danjuan-77.github.io/" target="_blank" rel="noopener noreferrer">Wenming Tu</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
        <div class="affil">Beijing Institute for General Artificial Intelligence</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/ziyang.jpg" alt="Ziyang Ma">
      <div class="meta">
        <div class="name">
          <a href="https://ziyang.tech/" target="_blank" rel="noopener noreferrer">Ziyang Ma</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
        <div class="affil">Shanghai Innovation Institute</div>
        <div class="affil">Nanyang Technological University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/ruiyang.jpg" alt="Ruiyang Xu">
      <div class="meta">
        <div class="name">
          <a href="https://xrysamuel.github.io/" target="_blank" rel="noopener noreferrer">Ruiyang Xu</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/hankun-wang.png" alt="Hankun Wang">
      <div class="meta">
        <div class="name">
          <a href="https://scholar.google.com/citations?user=mcQFLgoAAAAJ&amp;hl=en" target="_blank" rel="noopener noreferrer">Hankun Wang</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/bohan-li.jpg" alt="Bohan Li">
      <div class="meta">
        <div class="name">
          <a href="https://scholar.google.com/citations?user=ci5K3f4AAAAJ&amp;hl=en" target="_blank" rel="noopener noreferrer">Bohan Li</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/ruiqi-yan.jpg" alt="Ruiqi Yan">
      <div class="meta">
        <div class="name">
          <a href="https://ruiqi-yan.github.io/" target="_blank" rel="noopener noreferrer">Ruiqi Yan</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/zilong-zheng.jpg" alt="Zilong Zheng">
      <div class="meta">
        <div class="name">
          <a href="https://zilongzheng.github.io/" target="_blank" rel="noopener noreferrer">Zilong Zheng</a>
        </div>
        <div class="affil">Beijing Institute for General Artificial Intelligence</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/chunxiang-jin.jpg" alt="Chunxiang Jin">
      <div class="meta">
        <div class="name">Chunxiang Jin</div>
        <div class="affil">Inclusion AI, Ant Group</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/pengcheng-zhu.jpg" alt="Pengcheng Zhu">
      <div class="meta">
        <div class="name">
          <a href="https://scholar.google.com/citations?hl=zh-CN&amp;user=puGCxRQAAAAJ&amp;view_op=list_works&amp;sortby=pubdate" target="_blank" rel="noopener noreferrer">Pengcheng Zhu</a>
        </div>
        <div class="affil">Ant Group</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/hung-yi-lee.jpg" alt="Hung-yi Lee">
      <div class="meta">
        <div class="name">
          <a href="https://speech.ee.ntu.edu.tw/~hylee/index.php" target="_blank" rel="noopener noreferrer">Hung-yi Lee</a>
        </div>
        <div class="affil">National Taiwan University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/jinyu.jpeg" alt="Jinyu Li">
      <div class="meta">
        <div class="name">
          <a href="https://www.microsoft.com/en-us/research/people/jinyli/" target="_blank" rel="noopener noreferrer">Jinyu Li</a>
        </div>
        <div class="affil">Microsoft Corporation</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/carlos.jpeg" alt="Carlos Busso">
      <div class="meta">
        <div class="name">
          <a href="https://carlosbusso.com/" target="_blank" rel="noopener noreferrer">Carlos Busso</a>
        </div>
        <div class="affil">Carnegie Mellon University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/kai.jpg" alt="Kai Yu">
      <div class="meta">
        <div class="name">
          <a href="https://x-lance.sjtu.edu.cn/~kaiyu/" target="_blank" rel="noopener noreferrer">Kai Yu</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/engsiong.jpeg" alt="Eng Siong Chng">
      <div class="meta">
        <div class="name">
          <a href="https://aseschng.github.io/intro1.html" target="_blank" rel="noopener noreferrer">Eng Siong Chng</a>
        </div>
        <div class="affil">Nanyang Technological University</div>
      </div>
    </div>
    <div class="organizer">
      <img src="img/organizers/xie.jpg" alt="Xie Chen">
      <div class="meta">
        <div class="name">
          <a href="https://chenxie95.github.io/en" target="_blank" rel="noopener noreferrer">Xie Chen</a>
        </div>
        <div class="affil">Shanghai Jiao Tong University</div>
        <div class="affil">Shanghai Innovation Institute</div>
      </div>
    </div>
  </div>
</div>

<div id="references" style="max-width: 980px; margin: 12px auto 40px; padding: 16px; border-radius: 8px; background:#fff; box-shadow: 0 1px 2px rgba(0,0,0,0.03);">
  <style>
    #references h2 { font-family: 'Inter', sans-serif; font-size: 1.1em; margin: 0 0 10px; }
    #references ol { margin: 0; padding-left: 20px; color: #333; }
    #references li { margin: 8px 0; font-size: 0.95em; line-height: 1.4; }
    #references a { color: #0b66ff; text-decoration: none; }
    #references a:hover { text-decoration: underline; }
  </style>

  <h2>References</h2>
  <ol>
    <li>Peng, Puyuan, et al. "VoiceCraft: Zero-Shot Speech Editing and Text-to-Speech in the Wild." Proc. ACL (2024).</li>
    <li>Zhang, Yixiao, et al. "MusicMagus: Zero-Shot Text-to-Music Editing via Diffusion Models." arXiv:2402.06178 (2024).</li>
    <li>Wang, Yuancheng, et al. "AUDIT: Audio Editing by Following Instructions with Latent Diffusion Models." Proc. NeurIPS (2023).</li>
    <li>Tao, Ye, et al. "MMEdit: A Unified Framework for Multi-Type Audio Editing via Audio Language Model." arXiv:2512.20339 (2025).</li>
    <li>Tian, Zeyue, et al. "Audio-Omni: Extending Multi-modal Understanding to Versatile Audio Generation and Editing." Proc. SIGGRAPH (2026).</li>
    <li>Lan, Zitong, et al. "Guiding Audio Editing with Audio Language Model." Proc. NeurIPS (2025).</li>
    <li>Qiang, Chunyu, et al. "UniSonate: A Unified Model for Speech, Music, and Sound Effect Generation with Text Instructions." Proc. ACL (2026).</li>
    <li>Gong, Junmin, et al. "ACE-Step 1.5: Pushing the Boundaries of Open-Source Music Generation." arXiv:2602.00744 (2026).</li>
    <li>Li, Zhaoqing, et al. "UNISON: A Unified Sound Generation and Editing Framework via Deep LLM Fusion." arXiv:2605.31530 (2026).</li>
    <li>Chen, Junyang, et al. "CosyEdit: Unlocking End-to-End Speech Editing Capability from Zero-Shot Text-to-Speech Models." arXiv:2601.05329 (2026).</li>
    <li>Zhang, Dong, et al. "MiMo-Audio: Audio Language Models are Few-Shot Learners." arXiv:2512.23808 (2025).</li>
    <li>Chen, William, et al. "AudioChat: Unified Audio Storytelling, Editing, and Understanding with Transfusion Forcing." arXiv:2602.17097 (2026).</li>
    <li>Wang, Hankun, et al. "dots.tts.edit: Precisely Controlled Speech Editing with a Continuous Autoregressive Model." arXiv:2608.02673 (2026).</li>
    <li>Ma, Ziyang, et al. "MMAE: A Massive Multitask Audio Editing Benchmark." arXiv:2606.07229 (2026).</li>
    <li>Yan, Chao, et al. "Step-Audio-EditX Technical Report." arXiv:2511.03601 (2025).</li>
    <li>Yan, Canxiang, et al. "Ming-UniAudio: Speech LLM for Joint Understanding, Generation and Editing with Unified Representation." arXiv:2511.05516 (2025).</li>
    <li>Xu, Jin, et al. "Qwen3-Omni Technical Report." arXiv:2509.17765 (2025).</li>
  </ol>
</div>

---

<div style="text-align: center; margin-top: 60px; color: #888;">
  <p>Follow us on GitHub for updates:
    <a href="https://github.com/Audio-Editing-Challenge" target="_blank" rel="noopener noreferrer">@Audio-Editing-Challenge</a>
  </p>
</div>
