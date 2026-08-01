# Business Problem

## Context

Property risk analytics platforms in the P&C insurance space increasingly let a
property's risk score reflect verified real-world mitigation — a roof upgrade,
added defensible space, a structural retrofit — rather than treating risk as
static. This kind of score often supports regulatory rate filings, which means
any claim that "mitigation reduces risk" behind it has to be statistically
defensible, not just directionally true.

## The analytical problem

Mitigation adoption is not randomized. A homeowner or carrier chooses to upgrade
a roof or clear defensible space — which means mitigated and non-mitigated
properties likely differ systematically before any mitigation happens at all
(owner wealth, construction age, regional building codes, carrier
risk-awareness). A naive before/after or treated-vs-untreated comparison will
conflate the effect of the mitigation with the effect of who tends to adopt it.

**This project's core question:**
Does a mitigation action produce a measurable, causally defensible reduction in
risk exposure — and what pipeline and methodology would be needed to answer that
repeatably as new mitigation data comes in across regions and perils?

## Data approach

Real claims and imagery data for this domain are typically proprietary. This
project simulates a property-level panel dataset with two properties that make
it useful as a real test of method, not just a toy:

1. **Non-random treatment assignment** — simulated mitigation adoption is
   correlated with observable property/regional characteristics, mirroring real
   self-selection.
2. **A known ground-truth effect** — the simulation embeds a true effect size,
   so the estimation method can be validated against a known answer rather than
   trusted blindly.

## Method

- Difference-in-differences as the primary estimator, with an explicit
  parallel-trends check (not just an assumption stated in passing)
- A pipeline (ingestion → dbt staging/marts → tests) built to reflect how this
  kind of analysis would actually sit on top of a production data product,
  including a monitoring layer so a stale or incomplete input dataset would be
  caught before it silently biased the analysis
- A short stakeholder memo as the final deliverable, since a number without
  communicated uncertainty isn't useful to a non-technical decision-maker