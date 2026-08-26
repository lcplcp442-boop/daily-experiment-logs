2026.08.10 xiPU 合并样本 bw/macs2 收尾 + RNA 重复合并
项目：xiPU
运行目录：/public/home/cpliu25/analy/xiPU/
代码版本：analy 下无 git；本次脚本为 002_result/project/bw2hebing、002_result/hebing
输入：002_result/hebing/bam 下 20 个合并 bam（08-08 产出）；RNA 各样本 clean fq
今日操作：
- hebing 合并 bam 的 bw + macs2 收尾（08-08 提交的 bw2 Job 75090354 今晨 10:42 Done）：hebing/peak 陆续产出 20 个合并样本 peaks（5 品种 SL/CDA/CY2/NY1/NY7 × ATAC + K273/K41/K43 narrowPeak + K92 broadPeak），时间 11:34（SL_K43）–14:38（NY7_ATAC）。
- 11:21 编写 bw2hebing 脚本（bamCoverage CPM + macs2，input 对照同 bw2），14:38 提交 Job 75096781 重跑/补跑 hebing 的 bw + macs2。
- 15:41–15:45 RNA 重复样本合并（samtools merge）：CDA_RNA_BnRS-72_73、CY2_RNA_BnRS-5_6、NY1_RNA_BnRS-19_20、NY7_RNA_BnRS-9_10、SL_RNA_BnRS-21_22，各出 merged bam + .bai 于 002_result/hebing/bam。
主要结果：
- hebing/peak 20 个合并样本 peaks 全部完成（ATAC/K273/K41/K43 narrowPeak、K92 broadPeak）。
- 5 个品种 RNA 合并 bam + bai 完成。
状态：ATAC/ChIP 合并分析完成；RNA 合并完成，下游定量待做。
异常：无（08-08 提到的 bw2 双作业并发重复跑 macs2 问题今日随作业结束自然终止，peaks 输出完整）。
注意：RNA 合并 bam 尚未做定量（featureCounts/STAR 等），后续补。
