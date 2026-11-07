# CellMol_SexChrom_*Canis lupus familiaris*

Torres, Rica Jane M.
Cell and Molecular Biology (section B)

## Part A: Organism & Assembly Metadata
* **Species:** *Canis lupus familiaris* (Domestic Dog)
* **Assembly Name:** Dog10K_Boxer_Tasha (canFam6)
* **RefSeq Assembly Accession:** GCF_000002285.5  https://www.ncbi.nlm.nih.gov/datasets/genome/GCA_000002285.4/
* **GenBank Assembly Accession:** GCA_000002285.4
* **Assembly Level:** Chromosome
* **Assembly Donor BioSample:** SAMN02953603 (Tasha, Female Boxer) https://www.ncbi.nlm.nih.gov/biosample/SAMN02953603/
* **Ploidy & Sex System:** Diploid ($2n = 78$), XX/XY sex-determination system. The X chromosome is explicitly annotated as a distinct chromosome (NC_006621.4).
* **WGS Read Run Accession:** SRR13131602 (Illumina HiSeq X Ten, Paired-end)
* **WGS BioSample Accession:** SAMN02953603 (Same individual/donor as reference genome)
* **Galaxy Workflow / History Link:** https://usegalaxy.org/u/ricajanetorres/h/sex-dosage-canis-lupus-familiaris

## Part B: Data Retrieval, Read Mapping, and Coverage Analysis
* **Galaxy History Name:** Sex_Dosage_Canis lupus familiaris
* **Galaxy Workflow Steps & Tools Used:**
  1. **Upload:** I imported the reference genome FASTA (`.fna.gz`) and assembly report for *Canis lupus familiaris* (canFam6) from NCBI into my Galaxy history.
  2. **Faster Download:** I used the **fasterq-dump** tool to download the WGS read dataset (`SRR13131602`), obtaining paired-end read collections.
  3. **Unzip Collection:** I used **unzip collection** to unpack and organize my paired-end sequence files into separate forward and reverse read datasets (`collection 9` and `collection 10`)
  4. **FastQC:** I ran **FastQC** on my read collections to evaluate base quality scores and adapter content prior to alignment.
  5. **BWA-MEM2:** I mapped the paired-end reads to the reference genome using **BWA-MEM2**, generating a coordinate-sorted and indexed BAM alignment file (`dataset 19`).
  6. **Samtools Coverage:** I ran **Samtools coverage** on the sorted BAM file (specifying tabular output, minimum mapping quality = 20, and minimum base quality = 20) to generate my per-chromosome coverage statistics (`chromosome_coverage.tsv`).
 
<img width="1349" height="611" alt="uploading the file" src="https://github.com/user-attachments/assets/0f629056-969c-4d9e-b192-822e3ff369fc" />

*Figure 1:* Uploading reference genome FASTA and assembly report files into the Galaxy history

<img width="1344" height="608" alt="uploaded file" src="https://github.com/user-attachments/assets/2c8365d2-634f-4f1e-8c94-9c31662c9183" />

*Figure 2:* Successful import of the reference genome FASTA and assembly report into the Galaxy history

<img width="1365" height="604" alt="done running faster download 1" src="https://github.com/user-attachments/assets/65c1dad8-c3e9-432e-a3c2-8650c861c6e7" />

*Figure 3:* Successful execution of fasterq-dump showing downloaded paired-end WGS reads (SRR13131602) in the Galaxy history panel.

<img width="1362" height="606" alt="unzip collection" src="https://github.com/user-attachments/assets/6ac3b6cc-d054-4ea1-aa42-e7519af9b4b3" />

*Figure 4:* Using the Unzip collection tool in Galaxy to separate the paired-end read collection into distinct forward and reverse datasets (SRR13131602).

<img width="1362" height="607" alt="done running fastqc 1" src="https://github.com/user-attachments/assets/1ec58383-039f-44b3-b7a1-8a32b95637b4" />

*Figure 5:* Running FastQC quality control analysis on the paired-end read collection (SRR13131602) within Galaxy.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/bf043541-af03-4200-89b8-833c68bea612" />

*Figure 6:* FastQC quality control report showing adapter content and per-base sequence metrics for the forward read dataset (SRR13131602).

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/7226f4db-e763-48c7-8d77-61175b3354f9" />

*Figure 7:* FastQC quality control report displaying adapter content and per-base metrics for the reverse read dataset (SRR13131602).

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/7c82d82c-819e-4c4c-aca0-9f06d0a2ceab" />

*Figure 8:* FastQC Basic Statistics table and per-base sequence quality plot for the forward read dataset (forward.gz), showing read count, total bases, and quality score distribution.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/da1eb45a-6b69-4172-b833-e12a698baf9e" />

*Figure 9:* FastQC Basic Statistics table and per-base sequence quality plot for the reverse read dataset (reverse.gz), showing total sequence count, read length, and GC content.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/2654cb27-8fe6-4576-afed-659e04edce6b" />

*Figure 10:* Aligning paired-end WGS reads (SRR13131602) to the reference genome using BWA-MEM2 in Galaxy to generate coordinate-sorted BAM alignments.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/e622d61a-7fdc-4c70-aab2-a4e562021d28" />

Figure: Samtools coverage tabular output showing per-chromosome alignment statistics (meandepth, coverage, and numreads) generated from the sorted BAM file.

## Part C: Chromosome Grouping (`chromosome_groups.csv`)
To prepare for the R analysis, I created a plain-text CSV file named `chromosome_groups.csv` mapping the RefSeq accessions to their respective chromosome groups (`A` for autosomes and `X` for the sex chromosome).

| Reference Name (`rname`) | Group (`group`) | Description / Assignment |
| :--- | :---: | :--- |
| `NC_006583.4` | A | Autosome |
| `NC_006584.4` | A | Autosome |
| `NC_006585.4` | A | Autosome |
| `NC_006586.4` | A | Autosome |
| `NC_006587.4` | A | Autosome |
| `NC_006588.4` | A | Autosome |
| `NC_006589.4` | A | Autosome |
| `NC_006590.4` | A | Autosome |
| `NC_006591.4` | A | Autosome |
| `NC_006592.4` | A | Autosome |
| `NC_006593.4` | X | Sex Chromosome (X) |

## Part D: R Analysis 
I ran the provided R analysis script in RStudio (sex_depth_analysis.R) using chromosome_coverage.tsv and chromosome_groups.csv.

**R Code Used:**

<img width="648" height="477" alt="image" src="https://github.com/user-attachments/assets/7ecad28b-e9bc-4a5b-9e74-02deff7c22fe" />

<img width="648" height="445" alt="image" src="https://github.com/user-attachments/assets/3fee63a1-b186-43b2-8c1a-705ca315e8bb" />

## Part E: Results Interpretation & Report Questions

### Q1: What species did you choose, and what evidence supports a diploid XX/XY or ZZ/ZW system?
* **Answer:** I chose *Canis lupus familiaris* (domestic dog). It possesses a diploid karyotype ($2n = 78$) characterized by a well-established XX/XY chromosomal sex-determination system, where females possess two X chromosomes and males possess one X and one Y chromosome.

### Q2: What are your assembly accession, WGS run, and both BioSample accessions? Are the donors the same?
* **Answer:** 
  * **RefSeq Assembly Accession:** `GCF_000002285.5`
  * **WGS Run Accession:** `SRR13131602`
  * **Assembly Donor BioSample:** `SAMN02953603`
  * **WGS BioSample Accession:** `SAMN02953603`
  * **Are donors the same?** Yes, both the reference genome assembly and the whole-genome sequencing reads originate from the exact same individual donor (Tasha, a female Boxer).

### Q3: Which sequences were used as autosomes and as X or Z? How did you verify their identities?
* **Answer:** I used ten autosomal RefSeq accessions (`NC_006583.4` through `NC_006592.4`) and the canonical X chromosome accession (`NC_006593.4`). I verified their identities by cross-referencing the NCBI assembly report and checking chromosome coordinate lengths and identifiers in my `chromosome_coverage.tsv` output.

### Q4: What are the median autosomal depth, X:A or Z:A ratio, and inferred sex-chromosome complement?
* **Answer:** 
  * **Median Autosomal Depth ($A$):** 3.935×
  * **X:A Ratio:** 1.018
  * **Inferred Sex-Chromosome Complement:** XX-like

### Q5: Does your result agree with the recorded sex of the WGS donor, if reported? Explain any discrepancy or uncertainty.
* **Answer:** Yes, my result completely agrees with the recorded metadata. The WGS donor BioSample (`SAMN02953603`) corresponds to a female dog (Tasha), and my calculated X:A ratio of 1.018 falls right around the expected 1.0 threshold for an XX individual, confirming strong concordance between sequence coverage data and donor metadata.

### Q6: Why is a chromosome-level assembly alone insufficient for a reliable read-depth sex inference?
* **Answer:** A reference assembly only provides the structural framework of the genome and does not contain empirical sequencing data for the specific individual being tested. Without aligning individual WGS reads to compute relative read depth coverage across chromosomes, it is impossible to determine chromosomal copy number or dosage variation.
"Compare with BioSample sex and discuss limitations.")
writeLines(summary, "results/sex_inference.txt")
cat(paste(summary, collapse = "\n"), "\n")

