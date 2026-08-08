2026.08.05 xiPU WGBS 基因区处理 + WGS/ChIP 统计
项目：xiPU
运行目录：/public/home/cpliu25/analy/xiPU/
今日操作：
- WGBS（35 文件）：5 样本（CDA/CY2/NY1/NY7/SL）基因区处理--gene.sort.bam -> gene_dup_removed.bam -> MAPQ20.bam -> bamstat + metrics；mapped.stat；提交 BSrun2/BSrun3。Job ame74989319（13:12）、ame74992575（19:33，.err 467 KB）。
- WGS（7 文件）：tongji.txt 比对统计（WGS-107~111）。Job ame74987087（10:13 Exited 130）、ame74987319（10:25 Done）。
- ChIP（4 文件）：input 子目录 tongji.txt（BSCS-283/284 对照）。Job ame74986734（10:00 Done）。
主要结果：
- WGBS MAPQ20 mapped reads：CDABS 56,891,727；CY2BS 93,577,675；NY1BS 69,067,089；NY7BS 85,842,484；SLBS 67,867,639。
- ChIP input：BSCS-283 mapped 99.41%、BSCS-284 98.93%。
状态：WGBS 基因区处理完成、BSrun2/3 已提交；WGS/ChIP 统计完成。
异常：WGS ame74987087 退出码 130（中断）；WGBS ame74992575 .err 较大，需确认。
