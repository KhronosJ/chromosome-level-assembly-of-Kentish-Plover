# arcs构建scaffold
使用数据为第二次二代纠错后数据
```bash
(base) [tujie@AEE ~]$ conda activate env2
##安装arcs-1.2.1
(env2) [tujie@AEE ~]$ conda install -c bioconda arcs
(env2) [tujie@AEE ~]$ mkdir /usr/section2/kp/tujie/output/ARCS
(env2) [tujie@AEE ~]$ gzip /usr/section2/kp/tujie/output/bwa/KP_p17S4_2/KP_p17S4.srp.fa
(env2) [tujie@AEE ~]$ cd /usr/section2/kp/tujie/output/ARCS
