```bash
(base) [tujie@AEE ~]$ conda activate env2
bash: dirname: command not found...
bash: dirname: command not found...
(env2) [tujie@AEE ~]$ cd /usr/section2/kp/tujie/output/ARCS
(env2) [tujie@AEE ARCS]$ gzip /usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq
(env2) [tujie@AEE ARCS]$  arcs-make arcs draft=/usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp reads=/usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb z=1000
---
perl -ne 'chomp; if(/>/){$ct+=1; print ">$ct\n";}else{print "$_\n";} ' < /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.fa > /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa
touch empty.fof
bwa index /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa
[bwa_index] Pack FASTA... 9.62 sec
[bwa_index] Construct BWT for the packed sequence...
[BWTIncCreate] textLength=2469791450, availableWord=185783168
[BWTIncConstructFromPacked] 10 iterations done. 99999994 characters processed.
[BWTIncConstructFromPacked] 20 iterations done. 199999994 characters processed.
[BWTIncConstructFromPacked] 30 iterations done. 299999994 characters processed.
[BWTIncConstructFromPacked] 40 iterations done. 399999994 characters processed.
[BWTIncConstructFromPacked] 50 iterations done. 499999994 characters processed.
[BWTIncConstructFromPacked] 60 iterations done. 599999994 characters processed.
[BWTIncConstructFromPacked] 70 iterations done. 699999994 characters processed.
[BWTIncConstructFromPacked] 80 iterations done. 799999994 characters processed.
[BWTIncConstructFromPacked] 90 iterations done. 899999994 characters processed.
[BWTIncConstructFromPacked] 100 iterations done. 999999994 characters processed.
[BWTIncConstructFromPacked] 110 iterations done. 1099999994 characters processed.
[BWTIncConstructFromPacked] 120 iterations done. 1199999994 characters processed.
[BWTIncConstructFromPacked] 130 iterations done. 1299999994 characters processed.
[BWTIncConstructFromPacked] 140 iterations done. 1399999994 characters processed.
[BWTIncConstructFromPacked] 150 iterations done. 1499999994 characters processed.
[BWTIncConstructFromPacked] 160 iterations done. 1599999994 characters processed.
[BWTIncConstructFromPacked] 170 iterations done. 1699999994 characters processed.
[BWTIncConstructFromPacked] 180 iterations done. 1799979690 characters processed.
[BWTIncConstructFromPacked] 190 iterations done. 1893563082 characters processed.
[BWTIncConstructFromPacked] 200 iterations done. 1976736202 characters processed.
[BWTIncConstructFromPacked] 210 iterations done. 2050656698 characters processed.
[BWTIncConstructFromPacked] 220 iterations done. 2116353402 characters processed.
[BWTIncConstructFromPacked] 230 iterations done. 2174740794 characters processed.
[BWTIncConstructFromPacked] 240 iterations done. 2226631626 characters processed.
[BWTIncConstructFromPacked] 250 iterations done. 2272748314 characters processed.
[BWTIncConstructFromPacked] 260 iterations done. 2313732938 characters processed.
[BWTIncConstructFromPacked] 270 iterations done. 2350156138 characters processed.
[BWTIncConstructFromPacked] 280 iterations done. 2382525162 characters processed.
[BWTIncConstructFromPacked] 290 iterations done. 2411290778 characters processed.
[BWTIncConstructFromPacked] 300 iterations done. 2436853706 characters processed.
[BWTIncConstructFromPacked] 310 iterations done. 2459570058 characters processed.
[bwt_gen] Finished constructing BWT in 315 iterations.
[bwa_index] 1171.06 seconds elapse.
[bwa_index] Update BWT... 8.21 sec
[bwa_index] Pack forward-only FASTA... 5.99 sec
[bwa_index] Construct SA from BWT and Occ... 521.65 sec
[main] Version: 0.7.17-r1188
[main] CMD: bwa index /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa
[main] Real time: 1716.931 sec; CPU: 1716.532 sec
sh -c 'bwa mem -t8 -C -p /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa /usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq.gz | samtools view -Sb - | samtools sort -@8 -n - -o /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.sorted.bam' 
sh: samtools: command not found
sh: samtools: command not found
[M::bwa_idx_load_from_disk] read 0 ALT contigs
make: *** [/usr/section/tujie/miniconda3/envs/env2/bin/share/arcs-1.2.1-1/Examples/arcs-make:213: /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.sorted.bam] Error 127
```
