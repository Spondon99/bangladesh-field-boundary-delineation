| ID | Setup | Pretrain | Fine-tune | Test on | Purpose |
|---|---|---|---|---|---|
| **A** | Proxy transfer | Germany (or other) | India + Vietnam | Bangladesh (held-out digitized chips) | Does proxy fine-tuning help on an unseen country? |
| **A1** | Proxy ablation | Germany | India only, Vietnam only, or both | Bangladesh | Which proxy transfers best? |
| **B** | Proxy in-domain check | Germany | India + Vietnam | Held-out India and Vietnam test chips, spatially separate from fine-tuning chips | Measures how well fine-tuning works on the proxies themselves |
| **C** | Zero-shot | Germany | None | Bangladesh, India, Vietnam | The starting gap, and the only clean zero-shot test on India and Vietnam |
| **D** | Off-the-shelf baselines | FTW checkpoint, or PRUE global predictions | None | Bangladesh | Existing models to beat. India and Vietnam were in their training, so don't report those as unseen |
| **E** | Label-budget curve (core question) | Germany | Bangladesh polygons at 0 / 50 / 100 / 200 | Held-out Bangladesh chips | How little local data closes the gap? |
| **F** | From-scratch control | None | Bangladesh polygons at the same budgets | Held-out Bangladesh chips | Shows whether pretraining actually helps |
| **G** | In-domain ceilings | None | Train on India or Vietnam (FTW official splits) | Same-country test split | Upper bound for the "% gap closed" formula |
| **H** *(optional)* | Source diversity | Germany only, multi-country, or Asia-only (e.g., Cambodia) | Same as A | Bangladesh | Does source similarity matter? |

**Rules that apply to every setup**
- Use identical test chips and identical metrics (pixel IoU, object precision/recall at IoU ≥ 0.5) across all setups.
- Use FTW's input spec for the Bangladesh chips (4 bands, 2 seasonal windows).
- Keep Bangladesh fine-tuning and evaluation chips spatially separated, and digitize every field in each evaluation chip.
- Run multiple seeds and random label subsets for E and F, and report mean ± spread.
- Gap closed = (fine-tuned IoU − zero-shot IoU) / (ceiling IoU − zero-shot IoU), with zero-shot from C and the ceiling from G.