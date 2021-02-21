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

```
