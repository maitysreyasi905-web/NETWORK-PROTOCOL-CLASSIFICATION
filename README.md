# NETWORK-PROTOCOL-CLASSIFICATION

This project explores whether a network packet's size and capture time can be used to predict its network protocol. The analysis is implemented in a Jupyter notebook and compares four supervised classification models.

## Project workflow

The notebook:

1. Combines five packet-capture CSV files (`YouTube_Live_1.csv` through `YouTube_Live_5.csv`) into `YouTube_Live_Merged.csv`.
2. Cleans column names and text values, parses packet timestamps, converts packet length to a number, removes invalid records and duplicates, and retains protocol classes with at least 50 records.
3. Takes a reproducible random sample of 100,000 records (`random_state=42`).
4. Extracts hour, minute, and second from the timestamp.
5. Uses `Length`, `Hour`, `Minute`, and `Second` as input features and `Protocol` as the prediction target.
6. Trains and compares Logistic Regression, K-Nearest Neighbors, Decision Tree, and Random Forest classifiers using an 80/20 stratified train/test split.
7. Reports model accuracy and evaluates the Random Forest with a classification report, confusion matrix, and feature-importance plot. It also displays a shallow view of the decision tree and demonstrates a prediction for a sample packet.

## Requirements

- Python 3
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- Jupyter Notebook, or Google Colab

Install the Python packages with:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

The notebook's first cells use Google Colab's `google.colab.files` to download the merged CSV. That import and download step is Colab-specific. When running locally, place the five source CSV files in the expected location and replace the Colab upload/download code with local file paths as needed.

## Input data

The merge step expects these files:

```text
YouTube_Live_1.csv
YouTube_Live_2.csv
YouTube_Live_3.csv
YouTube_Live_4.csv
YouTube_Live_5.csv
```

The merged data is expected to include `Time`, `Length`, and `Protocol` columns. The notebook also expects the source files to be available at `/content/` when run in Colab, and `YouTube_Live_Merged.csv` to be in the notebook's working directory for the analysis portion.

## Run the project

1. Open the notebook in Google Colab or Jupyter.
2. Add the five source CSV files in the expected location and run the merge cell if you need to create the merged dataset.
3. Ensure `YouTube_Live_Merged.csv` is available to the notebook.
4. Run the notebook cells in order to clean the data, train the models, and view the comparison and evaluation plots.

The analysis cell samples exactly 100,000 eligible rows. The cleaned data must therefore contain at least 100,000 rows after filtering for valid timestamps, nonmissing protocol and length, deduplication, and protocol classes with at least 50 records. If it contains fewer, reduce the sample size in the notebook or omit sampling.

## Evaluation

The notebook compares test-set accuracy across all four models. For Random Forest, it also shows per-class precision, recall, F1-score, and support, alongside a confusion matrix. The notebook does not include fixed benchmark scores; results depend on the supplied capture data.

## Notes

- The model uses only packet length and time-of-day components. It does not use source/destination addresses or packet information text.
- The sample synthetic packet near the end of the notebook illustrates prediction usage; it is not a real capture record.
- The notebook includes an intermediate section that reads an instructor-provided DOCX file. That section requires `python-docx` and the document at `/content/Project 1 for ML.docx`; it is not needed for the CSV classification workflow.
