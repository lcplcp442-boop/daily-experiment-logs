2026.08.07 xiPU ATAC 补测样本 BXAS-23 全流程 + 002_result 已处理结果汇总
项目：xiPU
Run ID：<!-- 待填 -->
目的：<!-- 待用户提供：ATAC 补测样本 BXAS-23 重新比对处理；将 ATAC/ChIP/RNA 已处理结果汇总入 002_result -->
运行目录：/public/home/cpliu25/analy/xiPU/
代码版本：analy 下无 git；本次脚本为 ATAC/bu/{bidui,ame,ame2,bw}（LSF normal 队列，-n 10）
输入：ATAC/bu/BXAS-23.merge.R1/R2.clean.fq.gz；参考 000_gene/Brassica_napus_NY7.fasta
今日操作：
- ATAC/bu（补测样本 BXAS-23，全流程 15:09–20:39）：
  - 比对 bidui--Job 75069869（bwa mem -t 4，4 核，normal），15:09 提交、16:36 Done（run 5075 s/约 85 min，max mem 2186 MB）→ BXAS-23.merge.sam（47.9 GB）。
  - 处理 ame--Job 75073376（sam→bam→flagstat→sort→拆 ChrM/ChrC→picard MarkDuplicates→MAPQ30 -q30 -f2），18:03 Done（run 3070 s/约 51 min，max mem 25.6 GB）。
  - 统计 ame2--Job 75079453，20:39 Done（10 s）→ tongji.txt。
  - bigwig/peak bw--Job 75079454，20:39 Done（33 s）。
- 002_result 汇总（17:12–17:25）：将已处理结果复制入 002_result--ATAC 29 文件、ChIP K273/K41/K43/K92 各约 40、RNA 20（均为 MAPQ30.bam/.bai/.bw/peaks 子集）；新建 002_result/weihebing 子目录（20:46，空）。
主要结果：
- BXAS-23 flagstat（xipuatac.txt）：111,239,381 reads，98.86% mapped，97.92% properly paired；ChrM 3,841,145、ChrC 44,152,695（线粒体/叶绿体 sort.bam 均 99.99% mapped）。
- MarkDuplicates 标记重复 37,254,569；gene_dup_removed.bam 25,990,972 reads（ame2/tongji）；MAPQ30 properly-paired 3,448,221 reads（ame.out）。
- macs2（BAMPE，--nomodel --shift -100 --extsize 200，-g 603088334）1,723,746 fragments→39,277 peaks。
状态：ATAC/bu BXAS-23 比对+处理+统计完成；bw 作业部分失败（见异常）；002_result 已处理结果汇总完成（weihebing 待填）。
异常：bw Job 75079454 部分失败--bamCoverage（command not found，.bw 未生成）、run_spp.R（spp 包缺失，.Rout/.qual 未生成）、bamToBed/intersectBed（command not found，.bed/.intersectBed 0 字节，FRIP 峰内 reads 数未算出）；macs2 peaks 正常。作业环境 PATH/conda env 缺工具。
注意：Run ID、目的待补；原 08-07 上午版日志误记"08-07 无新作业"，实际 15:09 起有上述 ATAC 补测全流程；08-06 WGBS/000_gene/WGS 内容已记于 08-06 日志，本条不再重复。
