# Investigation by AI about the mysterious 137

A three-hour, human-steered dialogue between AI systems on the origin of the fine-structure constant, with every script needed to reproduce the numbers.

**Authors:** Fable5.1, GPT5.6-Sol, l0d0v1c, pseudoLuc

> **Read this first.** This repository documents an *experiment*, not a discovery. The question was how far a steered conversation between AI systems, equipped with a Python sandbox and web search, can go in about three hours on a hard and numerology-prone topic, and in particular whether it can re-derive known results by partly independent routes while keeping track of its own errors. Nothing here has been peer reviewed or checked by a specialist. Almost every positive result turned out to be already in the literature, and the paper says so.

## What is in the paper

Starting from a naive question (does α tend to an asymptote at high energy?), the conversation ended up covering:

- **Direct geometric formulae fail.** 4.8 million products of volumes of symmetric spaces were tested against 1/α and three mass ratios, with decoy targets as a look-elsewhere control. The real constants behave like generic numbers. Wyler's 1969 formula is recovered as the unique hit of its class, and is shown to lie *above* the infrared floor of 1/α, so it cannot be α at any scale.
- **A conservation lemma.** A rigid ultraviolet condition (induced electrodynamics, duality fixed point) does not remove a continuous parameter: it trades the unified coupling for a threshold mass. A blind scan of 151,263 vector-like spectra rediscovers the "strong unification" scenario along the way.
- **The hypercharge normalisation.** At two loops, the Standard Model alone unifies for k_Y = 1.341 ± 0.004, compatible with k_Y = 4/3, which then predicts 1/α(0) = 136.7 (−0.26 %). This reproduces Barger, Jiang, Langacker and Li (2005) from independent inputs.
- **Where 4/3 can come from.** It is the normalisation of the U(1) commuting with SU(3)×SU(3) inside SU(6), and a generalised Schellekens condition ties it to electric charges in units of 1/6.
- **Stress tests.** Kaluza-Klein thresholds of the 7D SU(6) model, Bayesian evidence with an explicit Occam penalty, degeneracy of k_Y with the supersymmetry scale, and the Higgs quartic coupling. Three of the four weaken the conclusion, which ends up conditional.
- **A scorecard and an error log.** Section 7 lists eleven established results that were recovered and by which route. Section 8 lists the mistakes and retractions made during the session, in chronological order.

## Repository layout

```
.
├── README.md
├── paper/
│   ├── ai_investigation_137.tex     # self-contained LaTeX source (scripts embedded in Appendix B)
│   └── ai_investigation_137.pdf     # compiled paper, 24 pages
├── scripts/                         # the nine Python scripts, English comments
│   ├── 01_wyler.py
│   ├── 02_cartan_volumes.py
│   ├── 03_spectrum_scan.py
│   ├── 04_strong_coupling_prediction.py
│   ├── 05_kY_two_loops.py
│   ├── 06_kY_origin.py
│   ├── 07_KK_thresholds_SU6.py
│   ├── 08_two_scale_scan.py
│   └── 09_architecture_comparison.py
└── notes/                           # optional: working notes of the session (in French)
    ├── alpha-origine-geometrique-v6.md
    └── alpha-synthese.md
```

The scripts in `scripts/` are byte-for-byte the ones printed in Appendix B of the paper. Use the files rather than copying from the PDF, where long lines are wrapped for display.

## Requirements

- Python 3.9 or later
- `numpy` (no other dependency)

```bash
pip install numpy
```

## Reproducing the numbers

Every script is standalone, takes no input file and prints its results to the terminal.

```bash
cd scripts
python3 01_wyler.py
python3 05_kY_two_loops.py
python3 03_spectrum_scan.py 80      # optional argument: number of decoy worlds
```

| Script | Paper section | What it does | Indicative run time (one core) |
|---|---|---|---|
| `01_wyler.py` | 3.3 | Wyler's recipe in dimension n; brute-force search in the class 2^a 3^b 5^c π^d | seconds |
| `02_cartan_volumes.py` | 3.3 | Coincidences with volumes of Cartan domains, spheres and Shilov boundaries; decoy targets | ~1 min, ~1 GB RAM |
| `03_spectrum_scan.py` | 4.2 | Which of 151,263 vector-like spectra make all three couplings strong at a common scale; decoy worlds | minutes, proportional to the number of decoys |
| `04_strong_coupling_prediction.py` | 4.3 | Prediction of 1/α(0) under common strong coupling; sensitivity to the threshold mass | instant |
| `05_kY_two_loops.py` | 5.1 | Two-loop determination of k_Y and prediction of 1/α(0), Standard Model only | ~1 min |
| `06_kY_origin.py` | 5.2 | Generalised Schellekens condition, SU(N) embeddings, one-parameter heterotic fit, brane relations | ~2 min |
| `07_KK_thresholds_SU6.py` | 6.1 | Mode counting for the 7D SU(6) orbifold model, shift of the apparent k_Y, relic estimate | seconds |
| `08_two_scale_scan.py` | 4.2 | Extension of script 03 to two mass scales | ~4 min with 16 decoys |
| `09_architecture_comparison.py` | 6.2 to 6.4 | Bayesian evidence of the architectures, k_Y versus the supersymmetry scale, Higgs quartic | ~3 min |

Scripts 03 and 08 use a fixed random seed for the decoy worlds, so results are reproducible; p-values quoted in the paper come from 80 decoys (script 03) and 16 decoys (script 08).

## Building the paper

The LaTeX source is a single file with no external figure or bibliography file.

```bash
cd paper
pdflatex ai_investigation_137.tex
pdflatex ai_investigation_137.tex     # second pass for the table of contents and references
```

Packages used: `amsmath`, `amssymb`, `booktabs`, `array`, `authblk`, `xcolor`, `textcomp`, `upquote`, `listings`, `pgfplots`, `hyperref`, `geometry`. All are part of a standard TeX Live installation. A commented line in the preamble enables Latin Modern fonts if they are installed.

## How the session worked

- One conversation of about three hours, as timed by the human participants.
- The first AI system (Fable5.1, i.e. Claude Fable 5.1 by Anthropic) had a sandboxed Linux machine with Python and a web-search tool. It wrote and ran all scripts, checked the literature and drafted the paper.
- Midway, the working notes were submitted to a second AI system (GPT5.6-Sol). Its critique was pasted back into the conversation; the first system verified every number in it, conceded where it was wrong and objected where it disagreed.
- The human participants asked the questions, relayed material between the two systems, chose which follow-up to pursue and kept the time. No human supplied physics content.

## Known limitations

Please read Section 9 of the paper before relying on anything here. In short:

- One- and two-loop running only, with unknown thresholds at the unification scale.
- Some two-loop terms in script 09 (top Yukawa and Higgs quartic) were written from the model's memory and are validated only because the resulting vacuum-stability bound agrees with the literature.
- Decoy p-values depend on the chosen family of representations and on the multiplicity bounds.
- The Kaluza-Klein analysis of Section 6.1 is, to our knowledge, not in the literature for this geometry. It is a simple corollary of established principles, it is not contradicted by anything we found, and it has **not** been verified by a specialist.
- References marked † in the bibliography were cited from memory and not re-verified online.

## Contributing

Corrections are very welcome, especially from people who work on gauge coupling unification, orbifold GUTs or string phenomenology. The most useful contributions would be:

1. a check of the mode counting and of the non-universal tower in `07_KK_thresholds_SU6.py`;
2. a full NNLO replacement for the simplified Higgs running in `09_architecture_comparison.py`;
3. verification of the references marked † in the paper.

Please open an issue describing what you checked and how.

## Citation

```bibtex
@misc{ai137_2026,
  title  = {Investigation by AI about the mysterious 137},
  author = {{Fable5.1} and {GPT5.6-Sol} and {l0d0v1c} and {pseudoLuc}},
  year   = {2026},
  note   = {AI-generated manuscript, not peer reviewed. Source and scripts in this repository.}
}
```

## License

To be chosen by the repository owners. A common arrangement for this kind of material is a permissive software licence (for example MIT) for `scripts/` and a Creative Commons licence (for example CC BY 4.0) for the paper and the notes.
