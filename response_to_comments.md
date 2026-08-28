# Response to comments on the first draft

Date: 27 August 2026  
Manuscript: *Hydrostatically constrained GNSS tropospheric delays and integrated water vapour with the Aparicio (2026) refractivity model: formulation, uncertainty, and a midlatitude demonstration*

Thank you for the careful reading and constructive comments. The manuscript structure and tone have been retained, while the refractivity partition, polarization presentation, uncertainty section, numerical examples, Lindenberg framing, references, and MATLAB implementation have been revised. The principal scientific correction is the use of total atmospheric mass in the hydrostatic reference term, including subtraction of (q_{1r}) from the liquid- and ice-water residual coefficients.

## Major comments

### 1. Accessibility and derivation of the polarization treatment

The main text now introduces a local transverse ((E_x,E_y)) Jones basis before using the Aparicio (H) and (V) material responses. It explicitly distinguishes field components from the particle-axis response labels. The receiver convention is now written as RCP rather than the unexplained subscript (R).

A new appendix derives the (cos^2 E) projection and the circular co-polar mean phase from a diagonal Jones matrix. Jones (1941) and Born and Wolf are cited for the Jones calculus and modal-phase result; antenna phase-centre references were added for the receiver-side caveat. The main text points to both the slant numerical example and the new ZTD-projection example.

The scope is now limited to two practical levels: a spherical-particle baseline with a condition-dependent uncertainty, and a first-order replay using NWP condensate and the actual GNSS observation schedule. The more elaborate experimental programme has been removed.

### 2. Lindenberg and the companion intercomparison

The title now says “midlatitude demonstration” rather than naming Lindenberg. Lindenberg remains the concrete use case in Sect. 6.

The existing AP/BE/RU/TH metrics are retained only as **preliminary gas-phase values**. The draft states in the front matter, figure caption, Sect. 6, and conclusions that they pre-date the corrected condensate partition and must be replaced after the code is rerun. The text now quantifies what refractivity choice explains: relative to AP, BE reduces the mean RS+ERA5-minus-GNSS difference by 1.21 mm (about 20%), TH by 0.49 mm (about 8%), whereas RU increases it by 1.90 mm. No causal attribution is made from this comparison alone.

The available GFZ and NGL chains, plus the GFZ mapping-function and elevation-cut-off experiments, are identified as processing-robustness evidence. They are not described as statistically independent measurements. Detailed multi-site and multi-year attribution is explicitly reserved for a separate intercomparison.

### 3. Scope of the metrological-closure discussion

The six-item project-style programme has been replaced. The revised discussion defines metrological closure operationally: all systems must represent the same measurand, epoch, antenna height, and atmospheric column, and their differences must be consistent with a covariance model. Only the evidence needed for the revised Lindenberg analysis is listed. No detailed ANR/COST project design is disclosed.

### 4. Quantifying uncertainty for Lindenberg

The revised Sect. 6 distinguishes the GUM evaluation methods:

- Type A: sampling variability of the launch differences, evaluated with launch-cluster/block resampling or an autocorrelation-adjusted effective sample size.
- Type B: GRUAN correlated and uncorrelated (p,T,mathrm{RH}) components; independent antenna-level pressure and height transfer; ERA5 lower/gap/top completion; equation of state; condensate; quadrature; GNSS formal covariance; and processing sensitivity from GFZ/NGL and the GFZ tests.

For orientation only, treating all 1520 collocations as independent would give (7.88/sqrt{1520}=0.20) mm for the AP mean, but the manuscript states that this is not a defensible final standard uncertainty. The revised formulation uses a covariance matrix,

\[
u_B^2(\bar d)=\mathbf a^\mathsf{T}\mathbf C_B\mathbf a,
\qquad
u_c^2(\bar d)=u_A^2(\bar d)+u_B^2(\bar d),
\]

\[
u_B^2(\bar{d}) = \mathbf{a}^\mathsf{T} \mathbf{C}_B \mathbf{a}, \qquad u_c^2(\bar{d}) = u_A^2(\bar{d}) + u_B^2(\bar{d})
\]

`[!u_B^2(\bar{d}) = \mathbf{a}^\mathsf{T} \mathbf{C}_B \mathbf{a}, \qquad u_c^2(\bar{d}) = u_A^2(\bar{d}) + u_B^2(\bar{d})]`

so fully correlated calibration contributions do not incorrectly decrease as (n^{-1/2}). A three-cornered-hat estimate is retained only as a diagnostic and its independence assumption is stated. Final numerical uncertainties require the per-launch GRUAN uncertainty fields, surface-pressure record, collocation metadata, and GNSS processing information.

## Specific comments

| Comment | Revision |
|---|---|
| Title: Lindenberg versus midlatitude | Changed to “a midlatitude demonstration”; Lindenberg is the use case. |
| Abstract precision | Intercomparison statistics are rounded to two decimals. Synthetic digits are retained only where they document algebraic closure and are described as non-metrological. |
| Define (N_d,N_v,N_c) | Added the dry, vapour, and condensate physical decomposition before the hydrostatic partition. |
| IAPWS/TEOS-10 reference | Added the IAPWS humid-air guideline and Feistel et al. (2010). |
| Impact-parameter reference | Added (a=nr\sin\psi) with Born and Wolf and Healy (2001). |
| Superscript AP on zenith equation | Removed from unqualified zenith quantities; AP is now stated once as the default model. |
| Introduce the physical delay partition | Added (\mathrm{ZTD}=Z_{0,d}+Z_{0,w}+Z_{0,c}+Z_{\mathrm{NL}}). |
| Clarify (E_x,E_y) versus (H,V) | Rewritten with a local Jones basis and material-response definitions. |
| Derive Sect. 2.4 | Added a Jones-vector appendix. |
| Reference for mean circular phase | Added Jones (1941) and Born and Wolf. |
| Meaning of subscript (R) | Replaced by and defined as RCP. |
| “Companion analysis” | Removed. The manuscript now points to its own numerical subsections. |
| Receiver/antenna reference | Added Mader (1999) and Schmid et al. (2005); the limitations of a scalar atmospheric correction are stated. |
| Mention numerical example | Added explicit pointers to the slant and ZTD-projection examples. |
| Geometric range notation in Eq. 19 | Replaced by (\lVert\mathbf r_s-\mathbf r_r\rVert); the ambiguity symbol was also changed. |
| Meaning of (T^{\mathrm{AP}}) and the 3-D/bending term | Removed the unnecessary AP superscript. The term is now (\delta T_{\mathrm{op},j}), explicitly defined as the residual between the reference ray-traced delay and the parameterized estimator model. |
| Design matrix (A\rightarrow X) | Changed. |
| Define Eq. 21 terms | The text now points to Sect. 3 and defines the residual terms there. |
| Condensate error in MATLAB partition | Corrected in the equations and MATLAB code: (\rho_m=\rho_d+\rho_v+\rho_l+\rho_i), and (q_{1r}) is subtracted from both condensate coefficients. |
| Explain Eq. 35 subscripts | Added definitions for the bottom, radiosonde, gap, and top domains and the radiosonde/model source transitions. |
| Source fractions and quality flags | Defined as archived fractions of the integrated term by source, plus gap, extrapolation, pressure, condensate, and EOS decisions. |
| Ground-check pressure | Corrected: a reference pressure may be used in the pre-flight ground check, while the default GDP pressure profile is generally `press_gnss`; an independent station barometer remains distinguishable. |
| Assimilation Jacobian references | Added Courtier et al. (1994) and Evensen (2003). |
| Collocation parameters | Epoch tolerance, horizontal distance, antenna/launch height transfer, model interpolation, sonde-drift treatment, and accepted profile flags are now named. |
| Rename IWV coefficient (C\rightarrow Q) | Changed throughout equations, derivatives, text, and implementation checks. |
| Unexplained precise (T_m), IWV, humidity scale | Replaced by a declared synthetic U.S. Standard Atmosphere column. IWV is exactly 20.0 kg m(^{-2}), the 2.0 km vapour scale is explicitly illustrative, and (T_m) is an output rather than an independently selected value. |
| Describe standard temperature profile | Added the U.S. Standard Atmosphere 1976 lapse-rate construction and surface state. |
| Choke-ring reference | Added Mader (1999) and Schmid et al. (2005). |
| Add polarization-to-ZTD example | Added Sect. 5.3. For the declared nine-elevation schedule, the strong-rain example projects to (-0.22) mm with (\sin^2E) weights and (-0.35) mm with unit weights; these are explicitly not Lindenberg corrections. |
| Equation reference for IWV conversion | Corrected to cite both the conversion and uncertainty equations where appropriate. |
| Three-cornered-hat reference | Added Premoli and Tavella (1993), with the shared-error limitation. |
| Define Type A and Type B | Added the GUM definitions and citation. |
| Quantify target accuracy | Added (10^{-4}), approximately 0.24 mm for a 2.4 m ZTD. |
| Specify CIPM domain | Added 600--1100 hPa, 15--27 °C, and 0--100% RH; the MATLAB code now flags use outside this recommended domain. |
| Reorder EOS strategy | The surface-pressure hydrostatic constraint is now first, followed by the lower-atmosphere EOS and an extended aloft formulation. |
| Polarization treatment levels | Reduced from three to the requested baseline and first-order levels. |
| Metrological-closure programme | Replaced by a compact, scope-safe definition and Lindenberg evidence plan. |

## MATLAB implementation changes

The revised `compute_ztd_rs41_aparicio2026.m` now:

- uses total mass density in the hydrostatic and pressure-coordinate quadrature;
- computes (N_{0,c^\star}=(q_5f_l-q_{1r})\rho_l+(q_6f_i-q_{1r})\rho_i);
- exposes `N0_cstar`, `Z_0_cstar_m`, radiosonde-span and ERA5 counterparts;
- retains `Z_0_c_m` and the old `physical_partition_*` names only as backward-compatible aliases;
- adds unambiguous `ZTD_hydrostatic_partition_m` and closure fields;
- reports total-column mass explicitly while retaining historical `gas_column_mass_*` aliases;
- uses the vapour fraction on the same total-mass basis for pressure-coordinate IWV;
- flags evaluation outside the recommended CIPM-2007 domain;
- preserves strict surface-pressure decoupling and the independent ERA5-only result.

Randomized pointwise tests close the corrected linear partition to floating-point precision. The zero-condensate algebra is unchanged. MATLAB or Octave was not available in the preparation environment, so the complete table/datetime workflow still requires execution in MATLAB before the updated Lindenberg analysis.

## Items awaiting author data or decisions

1. Replace the preliminary Lindenberg figure and AP/BE/RU/TH statistics after rerunning the corrected code with the new condensate inputs.
2. Supply the exact GFZ and NGL processing metadata, collocation rules, surface-pressure provenance, and GRUAN uncertainty fields.
3. Confirm affiliations, corresponding author, CRediT roles, data identifiers, acknowledgements, and public software repository details.
4. Decide whether the first submitted paper should include the full empirical Lindenberg uncertainty table or present the operator and one-station diagnostic while reserving extended attribution for the companion paper.
