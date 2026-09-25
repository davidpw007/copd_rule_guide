# RG-FTCM: Rule-Guided Multimodal Learning for COPD Risk Assessment

This repository contains the research code for **RG-FTCM** (Rule-Guided Face–Tongue–Constitution Multimodal framework), a deep learning framework for COPD risk assessment using routinely collected clinical and questionnaire variables together with traditional Chinese medicine (TCM) tongue, facial, and constitution features.

RG-FTCM incorporates knowledge derived from clinical guidelines and expert-defined directions of risk associations as differentiable logic constraints and rule-derived priors. The framework was designed for a setting in which reference-standard COPD labels are limited and additional participants have multimodal features but no reference-standard label.

> **Research use only.** This repository presents an experimental model and is not a medical device. Its predictions must not replace clinical assessment, post-bronchodilator spirometry, or physician judgment.

## Study objectives

The study had two prespecified objectives:

1. To evaluate whether TCM tongue, facial, and constitution features provide incremental predictive value beyond routinely collected clinical and questionnaire variables.
2. To evaluate whether rule guidance improves model performance when reference-standard labels are limited.

## Repository structure

```text
.
├── tcm_copd_ltn_att_biclass_all_M1M2M3_bootstrap_all_metrics.ipynb
├── tcm_copd_ltn_att_biclass_all_rule.ipynb
├── tcm_copd_multi_model_biclass_fold_external_inline_CI.ipynb
└── README.md
```

- `tcm_copd_ltn_att_biclass_all_M1M2M3_bootstrap_all_metrics.ipynb`  
  Runs the M1/M2/M3 experiments, generates participant-level out-of-fold (OOF) predictions, and performs paired stratified bootstrap comparisons for AUC, accuracy, sensitivity, specificity, and macro-F1.

- `tcm_copd_ltn_att_biclass_all_rule.ipynb`  
  Implements the complete rule-guided multimodal framework and its ablation experiments.

- `tcm_copd_multi_model_biclass_fold_external_inline_CI.ipynb`  
  Loads a saved fold/global-best checkpoint and performs preliminary external evaluation with bootstrap 95% confidence intervals.

Notebook names may be shortened in future releases; their experimental roles will remain unchanged.

## Data

Participant-level data are not included in this repository because they contain sensitive clinical information and potentially identifiable facial images. Access, where permitted, is subject to participant consent, institutional policy, ethics approval, and an appropriate data-use agreement.

### Expected input domains

- routinely collected clinical variables;
- questionnaire variables;
- TCM constitution data;
- tongue features;
- facial features;
- reference-standard label (`isCopd`) for labeled participants.

The current notebooks contain local Windows file paths. Before running them, replace the dataset, image-root, output, and checkpoint paths with paths valid in your environment. Do not commit identifiable participant data or absolute private paths to a public repository.

## Environment

The code was developed in Python with the following principal packages:

- Python 3.9 or later;
- PyTorch and torchvision;
- NumPy and pandas;
- scikit-learn;
- SciPy;
- matplotlib and seaborn;
- SHAP;
- LTNtorch / a compatible `ltn` package;
- Jupyter Notebook or JupyterLab.

Example installation:

```bash
python -m venv .venv

# Linux/macOS
source .venv/bin/activate

# Windows PowerShell
# .venv\Scripts\Activate.ps1

python -m pip install --upgrade pip
pip install torch torchvision numpy pandas scikit-learn scipy matplotlib seaborn shap jupyter ltn
```

Package compatibility can differ across operating systems and CUDA versions. For strict reproduction, export the working environment after confirming the package versions used on your machine.

## Running the experiments

1. Clone the repository and create the Python environment.
2. Place the authorized, de-identified data outside the public repository.
3. Open the relevant notebook and update all data, image, checkpoint, and output paths.
4. Run the M1/M2/M3 notebook from top to bottom to generate five-fold results, pooled OOF predictions, and paired bootstrap comparisons.
5. Run the rule-guided notebook for the complete model and ablation analyses.
6. Run the external-evaluation notebook only after training is complete. The external cohort must not be used for training, early stopping, model selection, threshold selection, or hyperparameter tuning.

Example:

```bash
jupyter lab
```

For reproducible comparisons, use identical patient-level stratified folds and random seeds for M1, M2, and M3. All records from the same participant must remain in the same fold.



## Reproducibility notes

- Split data at the participant level to prevent information leakage.
- Fit preprocessing transformations on each training fold only, then apply them to the corresponding validation fold.
- Use the same folds for paired model comparisons.
- Preserve OOF predictions and participant identifiers for auditing.
- Select classification thresholds without using the external cohort.
- Report confidence intervals and exact sample counts alongside point estimates.
- Do not select a model solely because it produced the most favorable external result.

## Limitations

- Only a subset of participants had reference-standard COPD labels.
- The external evaluation was preliminary and included few positive cases.
- Facial and tongue measurements may be sensitive to acquisition devices, lighting, centers, and annotation procedures.
- Additional prospective, multicenter validation and calibration assessment are required before clinical use.
- The present results do not establish that the framework can replace spirometry or existing clinical screening pathways.

## Citation

If you use this code, please cite the associated article once its final bibliographic information is available:

```bibtex
@article{rgftcm_copd,
  title   = {Rule-guided multimodal model for COPD risk assessment using tongue, face, constitution and clinical data},
  author  = {Author list to be added},
  journal = {To be added},
  year    = {To be added}
}
```

## License

No open-source license has yet been specified. Until a license file is added, all rights are reserved and reuse requires permission from the copyright holders.

## Contact

For questions about the code, data-access conditions, or study methods, please contact the corresponding author listed in the associated manuscript.
