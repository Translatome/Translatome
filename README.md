# Translatome
Workflows for polysome and ribosome profiling analyses

----------------------------------------------------
## Context:
Translation is the second phase of protein synthesis that involves converting the information on the mRNA sequence to an amino acid sequence. 
This process requires mRNA, ribosomes, amino acids, tRNA, and other factors.

Translatomics is the study of all open reading frames (ORFs) that are being actively translated in a cell or organism. 
This collection of ORFs is referred to as the translatome. 
Characterizing a cell's translatome can give insight into the array of biological pathways that are active in the cell.

Polysome and ribosome profiling are two molecular techniques that require specific bioinformatic analysis due to their technical differences and limitations.

Polysome profiling is a technique that infer the translation status of a specific mRNA by analyzing the behavior of polysomes, i.e. to the group of ribosomes bound to an mRNA, that is present during the elongation phase of translation.
Polysome profiling consists in the quantification of mRNA abundance in polysome fractionation by sucrose density gradient centrifugation. 
Based on the assumption that ribosome density is highly correlated with protein production, the translational efficiency of individual genes can be calculated.
Translational efficiency is calculated by comparing two RNA-seq profiles, one for transcription (all mRNA) and one for translation (mRNA with ribosomes bound). 

Ribosome profiling differs in the sense that the ribosome behavior is analyzed using only the mRNA sequence during translation.
Ribosomes leave ~30 nt footprints (ribosome-protected RNA fragments, RPF) when they are bound to mRNAs.
Ribosome profiling captures positional information of ribosome footprints at the subcodon level.
Deep sequencing of RPFs would globally quantify the abundance of ribosome footprints on individual genes and pinpoint the position of ribosomes on mRNAs.

We provide here two Snakemake workflows to analyze these different visions of the translatome:

1/ Polysome profiling (POL-SEQ)
- Quality checking
- Filtering of RNA-seq data
- Alignment on reference genome
- Read counts
- Statistics
- GSEA enrichment analysis
(with some variation according to kinetic studies or not)

2/ Ribosome profiling (RIBO-SEQ)
- Quality checking
- Filtering of RIBO-seq data
- Alignments on reference genome and transcriptome
- Read counts
- Codon usage
- Codon coverage
- Statistics

These workflows are provided as is, without garanty if any modification is made.

Several packages and softwares are used here, please cite them or cite this Github Project.

[<small>[top↑]</small>](#)

------------------------------------------------------
## LICENSE

[LICENSE]() terms are in agreement with CeCILL License.

See : http://www.cecill.info/licences.fr.html

## Contributions

See the [contributing]() file and please follows the recommandation in the [code of conduct]()

[<small>[top↑]</small>](#)

-------------------------------------------------------
## Requirements

These workflows require:
- Python3
- Snakemake v.7 or <
- Conda and/or Mamba
- Internet connection for steps 00, 05 and 06

Most of the programs are installed using conda environments.
Other programs are provided as Java archives (jar) and do not require installation.
Please, do not decompress JAR archives.

## Installation

### Clone workflows into desired working directory
```shell
git clone https://github.com/Translatome/Translatome.git path/to/workdir
cd path/to/workdir
```

### Install Snakemake through MiniConda

1. Download the installer miniconda: [https://conda.io/miniconda.html](https://conda.io/miniconda.html)

2. In your Terminal window, run:
```shell
bash Miniconda3-latest-Linux-x86_64.sh
```
3. Follow the prompts on the installer screens.

4. Install Snakemake in a dedicated environment
```shell
conda install -c bioconda -c conda-forge -n snakemake snakemake
conda activate snakemake
```

### Install wrapper system package
```shell
pip install .
```

## Execution

### Edit config and complete with your project information
We provide differents examples of configuration file in configs.
```shell
vim configs/config_ribosome.yml
```

### Run Snakemake
Here, this run shows the documentation associated to the rules:
```shell
snakemake -s translatome/workflows/raw_quality/00_download_references.smk --use-conda --conda-frontend mamba --configfile configs/config_ribosome.yml -l
```

Here, this run tests the execution in dry mode:
```shell
snakemake -s translatome/workflows/raw_quality/00_download_references.smk --use-conda --conda-frontend mamba --configfile configs/config_ribosome.yml -j 1 -p -r -n
```

[<small>[top↑]</small>](#)
