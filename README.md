
# Subtractive Genomics Approach for Drug Target Identification in *Mycobacterium tuberculosis*

A computational pipeline implementing the subtractive genomics methodology to identify potential novel drug targets in *Mycobacterium tuberculosis* (H37Rv strain), the causative agent of tuberculosis (TB).

## Project Road Map

🔗 [Project Roadmap](https://roadmap.sh/r/substractive-genomic-approach)

## Overview

This project systematically screens protein sequences from the UniProt database through a series of biological filters to identify essential, non-homologous bacterial proteins suitable as drug targets. The pipeline reduced an initial pool of **4,000 protein sequences** down to **8 promising drug target candidates**.

## Methodology

The subtractive genomics pipeline consists of four critical filtering steps:

### Step 1: Sequence Length Filter
- **Tool**: BioPython (SeqIO)
- **Criterion**: Excluded sequences shorter than **100 amino acids**
- **Rationale**: Ensures selection of proteins with stable, druggable biological domains

### Step 2: Host Non-Homology Screening
- **Tool**: NCBI BLAST+ (blastp)
- **Criterion**: Removed proteins with homology to human proteome (e-value ≤ 1e-4)
- **Rationale**: Avoids cross-reactivity and minimizes potential side effects

### Step 3: Essentiality Analysis
- **Tool**: NCBI BLAST+ against Database of Essential Genes (DEG)
- **Criterion**: Proteins with ≥30% identity and bitscore ≥100 against DEG entries
- **Rationale**: Selects proteins indispensable for bacterial survival

### Step 4: Subcellular Localization
- **Tool**: PSORTb v3.0
- **Criterion**: Predicted spatial location within the cell
- **Rationale**: Determines therapeutic strategy — membrane proteins for vaccines, cytoplasmic proteins for antibiotics

## Results

| Metric | Count |
|--------|-------|
| Initial sequences | 4,000 |
| Final drug target candidates | **8** |
| Selected for structural modeling | **P9WJD9 (EspB)** |

### Final Candidate Proteins

The 8 candidate proteins represent promising drug targets with confirmed essentiality, no human homology, and defined subcellular localization.

### Structural Analysis: P9WJD9 (EspB)

- **Protein**: ESX-1 secretion-associated protein EspB
- **UniProt ID**: P9WJD9
- **Localization**: Cytoplasmic (Score: 10.00)
- **3D Structure**: [RCSB PDB: 4XWP](https://www.rcsb.org/structure/4XWP)

#### Protein 3D Structure

🔗 [View on RCSB PDB](https://www.rcsb.org/structure/4XWP)

#### PyMOL Visualization

To visualize the druggable active pocket of EspB in PyMOL, use the following commands:

```pymol
hide everything
show cartoon, polymer
color gray80, polymer
show spheres, resn CA
color red, resn CA
select pocket, (byres (polymer within 5.0 of resn CA))
show sticks, pocket
show surface
color gray80, all
color gold, pocket
```

**Analysis Result**: The structural analysis revealed a **druggable active pocket** characterized by a deep, biologically conserved geometric cavity, making it an ideal docking site for protein inhibition to trigger bacterial cell death.

## Tools & Resources

| Tool | Purpose |
|------|---------|
| [BioPython](https://biopython.org/) | FASTA parsing, sequence handling |
| [NCBI BLAST+](https://blast.ncbi.nlm.nih.gov/) | Sequence similarity searches |
| [PSORTb](https://psort.org/psortb/) | Subcellular localization prediction |
| [PyMOL](https://pymol.org/) | 3D protein structure visualization |
| [UniProt](https://www.uniprot.org/) | Protein sequence database |
| [DEG](http://tubic.org/Deg/) | Database of Essential Genes |
| [RCSB PDB](https://www.rcsb.org/) | Protein structure database |

## Subcellular Localization

🔗 [PSORTb Server](https://psort.org/psortb/)

## Data Sources

🔗 [Download Project Data](https://drive.google.com/drive/folders/1zISzni_PJbTk3Yq6z9zl_oHAmSz93iKi?usp=drive_link)

- **Protein Sequences**: UniProt database (*M. tuberculosis* H37Rv, strain ATCC 25618)
- **Human Proteome**: UniProt *Homo sapiens* proteome
- **Essential Genes**: DEG 10.aa (Database of Essential Genes)

## Jupyter Notebooks

| Notebook | Step | Description |
|----------|------|-------------|
| `SeqIO.ipynb` | 1 | Parse FASTA files and filter by sequence length |
| `Blast_linux_Alignment_.ipynb` | 1-2 | BLAST alignment against human proteome |
| `Filter_operation_02.ipynb` | 2 | Remove human homologous proteins |
| `Pandas_operation.ipynb` | 2 | Exploratory analysis of BLAST results |
| `Filter_operation_03.ipynb` | 3 | Essential gene filtering using DEG |
| `Filter_Phase_04(2).ipynb` | 4 | PSORTb parsing and candidate selection |

## How to Run

1. Install dependencies:
   ```bash
   pip install biopython pandas
   sudo apt-get install ncbi-blast+
   ```

2. Follow the notebooks in order (Step 01 → Step 04)

3. For PSORTb analysis, submit sequences to [PSORTb web server](https://psort.org/psortb/)
