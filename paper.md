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

The package utilizes a minimal set of core dependencies: `numpy` @Harris2020, `scipy` @Virtanen2020, `sympy` @Meurer2017 (with optional `symengine` @symengine support) and a set of visualizations created with `matplotlib` @Hunter2007.

![Illustration of the scattering contributions considered in the RT1 model (from @Quast2023) \label{fig_model}](docs/_static/model.png)

# Statement of need


Radiative transfer theory is used in a variety of contexts to retrieve biophysical characteristics from radar signals.

The presented generic solution to the problem of a rough surface covered by a tenuous distribution of particulate media with respect to parametric distribution functions allows a intuitive yet flexible way to parametrize


The description of the scattering characteristics of a rough surface covered by vegatation remains challenging.


With the increasing availability of bistatic measurements (for example from GNSS), the need for bi-static parameterization stragegies  

For example, the RT1 modeling framework was used for soil-moisture retrieval from microwave c-band radar data (@Quast2019, @Quast2023) and adapted for rice-crop monitoring @Yadav2022 with a ground based bistatic scatterometer.





# References
