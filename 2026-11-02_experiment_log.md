# 实验日志 2026-11-02

## 基本信息

| 字段 | 内容 |
|---|---|
| 日期 | 2026-11-02（周一） |
| 项目 | Ding ChIP 原始计数、30 样本 RRPM bigWig、K92/H3K9me2 TE 边界切分与计数 |
| 今日目的 | 对 Ding 的 40 个最终 Brassica BAM 完成 MACS2、peak 合并和 multicov；生成 30 条 RRPM bigWig；按 TE 边界切分 K92 peak 并重新计数 |
| 运行目录 | ROOT=`/share/home/cpliu25/001.work`；GPT=`/share/home/cpliu25/GPT`；BEDROOT=`/share/home/cpliu25/004.bed`；REF=`/share/home/cpliu25/003.gene` |
| 运行概况 | 截至 21:15：Ding 原始计数、30 条 RRPM BW 和 K92-TE 切分计数成功；初始 featureCounts 与 K92 首轮计数曾失败；Ding 的 10 样本合并矩阵未发现最终产物 |

## 今日操作

### Ding ChIP 原始计数

1. **12:03–12:04** 核对 40 个最终 Brassica BAM，确认均为 coordinate-sorted 且存在 `.bai`；按材料采用有效基因组大小 AzAz 330,645,022 bp、C2C2 512,482,597 bp、A+C 组 829,253,921 bp。
2. **12:04** 提交作业 `40787556`。30 个 ChIP 重复分别 callpeak，`-c` 使用同组两个 Input 合并背景；K43 取 narrow，K273/K92 取 broad。
3. **12:59** 30 个 callpeak 全部完成；每种修饰汇总 10 个样本 peak，并用 `bedtools merge -i - -c 4 -o distinct,count_distinct` 生成 5 列 BED。
4. **12:59–13:10** 对 5 个材料组分别使用两个 ChIP BAM 做 `bedtools multicov`，生成 15 份 7 列、无表头 `.bed.mapstats`。
5. **13:13** 作业 `40787556` 成功结束；合并区间共 155,559 个，行数、列数、坐标一致性和非负整数检查均通过。

### RRPM bigWig

1. **16:27–16:37** 核对系数表：H3K4me3、H3K27me3、H3K9me2 各 10 个样本，编号完整；确认使用 A+C 合并的 `*.Brassica.exclA.bam`。
2. **16:38** 复用 Ding 的同批 callpeak，提交作业 `40788140`；使用 `bamCoverage -p 28 --binSize 10 --normalizeUsing None --scaleFactor`。
3. **16:48** 30 条 bigWig 全部生成并通过数量与内容检查；未使用 `--extendReads`，未纳入 RNA。

### K92 / H3K9me2 TE 切分

1. **20:57** 从 `REF/ZS11_last/ZS11RS3.mod.EDTA.TEanno.gff3` 提取 9,905 个 `repeat_region`，按 `BEDROOT/split.sh` 和最长 5,000 bp 规则处理 K92 统一 peak。
2. **20:57–21:00** 作业 `40793908` 完成切分：53,314 个原 peak 中，41,657 个短 peak 原样保留，11,657 个长 peak 切成 38,418 段，最终 80,075 段；随后计数因列索引解析错误使作业整体失败。
3. **21:07–21:12** 提交修复作业 `40793952`，只重跑 multicov；10 个 K92 BAM 完成计数并合并为 80,075 行 × 10 样本矩阵，5 份分组 mapstats 均为 80,075 行、7 列。

## 代码版本（逐脚本）

相关目录均未建立可用 Git 版本库；脚本为未提交状态。

| 脚本文件 | Commit | 改动说明 / 提交日期 |
|---|---|---|
| `GPT/001_Ding_chip/scripts/callpeak.py` | 未提交 | 30 个 ChIP 独立 MACS2；2026-11-02 |
| `GPT/001_Ding_chip/scripts/merge_peaks.py` | 未提交 | 同修饰 10 样本 peak 并集；2026-11-02 |
| `GPT/001_Ding_chip/scripts/multicov.py` | 未提交 | 分组双重复 multicov；2026-11-02 |
| `GPT/001_Ding_chip/scripts/combine_mapstats.py` | 未提交 | 10 样本合并矩阵脚本；2026-11-02，运行结果未发现 |
| `GPT/001_BW/scripts/make_bigwigs.py` | 未提交 | 按样本乘数生成 RRPM BW；2026-11-02 |
| `GPT/001_K92_TE/scripts/prepare_inputs.py` | 未提交 | TE 区域与长 peak 切分输入；2026-11-02 |
| `GPT/001_K92_TE/scripts/quantify.py` | 未提交 | K92-TE 逐 BAM multicov；2026-11-02 |

## 运行编号 / 状态

| 样品/任务 | Job ID / 本地标识 | 提交时间 | 状态 | 完成时间 | 节点 | 验证依据 |
|---|---|---|---|---|---|---|
| Ding 初始 featureCounts | 40787223 | 2026-11-02 10:48 前 | 失败，errCode 1；H3K4me3 子任务失败 -6 | 2026-11-02 10:48 | agent-ARM-23 | `GPT/001_chip_ding/logs/dsub_001_chip_quant_40787223.out` |
| Ding callpeak/merge/multicov | 40787556 | 2026-11-02 12:04 前 | 成功 | 2026-11-02 13:13 | agent-ARM-13 | `GPT/001_Ding_chip/logs/dsub_Ding_chip_40787556.out` |
| 30 条 RRPM bigWig | 40788140 | 2026-11-02 16:38 前 | 成功 | 2026-11-02 16:48 | agent-ARM-05 | `GPT/001_BW/logs/dsub_BW_chip_40788140.out` |
| K92 TE 切分及首轮计数 | 40793908 | 2026-11-02 20:57 前 | 切分成功，计数失败 errCode 1 | 2026-11-02 21:00 | 未记录 | `GPT/001_K92_TE/logs/dsub_K92_TE_40793908.err` |
| K92-TE 计数修复 | 40793952 | 2026-11-02 21:07 前 | 成功 | 2026-11-02 21:12 | agent-ARM-20 | `GPT/001_K92_TE/logs/dsub_K92_TE_quant_40793952.out` |

## 环境信息

- 使用 `analy1` 环境：samtools 1.24、bedtools 2.31.1、MACS2 2.2.9.1、deeptools/bamCoverage 3.5.5、Python 3.11.16；featureCounts 失败路径的版本未记录；dsub 版本未记录。
- Ding 主作业申请 12 CPU、64 GB；BW 作业申请 84 CPU、128 GB；K92-TE 计数申请 12 CPU、48 GB。
- 所有读取均为已排除 A 专属区域的最终 Brassica BAM；原始 BAM 未改写。

## 主要参数 / 改动

| 任务 | 项目 | 内容 |
|---|---|---|
| Ding callpeak | 窄峰 | K43：`-q 1e-5`、narrowPeak |
| Ding callpeak | 宽峰 | K273/K92：`-q 0.01 --broad --broad-cutoff 0.01` |
| Ding callpeak | 共同参数 | `-f BAMPE --keep-dup all`；每样本 `-c` 同组两个 Input |
| Ding 合并 | peak 并集 | `bedtools merge -i - -c 4 -o distinct,count_distinct` |
| Ding 计数 | 方法 | `bedtools multicov`，alignment/read-level，组内两重复分别计数 |
| BW | 输入 | A+C 合并的 `*.Brassica.exclA.bam` |
| BW | 参数 | `bamCoverage -p 28 --binSize 10 --normalizeUsing None --scaleFactor` |
| BW | 系数 | 按样本 ID 使用用户提供的 30 个系数 |
| K92-TE | 切分 | 只处理 >5 kb 长 peak，按 TE `repeat_region` 边界切分；不是删除全部 TE |
| K92-TE | 计数 | 10 个 BAM 分别 multicov 后按 peak ID 合并，不做归一化 |

## 初步结果 / 异常

| 样品/对象 | 指标（单位/分母） | 数值 | 证据 |
|---|---|---:|---|
| Ding BAM | 最终 BAM 审计 | 40/40 通过，bad 0 | `ROOT/Ding/CHIP/metadata/bam_audit.tsv` |
| Ding K43 | 合并区间 | 61,721 | `ROOT/Ding/CHIP/mergebed/K43.merged_peaks.bed` |
| Ding K273 | 合并区间 | 40,524 | `ROOT/Ding/CHIP/mergebed/K273.merged_peaks.bed` |
| Ding K92 | 合并区间 | 53,314 | `ROOT/Ding/CHIP/mergebed/K92.merged_peaks.bed` |
| Ding 三种修饰 | 合并区间合计 | 155,559 | 三份 merge BED 行数 |
| Ding mapstats | 分组计数文件 | 15 份，每组 7 列 | `ROOT/Ding/CHIP/mapstats/` |
| BW | RRPM bigWig | 30/30 通过 | `ROOT/BW/` |
| K92-TE | 切分前 → 后 peak | 53,314 → 80,075（增加 26,761，50.2%） | `ROOT/Ding/CHIP/K92_TE_split/` |
| K92-TE | 切分后片段 | ≤5 kb 短 peak 41,657；长 peak 切出 38,418 | `GPT/001_K92_TE/logs/dsub_K92_TE_40793908.out` |
| K92-TE 矩阵 | 片段 × 样本 | 80,075 × 10 | `ROOT/Ding/CHIP/K92_TE_split/K92.TE_split.raw_counts.tsv` |

- 解释：Ding 的 155,559 个合并区间与三种修饰 mapstats 的坐标和行数一致；K92-TE 增加主要来自 11,657 个长 peak 被切分成 38,418 段。
- 异常 1：初始 Ding 定量使用 featureCounts，H3K4me3 子任务失败；随后按用户要求改用 MACS2 + peak 合并 + multicov，原失败结果未作为最终结果。
- 异常 2：`40793908` 的 TE 切分已完整产出，但计数阶段因输出列数不足解析 `IndexError`，作业整体为失败；修复后由 `40793952` 成功重跑计数。
- 异常 3：16:25 提出合并三种修饰的 10 样本矩阵，但截至补记时未发现对应最终矩阵文件；现有交付为 15 份分组 mapstats 和 K92-TE 的 10 样本矩阵。
- 异常 4：此前会话中的 `ROOT/K92_TE_split` 路径已不代表当前产物；当前实际路径为 `ROOT/Ding/CHIP/K92_TE_split/`。

## 主要输出文件

- `ROOT/Ding/CHIP/mergebed/{K43,K273,K92}.merged_peaks.bed`：三种修饰的统一合并 peak，已验证。
- `ROOT/Ding/CHIP/mapstats/`：15 份分组原始 multicov 表，已验证。
- `ROOT/Ding/CHIP/metadata/column_order.tsv`：mapstats 第 6、7 列样本对应表。
- `ROOT/BW/`：30 条 A+C RRPM bigWig，已验证。
- `ROOT/BW/metadata/scale_factors.tsv`：样本与系数对应表。
- `ROOT/Ding/CHIP/K92_TE_split/K92.TE_split.broadPeak`：TE 边界切分后的 80,075 个 peak 片段。
- `ROOT/Ding/CHIP/K92_TE_split/K92.TE_split.bed5`：5 列 multicov 输入。
- `ROOT/Ding/CHIP/K92_TE_split/K92.TE_split.raw_counts.tsv`：80,075 × 10 原始计数矩阵。

## 下一步计划

1. 运行 `GPT/001_Ding_chip/scripts/combine_mapstats.py` 或等价流程，生成 K43/K273/K92 各自的 10 样本合并计数矩阵，并核对列顺序。
2. 明确 K43、K273 是否也需要按 K92 的 TE 边界规则切分和重新计数。
3. 进入归一化或差异分析前固定原始 count、样本乘数和分组表版本。

---

生成/补记：2026-11-03 21:07；状态截至：2026-11-02 21:15。
来源：作业 `40787223/40787556/40788140/40793908/40793952` 日志、`ROOT/Ding/`、`ROOT/BW/`、`GPT/001_Ding_chip/`、`GPT/001_BW/`、`GPT/001_K92_TE/`、Codex 会话记录。
