# Evolutionary Analysis of Human-Accelerated Open Chromatin Regions

This repository presents a bioinformatics pipeline to identify human-accelerated genomic regions based on machine learning predictions of chromatin accessibility across mammalian species. The analysis integrates CNN-based predictions, phylogenetics, evolutionary distance modeling, and longevity association using statistical and comparative approaches.

## Project Overview
The goal of this project is to understand chromatin evolution by:
- Predicting open chromatin accessibility using CNNs trained on ATAC-seq data
- Comparing evolutionary divergence using molecular (CACTUS) and fossil (MYA) distances
- Identifying human-accelerated peaks (HARs) across 222 mammalian species
- Associating open chromatin changes with lifespan using phylogenetic models

## Objectives
- Load and preprocess chromatin accessibility predictions across species
- Correlate chromatin predictions with evolutionary divergence
- Build and compare evolutionary trees using molecular and chromatin distance
- Identify peaks with significant acceleration in humans and apes
- Assess association with longevity using phylogenetic linear modeling

## Dataset Description

| File Name                                             | Description                                                           |
|------------------------------------------------------|-----------------------------------------------------------------------|
| `m1.peakPred.1.csv`                                  | CNN-based predicted ATAC-seq signals for 222 species                  |
| `m1.peaks.hg38.bed`                                  | Coordinates of mouse motor cortex peaks                               |
| `ZoonomiaGenomeInfo_3.csv`                           | Metadata on evolutionary splits, genome quality, and longevity        |
| `200Mammal_hal_tree_noancestors_matrix.csv`          | Pairwise molecular similarity matrix                                  |
| `Zoonomia_ChrX_lessGC40_241species_30Consensus.tree` | Zoonomia phylogenetic tree                                            |
| `pantheriaLongevity.csv`                             | Species lifespan data                                                 |

**Packages Used:** `edgeR`, `ggplot2`, `ape`, `phylolm`

## Pipeline Summary

### 1. Data Import and Preprocessing
- Load chromatin prediction matrix and align with peak and species metadata
- Format molecular distance matrices and evolutionary time splits

### 2. Tree Construction and Distance Analysis
- Visualize the Zoonomia consensus tree and chromatin-based clustering
- Compare phylogenetic trees built from molecular vs chromatin predictions

### 3. Evolutionary Trends
- Assess correlation between chromatin predictions and evolutionary divergence
- Compare MYA (fossil) vs molecular (CACTUS) distances to validate evolutionary models

### 4. Detection of Human-Accelerated Regions (HARs)
- Perform t-tests across species groups (human vs monkeys)
- Adjust for multiple testing and isolate significantly accelerated peaks

### 5. Longevity Association
- Integrate lifespan data and test correlation with HARs using phylogenetic regression
- Visualize enhancer-longevity correlation across mammalian clades

## Key Results
- Strong negative correlation between molecular distance and chromatin accessibility (r = -0.88)
- Clear evolutionary separation of chromatin decay by clade
- Identified top HARs including peak30619_mo with strong species-specific divergence
- Phylogenetic regression suggests a potential link between enhancer activity and longevity

## Visualizations

### 1. Fan Plot - Evolutionary Tree with Decay Gradient  
Visualizes chromatin-based evolutionary tree with tip colors scaled by molecular distance.  
<img width="373" alt="Screenshot 2025-04-21 at 4 14 27 PM" src="https://github.com/user-attachments/assets/3baa6f2d-18be-4cb7-8a83-47cf28421797" />

### 2. Longevity vs Enhancer Activity  
Scatter plot showing lifespan correlation with predicted enhancer signal across clades.  
<img width="411" alt="Screenshot 2025-04-21 at 4 13 56 PM" src="https://github.com/user-attachments/assets/e9898326-d652-4129-9bbd-8a23a4d2df38" />

### 3. Evolutionary Decay vs Molecular Distance  
Non-linear decay of enhancer signal compared to molecular evolution across species.  
<img width="410" alt="Screenshot 2025-04-21 at 4 15 36 PM" src="https://github.com/user-attachments/assets/83134bd6-a67e-45a7-9759-40420fef7395" />

## Tech Stack
- **Languages**: R
- **Packages**: edgeR, ggplot2, ape, phylolm
- **Data Formats**: BED, CSV, Newick, Distance Matrix

## Scalability
This workflow can be extended to:
- Additional tissue-specific peaks or enhancer sets
- Cross-species trait correlation analysis
- Integration with epigenomic or transcriptomic datasets

## Example Applications
- Discovery of regulatory regions under human-specific selection
- Exploration of enhancer-trait associations across mammals
- Validation of phylogenetic assumptions via chromatin-based metrics

## License
MIT License
