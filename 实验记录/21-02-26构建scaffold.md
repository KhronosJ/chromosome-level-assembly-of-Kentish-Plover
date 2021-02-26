```bash
(envs3) [tujie@AEE ARCS]$ conda install Links
(envs3) [tujie@AEE ARCS]$ conda install Boost=1.61
(envs3) [tujie@AEE ARCS]$ conda install GCC
(envs3) [tujie@AEE ARCS]$ arcs-make arcs-long draft=/usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp reads=/usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb z=1000
perl -ne 'chomp; if(/>/){$ct+=1; print ">$ct\n";}else{print "$_\n";} ' < /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.fa > /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa 
touch empty.fof
minimap2 -ax map-ont -y -t8 --secondary=no /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa /usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.cut250.fq.gz | abyss-fixmate-ssq --all --qname | \
        samtools view -Sb - | samtools sort -@8 -O SAM -n - -o - | \
        arcs -f /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa -v -c 5 -m 50-10000 -s 98 -r 0.05 -e 30000 -z 1000 -d 0 --gap 100 -b /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000 --barcode-counts barcodeMultiplicityArcs.tsv /dev/stdin
arcs: /usr/section/tujie/miniconda3/envs/envs3/bin/../lib/libgomp.so.1: version `GOMP_4.0' not found (required by arcs)
arcs: /usr/section/tujie/miniconda3/envs/envs3/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.20' not found (required by arcs)
arcs: /usr/section/tujie/miniconda3/envs/envs3/bin/../lib/libstdc++.so.6: version `CXXABI_1.3.9' not found (required by arcs)
arcs: /usr/section/tujie/miniconda3/envs/envs3/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.21' not found (required by arcs)
[M::mm_idx_gen::28.522*1.96] collected minimizers
[M::mm_idx_gen::31.998*2.53] sorted minimizers
[M::main::31.998*2.53] loaded/built the index for 814 target sequence(s)
[M::mm_mapopt_update::34.827*2.40] mid_occ = 138
[M::mm_idx_stat] kmer size: 15; skip: 10; is_hpc: 0; #seq: 814
[M::mm_idx_stat::36.001*2.36] distinct minimizers: 81880134 (49.22% are singletons); average occurrences: 2.824; average spacing: 5.340
---
[M::worker_pipeline::20026.030*3.98] mapped 2014964 sequences
[M::worker_pipeline::20095.114*3.98] mapped 2015024 sequences
[M::worker_pipeline::20176.684*3.98] mapped 2014442 sequences
[M::worker_pipeline::20245.225*3.98] mapped 2014107 sequences
[M::worker_pipeline::20314.588*3.98] mapped 2013865 sequences
[M::worker_pipeline::20384.362*3.98] mapped 2013940 sequences
[M::worker_pipeline::20451.759*3.97] mapped 2013818 sequences
[M::worker_pipeline::20484.531*3.97] mapped 1007643 sequences
[M::main] Version: 2.17-r941
[M::main] CMD: minimap2 -ax map-ont -y -t8 --secondary=no /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa /usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.cut250.fq.gz
[M::main] Real time: 20485.009 sec; CPU: 81298.418 sec; Peak RSS: 9.752 GB
Mateless       82445  0.0281%
Unaligned   79167418  27%
Singleton   47758915  16.3%
FR         160947415  54.8%
RF            632908  0.215%
FF            190647  0.0649%
Different    4967802  1.69%
Total      293747550
[bam_sort_core] merging from 400 files and 8 in-memory blocks...
make: *** [/usr/section/tujie/miniconda3/envs/envs3/bin/share/arcs-1.2.1-1/Examples/arcs-make:233: /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000_original.gv] Error 1
```
```
(envs3) [tujie@AEE ARCS]$ conda uninstall gcc
(envs3) [tujie@AEE ARCS]$ conda install -c omgarcia gcc-6
(envs3) [tujie@AEE ARCS]$ arcs-make arcs-long draft=/usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp reads=/usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb z=1000
perl -ne 'chomp; if(/>/){$ct+=1; print ">$ct\n";}else{print "$_\n";} ' < /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.fa > /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa 
touch empty.fof
minimap2 -ax map-ont -y -t8 --secondary=no /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa /usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.cut250.fq.gz | abyss-fixmate-ssq --all --qname | \
        samtools view -Sb - | samtools sort -@8 -O SAM -n - -o - | \
        arcs -f /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa -v -c 5 -m 50-10000 -s 98 -r 0.05 -e 30000 -z 1000 -d 0 --gap 100 -b /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000 --barcode-counts barcodeMultiplicityArcs.tsv /dev/stdin
Reading user inputs...
Finished reading user inputs...entering runArcs()...
Running: arcs 1.2.1
ARCS method
 pid 78883
 -c 5
 -d 0
 -e 30000
 -l 0
 -m 50-10000
 -r 0.05
 -v 1
 -z 1000
 --gap=100
 -s 98
 -b /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000
 -g /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000.dist.gv
 --barcode-counts=barcodeMultiplicityArcs.tsv
 --tsv=/usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000_main.tsv
 -a NA
 -f /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa
 -u NA
 /dev/stdin

=> Getting scaffold sizes... Fri Feb 26 21:19:12 2021
Saw 814 sequences.

=> Reading alignment files... Fri Feb 26 21:19:17 2021
Reading alignments: /dev/stdin
[M::mm_idx_gen::28.427*1.89] collected minimizers
[M::mm_idx_gen::32.068*2.48] sorted minimizers
[M::main::32.068*2.48] loaded/built the index for 814 target sequence(s)
[M::mm_mapopt_update::34.879*2.36] mid_occ = 138
[M::mm_idx_stat] kmer size: 15; skip: 10; is_hpc: 0; #seq: 814
[M::mm_idx_stat::36.079*2.32] distinct minimizers: 81880134 (49.22% are singletons); average occurrences: 2.824; average spacing: 5.340

```

