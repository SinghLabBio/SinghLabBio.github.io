---
title: Systems biophysics for precision oncology - mapping mutant effects onto drug efficacy 
---

## Clinical variants are too rare for statistical inference alone.<br>Physical priors are needed. 

__*Individually occurring clinical variants are too infrequent to statistically infer their impact on a tumor, or therapeutic efficacy*__. 
Up to 40% of tumors have therapeutic resistance, spanning treatment insensitivity to compensatory mechanisms.
Our lab seeks to bridge this gap using biophysical priors to create a mechansitic atlas of clinical variants. 

Our work falls into three broad themes:

## 1. Mapping variant effects onto drug resistance, selectivity, and sensitivity 

A clinical mutation may induce resistance by directly *decreasing* drug binding affinity, *increasing* protein activity, *alter* signaling pathways by perturbing protein-protein interactions, or *retuning* a target’s inhibitor sensitivity profile. 
By iterating between computational modeling and biophysical/biochemical experiments, __we seek to classify and predict the impact of mutations on small-molecule inhibitor binding to identify drug-resistant and newly-sensitized mutants__


{{< side src="images/website-science/alchemical-mutation.gif" width="40%" caption="Non-equilibrium methods are our go-to" >}}
We have previously shown that modern alchemical methods are capable of classifying kinase mutations as drug-resistant or sensitizing[1].

On the methods side, we develop tools and methods to ensure that alchemical transformations are sampled sufficiently to converge to accurate predictions[2].
{{< /side >}}


{{< side src="images/website-science/mms-summary-image.png" width="40%" pos="left" caption="No kinase inhibitor is perfectly selective!" >}}
Moving forward, we are also interested in how polypharmacy (the use of multiple inhibitors) can target multiple proteins to overcome resistance. Our previous efforts in this realm led to the development of the multicompound–multitarget scoring (MMS) method[3], an approach to predict combinations of kinase inhibitors that reduce off-target binding while maintaing on-target binding.
{{< /side >}}


## 2. Understanding how mutations shift protein conformational populations to re-tune activity, binding, and signaling

Protein mutations can alter the conformational ensemble a protein adopts, which can in turn alter its binding interfaces and interactions with other proteins.
These ensembles report on key biophysical properties (populations and rates) that inform both drug binding and protein function. 
To understand how mutations alter conformational populations and rates, we take advantage of modern day structure-based AI/ML approaches to *seed* distributions of conformations and sample the conformational ensemble a protein adopts, an approach we call *__Transfer Seeding__*:


{{< side src="images/website-science/2026-transfer-seeding.gif" width="40%" pos="right" caption="No kinase inhibitor is perfectly selective!" >}}
By transfer-seeding protein mutants, we can construct atlases of protein conformational population shifts and observe how mutants alter thermodynamics and kinetics shift ensembles to create drug-insensitive states (causing resistance)...
{{< /side >}}

{{< side src="images/website-science/menin-pop-shift.png" width="70%" pos="left" caption="Beyond kinases, we see population shifts in other systems" >}}
or shifting towards more incompatible drug binding states that retune signaling networks....
{{< /side >}}


## 3. Learning about protein allostery and the dynamics-to-function relationship

At the fundamental level, we are interested in how dynamics drives protein function and how distal regions (and variants) of a protein regulate binding interfaces and activity.


This distal regulation, often called *__allostery__*, drives many cellular functions, but atomic-level quantitative descriptions of allostery remain elusive. 
Understanding allosteric coupling in proteins presents new opportunities for modulating biological processes, designing
therapeutics, or optimizing protein designs and their binding interfaces!
__We seek to understand and exploit allosteric regulation of binding interfaces using mutations and ligands that tap into existing allosteric networks.__


{{< side src="images/website-science/gdpRelease_strikingImage_color.png" width="55%" pos="right" caption="Allostery in activation!" >}}
We draw upon fundamental physical ideas (like dynamical heterogeneity) to construct predictive models of allosteric networks that can be used to modulate protein structure and dynamics.

Our previous efforts led to the Correlation of All Rotameric and Dynamical States (CARDS) which infers allostery both via concerted changes in protein structure and in correlated changes in conformational entropy (dynamic allostery).
Applications of CARDS enabled us to understand G protein activation, study potentially druggable pockets in ebolavirus VP35, and how a allosteric motions in \(beta)\-lactamase regulates activity [1][2].
{{< /side >}}

<!-- 
https://elifesciences.org/articles/38465 -->



## Our tools and methods

We are a hybrid lab of quantitative biologists, computational chemists, and experimental biophysicists.
We pair our simulations with experimental validation to study how mutations may alter protein-ligand interactions, including approaches like NanoBRET and turn-on fluorescence.

There are many mutations to map onto mechanistic descriptions. To tackle the data-hungry needs of our models, we approach this problem at scale: 

1. __Modern-day automation tooling to generate datasets and test hypotheses systematically:__ 


{{< side src="images/website-science/Time Lapse-Src Bos-12494.gif" width="75%" pos="right" caption="Allostery in activation!" >}}
Our lab has a combination of liquid handling robotics, small-volume liquid dispensers, and high-throughput plate readers to generate large-scale datasets for our studies.
{{< /side >}}

2. __Massively distributed computing architectures to run our simulations at scale:__ Our lab is a member of the [Folding@home](https://foldingathome.org/) distributed computing consortium, where citizen scientists donate their idle computing time to help us study conformational ensembles and many mutations at once using molecular simulation.

3. __Develop methods combining biophysics, computational chemistry, and modern AI/ML tooling:__ Our methods devlopment efforts focus on the need to 1. generate, 2. analyze, and 3. interpret protein conformational ensembles or large-scale experimental datasets. While human-error is always present, we try to use modern statistical inference methods, machine learning, and AI/ML tools to identify principled, unbiased descriptions that enable data-efficient studies of protein variants, conformational populations, and drug binding.

