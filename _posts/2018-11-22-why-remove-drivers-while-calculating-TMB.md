---
title: "Why remove drivers while calculating TMB"
excerpt: "Secret in TMB algorithm"
categories:
  - articles
tags:
  - Bioinformatics
---

Tumor mutational burden (TMB) is a measurement of mutations carried by tumor cells and is a predictive biomarker being studied to evaluate its association with response to Immuno-Oncology (I-O) therapy, such as nivolumab, pembrolizumab, and atezolizumab. We should know that TMB is a measurement of the numbers of mutations carried by tumor cells and the real “secret sauce” in TMB is neoantigen, which is a fraction of the mutations present in the tumor cells will code for proteins that presented on the surface of those cells. These make the immune system more likely to recognize the tumor as foreign. 

To precisely calculate TMB, [Daniel Lieber](http://www.dslieber.com/) from FMI has put forward a [method](https://cdn2.hubspot.net/hubfs/174278/Corporate%20Landing%20Pages/042017%20-%20AACR%20Landing%20Page/Lieber,%20D%20AACR%202017%20Tumor%20Mutational%20Burden%20Val_.pdf?t=1493408183691): include removing `polymorphisms` and `predicted drivers`, which has almost become the gold standard across NGS industry when counting TMB. The reason for eliminating polymorphisms is because germline variants contribute little to the neoantigen, but there is no doubt that drivers will produce neoantigens, why it is still necessary to remove them? 

At this part, I am trying to answer this question:

1. Increase TMB value unproperly 
Immunotherapy is a complement choice compared with target therapy. Tumors harboring known drivers (ALK, ROS1, EGFR, BRAF V600E, MET splice) had low TMB (median: 2.5, 3.6, 3.8, 3.8, 4.5)[^1] and should not receive immunotherapy. There is a study suggest that immunotherapy is not useful for EGFR-mutant lung cancer[^2], The benefit in OS was realized in patients with EGFR wild-type tumors (HR: 0.67; P < 0.001), but not in patients with EGFR-mutated NSCLC (HR: 1.11; P=0.54). If we take driver mutations into account, it will increase the TMB score and potential direct to immunotherapy by mistake. To avoid the accident, we should remove drivers.

2. Increase bias
NGS companies design panels for target hotspots on driver genes, and the TMB score is a by-product from this angle. Therefore, keeping drivers will yield bias while fitting the concordance curve between WES-TMB and Panel-TMB. Regularly, we design a panel for target therapy and including a large number of driver mutations, keep them when counting TMB will lead to a lower concordance score comparing with removing them.

By and large, we should remove drivers when counting TMB. I think the reasons I have posted above is of course not the best version, if someone has a better explanation, please leave a comment.


[^1]: Schrock A, Sharma N, Peled N, et al. MA14. 01 Updated Dataset Assessing Tumor Mutation Burden (TMB) as a Biomarker for Response to PD-1/PD-L1 Targeted Therapies in Lung Cancer (LC)[J]. Journal of Thoracic Oncology, 2017, 12(1): S422.
[^2]: Lee C K, Man J, Lord S, et al. Clinical and molecular characteristics associated with survival among patients treated with checkpoint inhibitors for advanced non–small cell lung carcinoma: a systematic review and meta-analysis[J]. JAMA oncology, 2018, 4(2): 210-216.
