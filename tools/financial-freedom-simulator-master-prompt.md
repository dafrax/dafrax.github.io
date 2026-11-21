# Goal-Based Financial Freedom Simulator — Master Specification

This file is the repository-local implementation specification for the Goal-Based Financial Freedom Simulator. The simulator is a standalone vanilla HTML application at `./financial-freedom-simulator.html`, integrated into the tools catalog without changing existing tool URLs.

## Product Goal

Start from the user's life goal, not a forced contribution amount. The simulator must answer: “Saya ingin pendapatan pasif X per bulan pada waktu Y; dengan kondisi sekarang, setoran, return, inflasi, dan biaya yang saya masukkan, strategi apa yang diperlukan dan kapan goal tercapai?” All nominal inputs are free-form.

## Scope

- Goal-first wizard: target passive income, today's/future value basis, expenses, coverage, target years/age.
- Current finances: investment capital, emergency fund separated from investment capital, monthly contribution, annual increase, lump sum, recurring, and single-cycle contribution.
- Assumptions: gross return, tax, fees, inflation, effective or nominal monthly conversion, withdrawal rate, and safety margin.
- Shared pure calculation engine for forward and reverse projections.
- Target capital, target contribution, target time, target passive income, and financial-freedom milestones.
- Single-cycle, monthly recurring, increasing contribution, lump sum, and custom-ready engine model.
- Monthly transaction order: opening balance → return → fees/tax-adjusted net result → end-of-month contribution → withdrawals → closing balance.
- Nominal and real values; inflation adjustment uses `(1 + nominal) / (1 + inflation) - 1`.
- Scenario comparison: conservative 3%, careful 4%, moderate 5%, and editable user assumption.
- Milestones: 25%, 50%, 75%, and 100% of the target income/capital goal.
- Dashboard KPIs, asset-growth bars, scenario table, milestones, annual projection table, monthly CSV export, and annual CSV export.
- Indonesian default UI, responsive layout, accessible labels, validation, and financial disclaimer.

## Financial Rules

- Default gross return: 7.5% annual.
- Default tax: 20% of gross return.
- Default net nominal return: 6% before fees.
- Effective monthly conversion: `(1 + netAnnual)^(1/12) - 1`.
- Alternative nominal monthly conversion: `netAnnual / 12`.
- Required capital: `targetMonthlyIncome * 12 / annualNetReturn`.
- Safety margin multiplies required capital by `1 + margin`.
- Return 0% must never produce `Infinity` or `NaN`.
- Emergency fund is not automatically investment capital.
- Results are simulations, not investment advice or guaranteed returns.

## Acceptance Criteria

- Goal inputs accept arbitrary valid Rupiah values and do not force Rp10 million.
- Single-cycle stops contributions after its selected month; recurring continues.
- End-of-month contribution does not earn same-month return.
- Tax and fees are applied once and transparently.
- Reinvestment and inflation calculations use the same engine as dashboard tables.
- Reverse calculations handle zero return, already-reached targets, impossible targets, and bounded iteration.
- Current tools `PocketPilot.html` and `financial-freedom-calc.html` remain unchanged and their URLs remain valid.
- No sensitive user financial data is sent to external APIs or stored automatically.
- HTML and JavaScript are valid without a build process or external dependency.

## Testing Requirements

The engine must cover zero balances, zero return, 31-month single cycle, recurring contributions beyond month 31, end-of-month timing, lump sum compounding, inflation adjustment, reverse contribution, already-reached goals, invalid/negative/extreme values, and consistent annual aggregation. Verify with the repository's available HTML/JavaScript checks and a Node regression harness.

## Security and Privacy

The simulator runs locally in the browser. It must not contain credentials, API keys, or private data. It must clearly state that projections are assumptions and not guarantees. GitHub Pages is public hosting; this tool must not be presented as a private financial-data service.
