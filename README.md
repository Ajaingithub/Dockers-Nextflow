# Developing Docker for

## 1. Whole Genome Sequencing

1. FASTQC
2. GATK
3. PICARD
4. BWA
5. ANNOVAR
6. SAMTOOLS

## 2. Gene Regulatory Network (SCIENICPlus):

it is install in the Conda environment
scenicplus:amd64 is being designed for the linux environment

### Docker on x86_64

docker pull abhinavjain1993/wgs:amd64
docker pull abhinavjain1993/scenicplus:amd64

#### For running docker in the arm64

docker pull abhinavjain1993/scenicplus_docker:latest

#### Running the scenicplus, activate conda using

source activate scenicplus

#### Singularity

singularity pull docker://abhinavjain1993/scenicplus_docker:amd64
singularity exec –bind <Mounted_directory>:/data --contain-all scenicplus_docker_latest.sif /bin/bash

##### Running a WGS files on the server

singularity pull docker://abhinavjain1993/wgs:amd64
fasterq-dump --split-3 DRR001913 -O ./ -t ./tmp/
head -10000 DRR001913_2.fastq > DRR001913_2_10000.fastq
head -10000 DRR001913_1.fastq > DRR001913_1_10000.fastq
java -jar /usr/local/bin/trimmomatic-0.39.jar PE -threads 4 DRR001913_1_10000.fastq DRR001913_2_10000.fastq trim_DRR001913_1_10000.fastq unpaired_DRR001913_1_10000.fastq trim_DRR001913_2_10000.fastq unpaired_DRR001913_2_10000.fastq AVGQUAL:20 SLIDINGWINDOW:5:20 MINLEN:50

###### Download the reference genome

wget https://ftp.ensembl.org/pub/release-107/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
