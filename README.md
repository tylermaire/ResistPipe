# ResistPipe

A simple Java-based bioinformatics tool for detecting known antibiotic resistance genes in unknown DNA sequences using reference-based, k-mer matching. ResistPipe is intended for educational and exploratory analyses (not clinical diagnostics).

---

## Table of contents

- [Overview](#overview)
- [Biological problem](#biological-problem)
- [Key features](#key-features)
- [Project structure](#project-structure)
- [Requirements](#requirements)
- [Build and run](#build-and-run)
- [Command line examples](#command-line-examples)
- [Input formats](#input-formats)
- [Output files and visualization](#output-files-and-visualization)
- [How it works (brief)](#how-it-works-brief)
- [Configuration & tuning](#configuration--tuning)
- [Limitations & disclaimer](#limitations--disclaimer)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements & data sources](#acknowledgements--data-sources)
- [Contact](#contact)

---

## Overview

ResistPipe scans an unknown DNA sequence for sequence similarity to a set of known antibiotic resistance genes. It reports per-gene match counts, longest-match lengths, and produces a compact ASCII bar-chart to summarize match strengths in the terminal. The tool is intended as a teaching example demonstrating file parsing, k-mer analysis, and simple visualization in Java.

---

## Biological problem

Antibiotic resistance genes enable bacteria to survive antibiotic exposure. Detecting these genes in genomes or metagenomic samples helps researchers screen for resistance determinants. ResistPipe performs a quick reference-based screen to detect the presence and approximate strength of matches to known resistance gene sequences.

---

## Key features

- FASTA parser for reference and query sequences
- K-mer–based sequence matching (fast, simple)
- Per-gene match counts and longest-match length reporting
- Text summary report (`results_summary.txt`)
- ASCII bar-chart visualization printed to the terminal
- Designed for educational use and small datasets

---

## Project structure

- `src/`  
  - `io/FastaReader.java`  
  - `FileWriterUtil.java`  
  - `model/GeneMatchResult.java`  
  - `analysis/KmerGenerator.java`  
  - `analysis/SequenceMatcher.java`  
  - `analysis/MatchScorer.java`  
  - `visualization/AsciiBarChart.java`  
  - `Main.java`  
- `sample_data/`  
  - `resistance_genes.fasta`  
  - `unknown_sequence.fasta`  
- `output/`  
  - `results_summary.txt`  
  - `gene_match_counts.csv`

---

## Requirements

- Java 8+ (JDK)
- Command-line shell (Linux/macOS/Windows)
- Small datasets — memory and performance depend on input sizes and k-mer configuration

---

## Build and run

1. Compile the project:
   - If the code files are in the default (no package) layout:
     - javac -d out src/**/*.java
   - If files use packages, ensure you compile with the correct source path or use an IDE/build tool (Maven/Gradle).

2. Run:
   - java -cp out Main <reference_fasta> <unknown_fasta>
   - Example:
     - java -cp out Main sample_data/resistance_genes.fasta sample_data/unknown_sequence.fasta

Notes:
- Replace `out` and `Main` with your actual compiled output directory and fully qualified main class name if packaged.
- If you use an IDE (IntelliJ/Eclipse) you can import as a Java project and run the `Main` class.

---

## Command line examples

Example run using the included sample data:

- Compile:
  - javac -d out src/io/*.java src/model/*.java src/analysis/*.java src/visualization/*.java src/Main.java
- Run:
  - java -cp out Main sample_data/resistance_genes.fasta sample_data/unknown_sequence.fasta

Expected console output (example):

Resistance Gene Match Strength
------------------------------
esterase_A         | ████████████████ (87 bp)
kdr_mutation_1     | ████████ (45 bp)
ace_gene           | ██████████ (62 bp)

A `results_summary.txt` file will be written to the `output/` directory summarizing matches and statistics.

---

## Input formats

Both inputs must be in FASTA format.

Reference FASTA (one or more genes):
> \>gene_name  
> ATGCGT...  

Unknown sequence FASTA (single or multiple sequences supported based on implementation):
> \>unknown_sample  
> ATGCGATCGATC...

---

## Output files and visualization

- `output/results_summary.txt` — human-readable text summary with:
  - Total reference genes
  - Number of detected genes
  - Per-gene: matches found, longest match length

- `output/gene_match_counts.csv` — optional CSV with per-gene counts (if implemented)

- Terminal ASCII visualization — horizontal bars showing longest match length per gene

Example excerpt from `results_summary.txt`:

Resistance Gene Detection Report
-------------------------------
Total reference genes: 10
Detected genes: 3

Gene: esterase_A
  Matches found: 5
  Longest match: 87 bp

---

## How it works (brief)

1. Parse the reference FASTA file and create k-mer sets for each reference gene.
2. Parse the unknown FASTA sequence(s) and generate k-mers from the query.
3. Compare query k-mers to reference gene k-mers to detect matches.
4. Score and summarize matches per gene (match counts, longest contiguous match).
5. Write a textual report and render an ASCII bar chart for quick interpretation.

K-mer matching is fast and memory-efficient but is a heuristic — it approximates similarity and can miss more complex variants or structural differences.

---

## Configuration & tuning

- K-mer size (k) affects sensitivity and specificity:
  - Smaller k → more sensitive, more false positives
  - Larger k → more specific, may miss shorter matches
- If the code exposes parameters (constants or CLI flags), adjust k and thresholds to suit your data size and expected similarity.
- For large datasets, consider streaming, indexing, or using a more optimized tool/library for scalability.

---

## Limitations & disclaimer

- Educational tool: not validated for clinical/diagnostic decisions.
- Results are approximate; use specialized tools (e.g., BLAST, DIAMOND, AMRFinder) for rigorous analyses.
- Short k-mers can produce false positives; long indels or rearrangements won't be detected reliably.

---

## Contributing

Contributions, bug reports, and feature requests are welcome.

- Fork the repo
- Create a branch: feature/my-change
- Make changes, add tests if applicable
- Open a pull request with a clear description

Please follow standard Java style and include comments where appropriate.

---

## License

This project is provided for educational purposes.

---

## Acknowledgements & data sources

- Reference sequences used in sample data were obtained from publicly available biological databases for educational use. Please cite original sources when using real datasets.

---

## Contact

Maintainer: @tylermaire  
Repository: https://github.com/tylermaire/ResistPipe

---

If you'd like, I can:
- Commit this README to a new branch and open a PR, or
- Update the README directly in the repo (tell me which you prefer).
