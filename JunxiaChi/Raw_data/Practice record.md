---
title: Practice record
---

## preparation
Sratoolkit turns SRA file into fastq file
fastq-dump SRR034580£¨.sra£©

## joint£º
Soybean data connector (TGGAATTCTCGGGTGCCAAGGAACTCCAGT)
cutadapt -a Joint sequence input file.fastq > output file.fastq
cutadapt -a TGGAATTCTCGGGTGCCAAGGAACTCCAGT --quality-base 33 -m 10 -q 20 --discard-untrimmed -o c697.fastq SRR1240697.fastq;

## Quality Control
fastq_quality_filter -q 33 -p 80 -Q 33 -i reads/soybean.fastq -o soybean_clean.fastq
-q : Minimum mass value to be left
-p 80: At least 80% of the bases in a read reach - Q
-Q 33: The data of Illumina platform must have this sentence

## Mapping£º
£¨1£©Database building
First, create a new soybean_index folder 
------ bowtie-build ACUP03.fasta /root/ForPaperMapping/soyen/soyen_index
Get index package

£¨2£©Input fastq file, strict match, mismatch 0, output all matches, output sam file (if input FASTA file, replace - q with - f)
 
------ bowtie -q -v 0 -a /root/ForPaperMapping/soyen/soyen_index /root/data/c707_18to25.fastq -S /root/ForPaperMapping/soyen/soyen_mapping.sam 2>/root/ForPaperMapping/soyen/soyen_mapping.info
 
£¨3£©Sam file to bam file
samtools view -bS soyen_mapping.sam > soyen_mapping.bam
£¨4£©rmdup
samtools rmdup soyen_mapping.bam soyen_mapping_rmdup.bam
£¨5£©Keep matching data
samtools view -bF 4 soyen_mapping_rmdup.bam > soyen_mapping_rmdup_.F.bam
£¨6£©bam file to sam file
samtools view -h soyen_mapping_rmdup_.F.bam > soyen_mapping_rmdup_.F.sam
£¨7£©bam file to fastq file
bam2fastq --aligned soyen_mapping_rmdup_.F.bam -o soyen_mapping_rmdup.fq
bam2fastq --aligned c707_rmdup_.F.bam -o c707_rmdup.fq


4¡¢open pycharm
5¡¢For soybeans_ clean.fastq file sequence extraction, output a sequence only txt file soybean_ clean_ seq.txt £¨seq_ extraction.py )
6¡¢For soybeans_ soybean_ perfect_ mapping_ rmdup.fq Extract the sequence and output a txt file with only sequence
	soybean_soybean_perfect_mapping_rmdup_seq.txt£¨seq_extraction.py£©
7¡¢For a sequence only file, soybean_ clean_ seq.txt Perform length control (18 to 25)£¬
	De duplication and type statistics, output as a txt file soybean_ clean_ sort_ len_ count.txt , format: sequence,length and quantity£¨new_Ded_sort_count.py£©
8¡¢Sequence only mapping and de redundant txt file soybean_ soybean_ perfect_ mapping_ rmdup_ seq.txt Length control (18 to 25) and weight removal,
get the mapped and de redundant miRNA sequence type TXT file soybean_soybean_perfect_mapping_rmdup_seq_dup.txt£¨new_Ded_sort.py£©
9¡¢The soybean_ clean_ sort_ len_ count.txt and soybeans_ soybean_ perfect_ mapping_ rmdup_ seq_ dup.txt convert to a csv file
10¡¢Merge the above two CSV files to get soybeanclean_save_soybeansoybeanmap_sort_len_count.csv£¨combine.py£©

11¡¢Standardization and screening
13¡¢Replace all T in miRNA with u
14¡¢Target gene prediction£¨tapir£©
£¨tapir£©tapir_hybrid 5081_150_U.fa ossequence.fa | hybrid_parser > 5081_150_ba2.txt  




