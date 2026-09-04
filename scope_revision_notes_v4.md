# Revision 4 scope and numerical-results request

## Scope retained in the formulation paper

The paper remains centred on the formulation and profile-based characterization of the
hydrostatically constrained Aparicio (AP) ZTD and IWV operators. Comparison with GNSS-estimated
delays, GNSS bias attribution, processing-centre differences, and three-cornered-hat analysis
remain reserved for the companion paper.

The following profile-based comparisons are retained in the present paper:

1. AP ZTD partition terms from RS41-GDP.1+ERA5 and matched ERA5-only columns.
2. AP gas refractivity versus Bevis 1994 (BE94), Thayer 1974 (TH74), Rüeger 2002 (RU02), and
   Smith--Weintraub 1953 (SW53), using identical atmospheric states and integration settings.
3. Strict AP surface-pressure decoupling using a ground-check reference-barometer measurement
   when an eligible independent value is archived in the RS41-GDP.1 NetCDF file. Such a value
   is known to be present for at least Lindenberg.

Sections 4 and 5 remain substantively unchanged. The previously requested notation is retained:
elevation is $$\(E\)$$, the electric field is $$\(\boldsymbol{\mathcal E}\)$$, its transverse components
are $$\(\mathcal E_{\parallel}\)$$ and $$\(\mathcal E_{\perp}\)$$, and RHCP denotes right-hand circular
polarization.

## Association inventory

`gnss_rs_association.csv` is whitespace-delimited and contains:

- 26 target-column/radiosonde associations;
- 15 physical GRUAN site codes;
- 18 RS41-GDP.1 sounding streams;
- several sites with multiple target antennas and/or manual and automatic sounding streams.

The GNSS identifiers define only the target location and antenna phase-centre height. No GNSS
delay estimate is used. Network summaries must not treat repeated target columns or sounding
streams at one physical site as independent climate samples.

## Revised Section 6 structure

### 6.1 Data set and operator configurations

- Inventory the 15 sites and 18 sounding streams.
- Evaluate the hybrid RS41-GDP.1+ERA5 and ERA5-only configurations at common 2021 epochs.
- Use identical coefficients, composition, gravity, target height, vertical bounds, gap rules,
  upper-tail treatment, and quadrature.
- Use ERA5 liquid- and ice-water contents in both AP configurations and retain their source.
- Screen every NetCDF file for a ground-check pressure value and the metadata needed to decide
  whether it is an independent surface-pressure observation.

### 6.2 ZTD-partition statistics

For each term and configuration, report:

- valid sample count and missing fraction;
- mean and standard deviation;
- median, q05, and q95;
- source fractions and quality-flag frequencies;
- for condensate, non-zero occurrence frequency and conditional q05/median/q95.

Terms:

$$
Z_{0,h},\;Z_{0,d^\star},\;Z_{0,w^\star},\;Z_{0,c^\star},\;
Z_{\mathrm{NL}},\;\mathrm{ZTD},\;\mathrm{IWV},\;T_m,
\;\langle g^{-1}\rangle_p.
$$

At common epochs, also report

$$
\Delta Z_k=Z_k^{\mathrm{RS+ERA5}}-Z_k^{\mathrm{ERA5}}.
$$

These are operator-sensitivity differences, not independent validation residuals, because
ERA5 completion and condensate are shared.

### 6.3 Refractivity-model comparison

Compute the following on each identical completed profile:

- AP gas delay, including its gas-only nonlinear correction;
- AP linear gas delay, excluding the nonlinear correction;
- SW53, BE94, TH74, and RU02 gas delays;
- optionally, the original TH74 expression with published dry/wet compressibility factors.

Use Rüeger's `best average` coefficient set for RU02, matching the existing implementation.

Use the explicit common convention $$\(e=e(T,\mathrm{RH},p)\)$$ from the selected humidity
conversion and $$\(p_d=p-e\)$$. Set condensate to zero for the gas-formulation comparison. If full
all-water delays are also shown, add the same AP condensate contribution to every formulation
and label it as a common augmentation.

For each classical model $$\(m\)$$, report

$$
\delta Z_{\mathrm{AP}-m}=Z_g^{\mathrm{AP}}-Z_g^m,
\qquad
\delta Z_{0,\mathrm{AP}-m}=
\delta Z_{\mathrm{AP}-m}-Z_{\mathrm{NL},g}^{\mathrm{AP}}.
$$

The second quantity separates the linear-formulation difference from the AP nonlinear term.
For each difference, provide count, mean, standard deviation, median, q05, and q95 by physical
site and for both RS41+ERA5 and ERA5-only states.

The existing MATLAB output labelled TH uses Thayer's coefficient set with unity component
compressibility factors. It should be labelled `TH74_u` in the analysis. If the original
Thayer compressibility factors are implemented, label that separate sensitivity `TH74_Z` and
report `TH74_Z - TH74_u`; do not silently replace the legacy series.

The supplied MATLAB version already computes BE94, TH74_u, and RU02. It does not yet compute
SW53, so an SW53 profile and column-output branch must be added before generating these results.

Computing the model comparison at all 15 sites is preferred because the differences depend on
pressure, temperature, and humidity. The main paper can show a compact all-site summary and
time series for a few representative climates. If only a restricted analysis is feasible,
use Lindenberg plus at least one cold/dry and one warm/humid site selected before inspecting
the results.

### 6.4 Strict-pressure experiment using ground-check measurements

For every candidate ground-check value, provide:

- NetCDF filename and sounding timestamp;
- exact variable or attribute name, dimensions, units, fill value, and flags;
- reference-barometer make/model or sensor identifier;
- measurement time and reference height;
- standard uncertainty and calibration/traceability information, when available;
- whether and how the value enters RS41 processing or `press_gnss`;
- launch-site and target antenna heights and the horizontal separation.

An observation is eligible for the strict experiment only if it is a reference pressure
independent of `press_gnss`, with usable time and height metadata. Transfer it to the target
height using the same humid-air density and gravity convention as the AP operator. Archive

$$
p_{\mathrm{gc}},\quad p_{\mathrm{gc}\rightarrow0},\quad
p_{0,\mathrm{prof}},\quad
\Delta p_{\mathrm{gc}}=p_{\mathrm{gc}\rightarrow0}-p_{0,\mathrm{prof}},
$$

and

$$
\Delta Z_{p_0}=10^{-6}q_{1r}\langle g^{-1}\rangle_p\Delta p_{\mathrm{gc}},
\qquad
\mathrm{ZTD}_{\mathrm{AP}}^{\mathrm{strict}}
=\mathrm{ZTD}_{\mathrm{AP}}^{\mathrm{prof}}+\Delta Z_{p_0}.
$$

Report availability, mean, standard deviation, median, q05, and q95 of
$$\(\Delta p_{\mathrm{gc}}\)$$ and $$\(\Delta Z_{p_0}\)$$, together with their propagated uncertainty.
If only Lindenberg has adequate 2021 coverage, present it as a clearly identified case study.
This tests the effect and feasibility of strict decoupling; without an independent delay
reference it does not prove that the corrected ZTD is more accurate.

### 6.5 Discussion questions

1. Does the AP partition close numerically at every site and epoch?
2. How does the hierarchy of AP terms change with climate, IWV, and $$\(T_m\)$$?
3. Which terms dominate RS41+ERA5 versus ERA5-only differences?
4. How do the sign, magnitude, variability, and climate dependence of AP--SW53, AP--BE94,
   AP--TH74, and AP--RU02 differ?
5. How much of each AP--classical difference is explained by the AP nonlinear term, and what
   is the impact of the TH74 compressibility convention?
6. For eligible files, what are the magnitude, variability, and uncertainty of the strict
   ground-check pressure correction?
7. How intermittent are condensate effects, and how does $$\(Z_{\mathrm{NL}}\)$$ scale with
   refractivity and humidity?
8. Are outliers linked to source fractions, gaps, upper-tail use, condensate, surface-pressure
   differences, or ground-check metadata?

## Numerical material requested for the next review

The preferred input has one row per target association and sounding epoch, containing:

- timestamp, physical site code, sounding stream, target ID, and target height;
- operator configuration (`RS+ERA5` or `ERA5-only`);
- all AP partition terms, AP ZTD, IWV, and $$\(T_m\)$$;
- surface pressure and source, inverse weighted mean gravity;
- lower/sonde/gap/top source fractions;
- condensate occurrence and liquid/ice columns;
- numerical closure residuals and quality flags;
- SW53, BE94, TH74_u, RU02, and optional TH74_Z gas delays;
- AP gas-linear and gas-nonlinear delays and every AP-minus-classical difference;
- all ground-check variables and metadata listed in Sect. 6.4;
- propagated per-term uncertainties, when available.

Separate small summary files are also acceptable if they include, for every physical site and
configuration, count, mean, standard deviation, median, q05, and q95 for all requested terms
and differences. Per-epoch output remains necessary for selecting time series, checking
seasonality, screening barometer values, and diagnosing outliers.

With these data, the next revision can populate the tables and figures, select representative
time series objectively, and update the abstract, discussion, and conclusions without
introducing the GNSS-delay comparison reserved for the companion paper.
