# Reproducing Results of the GeneDRAGNN Platform

The GeneDRAGNN implementation is publicly available on GitHub: [GeneDRAGNN Repository](https://github.com/geneDRAGNN/geneDRAGNN).

## Repository Contents:
- Code for various steps of the implementation.
- Supplementary data related to LUAD (lung adenocarcinoma), a literature review, and gene-enrichment analysis (gene-enrichment analysis was not the primary focus of this research).

---

## Steps to Run the Code

### 1. Clone the Repository:
Clone the GeneDRAGNN project to your local machine using the GitHub link provided.

### 2. Download Required Data:
- To reproduce the results, download the required data from [Google Drive](https://drive.google.com/file/d/17ifXIORwPtkjCGVPwZVdFTBdbfZzyRGg/view).
- Copy the downloaded file into the `data` folder.
- The downloaded file includes:
  - `raw_data` folder containing:
    - `protein_aliases`
    - `protein.links`
    - `GDA_dictionary`
    - `GDA_disease_summary_LUAD`
    - `GCD_LUAD_genes`
    - `HPA-Gene-features`

### 3. Software and Library Requirements:
- Python version **3.9.16** is required to run the code.

**Important Note:**  
Different versions of Python and libraries were tested during development. Some libraries may be incompatible with other versions or environments. To avoid errors:
- Install the required packages in their specified versions.
- If you encounter issues after installing from the `requirements` file, use a dedicated environment to manually install the necessary packages.

---

### Python Libraries Overview:

| **Category**         | **Library Name**        | **Version** | **Build**       | **Channel**   |
|-----------------------|-------------------------|-------------|-----------------|---------------|
| **Core Libraries**    | numpy                  | 1.26.3      | pypi_0          | pypi          |
|                       | pandas                 | 1.1.4       | pypi_0          | pypi          |
|                       | scipy                  | 1.13.1      | pypi_0          | pypi          |
|                       | sympy                  | 1.13.1      | pypi_0          | pypi          |
|                       | matplotlib-inline      | 0.1.7       | pyhd8ed1ab_1    | conda-forge   |
|                       | seaborn                | 0.12.3      | pypi_0          | pypi          |
| **Machine Learning**  | scikit-learn           | 0.24.1      | pypi_0          | pypi          |
|                       | torch                  | 2.5.1       | pypi_0          | pypi          |
|                       | torchvision            | 0.11.2+cu113 | pypi_0         | pypi          |
|                       | pytorch-lightning      | 1.5.1       | pypi_0          | pypi          |
|                       | tensorflow             | 2.18.0      | pypi_0          | pypi          |
| **Data Processing**   | dask                   | 2023.10.0   | pyhd8ed1ab_0    | conda-forge   |
|                       | fsspec                 | 2024.10.0   | pypi_0          | pypi          |
|                       | pyyaml                 | 6.0         | py39ha55989b_5  | conda-forge   |
|                       | requests               | 2.32.3      | pyhd8ed1ab_1    | conda-forge   |
|                       | urllib3                | 2.2.1       | pyhd8ed1ab_0    | conda-forge   |
| **Web Development**   | flask                  | 2.3.3       | pypi_0          | pypi          |
|                       | django                 | 4.3.1       | pypi_0          | pypi          |
|                       | aiohttp                | 3.11.10     | pypi_0          | pypi          |
|                       | httpx                  | 0.28.1      | pyhd8ed1ab_0    | conda-forge   |
| **Visualization**     | matplotlib             | 3.8.0       | pyhd8ed1ab_0    | conda-forge   |
|                       | plotly                 | 6.3.1       | pypi_0          | pypi          |
|                       | bokeh                  | 3.1.2       | pypi_0          | pypi          |
|                       | dash                   | 5.5.2       | pypi_0          | pypi          |
| **Utilities**         | ipython                | 8.12.0      | pyh08f2357_0    | conda-forge   |
|                       | jupyterlab             | 4.3.2       | pyhd8ed1ab_0    | conda-forge   |
|                       | notebook               | 7.3.1       | pyhd8ed1ab_0    | conda-forge   |
|                       | black                  | 23.11.0     | pypi_0          | pypi          |
|                       | mypy                   | 1.5.1       | pyhd8ed1ab_1    | conda-forge   |


---

### 4. Preprocess the Data:
- Navigate to the `data_preprocessing` folder.
- Use the provided code to import datasets.
- Run `main_data_pipeline.ipynb` to integrate datasets.
  - The output file `node_node2vec_data.csv` will be created in the `data/final_data` folder along with training labels and other data.

---

### 5. Running Models and Reproducing Results:
After integrating the dataset, train and evaluate different models using the generated data.

#### Baseline Models:
- Navigate to the `models` folder.
- Run `train_baseline_models.ipynb` to train:
  - Random Forest (RF)
  - Support Vector Machine (SVM)
  - K-Nearest Neighbors (KNN)

#### Experiment Details:
- Each model is trained 100 times using three feature sets:
  - Node features only
  - Node2Vec features
  - Combined Node + Node2Vec features

---

### 6. Challenges with MLP and GNN Models:
Training the baseline MLP and GNN models in `train_gnn_model.ipynb` may fail on machines without GPUs. Reproducing these results requires:
- A GPU with at least 8GB VRAM (e.g., GTX 1070).
- Advanced computational resources for training GNN models.

Despite various attempts, I could not reproduce results for these models without access to GPUs. The original results provided by the authors were used for analysis.

---

### 7. Instructions to Train MLP and GNN Models (If Resources Are Available):
- Modify the `model_name` in `train_gnn_model.ipynb` to select the desired model:
  - Example: Set `model_name = 'SGConv'` for SGConv or `model_name = 'MLP'` for MLP.
- Adjust parameters like `epochs` and `trials` in the `run_trials` function as needed.

---

### 8. Project Files:
The files I ran are included in this document for reference. For the full source code and project, clone the [main repository](https://github.com/geneDRAGNN/geneDRAGNN).

**Written by:** Ati Sarvi
