---
layout: page
title: Alchemical Calculations for KRAS Nucleotide Binding
description: Free-energy calculations comparing GDP/GTP binding in KRAS wild-type and the G12D, G12C, and G12V oncogenic mutants.
img: /assets/img/T253I.gif # Path to your image
importance: 4
category: Molecular Modeling
---

KRAS G12 mutations are usually explained through one lens: they cripple GTP hydrolysis, so the switch gets stuck "on." That explanation is built almost entirely on hydrolysis kinetics and static structures, and it treats G12C, G12D, and G12V as interchangeable, which the biology says they are not. G12C carries a reactive cysteine that made it the first druggable KRAS mutant, via covalent inhibitors like sotorasib and adagrasib that trap the switch II pocket, while G12D and G12V have no equivalent chemical handle and have stayed far harder to target, with G12D only recently becoming addressable through noncovalent inhibitors. If hydrolysis defects were the whole story, that druggability gap and the differences in downstream signaling bias across the three mutants would be harder to explain. The piece missing from the hydrolysis-only picture is thermodynamics: independent of how fast GTP gets cleaved, does each mutation change how strongly KRAS *prefers* to be bound to GTP over GDP in the first place?

That question is exactly what alchemical free-energy calculations are built to answer, and exactly what static structures or hydrolysis-rate measurements cannot. Rather than simulating the physical (and computationally intractable) process of one nucleotide unbinding while the other binds, alchemical methods construct a nonphysical thermodynamic pathway that "morphs" GTP into GDP directly inside the binding pocket, using a coupling parameter to interpolate between the two end states, and integrate the associated free-energy changes along the way (via thermodynamic integration and multistate free-energy estimators such as MBAR). Run for KRAS wild-type and for G12D, G12C, and G12V under the same protocol, this gives a directly comparable relative binding free energy, ΔΔG, for each mutant against wild-type: a rigorous, physics-based measure of how much each single-residue substitution reshapes the nucleotide-binding pocket's energetics, decoupled from hydrolysis chemistry entirely.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/T253I.gif" title="Alchemical transformation pathway" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Alchemical transformation of the bound nucleotide along a nonphysical coupling coordinate, used to compute relative GDP/GTP binding free energies for KRAS WT and each G12 mutant under an identical protocol.
</div>

This is deliberately the thermodynamic counterpart to the [dynamical network analysis of the same four systems](/projects/05_md_kras_solvation/): that project shows *how* each mutation rewires communication between the P-loop and the switch regions, while this one asks *how much energetic advantage* the GTP-bound state gains from each mutation, or loses, independent of hydrolysis. Together, they turn "G12 mutations lock KRAS on" from a qualitative label into a quantitative, mutant-specific energetic and structural profile, precisely the kind of resolution needed to explain why three mutations at the same codon produce different clinical behavior, and to identify pocket-level energetic differences in G12D and G12V that could be exploited by the next generation of noncovalent KRAS inhibitors, in a field where a covalent handle is not always available.
