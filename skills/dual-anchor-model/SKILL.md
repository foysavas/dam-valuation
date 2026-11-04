---
name: dual-anchor-model
description: >-
  Applies the Dual Anchor Model (DAM), a closed-form valuation screen that
  capitalizes next-period net income and adds a damped revenue-growth term.
  Use when the user asks to value a high-growth or currently unprofitable
  firm, apply DAM or the dual anchor model, compute a DAM ratio against
  market cap, or sanity-check a growth valuation relative to PEG or the
  Gordon growth model.
---

# Dual Anchor Model

Heuristic screen from Savas, *Dual Anchor Model (DAM) Valuation* (October 2026). Not a discounted-cash-flow model and not a buy or sell recommendation. Full note: [Dual_Anchor_Model.pdf](../../Dual_Anchor_Model.pdf). The growth rate to use is specified in [Choosing_the_Growth_Rate.pdf](../../Choosing_the_Growth_Rate.pdf).

## Formula

Inputs are forward, next-period figures. \(g\) and \(r\) are decimals.

\[
V_0 = \frac{\mathrm{NI}_1}{r} + \mathrm{Rev}_1 \cdot \frac{g}{r + (\alpha - 1) g}
\]

- Earnings anchor: \(\mathrm{NI}_1 / r\). At \(g = 0\) the model is only this term.
- Revenue anchor: the second term. At the reference case \(\alpha = 1\) it simplifies to \(\mathrm{Rev}_1 \cdot g / r\).
- If \(g < 0\), set \(g = 0\) in the revenue anchor only. Contracting revenue never adds a growth premium. Keep a negative earnings anchor.
- Default \(\alpha = 1\). Use a higher \(\alpha\) only when the user asks for a more conservative screen. For \(\alpha < 1\), compute only if \(r + (\alpha - 1) g > 0\); otherwise stop and say the denominator is not positive.
- \(r\) must be positive.

\(V_0\) is in the same currency unit as net income and revenue.

DAM ratio, when market capitalization is known:

\[
\text{DAM ratio} = V_0 / \text{market cap}
\]

A ratio near 1 means the price is roughly consistent with this heuristic. It is not a cheap or expensive signal.

## Growth rate

\(g\) is revenue growth at the moment: expected growth of the annual revenue base over the coming year. The decay term already fades growth. Do not substitute a perpetual rate, a terminal rate, a multi-year historical compound rate, or a long-term target above current growth.

When sources grow at different rates, build \(g\) from those sources instead of using one consolidated figure:

\[
g = \sum_i \frac{\mathrm{Rev}_{1,i}}{\mathrm{Rev}_1}\, g_i
\]

Each \(g_i\) is that source's own coming-year growth. Weights use revenue in the current base. A source that is not yet in the base gets no weight. Keep negative source rates so they reduce the blend, then if blended \(g < 0\) set the revenue anchor's \(g\) to 0.

Use guidance for the coming year when it is a revenue outlook. Use the latest year-over-year rate only when it still describes the present mix. State which construction was used. \(\mathrm{Rev}_1\) is the annual base this \(g\) applies to. The companion note is the authority for this section.

## Procedure

1. Collect \(\mathrm{NI}_1\), \(\mathrm{Rev}_1\), \(g\), \(r\), market cap, and \(\alpha\) if the user set it. Record the source, date, and currency unit of each figure.
2. Do not invent missing figures. Ask for them, or label each substitute as an assumption and keep going only if the user asked for a worked example.
3. Set \(g\) from the growth-rate section. Prefer a revenue-source buildup when sources differ. Otherwise use growth at the moment. If only a trailing rate is available, say so and label \(V_0\) as using a trailing proxy.
4. Convert percents to decimals before substituting. State the conversion.
5. If the user does not give \(r\), construct \(r =\) current 10-year Treasury yield \(+\) equity beta \(\times\) equity risk premium. Cite each component. If a component is an assumption, say so. Industry beta plus the implied equity risk premium is the construction used in the note.
6. Substitute. Show earnings anchor, revenue anchor, \(V_0\), and DAM ratio as separate lines with the arithmetic visible.
7. Interpret in a few sentences. State the limitations below. Do not call \(V_0\) intrinsic value or fair value.

## Output

```markdown
## Dual Anchor Model screen — [company]

**Inputs** (forward, [unit], [as-of date])
- NI_1: … ([source])
- Rev_1: … ([source])
- g: … ([growth at the moment, or source buildup with the weights])
- r: … ([components and sources])
- alpha: 1
- Market cap: … ([source]), or omitted

**Result**
- Earnings anchor = NI_1 / r = …
- Revenue anchor = Rev_1 · g / (r + (alpha − 1) g) = …
- V_0 = …
- DAM ratio = V_0 / market cap = …

**Reading**
[Whether the price sits near, above, or below the screen. Heuristic only.]

**Caveats**
The revenue term ignores reinvestment and the chance that growth destroys value. Net income includes non-cash and one-time items. Growth rates are noisy. This is a screen beside a full cash-flow model, not a standalone valuation.
```

## Check

\(\mathrm{NI}_1 = 2\), \(\mathrm{Rev}_1 = 50\), \(g = 0.20\), \(r = 0.10\), \(\alpha = 1\), market cap \(= 150\) (same currency unit):

- Earnings anchor \(= 2 / 0.10 = 20\)
- Revenue anchor \(= 50 \times 0.20 / 0.10 = 100\)
- \(V_0 = 120\)
- DAM ratio \(= 120 / 150 = 0.80\)

Same inputs with \(\mathrm{NI}_1 = -1\) and \(g = 0.40\): earnings anchor \(= -10\), revenue anchor \(= 80\), \(V_0 = 70\).

Same inputs with \(g = -0.05\): revenue anchor \(= 0\), \(V_0 = \mathrm{NI}_1 / r\).

## Boundaries

- Stays finite when \(g \ge r\). The Gordon growth model is undefined there. Say that only if the user invokes Gordon or perpetual growth.
- Stays defined when net income is negative or near zero, unlike PEG. Say that only if the user invokes PEG or the earnings multiple.
- In the note's backtest, durable compounders often landed near 0.75–1.15 times market cap, and the clearest bubble peaks near 0.30–0.45. Those ranges describe that sample. Do not use them as decision thresholds.
- Do not forecast margins, reinvestment, or fade inside this screen. If the user wants that, do a separate cash-flow or residual-income analysis and keep it distinct from \(V_0\).
