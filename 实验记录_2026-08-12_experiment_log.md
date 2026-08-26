2026.08.12 xiPU WGS 后处理（sort/拆分/markdup/MAPQ30）+ 变异 calling 全流程完成
项目：xiPU
运行目录：/public/home/cpliu25/analy/xiPU/WGS/
代码版本：analy 下无 git；本次脚本为 WGS/ame（Job 75104603）、ame2（Job 75105492）、bianyi（Job 75105513）
输入：WGS-107~111.sam（08-11 bwa mem 产出）；参考 000_gene/Brassica_napus_NY7.fasta + .dict + .len
今日操作：
- ame 后处理（10:25–13:12，逐样本）：
  - samtools view -b 转 bam -> sort + index；
  - 按染色体拆分：剔除 ChrM/ChrC 得 gene.sort.bam，另存 mitochondria/chloroplast.sort.bam；
  - markdup（去重，出 *_metrics）-> MAPQ30 过滤 -> index。
  - 产出节奏：WGS-107 10:25–10:53、WGS-108 10:59–11:29、WGS-109 11:34–12:01、WGS-110 12:05–12:35、WGS-111 12:40–13:12。
- 14:53 ame2（Job 75105492）汇总 flagstat 到 tongji.txt。
- 变异 calling（Job 75105513，Parabricks htvc GPU）：
  - 逐样本 gVCF（htvc，-nt 5 -g）：WGS-107 14:57、WGS-108 15:08、WGS-109 15:11、WGS-110 15:18、WGS-111 15:24；
  - GATK CombineGVCFs（gvcf.list 5 样本）16:02 -> combined.gvcf.gz；
  - GenotypeGVCFs 16:34 -> combined.gt.vcf.gz；
  - SelectVariants 分 SNP（16:34）/INDEL（16:35）-> VariantFiltration（16:37–16:38，阈值同 08-08 脚本：SNP QD<2/FS>60/MQ<30/MQRankSum<-12.5/ReadPosRankSum<-8；INDEL QD<2/FS>200/ReadPosRankSum<-20）-> 保留 pass。
主要结果：
- 5 样本 gene_dup_removed.MAPQ30.bam 全部完成，比对率 99.48%–99.77%（flagstat，tongji.txt）：
  - WGS-107：总 reads 45,930,591，mapped 99.68%，properly paired 97.38%；
  - WGS-108：47,328,523，mapped 99.48%，properly paired 94.98%；
  - WGS-109：42,108,614，mapped 99.77%，properly paired 97.54%；
  - WGS-110：45,917,732，mapped 99.65%，properly paired 96.31%；
  - WGS-111：50,888,555，mapped 99.72%，properly paired 97.47%。
- 变异结果：原始 SNP 7,239,688 个，过滤后 pass 7,182,094（保留 99.2%）；INDEL pass 1,552,910。
状态：WGS 比对、后处理、变异 calling 全流程完成。
异常：无；WGS-108 properly paired 94.98% 略低于其余样本（>96%），secondary reads 也偏多（1,048,254），如后续分析用到可关注。
注意：最终文件 hebing.gatk.all.{SNP,INDEL}.pass.filter.vcf.gz 在 WGS/ 下；叶绿体/线粒体拆分 bam 已单独保留可做细胞器基因组分析。
