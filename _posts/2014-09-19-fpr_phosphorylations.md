---
layout: post
title: FPR phosphorylations (information retrieval)
categories: [FPR to NOX2, ROS signaling]
tags: [FPR, literature]
description: 
Date: 2014-09-19
---

[Maestes et. al.][Maestes:1999] discusses the phosphorylations of the 11 Ser/Thr residues at the carboxyl terminal end of FPR and the effects on desentization and internalization. They are S<sup>319</sup>, T<sup>325</sup>, S<sup>328</sup>, T<sup>329</sup>, T<sup>331</sup>, S<sup>332</sup>, T<sup>334</sup>, T<sup>336</sup>, S<sup>338</sup>, T<sup>339</sup>, and S<sup>342</sup>.

> receptor phosphorylation, desensitization, and internalization are not obligatory steps for chemotaxis[Hsu:1997][Hsu:1997bv].

> phosphorylation of the FPR occurs in a hierarchical manner within a region in which 8 out of 12 continuous residues (between residues 328 –339) are either serine or threonine [Prossnitz:1995][Prossnitz:1995tj]

> Receptor phosphorylation by itself does not appear to prevent coupling to G proteins. Desensitization most likely requires the binding of an accessory molecule, such as arrestin, which specifically binds phosphorylated GPCRs and sterically prevents G protein association

However, [Bennett et al.][Bennet:2001] has shown indications that fMLF-induced phosphorylation of FPR1 can **block FPR1 interaction with G proteins independently of β-arrestin**

> p.29794: these results suggest that in the wild type receptor, phosphorylation probably occurs at minimally three sites, defined by C, D, and B

> p.29795: all partially phosphorylated mutants underwent complete internalization

> p.29795: FPR internalization cannot be responsible for its desensitization

To summarize the above, the S/T residues in question can be divided into three groups, B (T<sup>334</sup>, T<sup>336</sup>, S<sup>338</sup>, T<sup>339</sup>), C (S<sup>328</sup>, T<sup>329</sup>) and D (T<sup>331</sup>, S<sup>332</sup>). Phosphorylation at either B or C and D together (might be enough with only one, but that isn't tested) is enough to get internalization, while both B and C or D is required for desensitization. See Figure 1.

![Figure 1]({{ site.baseurl }}/assets/media/FPR_phosphorylations.svg){:style="width: 100%"}

It is however unclear to me how the FPR can be internalized to 75% but only desensitized to 40% such as is reported for the A-mutant in [Maestes et. al.][Maestes:1999]

The work in [Maestes et. al.][Maestes:1999] was continued in [Potter et. al. in 2006][Potter:2006]. Here they continue to break apart the different phosphorylations and study their effect on desensitization, internalization, and arrestin binding. The serine residues residues S<sup>328</sup>, S<sup>332</sup>, and S<sup>338</sup> are able to promote internalization, desensitization, and arrestin binding when present in isolation. They also states that the fact that the Thr residues get phosphorylated in WT receptor suggests that they may be involved in negative regulation or other aspects of receptor function. Indeed, the addition of T<sup>334</sup>, T<sup>336</sup>, and T<sup>339</sup> to S<sup>338</sup> (the ∆A mutant from [Maestes et. al.][Maestes:1999]) inhibits desensitazation and arresting binding. Since the correlation between arresting binding and desensitization is low in [Potter et. al.][Potter:2006] this also strengthen the results from [Bennett et al.][Bennet:2001] that desensitize FPR1 independent of arrestin even though arrestin binding model in the latter paper doesn't fit the data from Potter et. al.

[Maestes:1999]: https://dx.doi.org/10.1074/jbc.274.42.29791
[Prossnitz:1995tj]: https://dx.doi.org/10.1074/jbc.270.3.1130
[Hsu:1997bv]: https://dx.doi.org/10.1074/jbc.272.47.29426
[Bennet:2001]: https://dx.doi.org/10.1074/jbc.M106414200
[Potter:2006]: https://dx.doi.org/10.4049/jimmunol.176.9.5418
