2026.07.27 xiPU 多组学处理（ATAC / CHIP / WGBS）
项目：xiPU
Run ID：<!-- 待填 -->
目的：<!-- 待用户提供；纸质本同步记录 -->
运行目录：/public/home/cpliu25/analy/xiPU/
代码版本：<!-- 待填：/public/home/cpliu25/analy git commit -->
输入：ATAC（BXAS-169、BXAS-170）、CHIP（k41/BSCS-222、k43/BSCS-220、k273/BSCS-224、input/BSCS-283、k92/BXCS-25）、WGBS（SLBS）比对后 sam/bam。
今日操作：
- WGBS：SLBS 用 batMeth2 跑甲基化分析，产出 SLBS_loci/Region.CG/CHG/CHH、methratio、AverMethylevel、batmeth2.html 等。Job ID 74807491。01:11–01:20 完成。
- ATAC：跑 ame 流程（samtools sort+index → 拆分 gene/ChrM/ChrC → Picard MarkDuplicates 去重 → MAPQ30+properly-paired 过滤）。
  · BXAS-169 全流程完成（16:07 bam → 16:46 MAPQ30）。flagstat 110,366,047 reads，99.82% mapped；ChrM 3,695,601，ChrC 37,974,906。
  · BXAS-170 bam 16:57 生成（flagstat 133,387,988 reads，99.83% mapped），samtools sort 进行中（tmp 文件至 17:09）。Job ID 74827722。
- CHIP：同 ame 拆分/去重流程，k41、k43、k273、input 四样本 bam→sort→gene/mito/chloro→去重，16:45–17:09 陆续产出；k92/raw_weihebing/try/BXCS-25.merge.sam（7.7 GB）合并进行中。
状态：WGBS 完成；ATAC BXAS-169 完成、BXAS-170 排序中；CHIP 主流程基本完成、k92 BXCS-25 合并进行中。
异常：WGBS 目录出现 core.200475，需确认是否有子进程崩溃。
注意：目的、Run ID、代码版本待补；BXAS-170 与 BXCS-25 完成后补结果。
