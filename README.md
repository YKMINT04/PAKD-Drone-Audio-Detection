# CWPKD: Consensus-Weighted Preference Knowledge Distillation for Drone Acoustic Detection

**English** | [简体中文](README_zh-CN.md)

This repository accompanies our study on Consensus-Weighted Preference Knowledge Distillation (CWPKD) for drone acoustic detection. It provides model checkpoints and experimental result records. Version `v1.0-review-materials` includes the array revision for manuscript v10.25 described below.

## Currently available materials

- 53 model checkpoints corresponding to experiments reported in the manuscript, stored in `checkpoints/` and managed with Git LFS;
- the supervised array-device classification head, stored as `checkpoints/array_v9_1s_device_head.json`;
- 12 result records corresponding one-to-one with Tables 1–12, stored in `results/`;
- a checkpoint-to-experiment-to-table mapping;
- per-clip held-group array results and replay verification in `results/array_v9_1s/`;
- coverage of binary teacher models, lightweight student models, in-domain evaluation, cross-dataset evaluation on DADS, comparisons of knowledge-distillation methods, CWPKD component ablations, repeated experiments, the three-class extension, eight-microphone-array field experiments, and edge deployment.

## Repository structure

- `checkpoints/`: model checkpoints corresponding to the experiments reported in the manuscript;
- `results/`: numerical result records for Tables 1–12;
- `docs/checkpoint_experiment_mapping.txt`: mapping from each checkpoint to its experiment and manuscript table.

## Manuscript experiments and model checkpoints

The checkpoints use neutral identifiers `C001`–`C053`. Their complete filenames and experiment associations are listed in `docs/checkpoint_experiment_mapping.txt`.

| Manuscript location | Experiment | Checkpoint(s) | Result file |
| --- | --- | --- | --- |
| Table 1 | Feature-space separation and compactness of the MFCC-only model and MFCC-primary PriXFuse teacher | `C004`, `C052` | `results/Table1_feature_representation.txt` |
| Table 2 | Attention-structure comparison for the lightweight Mel student: no attention, SE, and TriTGate | `C001`–`C003` | `results/Table2_mtfa_ablation.txt` |
| Table 3 | Teacher-branch ablation: MFCC only, MFCC+LFCC, MFCC+Mel, and the complete PriXFuse teacher | `C004`–`C006`, `C052` | `results/Table3_teacher_branch_ablation.txt` |
| Table 4 | Reference-model comparison on the self-collected test set: AST, CAM++, ConvNeXt-Tiny, DASS, MobileNetV4, ResNet-50, ViT-MediumD, and the selected PriXFuse teacher | `C007`–`C013`, `C052` | `results/Table4_in_domain_reference_comparison.txt` |
| Table 5 | Student task learning and CWPKD distillation on the self-collected test set, covering LFCC, Mel, and MFCC students with different primary-teacher configurations | `C020`–`C031` | `results/Table5_in_domain_distillation.txt` |
| Table 6 | Teacher–student matrix and class-wise cross-dataset results on external DADS | `C020`–`C031` | `results/Table6_teacher_student_matrix_dads.txt` |
| Table 7 | Comparison of distillation strategies on DADS: task loss, AT, Hinton KD, NormKD, TRKD-inspired, DKD, RKD, and CWPKD | `C024`, `C027`, `C032`–`C037` | `results/Table7_kd_strategy_comparison_dads.txt` |
| Table 8 | CWPKD component ablation: CE/KL, pairwise preference, confidence, branch consistency, and feature distillation | `C027`, `C034`, `C038`–`C041` | `results/Table8_pakd_component_ablation.txt` |
| Table 9 | Repeated cross-dataset experiments for AT, the task-loss student, and the CWPKD student | `C014`–`C019`, `C024`, `C027`, `C032` | `results/Table9_repeated_experiments.txt` |
| Table 10 | Three-class extension: task loss, AT, Hinton KD, NormKD, TRKD-inspired, DKD, RKD, CWPKD, and the three-class PriXFuse teacher | `C042`–`C049`, `C053` | `results/Table10_three_class_results.txt` |
| Table 11 | 1-s independent-clip grouped development evaluation at 5–120 m and two background scenes; frozen CWPKD student plus supervised linear device head | C027 + array_v9_1s_device_head.json | results/Table11_array_assisted_field_recognition.txt |
| Table 12 | Edge-device deployment records for the selected lightweight Mel-CWPKD student | `C027` | `results/Table12_edge_deployment_records.txt` |

In addition to the tabulated experiments, `C050`–`C052` correspond respectively to the LFCC-primary, Mel-primary, and selected MFCC-primary PriXFuse binary teachers used in the teacher-model comparison and external DADS evaluation described in the manuscript. A trained model may support more than one analysis; these reuse relationships are explicitly recorded in the mapping file.

## Overview of the experimental materials

### 1. Teacher models and acoustic representations

The teacher checkpoints cover MFCC, LFCC, and Mel branches, as well as single-branch, two-branch, and complete PriXFuse structures. Tables 1 and 3 examine acoustic-representation selection and teacher-branch fusion. The external evaluations reported in the manuscript additionally compare PriXFuse teachers with different primary branches on DADS.

### 2. Lightweight student and TriTGate

The three checkpoints associated with Table 2 compare no attention, SE, and TriTGate. The selected student uses Mel input and the TriTGate architecture and serves as the student network for subsequent CWPKD distillation and edge deployment.

### 3. In-domain and cross-dataset distillation

Tables 5 and 6 jointly cover LFCC, Mel, and MFCC students distilled from LFCC-primary, Mel-primary, and MFCC-primary teachers. Table 5 reports results on the self-collected test set, whereas Table 6 reports results on the external DADS archive, which was not used for training. Together, they present in-domain performance and cross-dataset generalization.

### 4. Knowledge-distillation comparisons and CWPKD ablations

Table 7 contains checkpoints for the task-loss student, classical distillation methods, recent representative distillation methods, and CWPKD. Table 8 further maps the pairwise-preference, confidence-weighting, branch-consistency, and feature-distillation components of CWPKD, enabling verification of the complete method and its ablation variants.

### 5. Repeated experiments, three-class extension, array extension, and deployment

Table 9 summarizes repeated experiments for AT, the task-loss student, and the CWPKD student; all three CWPKD runs use the MFCC-primary PriXFuse teacher and the Mel student. Table 10 extends teacher–student distillation to the three-class task and provides checkpoints for the listed methods and the three-class teacher. Table 11 reports independent 1-s clips, including 120 m, with a supervised linear device head. Table 12 remains the original student edge benchmark, not validation of the new complete pipeline.

## Downloading model checkpoints

The model checkpoints are managed with Git LFS. After cloning the repository, run:

```bash
git lfs install
git lfs pull
```

## Planned releases and long-term maintenance

This repository will be maintained as the long-term public archive for the paper. The authors commit to retaining the repository and its published history permanently, including after publication. During pre-submission preparation, the v1.0 review-materials tag is updated to the latest review snapshot; earlier snapshots remain accessible through commit history. After submission, subsequent revisions will use separate version tags.

- Within three days after formal publication, we will upload the data-preprocessing, teacher- and student-model, CWPKD-training, evaluation, three-class-extension, eight-microphone-array processing, and deployment code corresponding to the final paper.
- Within one week after formal publication, we will release the self-collected binary and three-class datasets and the 5–120 m eight-microphone-array field recordings, together with stable download links and data documentation in this repository.
- After the code, data, and documentation have been added, a new version tag will be issued while the current review-materials version remains available.

The checkpoints, result records, and experiment mapping in this repository constitute the public verification materials for the current manuscript. After formal publication, the repository will be expanded into a complete project page containing the code, data-access information, and usage documentation.

## Array revision for manuscript v10.25

Raw eight-channel audio is segmented first. Each clip of up to 1 s is independently beamformed and classified, without cross-clip audio, temporal voting, or state carry-over. Frozen student C027 is unchanged; a supervised linear device head combines student features with clip-local acoustic descriptors.

Table 11 reports 1661/1678 correct clips (98.99% overall), including 1271/1278 drone clips (99.45%). Performance at 120 m is 84/90 (93.33%); indoor and outdoor background results are 100/100 and 290/300. Drone recordings are held out in full; background evaluation holds out 50-s blocks with a 10-s training exclusion guard. These are grouped development results. The released all-data deployment head supports inference; the table is calculated with separate held-group heads.

`results/array_v9_1s/` contains the per-clip grouped results, the additional whole-recording background holdout, and the original 99-clip replay verification. These records are kept separate from the previous 2-s archive.

Laptop replay of 99 clips took 0.379 s on average, with 0.398 s p95 and 0.441 s maximum, for the complete computation excluding file I/O and initial loading. The original student edge benchmark and >300-hour operation remain a separate experiment (Table 12).

Historical PAKD/TripleFusion/MTFA identifiers in filenames correspond to current CWPKD/PriXFuse/MelTriGate–TriTGate terminology. Previous 2-s and 10-s records and the old RBF head remain historical evidence, not the current Table 11. This initial release still contains checkpoints, heads, and result records; implementation and data retain the release schedule above.
