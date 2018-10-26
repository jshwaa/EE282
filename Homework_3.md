_Summarize a genome assembly
We will be working with the Drosophila melanogaster genome. You can start at flybase.org. Go to the most current download genomes section and download the gzipped fasta file for all chromosomes._

##File integrity
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
    Use grep to get all lines excluding headers (lines starting with ">") and whitespace to return all nucleotides:
    
        zgrep -v "^>" dmel* | grep [NAGTC] | tr -d "\n" | wc -m    
        143726002

        
    To confirm these are all either "A", "G", "C", "T", or "N" nucleotides, use:
        
        zgrep -v "^>" dmel* | zgrep [^ANTCG] | wc -m
        0
        
2. Total number of Ns:

3. Total number of sequences:

