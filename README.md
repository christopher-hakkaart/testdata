# Creating test data for nanoseq variant calling 

## Random gene of interest with known SV

```bash
EDIL3
chr5:83940554-84384880 (-)
id = NM_005711.5
```

## Make bed file

``` bash
touch GRCh38_EDIL3.bed
echo -e "chr5\t83940554\t84384880\tEDIL3\t0\t-\n" >> GRCh38_EDIL3.bed
```

## Find reads mapped to EDIl3 convert to fastq, and gzip

```bash
samtools view -b A04.bam "chr5:83940554-84384880" > EDIL3.bam```
samtools index EDIL3.bam 
samtools fastq EDIL3.bam > NA12878_DNA.fastq
gzip NA12878_DNA.fastq
```

## Make new reference genome

``` bash
bedtools getfasta -name -fi Homo_sapiens_assembly38.fasta -bed GRCh38_EDIL3.bed > GRCh38_EDIL3.fa
samtools faidx GRCh38_EDIL3.fa
```

## Notes for future development
TODO Add second chromosome and reads to use as base for development of variant calling for each chromosome separately.

TODO Fix error that occurs with default chromosome naming from bedtools – temporary solution is to arbitrarily name chromosome removing characters that were causing the problem.
