# Open Chromatin Evolution and Human-Accelerated Regions

This repository presents a cross-species comparative genomics pipeline to identify **human-accelerated regulatory regions (HARs)** based on predicted open chromatin activity. By integrating ATAC-seq derived CNN models with phylogenetic data, molecular distances, and longevity traits, we study the evolution of regulatory DNA across mammals with a focus on the primate brain.

## Project Overview
We investigate the evolutionary trajectory of chromatin accessibility using:
- Machine learning predictions of ATAC-seq peaks across 222 species
- Whole-genome alignments from Zoonomia and molecular distance matrices
- Comparative modeling of evolutionary decay and divergence from mouse
- Statistical association of open chromatin signals with longevity traits

The project outputs enhancer-like regions with elevated activity in humans and evaluates their evolutionary relevance.

## Objectives
- Quantify chromatin accessibility at orthologous motor cortex regions
- Measure evolutionary decay of open chromatin signal across species
- Build phylogenetic and distance-based trees from sequence similarity and predicted activity
- Identify HARs by statistical contrast between human and non-human primates
- Model enhancer-longevity relationships using phylogenetic linear models (phylolm)

## Dataset Description
| File Name                                          | Description                                                         |
|---------------------------------------------------|---------------------------------------------------------------------|
| `m1.peakPred.1.csv`                               | CNN-based predicted ATAC-seq signals for 222 species                |
| `m1.peaks.hg38.bed`                               | Coordinates of mouse motor cortex peaks                             |
| `ZoonomiaGenomeInfo_3.csv`                        | Metadata on evolutionary splits, genome quality, and longevity      |
| `200Mammal_hal_tree_noancestors_matrix.csv`       | Pairwise molecular similarity matrix                                |
| `Zoonomia_ChrX_lessGC40_241species_30Consensus.tree` | Zoonomia phylogenetic tree                                      |
| `pantheriaLongevity.csv`                          | Species lifespan data                                               |

**Packages Used:** `edgeR`, `ggplot2`, `ape`, `phylolm`

## Pipeline Summary

### 1. Chromatin Accessibility and Evolutionary Distance
- Parse and reshape predicted ATAC-seq matrix (rows: peaks, cols: species)
- Map predicted activity to peak coordinates and species metadata
- Correlate chromatin decay with molecular (CACTUS) and chronological (MYA) distances from mouse
- Perform scatterplot and smoothing to visualize decay patterns

### 2. Human-Accelerated Region Detection
- Define foreground: Homo sapiens, Pan troglodytes, Pan paniscus
- Define background: other Old World monkeys and apes (MYA 7-30)
- Perform t-tests on each peak; adjust p-values using Benjamini-Hochberg FDR
- Export top HAR as `.bed` file and inspect predicted chromatin values

### 3. Tree and Subtree Analysis
- Visualize phylogenetic trees using molecular and chromatin similarity
- Compare clustering methods: average vs single linkage
- Render fan-style trees colored by evolutionary decay and species group (mouse, rat, primates)
- Subset rodent-specific trees from Zoonomia to focus on target clades

### 4. Longevity Association
- Merge longevity values with peak predictions across foreground/background species
- Use `phylolm()` to regress peak activity against longevity in the context of shared ancestry
- Visualize regression and print model summary

## Visualizations

### 1. Fan Plot - Evolutionary Tree with Decay Gradient  
Visualizes chromatin-based evolutionary tree with tip colors scaled by molecular distance.  
<img width="373" alt="Screenshot 2025-04-21 at 4 14 27 PM" src="https://github.com/user-attachments/assets/66aeeb32-7b19-4929-9120-6955ce5c866a" />

### 2. Longevity vs Enhancer Activity  
Scatter plot showing lifespan correlation with predicted enhancer signal across clades.  
<img width="411" alt="Screenshot 2025-04-21 at 4 13 56 PM" src="https://github.com/user-attachments/assets/756eed03-c425-4ad1-8288-730a8c994944" />

### 3. Evolutionary Decay vs Molecular Distance  
Non-linear decay of enhancer signal compared to molecular evolution across species.  
<img width="410" alt="Screenshot 2025-04-21 at 4 15 36 PM" src="https://github.com/user-attachments/assets/56c45a48-4a78-4fd6-8d0e-b2bf3c232882" />

## Tech Stack
- **Languages**: R (data.table, ggplot2, ape, phylolm)
- **Data Sources**: Zoonomia, Pantheria, UCSC genome alignments
- **Statistical Tests**: t-test, correlation (Pearson), regression with phylogenetic correction
- **Tree Tools**: ape, drop.tip, hclust, plot.phylo

## Scalability
- Generalizable to other tissues beyond motor cortex
- CNN-based predictions allow flexibility across genomes
- Easily extended to enhancer-to-trait mapping (e.g., lifespan, brain size, etc.)

## Example Applications
- Cross-species enhancer evolution studies
- HAR discovery using non-traditional phenotypes (e.g., longevity)
- Linking molecular evolution to functional regulatory elements

## License
MIT License
