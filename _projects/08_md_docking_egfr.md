---
layout: page
title: Multi-study workflow (Docking, MD, QM/MM) to prioritize small molecules as potential EGFR inhibitors
description: An integrated workflow combining docking, molecular dynamics, and QM/MM refinement to rank small molecules as potential EGFR inhibitors.
img: /assets/img/proj8-workflow.svg # Path to your image
importance: 3
category: Molecular Modeling
---

Ranking small molecules against a drug target is a classic funnel problem: you need enough throughput to screen a large compound space, but enough physical rigor at the end that the final ranking is actually trustworthy. No single method gives you both. Docking alone is fast but too coarse to trust for a final call; full quantum-mechanical treatment of every compound is accurate but computationally impossible at scale. This project's answer is to chain three methods of increasing cost and increasing physical fidelity, docking, then MD, then QM/MM, so that each stage only has to do the amount of work its narrowing candidate pool actually justifies.

<div class="row justify-content-sm-center">
    <div class="col-sm-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/proj8-workflow.svg" title="Docking, MD, QM/MM funnel" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    High-throughput docking identifies putative binders; MD evaluates which of those survive contact with a flexible, solvated, induced-fit binding site; QM/MM refines the binding energetics of the compounds that make it through.
</div>

High-throughput docking against EGFR wild-type and clinically relevant resistant mutants first identifies putative binders from a large compound library, using a rigid or lightly flexible receptor as the cost of screening at scale. Explicit-solvent MD then takes that shortlist and asks the question docking cannot: does the binding pose actually hold up once the receptor is allowed to move, the binding site is allowed to induced-fit around the ligand, and water is treated explicitly rather than implicitly? Compounds that only look good against a static pocket tend to fall away at this stage. QM/MM calculations are then reserved for the smallest, most promising set, refining binding energetics with an electronic-structure-accurate treatment of the binding site, which matters directly for EGFR inhibitors that engage the kinase covalently: whether a candidate can actually reach and react with Cys797 is exactly the kind of solvent-accessibility and local-geometry question this project's [companion structure-function study](/projects/05_md_kras_solvation/) showed can be disrupted by EGFR's own resistance mutations {% cite Imam2024EGFR %}.

Running docking, MD, and QM/MM as one coherent pipeline, rather than as three disconnected analyses handed off manually between tools, is itself the harder engineering problem, and the reason this workflow was presented at the Platform for Advanced Scientific Computing Conference (PASC '25) as "In-Silico Predictions of Drug Resistance in Lung Cancers with EGFR Mutation," a multi-institution collaboration spanning Lawrence Berkeley National Laboratory and the University of Kentucky. Automating the handoffs between simulation codes, batching jobs across HPC resources, and keeping the pipeline reproducible across wild-type and multiple resistant mutants in parallel is what makes it possible to apply this funnel at a scale that yields an actionable shortlist rather than a handful of one-off calculations, work that ultimately narrowed the field down to 12 candidate compounds recommended for experimental follow-up against EGFR wild-type and its osimertinib-resistant variants.
