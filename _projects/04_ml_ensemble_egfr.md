---
layout: page
title: Develop ML ensemble with late fusion to identify hERG and CYP3K potential binders
description: Building a late-fusion ensemble machine-learning pipeline to identify potential hERG and CYP3A4 binders from molecular features and model outputs.
img: /assets/img/proj3.png # Path to your image
importance: 2
category: Machine Learning
---

hERG channel blockade and CYP3A4-mediated metabolism are two of the most common reasons a promising compound fails late in drug development: hERG inhibition risks cardiac QT-interval prolongation, and CYP3A4 liability drives unpredictable exposure and drug-drug interactions since it metabolizes roughly half of marketed small molecules. Flagging both liabilities early, and flagging compounds that carry both at once, is far cheaper than discovering them in the clinic. This project builds a late-fusion ensemble classifier that predicts hERG and CYP3A4 inhibition from molecular structure, designed so that no single algorithm or single molecular representation can dominate or bias the final call.

#### Data pipeline

1. Download hERG activity data.
2. Download CYP3A4 activity data.
3. Standardize molecule IDs and SMILES.
4. Encode hERG labels (1 = inhibitor, 0 = non-inhibitor).
5. Encode CYP3A4 labels (1 = inhibitor, 0 = non-inhibitor).
6. Create the union dataset for multitask modeling.
7. Create the intersection dataset for four-class analysis (neither / hERG-only / CYP3A4-only / dual liability), which is the split that matters most for prioritization, since a dual hERG/CYP3A4 liability compound is a materially different risk than either liability alone.

#### Two-stage late fusion

For each target, separate base learners were trained for every algorithm-fingerprint combination, spanning three algorithms (XGBoost, LightGBM, Random Forest) and multiple complementary molecular fingerprint representations. Fusing at this level, rather than training one model on one flattened feature vector, means the ensemble can draw on structural information that any single fingerprint alone would miss.

Fusion then happens in two stages:

- **Stage 1, within-algorithm fusion:** for each algorithm, the predicted probabilities from its fingerprint-specific models are averaged, weighted by each model's internal validation average-precision (AP) score. This produces one XGBoost ensemble, one LightGBM ensemble, and one Random Forest ensemble per target.
- **Stage 2, across-algorithm fusion:** the three algorithm-level ensemble probabilities are averaged into a single final model-level prediction.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/proj3-late-fusion.svg" title="Two-stage late-fusion ensemble architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Late fusion happens in two stages: fingerprint-specific base learners are combined within each algorithm (AP-weighted), and the three resulting algorithm-level ensembles are then averaged into one final prediction.
</div>

Weighting by internal validation AP, rather than fusing with uniform weights, lets the ensemble down-rank a fingerprint-algorithm combination that happens to perform poorly for a given target without throwing it out of the architecture entirely. Critically, the external paired hERG/CYP3A4 test set was held out from every step of this process, it was not used to tune base-learner hyperparameters, choose fingerprints, or set fusion weights, so the reported performance reflects genuine generalization rather than indirect overfitting to the evaluation set.

The result is a single, reusable ensemble framework that scores new compounds for hERG and CYP3A4 liability simultaneously, giving medicinal chemistry teams an early, defensible signal for which candidates are safe to advance and which combinations of liabilities warrant a redesign.
