# ResistPipe
**Overview**

  

This project is a Java-based bioinformatics tool designed to detect known antibiotic resistance genes within an unknown DNA sequence using reference-based sequence comparison. The program compares an unknown nucleotide sequence against a curated set of resistance gene sequences obtained from public databases and reports potential matches.

  

In addition to generating a detailed text report, the program produces a visual ASCII-based summary to help users quickly interpret results.

  

This project was developed as a comprehensive programming assignment demonstrating Java design, file handling, algorithmic thinking, and biological data analysis.

  

**Biological Problem**

  

Antibiotic resistance genes allow bacteria to survive exposure to antimicrobial compounds. Identifying these genes in genomic or environmental samples is an important first step in resistance surveillance and research.

  

This program addresses the question:

  

Does an unknown DNA sequence contain known antibiotic resistance genes?

  

The tool is intended for educational and preliminary screening purposes only.

  

**Features**

  

The program includes the following features:

  

• Parses FASTA-formatted DNA sequences• Screens unknown sequences against known resistance genes• Uses a k-mer–based matching strategy• Reports the number of matches per gene• Reports the longest contiguous match length• Generates a text-based summary report• Generates an ASCII bar chart visualization• Modular, well-documented Java code• GitHub-ready project structure

  

**Input Files**

  

1.  Reference Resistance Genes (FASTA)

  

A FASTA file containing one or more known antibiotic resistance genes.

  

Example:

  

\> esterase\\\_AATGACCGTTGAC...

  

1.  Unknown DNA Sequence (FASTA)

  

A FASTA file containing the unknown sequence to be analyzed.

  

Example:

  

\> unknown\\\_sampleATGCGATCGATCG...

  

**Output Files**

  

Text Summary Output

  

The program generates a results\\\_summary.txt file containing:

  

Resistance Gene Detection Report

\--------------------------------

  

Total reference genes: 10Detected genes: 3

  

Gene: esterase\\\_AMatches found: 5Longest match: 87 bp

  

**Visual Output (Terminal)**

  

The program generates an ASCII bar chart representing the longest match length per gene:

  

Resistance Gene Match Strength

\------------------------------

  

esterase\\\_A | ████████████████ (87 bp)kdr\\\_mutation\\\_1 | ████████ (45 bp)ace\\\_gene | ██████████ (62 bp)

  

**Program Workflow**

  

The program follows the pipeline below:

  

Load reference FASTA fileLoad unknown FASTA fileParse sequencesGenerate k-mersSearch for matchesScore matchesGenerate text reportGenerate ASCII visualization

  

**Project Structure**

  

The project is organized into the following directory structure:

  

src/io/FastaReader.javaFileWriterUtil.java

  

model/GeneMatchResult.java

  

analysis/KmerGenerator.javaSequenceMatcher.javaMatchScorer.java

  

visualization/AsciiBarChart.java

  

Main.java

  

sample\\\_data/resistance\\\_genes.fastaunknown\\\_sequence.fasta

  

output/results\\\_summary.txtgene\\\_match\\\_counts.csv

  

**How to Run**

  

1.  Compile the program using the Java compiler.

2.  Run the program by providing the reference FASTA file and unknown FASTA file as input arguments.

3.  View results in the terminal and in the output directory.

  

**Data Sources**

  

Reference resistance gene sequences were obtained from publicly available biological databases for educational use.

  

**Acknowledgments**

  

Reference sequences were sourced from publicly available biological databases.This project was developed independently for educational purposes.External resources used are acknowledged in code comments where applicable.

  

**Disclaimer**

  

This software is intended for educational and research use only. It is not designed for clinical or diagnostic applications.
