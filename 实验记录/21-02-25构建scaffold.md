```bash
(envs3) [tujie@AEE ARCS]$conda install abyss
(envs3) [tujie@AEE ARCS]$conda install minimap2
(envs3) [tujie@AEE ARCS]$ arcs-make arcs-long draft=/usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp reads=/usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb z=1000
perl -ne 'chomp; if(/>/){$ct+=1; print ">$ct\n";}else{print "$_\n";} ' < /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.fa > /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa 
touch empty.fof
sh -c 'gunzip -c /usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq.gz | /usr/section/tujie/miniconda3/envs/envs3/bin/share/arcs-1.2.1-1/Examples/../Examples/long-to-linked-pe -l250 --fastq | bgzip -@8 > /usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.cut250.fq.gz'
```
