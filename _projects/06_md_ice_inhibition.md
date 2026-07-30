---
layout: page
title: Ice Growth Inhibition by Antifreeze Peptides
description: A molecular dynamics simulation study on the mechanism of ice growth inhibition.
img: /assets/img/proj6-fixed.png  # Path to your image
importance: 2
category: Molecular Modeling
related_publications: true
---

Finding a peptide that scores well against an ice-binding classifier, or even one that docks stably onto a static ice slab, is not the same as finding a peptide that actually stops ice from growing. A real antifreeze peptide has to survive a moving target: as a crystal grows, it has to stay anchored to its binding face, keep that face locked to the ice lattice, and resist being overtaken or engulfed by the advancing growth front. This project takes the top computational candidates surfaced in the [PLM-guided antifreeze peptide search](/projects/01_ml_peptide_selection/) {% cite Imam2026Discov %} and puts them through exactly that stress test, large-scale, extended-timescale MD at sustained subzero temperature, with an active ice-water interface rather than a static crystal.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/proj6-fixed.png" title="Ice growth inhibition simulation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A candidate peptide positioned at an active ice-water growth interface, run under continuous subzero conditions to test whether its ice-binding face remains locked to the crystal lattice as growth proceeds.
</div>

Classic antifreeze activity works by an adsorption-inhibition mechanism: a peptide that anchors irreversibly to the ice surface forces the growth front to bulge around each pinning point rather than advance past it, and the resulting curvature raises the local melting point at that point enough to halt growth locally, the microscopic basis of the Kelvin (Gibbs-Thomson) effect behind thermal hysteresis. That mechanism only works if the peptide's ice-binding face keeps its structural register with the lattice under sustained thermal and mechanical stress at the interface, so that is exactly what we tracked: whether the ice-binding surface stayed rigid and correctly oriented, whether the peptide's anchoring contacts persisted as the crystal grew around it, and whether pinned peptides produced the expected local curvature at the growth front instead of simply being pushed off or buried.

Framed this way, the simulation is less a single measurement and more a filter that the antifreeze classifier's candidates have to pass before they are credible cryoprotectant leads: peptides that hold their ice-binding geometry under continuous subzero growth pressure are structurally consistent with genuine growth-inhibition activity, while peptides that lose their binding-face register or get engulfed reveal that a favorable static pose was not the whole story. That distinction is what turns this study into a design tool, it tells you which structural features of a candidate peptide are load-bearing for antifreeze function under real, dynamic ice-growth conditions, information a static docking or classification score alone cannot provide.
