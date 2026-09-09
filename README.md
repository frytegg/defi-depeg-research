# DeFi Peg Failure & Tracking Error — Research Portfolio

**Alexandre Lemière** — [LinkedIn](https://linkedin.com/in/alexandre-lemiere) · [Portfolio site](https://frytegg.github.io/defi-depeg-research/)

Sixteen weeks of applied research (May–August 2026) into how and why DeFi synthetic
assets — stablecoins, synthetic equities, liquid-staking tokens, delta-neutral dollars
— lose their peg, and what that implies for designing a new protocol. Conducted during
a research internship at [Derivalink](#scope--confidentiality) (placement via Acensi,
ESILV engineering programme). Twenty sub-reports, each a self-contained audited
data pipeline plus econometric/ML/graph-theoretic analysis, sit under one umbrella
report and one evaluation standard.

**Start here → [Internship Report (PDF, 71pp, EN)](reports/internship_report/Internship_Report_Alexandre_Lemiere.pdf)**
— the synthesis: methodology, four research questions and their verdicts, an
internally-audited result that was found wanting and retracted, and what the findings
imply for a production protocol design.

All quantitative results below are computed from **public on-chain data, public
exchange data, and code written during the internship** — no proprietary data or
internal specification content is reproduced here (see [Scope](#scope--confidentiality)).

---

## Sub-reports, by peg mechanism

Each report is a full data audit → tracking-error decomposition → findings writeup,
with figures and references. FR = French edition, where one exists.

### Full collateral (CDP-backed)

| Report | Headline finding | Read |
|---|---|---|
| **MakerDAO — DAI** | Survived the March 2020 liquidation cascade *and* the March 2023 SVB contagion; during SVB the push oracle floored at $0.88 while the market traded to $0.810 — a 697bp gap invisible to a single-oracle circuit breaker. | [PDF](reports/maker/dai/main.pdf) |
| **Liquity — LUSD** | Structurally premium-biased peg; the $1 redemption floor binds hard, with redemption intensity 7–8× higher below par than above. | [PDF](reports/liquity/lusd/main.pdf) |
| **Curve — crvUSD** | PegKeeper-defended, slightly sub-peg by design; Egorov's insulation architecture holds up empirically — stress routes into the LLAMMA soft-liquidation mechanism, not into the peg itself. | [PDF](reports/curve/crvusd/main.pdf) |

### Partial / algorithmic collateral

| Report | Headline finding | Read |
|---|---|---|
| **Iron Finance — IRON/TITAN** | Full forensic reconstruction of the June 2021 collapse: TITAN's supply inflated ~335,000× in about 24 hours; only 1 of 8 pre-registered early-warning signals carried real information. | [PDF](reports/iron_finance/iron/main.pdf) |
| **FRAX — V1** | The survivor half of the Iron Finance comparison: near-identical contract logic, but FRAX *raised* its collateral ratio +8pp under stress while Iron *let it fall* −25.7pp — and only one of the two protocols is still alive. | [PDF](reports/frax/v1/main.pdf) |
| **Terra — UST** | Full reconstruction of the May 2022 collapse of the (then) third-largest stablecoin; a DebtRank systemic-risk replay overshoots the real loss by 1.3× because the model has no mechanism for the Luna Foundation Guard's reserve defense. | [PDF](reports/terra/ust/main.pdf) · [FR](reports/terra/ust/main_fr.pdf) |
| **Mirror Protocol** | 34 synthetic assets (mAssets) on Terra; the Band oracle freeze that silently broke tracking is empirically dated, and tracking error is shown to be undefined after the 2022-06-01 freeze — not zero, undefined. | [PDF](reports/terra/mirror/main.pdf) · [FR](reports/terra/mirror/main_fr.pdf) |

### Shared debt pool (Synthetix)

| Report | Headline finding | Read |
|---|---|---|
| **sUSD** | The base synth of the pool; a soft, structural sub-peg (~−0.4% baseline) turned into an acute, still-open depeg starting May 2024, with a daily-median trough of $0.593 reached February 2026. | [PDF](reports/synthetix/susd/main.pdf) · [FR](reports/synthetix/susd/main_fr.pdf) |
| **Crypto cohort** (sETH, sBTC, sLINK…) | Oracle fidelity is essentially perfect across 6 years — the apparent "depeg" investors see is DEX-venue liquidity decay setting in from 2024, not an oracle failure. | [PDF](reports/synthetix/crypto/main.pdf) · [FR](reports/synthetix/crypto/main_fr.pdf) |
| **Equity cohort** (sTSLA, sAAPL…) | One flagship offset (sGOOG) is correctly re-attributed from an assumed dividend effect to a genuine, measurable Chainlink feed low-bias. | [PDF](reports/synthetix/equity/main.pdf) · [FR](reports/synthetix/equity/main_fr.pdf) |
| **Commodity / index cohort** (sXAU, sXAG, sFTSE, sNIKKEI) | The Wezen-release redemption freeze is dated precisely via a difference-in-differences design. | [PDF](reports/synthetix/commodity_index/main.pdf) · [FR](reports/synthetix/commodity_index/main_fr.pdf) |
| **Inverse cohort** (iETH, iBTC…) | Tracking error is the *wrong lens* for this cohort — the price is a deterministic clamped formula. The real story: 1,161 clamp episodes and a 2020–2021 freeze cascade (29 events) as the bull run pinned every inverse synth to its floor. | [PDF](reports/synthetix/inverse/main.pdf) |

### Fiat-backed (centralized)

| Report | Headline finding | Read |
|---|---|---|
| **Circle — USDC** | Reference stablecoin; full forensic reconstruction of the March 2023 SVB depeg used as the calibration case for the whole corpus. | [PDF](reports/circle/usdc/main.pdf) |
| **Tether — USDT** | Peg fidelity is high in the center but sharply heavy-tailed; the real-time stress signal is the Curve 3pool weight imbalance, not the (opaque, off-chain-backed) oracle. | [PDF](reports/tether/usdt/main.pdf) |

### Liquid staking, index & delta-neutral

| Report | Headline finding | Read |
|---|---|---|
| **Lido — stETH** | Reconstructed through the June 2022 Celsius/3AC contagion; the withdrawal-queue's latency is priced — each extra day of queue costs −1.28bp of discount. | [PDF](reports/lido/steth/main.pdf) |
| **GMX — GLP** | A NAV-tracking, perpetuals-linked liquidity index; trading fees couldn't offset basket drawdown and GMX V1 wound down −99.8%. | [PDF](reports/gmx/glp/main.pdf) |
| **Ethena — USDe / sUSDe** | 2024 launch through the October 2025 Binance oracle-bug case study; a mis-measured "peg improvement" claim is corrected to a real median bias of −4.45bp. | [PDF](reports/ethena/usde/main.pdf) · [FR](reports/ethena/usde/main_fr.pdf) |
| **Resolv — USR** | The March 2026 depeg is forensically identified as an AWS-key/opsec breach (an illicit mint of ~80M unbacked USR) — explicitly **not** a failure of the delta-neutral hedge design itself. | [PDF](reports/resolv/usr/main.pdf) · [FR](reports/resolv/usr/main_fr.pdf) |
| **Vertex Protocol — perps** | Top-3 perpetual markets; tracking error measured against the perp-mid reference rather than a single spot oracle. | [PDF](reports/vertex/perps/main.pdf) · [FR](reports/vertex/perps/main_fr.pdf) |
| **Backed Finance — xStocks** | Physically-backed tokenized equities track ~9× tighter than the now-dead synthetic equivalent (0.66% vs 5.8% RMSE) — and survived where the synthetic died at a 2021 freeze event. | [PDF](reports/backed/xstocks/main.pdf) |

### Cross-cutting syntheses

| Report | Headline finding | Read |
|---|---|---|
| **Implied-volatility smirk gate (S8)** | The 25-delta BTC/ETH skew carries statistically significant *incremental* information about stress beyond a DVOL-style index — but an initial claim that it *anticipates* stress days in advance was retracted after an adversarial self-audit found the result was an artifact of a bounded search window. | [PDF](reports/s8_iv_smirk/main.pdf) · [FR](reports/s8_iv_smirk/main_fr.pdf) |
| **Systemic-risk graph theory (S9)** | A from-scratch DebtRank contagion model, validated against three real historical collapses (DAI/SVB, UST/Terra, Iron Finance) before being run at scale. The real cross-protocol on-chain dependency graph turns out to be a mostly-disconnected forest — 72 connected components across 110 nodes — which is itself a finding about how little systemic interconnection currently exists on-chain. | [PDF](reports/graphs/s9_closing_report/main.pdf) · [FR](reports/graphs/s9_closing_report/main_fr.pdf) |

---

## What ties it together

Across ~20 heterogeneous protocols and every major peg-design family, the same
evaluation discipline is applied throughout: pre-registered gates, adversarial
self-audits, negative results reported with the same confidence intervals as positive
ones, and — in one case — a headline result written up, then found wanting under
audit, then retracted. The [internship report](reports/internship_report/Internship_Report_Alexandre_Lemiere.pdf)
is the place to see how those individual findings resolve into four answered research
questions and a set of concrete, numeric design recommendations.

## Scope & confidentiality

This research was conducted at **Derivalink**, a company building on-chain synthetic-
asset infrastructure, through the placement agency **Acensi**, as part of the ESILV
engineering programme. Derivalink's own internal research specification and product
design are proprietary and are not reproduced anywhere in this repository. Every
quantitative result here is derived from public on-chain data, public exchange data,
or code written during the internship — nothing in this repository required, or came
from, privileged access to non-public information.

## License

Shared for portfolio and informational purposes. All content © Alexandre Lemière.
Feel free to read, cite, or link to any report; please ask before reposting a report
in full elsewhere.
