2026.08.08 xiPU ATAC/ChIP 重复合并 + bigwig/macs2 + WGBS 链特异 bedGraph + WGS 变异 calling 提交
项目：xiPU
运行目录：/public/home/cpliu25/analy/xiPU/
代码版本：analy 下无 git；本次脚本为 002_result/hebing/{bw,bw2}、WGBS/bw、WGS/bianyi（LSF normal 队列）
输入：002_result 下各样本 gene_dup_removed.MAPQ30.bam；WGBS/*.methratio.txt；WGS/*.gene_dup_removed.MAPQ30.bam；参考 000_gene/Brassica_napus_NY7.fasta（+ .len）
今日操作：
- 002_result/hebing（ATAC/ChIP 重复样本合并 + bw + macs2）：
  - 合并 merge--Job 75090109（samtools merge -@ 16，-n 18，normal，c07n04），16:36 提交、16:43–17:21 Done（约 38 min，.err 空）-> 20 个合并 bam + .bai（5 品种 SL/CDA/CY2/NY1/NY7 × ATAC + K273/K41/K43/K92，各含两个重复；SL 16:45 起、NY7 17:21 止）。
  - bigwig/peak bw--第一次 Job 75090305（bw 脚本，bamCoverage --normalizeUsing CPM -e --binSize 10），17:32 提交、1 s 退出码 127（bamCoverage: command not found，同 08-07 PATH/conda 缺工具）。
  - 改写 bw2 脚本（17:47）重提：bamCoverage(CPM) + macs2 callpeak（-f BAMPE -B -q 1e-5；K43/K41/K273 narrow，K92 --broad --broad-cutoff 0.01；ATAC 无 control，ChIP 用 CHIP/input/result 各品种 2 个 input 做 control；-g SL/CY2/NY1/NY7 603088334、CDA 332248259；输出 bw_macs2/）。Job 75090328（17:37，10 核 c02n08）、75090354（17:47，10 核 c06n04）RUN 中。
- WGBS（甲基化 bigwig/bedGraph）：WGBS/bw 脚本（BatMeth2 batmeth2_to_bigwig.py -sort -strand，参考 .fasta.len）--Job 75090013（BW，-n 18，normal，c07n11），15:59 提交、RUN 中（约 2.4 h）。处理 5 样本 methratio.txt；CY2BS 已出 mr_bt2_strand.{cg/chg/chh/c}.bedGraph（16:56–17:42），.bw 待生成；WGBS/TXT 空文件占位（15:44）。
- WGS（变异 calling）：WGS/bianyi（callbianyi.sh，08-06 待补正文，今日 16:56 补好提交）--Parabricks pbrun haplotypecaller（GPU，singularity clara-parabricks/4.0.1-1.sif）逐样本 gVCF -> GATK CombineGVCFs -> GenotypeGVCFs -> SelectVariants 分 SNP/INDEL -> VariantFiltration（SNP QD<2/FS>60/MQ<30/MQRankSum<-12.5/ReadPosRankSum<-8；INDEL QD<2/FS>200/ReadPosRankSum<-20）-> 保留 pass。Job 75090123（16:56，-n 10 + GPU，normal）PEND，已排队约 1.5 h 未起。
主要结果：
- hebing 20 个合并 bam 完成（5 品种 × 4 组合，各含两重复）。
- macs2 已完成 SL 5 个 peaks（bw_macs2/，17:55–18:21）：K43 43,193、K41 62,601、K273 42,250、ATAC 53,849（narrowPeak），K92 27,243（broadPeak）。
- .bw 已生成 3 个（CDA_ATAC 17:49、CDA_K273 18:08、CDA_K41 18:24，进行中）--bw2 环境已修复（75090305 的 command not found 已解决）。
- WGBS CY2BS 链特异 bedGraph 已生成（CG 0.98 GB、CHG 1.01 GB、CHH 4.99 GB、全C 6.98 GB）。
状态：bam 合并完成；bw + macs2 进行中（75090328/75090354 RUN，SL peaks 完成、CDA .bw 生成中）；WGBS BW 75090013 RUN（CY2BS bedGraph 完成，余 4 样本待处理）；WGS 变异 calling 75090123 PEND（排队未起）。
异常：bw Job 75090305 退出码 127（bamCoverage: command not found，同 08-07）；改 bw2 重提后 .bw 正常生成，环境问题已解。
注意：bw2 脚本 for 循环内含完整 macs2，两个 bw.sh 作业（75090328/75090354）并行执行同一全量 for *bam，macs2 部分会重复触发同名输出（bw_macs2 内文件被覆盖），需留意并发重复；08-07 的 bw command not found 今日以 bw2 修复，08-06 的 WGS bianyi 待补正文今日已补并提交。
