```bash
(envs3) [tujie@AEE ARCS]$  arcs-make arcs draft=/usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp reads=/usr/section2/kp/tujie/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb z=1000
perl -ne 'chomp; if(/>/){$ct+=1; print ">$ct\n";}else{print "$_\n";} ' < /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.fa > /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa 
touch empty.fof
bwa index /usr/section2/kp/tujie/output/bwa/KP_p17S4_3/KP_p17S4.srp.renamed.fa 
[bwa_index] Pack FASTA... 9.47 sec
[bwa_index] Construct BWT for the packed sequence...
[BWTIncCreate] textLength=2469791450, availableWord=185783168
[BWTIncConstructFromPacked] 10 iterations done. 99999994 characters processed.

```
