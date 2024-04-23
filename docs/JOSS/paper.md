---
title: 'rt1_model: A python package for single-layer bistatic first-order radiative transfer scattering calculations.'

tags:
  - python
  - remote sensing
  - soil moisture
  - radiative transfer

authors:
  - name: Raphael Quast  
    orcid: 0000-0003-0419-4546  
    affiliation: TU Wien, Department of Geodesy and Geoinformation, Research Unit Remote Sensing  
  - name: Wolfgang Wagner  
    orcid: 0000-0001-7704-6857  
    affiliation: TU Wien, Department of Geodesy and Geoinformation, Research Unit Remote Sensing  
  - name: Bernhard Raml  
    affiliation: TU Wien, Department of Geodesy and Geoinformation, Research Unit Remote Sensing  

date: 24 April 2024

bibliography: paper.bib

---

# Summary

The `rt1_model` package implements a generic solution to the radiative transfer equation applied to the problem of a rough surface covered by a tenuous distribution of particulate media as described in @Quast2016.

It provides a flexible, object-oriented interface to specify the scattering characteristics of the ground surface and the covering layer via parametric distribution functions and to evaluate the resulting backscattering-coefficient ($\sigma_0$) for monostatic or bistatic measurement geometries as illustrated in Figure \ref{fig_model}.

The underlying calculations are implemented via symbolic expressions, allowing the user to create fully customized model parameterizations. To speed up parameter retrieval stragegies, analytic solutions for the Jacobian of arbitrary model parameters are provided.

The package utilizes a minimal set of core dependencies, namely: `numpy` @Harris2020, `scipy` @Virtanen2020, `sympy` @Meurer2017 (with optional `symengine` @symengine support) and a set of visualizations created with `matplotlib` @Hunter2007.

![Illustration of the scattering contributions considered in the RT1 model (from @Quast2023) \label{fig_model}](model.png)

# Statement of need


Radiative transfer theory is used in a variety of contexts to retrieve biophysical characteristics from radar signals.

The presented generic solution to the problem of a rough surface covered by a tenuous distribution of particulate media with respect to parametric distribution functions allows a intuitive yet flexible way to parametrize

The description of the scattering characteristics of a rough surface covered by vegatation remains challenging.

With the increasing availability of bistatic measurements (for example from GNSS), the need for bi-static parameterization stragegies  

For example, the RT1 modeling framework was used for soil-moisture retrieval from microwave c-band radar data (@Quast2019, @Quast2023) and adapted for rice-crop monitoring @Yadav2022 with a ground based bistatic scatterometer.

## Distribution functions

The package provides a set of distribution functions (Isotropic, Rayleigh, HenyeyGreenstein, ...) that can be used to describe basic volume- or surface scatternig behaviors. More complex scattering scenarios can then be modelled by utilizing parametric linear-combinations.

To support possibly anisotropic scattering characteristics, all functions are furthermore implemented with respect to a generalized scattering angle \ref{eq_scat_angle} @Lafortune:

$$\cos(\Theta_a) = a_0 \cos(\theta) \cos(\theta_s) + \sin(\theta)\sin(\theta_s) [ a_1 \cos(\phi)\cos(\phi_s) + a_2 \sin(\phi) \sin(\phi_s)] \label{eq_scat_angle}$$

where ($\theta, \phi$) denote the incident azimuth and polar angle and $(\theta_s, \phi_s)$ the corresponding exit angles and $(a_0, a_1, a_2)$ are the generalization parameters.

For example, a combination of a forward- and a backward oriented HenyeyGreenstein peak defined as:

$$BRDF = w * HG(-t, a_0=-1) + (1-w) * HG(t, a_0=1) \quad \textrm{with} \quad w, t \in (0,1)$$

Can be implemented via:

```
from rt1_model import surface

SRF_1 = surface.HenyeyGreenstein(t="-t", a=[-1, 1, 1], ncoefs=12)
SRF_2 = surface.HenyeyGreenstein(t="t",  a=[ 1, 1, 1], ncoefs=12)
SRF = surface.LinComb([("w", SRF_1), ("1-w", SRF_2)])
```


![Linear Combination of surface BRDFs. \label{fig_lin_comb_brdf}](lin_comb_brdf.png)


## Optimization

![Example of the analyzer-widget for a RT1 model result. \label{fig_retrieval_static}](retrieval_static.png)




# References
