2026.07.29 xiPU ChIP peak calling + WGBS 比对 + WGS 产 sam
项目：xiPU
运行目录：/public/home/cpliu25/analy/xiPU/
今日操作：
- ChIP（369 文件）：k273/k41/k43/k92 多样本 peak calling（bw、peaks、bed、pdf、qual、Rout、intersectBed）。Job bw74854930（k43 21:56）、bw74855250（k92 23:29）、bw74854925（k41 23:48）Done。
- WGBS（18 文件）：5 样本（CDA/CY2/NY1/NY7/SL）比对+排序+索引、叶绿体/线粒体分离、mapped.stat；NY1/NY7/SL 完成 gene_dup_removed.MAPQ20 bamstat。Job 74855711（BS，18:35）。
- WGS（10 文件）：WGS-107~111 产出 .sam。Job bidui74852640（biduo.sh，11:32 Done）；ame74854914（ameat.sh，17:02 Exited exit code 1）。
- 000_gene：生成 Brassica_napus_NY7.fasta.fai。
状态：ChIP 四标记 peak calling 大量产出；WGBS 5 样本比对完成；WGS 107~111 sam 产出。
异常：WGS ame74854914 退出码 1，需复查。
