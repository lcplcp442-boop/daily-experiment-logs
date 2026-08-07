2026.08.06 xiPU WGBS 细胞器甲基化计数 + 参考 index 重建
项目：xiPU
运行目录：/public/home/cpliu25/analy/xiPU/
今日操作：
- WGBS（10 文件）：跑 BSrun3.txt--Job 75022505（11:42–11:44）、75022607（11:47–11:50），均 18 核 c05n07 normal，Done；从各样本 methratio.txt 提取 ChrM/ChrC 的 mC（第5列）与 all_C（第6列），追加写入 {样本}.mapped.stat。
- 000_gene（2 文件）：重建 Brassica_napus_NY7.fasta.fai（9169 行；ChrC 152,860 / ChrM 221,853 / chrA01 31,225,393）与 .batmeth2.fa.fai（18338 行，正负链拆 f/r）。
- WGS（1 文件）：新建变异 calling 脚本 WGS/bianyi（callbianyi.sh，-n 10，normal），正文待补。
主要结果（细胞器 mC / all_C）：
- CDABS 线粒体 12,933/1,067,849、叶绿体 9,627/1,609,199
- CY2BS 线粒体 7,667/1,309,602、叶绿体 5,520/1,840,679
- NY1BS 线粒体 5,256/1,044,678、叶绿体 3,310/1,697,125
- NY7BS 线粒体 10,044/942,414、叶绿体 10,605/1,566,723
- SLBS 线粒体 7,242/1,225,396、叶绿体 3,330/1,597,820
状态：WGBS 5 样本细胞器甲基化计数入 mapped.stat；参考 index（含 batmeth2 链特异 fai）已重建；WGS bianyi 脚本待补正文。
