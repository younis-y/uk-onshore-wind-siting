# Where should onshore wind go in Great Britain, and does it pay?

A screening-level siting assessment for GB onshore wind: hard environmental
constraints are removed first, the remaining land is scored against five weighted
criteria using the Analytic Hierarchy Process, and the surviving candidate zones
are carried into an indicative LCOE and NPV calculation.

The point of the exercise is that suitability and viability are different
questions. A site can clear every planning constraint and still not pay, and the
figures are laid out so the two screens can be read against each other.

## The weighting, and its consistency check

AHP is only as good as the consistency of the pairwise comparisons behind it, so
the consistency ratio is reported rather than assumed:

| Criterion | Weight |
|---|---|
| Wind resource | 41.3% |
| Distance to grid | 25.7% |
| Slope | 15.4% |
| Settlement proximity | 8.8% |
| Land cover suitability | 8.8% |

λ<sub>max</sub> = 5.0364, CI = 0.0091, RI (n=5) = 1.12, **CR = 0.0081**, which is
comfortably inside the conventional 0.10 threshold. Had it exceeded 0.10 the
comparison matrix would need revising before the weights meant anything.

Wind resource and grid distance together carry two thirds of the weight. That is
a deliberate judgement, not a derived result — AHP formalises a preference
structure, it does not discover one.

## Figures

| | |
|---|---|
| `Figure1_2_Wind_Terrain_Combined.png` | Seasonal wind resource and terrain |
| `Figure3_Environmental_Constraints.png` | Ramsar, SAC and SPA designations, with overlap made explicit |
| `Figure4_Onshore_Wind_Pipeline.png` | Operational and consented capacity from the REPD |
| `Figure5a_AHP_Complete.png` | Comparison matrix, weights and consistency check |
| `Figure5c_6_Suitability_Candidates_Combined.png` | Composite suitability surface and candidate zones |
| `Figure7_Financial_Viability.png` | Indicative LCOE and NPV under neutral scenario labels |

## Running it

```bash
pip install geopandas rasterio xarray shapely pandas numpy matplotlib
jupyter lab wind_siting_screening.ipynb
```

The notebook expects the data files listed in [`data/README.md`](data/README.md)
in the working directory. They are not committed — see that file for why, and for
where each one comes from. All spatial layers are reprojected to EPSG:27700
(British National Grid) before any overlay.

## Scope

- **Screening-level, not site-level.** The output identifies zones worth
  investigating, not turbine positions. No wake modelling, no noise or shadow
  flicker assessment, no grid connection study, no landscape or visual impact
  appraisal, and no consultation with anybody who lives there.
- **The financial layer is indicative.** Capex, opex, capacity factor and
  discount rate are single point estimates carried through without a sensitivity
  analysis, so the LCOE and NPV figures show the shape of the answer rather than
  a number to bank.
- **The AHP weights are one analyst's judgement.** The consistency ratio shows
  the comparisons do not contradict each other; it says nothing about whether
  they are the right comparisons.
- **Constraint coverage is partial.** Designated conservation sites, terrain and
  settlement proximity are screened. Aviation and radar safeguarding, MOD
  danger areas, TPO woodland and peat depth are not.
- Produced for MSc coursework at UCL, and released because the method is
  reusable rather than because the siting conclusions are authoritative.

## Licence

Code and figures MIT, see [LICENSE](LICENSE). The input datasets are third-party
and carry their own terms, recorded in [`data/README.md`](data/README.md).
