2026.08.11 xiPU WGBS 甲基化 bw 全部完成 + WGS 比对提交
项目：xiPU
运行目录：/public/home/cpliu25/analy/xiPU/
代码版本：analy 下无 git；本次脚本为 WGBS/bw（08-08 提交）、WGS/{bidui,ame,ame2,bianyi}
输入：WGBS/*.methratio.txt；WGS 各样本 *.R1/R2.clean.fq.gz；参考 000_gene/Brassica_napus_NY7.fasta
今日操作：
- WGBS 链特异 bw 全部跑完（08-08 提交的 Job 75090013，batmeth2_to_bigwig.py -sort -strand）：凌晨起逐样本产出 CDA 00:02–00:06、CY2 01:45–01:55、NY1 03:16–03:23、NY7 04:54–05:03、SL 06:19–06:26，每样本 4 个（cg/chg/chh/c）共 20 个 .bw，06:26 作业收尾（bw75098938.out/err）。
- 上午编写 WGS 流程脚本（WGS/ 下）：
  - bidui：bwa mem -t 4 -M -R "@RG\tID/SM/LB:${prefix}\tPL:ILLUMINA" 比对到 000_gene/Brassica_napus_NY7.fasta，产出 sam；
  - ame/ame2：sam->bam（samtools view -b）-> flagstat -> sort + index -> 按 rname 拆分 ChrM/ChrC（叶绿体/线粒体）与 gene -> markdup -> MAPQ30 -> flagstat 汇总（xipuwgs.txt/tongji.txt）；
  - bianyi：变异 calling 脚本（pbrun/GATK 流程，08-08 版本待改用本地输出）。
- 10:52 生成参考 .dict（Brassica_napus_NY7.dict，GATK 需要）；16:20 000_gene/download 整理。
- 11:04 提交 WGS 比对 Job 75101185（bidui.sh，-n 10，normal 队列，串行 for 循环 5 样本）。
主要结果：
- WGBS 5 样本 × 4 上下文共 20 个链特异 .bw 全部完成（WGBS/ 下 *BS.mr_bt2_strand.{cg,chg,chh,c}.bw）。
- WGS 比对逐样本产出 sam：WGS-107 13:11、WGS-108 16:14、WGS-109 18:20、WGS-110 20:44、WGS-111 23:09（每个约 2.5 h）。
状态：WGBS bw 全部完成；WGS 比对 Job 75101185 夜间跑完 5 个 sam。
异常：无。
注意：bwa mem -t 4（脚本体 10 核申请但比对仅用 4 线程）；比对串行较慢，5 样本约 12 h。
