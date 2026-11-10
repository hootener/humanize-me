---
id: E0007
type: evidence
title: "State of the art for reproducing a specific person's writing voice"
description: "A literature survey of exemplars, fine-tuning, authorship-verification metrics, activation steering and critique loops, with the measured numbers and what each needs; the published failure modes match E0006's exactly, and no automated metric correlates well with an author's own verdict."
timestamp: "2026-11-10"
tags: [voice, profile, verification, research, findings, metrics]
status: active
---

Research done 2026-11-10 against the question: what beats a hand-written
distilled style profile at making a model write like one named person, and what
can measure whether it worked.

The short version is that the literature has already measured our failure.
[E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md) found that a
profile can pass every countable marker and still read as an impression. Two
independent 2026 preprints find the same thing with denominators attached: a
distilled profile is the *best* of the inference-time methods on
description-shaped metrics and on function-word stylometry, and is **not** the
best on authorship-verification metrics, and none of the methods clear the floor
set by two different humans writing about the same thing.

Equally important and less comfortable: the best-validated automated metric in
this area correlates with writers' own judgments of "does this sound like me" at
**r = 0.244** (n = 81). There is no metric here that would have predicted the
operator's rejection. That bounds what any checker we build can promise.

A note on provenance. Everything below was read at its primary source — arXiv
abstract or full text, ACL Anthology, model card, or official vendor
documentation. Several of the most on-point papers are 2026 arXiv preprints with
no venue I could confirm, and two of them share a single independent author;
those are flagged where they are load-bearing. Three PDF extractions returned
unusable or implausible text, and the numbers they would have supplied are
listed in *What I could not verify* rather than reported.

# Why the imitation fails in the first place

This belongs first because it reframes the other sections. The failure is not
that the model ignores the profile. The failure is that it obeys the profile
*inside its own style space*.

**The generated text is author-discriminable and still not author-like.**
*Theory-Grounded Evaluation Exposes the Authorship Gap in LLM Personalization*
(arXiv [2604.26460](https://arxiv.org/abs/2604.26460), Sawant, v1 2026-04-29,
v2 2026-08-14) and its companion *PersonalBench*
([2608.19746](https://arxiv.org/html/2608.19746v1), same author, 2026-08-20)
measure 50 authors and 1,000 generations from the Blog Authorship Corpus
(104K training posts, 26K test posts, mean post length 207 words), generating
with Qwen3-32B and validating on GLM-4-32B. Within the generated text, LUAR
tells the 50 target authors apart at **AUC 0.918**. Comparing generated text to
the real authors' text, it manages **AUC 0.632**. The model does change its
style per author; the change lands somewhere else.

**And the language is explicit about where.** *Catch Me If You Can? Not Yet*
(arXiv [2509.14543](https://arxiv.org/html/2509.14543v1), Wang, Tripto, Park,
Li & Zhou, 2025-09-18; also Findings of EMNLP 2025) tests 400+ real authors
with 50–150 samples each across Enron email, Blog, CCAT50 news and Reddit, with
GPT-4o, GPT-4o-mini, Gemini-2.0-Flash, Gemma-3-27B, DeepSeek-V3 and
Llama-4-Maverick, 40,000+ generations per model. Their diagnosis of the failing
domains is that models "default to an average, generic tone". Five-shot
authorship-verification accuracy (higher is better imitation; the authors state
"we assume that LLM-generated samples and the corresponding test set samples are
from the same authors, so the accuracy is the higher the better"):

| domain | 5-shot AV accuracy | top-5 attribution |
|---|---|---|
| CCAT50 (news) | 95–97% | 86–93% |
| Enron (email) | 95–97% | 56–62% |
| Reddit (forum) | 50–66% | 27–36% |
| Blog | 16–21% | 39–44% |

Against a human-text baseline of 87–91%. The structured, conventional registers
work; the personal ones collapse. GPTZero identified the generations as human
"always below 55% and often less than 20%". **Our register — published blog
posts — is the one that collapses.**

**There is a measured mechanism for the flattening.** *Verbalized Sampling*
(arXiv [2510.01171](https://arxiv.org/html/2510.01171v4), Zhang, Yu, Chong,
Sicilia, Tomz, Manning & Shi, v4 dated 2026-07-15) attributes mode collapse to
typicality bias in preference data rather than to the RL algorithm: annotators
prefer text with higher base-model log-probability beyond task correctness. They
decompose reward with a Bradley-Terry model over 6,874 correctness-matched
response pairs from HelpSteer and report a typicality coefficient of
**α̂ = 0.57 ± 0.07 and 0.65 ± 0.07, both p < 10⁻¹⁴**. Earlier and more
conservatively, Kirk et al., *Understanding the Effects of RLHF on LLM
Generalisation and Diversity* (arXiv
[2310.06452](https://arxiv.org/abs/2310.06452), ICLR 2024) report that "RLHF
significantly reduces output diversity compared to SFT across a variety of
measures" over two base models on summarisation and instruction following. The
abstract states no magnitude and I did not extract one.

So the attractor is not a bug in our profile. It is in the weights, it was put
there by the preference data, and prompting fights it rather than removing it.

# 1. In-context exemplars versus a distilled description

**Head-to-head, at our scale, exemplars edge out the profile on the authorship
metric and lose to it on every description-shaped metric.** This is the Sawant
result and it is worth reading carefully, because it is our
[E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md) in table
form. Four inference-time methods, same 50 authors and 1,000 generations
described above; few-shot used **5 author samples with no explicit
instruction**; "profile extraction" is an abstract style description, i.e. our
method; "contrastive" adds quantitative style signals, i.e. our markers:

| method | LUAR similarity | LLM-judge trait match | function-word stylometry |
|---|---|---|---|
| non-personalized | 0.484 ± .019 | 0.384 ± .058 | 0.741 ± .011 |
| few-shot (5 samples) | **0.508 ± .020** | 0.433 ± .061 | 0.749 ± .011 |
| profile extraction | 0.502 ± .019 | **0.542 ± .060** | **0.761 ± .010** |
| contrastive w/ features | 0.494 ± .020 | 0.447 ± .059 | 0.752 ± .011 |

Human ceiling (same author, held-out text) **0.756**; cross-author floor (two
different authors) **0.626**. Every method scores below the *floor*. And the
three metrics have **near-zero pairwise correlation, |r| < 0.07** — the authors'
words: "they measure different constructs".

Read the profile row. It wins the LLM judge and it wins the stylometry, by
margins outside the error bars, and it does not win the authorship metric. That
is a document that passes 8 of 8 markers and gets rejected by its author.

Caveats, stated because this paper carries a lot of weight here: single
independent author, two overlapping preprints, no venue I could confirm, one
corpus, English blogs only, 32B-scale models only, and the few-shot/profile
difference on LUAR (0.508 vs 0.502) is inside the reported standard errors. The
*ranking* is not established. The *absence of a profile advantage on the
authorship metric* is.

**Raw history beats a generated profile on surface fidelity, and the authors say
why.** *Self-supervised User Profile Generation for Personalization* (arXiv
[2606.05336](https://arxiv.org/html/2606.05336), Ju, Qiu, Zhao & Shah,
2026-06-03), with a Qwen3-4B-Instruct LoRA backbone on the LaMP generation
tasks:

| task | metric | raw history | BUMP (profile) | BUMP+ |
|---|---|---|---|---|
| LaMP-4 (news headline) | ROUGE-1 | **0.210** | 0.197 | 0.199 |
| LaMP-5 (scholarly title) | ROUGE-1 | **0.498** | 0.490 | 0.494 |
| LaMP-7 (tweet paraphrase) | ROUGE-1 | **0.542** | 0.530 | 0.536 |

Their explanation is the useful part: "ROUGE rewards n-gram surface overlap with
the user's prior outputs, which raw history preserves verbatim, while any
natural-language profile — ours or otherwise — abstracts away exactly that
idiolect." ROUGE is a poor proxy for voice, and this is a paper proposing
profiles reporting that its own profiles lose; both facts cut the same way.

**In-context learning is the strongest thing anyone has got working from ~500
words.** *Low-Resource Authorship Style Transfer: Can Non-Famous Authors Be
Imitated?* (arXiv [2212.08986](https://arxiv.org/html/2212.08986)v3, Patel,
Andrews & Callison-Burch, 2024-11-04) deliberately restricts to **16 posts,
≈500 words** per target author, against prior work that used over 100,000 words
for famous authors. Their in-context method Styll scores a joint metric of
0.29 (GPT-3) / 0.40 (BLOOM) on the Single split and 0.30 / 0.36 on Diverse,
against 0.25 / 0.19 for combined hand-written linguistic rules and 0.00 / 0.04
for STRAP (fine-tuned GPT-2). Their own verdict: "current approaches do not yet
achieve mastery of this challenging task." We have eighteen times their corpus.

**Two findings that constrain how we'd use exemplars, and both are negative.**

- **More exemplars barely help.** [2509.14543](https://arxiv.org/html/2509.14543v1)
  sweeps 2, 4, 6, 8, 10: "including more writing examples in the prompt affects
  the four metrics very little", with "limited gains in stylistic alignment".
  Five is as good as ten. Budget accordingly.
- **Topic-similar retrieval makes it worse.** Same paper: "Content-based
  exemplar selection (+Sim ctrl) surprisingly reduces attribution performance,
  especially in Enron, Reddit, and Blog" — **81.28% AV accuracy against a
  95.44% random-selection baseline on Enron**. Their reading is that narrowing
  to a topic cluster strips stylistic range. Length-aligned selection gave
  "modest gains in attribution" but lowered style-model accuracy.

So the retrieval idea in the brief — nearest corpus passages at generation time
— has a measured negative result against it *when nearness means topical
nearness*. Nearness by **text population** (headings retrieved for headings,
instructional prose for instructional prose) is a different proposal, is what
[D0021](../decisions/D0021-a-profile-is-derived-per-text-population-not.md)
already asks for, and is exactly what would have caught
[E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md)'s heading
failure. I found no paper that tests it; it is unmeasured, not refuted.

**A contrary data point on exemplars.** *Predicting Steering Vectors and Adapter
Weights for Few-Shot Author-Style Transfer* (arXiv
[2610.03163](https://arxiv.org/html/2610.03163), Popp, Liu, Sinhamahapatra &
Niehues, 2026-10-02) finds three-exemplar prompting **worse than zero-shot** on
style accuracy over 203 seen authors: 28.1% versus 31.0%, with quality
preference also dropping (91.5% vs 97.9%). Their explanation: instruction
following pulls the output toward a generic register. Three scientific-paper
abstracts is a thin and unusual exemplar budget, and this is a single preprint,
but it means exemplars-beat-descriptions is not a safe prior. It has to be
measured on the operator's own documents.

**Retrieval plus summary, rather than either.** *Integrating Summarization and
Retrieval for Enhanced Personalization via Large Language Models* (arXiv
[2310.20081](https://ar5iv.labs.arxiv.org/html/2310.20081), Richardson et al.)
reports that an offline LLM-generated summary plus **one** retrieved sample
matched or exceeded a four-sample retrieval baseline on LaMP tasks 3–7 — 75%
fewer retrieved samples for equal or better scores; on task 1, 0.743 accuracy
against 0.709 at k=4; on task 2, 0.814 F1 against 0.574. The original LaMP
benchmark (arXiv [2304.11406](https://arxiv.org/abs/2304.11406), Salemi,
Mysore, Bendersky & Zamani) reports retrieval augmentation giving "a relative
average improvement of 12.2%" zero-shot and "23.5% across the benchmark"
fine-tuned, with more retrieved items generally better. These are preference and
ROUGE tasks, not voice tasks, so treat the direction as suggestive and the
numbers as off-target.

**What this says for us.** Keep the profile; stop asking it to do the work
exemplars do better. The profile's remaining job is precisely
[E0004](E0004-what-the-professional-craft-skill-could-not-say.md)'s uncountable
list — negative space, the personal hedging floor, what the writer never does —
none of which a sample of five passages can state. Add verbatim exemplars drawn
from the same text population as the thing being written, about five of them,
chosen for population match rather than topic match.

# 2. Fine-tuning, LoRA and DPO on ~9,000 words

Three questions: is the data enough, is there a path without a GPU, and does it
cost anything that matters. The answers are "possibly", "not really any more",
and "yes, text quality".

**At our data scale, one study exists and it is a single-user case study.**
*Small Is Enough: Per-User Style Rewriting of AI-Edited Text via LoRA Adapters*
(arXiv [2607.29238](https://arxiv.org/html/2607.29238v1), Chakravorty,
2026-07-31) trains per-user adapters from **487 paragraphs drawn from ~36
scientific papers by one author** — 414 source paragraphs expanded to 1,242
training pairs by paraphrasing each through three helper models, 73 paragraphs
and 219 pairs held out. Qwen2.5 at 0.5B/1.5B/3B/7B, 4-bit NF4 QLoRA, rank 8,
α 16, dropout 0.05, all linear layers, 3 epochs, effective batch 16, 2,048
tokens, lr 2×10⁻⁴. Training took 9.53 minutes (0.5B) to 67.73 minutes (7B) on
one laptop GPU.

The composite score **plateaued at 0.69 for every model size and both decoding
modes**. The 7B greedy component breakdown is the interesting bit:

| component | score |
|---|---|
| content similarity | 0.93 |
| target similarity | 0.89 |
| authorship | 0.53 |
| AI-tell reduction | 0.50 |
| **stylometric improvement** | **0.00** |

LLM judges rated the rewrites 5.34 on perceived AI-ness against 6.85 for their
helper-model inputs (0–10 scale), "22% lower". One user, synthetic training
pairs, no human evaluation ("No completed human-participant ratings are
available"), eight source paragraphs behind the 400 judge ratings, and no
overfitting or forgetting analysis at all. The author's own limitation: the
experiments "cannot establish generalization across users, languages or amounts
of available writing."

Note what fine-tuning did *not* buy: stylometric improvement 0.00. Our markers
would not have moved.

**Fine-tuning buys style and sells quality, measurably.**
[2610.03163](https://arxiv.org/html/2610.03163) runs LoRA fine-tuning beside
inference-time methods on the same 203 seen authors (Qwen3-4B-Instruct-2507):

| method | style accuracy | quality preference rate |
|---|---|---|
| zero-shot | 31.0% | 97.9% |
| few-shot prompt (3 ex.) | 28.1% | 91.5% |
| **LoRA fine-tuning** | **49.8%** | **38.1%** |
| manual contrastive steering | 34.5% | 94.3% |
| learned steering | 35.0% | 89.6% |
| hypernetwork LoRA | 36.5% | 91.3% |

LoRA is the only method that moves style substantially, and it is the only
method whose output people stop preferring. A 38.1% preference rate against
97.9% is not a tradeoff we would accept on client-facing documents.

**Reported minima, from official documentation.** The commonly repeated
"100–500 examples" figure traces to vendor guidance and blog posts, not to a
study; here is what the vendors actually document.

| path | documented dataset size | access needed | status |
|---|---|---|---|
| OpenAI SFT | minimum **10** examples; "start with 50 well-crafted demonstrations"; improvements at "50–100" | API only | **Closing.** "OpenAI is winding down its fine-tuning platform; new users cannot access it, and eligible existing customers can only create training jobs until January 6, 2027." |
| Claude 3 Haiku on Bedrock | training 32–10,000 lines, validation 32–1,000, sum ≤ 10,000 | AWS account, us-west-2 | GA 2024-11-01; **requires purchasing Provisioned Throughput to serve the customized model** |
| Fireworks SFT/LoRA | "one JSON object per line, from 3 to 3 million lines" | API + rented GPU | on-demand dedicated deployment is "the only supported method for serving trained models" — no serverless |
| Together AI | no minimum stated in the data-preparation docs | API | see *could not verify* |

Anthropic's first-party API offers no fine-tuning; the only documented Claude
path is Claude 3 Haiku SFT on Bedrock. Supported models for OpenAI SFT are
`gpt-4.1`, `gpt-4.1-mini`, `gpt-4.1-nano` — and that door is shutting for anyone
not already through it.

**DPO on a corpus this small has a named failure mode.** *Style-Debiased DPO*
(arXiv [2609.16532](https://arxiv.org/html/2609.16532v1)) describes DPO pushing
down rejected responses that differ from the chosen one only in style, and
reports that the naive form lowers accuracy when the corpus is small "because
the phrasings are not diverse and the distribution is narrow". I read this from
the paper's own framing of related work rather than from a controlled experiment
at 9k words, so treat it as a flag rather than a measurement.

**Verdict for us.** The data might be enough, the hosted paths are closing or
carry standing infrastructure cost, the one study at our scale moved no
stylometry and ran no human evaluation, and the best-measured LoRA result trades
away two thirds of its quality preference. And a fine-tuned model is not a
Claude Code plugin — it is a model, which breaks
[D0019](../decisions/D0019-humanize-me-ships-as-a-claude-code-plugin.md) by
construction.

# 3. Authorship verification and style embeddings as the metric

This was the high-priority ask and it has the most useful answer, plus the most
important bad news.

## The bad news first: no metric here predicts the author's verdict

*Can You Make It Sound Like You? Post-Editing LLM-Generated Text for Personal
Style* (arXiv [2604.24444](https://arxiv.org/abs/2604.24444), Baumler, Bao,
Nghiem, Yang, Carpuat & Daumé III, 2026-04-27) is a pre-registered study,
**n = 81**, in which people post-edited LLM drafts for tasks where personal
style mattered to them — wedding vows, apology letters, eulogies, condolence
letters, six of eight tasks each. LUAR-MUD was the primary metric, chosen for
scoring highest on their authorship-identification comparison (MRR 0.5888,
R@1 0.4506). Findings:

- Post-editing raised similarity to the writer's own unassisted writing
  (p = .0002, Hedges' g = 0.55, 95% CI 0.38–0.71) and lowered similarity to the
  LLM text (g = −0.41).
- Post-edited text nonetheless stayed **closer to the LLM than to the writer's
  own control text, g = −1.43**, and was more stylistically homogeneous than
  unassisted human writing (g = 1.42).
- The one that matters most: LUAR similarity against the writers' *own*
  perception of stylistic similarity is "significantly positive but weakly
  calibrated correlation (H3, **r = 0.244 ± 0.076, p < .0001**)".
- Participants rated their post-edited text as **no less representative of their
  personal style than their own unassisted writing** (p = .9062, g = 0.01),
  while the embedding still saw LLM traces.

So the metric and the author disagree, in both directions, and the disagreement
is the normal case rather than an edge case. Add the |r| < 0.07 between LUAR,
LLM-judge and stylometry from [2604.26460](https://arxiv.org/abs/2604.26460) and
the picture is four measuring instruments that do not agree with each other or
with the person. **An embedding score is a regression tripwire, not an acceptance
test.** It will catch a document drifting away from the corpus. It will not tell
us the operator will accept it.

## What is runnable, and which model to pick

All three of these are RoBERTa-scale encoders in the 82M–125M parameter range on
HuggingFace — trivially CPU-runnable, and small enough to vendor into a plugin's
local script.

**LUAR** — *Learning Universal Authorship Representations*, Rivera-Soto, Miano,
Ordonez, Chen, Khan, Bishop & Andrews,
[EMNLP 2021](https://aclanthology.org/2021.emnlp-main.70/). Contrastively
trained to score whether two *collections* of documents share an author; zero-
shot transfer tested across Amazon reviews, fanfiction and Reddit comments, with
the abstract reporting variable success by domain pair. Checkpoint
[`rrivera1849/LUAR-MUD`](https://huggingface.co/rrivera1849/LUAR-MUD),
**82.5M parameters**, Apache-2.0, `trust_remote_code=True`, trained on the
Reddit Million User Dataset; code at [LLNL/LUAR](https://github.com/LLNL/LUAR),
Apache-2.0. **It consumes "episodes" — several documents presumed to share an
author — and gives no per-document vector**, which is why the genealogy paper
below had to exclude it from a per-document analysis. For us that means scoring
a single generated document requires deciding what its episode is.

**Wegmann style embeddings** — *Same Author or Just Same Topic? Towards
Content-Independent Style Representations*, Wegmann, Schraagen & Nguyen, arXiv
[2204.04907](https://arxiv.org/abs/2204.04907), RepL4NLP 2022. The contribution
is a variation of the authorship-verification training task that **controls for
content using conversation or domain labels**, because "as the same author might
typically write about certain topics, representations trained on AV might also
encode content information instead of style alone". Their finding, verbatim:
"representations trained by controlling for conversation are better than
representations trained with domain or no content control at representing style
independent from content." Checkpoint
[`AnnaWegmann/Style-Embedding`](https://huggingface.co/AnnaWegmann/Style-Embedding),
`roberta-base`, a sentence-transformers model producing 768-dimensional
vectors — so it *does* give a per-document vector, unlike LUAR.

**StyleDistance** — Patel, Zhu, Qiu, Horvitz, Apidianaki, McKeown &
Callison-Burch, arXiv [2410.12757](https://arxiv.org/html/2410.12757v2)v2,
2025-02-08. Trained on SynthStel: ~320,000 contrastive triplets over 40 style
features in 7 linguistic categories, from 100 GPT-4-generated parallel pairs per
feature where style varies and meaning is held constant. `roberta-base` with
LoRA r=8. Checkpoint
[`StyleDistance/styledistance`](https://huggingface.co/StyleDistance/styledistance).
Their reported comparison on the STEL framework and its content-controlled
variant (Wegmann & Nguyen, *Does It Capture STEL?*,
[EMNLP 2021](https://aclanthology.org/2021.emnlp-main.569/) — 1,830 tasks across
4 style dimensions):

| model | STEL | STEL-or-Content | AV ROC-AUC (avg) | style-transfer eval |
|---|---|---|---|---|
| LUAR | **0.86** | **0.03** | 0.56–0.57 | 0.38 |
| Wegmann et al. 2022 | 0.77 | 0.22 | 0.56–0.57 | 0.39 |
| StyleDistance | 0.87 | **0.29** | **0.64** | **0.46** |

**The LUAR row is the decision.** 0.86 on STEL and **0.03** on
STEL-or-Content means LUAR, asked to choose between a style match and a content
match, takes the content match almost every time. Our generated documents are
client-facing feature walkthroughs; our corpus is published blog posts about
measurement and CI. The topics do not overlap. A content-sensitive encoder would
score that mismatch as a voice failure. **StyleDistance is the right default for
us and LUAR is the wrong one**, which is a conclusion neither paper states, but
it follows directly from the 0.03 against 0.29 and from the register gap
recorded in
[E0005](E0005-markers-are-genre-sensitive-and-the-checker-must.md). Noted as our
inference, not as a cited result.

## The metric needs a floor and a ceiling or it means nothing

The most portable methodological lesson in this whole survey is Sawant's
calibration: a raw similarity number is uninterpretable. Compute, from the
operator's own corpus:

- a **ceiling** — the operator's held-out samples scored against the training
  samples (their 0.756), which is the best any generation could honestly hope
  for; and
- a **floor** — the operator's samples scored against *other people's* writing
  in the same register (their 0.626), below which a score carries no
  author-specific information at all.

All four of their personalization methods scored 0.484–0.508, below the floor.
A checker reporting "similarity 0.51" without those two anchors would have read
as a pass. We already have the held-out split that the ceiling needs: the 2
reserved samples, 2,302 words, from
[E0005](E0005-markers-are-genre-sensitive-and-the-checker-must.md).

## One caution on what the embedding is actually measuring

*Writing Style Similarity Reflects Academic Genealogy* (arXiv
[2608.14843](https://arxiv.org/html/2608.14843), Manzo) builds a corpus of 5,803
arXiv authors with ≥2 solo-authored papers plus 2,501 ground-truth
advisor–student pairs from the Mathematics Genealogy Project, and finds academic
siblings — two students of one advisor who may never have met — sitting **30.4%
closer across 8,360 pairs**, with closed-set attribution errors landing on the
true author's advisor, student, sibling or lab mate **11 times more often than
chance**. Stylistic similarity tracks shared training, not identity. For a
one-author regression check that is survivable; it is why the cross-author floor
is not zero.

## Classical stylometry, for completeness

Both CPU-only and installable in a line, if Burrows' Delta is wanted beside the
neural scores: [`faststylometry`](https://pypi.org/project/faststylometry/) on
PyPI (Python, Burrows' Delta) and
[`stylo`](https://cran.r-project.org/web/packages/stylo/stylo.pdf) 0.6.3 on CRAN
(R, GPL-3, multiple distance metrics). For interpretable feature counts at
scale, **Neurobiber** (Alkiek, Wegmann, Zhu & Jurgens, arXiv
[2502.18590](https://arxiv.org/html/2502.18590v1)v1, 2025-02-25) predicts 96
Biber-style features at macro-F1 0.97 / micro-F1 0.98 on a held-out set of
~4 million sequences, 117,000 tokens/sec on one RTX A6000 at batch size 128 and
**56× faster than the CPU-based Multidimensional Analysis Tagger**; checkpoint
[`Blablablab/neurobiber`](https://huggingface.co/Blablablab/neurobiber), ~0.1B
parameters. CPU inference is not discussed in the paper or demonstrated on the
card — the examples move the model to CUDA — but 0.1B parameters is well within
CPU reach for a handful of documents. This is an upgrade path for our marker
layer, not a replacement for it, and note that
[E0005](E0005-markers-are-genre-sensitive-and-the-checker-must.md) and
[E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md) already
established that the marker layer is not where the value is.

# 4. Activation steering and style vectors

**Honest answer: unreachable, and not as a matter of difficulty.** Every method
in this family needs to read or write something the Anthropic API does not
expose.

| method | what it needs |
|---|---|
| Style Vectors (Konen, Jentzsch, Diallo, Schütt, Bensch, El Baff, Opitz & Hecking, [Findings of EACL 2024](https://aclanthology.org/2024.findings-eacl.52/)) | "recorded layer activations for input texts in a specific style", then addition into hidden layers during generation |
| StyleVector (Zhang, Liu, Wang, Liu, Wu, Wang & Chua, arXiv [2503.05213](https://arxiv.org/abs/2503.05213), 2025-03-07) | the LLM's activation space; training-free otherwise. Reports "a significant 8% relative improvement in personalized generation while reducing storage requirements by 1700 times over PEFT" |
| CHAMELEON (Zhang, Adila, Shin & Sala, arXiv [2503.01048](https://arxiv.org/html/2503.01048v3)v3, Findings of NAACL 2025) | embedding editing on MLP outputs of selected decoder layers — weights and hidden representations |
| Hypernetwork LoRA / learned steering ([2610.03163](https://arxiv.org/html/2610.03163)) | frozen Qwen3-4B plus hidden-layer activations for injection |
| Weightless Fine-Tuning (Zhang, Ni, Wang & Dhillon, arXiv [2608.11342](https://arxiv.org/html/2608.11342v1), 2026-08-11) | output logits **and** the ability to enable dropout at inference, i.e. stochastic forward passes through the frozen model |

Weightless Fine-Tuning is the closest near-miss and deserves naming because its
pitch sounds API-compatible: it "does not require direct access to model weights
and operates only through stochastic forward passes and output logits",
approximates SFT at under 7% of its effective computation, was preferred over
SFT in **31 of 50** human comparisons, and matches SFT's logit shift at cosine
similarity 0.875 on top-10 tokens, using up to 50 training sequences per author
on LaMP. It still needs logits and runtime dropout control. The Anthropic
Messages API provides neither.

CHAMELEON is worth one more line for a transferable number: its ablation finds
performance degrading at 5 user-history entries and **also** declining at 25+,
with an optimum around 10–15. That is a second independent signal that the
useful exemplar budget is small, consistent with
[2509.14543](https://arxiv.org/html/2509.14543v1)'s 2-to-10 sweep showing almost
no movement.

If we ever want this family, it means running an open-weights model locally,
which is a different project with different constraints. Recorded so nobody
re-researches it.

# 5. Iterative critique-and-revise with a style judge

**The loop works and is API-only; the specific question the brief asked is
unanswered in the literature.**

*Iterative Critique-Refine Framework for Enhancing LLM Personalization*
("PerFine", arXiv [2510.24469](https://arxiv.org/html/2510.24469v1), Maram,
Gandhi, Yao, Akkinapalli, Dernoncourt, Wang, Rossi & Ahmed, 2025-10-28) is
training-free: a generator drafts conditioned on a retrieved user profile, a
separate critic LLM — conditioned on **the same raw retrieved texts, not an
abstracted description** — returns structured feedback on tone consistency,
vocabulary match, sentence structure and topic relevance, and the generator
revises. Measured against PGraphRAG on the AgentSociety Challenge data:

| dataset | GEval | METEOR |
|---|---|---|
| Yelp | 0.400 → 0.441 (+10.25%) | 0.180 → 0.195 |
| Goodreads | 0.445 → 0.480 (+7.8%) | 0.206 → 0.216 |
| Amazon | 0.410 → 0.465 (+13.41%) | 0.190 → 0.204 |

"Gains accumulate over 3–5 refinement rounds before leveling off"; experiments
fix T=5.

**But it does not run the ablation we wanted.** Both generator and critic always
see retrieved raw samples; there is no condition isolating a sample-conditioned
critic against a description-conditioned critic. So "does a judge holding the
author's samples beat a judge holding a style description" has no direct
measurement I could find. The adjacent evidence is indirect and points the same
way: reference-guided LLM judging, where human-written references act as
comparison anchors rather than abstract rubric criteria, is reported to mitigate
limitations of rubric-only evaluation; and the rubric-artifact literature (e.g.
arXiv [2609.02942](https://arxiv.org/html/2609.02942v1)) finds judges encoding
latent priors in rubric formulations. Both are consistent with samples beating
descriptions and neither measures authorial voice. Flagging this as the clearest
gap in the survey, and one we could close ourselves cheaply.

One more reason to expect a judge to be the weak link: in Sawant's data the
LLM judge is the metric that *most* rewards the profile (0.542 against 0.433 for
few-shot) while the authorship metric does not. A judge given a style
description may be grading how well the output matches the description — which
is how our 8-of-8 document came to exist.

**Verbalized Sampling is the one generation-time trick that is both training-free
and confirmed to work through a plain API.**
[2510.01171](https://arxiv.org/html/2510.01171v4) replaces "write X" with "write
5 of X with their corresponding probabilities"; the authors state it is
training-free and requires "no logit access", and they tested it on GPT, Gemini,
Claude, o3, Llama and Qwen. Measured: semantic diversity (1 − mean pairwise
cosine similarity) up **1.6–2.1×** over direct prompting on poem continuation,
story generation and joke writing, 100 data points per task, k=5 candidates per
call, N=30 samples per prompt; human-rated diversity 2.39 / 3.06 / 3.01
(poem / story / joke) against direct prompting's 1.90 / 2.74 / 1.83 on a 4-point
scale, 90 annotators (30 per task), 90 pairs per task, inter-annotator agreement
0.49–0.87, reported as a 25.7% improvement. What it measures is *diversity*, not
authorship fidelity. The reason to try it anyway is that the diagnosed failure
is collapse to a generic register, and this is the cheapest published lever
against that collapse: generate five candidate drafts, then pick with the
embedding score rather than taking the first.

# What I would try, ranked, against our constraints

Ordered by expected value per unit of work given ~9,000 words, API-only access,
no GPU, and a plugin as the delivery vehicle.

**1. Run the held-out regeneration diff. It is already in the design and still
has not run.** [E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md)
named it as the only check that could have caught either failure, and this survey
supports that from the outside: the author-facing verdict correlates with the
best automated metric at r = 0.244 (n = 81), and the automated metrics correlate
with each other at |r| < 0.07. When every instrument disagrees with the person,
the test is to regenerate text the operator already wrote and diff it against
what they actually wrote. Cost: zero new dependencies. It is also the only test
in the design whose answer the operator cannot dispute, because they wrote the
answer key.

**2. Add population-matched verbatim exemplars to the generation prompt, and cut
the profile back to what exemplars cannot carry.** Five passages, retrieved by
*text population* — headings for headings, paragraph prose for paragraph prose —
never by topic. Justification: raw history beats generated profiles on every
LaMP generation row; the profile method wins the LLM judge and the stylometry
and loses the authorship metric; topic-similar selection measurably hurts
(81.28% vs 95.44%); 5 exemplars performs like 10. The profile keeps
[E0004](E0004-what-the-professional-craft-skill-could-not-say.md)'s uncountable
seven — negative space, the hedging floor, what this writer never does — which
no sample states. This is also the change that directly fixes
[E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md) cause 1:
the corpus headings were in the training set the whole time, and putting them in
the prompt is strictly better than describing them. Measure it against the
held-out diff before believing it —
[2610.03163](https://arxiv.org/html/2610.03163) has three-shot prompting
*losing* to zero-shot.

**3. Replace the marker gate with a calibrated StyleDistance score, and keep the
markers as diagnostics rather than as the gate.** `StyleDistance/styledistance`,
roberta-base, HuggingFace, CPU, one script. Compute the ceiling (operator's
2,302 held-out words against the 5,685 training words) and the floor (operator
against other authors in the same register) once, and report every generated
document as a position between them. Choose StyleDistance over LUAR because
LUAR scores 0.03 on STEL-or-Content against StyleDistance's 0.29 and our
generated documents are off-corpus-topic by construction; also because LUAR
needs an episode and gives no per-document vector. **Promise it as a drift
tripwire, not an acceptance test** — r = 0.244 is the honest ceiling on what it
predicts about the operator's reaction, and
[E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md) is what
happens when a gate gets promoted to a verdict.

**4. Add a critique-and-revise pass whose critic holds corpus passages, not the
profile.** PerFine's structure, training-free, API-only, +7.8% to +13.4% GEval,
3–5 rounds then plateau. Two reasons to expect more from it here than the
published numbers suggest: both of
[E0006](E0006-the-operator-rejected-a-profile-that-passed-every.md)'s causes are
already stated as mechanical rules — "if the short sentence contains a claim the
paragraph did not make, it is not this writer's landing", and the three heading
shapes — and a critic can check a mechanical rule against the corpus far more
reliably than a generator can obey a described one. Second, the
description-conditioned judge is the instrument that most flattered our profile
in Sawant's table, so swapping its context is the cheap experiment. And since
nobody has published the sample-critic versus description-critic ablation, we
would be measuring something new rather than reproducing something known.

**5. Try Verbalized Sampling at the drafting step, and pick with the score from
(3).** Five candidates with stated probabilities, rank by StyleDistance against
the corpus, keep one. Training-free, no logit access, confirmed on Claude,
1.6–2.1× diversity. Low confidence it helps *voice* — the measured outcome is
diversity, not authorship — but it is an afternoon, it attacks the exact failure
mode the field has diagnosed, and it composes with everything above.

**Not recommended: fine-tuning.** No first-party Anthropic path exists; the
Bedrock path is Claude 3 Haiku in us-west-2 and requires buying Provisioned
Throughput to serve the result; OpenAI's is closed to new users and ends
2027-01-06; Fireworks requires a dedicated deployment. On the merits rather than
the logistics: the one study at our data scale plateaued at 0.69 for every model
size with stylometric improvement of exactly 0.00, ran no human evaluation, and
covered one user; and the best-controlled LoRA comparison shows style accuracy
rising 31.0% → 49.8% while quality preference falls 97.9% → 38.1%. We would be
buying the thing our markers already measure and selling the thing the operator
actually rejected the document for.

**Not available: activation steering.** Hidden-state read/write or logits plus
runtime dropout, in every variant. The Anthropic API exposes neither. This is a
boundary, not a backlog item.

# What I could not verify

- **The LUAR paper's own retrieval numbers.** The ACL Anthology PDF extraction
  returned corrupted text and I did not obtain the R@8 / MRR tables, the
  per-dataset author counts, or the episode-length ablation. The LUAR numbers
  reported above (MRR 0.5888, R@1 0.4506) come from
  [2604.24444](https://arxiv.org/abs/2604.24444)'s own comparison, not from
  Rivera-Soto et al.
- **The STEL accuracies in Wegmann et al. 2022.** One PDF extraction produced a
  table of numbers plus a model name and parameter count that contradicted the
  model card and the known size of `roberta-base`; I discarded all of it. The
  Wegmann figures quoted above (STEL 0.77, STEL-or-Content 0.22) are
  StyleDistance's reported reproduction, not the original paper's own.
- **The magnitude of RLHF's diversity reduction** in Kirk et al. The abstract
  says "significantly reduces... across a variety of measures" and names no
  number; I did not reach the results tables.
- **Numbers from *Can Activation Steering Capture Multidimensional Authorship
  Style?*** (arXiv [2609.04792](https://arxiv.org/pdf/2609.04792), Tran, Bao &
  Carpuat). The PDF extraction yielded only qualitative claims. The access
  requirement — weights and activations — is confirmed; the results are not.
- **Together AI's minimum dataset size.** Their official data-preparation page
  states that validation checks "the line count exceeds the minimum" without
  saying what the minimum is. The widely repeated "low hundreds of examples for
  LoRA" figure traces to a third-party blog, not to Together's documentation,
  and is not reported above as fact.
- **Whether Claude 3 Haiku fine-tuning on Bedrock is still offered in 2026.**
  The GA announcement is dated 2024-11-01 and is primary; the AWS documentation
  page listing currently customizable models returned no readable table on
  fetch, and the claim that it remains the only Claude fine-tuning path appeared
  only in secondary sources.
- **A direct sample-conditioned versus description-conditioned style-judge
  comparison.** I did not find one. The adjacent reference-guided-judging
  literature points the right way but measures instruction following, not voice.
- **Any paper testing population-matched exemplar retrieval** (headings
  retrieved for headings). Topic-matched retrieval has a measured negative
  result; the population-matched variant appears to be untested, which makes
  recommendation 2 an experiment rather than an application.
- **Peer-review status.** 2604.26460, 2608.19746, 2606.05336, 2607.29238,
  2609.04792, 2610.03163, 2604.24444 and 2608.14843 are arXiv preprints whose
  venue I could not confirm. 2604.26460 and 2608.19746 are two overlapping
  papers by one independent researcher and carry more weight in this node than
  any single unreviewed preprint comfortably should.

# Citations

Read 2026-11-10. Grouped by what they are used for.

**The authorship gap and the method comparison**
- Sawant, *Theory-Grounded Evaluation Exposes the Authorship Gap in LLM
  Personalization*, arXiv [2604.26460](https://arxiv.org/abs/2604.26460)
  (v1 2026-04-29, v2 2026-08-14)
- Sawant, *PersonalBench: Measuring the Authorship Gap in LLM Personalization*,
  arXiv [2608.19746](https://arxiv.org/html/2608.19746v1) (2026-08-20)
- Wang, Tripto, Park, Li & Zhou, *Catch Me If You Can? Not Yet: LLMs Still
  Struggle to Imitate the Implicit Writing Styles of Everyday Authors*, arXiv
  [2509.14543](https://arxiv.org/html/2509.14543v1) (2025-09-18; Findings of
  EMNLP 2025)

**Exemplars, profiles and retrieval**
- Patel, Andrews & Callison-Burch, *Low-Resource Authorship Style Transfer: Can
  Non-Famous Authors Be Imitated?*, arXiv
  [2212.08986](https://arxiv.org/html/2212.08986)v3 (2024-11-04)
- Ju, Qiu, Zhao & Shah, *Self-supervised User Profile Generation for
  Personalization*, arXiv [2606.05336](https://arxiv.org/html/2606.05336)
  (2026-06-03)
- Salemi, Mysore, Bendersky & Zamani, *LaMP: When Large Language Models Meet
  Personalization*, arXiv [2304.11406](https://arxiv.org/abs/2304.11406)
- Richardson et al., *Integrating Summarization and Retrieval for Enhanced
  Personalization via Large Language Models*, arXiv
  [2310.20081](https://ar5iv.labs.arxiv.org/html/2310.20081)

**Style embeddings and stylometry**
- Rivera-Soto, Miano, Ordonez, Chen, Khan, Bishop & Andrews, *Learning Universal
  Authorship Representations*, [EMNLP 2021](https://aclanthology.org/2021.emnlp-main.70/);
  code [LLNL/LUAR](https://github.com/LLNL/LUAR); checkpoint
  [`rrivera1849/LUAR-MUD`](https://huggingface.co/rrivera1849/LUAR-MUD)
- Wegmann, Schraagen & Nguyen, *Same Author or Just Same Topic? Towards
  Content-Independent Style Representations*, arXiv
  [2204.04907](https://arxiv.org/abs/2204.04907) (RepL4NLP 2022); checkpoint
  [`AnnaWegmann/Style-Embedding`](https://huggingface.co/AnnaWegmann/Style-Embedding)
- Wegmann & Nguyen, *Does It Capture STEL? A Modular, Similarity-based
  Linguistic Style Evaluation Framework*,
  [EMNLP 2021](https://aclanthology.org/2021.emnlp-main.569/)
- Patel, Zhu, Qiu, Horvitz, Apidianaki, McKeown & Callison-Burch,
  *StyleDistance: Stronger Content-Independent Style Embeddings with Synthetic
  Parallel Examples*, arXiv [2410.12757](https://arxiv.org/html/2410.12757v2)v2
  (2025-02-08); checkpoint
  [`StyleDistance/styledistance`](https://huggingface.co/StyleDistance/styledistance)
- Alkiek, Wegmann, Zhu & Jurgens, *Neurobiber: Fast and Interpretable Stylistic
  Feature Extraction*, arXiv
  [2502.18590](https://arxiv.org/html/2502.18590v1)v1 (2025-02-25); checkpoint
  [`Blablablab/neurobiber`](https://huggingface.co/Blablablab/neurobiber)
- Manzo, *Writing Style Similarity Reflects Academic Genealogy*, arXiv
  [2608.14843](https://arxiv.org/html/2608.14843)
- [`faststylometry`](https://pypi.org/project/faststylometry/) (PyPI);
  [`stylo`](https://cran.r-project.org/web/packages/stylo/stylo.pdf) 0.6.3
  (CRAN, GPL-3)

**The metric-versus-person gap**
- Baumler, Bao, Nghiem, Yang, Carpuat & Daumé III, *Can You Make It Sound Like
  You? Post-Editing LLM-Generated Text for Personal Style*, arXiv
  [2604.24444](https://arxiv.org/abs/2604.24444) (2026-04-27)

**Fine-tuning at small scale, and the hosted paths**
- Chakravorty, *Small Is Enough: Per-User Style Rewriting of AI-Edited Text via
  LoRA Adapters*, arXiv [2607.29238](https://arxiv.org/html/2607.29238v1)
  (2026-07-31)
- Popp, Liu, Sinhamahapatra & Niehues, *Predicting Steering Vectors and Adapter
  Weights for Few-Shot Author-Style Transfer*, arXiv
  [2610.03163](https://arxiv.org/html/2610.03163) (2026-10-02)
- *Style-Debiased DPO*, arXiv [2609.16532](https://arxiv.org/html/2609.16532v1)
- OpenAI, [Supervised fine-tuning](https://developers.openai.com/api/docs/guides/supervised-fine-tuning)
  (official docs)
- AWS, [Fine-tuning for Anthropic's Claude 3 Haiku model in Amazon Bedrock is
  now generally available](https://aws.amazon.com/blogs/aws/fine-tuning-for-anthropics-claude-3-haiku-model-in-amazon-bedrock-is-now-generally-available/)
  (2024-11-01)
- Fireworks AI, [Supervised Fine-Tuning (SFT) with LoRA](https://docs.fireworks.ai/fine-tuning/supervised-fine-tuning)
  (official docs)
- Together AI, [Data preparation](https://docs.together.ai/docs/fine-tuning/data-preparation)
  (official docs)

**Steering and the access boundary**
- Konen, Jentzsch, Diallo, Schütt, Bensch, El Baff, Opitz & Hecking, *Style
  Vectors for Steering Generative Large Language Models*,
  [Findings of EACL 2024](https://aclanthology.org/2024.findings-eacl.52/)
- Zhang, Liu, Wang, Liu, Wu, Wang & Chua, *Personalized Text Generation with
  Contrastive Activation Steering*, arXiv
  [2503.05213](https://arxiv.org/abs/2503.05213) (2025-03-07)
- Zhang, Adila, Shin & Sala, *Personalize Your LLM: Fake it then Align it*
  (CHAMELEON), arXiv [2503.01048](https://arxiv.org/html/2503.01048v3)v3
  (Findings of NAACL 2025)
- Zhang, Ni, Wang & Dhillon, *Weightless Fine-Tuning: Personalizing LLMs via
  Logit-Space Transport*, arXiv
  [2608.11342](https://arxiv.org/html/2608.11342v1) (2026-08-11)

**Critique loops, judges, and mode collapse**
- Maram, Gandhi, Yao, Akkinapalli, Dernoncourt, Wang, Rossi & Ahmed, *Iterative
  Critique-Refine Framework for Enhancing LLM Personalization* (PerFine), arXiv
  [2510.24469](https://arxiv.org/html/2510.24469v1) (2025-10-28)
- *Judging LLM-as-a-Judge: Concerning Rubric Artifacts in LLM-based Automated
  Text Generation Evaluation*, arXiv
  [2609.02942](https://arxiv.org/html/2609.02942v1)
- Zhang, Yu, Chong, Sicilia, Tomz, Manning & Shi, *Verbalized Sampling: How to
  Mitigate Mode Collapse and Unlock LLM Diversity*, arXiv
  [2510.01171](https://arxiv.org/html/2510.01171v4)v4
- Kirk, Mediratta, Nalmpantis, Luketina, Hambro, Grefenstette & Raileanu,
  *Understanding the Effects of RLHF on LLM Generalisation and Diversity*, arXiv
  [2310.06452](https://arxiv.org/abs/2310.06452) (ICLR 2024)

**Style-transfer systems recorded for completeness, all GPU-bound**
- Khan, Wang, Hager & Andrews, *Learning to Generate Text in Arbitrary Writing
  Styles* (StyleMC), arXiv
  [2312.17242](https://arxiv.org/html/2312.17242v2)v2 (2024-03-04) — ~16 samples
  averaging 68 words per author; UAR 0.849 against GPT-4's 0.767 and a human
  reference of 0.852, on 800 Reddit authors; needs token-level logit rescoring,
  "commodity hardware (e.g., a single GPU) is sufficient"
- Horvitz, Patel, Singh, Callison-Burch, McKeown & Yu, *TinyStyler: Efficient
  Few-Shot Text Style Transfer with Authorship Embeddings*, arXiv
  [2406.15586](https://arxiv.org/html/2406.15586v2)v2 (2024-11-07) — T5-Large,
  800M parameters, conditions on style embeddings, 16 target examples at
  inference; authorship-transfer joint 0.69 with reranking against GPT-4's 0.68;
  checkpoint [`tinystyler/tinystyler`](https://huggingface.co/tinystyler/tinystyler);
  0.47s per example on an A100
