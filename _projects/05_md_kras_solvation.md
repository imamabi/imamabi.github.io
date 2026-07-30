---
layout: page
title: MD Simulation for structure-function relationship in EGFR, KRAS and p53 proteins
description: Atomistic molecular dynamics studies of structure-function relationships and mutation-induced effects in EGFR, KRAS, and p53.
img: /assets/img/Structure_function_relationship.png
importance: 1
category: Molecular Modeling
related_publications: true
---

Cancer mutations rarely rewrite a protein wholesale, most swap a single residue. This work asks what that single swap does to the *dynamics* around it: which hydrogen bonds break or form, which surfaces become newly solvent-exposed, and which internal communication pathways between distant regions of the protein get rewired. All-atom molecular dynamics makes those questions answerable, and applying the same analysis lens across three very different oncoproteins, EGFR, KRAS, and p53, turns three separate case studies into one coherent picture of how point mutations convert into biochemical phenotypes.

#### EGFR: how a resistance mutation hides its own drug target

Osimertinib is a third-generation EGFR inhibitor that works by forming a covalent bond to Cys797 in the kinase active site, but tumors on osimertinib reliably develop secondary resistance mutations. We ran all-atom MD on EGFR L858R alone and on the two clinically reported resistant double mutants, L858R/L718Q and L858R/L792H, and tracked the solvent-accessible surface area (SASA) of Cys797 throughout the trajectories.

<div class="row justify-content-sm-center">
    <div class="col-sm-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/EGFR-sasa.png" title="EGFR C797 solvent accessibility across resistance mutations" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The secondary mutations L718Q and L792H each further narrow the SASA distribution of Cys797, the covalent osimertinib target, relative to L858R alone.
</div>

The mechanism turned out to be almost architectural rather than chemical: L718Q and L792H each introduce additional hydrogen bonds between active-site residues and ordered water molecules, and those extra bonds reshape the local secondary structure and flexibility around the ATP pocket enough to reduce Cys797's solvent exposure. A covalent inhibitor that cannot reach its target residue cannot bind it, no matter how favorable the chemistry, so this gives a physical, structure-level explanation for clinically observed osimertinib resistance rather than a purely statistical one, and a concrete design constraint (restore or bypass C797 accessibility) for next-generation inhibitors {% cite Imam2024EGFR %}.

#### KRAS: one mutated codon, three different diseases

KRAS G12 mutations are the most common oncogenic RAS alterations in human cancer, but G12C, G12D, and G12V are not interchangeable. All three impair GTP hydrolysis and lock KRAS toward its active, effector-engaging state, yet they differ in downstream signaling bias and, critically, in druggability: G12C's cysteine thiol enabled the first-ever direct KRAS inhibitors (sotorasib, adagrasib) via covalent trapping in the switch II pocket, while G12D and G12V offer no equivalent reactive handle and remained far harder to drug. That divergence from one shared codon is the puzzle this project is built around.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/KRAS.png" title="Allosteric network coupling in KRAS WT and G12 mutants" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Dynamical network analysis of switch I (SW1), P-loop, switch II (SW2), and interswitch (Inter) coupling in WT and G12C/G12D/G12V KRAS, resolved separately for the GDP-bound (off) and GTP-bound (on) states.
</div>

Rather than treating G12 mutants as three flavors of "always on," we built dynamical network maps from the MD trajectories that trace how motion in the nucleotide-sensing P-loop propagates to the effector-binding switch I and switch II regions, in both the GDP- and GTP-bound states. The nucleotide state alone reshapes the network considerably, and layering each mutation on top produces a distinct rewiring rather than a uniform effect: some mutants largely preserve the wild-type communication pathways while others sparsify the network into a much more disconnected topology. That is the structural argument for why G12C, G12D, and G12V behave as biochemically distinct oncoproteins rather than one lesion with three names, and it sets up the natural next question: exactly how much does each mutation shift the thermodynamics of the nucleotide switch itself, which is what the [alchemical free-energy project](/projects/07_md_alchemical_kras/) was designed to quantify.

#### p53: a hydration pathway to loss of tumor-suppressor function

p53 is inactivated in roughly half of all human cancers, and many of those hits are missense mutations in the DNA-binding domain that destabilize the fold rather than directly disrupting the DNA interface. Thr253 sits in a loop region adjacent to a partially buried Tyr236, and using well-tempered metadynamics to sample the domain's low-probability "breathing" conformations, we found that these two residues are not the well-packed hydrogen-bonded pair that static crystal structures suggest.

<div class="row justify-content-sm-center">
    <div class="col-sm-9 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/p53.png" title="T253X mutations and Tyr236 hydration in the p53 DNA-binding domain" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Mutating Thr253 to Pro, Ala, Asn, or Ile opens a water-accessible channel near the S4-S9 and S6-S7 loops, driving solvent penetration toward Tyr236 that is largely absent in the wild-type packing.
</div>

Substituting Thr253 for proline, alanine, asparagine, or isoleucine consistently opened a channel that let water penetrate toward Tyr236, a residue that is buried and hydrophobically shielded in the properly folded domain. Hydrating an interior residue is an early, sensitive marker of local unfolding, well upstream of the kind of gross structural collapse that is easy to see but too late to intervene on. That gives a mechanistic account of how a single loop-region substitution can destabilize the DNA-binding domain through a specific, trackable hydration pathway, rather than through nonspecific "the protein got looser" reasoning, and it identifies Tyr236 hydration as a candidate early read-out for domain stability in mutation-screening and small-molecule stabilizer efforts {% cite Imam2026p53 %}.
