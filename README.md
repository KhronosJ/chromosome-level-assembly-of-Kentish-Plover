[toc]
# chromosome-level-assembly-of-Kentish-Plover
环颈鸻三代基因组染色体组装；实验记录
## 20-10-24

基于***conda-4.9.0***

安装***canu-2.0***

```bash
##激活conda下envs1小环境
conda activate envs1
##通过conda在envs1环境下安装canu
conda install canu
```

## 20-10-25

安装***wtdbg2-2.5***

```bash
##下载地址https://github.com/ruanjue/wtdbg2/releases/tag/v2.5
##解压
tar zxvf /usr/section/tujie/wtdbg-2.5_x64_linux.tgz -C /usr/section/tujie/opt/biosoft
```

## 20-11-06

从硬盘上传文件到/usr/section/tujie/Projects/KP-chromosome-level-assembly/ 

## 20-11-10

删除服务器上文件，将硬盘挂载到染色体，路径/usr/section/tujie/disk/$RECYCLE.BIN/pacbio

## 20-11-12

安装***samtools-1.11***

~~~bash
##base环境下安装
conda install samtools
~~~

## 20-11-13

安装***bedtools-2.29.2***

~~~bash
##激活conda下envs1小环境
conda activate envs1
##安装bedtools
conda install bedtools
~~~

## 20-11-14

~~~bash
##bam文件转换为fastq格式
bedtools bamtofastq -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/pacbio/m64165_201016_013002.subreads.bam -fq KPpb.fq
mv KPpb.fq /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022
~~~

## 20-11-15

canu纠错

```bash
(envs1) [tujie@AEE ~]$ canu -correct \-p KPPB -d /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022 genomeSize=1g minReadLength=5000  corOutCoverage=270 -pacbio-raw /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq
# -p 输出文件的前缀，必须指定
# -d 输出文件夹
# genomeSize 估计的基因组大小
# minReadLength read长度小于这个值将不会被用来组装
# -pacbio-raw 原始测序文件
# maxThreads=20 线程
```

## 20-11-20

取7G数据10线程检验canu纠错速度

~~~bash
(envs1) [tujie@AEE ~]$ canu -correct \
> -p pre-KPPB -d /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022 \
> genomeSize=1g minReadLength=5000 corOutCoverage=7 maxThreads=20 -pacbio-raw /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq
#Starting command on Sat Nov 21 22:28:50 2020 with 2066.351 GB free disk spac
~~~

## 20-11-24

### KP

~~~bash
(envs1) [tujie@AEE ~]$ cd /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux
(envs1) [tujie@AEE wtdbg-2.5_x64_linux]$ wtdbg2 -x sq -g 1G 
-i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq 
-o KP -K 2000 --edge-min 4 -p 17 -S 1 -L 5000 --tidy-reads 5000
# -x测序平台sq=pacbio sequel
# -g预估基因组大小
# -K Filter high frequency kmers, maybe repetitive, [1000.05]
             >= 1000 and indexing >= (1 - 0.05) * total_kmers_count
# -k普通k-mers的长度
# -p HPC k-mers长度
# -e 默认为3，the minimum read coverage of an edge in the assembly graph
# https://github.com/ruanjue/wtdbg2/blob/master/README.md
# https://github.com/ruanjue/wtdbg2/blob/master/README-ori.md
-- total memory      263853096.0 kB
-- available         115001592.0 kB
-- 40 cores
-- Starting program: wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP -K 2000 --edge-min 4 -p 17 -S 1 -L 5000 --tidy-reads 5000
-- pid                    152095
-- date         Tue Nov 24 10:13:21 2020
#out
Quatiles:
   10%   20%   30%   40%   50%   60%   70%   80%   90%   95%
   145   252   464   657   819   989  1201  1552  2803  6348
** PROC_STAT(0) **: real 11853.128 sec, user 6753.530 sec, sys 410.600 sec, maxrss 30574896.0 kB, maxvsize 31865296.0 kB
[Tue Nov 24 13:32:05 2020] - Total kmers = 86090263
[Tue Nov 24 13:32:05 2020] - average kmer depth = 287
[Tue Nov 24 13:32:05 2020] - 3640 low frequency kmers (<2)
[Tue Nov 24 13:32:05 2020] - 964216 high frequency kmers (>2000)
[Tue Nov 24 13:32:05 2020] - indexing 85122407 kmers, 24472991711 instances (at most)
195312411 bins
[Tue Nov 24 15:06:48 2020] - indexed  85122407 kmers, 24470741194 instances
[Tue Nov 24 15:06:49 2020] - masked 18211985 bins as closed
[Tue Nov 24 15:06:49 2020] - sorting
** PROC_STAT(0) **: real 17815.676 sec, user 26301.470 sec, sys 5026.510 sec, maxrss 173938124.0 kB, maxvsize 176102096.0 kB
[Tue Nov 24 15:11:27 2020] Done
6000|262794
44000|2610388Killed
~~~

### KP_1

~~~bash
(base) [tujie@AEE ~]$ cd /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux
#--edge-min 4→ --edge-min 2 --rescue-low-cov-edges
(base) [tujie@AEE wtdbg-2.5_x64_linux]$  wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_1 -K 2000 --edge-min 2 --rescue-low-cov-edges -p 17 -S 1 -L 5000 --tidy-reads 5000

-- total memory      263853096.0 kB
-- available         217643448.0 kB
-- 40 cores
-- Starting program: wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_1 -K 2000 --edge-min 2 --rescue-low-cov-edges -p 17 -S 1 -L 5000 --tidy-reads 5000
-- pid                    153427
-- date         Tue Nov 24 10:33:46 2020
## out
Quatiles:
   10%   20%   30%   40%   50%   60%   70%   80%   90%   95%
   145   252   464   657   819   989  1201  1552  2803  6348
** PROC_STAT(0) **: real 10688.090 sec, user 6678.800 sec, sys 363.400 sec, maxrss 30569156.0 kB, maxvsize 31859668.0 kB
[Tue Nov 24 13:31:55 2020] - Total kmers = 86090263
[Tue Nov 24 13:31:55 2020] - average kmer depth = 287
[Tue Nov 24 13:31:55 2020] - 3640 low frequency kmers (<2)
[Tue Nov 24 13:31:55 2020] - 964216 high frequency kmers (>2000)
[Tue Nov 24 13:31:55 2020] - indexing 85122407 kmers, 24472991711 instances (at most)
##out of memory
400000Killed
~~~

## 20-11-28

### KP_2

```bash
(base) [tujie@AEE ~]$ cd /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP_2
#--edge-min 4 -p 17 -S 1→4 --tidy-reads 5000→8000
(base) [tujie@AEE KP_2]$ /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_2 -K 2000 --edge-min 4 -p 17 -S 4 -L 5000 --tidy-reads 8000
--
-- total memory      263853096.0 kB
-- available         253616176.0 kB
-- 40 cores
-- Starting program: /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_2 -K 2000 --edge-min 4 -p 17 -S 4 -L 5000 --tidy-reads 8000
-- pid                    112066
-- date         Sat Nov 28 03:11:46 2020
--
[Sat Nov 28 03:11:46 2020] loading reads
```

---

### output

```bash
[Mon Nov 30 05:06:11 2020] deleted 89 isolated nodes
[Mon Nov 30 05:06:11 2020] building unitigs
[Mon Nov 30 05:06:12 2020] TOT 1288317184, CNT 1662, AVG 775161, MAX 58297856, N50 19153920, L50 21, N90 2285056, L90 85, Min 1280
[Mon Nov 30 05:06:13 2020] output "/usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP_2.frg.nodes". Done.
[Mon Nov 30 05:06:13 2020] generating links
[Mon Nov 30 05:06:14 2020] generated 1279 links
[Mon Nov 30 05:06:14 2020] output "/usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP_2.frg.dot.gz". Done.
[Mon Nov 30 05:06:14 2020] rescue 0 weak links
[Mon Nov 30 05:06:14 2020] deleted 117 binary links
[Mon Nov 30 05:06:14 2020] cut 120 transitive links
[Mon Nov 30 05:06:14 2020] remove 65 boomerangs
[Mon Nov 30 05:06:14 2020] remove 509 weak branches
[Mon Nov 30 05:06:14 2020] cut 35 tips
[Mon Nov 30 05:06:14 2020] pop 2 bubbles
[Mon Nov 30 05:06:14 2020] detached 1 repeat-associated paths
[Mon Nov 30 05:06:14 2020] cut 2 tips
[Mon Nov 30 05:06:14 2020] output "/usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP_2.ctg.dot.gz". Done.
[Mon Nov 30 05:06:14 2020] building contigs
[Mon Nov 30 05:06:14 2020] searched 1234 contigs
[Mon Nov 30 05:06:14 2020] Estimated: TOT 1290913792, CNT 814, AVG 1585890, MAX 97530624, N50 24479744, L50 14, N90 3923200, L90 55, Min 4864
[Mon Nov 30 05:50:42 2020] output 814 contigs
[Mon Nov 30 05:50:45 2020] Program Done
** PROC_STAT(TOTAL) **: real 182633.474 sec, user 699311.180 sec, sys 15923.510 sec, maxrss 67379684.0 kB, maxvsize 116827772.0 kB

```

## 20-12-01

### KP3

```bash
(base) [tujie@AEE ~]$ cd /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP3_p18S4
#-p 18
(base) [tujie@AEE KP3_p18S4]$ /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_p18S4 -K 2000 --edge-min 4 -p 18 -S 4 -L 5000 --tidy-reads 8000
--
-- total memory      263853096.0 kB
-- available         251314200.0 kB
-- 40 cores
-- Starting program: /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_p18S4 -K 2000 --edge-min 4 -p 18 -S 4 -L 5000 --tidy-reads 8000
-- pid                    191641
-- date         Tue Dec  1 00:12:34 2020
--
[Tue Dec  1 00:12:34 2020] loading reads
```

#### output

```bash
Quatiles:
   10%   20%   30%   40%   50%   60%   70%   80%   90%   95%
    43    76   132   192   244   301   374   504  1057  3034
** PROC_STAT(0) **: real 3583.297 sec, user 2422.910 sec, sys 141.220 sec, maxrss 14403296.0 kB, maxvsize 15926404.0 kB
[Tue Dec  1 01:12:18 2020] - Total kmers = 64487488
[Tue Dec  1 01:12:18 2020] - average kmer depth = 92
[Tue Dec  1 01:12:18 2020] - 269225 low frequency kmers (<2)
[Tue Dec  1 01:12:18 2020] - 77311 high frequency kmers (>2000)
[Tue Dec  1 01:12:18 2020] - indexing 64140952 kmers, 5919152727 instances (at most)
170503312 bins
[Tue Dec  1 01:28:14 2020] - indexed  64140952 kmers, 5918576320 instances
[Tue Dec  1 01:28:14 2020] - masked 11090057 bins as closed
[Tue Dec  1 01:28:14 2020] - sorting
** PROC_STAT(0) **: real 4574.420 sec, user 6239.750 sec, sys 376.830 sec, maxrss 49103524.0 kB, maxvsize 52660196.0 kB
[Tue Dec  1 01:28:49 2020] Done
1931660 reads|total hits 64401676
** PROC_STAT(0) **: real 77289.446 sec, user 297705.560 sec, sys 9160.080 sec, maxrss 52001716.0 kB, maxvsize 56301164.0 kB
[Tue Dec  1 21:40:44 2020] sorting rdhits ... Done
[Tue Dec  1 21:40:49 2020] clipping ... 27.21% bases
[Tue Dec  1 21:40:55 2020] generating regs ... 888396136
[Tue Dec  1 21:42:38 2020] sorting regs ...  Done
[Tue Dec  1 21:43:14 2020] generating intervals ...  31168719 intervals
[Tue Dec  1 21:43:23 2020] selecting important intervals from 31168719 intervals
[Tue Dec  1 21:46:23 2020] Intervals: kept 1252422, discarded 29916297
** PROC_STAT(0) **: real 77628.452 sec, user 298473.150 sec, sys 9285.270 sec, maxrss 52001716.0 kB, maxvsize 60758616.0 kB
[Tue Dec  1 21:46:23 2020] Done, 1252422 nodes
[Tue Dec  1 21:46:23 2020] output "KP_p18S4.1.nodes". Done.
[Tue Dec  1 21:46:46 2020] median node depth = 23
[Tue Dec  1 21:46:46 2020] masked 468 high coverage nodes (>200 or <4)
[Tue Dec  1 21:47:07 2020] masked 1200 repeat-like nodes by local subgraph analysis
[Tue Dec  1 21:47:07 2020] generating edges
[Tue Dec  1 21:49:14 2020] Done, 43876197 edges
[Tue Dec  1 21:49:14 2020] output "KP_p18S4.1.reads". Done.
[Tue Dec  1 21:49:34 2020] output "KP_p18S4.1.dot.gz". Done.
[Tue Dec  1 21:50:35 2020] graph clean
[Tue Dec  1 21:50:39 2020] rescued 2802 low cov edges
[Tue Dec  1 21:50:41 2020] deleted 582 binary edges
[Tue Dec  1 21:50:41 2020] deleted 12801 isolated nodes
[Tue Dec  1 21:50:48 2020] cut 772522 transitive edges
[Tue Dec  1 21:50:48 2020] output "KP_p18S4.2.dot.gz". Done.
[Tue Dec  1 21:51:06 2020] 145312 bubbles; 6537 tips; 68 yarns; rescued 294279 high edges
[Tue Dec  1 21:51:07 2020] deleted 298825 isolated nodes
[Tue Dec  1 21:51:07 2020] output "KP_p18S4.3.dot.gz". Done.
[Tue Dec  1 21:51:10 2020] cut 863 branching nodes
[Tue Dec  1 21:51:11 2020] deleted 160 isolated nodes
[Tue Dec  1 21:51:11 2020] building unitigs
[Tue Dec  1 21:51:12 2020] TOT 1279265280, CNT 2154, AVG 593903, MAX 56978432, N50 16020992, L50 25, N90 1286144, L90 116, Min 1280
[Tue Dec  1 21:51:12 2020] output "KP_p18S4.frg.nodes". Done.
[Tue Dec  1 21:51:12 2020] generating links
[Tue Dec  1 21:51:14 2020] generated 1875 links
[Tue Dec  1 21:51:14 2020] output "KP_p18S4.frg.dot.gz". Done.
[Tue Dec  1 21:51:14 2020] rescue 0 weak links
[Tue Dec  1 21:51:14 2020] deleted 134 binary links
[Tue Dec  1 21:51:14 2020] cut 202 transitive links
[Tue Dec  1 21:51:14 2020] remove 87 boomerangs
[Tue Dec  1 21:51:14 2020] remove 700 weak branches
[Tue Dec  1 21:51:14 2020] cut 49 tips
[Tue Dec  1 21:51:14 2020] pop 4 bubbles
[Tue Dec  1 21:51:14 2020] detached 3 repeat-associated paths
[Tue Dec  1 21:51:14 2020] cut 4 tips
[Tue Dec  1 21:51:14 2020] output "KP_p18S4.ctg.dot.gz". Done.
[Tue Dec  1 21:51:14 2020] building contigs
[Tue Dec  1 21:51:14 2020] searched 1453 contigs
[Tue Dec  1 21:51:14 2020] Estimated: TOT 1283054848, CNT 949, AVG 1352008, MAX 59054592, N50 22924032, L50 17, N90 3228928, L90 68, Min 4864
[Tue Dec  1 22:25:19 2020] output 949 contigs
[Tue Dec  1 22:25:21 2020] Program Done
** PROC_STAT(TOTAL) **: real 79966.914 sec, user 307244.380 sec, sys 9392.730 sec, maxrss 52001716.0 kB, maxvsize 60758616.0 kB
```



### KP4

```bash
(base) [tujie@AEE ~]$ cd /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP4_p19S4
#-p 19
(base) [tujie@AEE KP4_p19S4]$/usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_p19S4 -K 2000 --edge-min 4 -p 19 -S 4 -L 5000 --tidy-reads 8000
--
-- total memory      263853096.0 kB
-- available         249137556.0 kB
-- 40 cores
-- Starting program: /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_p19S4 -K 2000 --edge-min 4 -p 19 -S 4 -L 5000 --tidy-reads 8000
-- pid                    191840
-- date         Tue Dec  1 00:15:13 2020
--
[Tue Dec  1 00:15:13 2020] loading reads
```

#### output

```bash
Aborted (core dumped)
```

### KP5

```bash
(base) [tujie@AEE ~]$ cd /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP5_p17S5
#-P 17 -S 5
(base) [tujie@AEE KP5_p17S5]$/usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_p17S5 -K 2000 --edge-min 4 -p 17 -S 5 -L 5000 --tidy-reads 8000
--
-- total memory      263853096.0 kB
-- available         241856700.0 kB
-- 40 cores
-- Starting program: /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_p17S5 -K 2000 --edge-min 4 -p 17 -S 5 -L 5000 --tidy-reads 8000
-- pid                    192698
-- date         Tue Dec  1 00:26:48 2020
--
[Tue Dec  1 00:26:48 2020] loading reads
```

#### output

```bash
[Wed Dec  2 16:33:17 2020] deleted 191088 isolated nodes
[Wed Dec  2 16:33:17 2020] output "KP_p17S5.3.dot.gz". Done.
[Wed Dec  2 16:33:21 2020] cut 243 branching nodes
[Wed Dec  2 16:33:22 2020] deleted 32 isolated nodes
[Wed Dec  2 16:33:22 2020] building unitigs
[Wed Dec  2 16:33:23 2020] TOT 1285582336, CNT 1523, AVG 844112, MAX 81632512, N50 18874880, L50 20, N90 2770688, L90 82, Min 1280
[Wed Dec  2 16:33:23 2020] output "KP_p17S5.frg.nodes". Done.
[Wed Dec  2 16:33:24 2020] generating links
[Wed Dec  2 16:33:25 2020] generated 871 links
[Wed Dec  2 16:33:25 2020] output "KP_p17S5.frg.dot.gz". Done.
[Wed Dec  2 16:33:25 2020] rescue 0 weak links
[Wed Dec  2 16:33:25 2020] deleted 84 binary links
[Wed Dec  2 16:33:25 2020] cut 59 transitive links
[Wed Dec  2 16:33:25 2020] remove 56 boomerangs
[Wed Dec  2 16:33:25 2020] remove 247 weak branches
[Wed Dec  2 16:33:25 2020] cut 25 tips
[Wed Dec  2 16:33:25 2020] pop 1 bubbles
[Wed Dec  2 16:33:25 2020] detached 3 repeat-associated paths
[Wed Dec  2 16:33:25 2020] cut 0 tips
[Wed Dec  2 16:33:25 2020] output "KP_p17S5.ctg.dot.gz". Done.
[Wed Dec  2 16:33:25 2020] building contigs
[Wed Dec  2 16:33:25 2020] searched 1161 contigs
[Wed Dec  2 16:33:25 2020] Estimated: TOT 1288049920, CNT 759, AVG 1697036, MAX 100953344, N50 38095872, L50 11, N90 4219392, L90 52, Min 5120
[Wed Dec  2 17:15:46 2020] output 759 contigs
[Wed Dec  2 17:15:49 2020] Program Done
** PROC_STAT(TOTAL) **: real 146941.284 sec, user 563480.270 sec, sys 12526.500 sec, maxrss 59522848.0 kB, maxvsize 116724220.0 kB
```

## 20-12-06

### KP6

```bash
(base) [tujie@AEE ~]$ cd /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/wtdbg2/KP6_p21S4
#-p 21 -S 4
(base) [tujie@AEE KP4_p19S4]$/usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_p21S4 -K 2000 --edge-min 4 -p 21 -S 4 -L 5000 --tidy-reads 8000
--
-- total memory      263853096.0 kB
-- available         245383696.0 kB
-- 40 cores
-- Starting program: /usr/section/tujie/opt/biosoft/wtdbg-2.5_x64_linux/wtdbg2 -x sq -g 1G -i /usr/section/tujie/disk/X101SC20061101-Z01_jirou_Data_Release_20201022/KPpb.fq -o KP_p21S4 -K 2000 --edge-min 4 -p 21 -S 4 -L 5000 --tidy-reads 8000
-- pid                    178756
-- date         Sun Dec  6 07:29:13 2020
--
[Sun Dec  6 07:29:13 2020] loading reads
```


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

