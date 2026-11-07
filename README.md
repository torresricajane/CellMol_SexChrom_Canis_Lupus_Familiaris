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

rname,group
NC_006583.4,A
NC_006584.4,A
NC_006585.4,A
NC_006586.4,A
NC_006587.4,A
NC_006588.4,A
NC_006589.4,A
NC_006590.4,A
NC_006591.4,A
NC_006592.4,A
NC_006593.4,X

## Part D: R Analysis 
I ran the provided R analysis script in RStudio (sex_depth_analysis.R) using chromosome_coverage.tsv and chromosome_groups.csv.

**R Code Used:**

# Sex-chromosome dosage from whole-genome DNA read depth
# Input: Samtools coverage TSV + student chromosome labels
cov <- read.delim("chromosome_coverage.tsv", comment.char = "",
check.names = FALSE, stringsAsFactors = FALSE)
names(cov)[1] <- "rname" # Accepts the '#rname' header
if (!"meandepth" %in% names(cov)) stop("Missing meandepth column")
key <- read.csv("chromosome_groups.csv", stringsAsFactors = FALSE)
if (!all(c("rname", "group") %in% names(key))) stop("Bad key columns")
key$rname <- trimws(key$rname)
key$group <- toupper(trimws(key$group))
if (anyDuplicated(key$rname)) stop("Repeated rname in key file")
if (!all(key$group %in% c("A", "X", "Y", "Z", "W")))
stop("Use only A, X, Y, Z or W in the group column")
x <- merge(key, cov[, c("rname", "meandepth")],
by = "rname", all.x = TRUE, sort = FALSE)
x$meandepth <- suppressWarnings(as.numeric(x$meandepth))
if (anyNA(x$meandepth)) stop("Missing depths: check rname matches")
if (any(x$meandepth < 0)) stop("Negative depth is not valid")
if (sum(x$group == "A") < 5) stop("Label at least 5 autosomes")
if ("X" %in% x$group && "Z" %in% x$group)
stop("Choose either an XY or a ZW species, not both")
if (sum(x$group == "X") == 1 && !any(x$group == "Z")) {
target <- "X"
one_copy <- "XY-like"
two_copies <- "XX-like"
} else if (sum(x$group == "Z") == 1 && !any(x$group == "X")) {
target <- "Z"
one_copy <- "ZW-like"
two_copies <- "ZZ-like"
} else stop("Label exactly one X or exactly one Z chromosome")
A <- median(x$meandepth[x$group == "A"])
if (!is.finite(A) || A <= 0) stop("No usable autosomal coverage")
x$relative_depth <- x$meandepth / A
ratio <- x$relative_depth[x$group == target]
call <- if (ratio >= 0.80) two_copies else if (ratio <= 0.65)
one_copy else "Ambiguous"
if (A < 1) call <- "Inconclusive: very low autosomal depth"
# Additional Y or W evidence can support, but not prove, a call
partner <- if (target == "X") "Y" else "W"
partner_ratio <- if (partner %in% x$group)
x$relative_depth[x$group == partner][1] else NA_real_
# Export results and a simple, reproducible figure
dir.create("results", showWarnings = FALSE)
write.csv(x, "results/chromosome_relative_depth.csv", row.names = FALSE)
png("results/chromosome_depth.png", width = 1000, height = 580)
par(mar = c(8, 4, 3, 1))
barplot(x$relative_depth, names.arg = x$rname, las = 2,
ylab = "Depth relative to median autosome",
main = "Autosomal and sex-chromosome depth", cex.names = 0.75)
abline(h = c(0.5, 1.0), lty = 2)
dev.off()
summary <- c(paste("Median autosome depth:", round(A, 3)),
paste(target, "/ A ratio:", round(ratio, 3)),
paste(partner, "/ A ratio:", round(partner_ratio, 3)),
paste("Dosage interpretation:", call),
"Compare with BioSample sex and discuss limitations.")
writeLines(summary, "results/sex_inference.txt")
cat(paste(summary, collapse = "\n"), "\n")

