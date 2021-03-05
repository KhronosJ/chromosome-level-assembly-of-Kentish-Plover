```bash
##卸载conda安装的links
(envs3) [tujie@AEE lib]$ conda uninstall links
##重新安装links
(envs3) [tujie@AEE ARCS]$ wget https://github.com/bcgsc/LINKS/releases/download/v1.8.7/links_v1-8-7.tar.gz
(envs3) [tujie@AEE ARCS]$ tar -zxvf /usr/section2/kp/tujie/output/ARCS/links_v1-8-7.tar.gz -C /usr/section/tujie/opt/biosoft
(envs3) [tujie@AEE ARCS]$ cd /usr/section/tujie/opt/biosoft/links_v1.8.7/lib
(envs3) [tujie@AEE lib]$ rm -rf bloomfilter/
(envs3) [tujie@AEE lib]$ git clone git://github.com/bcgsc/bloomfilter.git
##安装swig
https://sourceforge.net/projects/swig/files/swig/swig-4.0.2/swig-4.0.2.tar.gz/download?use_mirror=nchc


```
