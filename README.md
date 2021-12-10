# Creating test data for nanoseq variant calling 

## Gene of interest with SV
EDIL3

chr5:83940554-84384880 (-)

id = NM_005711.5

## Make bed file
touch GRCh38_EDIL3.slop_10kb.bed

echo -e "chr5\t83940554\t84384880\tEDIL3\t0\t-\n" >> GRCh38_EDIL3.slop_10kb.bed


## Find reads mapped to EDIl3 + 10kb, convert to fastq, and gzip
samtools view -b 34x.bam "chr5:83940554-84384880" > EDIL3.bam

samtools index EDIL3.bam 

samtools fastq EDIL3.bam > A04.fq

gzip A04.fq

## Make new reference genome
bedtools getfasta -name -fi /mnt/share/data/igenomes/Homo_sapiens/GATK/GRCh38/Sequence/WholeGenomeFasta/Homo_sapiens_assembly38.fasta -bed GRCh38_EDIL3.slop_10kb.bed > GRCh38_EDIL3.fa

Problem with format of reference name, manually changed chromosome name to chr0.

samtools faidx GRCh38_EDIL3.fa
