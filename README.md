# HW3
## Summarize a genome assembly
Get the chromosome fasta file.
```
curl ftp://ftp.flybase.net/genomes/Drosophila_melanogaster/current/fasta/dmel-all-chromosome-r6.24.fasta.gz  -O
```

Verify the file integrity of the gzipped fasta file using a checksum.
```
curl ftp://ftp.flybase.net/genomes/Drosophila_melanogaster/current/fasta/md5sum.txt | grep chromosome | md5sum -c
```
The result is ```dmel-all-chromosome-r6.24.fasta.gz: OK```.

To calculate the size, load the software first.
```
module load jje/kent
```
And faSize is used, the result is saved in size.txt.
```
faSize -tab dmel-all-chromosome-r6.24.fasta.gz > size.txt
```


## Summarize an annotation file
Get the gtf file.
```
curl ftp://ftp.flybase.net/genomes/Drosophila_melanogaster/current/gtf/dmel-all-r6.24.gtf.gz -O
```

Verify the file integrity of the gzipped fasta file using a checksum.
```
curl ftp://ftp.flybase.net/genomes/Drosophila_melanogaster/current/gtf/md5sum.txt | md5sum -c
```
The result is ```dmel-all-r6.24.gtf.gz: OK```.

Then the report for thr total number of features of each type, sorted from the most common to the least common.
```
zcat dmel-all-r6.24.gtf.gz | gawk '{print $3}' | sort | uniq -c | sort -rn | nl >  feature_report.txt
```

Total number of genes on chromosome X
```
zcat dmel-all-r6.24.gtf.gz | gawk '{print $1,$3}' | grep '\<gene' | grep ‘\<X’ | uniq -c
```
It shows 2676. For Y, 113. For 2L, 3501. For 2R, 3628. For 3L, 3463. For 3R, 4202. For 4, 111.
