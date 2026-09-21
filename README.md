# PAKD: Preference-Aligned Knowledge Distillation for Drone Acoustic Detection

**English** | [简体中文](README_zh-CN.md)

This repository accompanies our study on Preference-Aligned Knowledge Distillation (PAKD) for drone acoustic detection. It provides model checkpoints and experimental result records. Version `v1.0-review-materials` includes the array revision for manuscript v10.21 described below.

## Currently available materials

- 53 model checkpoints corresponding to experiments reported in the manuscript, stored in `checkpoints/` and managed with Git LFS;
- the supervised array-device classification head, stored as `checkpoints/array_v8_device_head.json`;
- 12 result records corresponding one-to-one with Tables 1–12, stored in `results/`;
- a checkpoint-to-experiment-to-table mapping;
- coverage of binary teacher models, lightweight student models, in-domain evaluation, cross-dataset evaluation on DADS, comparisons of knowledge-distillation methods, PAKD component ablations, repeated experiments, the three-class extension, eight-microphone-array field experiments, and edge deployment.

## Repository structure

- `checkpoints/`: model checkpoints corresponding to the experiments reported in the manuscript;
- `results/`: numerical result records for Tables 1–12;
- `docs/checkpoint_experiment_mapping.txt`: mapping from each checkpoint to its experiment and manuscript table.

## Manuscript experiments and model checkpoints

The checkpoints use neutral identifiers `C001`–`C053`. Their complete filenames and experiment associations are listed in `docs/checkpoint_experiment_mapping.txt`.

| Manuscript location | Experiment | Checkpoint(s) | Result file |
| --- | --- | --- | --- |
| Table 1 | Quantitative analysis of MFCC, LFCC, and Mel representations, together with the selected MFCC-primary TripleFusion binary teacher | `C052` | `results/Table1_feature_representation.txt` |
| Table 2 | Attention-structure comparison for the lightweight Mel student: no attention, SE, and MTFA | `C001`–`C003` | `results/Table2_mtfa_ablation.txt` |
| Table 3 | Teacher-branch ablation: MFCC only, MFCC+LFCC, MFCC+Mel, and the complete TripleFusion teacher | `C004`–`C006`, `C052` | `results/Table3_teacher_branch_ablation.txt` |
| Table 4 | Reference-model comparison on the self-collected test set: AST, CAM++, ConvNeXt-Tiny, DASS, MobileNetV4, ResNet-50, ViT-MediumD, and the selected TripleFusion teacher | `C007`–`C013`, `C052` | `results/Table4_in_domain_reference_comparison.txt` |
| Table 5 | Student task learning and PAKD distillation on the self-collected test set, covering LFCC, Mel, and MFCC students with different primary-teacher configurations | `C020`–`C031` | `results/Table5_in_domain_distillation.txt` |
| Table 6 | Teacher–student matrix and class-wise cross-dataset results on the complete external DADS archive | `C020`–`C031` | `results/Table6_teacher_student_matrix_dads.txt` |
| Table 7 | Comparison of distillation strategies on DADS: task loss, AT, Hinton KD, NormKD, TRKD-inspired, DKD, RKD, and PAKD | `C024`, `C027`, `C032`–`C037` | `results/Table7_kd_strategy_comparison_dads.txt` |
| Table 8 | PAKD component ablation: CE/KL, pairwise preference, confidence, branch consistency, and feature distillation | `C027`, `C034`, `C038`–`C041` | `results/Table8_pakd_component_ablation.txt` |
| Table 9 | Repeated cross-dataset experiments for AT, the task-loss student, and the PAKD student | `C014`–`C019`, `C024`, `C027`, `C032` | `results/Table9_repeated_experiments.txt` |
| Table 10 | Three-class extension: task loss, AT, Hinton KD, NormKD, TRKD-inspired, DKD, RKD, PAKD, and the three-class TripleFusion teacher | `C042`–`C049`, `C053` | `results/Table10_three_class_results.txt` |
| Table 11 | 2-s development evaluation of 33 recordings at 5–120 m and two background scenes; frozen CWPKD student plus supervised RBF device head | C027 + array_v8_device_head.json | results/Table11_array_assisted_field_recognition.txt |
| Table 12 | Edge-device deployment records for the selected lightweight Mel-PAKD student | `C027` | `results/Table12_edge_deployment_records.txt` |

In addition to the tabulated experiments, `C050`–`C052` correspond respectively to the LFCC-primary, Mel-primary, and selected MFCC-primary TripleFusion binary teachers used in the teacher-model comparison and external DADS evaluation described in the manuscript. A trained model may support more than one analysis; these reuse relationships are explicitly recorded in the mapping file.

## Overview of the experimental materials

### 1. Teacher models and acoustic representations

The teacher checkpoints cover MFCC, LFCC, and Mel branches, as well as single-branch, two-branch, and complete TripleFusion structures. Tables 1 and 3 examine acoustic-representation selection and teacher-branch fusion. The external evaluations reported in the manuscript additionally compare TripleFusion teachers with different primary branches on DADS.

### 2. Lightweight student and MTFA

The three checkpoints associated with Table 2 compare no attention, SE, and MTFA. The selected student uses Mel input and the MTFA architecture and serves as the student network for subsequent PAKD distillation and edge deployment.

### 3. In-domain and cross-dataset distillation

Tables 5 and 6 jointly cover LFCC, Mel, and MFCC students distilled from LFCC-primary, Mel-primary, and MFCC-primary teachers. Table 5 reports results on the self-collected test set, whereas Table 6 reports results on the external DADS archive, which was not used for training. Together, they present in-domain performance and cross-dataset generalization.

### 4. Knowledge-distillation comparisons and PAKD ablations

Table 7 contains checkpoints for the task-loss student, classical distillation methods, recent representative distillation methods, and PAKD. Table 8 further maps the pairwise-preference, confidence-weighting, branch-consistency, and feature-distillation components of PAKD, enabling verification of the complete method and its ablation variants.

### 5. Repeated experiments, three-class extension, array extension, and deployment

Table 9 summarizes repeated experiments for AT, the task-loss student, and the PAKD student; all three PAKD runs use the MFCC-primary TripleFusion teacher and the Mel student. Table 10 extends teacher–student distillation to the three-class task and provides checkpoints for the listed methods and the three-class teacher. Table 11 now reports 2-s development evaluation of 33 recordings including 120 m with a supervised device head. Table 12 remains the original student edge benchmark, not validation of the new complete pipeline.

## Downloading model checkpoints

The model checkpoints are managed with Git LFS. After cloning the repository, run:

```bash
git lfs install
git lfs pull
```

## Planned releases and long-term maintenance

This repository will be maintained as the long-term public archive for the paper. The authors commit to retaining the repository and its published history permanently, including after publication. During pre-submission preparation, the v1.0 review-materials tag is updated to the latest review snapshot; earlier snapshots remain accessible through commit history. After submission, subsequent revisions will use separate version tags.

- Within three days after formal publication, we will upload the data-preprocessing, teacher- and student-model, PAKD-training, evaluation, three-class-extension, eight-microphone-array processing, and deployment code corresponding to the final paper.
- Within one week after formal publication, we will release the self-collected binary and three-class datasets and the 5–120 m eight-microphone-array field recordings, together with stable download links and data documentation in this repository.
- After the code, data, and documentation have been added, a new version tag will be issued while the current review-materials version remains available.

The checkpoints, result records, and experiment mapping in this repository constitute the public verification materials for the current manuscript. After formal publication, the repository will be expanded into a complete project page containing the code, data-access information, and usage documentation.

## Array revision for manuscript v10.21

PAKD, TripleFusion and MTFA are historical code names; the manuscript now uses CWPKD, PriXFuse and MelTriGate/TriTGate. Only the array evaluation is revised here; other tables were not re-audited in this update. The evaluation covers 33 recordings, including two at 120 m, split into 840 non-overlapping clips of up to 2 s. This review package provides result records and the device head, not the audio or implementation code; their release schedule is given above. Student C027 is unchanged; the added device head is trained with field labels. Every scene reaches at least 90% in grouped development evaluation. Whole-recording background holdout gives 4% indoors and 0% outdoors; these results do not establish unseen-background generalization. Previous 10-s results remain in results/history, with current evidence in results/array_v8_2s. Live end-to-end and 300-hour operation of this new combination have not been validated.
