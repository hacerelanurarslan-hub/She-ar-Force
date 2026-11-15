# SHE'AR FORCE — Lunar Landing Site Navigator

[**Explore the interactive public demo**](https://hacerelanurarslan-hub.github.io/She-ar-Force/) *(expected GitHub Pages URL; accessible only after Pages is enabled)*

**NASA Space Apps Challenge 2026** · [Lunar Landing Site Navigator](https://www.spaceappschallenge.org/2026/challenges/lunar-landing-site-navigator/) · Student research prototype.

> **Status:** Preliminary model, not a NASA-certified landing-site assessment. This repository contains team-supplied model output; the upstream JPL Horizons and LOLA calculations have **not been independently reproduced and certified** in this release. The repository's internal data checks are not NASA verification.

## The mission question

How does the lunar south-pole terrain horizon affect visibility of the **Sun** (a geometric proxy relevant to solar planning) and **Earth** (a geometric prerequisite for direct-to-Earth links)? This navigator compares three **research sample points**, lets visitors select a point and play through the modeled time window, and depicts both bodies relative to a **schematic, stylized lunar horizon**.

## Try the demo

- **Website:** `index.html` — standalone HTML/CSS/JavaScript; all three datasets are embedded for offline use. Open it in any modern browser. No Python, login, or API token required.
- **Public URL, once GitHub Pages is enabled:** https://hacerelanurarslan-hub.github.io/She-ar-Force/
- **Source code and original numeric precision:** `science/` (Python analysis and tests, historic Streamlit science pages), especially `science/data/v3/uc_bolge_saatlik_2163_satir.csv`.

## Modeled results: V3 / bilinear skyline

| Sample site (not a certified landing site) | Latitude, longitude | Sun unobstructed | Earth unobstructed | Both unobstructed |
| --- | --- | ---: | ---: | ---: |
| MM-01 — Mons Mouton sample | -85.4°, 31.7° E | 388 / 721 (53.81%) | 690 / 721 (95.70%) | 388 / 721 (53.81%) |
| MMP-02 — Mons Mouton Plateau sample | -84.3°, 30.6° E | 193 / 721 (26.77%) | 436 / 721 (60.47%) | 193 / 721 (26.77%) |
| NR-03 — Nobile Rim 1 vicinity sample | -85.4°, 37.3° E | 216 / 721 (29.96%) | 0 / 721 (0.00%) | 0 / 721 (0.00%) |

**Sampling:** Nov 14, 2026 00:00 UTC — Dec 14, 2026 00:00 UTC, inclusive, in 1-hour steps; **721 samples per site** and **2,163 rows overall**. These fractions are of *sampled instants*, not continuous illumination or contact hours. **NR-03's zero Earth visibility is not independently verified.**

## Technical overview

1. Lunar-observer Sun/Earth azimuth and elevation directions are attributed by the team to NASA/JPL Horizons.
2. The team-supplied LOLA-derived skyline is modeled using 20 m near-field and 80 m far-field terrain resolution, excluding the first 40 m around the observer.
3. Center visibility flag is 1 when `body_elevation_deg > terrain_horizon_deg` at the same azimuth. The overlap flag is 1 when both bodies pass this test at the same sample.
4. The website visualizes precomputed, embedded records; it does **not** fetch live NASA data or recompute the DEM.
5. The animated foreground landscape is **illustrative**, not an accurate georeferenced panorama. Model and interpolation uncertainty remain.

For full limitations read [Methodology](docs/METHODOLOGY.md) and [Validation status](docs/VALIDATION_STATUS.md). Older **V2** single-site results are kept in the Python science folder for historical comparison and **must not be mixed with V3** as if both used identical assumptions.

## Repository guide

| Path | Purpose |
| --- | --- |
| `index.html` | GitHub Pages website; latest corrected English cinematic edition |
| `science/` | Reproducible analysis source modules, tests, optional Streamlit dashboard, historical V2, precomputed V3 data |
| `science/data/v3/` | Full-precision CSV and accompanying JSON / method comparison |
| `tools/verify_embedded_data.py` | Verify HTML arrays and visibility flags against the full-precision V3 CSV |
| `docs/METHODOLOGY.md` | Formulas, parameters, modeling limits, interpretation |
| `docs/SOURCES.md` | NASA/other source links and important provenance caveats |
| `docs/AI_DISCLOSURE.md` | Use of Claude and ChatGPT in project development |
| `docs/THIRD_PARTY_NOTICES.md` | Licenses and source attribution |
| `submission/PROJECT_TEXT_EN.md` | Editable English NASA project-page text |
| `submission/DEMO_SCRIPT_EN.md` | Optional 30-second demo outline; not a substitute for an uploaded public video |

## Run the optional Python science app locally

```bash
cd science
python -m pip install -r requirements.txt
python -m streamlit run Mission_Control.py
```

The standalone website is the recommended judge-facing demo; the Python app provides additional legacy analysis screens. The app is local unless it is separately deployed. `localhost` is **not** a public judging URL.

## Scientific ethics and attribution

- NASA/JPL Horizons and NASA GSFC LOLA resources are **data sources, not endorsements**.
- The landing regions, center-site coordinates, lunar heights, shadowing and communications assumptions are not flight qualified.
- Atmospheric effects, finite apparent discs, eclipses, power-system output, radio link budgets, rover paths and landing hazards are **not** modeled.
- The website and supporting code were built with AI assistance and require team review. See [AI Disclosure](docs/AI_DISCLOSURE.md).

## License

Original project code and documentation are released under **Apache License 2.0** (see [LICENSE](LICENSE)). NASA datasets and third-party resources retain their own terms; this project license does not relicense them. Cite data and software sources. The project is not affiliated with NASA.
