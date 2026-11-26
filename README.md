# tardi-behavior

Code and data for making the figures and tables in **Kiser et al.** *(DOI TBD)*.

The study pairs field sampling of tardigrades from moss and lichen with 18S rRNA barcoding (to assign individuals to OTUs) and video tracking of locomotion. The notebooks here regenerate the sampling summaries, community comparisons, species-accumulation curve, and the between-OTU comparisons of body size, activity, speed and turning.

> Raw video clips are not in this repository. They are archived on Zenodo: https://doi.org/10.5281/zenodo.24562925

---

## Repository contents

```
tardi-behavior/
├── code sampling analysis.ipynb    # sampling summaries, moss vs. lichen, OTU accumulation
├── code compare otus.ipynb         # locomotion comparisons among OTUs + statistics
├── Tables/                         # tables from the paper (inputs for the notebooks)
├── locomotion/                     # per-OTU tracking summaries (one .xlsx per OTU)
├── otu_colors.xlsx                 # plotting color + marker for each OTU
├── otu_revision.xlsx               # map: OTU name used in files → revised OTU name used in the paper
├── walking pics no background/     # one background-removed image of a walking individual per OTU
│   └── 0 backups or unused/        # alternate / unused images (not used in figures)
└── mapping/species_icons/0 pngs/   # small icons per OTU, used for map and figure lineups
```

### Notebooks

| Notebook | What it does | Paper outputs |
|---|---|---|
| `code sampling analysis.ipynb` | Counts samples with and without tardigrades by substrate (moss / lichen); chi-squared and Fisher's exact tests; tallies the samples, locations and substrates in which each OTU was found; genus-level moss vs. lichen chi-squared test; species-accumulation (sampling saturation) curve, restricted to Ithaca-area samples | Table 1, Supplemental Figure 1, Table 4, accumulation curve |
| `code compare otus.ipynb` | Loads per-OTU tracking data, keeps sequenced individuals (optional), and plots body length, speed, proportion of active individuals ("movers", ≥ 2 body lengths traveled), and speed / bearing change while cruising. Runs Kruskal–Wallis with Dunn's post-hoc tests (Bonferroni) and Cliff's delta, a regression of speed against body length, and an ANCOVA (speed ~ body length + OTU) | Figures 3 and 5, Supplemental Tables 4 and 5 |

Figure-saving lines (`plt.savefig(...)`) and table exports are commented out in the notebooks. Uncomment them to write PNG / XLSX files. Some cells depend on variables set in earlier cells (noted in the notebooks), so run them top to bottom.

### Tables

| File | Contents |
|---|---|
| `Table 1.xlsx` | Sample summary: number of samples, samples with / without tardigrades, % with tardigrades, mean tardigrades per sample (all / moss / lichen) |
| `Table 2.xlsx` | 18S PCR and sequencing success counts |
| `Table 3.xlsx` | OTU list with number of individuals (N) and GenBank accessions and top BLAST hits for 18S, 28S and COI |
| `Table 4.xlsx` | For each OTU: number of samples, locations, and moss / lichen samples in which it occurred |
| `Supplemental Table 1.xlsx` | Environmental samples: `UniqueID`, latitude, longitude, substrate (moss / lichen), location |
| `Supplemental Table 2.xlsx` | Every tardigrade collected: sample ID, tardigrade number, unique ID |
| `Supplemental Table 3.xlsx` | Sequenced individuals: OTU, `SeqID`, notes, trimmed 18S (F566) sequence; one `consensus` row per OTU |
| `Supplemental Table 4.xlsx` | Pairwise Dunn's tests on cruising speed (Z, raw and Bonferroni p, Cliff's delta, effect size) and the adjusted-p matrix |
| `Supplemental Table 5.xlsx` | Pairwise Dunn's tests on bearing change while cruising (same layout as Supplemental Table 4) and the adjusted-p matrix |
| `Table of Materials.xlsx` / `.xls` | Materials and equipment list |

### Locomotion data

Each OTU has one file in `locomotion/` named `<OTU>_combined.xlsx`. Each row is one tracked individual. The columns include:

- **Identity:** `Identifier`, `treatment` (sample), `individual`, `date`, `Scale (pixels in 1mm)`, `# clips`
- **Body size:** `Body Size (mm^2)`, `Body Length (mm)`, `Body Width (mm)`, `Body Width/Length Ratio`
- **Movement:** `Duration analyzed (sec)`, `Distance traveled (mm)`, `Bodylengths traveled`, `Speed (mm/sec)`, `Speed (body lengths / sec)`
- **Cruising:** `Percentage of time cruising`, `Speed (mm/sec cruising)`, `Speed (body lengths / sec cruising)`
- **Turning and stops:** `Total bearing change (deg)`, `Explore index`, `Bearing change (deg) / sec`, `Bearing change (deg) / sec cruising`, `Number of stops`, `Stops / sec`, `Number of turns`, `Turns / sec`

---

## Naming conventions

**Sample and individual IDs.** Samples are `YYYYMMDD-sNN` (collection date + sample number). Individual tardigrades are `YYYYMMDD-sNN-tNN`. A suffix `-pNN` on an image name marks a specific path / clip.

**OTU names.** Files and code use the OTU names assigned at submission (e.g. `Echiniscus_a`). Some were revised for the final paper (e.g. `Echiniscus_a` → *Viridiscus* sp. a). `otu_revision.xlsx` maps one to the other, and the notebooks use it to label figures with the revised names. In `walking pics no background/`, names like `Adropion_a was a2` record an earlier label for the same OTU.

**Locations.** Most samples are from the Ithaca, NY area. A few come from Georgia, Virginia, Puerto Rico and Cranberry Lake, NY. These are excluded from the species-accumulation curve.

---

## Requirements

Python 3 with Jupyter, plus:

```
pandas numpy matplotlib seaborn pillow openpyxl
scipy statsmodels scikit-posthocs scikit-bio
```

For example:

```bash
pip install jupyter pandas numpy matplotlib seaborn pillow openpyxl scipy statsmodels scikit-posthocs scikit-bio
```

## Usage

```bash
git clone https://github.com/enwudz/tardi-behavior.git
cd tardi-behavior
jupyter notebook
```

Open either notebook from the repository root, since the file paths are relative to it, and run the cells in order.

---

## Citation

If you use these data or code, please cite:

> Kiser et al. TBD
