# Payroll

The common payroll vocabulary -- the pay runs a company processes, the pay stubs they produce, the schedules they run on, and the earnings, deductions and taxes on every stub -- distilled from the APIs that already exist. Employees themselves belong to the HR context. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Payroll, Global Payroll, Employer of Record, EOR, Payroll Processing, Human Resources, HRIS, HR Tech, HCM, Workforce Management in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| pay_run | 16 | 15 | id 67% | payrolls 6, payroll 5, payroll-runs 3, payruns 2 |
| pay_stub | 18 | 15 | id 80%, gross_pay 53%, net_pay 53% | payslips 11, paystubs 4, payslip 2, payments 2 |
| pay_schedule | 4 | 3 | id 100%, name 100% | pay-groups 2, pay_schedules 1, paygroups 1 |

Cohort: 192 providers with harvested OpenAPI, 27 crosswalks. Of the providers exposing a pay_run: 56% create, 81% list, 69% fetch, 19% update, 19% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Payroll publishes little: 192 HR and payroll providers in the cohort, 27 mapped. Most payroll engines keep their API private or partner-gated.
- A pay stub agrees on gross and net pay (both core), and carries earnings, deductions and taxes as lines -- the market does not model those as resources of their own.
- Pay stubs come from two kinds of provider: payroll engines, and income-verification networks (Argyle, Pinwheel) that read stubs on a worker's behalf. Both count.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The HR tags are in the cohort: payroll products are tagged Human Resources far more often than Payroll.
- Earnings, deductions and taxes are not concepts: measured, 3, 5 and 2 providers expose them as resources. They are properties of the pay stub.
- `benefits` is not a deduction: reviewed, it is benefit enrollment, a domain of its own.
- A bare `runs` is not a pay run (CI and workflow runs); `payroll-runs`, `payruns` and `payrolls` are.
- A pay stub needs no pay run: income-verification providers expose stubs without running payroll, so `requires` was dropped for it.
- Duplicates merged: Argyle (two listings), KUFU into SmartHR (the same company, renamed), Remote, Thatch, Ethena, ADP and five Workday listings.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
