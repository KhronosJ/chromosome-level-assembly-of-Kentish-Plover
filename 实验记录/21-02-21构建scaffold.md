```bash
##env2环境下安装samtools-1.7
(env2) [tujie@AEE ~]$ conda install samtools
(env2) [tujie@AEE ARCS]$  arcs-make arcs draft=/usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp reads=/usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb z=1000
---
##报错
[BWTIncConstructFromPacked] 280 iterations done. 2382525162 characters processed.
[BWTIncConstructFromPacked] 290 iterations done. 2411290778 characters processed.
[BWTIncConstructFromPacked] 300 iterations done. 2436853706 characters processed.
[BWTIncConstructFromPacked] 310 iterations done. 2459570058 characters processed.
[bwt_gen] Finished constructing BWT in 315 iterations.
[bwa_index] 1053.43 seconds elapse.
[bwa_index] Update BWT... 7.86 sec
[bwa_index] Pack forward-only FASTA... 5.78 sec
[bwa_index] Construct SA from BWT and Occ... 399.16 sec
[main] Version: 0.7.17-r1188
[main] CMD: bwa index /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa
[main] Real time: 1476.194 sec; CPU: 1475.864 sec
sh -c 'bwa mem -t8 -C -p /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa /usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq.gz | samtools view -Sb - | samtools sort -@8 -n - -o /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.sorted.bam'
samtools: error while loading shared libraries: samtoolslibcrypto.so.1.0.0: cannot open shared object file: : error while loading shared libraries: libcrypto.so.1.0.0: cannot open shared object file: No such file or directory
No such file or directory
[M::bwa_idx_load_from_disk] read 0 ALT contigs
make: *** [/usr/section/tujie/miniconda3/envs/env2/bin/share/arcs-1.2.1-1/Examples/arcs-make:213: /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.sorted.bam] Error 127
##原因为samtools版本为1.7
##重新安装samtools 1.9
(env2) [tujie@AEE ARCS]$ conda uninstall samtools
(env2) [tujie@AEE ARCS]$ conda install samtools=1.9
##报错
##在envs3环境下安装samtools和arcs
(envs3) [tujie@AEE ARCS]$ conda install samtools=1.9
(envs3) [tujie@AEE ARCS]$ conda install bwa
(envs3) [tujie@AEE ARCS]$  arcs-make arcs draft=/usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp reads=/usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb z=1000
##程序中断
[M::mem_process_seqs] Processed 4962 reads in 2372.588 CPU sec, 410.926 real sec
[M::process] 5014 single-end sequences; 0 paired-end sequences
[M::process] read 5020 sequences (80027985 bp)...
[M::mem_process_seqs] Processed 5014 reads in 2028.618 CPU sec, 267.138 real sec
[M::process] 5020 single-end sequences; 0 paired-end sequences
[M::process] read 5168 sequences (80000601 bp)...
[M::mem_process_seqs] Processed 5020 reads in 1962.249 CPU sec, 265.454 real sec
[M::process] 5168 single-end sequences; 0 paired-end sequences
[M::process] read 4886 sequences (80033455 bp)...
[M::mem_process_seqs] Processed 5168 reads in 2673.919 CPU sec, 706.813 real sec
[M::process] 4886 single-end sequences; 0 paired-end sequences
[M::process] read 4950 sequences (80004776 bp)...
[M::mem_process_seqs] Processed 4886 reads in 1973.483 CPU sec, 257.785 real sec
[M::process] 4950 single-end sequences; 0 paired-end sequences
[M::process] read 4892 sequences (80022490 bp)...
[M::mem_process_seqs] Processed 4950 reads in 2110.366 CPU sec, 316.421 real sec
[M::process] 4892 single-end sequences; 0 paired-end sequences
[M::process] read 5046 sequences (80010406 bp)...
[M::mem_process_seqs] Processed 4892 reads in 1955.841 CPU sec, 250.350 real sec
[M::process] 5046 single-end sequences; 0 paired-end sequences
[M::process] read 5090 sequences (80001908 bp)...



```
