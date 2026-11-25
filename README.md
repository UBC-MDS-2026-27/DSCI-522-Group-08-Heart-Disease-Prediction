# Heart Disease Predictor

**Authors:** Yuhao Gao, Sarika Tasnim, Christa Ingabire, Nassiba Taib

A data analysis project for DSCI 522 (Data Science Workflows), a course in the Master of Data Science program at the University of British Columbia.

## About

In this project, we build a classification model that uses routine clinical measurements, such as age, chest pain type, resting blood pressure, cholesterol, and maximum heart rate, to predict whether a patient has heart disease.

We compared a dummy classifier, logistic regression, and a support vector classifier (SVC). Logistic regression had the highest cross-validation accuracy and recall, so we selected it for the final evaluation. On the unseen test set of 61 patients, the model achieved **90.2% accuracy and 82.1% recall**, compared with approximately 54% cross-validation accuracy for a baseline that always predicts no heart disease. The model missed 5 of the 28 patients with heart disease in the test set. This is an important limitation if a model like this were used to support healthcare decisions. Although the results are encouraging, further evaluation would be needed before considering any clinical use.

The dataset used in this project is the Heart Disease dataset (Janosi et al., 1989), created by Andras Janosi, William Steinbrunn, Matthias Pfisterer, and Robert Detrano, and obtained from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/45/heart+disease). The dataset was also analyzed by Detrano et al. (1989).

We use the Cleveland Clinic Foundation subset, where each row represents one patient. The dataset contains 13 clinical measurements and a diagnosis of heart disease, recorded on a scale from 0 (no disease) to 4. We combine values 1 through 4 into a single "heart disease present" class, making this a binary classification problem.


## Report

The rendered analysis report is available [here](https://ubc-mds-2026-27.github.io/DSCI-522-Group-08-Heart-Disease-Prediction/).

## Usage

The following instructions explain how to reproduce the analysis and render the report.

### 1. Install the required tools

Install [uv](https://docs.astral.sh/uv/getting-started/installation/) and [Quarto](https://quarto.org/docs/get-started/). Both provide installation instructions for macOS and Windows.

### 2. Clone the repository

Open a terminal and run:

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-08-Heart-Disease-Prediction.git
cd DSCI-522-Group-08-Heart-Disease-Prediction
```

### 3. Set up the Python environment

Run the following command from the repository root:

```bash
uv sync
```

This installs the project's Python dependencies using the versions specified in `uv.lock`. If the required Python version is not installed, uv will download it automatically.

### 4. Render the report

From the repository root, run:

```bash
uv run quarto render analysis/heart_disease_analysis.qmd
```

This executes the analysis and generates the HTML report at:

```text
analysis/heart_disease_analysis.html
```

The analysis downloads the Cleveland dataset programmatically from the UCI Machine Learning Repository. An unmodified copy is saved in `data/raw/`, and the cleaned dataset is saved in `data/processed/`.

**Note:** An internet connection is required to download the dataset. Rendering the report runs the analysis again and may overwrite previously generated data and report files.

## Dependencies

- [uv](https://docs.astral.sh/uv/) (version 0.12 or higher)
- [Quarto](https://quarto.org/) (version 1.10.18 or higher)
- Python 3.14, managed through uv
- Python packages specified in [`pyproject.toml`](pyproject.toml), with versions locked in [`uv.lock`](uv.lock)

## AI use statement

We used Anthropic Claude(Opus 5.5) and OpenAI ChatGPT(GPT-6) to assist with various aspects of this project. These tools supported debugging Python code, troubleshooting dependency and environment configuration errors, improving data wrangling and visualization code, resolving Git and GitHub issues, and diagnosing Quarto rendering problems. We also used AI to help interpret error messages, check the reproducibility of our analysis, and revise portions of the report and README for clarity.

All AI-generated code, explanations, and writing suggestions were reviewed and edited by the authors. Code changes were tested where applicable, and analytical results were checked against the outputs of our implementation. The authors take full responsibility for the accuracy and content of this repository.

Examples of prompts used during the project include:

- "Why does `uv sync` fail with `Expected a Python module at: src/dsci_522_group_08/__init__.py`, and how can I fix the package configuration?"
- "How can I troubleshoot a Quarto report that fails to render because of Python environment or dependency issues?"
- "How do I debug an Altair visualization that is not correctly displaying the proportion of patients with heart disease across different clinical categories?"
- "How can I verify that running the Quarto report from a clean environment reproduces the data processing steps and model evaluation results?"


## License

The Heart Disease Predictor report contained in this repository is licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/).

The software code in this repository is licensed under the MIT License.

See [`LICENSE.md`](LICENSE.md) for more information. If reusing materials from this repository, please provide appropriate attribution and a link to the repository.

## References

Detrano, Robert, Andras Janosi, Walter Steinbrunn, Matthias Pfisterer, Johann-Jakob Schmid, Sarbjit Sandhu, Kern H. Guppy, Stella Lee, and Victor Froelicher. 1989. "International Application of a New Probability Algorithm for the Diagnosis of Coronary Artery Disease." *The American Journal of Cardiology* 64 (5): 304–310. https://doi.org/10.1016/0002-9149(89)90524-9.

Janosi, Andras, William Steinbrunn, Matthias Pfisterer, and Robert Detrano. 1989. "Heart Disease." UCI Machine Learning Repository. https://doi.org/10.24432/C52P4X.