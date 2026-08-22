# PAKD：面向无人机声学检测的偏好对齐知识蒸馏

本仓库是 PAKD（Preference-Aligned Knowledge Distillation）无人机声学检测研究的配套公开仓库，用于提供与当前论文稿件相对应的模型权重、实验结果记录及文件完整性信息。当前送审材料已通过 `v1.0-review-materials` 标签固化，便于审稿人与读者按照论文 Table I–XI 核查主要实验。

## 当前公开内容

- 53 个与论文实验对应的模型检查点，统一存放于 `checkpoints/`，并通过 Git LFS 管理；
- 11 个与论文 Table I–XI 一一对应的结果记录，统一存放于 `results/`；
- 检查点—实验—论文表格映射、结果文件映射和 SHA-256 完整性校验信息；
- 覆盖二分类教师模型、轻量学生模型、同域测试、DADS 跨数据集测试、知识蒸馏方法比较、PAKD 组件消融、重复实验、三分类扩展和边缘部署实验。

## 仓库目录

- `checkpoints/`：论文所报告实验对应的模型检查点；
- `results/`：Table I–XI 的数值结果记录；
- `docs/checkpoint_inventory.csv`：检查点编号、文件名、大小和 SHA-256 清单；
- `docs/checkpoint_experiment_mapping.txt`：每个检查点对应的论文表格与实验说明；
- `docs/result_mapping.csv`：论文表格与 `results/` 中结果文件的对应关系；
- `MANIFEST.csv`：仓库文件清单及其完整性信息；
- `SHA256SUMS.txt`：用于独立校验文件内容的 SHA-256 摘要。

## 论文实验与模型检查点

检查点使用 `C001`–`C053` 的中性编号。完整文件名和 SHA-256 值见 `docs/checkpoint_experiment_mapping.txt` 与 `docs/checkpoint_inventory.csv`。

| 论文位置 | 实验内容 | 对应检查点 | 结果文件 |
| --- | --- | --- | --- |
| Table I | MFCC、LFCC 与 Mel 表示的定量分析，以及所选 MFCC-primary TripleFusion 二分类教师 | `C052` | `results/TableI_feature_representation.txt` |
| Table II | 轻量 Mel 学生的注意力结构比较：无注意力、SE 和 MTFA | `C001`–`C003` | `results/TableII_mtfa_ablation.txt` |
| Table III | 教师分支消融：MFCC 单分支、MFCC+LFCC、MFCC+Mel 与完整 TripleFusion 教师 | `C004`–`C006`, `C052` | `results/TableIII_teacher_branch_ablation.txt` |
| Table IV | 自采测试集上的参考模型比较：AST、CAM++、ConvNeXt-Tiny、DASS、MobileNetV4、ResNet-50 和 ViT-MediumD | `C007`–`C013` | `results/TableIV_in_domain_reference_comparison.txt` |
| Table V | 自采测试集上的学生任务学习与 PAKD 蒸馏结果；覆盖 LFCC、Mel、MFCC 学生及不同主教师组合 | `C020`–`C031` | `results/TableV_in_domain_distillation.txt` |
| Table VI | 完整 DADS 外部数据上的教师—学生组合矩阵与分类别跨数据集结果 | `C020`–`C031` | `results/TableVI_teacher_student_matrix_dads.txt` |
| Table VII | DADS 上的蒸馏策略比较：任务损失、AT、Hinton KD、NormKD、TRKD-inspired、DKD、RKD 与 PAKD | `C024`, `C027`, `C032`–`C037` | `results/TableVII_kd_strategy_comparison_dads.txt` |
| Table VIII | PAKD 组件消融：CE/KL、成对偏好、置信度、分支一致性和特征蒸馏 | `C027`, `C034`, `C038`–`C041` | `results/TableVIII_pakd_component_ablation.txt` |
| Table IX | AT、任务损失学生与 PAKD 学生的多次跨数据集实验 | `C014`–`C019`, `C024`, `C027`, `C032` | `results/TableIX_repeated_experiments.txt` |
| Table X | 三分类扩展：任务损失、AT、Hinton KD、NormKD、TRKD-inspired、DKD、RKD、PAKD 及三分类 TripleFusion 教师 | `C042`–`C049`, `C053` | `results/TableX_three_class_results.txt` |
| Table XI | 所选轻量 Mel-PAKD 学生的边缘设备部署记录 | `C027` | `results/TableXI_edge_deployment_records.txt` |

除表格实验外，`C050`–`C052` 分别对应 LFCC-primary、Mel-primary 和所选 MFCC-primary TripleFusion 二分类教师，用于论文正文中的教师模型比较及 DADS 外部评价。部分模型在训练完成后被用于多个分析，因此同一检查点可同时对应多张论文表格；这种复用关系已在映射文件中明确记录。

## 主要实验材料说明

### 1. 教师模型与声学表示

教师相关检查点覆盖 MFCC、LFCC 和 Mel 分支，以及单分支、双分支和完整 TripleFusion 结构。Table I 与 Table III 用于说明声学表示选择和教师分支融合的作用；正文中的外部评价进一步记录不同主分支教师在 DADS 上的表现。

### 2. 轻量学生与 MTFA

Table II 对应的三个检查点用于比较无注意力、SE 和 MTFA。所选学生采用 Mel 输入与 MTFA 结构，并作为后续 PAKD 蒸馏和边缘部署的学生网络。

### 3. 同域与跨数据集蒸馏

Tables V 和 VI 共同覆盖 LFCC、Mel、MFCC 三类学生及 LFCC-primary、Mel-primary、MFCC-primary 教师组合。Table V 记录自采测试集结果，Table VI 记录不参与训练的 DADS 外部数据结果，从而呈现同域性能与跨数据集泛化能力。

### 4. 知识蒸馏对比与 PAKD 消融

Table VII 收录任务损失学生、经典蒸馏方法、近期代表性蒸馏方法和 PAKD 的对比检查点。Table VIII 进一步对应 PAKD 的成对偏好、置信度加权、分支一致性和特征蒸馏等组成部分，用于核查完整方法及各消融变体。

### 5. 重复实验、三分类与部署

Table IX 汇总 AT、任务损失学生和 PAKD 学生的多次实验。Table X 将教师—学生蒸馏扩展到三分类任务，并提供所列各方法和三分类教师的检查点。Table XI 对应最终选定的轻量 Mel-PAKD 学生，并记录其边缘部署结果。

## 下载与完整性校验

模型权重由 Git LFS 管理。克隆仓库后可执行：

```bash
git lfs install
git lfs pull
```

下载完成后，可根据 `SHA256SUMS.txt` 或 `docs/checkpoint_inventory.csv` 核验文件完整性。例如在 PowerShell 中：

```powershell
Get-FileHash .\checkpoints\checkpoint_001.pth -Algorithm SHA256
```

## 后续公开计划与长期维护承诺

本仓库将作为论文的长期公开存档持续维护。作者承诺永久保留本仓库及已发布版本，不会在论文发表后删除仓库、撤下送审材料或覆盖已经发布的版本；后续更新将通过新的提交、版本标签和 Release 追加，`v1.0-review-materials` 将继续保留。

- 论文正式发表后三日内，上传与最终论文对应的数据预处理、教师与学生模型、PAKD 训练、评价、三分类扩展及部署相关代码；
- 论文正式发表后一周内，上传自采二分类和三分类数据集，并在本仓库提供稳定的下载链接与数据说明；
- 代码、数据和文档更新完成后，将发布新的版本标签，同时保留当前送审版本以便追溯。

本仓库中的模型、结果记录和完整性清单共同构成当前论文实验的公开核查材料。论文正式发表后，仓库将进一步扩展为包含代码、数据访问和使用说明的完整项目页面。
