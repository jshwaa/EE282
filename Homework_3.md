_Summarize a genome assembly
We will be working with the Drosophila melanogaster genome. You can start at flybase.org. Go to the most current download genomes section and download the gzipped fasta file for all chromosomes._

## File integrity
__Verify the file integrity of the gzipped fasta file using a checksum__

First, download the most recent (last modified 10-4-18) gzipped fasta file for all chromosomes, and checksum against reposity md5sum.txt:
   
    mkdir ~/homework3
    cd ~/homework 3
    wget ftp://ftp.flybase.net/genomes/Drosophila_melanogaster/current/fasta/dmel-all-chromosome-r6.24.fasta.gz
    wget ftp://ftp.flybase.net/genomes/Drosophila_melanogaster/current/fasta/md5sum.txt
    md5sum -c md5sum.txt
    dmel-all-chromosome-r6.24.fasta.gz: OK
  
__Calculate the following for the whole genome:__
1. Total number of nucleotides:
`grep` out any sequence headers, then subtract total newlines from total characters (which includes newline count):
```
 zgrep -v "^>" dmel-all-chromosome-r6.24.fasta.gz | wc -lm | awk '{print $2-$1}'
 143726002
```    
2. Total number of Ns
`grep` out sequence headers, delete anything that is the complement of N nucleotides, then count characters:
```
 zgrep -v "^>" dmel-all-chromosome-r6.24.fasta.gz | tr -cd '[N]' | wc -m
 1152978
```      
3. Total number of sequences
Each sequence begins with a ">", so just count lines beginning with this with `grep`:
```
zgrep -c "^>" dmel-all-chromosome-r6.24.fasta.gz
1870
```    
_Summarize an annotation file
Go to the most current download genomes section at flybase.org and download the gzipped gtf annotation file for D. melanogaster._

## File integrity
__Verify the file integrity of the gzipped gtf annotation using a checksum__
 
    wget ftp://ftp.flybase.net/genomes/Drosophila_melanogaster/dmel_r6.24_FB2018_05/gtf/dmel-all-r6.24.gtf.gz
    wget ftp://ftp.flybase.net/genomes/Drosophila_melanogaster/dmel_r6.24_FB2018_05/gtf/md5sum.txt
    md5sum -c md5sum.txt.1
    dmel-all-r6.24.gtf.gz: OK

__Print a summary report with the following information:__
  1. Total number of features of each type, sorted from the most common to the least common
  
    zcat *.gtf.gz | cut -f3 | sort | uniq -c | sort -rn        
    187315 exon
    161014 CDS
    46339 5UTR
    33358 3UTR
    30591 start_codon
    30533 stop_codon
    30507 mRNA
    17772 gene
    2961 ncRNA
    485 miRNA
    334 pseudogene
    312 tRNA
    299 snoRNA
    262 pre_miRNA
    115 rRNA
    32 snRNA
  
  2. Total number of genes per chromosome arm (X, Y, 2L, 2R, 3L, 3R, 4)
   
    zcat *.gtf.gz | cut -f1,3 | grep -w "gene" | grep -E -w -o 'X|Y|2L|2R|3L|3R|4' | sort | uniq -c
    3501 2L
    3628 2R
    3464 3L
    4202 3R
    111 4
    2676 X
    113 Y


