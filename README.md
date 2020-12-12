# chromosome-level-assembly-of-Kentish-Plover
环颈鸻三代基因组染色体组装；实验记录
# 20-12-11

```bash
# derive consensus
(base) [tujie@AEE ~]$ cd /usr/section/tujie/disk/X101SC20061101Z01_jirou_Data_Release_20201022/wtdbg2/KP2_p17S4
(base) [tujie@AEE KP2_p17S4]$ /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtpoa-cns -i KP_2.ctg.lay.gz -fo KP_P17S4.ctg.fa
--
-- total memory      263853096.0 kB
-- available         182326424.0 kB
-- 40 cores
-- Starting program: /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtpoa-cns -i KP_2.ctg.lay.gz -fo KP_P17S4.ctg.fa
-- pid                     69753
-- date         Fri Dec 11 08:52:32 2020
--
1 contigs 1700 edges 0 bases
```

# 20-12-12

```bash
# 创建新环境env2
(base) [tujie@AEE ~]$ conda activate env2
# env2下安装minimap2-2.17
(env2) [tujie@AEE ~]$ conda install minimap2
# polish consensus
(env2) [tujie@AEE ~] $ cd /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP2_p17S4
(env2) [tujie@AEE KP2_p17S4]$ minimap2 -ax map-pb -r2k KP_P17S4.ctg.fa /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq
_ _ _
@PG     ID:minimap2     PN:minimap2     VN:2.17-r941    CL:minimap2 -ax map-pb -r2k KP_P17S4.ctg.fa /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq
[M::main::27.001*1.96] loaded/built the index for 814 target sequence(s)
[M::mm_mapopt_update::28.764*1.90] mid_occ = 85
[M::mm_idx_stat] kmer size: 19; skip: 10; is_hpc: 1; #seq: 814
[M::mm_idx_stat::29.784*1.87] distinct minimizers: 70560609 (55.93% are singletons); average occurrences: 2.268; average spacing: 7.814

```

