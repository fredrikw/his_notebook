---
layout: post
title: Analysis of first set of inhibition experiments
categories: [FPR to NOX2, ROS signaling]
tags: [NOX2, in vitro]
description:
Date: 2015-03-11
---
(This post is mainly created by nbconvert from the actual analysis ipython notebook with some modifications to match the ONS format).

# Analysis of inhibition experiments

Francesco de Luca has performed a first set of four experiments where the
inhibitors 'Go6983', '8Br-cADPR', '2-ADP', 'Wortmannin', 'BIRB796', 'SCH772981'
have been combined with different NOX2 activators, both FPR-agonists and others.

In this notebook, these data are analyzed to see the effects of the inhibitors
on activators with different MOA to try to better understand the signaling
between FPR and NOX2.

### Data import and formatting
We'll start by importing and format the data.


    %matplotlib inline


    import pandas as pd


    fdl_150226_datafile = pd.ExcelFile("1502026_data+kinetics.xlsx")
    fdl_150228_datafile = pd.ExcelFile("1502028_data+kinetics.xlsx")
    fdl_150306_datafile = pd.ExcelFile("150306_data+kinetics.xlsx")
    fdl_150309_datafile = pd.ExcelFile("150309_data+kinetics.xlsx")


    fdl_150226_data = fdl_150226_datafile.parse("Sorted_data", parse_cols="A:D,G:AH")
    fdl_150226_data.ix[[i in ['30 ng/mL', '200 nM', '25 μM', 'P. Control', 'N. Control'] for i in fdl_150226_data["Activator"]], "Activator"] = pd.np.nan
    fdl_150226_data.replace("-", pd.np.nan, inplace=True)
    fdl_150226_data.dropna(inplace=True, subset=["Final Conc"])
    fdl_150226_data.fillna(method='ffill', inplace=True)
    fdl_150226_data['repl'] = fdl_150226_data.Replicate.str.replace('.*\.', '')
    fdl_150226_data.repl.fillna(value=fdl_150226_data.Replicate, inplace=True)
    fdl_150226_data.replace(['α.*', 'β.*', 'γ.*', 'δ.*', 'ε.*', 'ζ.*'], ['Go6983', '8Br-cADPR', '2-ADP', 'Wortmannin', 'BIRB796', 'SCH772981'], inplace=True, regex=True)
    fdl_150226_data.rename(columns={'Replicate': 'Inhibitor', 'AUC ': 'AUC'}, inplace=True)
    fdl_150226_data.Inhibitor[fdl_150226_data.Inhibitor.isin([1,2,3,4])] = ""
    fdl_150226_data.set_index(["Activator", "Inhibitor", "Final Conc", "repl"], inplace=True)


    fdl_150228_data = fdl_150228_datafile.parse("Sorted_data", parse_cols="A:D,G:AH")
    fdl_150228_data.ix[[i in ['30 ng/mL', '200 nM', '25 μM', 'P. Control', 'N. Control'] for i in fdl_150228_data["Activator"]], "Activator"] = pd.np.nan
    fdl_150228_data.replace("-", pd.np.nan, inplace=True)
    fdl_150228_data.dropna(inplace=True, subset=["Final Conc"])
    fdl_150228_data.fillna(method='ffill', inplace=True)
    fdl_150228_data['repl'] = fdl_150228_data.Replicate.str.replace('.*\.', '')
    fdl_150228_data.repl.fillna(value=fdl_150228_data.Replicate, inplace=True)
    fdl_150228_data.replace(['α.*', 'β.*', 'γ.*', 'δ.*', 'ε.*', 'ζ.*'], ['Go6983', '8Br-cADPR', '2-ADP', 'Wortmannin', 'BIRB796', 'SCH772981'], inplace=True, regex=True)
    fdl_150228_data.rename(columns={'Replicate': 'Inhibitor', 'AUC ': 'AUC'}, inplace=True)
    fdl_150228_data.loc[fdl_150228_data.Inhibitor.isin([1,2,3,4]), 'Inhibitor'] = ""
    fdl_150228_data.set_index(["Activator", "Inhibitor", "Final Conc", "repl"], inplace=True)


    fdl_150306_data = fdl_150306_datafile.parse("Sorted_data", parse_cols="A:D,G:AH")
    fdl_150306_data.ix[[i in ['30 ng/mL', '200 nM', '25 μM', 'P. Control', 'N. Control'] for i in fdl_150306_data["Activator"]], "Activator"] = pd.np.nan
    fdl_150306_data.replace("-", pd.np.nan, inplace=True)
    fdl_150306_data.dropna(inplace=True, subset=["Final Conc"])
    fdl_150306_data.fillna(method='ffill', inplace=True)
    fdl_150306_data['repl'] = fdl_150306_data.Replicate.str.replace('.*\.', '')
    fdl_150306_data.repl.fillna(value=fdl_150306_data.Replicate, inplace=True)
    fdl_150306_data.replace(['α.*', 'β.*', 'γ.*', 'δ.*', 'ε.*', 'ζ.*'], ['Go6983', '8Br-cADPR', '2-ADP', 'Wortmannin', 'BIRB796', 'SCH772981'], inplace=True, regex=True)
    fdl_150306_data.rename(columns={'Replicate': 'Inhibitor', 'AUC ': 'AUC'}, inplace=True)
    fdl_150306_data.loc[fdl_150306_data.Inhibitor.isin([1,2,3,4]), 'Inhibitor'] = ""
    fdl_150306_data.set_index(["Activator", "Inhibitor", "Final Conc", "repl"], inplace=True)


    fdl_150309_data = fdl_150309_datafile.parse("Sorted_data", parse_cols="A:D,G:AH")
    fdl_150309_data.ix[[i in ['30 ng/mL', '200 nM', '25 μM', 'P. Control', 'N. Control'] for i in fdl_150309_data["Activator"]], "Activator"] = pd.np.nan
    fdl_150309_data.replace("-", pd.np.nan, inplace=True)
    fdl_150309_data.dropna(inplace=True, subset=["Final Conc"])
    fdl_150309_data.fillna(method='ffill', inplace=True)
    fdl_150309_data['repl'] = fdl_150309_data.Replicate.str.replace('.*\.', '')
    fdl_150309_data.repl.fillna(value=fdl_150309_data.Replicate, inplace=True)
    fdl_150309_data.replace(['α.*', 'β.*', 'γ.*', 'δ.*', 'ε.*', 'ζ.*'], ['Go6983', '8Br-cADPR', '2-ADP', 'Wortmannin', 'BIRB796', 'SCH772981'], inplace=True, regex=True)
    fdl_150309_data.rename(columns={'Replicate': 'Inhibitor', 'AUC ': 'AUC'}, inplace=True)
    fdl_150309_data.loc[fdl_150309_data.Inhibitor.isin([1,2,3,4]), 'Inhibitor'] = ""
    fdl_150309_data.set_index(["Activator", "Inhibitor", "Final Conc", "repl"], inplace=True)

### Calculations of FC
To improve the interexperiment interpretability, each experiment is normalized
to DMSO control by deviding the AUC value with the mean AUC value from four
replicate blank DMSO samples.


    for data in [fdl_150226_data, fdl_150228_data, fdl_150306_data, fdl_150309_data]:
        DMSO_FC = data.convert_objects(convert_numeric=True).groupby(level="Activator").mean().loc["DMSO", "AUC"]
        data["FC_vs_DMSO"] = data.convert_objects(convert_numeric=True).loc[:, "AUC"] / DMSO_FC

### Plotting
For each activator, the FC vs DMSO is plotted in a bar chart where the inhibitor
and concentration is varied on the x axis.


    import matplotlib.pyplot as plt


    fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12,8))

    for x, y, exp, data in zip([0, 0, 1, 1], [0, 1, 0, 1], ["fdl_150226", "fdl_150228", "fdl_150306", "fdl_150309"], [fdl_150226_data, fdl_150228_data, fdl_150306_data, fdl_150309_data]):
        data.ix[("WM",), "FC_vs_DMSO"].plot(ax = axes[x, y], kind='bar', color=['b', 'b', 'b', 'b', 'b', 'b', 'r', 'r', 'r', 'r', 'r', 'r'])
        axes[x, y].set_title(exp)

    fig.suptitle("WKYMWM")








![png]({{ site.baseurl }}/assets/media/150311_Data%20overview_FW_14_1.png)



    fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12,8))

    for x, y, exp, data in zip([0, 0, 1, 1], [0, 1, 0, 1], ["fdl_150226", "fdl_150228", "fdl_150306", "fdl_150309"], [fdl_150226_data, fdl_150228_data, fdl_150306_data, fdl_150309_data]):
        data.ix[("Wm",), "FC_vs_DMSO"].plot(ax = axes[x, y], kind='bar', color=['b', 'b', 'b', 'b', 'b', 'b', 'r', 'r', 'r', 'r', 'r', 'r'])
        axes[x, y].set_title(exp)

    fig.suptitle("WKYMWm")








![png]({{ site.baseurl }}/assets/media/150311_Data%20overview_FW_15_1.png)



    fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12,8))

    for x, y, exp, data in zip([0, 0, 1, 1], [0, 1, 0, 1], ["fdl_150226", "fdl_150228", "fdl_150306", "fdl_150309"], [fdl_150226_data, fdl_150228_data, fdl_150306_data, fdl_150309_data]):
        data.ix[("fMLF",), "FC_vs_DMSO"].plot(ax = axes[x, y], kind='bar', color=['b', 'b', 'b', 'b', 'b', 'b', 'r', 'r', 'r', 'r', 'r', 'r'])
        axes[x, y].set_title(exp)

    fig.suptitle("fMLF")








![png]({{ site.baseurl }}/assets/media/150311_Data%20overview_FW_16_1.png)



    fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12,8))

    for x, y, exp, data in zip([0, 0, 1, 1], [0, 1, 0, 1], ["fdl_150226", "fdl_150228", "fdl_150306", "fdl_150309"], [fdl_150226_data, fdl_150228_data, fdl_150306_data, fdl_150309_data]):
        data.ix[("PMA",), "FC_vs_DMSO"].plot(ax = axes[x, y], kind='bar', color=['b', 'b', 'b', 'b', 'b', 'b', 'r', 'r', 'r', 'r', 'r', 'r'])
        axes[x, y].set_title(exp)

    fig.suptitle("PMA")








![png]({{ site.baseurl }}/assets/media/150311_Data%20overview_FW_17_1.png)


## Summary
To summarize the data, Go6983 inhibits all activators in a dose-dependant
manner, indicating the importance of PKC in the NOX2 activation. Other than
that, Wortmannin is inhibiting the FPR-signaling activators, albeight to a much
lesser extent.

The other inhibitors have only week tendancies towards an effect and nothing
that can be used to draw any conclusions.

## Continuation
To further study the inhibitors, combinations should be tested.

- Add lowest concentration Go6983 (31 nM) to all other inhibitors att all
concentrations
- Combine 8Br-cADPR and 2-ADP since both should inhibit different Ca-transports
    - First experiment, add high conc to high conc, medium to medium and low to
low
- Combine BIRB796 and SCH77298 since ERK and p38 could compensate for each other
    - Again, add high to high etc.
