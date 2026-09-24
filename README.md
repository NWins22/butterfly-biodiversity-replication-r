# Butterfly Biodiversity Replication in R

A reproducible replication of a published ecological study, built with R and Quarto. The project reproduces the study's descriptive statistics, ANOVA results, and detrended correspondence analysis (DCA), then extends the analysis with a correspondence analysis (CA) of log-transformed data.

**[View the full report](https://nwins22.github.io/butterfly-biodiversity-replication-r/)**

## Overview

The goal was to check whether the results of a published butterfly biodiversity study (Loos et al., 2014) could be reproduced from its data, and to interpret what the results mean. Where my numbers differed from the paper's, I documented the differences rather than adjusting the analysis to match.

## Key Findings

- **Descriptive statistics replicated closely.** The most abundant species matched the paper. Small differences appeared in the species richness range (3-47 vs. 3-45 per site) and in the total counts of individuals and species, possibly due to taxonomic inconsistencies in the dataset.
- **Land use had little effect on richness or abundance.** ANOVA showed little difference between arable and grassland sites, consistent with the paper.
- **The DCA reproduced Figure 2** of the paper (without the environmental vectors).
- **DCA was the better ordination for these data.** A CA of log-transformed counts explained only about 10% of the variance on its first two axes and showed an arch effect, which exaggerates group separation.

## Methods

1. Removed forest sites so only arable and grassland sites remained.
2. Separated species counts from environmental variables and dropped species with no occurrences in the remaining sites.
3. Calculated total individuals, species richness, and abundance per site, then compared land-use types with one-way ANOVA.
4. Ran DCA with `vegan::decorana()`.
5. Log-transformed the counts and ran CA with `vegan::cca()`, then compared the result with the DCA.

**Tools:** R, Quarto, `vegan`, `dplyr`, `readxl`

## Repository Structure

```
butterfly-biodiversity-replication-r/
├── README.md
├── analysis/
│   └── butterfly-replication.qmd   # Source code and write-up
├── data/                           # Dataset from Dryad (see Data section)
└── docs/
    └── index.html                  # Rendered report (published via GitHub Pages)
```

## Data

The analysis uses the butterfly survey dataset from Loos et al. (2014), which is publicly available on Dryad:

**[Data from: Low-intensity agricultural landscapes in Transylvania support high butterfly diversity (Dryad, doi:10.5061/dryad.97s1k)](https://doi.org/10.5061/dryad.97s1k)**

The file is included in `data/` as `Loos+et+al+2014+Butterflies.xls`. It contains butterfly counts and environmental variables for each survey site.

## Reproducing the Analysis

1. Install [R](https://www.r-project.org/) and [Quarto](https://quarto.org/).
2. Install the required packages in R:

   ```r
   install.packages(c("readxl", "vegan", "dplyr"))
   ```

3. If `data/` is empty, download the dataset from [Dryad](https://doi.org/10.5061/dryad.97s1k) and save it as `Loos+et+al+2014+Butterflies.xls` in the same folder as the QMD.
4. Render the report from the repository root:

   ```bash
   quarto render analysis/butterfly-replication.qmd
   ```

   The output is a self-contained HTML file in `analysis/`. To publish it, copy it to `docs/index.html`.

## Reference

Loos, J., Dorresteijn, I., Hanspach, J., Fust, P., Rakosy, L., & Fischer, J. (2014). Low-intensity agricultural landscapes in Transylvania support high butterfly diversity: implications for conservation. *PLoS ONE, 9*(7), e103256.

Loos, J., Dorresteijn, I., Hanspach, J., Fust, P., Rakosy, L., & Fischer, J. (2015). *Data from: Low-intensity agricultural landscapes in Transylvania support high butterfly diversity: implications for conservation* [Dataset]. Dryad. https://doi.org/10.5061/dryad.97s1k

## Author

Nikolay Winslow
[LinkedIn](https://linkedin.com/in/nikolay-winslow-2b7b24420) | nwinslow22@outlook.com

Completed as part of graduate coursework in mathematical sciences at the University of Southern Mississippi.
