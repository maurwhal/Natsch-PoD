# Natsch PoD Calculator — *Marvelous Maura Model* (v5)

Implements equations **EQ1, EQ4, EQ5, EQ6, EQ7** exactly as in the Natsch calculator templates. **Defaults and normalizations match the papers.**

This is a single‑page app to compute **pEC3/EC3** from in‑vitro KE data (kDPRA, KeratinoSens™, h‑CLAT) and vapor pressure. Usage: open `index.html`, enter values (µM or µg/mL; auto‑conversion provided), then **Calculate** to see all five equations.

> pEC3 = log10(MW / EC3)  →  EC3 = MW / 10^{pEC3}

**Publish on GitHub Pages:** upload `index.html` to a public repo (root), then Settings → Pages → Deploy from a branch → `main` / `(root)`.

— Updated 2025-09-02
