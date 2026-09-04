# Scope revision and Section 6 results plan

## Scope decision implemented

The paper is now centred on formulation and operator characterization. The 2021 GNSS comparison, Lindenberg figure, AP/BE/RU/TH comparison statistics, GNSS bias discussion, three-cornered-hat analysis, and GFZ/NGL processing discussion have been removed. GNSS/profile comparison and bias attribution are reserved for the companion paper.

Sections 4 and 5 have been retained, apart from the requested polarization notation changes and two site-specific phrases made generic for consistency.

## Notation changes

- Elevation remains (E); the electric field is now $$(\mathcal E)$$.
- Transverse components are ($$\mathcal E_{\parallel}$$) and ($$\mathcal E_{\perp}$$), respectively parallel and perpendicular to the vertical propagation plane.
- The Aparicio (H,V) labels remain material responses relative to the particle-symmetry axis and are explicitly distinguished from ($$\parallel,\perp$$).
- RCP is replaced by RHCP, defined as right-hand circular polarization.
- The Jones-vector appendix uses the same ($$\parallel,\perp$$) basis.
- In the operator-uncertainty equation, $$(r,s\in\{x,q,a\}), (r<s)$$ means that each unordered pair is included once, and the factor 2 restores the symmetric covariance contribution.

## Association-file summary

`gnss_rs_association.csv` is whitespace-delimited. It contains:

- 26 target-column/radiosonde associations;
- 15 physical GRUAN site codes;
- 18 RS41-GDP.1 sounding streams;
- several sites with multiple target antennas and/or manual and automatic sounding streams.

In the formulation paper, GNSS identifiers define only the target location and antenna phase-centre height. No GNSS delay estimate is used. Network-level summaries should weight physical sites explicitly and should not treat repeated target columns or sounding streams as independent climate samples.

## Proposed Section 6 structure

### 6.1 Data set and configurations

- Inventory the 15 sites and 18 sounding streams.
- Define the hybrid RS41-GDP.1+ERA5 and ERA5-only configurations at common 2021 sounding epochs.
- State identical coefficients, gravity, target height, vertical bounds, and quadrature.
- State that ERA5 liquid and ice water are used in both configurations.
- State that no independent station barometer is available: this evaluates profile-pressure mode, not strict surface-pressure decoupling.

### 6.2 Statistics and figures

For each term and configuration, report:

- valid sample count and missing fraction;
- mean and standard deviation;
- median, q05, and q95;
- source fractions and quality-flag frequencies;
- for condensate, non-zero occurrence frequency and conditional q05/median/q95.

Terms:

$$
\left[ Z_{0,h},\; Z_{0,d^\star},\; Z_{0,w^\star},\; Z_{0,c^\star},\; Z_{\mathrm{NL}},\; \mathrm{ZTD},\; \mathrm{IWV},\; T_m,\; \left\langle g^{-1}\right\rangle_p \right].
$$


At common epochs, also report

$$
\Delta Z_k=Z_k^{\mathrm{RS+ERA5}}-Z_k^{\mathrm{ERA5}}.
$$

These are operator-sensitivity differences, not validation residuals, because ERA5 completion and condensate are shared.

Recommended displays:

1. Per-site statistics and source/quality summary.
2. Multi-panel 2021 time series for representative polar, midlatitude, maritime, and tropical sites. Plot the dominant ($$Z_{0,h}$$)/ZTD separately from the small residual terms.
3. All-site forest plot or matrix of median and q05--q95 for each ($$\Delta Z_k$$).
4. Full association-level tables and time series in the Supplement.

### 6.3 Discussion questions

1. Does the partition close numerically at every site and epoch?
2. How does the hierarchy of terms change with climate, IWV, and ($$T_m$$)?
3. Which terms dominate RS41+ERA5 versus ERA5-only differences?
4. How intermittent are condensate effects, and how does ($$Z_{\mathrm{NL}}$$) scale with refractivity and humidity?
5. Are outliers linked to source fractions, gaps, upper-tail use, condensate, or surface-pressure differences?

## Numerical material requested for the next review

The most efficient input would contain one row per target association and sounding epoch, with at least:

- timestamp, physical site code, RS stream, target ID, target height;
- operator configuration (`RS+ERA5` or `ERA5-only`);
- every ZTD partition term listed above, ZTD, IWV, and (T_m);
- surface pressure and its source, inverse weighted mean gravity;
- lower/sonde/gap/top source fractions;
- condensate occurrence or liquid/ice columns;
- quality flags and numerical closure residuals;
- propagated per-term uncertainties, if already available.

With those data, the next revision can populate the tables, select representative time series objectively, and update the abstract, discussion, and conclusions without introducing any GNSS comparison.
