# Dual Anchor Model (DAM) Valuation

A closed-form valuation screen for high-growth firms. The full note is [Dual_Anchor_Model.pdf](Dual_Anchor_Model.pdf). Source is [Dual_Anchor_Model.tex](Dual_Anchor_Model.tex).

Foy Savas, CFA · October 2026 · [foy@sav.as](mailto:foy@sav.as)

## Summary

Standard models value growth only after it becomes free cash flow earned above the cost of capital. Markets often price high-growth firms well before that, including when current net income is low or negative.

The Dual Anchor Model makes that logic explicit as a two-term heuristic. It capitalizes next-period net income and adds a revenue-growth term. An endogenous decay rate on growth, \(\delta(g) = \alpha g\), damps the premium. At the reference case \(\alpha = 1\), decay exactly offsets growth in the denominator:

\[
V_0 = \frac{\mathrm{NI}_1}{r} + \mathrm{Rev}_1 \cdot \frac{g}{r}
\]

The first term is the earnings anchor. The second is the revenue anchor, a multiple of \(g/r\). Negative growth is treated as zero, so contracting revenue never adds a growth premium. The value stays finite even when reported growth exceeds the discount rate.

The formula is a screen, not a discounted-cash-flow model. It does not forecast margins, reinvestment, or the fade of excess returns. Raising \(\alpha\) above 1 makes the screen more conservative.

## Backtest

The note applies \(\alpha = 1\) to Amazon, Tesla, Zoom, Peloton, Shopify, Netflix, and Meta. The discount rate \(r\) is year- and industry-specific: the contemporaneous 10-year Treasury yield plus an industry beta times that year’s implied equity risk premium (Damodaran). Figures are approximate and meant to show direction, not precision.

For durable compounders such as Amazon, model value is typically about 0.75–1.15 times contemporaneous market capitalization. On the clearest bubble episodes—Tesla 2020–21, Zoom 2020, Peloton 2020–21, and Shopify 2020–21—the model sits around 0.30–0.45 times peak prices. Later collapses often brought prices closer to, or below, the model value. The formula never produces infinite values.

## How it differs from PEG and Gordon growth

The DAM ratio is model value divided by market capitalization. A ratio near 1 means the price is roughly consistent with the two-anchor heuristic.

PEG divides a price-to-earnings multiple by a growth rate and is undefined when earnings are non-positive. DAM stays defined in that case, discounts growth at \(r\), and scales the growth term with the revenue base.

The Gordon growth model capitalizes one growing cash-flow stream and is undefined when growth is at least the discount rate, or when the cash-flow numerator is non-positive. DAM separates an earnings perpetuity from a revenue-growth term and remains defined in both cases, at the cost of ignoring the capital required to grow.

## Limitations

Net income includes non-cash items and one-time charges. Revenue growth is noisy and often mean-reverts faster than the formula assumes. The pure revenue term ignores both the capital required to grow and the chance that growth destroys value. Use the model as a sanity check beside multi-stage free-cash-flow or residual-income analysis, not as a standalone valuation.
