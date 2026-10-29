
👗 Deep Learning-Based Fashion Visual Search
Find fashion products by image using deep learning and visual similarity.
ResNet50 · Feature Extraction · Metadata Filtering · Cosine Similarity


� � � � �

✨ Project Overview
Imagine finding a fashion product simply by uploading a picture. This project explores that idea with a deep learning-powered visual search system that compares an uploaded fashion image with a catalog of fashion product images and returns visually similar results.
The system uses a pretrained ResNet50 model to extract image features, predicts product metadata such as gender and article type, narrows down candidate products using those predictions, and ranks the candidates by cosine similarity.
Project goal: Make fashion discovery more visual, intuitive, and convenient than searching by text alone.
🚀 Key Features
🖼️ Image-based search — use a fashion image as the search query.
🧠 Deep feature extraction — leverage ImageNet-pretrained ResNet50.
🏷️ Metadata prediction — predict gender and article type with a neural-network classification head.
🎯 Smart candidate filtering — narrow the catalog using predicted metadata.
📊 Similarity ranking — rank candidate images using cosine similarity.
🔝 Top-5 recommendations — display the five highest-ranked candidates from the filtered set.
☁️ Google Colab workflow — run the notebook in a cloud-based Python environment.
🧭 How It Works
       Upload a fashion image
                 │
                 ▼
     Preprocess the query image
                 │
                 ▼
      ResNet50 feature extraction
                 │
        ┌────────┴────────┐
        ▼                 ▼
  Image feature       Metadata prediction
     vector          (gender + article type)
        │                 │
        │                 ▼
        │          Filter product catalog
        │                 │
        └────────┬────────┘
                 ▼
       Cosine similarity ranking
                 │
                 ▼
      Display the top 5 matches
🔬 Technical Pipeline
Dataset preparation: Download the Fashion Product Images Dataset using KaggleHub.
Metadata cleaning: Read styles.csv, handle missing metadata, and retain products with usable image files.
Feature extraction: Load ResNet50 without its original classification top and apply Global Average Pooling.
Feature normalization: L2-normalize the extracted feature vectors for similarity comparison.
Metadata classification: Train a neural-network head to predict gender and article type.
Query processing: Upload a fashion image and obtain its predicted metadata and visual feature vector.
Candidate filtering: Narrow the catalog using the predicted metadata.
Similarity search: Rank candidates with cosine similarity and show the top five results.
🛠️ Technology Stack
Technology
Purpose
Python
Core programming language
TensorFlow / Keras
Deep learning and model construction
ResNet50
Pretrained visual feature extraction
Scikit-learn
Machine-learning utilities
Pandas & NumPy
Dataset preparation and numerical operations
Pillow (PIL)
Image loading and processing
Matplotlib
Visualization
tqdm
Progress bars
KaggleHub
Dataset download
Google Colab
Notebook execution and image upload workflow
📦 Dataset
This project uses the Fashion Product Images Dataset, downloaded through KaggleHub.
Dataset identifier:
dataset_path = kagglehub.dataset_download(
    "paramaggarwal/fashion-product-images-dataset"
)
The notebook uses product image files and the styles.csv metadata file to associate product IDs with their attributes and images.
Before sharing: Review the dataset publisher's current license and citation requirements. Do not upload the complete dataset to this repository unless redistribution is permitted.
⚙️ Getting Started
Option 1 — Run in Google Colab (recommended)
Open Google Colab.
Upload the project notebook (.ipynb) or create a notebook and copy in the project code.
Run the package installation cell.
Run the dataset download and metadata preparation cells.
Run feature extraction and classifier training.
Upload a fashion image when prompted.
Review the predicted metadata and the top-five visual matches.
Option 2 — Install the dependencies
Run this command in a Python environment that supports the required packages:
pip install kagglehub tensorflow scikit-learn pandas matplotlib pillow tqdm
The current image-upload flow uses google.colab.files, so it is designed for Google Colab. A local Python environment may require changes to the upload code.
💡 Runtime Tip
The first run may take time because the dataset must be downloaded and image features extracted. If available, enable a GPU in Colab using Runtime → Change runtime type to help speed up model computation.
📁 Suggested Repository Structure
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
Update the filenames to match the files actually included in your repository.
🧠 Model & Methodology
ResNet50 Feature Extraction
ResNet50, pretrained on ImageNet, is loaded without its original classification layer (include_top=False). Global Average Pooling converts its convolutional feature maps into a compact feature vector for each image. The vectors are L2-normalized before similarity comparison.
Multi-Output Classification
A small neural-network head uses a 512-unit ReLU dense layer, dropout, and two softmax outputs to predict:
Gender
Article type
The provided code trains this classifier for eight epochs. Actual accuracy and generalization must be measured by running the notebook and evaluating it on held-out data.
Cosine Similarity
The query image is processed using the same feature-extraction pipeline. Its feature vector is compared with candidate product vectors using cosine similarity, and the highest-scoring candidates are returned.
⚠️ Current Limitations
This repository is a research / case-study prototype, not a production-ready web application.
Feature-index alignment: Dataframe rows and feature-matrix indices may become misaligned during filtering and reordering. Use one stable index mapping for both metadata and feature vectors before trusting retrieved results.
Strict metadata filtering: Incorrect metadata predictions can exclude relevant products. Confidence-aware filtering or a fallback search across the full catalog could improve recall.
Class imbalance: Some article types may have fewer examples than others. Evaluate per-class precision and recall and consider stratified data splits where feasible.
Evaluation: The README does not claim measured accuracy or retrieval quality. Add a held-out test set and report metrics such as Precision@K, Recall@K, top-k retrieval accuracy, and a classification confusion matrix.
Repeated computation: Feature caching would reduce the need to extract features again on every run.
Image errors: Add logging for unreadable or missing images to make dataset issues easier to diagnose.
Deployment: A web interface and a scalable vector index have not yet been implemented.
🛣️ Future Enhancements
[ ]
Fix and test the alignment between product metadata and image-feature indices.
[ ]
Cache extracted feature vectors for faster repeated searches.
[ ]
Add confidence-aware metadata filtering and a full-catalog fallback.
[ ]
Evaluate classification and retrieval quality on a held-out test set.
[ ]
Display similarity scores alongside recommended products.
[ ]
Build an interactive interface with Streamlit or FastAPI.
[ ]
Explore vector indexing for faster search on larger catalogs.
[ ]
Add robust logging and input-image validation.
🔐 Reproducibility & Responsible Use
Record dataset version, package versions, runtime type, and random seeds.
Report only metrics that have actually been measured.
Check the dataset license before redistributing images or derived assets.
Keep credentials, API keys, datasets, caches, and large generated artifacts out of Git.
Use a .gitignore file to help prevent accidental commits of unnecessary files.
📚 Credits & References
ResNet50: TensorFlow / Keras Applications
Dataset download: KaggleHub
Dataset: Fashion Product Images Dataset by paramaggarwal
Refer to the dataset's official Kaggle page for its latest license and citation requirements.

Built to explore the intersection of fashion discovery and computer vision. ✨
Current stage: Research prototype · Google Colab notebook
