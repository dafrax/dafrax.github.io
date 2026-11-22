# Goal-Based Financial Freedom Simulator

Repository-local specification for `financial-freedom-simulator.html`.

## Product Direction

Follow the simple Financial Freedom Calculator pattern used by Parqet: one page, three clear input groups, one calculation action, and results immediately below. Do not use a long onboarding wizard.

## Input Groups

1. **Tujuan Financial Freedom**
   - Desired net monthly income.
   - Current age (optional).
   - Target age (optional).
   - Duration is derived automatically from ages; do not ask for months when both ages are available.
2. **Kondisi Keuangan**
   - Existing investment assets available for this goal.
   - Emergency fund separated from investments.
   - Monthly contribution optional and may be zero.
   - Annual bonus contribution optional.
3. **Strategi Investasi**
   - Annual return, inflation, tax, fees, withdrawal rate, and contribution timing.
   - Explain assumptions; results are not guarantees or personal investment advice.

## Results

Show separately:

- Required target capital to fund desired income.
- Projected assets from current assets, contributions, bonuses, and return.
- Gap or surplus.
- Duration in years/months.
- Whether the selected age target is achievable.
- Estimated passive income from projected assets.
- Required contribution when a target age exists.
- Annual table, asset growth visualization, milestones, and CSV export.

## Financial Model

Net annual return is gross return reduced once by tax and fees. Monthly effective return uses `(1 + netAnnual)^(1/12) - 1`. End-of-month contributions are the default. Required capital is `monthlyIncome * 12 / withdrawalRate`; inflation adjusts a today-value target until the target age. Zero return must never render `Infinity` or `NaN`. Emergency funds are not investment capital.

## Constraints

- Vanilla HTML, CSS, and JavaScript; no backend or external financial API.
- Rupiah formatting uses `Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR' })`.
- Existing tool URLs remain unchanged.
- All calculations, tables, exports, and displayed summaries use one calculation engine.
- Do not store financial input remotely or include credentials.
- Validate age ordering, empty input, zero return, and extreme values.
