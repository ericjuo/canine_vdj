==================  
This project is to extract VDJ immunoglobulin gene segment from canine genome.  

Written by: Eric Juo  

First created: 2022/10/29  

Lastest modified: 2022/10/29  

===================

## Download canis lupus familiaris genome
- Date of download: 2022/10/29  
- Genome: https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/014/441/545/GCF_014441545.1_ROS_Cfam_1.0/GCF_014441545.1_ROS_Cfam_1.0_genomic.fna.gz  
- Annotation file(gff): https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/014/441/545/GCF_014441545.1_ROS_Cfam_1.0/GCF_014441545.1_ROS_Cfam_1.0_genomic.gff.gz  

## List features in gff file:
```
bioawk -c gff '{print $feature}' GCF_014441545.1_ROS_Cfam_1.0_genomic.gff | sort | uniq
```

## Count C_gene_segment
```
bioawk -c gff 'BEGIN {counter = 0} {if ($feature ~ /C_gene_segment/) counter += 1} END {print counter}' GCF_014441545.1_ROS_Cfam_1.0_genomic.gff
```
There are 25 C_gene_segment in the annotation file.

## Count V_gene_segment
```
bioawk -c gff 'BEGIN {counter = 0} {if ($feature ~ /V_gene_segment/) counter += 1} END {print counter}' GCF_014441545.1_ROS_Cfam_1.0_genomic.gff
```
There are 201 V_gene_segment in the annotation file.

## Install AGAT (In order to extract sequence of features in the gff file)
```
conda install -c bioconda agat
```

## Extract c_gene_segment sequence from genome
```
agat_sp_extract_sequences.pl -g GCF_014441545.1_ROS_Cfam_1.0_genomic.gff -f GCF_014441545.1_ROS_Cfam_1.0_genomic.fna -t C_gene_segment -o ../data/03_processed/c_gene_segment.fasta
```

## Extract v_gene_segment sequence from genome
```
agat_sp_extract_sequences.pl -g GCF_014441545.1_ROS_Cfam_1.0_genomic.gff -f GCF_014441545.1_ROS_Cfam_1.0_genomic.fna -t V_gene_segment -o ../data/03_processed/v_gene_segment.fasta
```
