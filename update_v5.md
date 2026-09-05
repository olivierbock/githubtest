Yes-this is likely the most accurate and robust radiosonde-based estimator, but the decomposition needs one additional dry residual term and careful avoidance of water-mass double counting.

Aparicio’s linear refractivity is

$$
N_0=A_d\rho_d+A_w\rho_w+A_l\rho_l+A_i\rho_i,
$$

with

$$
\begin{aligned}
A_d &=
q_1(x_{\mathrm{O_2}},x_{\mathrm{CO_2}})
+0.097\,\tau,\\
A_w &=6703.497+6393.484\,\tau,\\
A_l &=1447.827\,f_l,\\
A_i &=686.944\,f_i,
\end{aligned}
\qquad
\tau=\frac{273.15\ \mathrm{K}}{T}-1 .
$$

The full refractivity is

$$
N=N_0+\frac{10^{-6}}{6}N_0^2.
$$

These are Aparicio’s Eqs. (17)-(38). [Aparicio (2026)](https://amt.copernicus.org/articles/19/5135/2026/)

## Exact hydrostatic decomposition

Choose a constant reference mass-refractivity coefficient

$$
q_h=q_1(x_{\mathrm{O_2}}^{*},x_{\mathrm{CO_2}}^{*}),
$$

normally evaluated for the station epoch and representative composition. For gaseous air,

$$
\rho_g=\rho_d+\rho_w,
\qquad
\frac{\mathrm{d}p}{\mathrm{d}z}
=-g(\varphi,z)\rho_g .
$$

Then the linear term can be rewritten exactly as

$$
\boxed{
N_0=
q_h\rho_g
+
(A_d-q_h)\rho_d
+
(A_w-q_h)\rho_w
+
A_l\rho_l
+
A_i\rho_i .
}
$$

Consequently,

$$
Z_0
=
Z_{0,h}
+
Z_{0,d*}
+
Z_{0,w}^{*}
+
Z_{0,c},
$$

where

$$
Z_{0,h}
=
10^{-6}q_h
\int_{z_A}^{\infty}\rho_g\,\mathrm{d}z
=
10^{-6}q_h
\int_{0}^{p_A}\frac{\mathrm{d}p}{g(\varphi,z(p))},
$$

$$
Z_{0,d*}
=
10^{-6}
\int_{z_A}^{\infty}
\left[
q_1(z)-q_h+0.097\,\tau
\right]\rho_d\,\mathrm{d}z,
$$

$$
Z_{0,w}^{*}
=
10^{-6}
\int_{z_A}^{\infty}
\left[
6703.497+6393.484\,\tau-q_h
\right]\rho_w\,\mathrm{d}z,
$$

and

$$
Z_{0,c}
=
10^{-6}
\int_{z_A}^{\infty}
\left[
1447.827f_l\rho_l
+
686.944f_i\rho_i
\right]\mathrm{d}z .
$$

The asterisk on \(Z_{0,w}^{*}\) emphasizes that this is the wet refractivity in excess of the mass-proportional hydrostatic contribution.

### Two important corrections to your proposed decomposition

1. A small dry residual \(Z_{0,d*}\) remains because of the \(0.097\,\tau\rho_d\) term and any vertical variation of composition.

2. If \(Z_{0,h}\) is calculated from total gas pressure, the wet term must use \(A_w-q_h\), not the full \(A_w\). Otherwise the water-vapour mass contribution \(q_h\rho_w\) is counted twice.

If \(q_1\) is constant over the profile,

$$
Z_{0,d*}
=
10^{-6}\int 0.097\,\tau\rho_d\,\mathrm{d}z.
$$

It is small-generally at the few hundredths of a millimetre level-but should be retained in a \(10^{-4}\)-accuracy implementation.

## Complete recommended estimator

I would formulate the radiosonde estimator as

$$
\boxed{
\widehat{\mathrm{ZTD}}
=
Z_{0,h}(p_A,\varphi,h_A,q_h)
+
\sum_{r\in\{\mathrm{bottom,RS,top}\}}
\left[
Z_{0,d*}^{(r)}
+
Z_{0,w}^{*(r)}
+
Z_{0,c}^{(r)}
+
Z_{\mathrm{NL}}^{(r)}
\right],
}
$$

with

$$
Z_{\mathrm{NL}}^{(r)}
=
\frac{10^{-12}}{6}
\int_r N_0^2\,\mathrm{d}z .
$$

Thus, once \(Z_{0,h}\) is evaluated from the antenna-level surface pressure for the whole atmospheric column:

- `bottom` contains only the residual linear terms and \(N_{\mathrm{NL}}\) between antenna and first sonde point;
- `top` contains only those residual terms above the sonde burst;
- the hydrostatic part must not be added again in either correction.

This substantially reduces the upper-atmosphere correction because almost all upper-stratospheric delay is already included through \(p_A\).

## Why it is generally more accurate

The reformulation does not change Aparicio’s physics: with perfect profiles and exact integration, it is algebraically identical to direct integration. Its practical advantages are:

- the dominant \(2.3\ \mathrm{m}\) contribution is constrained by one surface-pressure measurement;
- it automatically includes the hydrostatic mass above the radiosonde burst;
- it reduces sensitivity to radiosonde gaps, temperature errors and quadrature resolution;
- surface-pressure uncertainty is correctly represented as one column-correlated uncertainty;
- it reduces sensitivity to radiosonde horizontal drift for the dominant dry component.

For an RS41-GDP profile, the gain is mostly numerical and metrological rather than independent information: `press_gnss` is already generated hydrostatically from a surface-barometer boundary. The hybrid and direct-density estimators should therefore agree closely. A significant difference is a useful diagnostic for boundary-height, pressure, EOS or integration inconsistencies. [GRUAN-TD-8, Sect. 4.4.2](https://www.gruan.org/gruan/editor/documents/gruan/GRUAN-TD-8_RS41_v1.0.0_20230628_final.pdf)

## Surface pressure and gravity requirements

Write

$$
Z_{0,h}
=
10^{-6}q_h p_A\,
\overline{g^{-1}}_p,
\qquad
\overline{g^{-1}}_p
=
\frac{1}{p_A}
\int_0^{p_A}\frac{\mathrm{d}p}{g(\varphi,z(p))}.
$$

Near normal surface conditions,

$$
\frac{\partial Z_{0,h}}{\partial p_A}
\simeq 2.27\ \mathrm{mm\,hPa^{-1}}.
$$

Therefore, a \(0.1\ \mathrm{hPa}\) pressure uncertainty produces approximately

$$
u(Z_{0,h})\simeq 0.23\ \mathrm{mm},
$$

already comparable to \(10^{-4}\) of the total ZTD.

Use pressure at the GNSS antenna phase centre. `g.SurfaceObs.Pressure` or the first `press` value normally refers to the sonde launch level, so it must be transferred to antenna height if the two heights differ.

For the \(10^{-4}\) target, I would not use the conventional \(0.0022768p/f(\varphi,H)\) expression unmodified: its coefficient belongs to an older refractivity convention, and simplified closed hydrostatic models can retain geographically and seasonally dependent millimetre-level differences. Instead, use Aparicio’s \(q_h\) and calculate \(\overline{g^{-1}}_p\) from the radiosonde-ERA5 height-pressure profile. The conventional formula remains valuable as a check. [IERS Conventions 2010](https://www.iers.org/iers/en/publications/technicalnotes/tn36), [Fan et al. (2023)](https://gmd.copernicus.org/articles/16/1345/2023/)

So the short conclusion is:

$$
\boxed{
\text{Yes, use the surface-pressure hydrostatic separation,}
}
$$

but implement it as

$$
Z_{0,h}
+
Z_{0,d*}
+
Z_{0,w}^{*}
+
Z_{0,c}
+
Z_{\mathrm{NL}},
$$

with bottom and top corrections applied only to the residual terms.
