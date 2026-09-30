Stellar electron-capture (EC) and β⁻-decay rates from finite-temperature
FT-HBCS + FT-pnRQRPA calculations with the D3C\* relativistic energy density
functional (DLR: Dasher, Lalit, Ravlic), written in the format of MESA's
`weakreactions.tables`, together with three interactive pages for inspecting
the rates.

## Contents

| File | What it is |
|---|---|
| `weakrates_DLR.tables` | MESA weak-rate table with DLR rates wherever they are available |
| `weakrates_MESA_DLR.tables` | Original MESA table, extended with DLR rates for nuclei it does not contain |
| `beta_EC_rates_viewer.html` | Viewer for the DLR β⁻ and EC rates of all 1234 nuclei |
| `dlr_vs_mesa_comparison.html` | DLR rates compared with the MESA rates they replace |
| `halflives_vs_exp.html` | DLR β⁻ half-lives compared with experiment (NUBASE2020) |

## The two tables

Both files have the layout of MESA's `weakreactions.tables`. They list the
same 1352 reaction pairs (2704 rates) on the same grid: T₉ = 0.01–30
(12 points) and log₁₀(ρYₑ) = 1–11. Each pair X(A,Z) ↔ Y(A,Z−1) gives
positron emission, electron capture and neutrino loss for X → Y
(`lbeta+`, `leps-`, `lnu`), and β⁻ emission, positron capture and
antineutrino loss for Y → X (`lbeta-`, `leps+`, `lnubar`). The source of each
pair is given at the end of its header line.

**`weakrates_DLR.tables`: DLR everywhere possible.**
- 225 of the 231 original pairs use DLR rates.
- Six pairs keep their original entries:
  - p ↔ n (LMP), and ⁴⁰Ti ↔ ⁴⁰Sc and ⁵⁷Zn ↔ ⁵⁷Cu (FFN), because DLR does not have ⁴⁰Ti, ⁵⁷Zn or the free nucleons.
  - ¹⁴N ↔ ¹⁴C (GMP), because the DLR Q value for this pair is far from experiment.
  - The state-resolved ²⁶Al pairs `al-6` and `al*6` ↔ ²⁶Mg (FFN).
- 1121 DLR pairs are appended for nuclei the original table does not have.

**`weakrates_MESA_DLR.tables`: original MESA plus DLR.**
- All 231 original pairs (FFN, OHMT, LMP, GMP) are unchanged.
- The same 1121 DLR pairs are appended.

The appended pairs cover all DLR nuclei, Z = 6–40, and their partners, up to
Z = 41. In 228 of them only one nucleus has DLR data, so only one direction is
filled; the other is −99.999. Examples are EC on the C isotopes (DLR has
no B) and β⁻ of the Zr isotopes (DLR has no Nb).

### What the DLR entries contain

- `leps-` and `lnu` come from the DLR EC rate and neutrino energy loss.
  `lbeta-` and `lnubar` come from the DLR β⁻ rate and antineutrino energy loss.
- Positron emission (`lbeta+`) and positron capture (`leps+`) are not
  computed and are set to −99.999. As a result, `lnu` contains only EC and
  `lnubar` only β⁻.
- The EC rates exclude the 0⁺ multipole.
- DLR rates are computed for T₉ = 1–30 and log₁₀(ρYₑ) = 5–12. Lower
  temperatures repeat the T₉ = 1 values, and lower densities repeat the
  log₁₀(ρYₑ) = 5 values.
- Rates of zero, or below 10⁻⁹⁹·⁹⁹⁹, are written as −99.999.

### Using a table in MESA

MESA reads its weak rates from `weakreactions.tables` in its rates data
directory (`$MESA_DIR/data/rates_data/`). Keep a copy of the original. Copy
one of these tables in its place under that name, and let MESA rebuild any
cached weak-rate data. Details depend on the MESA version.

MESA only uses a pair when both nuclides are in the network of the run.

## Known limitations

- **Low temperature and density.** Below T₉ = 1 and log₁₀(ρYₑ) = 5, the DLR
  entries are copies of the grid-edge values, not calculations. This
  overestimates thermally enhanced rates at low T, and EC rates at low
  density.
- **No positron channels.** Missing β⁺ matters mainly for proton-rich
  nuclei at low density. Missing positron capture matters for neutron-rich
  nuclei at T₉ ≳ 3.
- **Half-lives near stability.** Compared with NUBASE2020 at T₉ = 1:
  - for measured half-lives below 1 s, the DLR β⁻ half-lives agree within a
    factor 10 for 95 % of nuclei (rms 0.47 dex);
  - for longer-lived nuclei near stability the agreement is poor, and 46
    measured β⁻ emitters have a DLR rate of zero.

  See `halflives_vs_exp.html`. For these nuclei,
  `weakrates_MESA_DLR.tables` is the safer choice.

## Interactive pages

The three `.html` files open in any recent web browser. The data is embedded
in each file, but the pages load the Plotly plotting library and the fonts
from public CDNs, so they need an internet connection.

- **`beta_EC_rates_viewer.html`** shows β⁻ rates, EC rates and their ratio for
  all 1234 nuclei on the computed grid (T₉ = 1–30, log₁₀(ρYₑ) = 5–12). It has:
  - a nuclide chart with an adjustable colour range;
  - per-nucleus plots against T and density, the multipole contributions,
    Q_β and the chemical potentials, and the mean lepton energies.
- **`dlr_vs_mesa_comparison.html`** compares DLR with the original table for
  the 226 pairs where DLR replaced a MESA rate. It shows:
  - the differences for each source table, against mass number, and on a
    nuclide chart;
  - a sortable pair list;
  - per-pair plots that include the MESA positron channels.
- **`halflives_vs_exp.html`** compares DLR β⁻ half-lives at T₉ = 1 and
  log₁₀(ρYₑ) = 5 with the NUBASE2020 partial β⁻ half-lives for 465 nuclei. The
  MESA values are shown as a reference.

## References

- DLR: Dasher, Lalit, Ravlic, FT-HBCS+FT-pnRQRPA (D3C\*), this work.
- FFN: G. M. Fuller, W. A. Fowler, M. J. Newman, Astrophys. J. 293 (1985).
- OHMT: T. Oda, M. Hino, K. Muto, M. Takahara, K. Sato, At. Data Nucl. Data Tables (1994).
- LMP: K. Langanke, G. Martínez-Pinedo, Nucl. Phys. A 673 (2000) 481–508.
- GMP: G. Martínez-Pinedo, private communication.
- NUBASE2020: F. G. Kondev, M. Wang, W. J. Huang, S. Naimi, G. Audi, Chin. Phys. C 45, 030001 (2021).
