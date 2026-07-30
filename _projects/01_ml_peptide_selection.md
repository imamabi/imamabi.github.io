---
layout: page
title: Integrating Protein Language Model and MD Simulation to discover functional peptides
description: Combining protein language models and molecular dynamics to discover and validate antifreeze and antibiofouling functional peptides.
img: /assets/img/proj2-peptide-workflow.svg
importance: 1
category: Machine Learning
related_publications: true
---

Natural microbiomes carry an enormous, mostly untested reservoir of peptide sequences, but wet-lab screening for a specific function (does this peptide bind ice? does it resist protein fouling?) does not scale to tens of thousands of candidates. This project builds a computational funnel that does: a protein language model (PLM) ensemble first narrows a large sequence library down to a mechanistically plausible shortlist, and explicit-solvent molecular dynamics then stress-tests those candidates against the physics of the target environment. The same pipeline was applied to two different design problems, published separately as {% cite Imam2026Discov %} (antifreeze) and {% cite Imam2025Antibiofouling %} (antibiofouling).

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/proj2-peptide-workflow.svg" title="PLM + MD discovery pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Shared discovery pipeline: a microbiome sequence library is filtered by an ensemble of protein-language-model classifiers, and the resulting shortlist is validated by explicit-solvent MD before a peptide is called a candidate.
</div>

#### Antifreeze peptides (Journal of Materials Chemistry B, 2026)

Antifreeze peptides slow ice recrystallization and are of direct interest for cryopreservation of cells and tissue, food storage, and anti-icing coatings, but known sequences are sparse and structurally diverse, which makes simple homology search a poor discovery tool. We instead treated antifreeze activity as a sequence-classification problem: 10 independent classifiers were built by prompt/adapter-tuning the ESM2 protein language model on different partitions of a curated training set of 73,766 labeled sequences, and their outputs were combined with a random-forest meta-learner into a single ensemble score. Applying this ensemble to 56,008 amino-acid sequences drawn from an Arctic microbiome library produced a ranked shortlist of previously uncharacterized antifreeze peptide candidates.

Because a high PLM score is a statistical association, not proof of ice-binding competence, every top-ranked candidate was then run through explicit-solvent MD in contact with an ice slab. These simulations tracked whether the peptide adsorbed to the ice growth front, whether it adopted an ice-binding-competent conformation once bound, and whether that binding was strong enough to pin the interface rather than being pushed off as the crystal grew — the same structural hallmarks used later in the [ice growth inhibition study](/projects/06_md_ice_inhibition/) to interrogate how these peptides behave under sustained subzero stress.

#### Antibiofouling peptides (Langmuir, 2025)

Antibiofouling peptides work by the opposite logic: instead of ordering water at an ice front, they maintain a disordered hydration layer at a surface that keeps proteins from adsorbing nonspecifically. Very few such sequences had been described, which limits how well existing designs generalize across applications, so we searched the same class of microbiome sequence libraries for candidates. The classifier architecture mirrored the antifreeze study, an ensemble of 10 ESM2 classifiers fine-tuned by prompt-tuning on distinct training partitions, fused through a random-forest meta-learner, giving a single model family that could be repointed at a new peptide function simply by retraining on function-specific labels.

Top-scoring candidates were again evaluated with explicit-solvent MD, here focused on interfacial water structure and residue-level contact behavior at the surface, to separate peptides that plausibly maintain a protective hydration layer from those that merely resemble known nonfouling motifs in sequence space.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Pep.png" title="Ranked peptide candidate structures" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Representative top-ranked candidates emerging from the PLM ensemble, spanning helical, extended, and disordered folds, before MD-based structural and interfacial screening.
</div>

Both studies rely on the same underlying design principle: let a language model handle the combinatorial scale of sequence space, and let physics-based simulation handle the question a language model cannot answer on its own — whether the molecule actually behaves the way its sequence suggests once placed at a real interface.
