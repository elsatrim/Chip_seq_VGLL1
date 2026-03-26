# 🧬 ChIP-seq Analysis of VGLL1 in Placental Cells

![Pipeline](https://img.shields.io/badge/Pipeline-ChIP--seq-blue)
![Language](https://img.shields.io/badge/Language-Bash%20%7C%20Python-green)
![Tools](https://img.shields.io/badge/Tools-Bioinformatics-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📌 Overview

This project implements a **complete ChIP-seq analysis pipeline** to identify genomic binding sites of **VGLL1**, a transcriptional co-activator involved in placental development and cancer.

The workflow covers the entire process from **raw sequencing data → biological interpretation**, including:

* Quality control
* Alignment
* Peak calling
* Motif discovery
* Functional enrichment

---

## 🧠 Biological Context

VGLL1 interacts with TEAD transcription factors in the **Hippo signaling pathway**, regulating:

* Cell proliferation
* Cell survival
* Tissue development

Its dysregulation is linked to:

* Tumorigenesis
* Placental disorders

---

## 📂 Dataset

| Type                         | ID          |
| ---------------------------- | ----------- |
| ChIP sample (VGLL1 antibody) | SRR29077837 |
| Control sample (input DNA)   | SRR29077838 |

* Platform: Illumina NovaSeq 6000
* Read type: Single-end (75 bp)

---

## ⚙️ Pipeline Workflow

```
SRA → FASTQ → QC → Trimming → Alignment → BAM processing
→ Peak Calling → Differential Analysis → Motif Discovery
→ Gene Annotation → Functional Enrichment
```

---

## 🛠️ Tools & Technologies

| Category            | Tools       |
| ------------------- | ----------- |
| Data download       | SRA Toolkit |
| QC                  | FastQC      |
| Trimming            | fastp       |
| Alignment           | Bowtie2     |
| Processing          | SAMtools    |
| Visualization       | IGV         |
| Coverage            | deepTools   |
| Peak calling        | MACS2       |
| Motif analysis      | RSAT        |
| Annotation          | GREAT       |
| Sequence extraction | BEDTools    |
| Enrichment          | g:Profiler  |

---

## 🚀 Step-by-Step Pipeline

### 1. 📥 Download Data

```bash
fastq-dump SRR29077837
fastq-dump SRR29077838
```

---

### 2. 🔍 Quality Control

```bash
fastqc *.fastq
```

✔️ Detects:

* Adapter contamination
* GC bias
* Overrepresented sequences

---

### 3. ✂️ Read Trimming

```bash
fastp -i input.fastq -o cleaned.fastq --adapter_sequence <adapter>
```

✔️ Removes:

* Adapters
* Low-quality bases

---

### 4. 🧬 Alignment

```bash
bowtie2 -x hg19 -U cleaned.fastq -S output.sam
```

---

### 5. 📦 BAM Processing

```bash
samtools view -b file.sam > file.bam
samtools sort file.bam -o sorted.bam
samtools index sorted.bam
```

---

### 6. 📊 Visualization (IGV)

* Compare ChIP vs control
* Inspect enrichment at genomic loci

---

### 7. 📈 Coverage Tracks

```bash
bamCoverage -b sorted.bam -o output.bw --binSize 5
```

---

### 8. ⛰️ Peak Calling

```bash
macs2 callpeak -t chip.bam -c control.bam -g 2.86e9 -q 0.05
```

Outputs:

* `.narrowPeak`
* `.summits.bed`
* `.xls`

---

### 9. 🔬 Differential Analysis

```bash
macs2 bdgdiff ...
```

✔️ Identifies condition-specific peaks

---

### 10. 🔥 Heatmap Visualization

```bash
computeMatrix
plotHeatmap
```

✔️ Shows enrichment around peak centers

---

### 11. 🧩 Motif Discovery

```bash
bedtools getfasta ...
```

* Performed using RSAT
* Identifies enriched DNA motifs

---

### 12. 🧬 Gene Association

* Tool: GREAT
* Links peaks → nearby genes

---

### 13. 📊 Functional Enrichment

* g:Profiler
* Gene Ontology (GO)

✔️ Reveals:

* Developmental pathways
* Cell signaling
* Cytoskeleton organization

---

## 📊 Key Results

✔️ Strong VGLL1 binding enrichment in ChIP sample
✔️ Clear peak signals vs control
✔️ Motifs linked to transcription factors (e.g., RUNX2, GRHL2)
✔️ Genes involved in:

* Placental development
* Cell proliferation
* Cancer pathways

---

## 📁 Project Structure

```
├── data/
│   ├── raw_fastq/
│   ├── cleaned_fastq/
│
├── alignment/
│   ├── bam/
│   ├── sorted_bam/
│
├── peaks/
│   ├── narrowPeak/
│   ├── bed/
│
├── motifs/
│   ├── fasta/
│   ├── rsat_results/
│
├── analysis/
│   ├── heatmaps/
│   ├── figures/
│
├── scripts/
│   ├── pipeline.sh
│
└── README.md
```

---

## 📌 Outputs

| File Type     | Description     |
| ------------- | --------------- |
| `.fastq`      | Raw reads       |
| `.bam`        | Aligned reads   |
| `.bw`         | Coverage tracks |
| `.bed`        | Genomic regions |
| `.narrowPeak` | Peaks           |
| `.fasta`      | Sequences       |
| `.png`        | Plots           |

---

## ⚠️ Limitations

* No biological replicates
* Initial adapter contamination
* Limited validation of motifs

---

## 🔮 Future Work

* Add replicates
* Integrate RNA-seq
* Cross-tissue comparison
* Experimental validation

---

## 📚 References

* Frontiers in Oncology (2024)
* NCBI SRA Database
* Tool documentation (FastQC, Bowtie2, MACS2, etc.)

---

## 👨‍💻 Author

Elsa Sánchez Fernández 

---


## 💡 Takeaway

This project demonstrates how **computational genomics can uncover regulatory mechanisms**, showing that VGLL1 plays a key role in **placental biology and cancer-related gene regulation**.

---
