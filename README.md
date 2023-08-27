# Summary
The R scripts in this repository can be used to generate summary statistics to use in Mendelian Randomization simulations

There are many different statistical methods available to perform Mendelian Randomization (MR). When these methods are introduced in the literature, simulations are performed to evaluate their performance. There is currently no standard for performing these simulations, hence some methods perform differently in separate simulations intended to mirror the same reality (eg [ref](https://doi.org/10.1101/2021.03.26.437168) and [ref](https://doi.org/10.1214/20-AOS2027
), [ref](https://doi.org/10.1016/j.ajhg.2023.02.014) and [ref](https://doi.org/10.1002/gepi.22295), [ref](https://doi.org/10.1093/ije/dyaa262) and [ref](https://doi.org/10.1016/j.ajhg.2021.05.014)).

The code in this repo is open source, meaning **you** can modify it by initiating a [pull request](https://github.com/noahlorinczcomi/simmr/pulls). We encourage you to make changes to our code with the intention that the community will eventually settle on an accepted standard for how simulations in MR should be performed.

![](https://github.com/noahlorinczcomi/simmr/blob/main/simmr_flowchart.svg)

# Who is this for?
This software is primarily for researchers evaluating the performance of their new or existing MR estimator. This software can also be used by reviewers and others to validate the performance of pre-published manuscripts reporting MR simulations using GWAS summary statistics.

# What is in the software?
This software generates GWAS summary statistics under different scenarios of
- Exposure and outcome GWAS sample overlap [(ref)](https://doi.org/10.1101/2021.06.28.21259622)
- Uncorrelated horizontal pleiotropy [(ref)](https://doi.org/10.1093/ije/dyv080)
- Correlated horizontal pleiotropy [(ref)](https://doi.org/10.1038/s41588-020-0631-4)
- Weak instruments [(ref)](https://doi.org/10.1101/2023.01.10.523480)
- Winner's curse [(ref)](https://doi.org/10.1101/2021.06.28.21259622)
- Linkage disequilibrium between instruments [(ref)](https://doi.org/10.1002/gepi.22506)

that researchers may want to use in the evaluation of univariable or multivariable Mendelian Randomization methods.

# How do I use it?
The main task is downloading three files and making them communicate with each other, which is very easy. 

You can follow these steps:
1) Download the (generate_data.R)[https://github.com/noahlorinczcomi/simmr/blob/main/generate_data.R], [set_params.R](https://github.com/noahlorinczcomi/simmr/blob/main/generate_data.R), and [basic_functions.R](https://github.com/noahlorinczcomi/simmr/blob/main/generate_data.R) files into any folder
2) Start an R session and make this folder your working directory
3) Open the `set_params.R` file and change the parameter settings however you'd like
    - There are descriptions of what each parameter represents within the file itself
4) Run the command on line 33, which is `source('generate_data.R')`
5) All done! Your global R environment will now contain the 10 new objects
    - `bx`: standardized estimates of association between the IVs and the exposure(s)
    - `bxse`: standardized standard errors corresponding to `bx`
    - `by`: standardized estimates of association between the IVs and the outcome
    - `byse`: standardized standard errors correspondings to `by`
    - `mStart`: the number of causal variants you specified for the exposure(s)
    - `mIVs`: the final number of instruments returned
    - `LDMatrix`: the LD matrix for the final set of IVs
    - `RhoME`: a $(p+1)\times(p+1)$ matrix of correlations between errors in GWAS estimates for the outcome and $p$ exposure(s)
        - Some multivariable MR methods such as [MVMR-cML](https://doi.org/10.1016/j.ajhg.2023.02.014) and [MRBEE](https://doi.org/10.1101/2023.01.10.523480) use this matrix to correct for bias from weak instruments
    - `theta`: $p$-length vector of true causal effects
    - `IVtype`: Classification for each IV in data generation: UHP, CHP, Valid. Does not consider weakness!
    - `bxunstd`: unstandardized estimates of association between the final IVs and the exposures 
    - `bxseunstd`: unstandardized standard errors corresponding to `bxunstd`

# Can I add ____ to the simulation?
**YES**

We want this work to be a collaborative effort involving the broader community of MR researchers. Please, if you feel any simulation code contains errors or could be improved in any way, **please initiate a [pull request](https://github.com/noahlorinczcomi/simmr/pulls) and directly modify the code yourself**. 

If you have questions, please contact me: noahlorinczcomi@gmail.com or njl96@case.edu








