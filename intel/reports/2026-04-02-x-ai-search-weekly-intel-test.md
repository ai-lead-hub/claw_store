# AI Search Weekly Intel — Mar 29 Round Up

**Seed Post:** https://x.com/aisearchio/status/2038101482160181265 (Pinned, Mar 29, 2026)  
**Items researched:** 12 named  
**Status:** Test Run — partial sources pending

---

## Executive Summary

A packed week ending March 29th brought a broad cross-section of AI releases: a new open-source video+audio model hitting SOTA, a landmark coding model closing the gap on Claude Opus, a landmark AGI benchmark where frontier AI scores below 1% vs humans at 100%, and a string of tools across audio, transcription, and dev infrastructure. The most significant theme: open-source models are compressing the gap with frontier proprietary models across modalities — video, coding, and audio all saw notable open releases this week.

---

## Grouped Findings

### 🎬 Video Generation

**DaVinci MagiHuman**
- Type: Open-source model
- Category: Text → Video + Audio (joint generation)
- Summary: 15B parameter single-stream Transformer that jointly generates video AND audio from text in one pass — no separate audio pipeline. Multilingual (6 languages). 80% win rate vs Ovi 1.1, 60.9% vs LTX 2.3 in 2,000 human evals. 5-sec 256p clip in 2 seconds on a single H100.
- Why it matters: First open model to treat video+audio as a unified generation problem rather than bolted-together pipelines. The speed and open release make it highly accessible.
- Links: [davincimagihuman.com](https://davincimagihuman.com/) · [arXiv:2603.21986](https://arxiv.org/abs/2603.21986)

**Matrix Game 3.0**
- Status: ⏳ Under review — source not yet confirmed

### 🎧 Audio Generation

**PrismAudio**
- Type: Open-source research model
- Category: Video → Audio (V2A), audio generation
- Summary: Alibaba Tongyi Lab's V2A framework using Decomposed Chain-of-Thought reasoning across four perceptual dimensions: semantic, temporal, aesthetic, spatial. Each dimension has its own CoT module + RL reward function. Fast-GRPO enables practical training. Accepted to ICLR 2026. State-of-the-art on VGGSound and new AudioCanvas benchmark.
- Why it matters: Solves the core V2A tradeoff problem — you no longer have to choose between sync and quality. The multi-dimensional CoT approach is a architectural pattern other V2A work will build on.
- Links: [prismaudio.github.io](https://prismaudio.github.io/) · [WaveSpeed AI explainer](https://wavespeed.ai/blog/posts/prismaudio-video-to-audio-ai-sound-generation-2026/)

### 🧠 Reasoning & Research Models

**GLM 5.1**
- Type: Open-source frontier model
- Category: Coding, general reasoning
- Summary: Zhipu AI's (now Z.ai) latest model released March 27, 2026. Scores 45.3 on coding eval vs Claude Opus 4.6's 47.9 — reaching 94.6% of Opus performance. Trained entirely on Huawei chips. Open weights. 202K context window.
- Why it matters: The open-source coding gap vs frontier proprietary models is now within 2-3 points on internal evals. GLM-5.1 is the most credible open challenger to Claude Opus for coding tasks to date.
- Links: [glm5.ai](https://glm5.ai/) · [arXiv:2602.15763](https://arxiv.org/abs/2602.15763) · [Z.ai Coding Plan](https://help.apiyi.com/en/glm-5-1-coding-plan-claude-opus-alternative-api-guide-en.html)

**ARC AGI 3**
- Type: Benchmark / competition
- Category: Agentic reasoning evaluation
- Summary: Released March 24, 2026 by ARC Prize Foundation (Francois Chollet). Tests interactive, experience-driven reasoning — agents must explore novel environments, infer goals, build world models, and adapt without language instructions. Frontier AI models score below 1%; humans score 100%. $2M+ prize pool.
- Why it matters: Makes the AGI gap concrete and measurable. Frontier models' near-0% score vs human 100% is a stark reminder how far agentic generalization still has to go.
- Links: [arcprize.org/arc-agi/3](https://arcprize.org/arc-agi/3) · [arXiv:2603.24621](https://arxiv.org/abs/2603.24621)

**Gemini Realtime Voice**
- Type: Product feature
- Category: Voice interaction
- Status: ⏳ Under review — Google DeepMind realtime voice capability referenced in the roundup. Full details pending source lookup.

### 🎙️ Transcription & Speech

**Cohere Transcribe**
- Type: Enterprise product
- Category: Speech-to-text, transcription API
- Summary: Cohere's production speech recognition API. 14 languages, optimized for enterprise noise/accents. Open-weights option for local/private deployment. Lowest WER available. Suitable for RAG pipelines, meeting intelligence, voice automation.
- Why it matters: Strong alternative to AssemblyAI and Whisper for enterprise workflows where accuracy under real-world conditions and data privacy are both critical.
- Links: [cohere.com/transcribe](https://cohere.com/transcribe)

### 🔧 Dev & Infrastructure Tools

**Real Restorer**
- Status: ⏳ Under review

**Tribe v2**
- Status: ⏳ Under review

**LumosX**
- Status: ⏳ Under review

**TurboQuant**
- Status: ⏳ Under review

**RealMaster**
- Status: ⏳ Under review

---

## What Matters Most

1. **DaVinci MagiHuman** is the standout open-source release — unified video+audio in a single model at SOTA quality with a 2-second inference time is a meaningful leap.
2. **GLM 5.1** closing to within 2.6 coding points of Claude Opus is a landmark for open-source coding capability.
3. **PrismAudio** represents a new architectural pattern (decomposed CoT + multi-dimensional RL) for video-to-audio that will be widely replicated.
4. **ARC AGI 3** reminds us that for all the progress, frontier agentic generalization remains near-zero — a healthy check on the hype cycle.

---

## Watch List

- ARC Prize 2026 results (top submissions could reveal breakthroughs)
- GLM-5.1 open-weight releases beyond coding plan
- DaVinci MagiHuman community fine-tunes and extensions
- Alibaba Tongyi Lab's next model family

---

## Sources Checked

- davincimagihuman.com
- prismaudio.github.io
- wavespeed.ai
- arcprize.org
- arxiv.org/abs/2602.15763
- arxiv.org/abs/2603.21986
- arxiv.org/abs/2603.24621
- cohere.com/transcribe
- x.com/aisearchio
- glm5.ai
- help.apiyi.com
- buildfastwithai.com
