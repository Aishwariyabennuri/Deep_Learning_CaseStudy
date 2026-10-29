Deep Learning-Based Fashion Visual Search System
Case Study: ResNet50 Feature Extraction + Metadata Filtering
Status: Initial prototype / case study
Environment: Google Colab (recommended)
1. Overview
This project implements an image-based fashion product search system. A user uploads a fashion image, and the system finds visually similar products from a fashion-product image catalog.
The system uses:
ResNet50 pretrained on ImageNet to extract visual features.
Global Average Pooling to convert convolutional feature maps into feature vectors.
A multi-output classification head to predict gender and article type.
Metadata filtering to narrow the candidate products.
Cosine similarity to rank the remaining products by visual similarity.
The current implementation is a research/case-study prototype. It is not yet a production web application.
2. Workflow
Download the Fashion Product Images Dataset through kagglehub.
Locate styles.csv and map product IDs to image files.
Clean missing metadata and retain products with usable images.
Load ImageNet-pretrained ResNet50 without its classification top.
Extract and L2-normalize image feature vectors.
Train a small neural-network classification head for gender and article type.
Upload a query image.
Predict its gender and article type.
Filter the catalog by predicted metadata.
Rank candidates using cosine similarity and display the top five results.
3. Dataset
The notebook downloads the Fashion Product Images Dataset using KaggleHub:
dataset_path = kagglehub.dataset_download(
    "paramaggarwal/fashion-product-images-dataset"
)
The dataset is subject to its publisher's terms and license. Review the dataset page and license before redistributing any images or dataset files. Do not commit the full dataset to GitHub.
4. Requirements
The notebook installs these Python packages:
pip install kagglehub tensorflow scikit-learn pandas matplotlib pillow tqdm
It also uses google.colab.files, so the upload workflow is intended for Google Colab.
5. Run the project in Google Colab
Create a new notebook at Google Colab.
Paste the project code into notebook cells, or upload the .ipynb file.
Run the installation cell.
Run the dataset download, metadata preparation, and feature extraction cells.
Run the classifier training cell.
When prompted, upload a query fashion image.
Review the predicted metadata and the top-five visual search results.
Save the notebook using File → Download → Download .ipynb.
Important: The first run may take time because the dataset is downloaded and features are extracted for many images. A GPU runtime may speed up inference and training; select Runtime → Change runtime type in Colab if a GPU is available.
6. Repository structure
Suggested structure:
fashion-visual-search/
├── README.md
├── Fashion_Visual_Search_Case_Study.ipynb
├── report/
│   └── Fashion_Visual_Search_Case_Study_Report.pdf
├── presentation/
│   └── Fashion_Visual_Search_Presentation.pptx
├── results/
│   └── screenshots/
└── .gitignore
Add your actual notebook, presentation, report, and screenshots using the filenames above or update the names to match your files. Do not upload the dataset, model weights, API keys, credentials, or large generated files unless you have a clear reason and permission.
7. Methodology
Feature extraction
ResNet50 is loaded with ImageNet weights and include_top=False. Global Average Pooling produces one feature vector per image. Features are L2-normalized before similarity comparison.
Classification
A dense layer with 512 ReLU units and dropout feeds two softmax outputs:
Gender
Article type
The classifier is trained for eight epochs in the provided code. Accuracy should be reported only after the notebook has actually run; no performance values are assumed in this README.
Similarity search
The query image is passed through the same feature extractor. Candidate features are compared using cosine similarity, and the highest-scoring candidates are displayed.
8. Current limitations and recommended improvements
Index alignment: The code builds path_to_index from valid_paths, then reorders df to match valid_paths. Later, filtered_indices are built using path_to_index (feature-matrix indices), but results are retrieved using df.iloc[original_index]. This can mismatch dataframe rows and feature vectors. Use a single stable feature index and keep it aligned with both the dataframe and feature matrix.
Strict metadata filtering: A wrong predicted gender/article type can exclude visually relevant products. Consider confidence-aware filtering or a fallback to the full catalog.
Class imbalance: Some article types may have many fewer samples than others. Report per-class precision/recall and consider stratified splits where feasible.
Evaluation: Add a held-out test set and metrics such as top-k retrieval accuracy, Precision@K, Recall@K, and a confusion matrix for classification.
Feature caching: Save feature vectors and metadata so the notebook does not need to extract all features on every run.
Robust image handling: Log unreadable files rather than silently skipping every exception.
Deployment: A future version could provide a Streamlit/FastAPI interface and a vector index for faster search at larger catalog sizes.
9. Reproducibility and responsible use
Record the dataset version, runtime type, package versions, and random seeds.
Do not claim accuracy or retrieval quality unless it is measured and recorded.
Check the dataset license before sharing any images or derived assets.
Add only project files to GitHub; exclude datasets, secrets, caches, and large artifacts.
10. Credits
ResNet50 / TensorFlow Keras Applications documentation
KaggleHub dataset download utility
Fashion Product Images Dataset publisher: paramaggarwal
Please check the dataset's official Kaggle page for the current license and citation requirements.
