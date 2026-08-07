2026.08.07 xiPU WGBS 细胞器甲基化计数汇总与参考 index 重建
项目：xiPU
Run ID：<!-- 待填 -->
目的：<!-- 待用户提供：汇总 WGBS 各样本线粒体/叶绿体 mC 计数、复核参考 index -->
运行目录：/public/home/cpliu25/analy/xiPU/
代码版本：<!-- 待填：analy 下无 git 仓库，请提供脚本版本/commit -->
输入：WGBS 5 样本（CDABS、CY2BS、NY1BS、NY7BS、SLBS）methratio.txt；参考 Brassica_napus_NY7.fasta。
今日操作：
- 08-07 截至生成时（约 10:30）analy 树无新文件产出、无新作业提交；今日主要为汇总 08-06 结果。
- （08-06 承接）WGBS：跑 BSrun3.txt——Job 75022505（11:42–11:44）与 Job 75022607（11:47–11:50），均 18 核 c05n07、normal 队列，Successfully completed；从各样本 methratio.txt 提取 ChrM/ChrC 的 mC（第5列）与 all_C（第6列）计数，追加写入 {样本}.mapped.stat。
- （08-06）000_gene：重建参考 index——Brassica_napus_NY7.fasta.fai（9169 行；ChrC 152,860 / ChrM 221,853 / chrA01 31,225,393）与 Brassica_napus_NY7.fasta.batmeth2.fa.fai（18338 行，按正负链拆 f/r，如 fChrC/rChrC/fChrM）。
- （08-06）WGS：新建变异 calling 作业脚本 WGS/bianyi（callbianyi.sh，-n 10，normal 队列），目前仅 BSUB 头部、正文待补。
主要结果：
- WGBS 细胞器 mC 计数（mC / all_C）：CDABS 线粒体 12,933 / 1,067,849、叶绿体 9,627 / 1,609,199；SLBS 线粒体 7,242 / 1,225,396、叶绿体 3,330 / 1,597,820（CY2/NY1/NY7 见各自 mapped.stat）。
- CDABS.sort.bam flagstat：134,602,649 reads，99.95% mapped；CDABS.gene_dup_removed.MAPQ20.bam 57,309,904 reads，100.00% mapped。
状态：WGBS 5 样本细胞器甲基化计数已入 mapped.stat；000_gene 参考 index（含 batmeth2 链特异 fai）已重建；WGS bianyi 脚本待补正文。
注意：目的、Run ID、代码版本待补；08-07 若有新作业请告知补记。
