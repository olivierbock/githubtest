Your outline has the right scientific ingredients, but I would reorganize it around one central question:

> Can GNSS and a traceable reference observe the same IWV measurand, at the same place and time, with differences consistent with their complete uncertainty budgets?

This makes “metrological closure” the narrative thread, rather than treating Type A, Type B, refractivity and the benchmark as separate topics.

For 20–25 minutes, I recommend 15 main slides plus one conclusion slide. The proposed duration is about 23 minutes.

## Recommended slide-by-slide presentation

| #  | Slide title                                         | Time |
| -- | --------------------------------------------------- | ---- |
| 1  | Towards metrological closure                        | 0:45 |
| 2  | Why absolute IWV accuracy matters                   | 1:30 |
| 3  | Accuracy and stability: two complementary questions | 1:00 |
| 4  | What do we mean by metrological closure?            | 1:45 |
| 5  | The GNSS-IWV measurement model                      | 1:30 |
| 6  | First-order sensitivity of IWV                      | 1:30 |
| 7  | What Type A and Type B actually mean                | 1:30 |
| 8  | Type A evaluation of GNSS ZTD                       | 1:30 |
| 9  | Type B evaluation of GNSS ZTD                       | 1:30 |
| 10 | Building an independent reference ZTD               | 2:00 |
| 11 | Why the refractivity formulation matters            | 1:45 |
| 12 | Lindenberg: what the present results establish      | 2:00 |
| 13 | Closure requires covariance and representativeness  | 1:45 |
| 14 | What currently prevents closure?                    | 1:30 |
| 15 | Proposed WG3 benchmark                              | 2:00 |
| 16 | From benchmark to metrological closure              | 1:00 |

### Slide 1 — Towards metrological closure of GNSS-derived IWV measurements

Subtitle:

> From an agreement test to a traceable measurement system

Include your name, affiliations, CRIM WG3, Trabzon, 21 September 2026.

Opening sentence:

> “We often validate GNSS IWV by reporting a bias and a standard deviation. Metrological closure asks a stronger question: have we defined the same measurand, traced every input and propagated enough of the uncertainty to explain the observed difference?”

This immediately distinguishes the talk from a conventional intercomparison.

***

### Slide 2 — Why absolute IWV accuracy matters

Combine slides 2 and 3 of BO26 rather than showing them separately.

Left side: GCOS requirements, explicitly labelled as 2-sigma measurement uncertainty:

| Level        | Uncertainty | Stability           |
| ------------ | ----------- | ------------------- |
| Goal         | 0.1 kg m⁻²  | 0.1 kg m⁻² decade⁻¹ |
| Breakthrough | 0.5 kg m⁻²  | 0.2 kg m⁻² decade⁻¹ |
| Threshold    | 1.0 kg m⁻²  | 0.5 kg m⁻² decade⁻¹ |

Right side: observed signals:

* Global annual anomalies: approximately ±0.1–0.5 kg m⁻².

* Local annual anomalies: approximately ±0.5–5 kg m⁻².

* Global trend: approximately 0.4 kg m⁻² decade⁻¹.

* Local trends: approximately ±0.2–1 kg m⁻² decade⁻¹.

Add one sentence below:

> Fixed absolute requirements correspond to very different relative requirements in polar and tropical atmospheres.

The current GCOS values are confirmed in the [WMO OSCAR requirements database](https://space.oscar.wmo.int/requirements/view/817?utm_source=chatgpt.com).

Take-home message:

> Biases of a few tenths of kg m⁻² are already comparable with climate signals and GCOS targets.

***

### Slide 3 — Accuracy and stability: two complementary questions

Use a two-column layout:

| Talk 1: accuracy and closure            | Talk 2: stability and homogenization               |
| --------------------------------------- | -------------------------------------------------- |
| Is the absolute IWV value traceable?    | Are changes through time climatic or instrumental? |
| GNSS processing uncertainty             | Change-point detection and attribution             |
| ZTD-to-IWV conversion                   | Offset estimation and correction                   |
| Comparison with GRUAN/reference systems | Trend preservation                                 |

Show the institutional links:

* GRUAN TT-GNSS: absolute accuracy and reference-quality products.

* CRIM WG3: benchmarking, uncertainty quantification and guidance.

* IAG JWG C.8 / ICCC: reprocessing and homogenization for climate records.

Closing sentence:

> “Today I focus on the vertical axis—absolute consistency. The following talk addresses the temporal axis—stability.”

***

### Slide 4 — What do we mean by metrological closure?

I suggest defining this operationally, since “metrological closure” is not itself a standard GUM term.

Closure requires:

1. The same measurand:

   * IWV above the same lower boundary;

   * same antenna/reference height;

   * same water phases included;

   * compatible spatial and temporal sampling.

2. Traceable input quantities and documented processing.

3. Corrections for known systematic effects.

4. A covariance-aware uncertainty budget.

For two measurement results I1​ and I2​, define

D=I1​−I2​, u2(D)=u2(I1​)+u2(I2​)−2cov(I1​,I2​).

A compatibility statistic can then be written as

E=ku(D)∣D∣​.

Results are compatible at the selected coverage level when E≤1.

Important speaker note:

> This is not simply a “bias smaller than two standard deviations” test. The standard deviation of paired differences is not the uncertainty of either measurement, and shared ERA5 inputs make the covariance term non-zero.

This is a more rigorous replacement for the closure equation on slide 8 of BO25.

***

### Slide 5 — The GNSS-IWV measurement model

Show the conventional chain:

GNSS observations→ZTD→ZWD=ZTD−ZHD(ps​)→IWV=Π(Tm​,ki​)ZWD.

Underneath, organize the influences into three levels:

* GNSS estimation:\
  observations, orbit and clocks, antenna/radome calibration, multipath, elevation weighting, mapping functions, gradients, parameter constraints and numerical implementation.

* Hydrostatic subtraction:\
  surface pressure, pressure height transfer, gravity and station reference height.

* Wet-delay conversion:\
  Tm​, refractivity coefficients, humidity thermodynamics and auxiliary NWP fields.

Take-home message:

> IWV is not a direct GNSS observable; it is the output of a coupled measurement model.

***

### Slide 6 — First-order sensitivity of IWV

Reuse the BO25 appendix, but reduce it to three prominent numbers:

∂ZTD∂IWV​≃0.15 kgm−2mm−1, ∂ps​∂IWV​≃−0.35 kgm−2hPa−1, ∂Tm​∂ln(IWV)​≃0.37% K−1.

Examples:

* 5 mm ZTD error → approximately 0.76 kg m⁻².

* 1 hPa pressure error → approximately 0.35 kg m⁻².

* 3 K Tm​ error → approximately 1.1%, or 0.20 kg m⁻² for IWV = 18 kg m⁻².

Then state:

> Ning et al. found that ZTD contributed about 77–82% of the estimated IWV variance at their three example sites—not universally “75% of uncertainty” under every processing configuration.

Their conclusion was based on a mainly theoretical propagation with several terms treated as uncorrelated. See [Ning et al. (2016)](https://amt.copernicus.org/articles/9/79/2016/?utm_source=chatgpt.com).

***

### Slide 7 — What Type A and Type B actually mean

This is an important correction to the original outline.

GUM Type A and Type B refer to the method used to evaluate uncertainty, not to random versus systematic errors.

| Type A evaluation                                  | Type B evaluation                                         |
| -------------------------------------------------- | --------------------------------------------------------- |
| Statistical analysis of observations               | Information other than the current statistical sample     |
| Repeatability and temporal residuals               | Calibration results and specifications                    |
| Processing ensembles                               | Physical modelling and prior experiments                  |
| Inter-software or inter-analysis-centre dispersion | Antenna models, orbit accuracy, mapping-model limitations |

A systematic effect can be evaluated by Type A methods, and a varying effect can be assigned a Type B uncertainty.

Therefore, rename sections 3 and 4 from “GNSS Type A/B uncertainty” to:

* Type A evaluation of GNSS-ZTD uncertainty.

* Type B evaluation and modelling of GNSS-ZTD uncertainty.

***

### Slide 8 — Type A evaluation of GNSS ZTD

Possible evidence sources:

* Repeat solutions with perturbed processing options.

* Processing by independent software packages or analysis centres.

* Twin or closely collocated GNSS stations.

* Residual analysis by elevation, azimuth and weather regime.

* Repeated comparisons with GRUAN, microwave radiometers or VLBI.

* Before/after equipment-change experiments.

Reuse the BO26 examples:

* Mean differences between analysis centres are generally small globally.

* Individual stations can differ by more than 3 mm.

* Incorrect or missing antenna/radome models can produce 12–20 mm discontinuities.

Connect with the previous agenda contribution:

> “Katarzyna’s processing-option experiments provide precisely the kind of ensemble needed for a Type A evaluation—but the resulting dispersion must be interpreted within a defined population of processing choices.”

Conclude:

> Type A studies estimate repeatability and processing sensitivity; they do not, by themselves, establish absolute accuracy.

***

### Slide 9 — Type B evaluation of GNSS ZTD

Use an “error-pathway” diagram rather than a long list:

* Satellite orbit and clock products.

* Receiver and satellite antenna phase-centre calibrations.

* Radomes and multipath.

* Tropospheric mapping functions and horizontal gradients.

* Elevation-dependent observation weighting.

* Correlation between ZTD, station height, clock and gradients.

* Slant asymmetry, bending and atmospheric representativeness.

* Numerical precision and software implementation.

Distinguish:

* Correctable effects: wrong antenna model, metadata error, known barometer height.

* Residual uncertainty after correction.

* Structural model discrepancy: effects not represented by the retrieval model.

The last category should not be hidden inside an inflated “formal ZTD uncertainty.”

***

### Slide 10 — Building an independent reference ZTD

Introduce the BOAP26 operator:

ZTD=Z0,h​+Z0,d⋆​+Z0,w⋆​+Z0,c⋆​+ZNL​.

Explain each term briefly:

* Z0,h​: dominant total-mass term constrained by pressure at antenna height.

* Z0,d⋆​: residual dry-composition and temperature term.

* Z0,w⋆​: water-vapour residual, directly related to IWV and Tm​.

* Z0,c⋆​: condensate correction.

* ZNL​: nonlinear refractivity correction.

Use the synthetic example:

| Term   | Delay      |
| ------ | ---------- |
| Z0,h​  | 2304.47 mm |
| Z0,d⋆​ | 0.10 mm    |
| Z0,w⋆​ | 127.86 mm  |
| Z0,c⋆​ | 0.00 mm    |
| ZNL​   | 0.07 mm    |
| Total  | 2432.50 mm |

This corresponds to IWV = 20.0 kg m⁻².

Key point:

> More than 94% of ZTD is replaced by one pressure-constrained mass term, leaving much smaller profile-dependent residuals.

The underlying refractivity formulation is described by [Aparicio (2026)](https://amt.copernicus.org/articles/19/5135/2026/?utm_source=chatgpt.com).

***

### Slide 11 — Why the refractivity formulation matters

Use Lindenberg results only, as you proposed, and label them “gas-delay sensitivity on identical atmospheric profiles.”

For the hybrid RS41+ERA5 columns:

| Difference                             | LIN mean  |
| -------------------------------------- | --------- |
| AP − Smith–Weintraub                   | +0.909 mm |
| AP − Bevis 1994                        | +1.212 mm |
| AP − Thayer, unity compressibility     | +0.491 mm |
| AP − Thayer, component compressibility | −0.455 mm |
| AP − Rüeger 2002                       | −1.904 mm |

The total spread is about 3.12 mm, equivalent to approximately 0.49 kg m⁻² if it were incorrectly attributed entirely to IWV.

Make three points:

* Differences are systematic and atmospheric-state dependent.

* Different “Thayer” implementations are not interchangeable.

* Agreement with one GNSS solution is not an accuracy ranking of refractivity models.

This modernizes the refractivity-coefficient sensitivity discussion from [Bock et al. (2021)](https://doi.org/10.5194/essd-13-2407-2021).

***

### Slide 12 — Lindenberg: what the present results establish

Show a compact result table:

| Diagnostic                          | Lindenberg result |
| ----------------------------------- | ----------------- |
| Number of hybrid profiles           | 1517              |
| RS41+ERA5 − ERA5-only ZTD           | +1.91 mm          |
| Standard deviation                  | 4.85 mm           |
| Ground-check pressure perturbation  | +0.166 hPa        |
| Corresponding hydrostatic increment | +0.377 mm         |
| Mean Z0,d⋆​                         | 0.110 mm          |
| Mean ZNL​                           | 0.065 mm          |
| Maximum condensate contribution     | 1.39 mm           |

Interpretation:

* The hybrid-minus-ERA5 difference quantifies profile substitution.

* It is not independent validation because both operators share ERA5 completion and condensate.

* The pressure test is a sensitivity experiment because independence of the ground-check pressure from the profile-derived pressure has not yet been documented.

* Sample SD and percentiles are atmospheric variability, not propagated uncertainty.

Do not show the obsolete revision-2 value\
ZTDRS+ERA5​−ZTDGNSS​=6.18 mm as a current result. It preceded the corrected condensate partition and belongs only in backup material, clearly marked as superseded.

***

### Slide 13 — Closure requires covariance and representativeness

Show the BOAP26 uncertainty framework in simplified form:

uH2​=Kx​Cx​KxT​+Kq​Cq​KqT​+Ka​Ca​KaT​+2r\<s∑​Kr​Crs​KsT​+urepr2​+unum2​.

Translate it verbally:

* Cx​: temperature, humidity, pressure and profile covariance.

* Cq​: refractivity-coefficient covariance.

* Ca​: pressure height, gravity, collocation and auxiliary inputs.

* Cross-covariances: shared profile variables and shared ERA5 data.

* urepr​: sonde drift, GNSS cone sampling and time/space mismatch.

* unum​: interpolation, quadrature, truncation and mapping approximations.

Key message:

> A three-cornered-hat or pairwise variance decomposition is invalid unless independence is demonstrated.

***

### Slide 14 — What currently prevents closure?

Present this as a checklist, with red/amber/green status.

Red:

* Pressure-coordinate versus height-coordinate integration discrepancy: 1.06–2.19 mm in absolute site means.

* No complete propagated covariance budget yet.

* No consistently processed GNSS solution has yet been included in the revised 15-site experiment.

Amber:

* Independence and calibration chain of ground-check pressure.

* Sonde gaps, lower/upper completion and launch-time matching.

* Balloon drift and GNSS–RS horizontal separation.

* Antenna phase-centre and pressure-reference height.

* Representativeness of the radiosonde trajectory versus the GNSS sensing cone.

Green:

* Exact algebraic closure of the ZTD partition.

* Condensate included consistently in total atmospheric mass.

* Same profiles, grids and integration bounds used for refractivity-model comparisons.

* Diagnostic terms and source fractions are available.

Phrase the 10−4 target carefully:

> “The 0.24 mm value is an aspirational numerical and structural consistency budget for a 2.4 m forward ZTD operator—not an achieved uncertainty and not a 10−4 IWV requirement.”

***

### Slide 15 — Proposed WG3 benchmark

Structure the benchmark in four coordinated layers.

1. Common observations and metadata

* Several GRUAN sites spanning polar, midlatitude and tropical regimes.

* Prefer sites with multiple GNSS receivers and traceable pressure.

* Document antenna/radome history, station heights and processing events.

2. GNSS processing ensemble

* Multiple software packages and institutions.

* Common satellite products plus deliberately varied processing options.

* Archive ZTD, gradients, formal covariance and residual diagnostics.

3. Common conversion and reference operators

* Conventional and AP refractivity formulations.

* Identical ps​, Tm​, gravity and height conventions.

* RS41+ERA5 best-estimate ZTD and IWV supplied with diagnostic component terms.

4. Closure assessment

* Blind comparison where possible.

* Explicit covariance and representativeness model.

* Results by site, humidity regime, elevation strategy and processing configuration.

* Separate repeatability, bias, structural discrepancy and uncertainty coverage.

A useful output table would contain:

| Output                                | Purpose                         |
| ------------------------------------- | ------------------------------- |
| Common GNSS ZTD solutions             | Processing sensitivity          |
| Best-estimate RS+ERA5 ZTD             | Reference comparator            |
| IWV under common conversion           | Isolate ZTD effects             |
| IWV under processor-native conversion | Evaluate full operational chain |
| Per-epoch uncertainty components      | Closure testing                 |
| Open scripts and metadata             | Reproducibility                 |

***

### Slide 16 — From benchmark to metrological closure

Use three conclusions:

1. ZTD remains the dominant contribution to operational GNSS-IWV uncertainty, but conversion and reference-definition errors are already important at the GCOS breakthrough and goal levels.

2. The AP hydrostatic partition offers a promising reference operator because it isolates the pressure-constrained mass term and makes small dry, wet, condensate and nonlinear corrections explicit.

3. Closure cannot be claimed from a small mean difference alone. It requires identical measurands, corrected systematic effects, covariance-aware uncertainty and an independent comparison design.

End with a concrete WG3 proposal:

> “For the benchmark, I can provide the RS41+ERA5 best-estimate ZTD operator and diagnostics for the GRUAN sites. GFZ already has extensive GNSS processing experiments. WG3 can connect these components into a common, blind and uncertainty-aware closure experiment.”

Then ask the meeting to agree on:

* Initial sites.

* GNSS solutions and software packages.

* Common metadata and output format.

* Reference pressure strategy.

* Responsibility for the uncertainty and representativeness model.

## Main changes I recommend to your outline

* Make metrological compatibility the spine of the talk.

* Introduce the closure equation before discussing individual uncertainty sources.

* Clarify that Type A/Type B classify evaluation methods, not physical error types.

* Separate GNSS-ZTD uncertainty from ZTD-to-IWV conversion uncertainty.

* Present the Aparicio formulation as a reference-operator framework, not as an already validated solution.

* Use revision-6 Lindenberg results only as operator characterization.

* Explicitly state that the 1.06–2.19 mm integration discrepancy currently prevents a numerical-accuracy claim.

* Finish with decisions needed for the Day-2 benchmark session, rather than only a general list of collaborations.

* Keep homogenization to slide 3; otherwise it will compete with your second talk and with Anna Klos’s following presentation.
