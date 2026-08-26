2026.08.18 xiPU 最终结果汇总整理到 002_result（统一命名 + 索引）+ 建立工作日志模板
项目：xiPU
运行目录：/public/home/cpliu25/analy/xiPU/002_result/
代码版本：analy 下无 git；本次为文件整理（cp/mv + samtools index），无新分析
输入：WGBS/*BS.mr_bt2_strand.*.bw、WGBS/ 各 BS bam、WGS/WGS-107~111.gene_dup_removed.MAPQ30.bam
今日操作：
- 20:35–20:41 汇总 BS/WGS bam 到 002_result/bam，统一命名"品种_类型_文库样本"：
  - BS（5 个）：SL_BS_BXBS-3、CDA_BS_BRBS-24_BRBS-25（两重复合并）、CY2_BS_BXBS-14、NY1_BS_BXBS-4、NY7_BS_BXBS-11；统一补 .csi 索引（20:38）；
  - WGS（5 个）：NY1_WGS_WGS-107、CDA_WGS_WGS-108、NY7_WGS_WGS-109、SL_WGS_WGS-110、CY2_WGS_WGS-111；统一 .bai 索引（20:41）。
- 20:38–20:39 WGBS 链特异 bw 汇总到 002_result/bw：5 样本 × {cg,chg,chh,c} 共 20 个 .bw（*BS.mr_bt2_strand.*.bw）。
- 22:24 项目根目录建立工作日志模板 WORKLOG_TEMPLATE.md，供后续 agent/人按统一格式记录日志。
主要结果：
- 002_result/bam：10 个终版 bam + 索引（BS 5 + WGS 5）；
- 002_result/bw：WGBS 甲基化 bw 20 个；
- 至此 002_result 含 bam/、bw/、hebing/（含 peak、bam）、project/、weihebing/ 各子目录，ATAC/ChIP/RNA/WGBS/WGS 主要产出均已归档。
状态：xiPU 各组学主流程产出整理完成。
异常：无。
注意：BS 样本 CDA 为 BRBS-24+BRBS-25 两重复合并后 bam；ATAC/ChIP/RNA 的合并结果在 hebing/（命名 *_*_peaks.* / *_*.bam），与 bam/ 的 BS/WGS 命名规则不同，交接时注意区分。
