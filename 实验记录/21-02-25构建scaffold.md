```bash
(envs3) [tujie@AEE ARCS]$conda install abyss
(envs3) [tujie@AEE ARCS]$conda install minimap2
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
 pid 64949
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

=> Getting scaffold sizes... Thu Feb 25 18:10:05 2021
Saw 814 sequences.

=> Reading alignment files... Thu Feb 25 18:10:10 2021
Reading alignments: /dev/stdin
[M::mm_idx_gen::28.888*2.03] collected minimizers
[M::mm_idx_gen::32.477*2.60] sorted minimizers
[M::main::32.477*2.60] loaded/built the index for 814 target sequence(s)
[M::mm_mapopt_update::35.123*2.48] mid_occ = 138
[M::mm_idx_stat] kmer size: 15; skip: 10; is_hpc: 0; #seq: 814
[M::mm_idx_stat::36.427*2.42] distinct minimizers: 81880134 (49.22% are singletons); average occurrences: 2.824; average spacing: 5.340

---
> Writing the ABySS graph file... Fri Feb 26 02:37:26 2021

{ "All_barcodes_unfiltered":0, "All_barcodes_filtered":0, "Scaffold_end_barcodes":0, "Min_barcode_reads_threshold":50, "Max_barcode_reads_threshold":10000 }

=> Writing TSV file... Fri Feb 26 02:37:26 2021

=> Writing reads per barcode TSV file... Fri Feb 26 02:37:26 2021

=> Done.
Fri Feb 26 02:37:26 2021
python /usr/section/tujie/miniconda3/envs/envs3/bin/share/arcs-1.2.1-1/Examples/../Examples/makeTSVfile.py /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000_original.gv /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000.tigpair_checkpoint.tsv /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa
ln -s /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000.tigpair_checkpoint.tsv /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000_l5_a0.3.tigpair_checkpoint.tsv
LINKS -f /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa -s empty.fof -b /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000_l5_a0.3 -l 5 -a 0.3 -z 1000
bash: LINKS: command not found
make: *** [/usr/section/tujie/miniconda3/envs/envs3/bin/share/arcs-1.2.1-1/Examples/arcs-make:296: /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp_c5_m50-10000_cut250_s98_r0.05_e30000_z1000_l5_a0.3.scaffolds.fa] Error 127


```
