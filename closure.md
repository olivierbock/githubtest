Concept

Metrological closure asks whether two or more independent realizations of the same measurand agree within their stated measurement uncertainties. For GNSS-integrated water vapour, it provides a rigorous test of the complete retrieval and uncertainty-propagation chain, rather than merely checking whether correlations are high or mean differences are small.

The term “metrological closure” is used operationally in atmospheric-observation communities such as GRUAN. It is closely connected to the VIM concepts of metrological compatibility, measurement uncertainty, and metrological traceability. The BIPM defines traceability as the property whereby a measurement result is related to a reference through a documented, unbroken calibration chain, with every step contributing to the uncertainty.

1. What does “closure” mean mathematically?

Suppose two systems measure the same atmospheric column water vapour:

x1±u1,x2±u2,x_1 \pm u_1,\qquad x_2 \pm u_2,

where:

x1x_1 and x2x_2 are measured IWV values;
u1u_1 and u2u_2 are standard uncertainties, nominally corresponding to one standard deviation;
both values refer to the same measurand, location, atmospheric column, and effective observation time.

Define the difference

d=x1−x2.d=x_1-x_2.

Its standard uncertainty is

ud=u12+u22−2 cov⁡(x1,x2).u_d = \sqrt{u_1^2+u_2^2-2\,\operatorname{cov}(x_1,x_2)}.

Equivalently, using an error correlation coefficient ρ\rho,

ud=u12+u22−2ρu1u2.u_d = \sqrt{u_1^2+u_2^2-2\rho u_1u_2}.

If the measurements are genuinely independent,

ud=u12+u22.u_d = \sqrt{u_1^2+u_2^2}.

The normalized closure residual is

En=x1−x2ud.E_n=\frac{x_1-x_2}{u_d}.

Closure is conventionally judged by comparing ∣En∣|E_n| with a coverage factor:

∣En∣≤1|E_n| \leq 1

for a one-standard-deviation compatibility test, or

∣En∣≤1.96|E_n| \leq 1.96

for an approximate two-sided 95% test under Gaussian assumptions.

Thus, closure does not mean x1=x2x_1=x_2. It means that the observed difference is statistically plausible given the uncertainty assigned to the difference.

2. GNSS IWV measurement equation

A ground-based GNSS analysis first retrieves the zenith total delay:

ZTD=ZHD+ZWD,\mathrm{ZTD}=\mathrm{ZHD}+\mathrm{ZWD},

where:

ZTD is zenith total delay;
ZHD is zenith hydrostatic delay;
ZWD is zenith wet delay.

The wet delay is inferred as

ZWD=ZTD−ZHD.\mathrm{ZWD}=\mathrm{ZTD}-\mathrm{ZHD}.

It is then converted to IWV through

IWVGNSS=Π(Tm) ZWD,\mathrm{IWV}_{\mathrm{GNSS}}=\Pi(T_m)\,\mathrm{ZWD},

where Π\Pi is the wet-delay-to-IWV conversion factor and TmT_m is the water-vapour-weighted mean atmospheric temperature,

Tm=∫e(z)T(z) dz∫e(z)T2(z) dz.T_m= \frac{\displaystyle \int \frac{e(z)}{T(z)}\,dz} {\displaystyle \int \frac{e(z)}{T^2(z)}\,dz}.

Here ee is water-vapour partial pressure and TT is absolute temperature. In routine retrievals, TmT_m may come from a numerical weather model, a radiosonde profile, or an empirical relationship with surface temperature.

The GNSS IWV uncertainty therefore depends on the whole measurement model:

u2(IWVGNSS)=J Cx JT,u^2(\mathrm{IWV}_{\mathrm{GNSS}}) = \mathbf{J}\,\mathbf{C}_x\,\mathbf{J}^{\mathrm T},

where J\mathbf{J} is the Jacobian of the IWV model with respect to its input quantities and Cx\mathbf{C}_x is their covariance matrix.

In a simplified form,

u2(IWVGNSS)≈Π2[u2(ZTD)+u2(ZHD)−2cov⁡(ZTD,ZHD)]+ZWD2u2(Π)+2Π ZWDcov⁡(Π,ZWD).\begin{aligned} u^2(\mathrm{IWV}_{\mathrm{GNSS}}) \approx {}& \Pi^2 \left[ u^2(\mathrm{ZTD}) + u^2(\mathrm{ZHD}) - 2\operatorname{cov}(\mathrm{ZTD},\mathrm{ZHD}) \right] \\ &+ \mathrm{ZWD}^2u^2(\Pi) + 2\Pi\,\mathrm{ZWD}\operatorname{cov}(\Pi,\mathrm{ZWD}). \end{aligned}

The ZHD uncertainty is strongly influenced by surface pressure and station height. The conversion factor is influenced by the representation of TmT_m, atmospheric profile uncertainty, and the spectroscopic constants used in the refractivity formulation. Radiosonde-based studies also show that profile truncation, humidity uncertainty, vertical error correlation, and the ZHD and TmT_m formulations can contribute appreciably to GNSS–radiosonde IWV differences.

3. Applying closure to GNSS and radiosonde IWV

Let

IG=IWVGNSS,IR=IWVRS.I_G = \mathrm{IWV}_{\mathrm{GNSS}}, \qquad I_R = \mathrm{IWV}_{\mathrm{RS}}.

For each collocated pair, calculate

di=IG,i−IR,i.d_i=I_{G,i}-I_{R,i}.

The uncertainty of that difference should include both measurement uncertainties and any comparison-specific term:

ud,i2=uG,i2+uR,i2−2 cov⁡(IG,i,IR,i)+urepr,i2.u_{d,i}^2 = u_{G,i}^2 + u_{R,i}^2 - 2\,\operatorname{cov}(I_{G,i},I_{R,i}) + u_{\mathrm{repr},i}^2.

Here urepru_{\mathrm{repr}} represents the fact that the two systems rarely sample exactly the same atmospheric volume.

The normalized residual is

zi=diud,i.z_i=\frac{d_i}{u_{d,i}}.

Pairwise closure at approximately 95% coverage is supported when

∣zi∣≤1.96.|z_i|\leq 1.96.

This is essentially the procedure proposed within GRUAN: compare collocated GNSS and radiosonde data products together with their individual uncertainties and establish whether they are metrologically compatible.

Numerical example

Suppose

IG=22.4 kg m−2,uG=0.70 kg m−2,I_G=22.4\ \mathrm{kg\,m^{-2}}, \qquad u_G=0.70\ \mathrm{kg\,m^{-2}},

and

IR=21.4 kg m−2,uR=0.50 kg m−2.I_R=21.4\ \mathrm{kg\,m^{-2}}, \qquad u_R=0.50\ \mathrm{kg\,m^{-2}}.

Assuming independence and negligible representativeness uncertainty,

d=1.0 kg m−2,d=1.0\ \mathrm{kg\,m^{-2}},

and

ud=0.702+0.502=0.86 kg m−2.u_d=\sqrt{0.70^2+0.50^2} =0.86\ \mathrm{kg\,m^{-2}}.

Therefore,

z=1.00.86=1.16.z=\frac{1.0}{0.86}=1.16.

The measurements do not agree within 1u1u, but they are compatible at the approximate 95% level because

1.16<1.96.1.16<1.96.

Now suppose the quoted uncertainties were only 0.250.25 and 0.20 kg m−20.20\ \mathrm{kg\,m^{-2}}. Then

ud=0.32 kg m−2,z=3.12.u_d=0.32\ \mathrm{kg\,m^{-2}}, \qquad z=3.12.

The same physical difference would now indicate failure of closure. This illustrates that closure evaluates measurements and their uncertainty statements jointly.

4. The representativeness problem

For GNSS–radiosonde comparisons, representativeness is often as important as instrument uncertainty.

GNSS sampling

A GNSS IWV estimate is obtained from slant paths distributed over a changing three-dimensional atmospheric volume. After mapping and parameter estimation, it represents something like a temporally averaged atmospheric cone around the antenna.

Radiosonde sampling

A radiosonde measures along a drifting ascent trajectory. During a one-hour ascent, it may travel tens or hundreds of kilometres horizontally, especially in the upper troposphere. It also samples the column sequentially rather than instantaneously.

Consequently, the difference can be written conceptually as

d=bG−bR+ϵG−ϵR+ϵrepr,d = b_G-b_R +\epsilon_G-\epsilon_R +\epsilon_{\mathrm{repr}},

where:

bG,bRb_G,b_R are systematic components;
ϵG,ϵR\epsilon_G,\epsilon_R are random measurement errors;
ϵrepr\epsilon_{\mathrm{repr}} is the sampling mismatch.

Ignoring ϵrepr\epsilon_{\mathrm{repr}} can make a sound uncertainty model appear too small. Conversely, arbitrarily inflating urepru_{\mathrm{repr}} can manufacture closure and hide real biases.

A defensible estimate can be obtained from:

high-resolution numerical weather model fields;
comparison of IWV integrated along the radiosonde trajectory with IWV over the GNSS sensitivity volume;
multiple nearby GNSS stations;
spatial structure functions or variograms of IWV;
sensitivity tests involving launch time, temporal averaging, drift distance, and weather regime.
5. Closure over an ensemble

Counting individual values satisfying ∣zi∣<1.96|z_i|<1.96 is useful but insufficient. A complete ensemble analysis should examine both bias closure and dispersion closure.

5.1 Weighted mean bias

With

wi=1ud,i2,w_i=\frac{1}{u_{d,i}^2},

the uncertainty-weighted mean difference is

dˉw=∑iwidi∑iwi,\bar d_w = \frac{\sum_i w_i d_i}{\sum_i w_i},

with nominal uncertainty

u(dˉw)=(∑iwi)−1/2,u(\bar d_w)= \left(\sum_i w_i\right)^{-1/2},

provided that the differences are independent.

A bias-closure statistic is

zbias=dˉwu(dˉw).z_{\mathrm{bias}}= \frac{\bar d_w}{u(\bar d_w)}.

A significant dˉw\bar d_w indicates a persistent systematic difference. For time series, however, serial correlation reduces the effective sample size, so the simple expression for u(dˉw)u(\bar d_w) is usually optimistic.

5.2 Reduced chi-square

The overall consistency of residual dispersion with the assigned uncertainties can be tested using

χν2=1ν∑i=1N(di−b^)2ud,i 2,\chi_\nu^2= \frac{1}{\nu} \sum_{i=1}^{N} \frac{(d_i-\hat b)^2}{u_{d,i}^{\,2}},

where b^\hat b is either zero, if zero bias is part of the closure hypothesis, or an estimated common bias, and ν\nu is the corresponding number of degrees of freedom.

Interpretation:

χν2≈1\chi_\nu^2\approx1: observed dispersion is consistent with stated uncertainties;
χν2≫1\chi_\nu^2\gg1: uncertainties are underestimated, covariance or representativeness is missing, outliers are present, or the measurement models are inconsistent;
χν2≪1\chi_\nu^2\ll1: uncertainties may be conservative, observations may be correlated, or uncertainty components may have been double-counted.
5.3 Distribution of normalized residuals

If the model is correctly specified and approximately Gaussian,

zi∼N(0,1).z_i\sim\mathcal N(0,1).

One should therefore inspect:

mean or median of ziz_i;
standard deviation and robust scale;
68% and 95% empirical coverage;
skewness and heavy tails;
dependence on IWV, season, solar elevation, rainfall, pressure, temperature, and radiosonde drift;
temporal autocorrelation;
change points associated with equipment, processing, or metadata changes.

For independent Gaussian residuals, approximately 68% should fall within [−1,1][-1,1] and 95% within [−1.96,1.96][-1.96,1.96]. These percentages should not be imposed blindly when the uncertainty distribution is non-Gaussian or the observations are correlated.

6. Shared inputs and correlated errors

The independence assumption is often violated.

For example, GNSS and radiosonde products may share:

surface-pressure observations;
numerical weather model profiles;
refractivity constants;
gravity and station-height information;
an empirical TmT_m formulation;
the same atmospheric fields for profile completion.

If the shared contribution produces positive covariance, then

ud2<uG2+uR2.u_d^2 < u_G^2+u_R^2.

Ignoring this covariance overestimates the uncertainty of the difference and makes closure artificially easy. Negative covariance has the opposite effect.

A particularly problematic design is to use the radiosonde profile to calculate TmT_m for the GNSS product and then describe the GNSS–radiosonde comparison as independent validation. That may provide a useful consistency test, but it is not a fully independent closure experiment.

7. What a closure failure tells you

Patterns in normalized residuals can help diagnose the source.

Observed pattern	Plausible explanationConstant GNSS–RS offset	Pressure bias, ZTD bias, antenna calibration, profile truncation, humidity bias
Difference proportional to IWV	Error in Π\Pi, TmT_m, humidity scale, or refractivity constants
Larger scatter in summer or humid conditions	Humidity-sensor behaviour, stronger spatial variability, underestimated representativeness
Dependence on radiosonde drift	Spatial sampling mismatch
Dependence on GNSS elevation cutoff	Multipath, mapping functions, gradients, residual antenna effects
Day–night dependence	Radiosonde radiation correction or diurnal representativeness
Site-specific bias	Local pressure datum, height inconsistency, equipment, processing configuration
χν2≫1\chi_\nu^2\gg1 but negligible mean bias	Underestimated random or representativeness uncertainty
Significant mean bias but χν2≈1\chi_\nu^2\approx1 after demeaning	Unmodelled systematic offset with otherwise realistic random uncertainty

This diagnostic decomposition is more useful than reporting only correlation, RMSE, or the standard deviation of differences.

8. Using three observing systems

With GNSS, radiosonde, and microwave radiometer observations, one can construct the closure loop

(IG−IR)+(IR−IM)+(IM−IG)=0.(I_G-I_R)+(I_R-I_M)+(I_M-I_G)=0.

The arithmetic loop is identically zero if all three differences are formed from the same values, so it is not itself an independent physical test. The useful information comes from:

three pairwise normalized residuals;
their covariance structure;
instrument-specific environmental sensitivities;
triple-collocation or three-cornered-hat methods.

Triple collocation can estimate error variances without designating one system as error-free, but it requires restrictive assumptions, notably sufficiently independent errors and an appropriate linear relationship to a common latent truth. Recent GNSS–radiometer–radiosonde work emphasizes that failure of the error-independence assumption or unstable covariance estimates can strongly affect inferred instrument errors.

9. Recommended practical workflow

For a robust GNSS–radiosonde closure study:

Define the measurand precisely
 State the lower and upper integration boundaries, reference surface, units, station height, effective time, and atmospheric volume.

Harmonize the IWV definition
 Correct for the vertical separation between the GNSS antenna, pressure sensor, and radiosonde launch point. Treat atmosphere above the sonde burst altitude consistently.

Collocate carefully
 Match radiosonde launches to GNSS temporal averages. Retain ascent duration, trajectory, maximum drift, and meteorological regime.

Construct per-observation uncertainty budgets
 Avoid assigning one constant uncertainty to every value if uncertainty depends on pressure, absolute humidity, satellite geometry, profile length, or weather.

Include covariance explicitly
 Identify shared inputs before treating products as independent.

Estimate representativeness separately
 Do not bury spatial mismatch inside the GNSS or radiosonde instrumental uncertainty.

Compute normalized residuals
 Use zi=di/ud,iz_i=d_i/u_{d,i}, not merely did_i.

Test both bias and dispersion
 Report mean difference, uncertainty of the mean, normalized-residual scale, empirical coverage, and reduced chi-square.

Stratify the results
 Examine station, season, IWV range, day/night, sonde type, processing stream, drift distance, and GNSS geometry.

Investigate non-closure physically
 Do not immediately rescale uncertainties to force χν2=1\chi_\nu^2=1. First search for omitted biases, correlations, metadata changes, and representativeness effects.

10. Key interpretation

Metrological closure answers:

Are the GNSS and reference-system IWV differences quantitatively consistent with the uncertainties assigned to the complete comparison?

It does not, by itself, prove that either system is unbiased or traceable to the SI. Two instruments can close while sharing the same bias. Conversely, two accurate instruments can fail a naïve closure test if they observe different air masses or if their uncertainty covariance has been omitted.

For GNSS IWV, a scientifically meaningful closure assessment therefore requires the combined treatment of:

measurement model+uncertainty propagation+covariance+spatiotemporal representativeness+ensemble statistics\boxed{ \text{measurement model} +\text{uncertainty propagation} +\text{covariance} +\text{spatiotemporal representativeness} +\text{ensemble statistics} }

This is the essential distinction between ordinary intercomparison and a genuinely metrological intercomparison.
