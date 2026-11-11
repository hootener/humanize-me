# References

Published work this project's design decisions actually rest on, and what each
one is load-bearing for. Everything here was read and checked against its
primary source; where a figure could not be verified, that is recorded in
[`brain/knowledge-catalog/reference/E0007`](brain/knowledge-catalog/reference/E0007-state-of-the-art-for-reproducing-a-specific.md),
which also lists work we read and did **not** build on.

Nothing in this library is a reimplementation of any paper below. These are
cited because they changed a decision.

## The author is not a reliable judge of their own voice

> Baumler, Bao, Nghiem, Yang, Carpuat & Daumé III. *Can You Make It Sound Like
> You? Post-Editing LLM-Generated Text for Personal Style.*
> arXiv:[2604.24444](https://arxiv.org/abs/2604.24444)

Pre-registered, n = 81. The correlation between a writer's own sense of
stylistic similarity and the best-performing authorship metric is
**r = 0.244 ± 0.076**. Participants rated post-edited LLM text as *no less*
representative of their personal style than their own unassisted writing
(p = .9062), while the embedding still saw LLM traces.

**Justifies:** D0018 as amended — a profile verified only by its author's
reaction to prose is weakly verified, and a style score is a drift tripwire
rather than an acceptance test. We reproduced the effect on a sample of one
(E0008): our operator identified his own published writing at exactly chance.

## Human preference carries a bias toward typical text

> Zhang, Yu, Chong, Sicilia, Tomz, Manning & Shi. *Verbalized Sampling: How to
> Mitigate Mode Collapse and Unlock LLM Diversity.*
> arXiv:[2510.01171](https://arxiv.org/abs/2510.01171)

Attributes mode collapse to typicality bias in preference data rather than to
the RL algorithm. Decomposing reward with a Bradley-Terry model over 6,874
correctness-matched response pairs gives a typicality coefficient of
**α̂ = 0.57 ± 0.07 and 0.65 ± 0.07, both p < 10⁻¹⁴**.

**Justifies:** D0022 — the preference signal is named defects, never blind
rankings. The bias was measured on human raters, so tuning a voice library on
a writer's blind preference would optimise toward the generic prose the library
exists to remove.

> Kirk, Mediratta, Nalmpantis, Luketina, Hambro, Grefenstette & Raileanu.
> *Understanding the Effects of RLHF on LLM Generalisation and Diversity.*
> arXiv:[2310.06452](https://arxiv.org/abs/2310.06452) (ICLR 2024)

Reports that RLHF "significantly reduces output diversity compared to SFT
across a variety of measures". The abstract states no magnitude and we did not
extract one — cited for direction only.

## Personal registers are the hard case

> Wang, Tripto, Park, Li & Zhou. *Catch Me If You Can? Not Yet: LLMs Still
> Struggle to Imitate the Implicit Writing Styles of Everyday Authors.*
> arXiv:[2509.14543](https://arxiv.org/abs/2509.14543) (Findings of EMNLP 2025)

400+ authors, 40,000+ generations per model. Five-shot authorship-verification
accuracy runs **95–97% on news and 16–21% on blogs**, against a human-text
baseline of 87–91%. Diagnoses failing domains as models defaulting to "an
average, generic tone".

**Justifies:** our expectations, and the decision to measure rather than assume.
Published blog prose is the domain that collapses, and it is the domain our
first corpus is made of.

## A described profile has no advantage on the authorship metric

> Sawant. *Theory-Grounded Evaluation Exposes the Authorship Gap in LLM
> Personalization.* arXiv:[2604.26460](https://arxiv.org/abs/2604.26460)
> — and *PersonalBench.* arXiv:[2608.19746](https://arxiv.org/abs/2608.19746)

50 authors, 1,000 generations. Four inference-time methods all score below the
**cross-author floor of 0.626** against a human ceiling of 0.756. A distilled
profile wins the LLM judge (0.542 vs 0.433) and function-word stylometry
(0.761 vs 0.749) and does **not** win the authorship metric (0.502 vs
few-shot's 0.508). The three metrics correlate pairwise at **|r| < 0.07**.

**Caveat we attach every time we cite this:** single independent author, two
overlapping preprints, no venue we could confirm, one corpus, English blogs
only. The *ranking* is not established; the absence of a profile advantage on
the authorship metric is.

**Justifies:** T0017 — testing verbatim exemplars against the described profile
rather than assuming the profile is the right artifact.

> Ju, Qiu, Zhao & Shah. *Self-supervised User Profile Generation for
> Personalization.* arXiv:[2606.05336](https://arxiv.org/abs/2606.05336)

Raw history beats generated profiles on every LaMP generation row. The authors'
own explanation: "any natural-language profile — ours or otherwise — abstracts
away exactly that idiolect." A paper proposing profiles, reporting that its
profiles lose.

> Patel, Andrews & Callison-Burch. *Low-Resource Authorship Style Transfer: Can
> Non-Famous Authors Be Imitated?*
> arXiv:[2212.08986](https://arxiv.org/abs/2212.08986)

In-context style transfer from ~500 words per author. Their verdict: "current
approaches do not yet achieve mastery of this challenging task."

## What we ruled out, and why

> Chakravorty. *Small Is Enough: Per-User Style Rewriting of AI-Edited Text via
> LoRA Adapters.* arXiv:[2607.29238](https://arxiv.org/abs/2607.29238)

The one study at our data scale plateaued at 0.69 for every model size with
**stylometric improvement of exactly 0.00**, no human evaluation, one user.

**Justifies:** not fine-tuning. The best-controlled LoRA comparison available
shows style accuracy rising 31.0% → 49.8% while quality preference falls
97.9% → 38.1%.

> Konen, Jentzsch, Diallo, Schütt, Bensch, El Baff, Opitz & Hecking. *Style
> Vectors for Steering Generative Large Language Models.*
> [Findings of EACL 2024](https://aclanthology.org/2024.findings-eacl.52/)

**Justifies:** not activation steering. Every variant needs hidden-state
read/write or logit access. The Anthropic Messages API exposes neither. A
boundary, not a backlog item.

## Measurement we may adopt but have not

> Patel, Zhu, Qiu, Horvitz, Apidianaki, McKeown & Callison-Burch.
> *StyleDistance: Stronger Content-Independent Style Embeddings with Synthetic
> Parallel Examples.* arXiv:[2410.12757](https://arxiv.org/abs/2410.12757)
> — checkpoint [`StyleDistance/styledistance`](https://huggingface.co/StyleDistance/styledistance)

Preferred over LUAR for our case because LUAR scores 0.03 on STEL-or-Content
against StyleDistance's 0.29, and our generated documents are off-corpus-topic
by construction.

> Rivera-Soto, Miano, Ordonez, Chen, Khan, Bishop & Andrews. *Learning
> Universal Authorship Representations.*
> [EMNLP 2021](https://aclanthology.org/2021.emnlp-main.70/)

> Maram, Gandhi, Yao, Akkinapalli, Dernoncourt, Wang, Rossi & Ahmed. *Iterative
> Critique-Refine Framework for Enhancing LLM Personalization* (PerFine).
> arXiv:[2510.24469](https://arxiv.org/abs/2510.24469)

Training-free critique-and-revise, +7.8% to +13.4% GEval, 3–5 rounds then
plateau. Not implemented here yet.
