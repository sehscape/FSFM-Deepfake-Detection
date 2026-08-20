### FSFM-Deepfake-Detection
A deep learning project for real vs. fake face detection using the FSFM-3C (Face Security Foundation Model) with a ViT-B/16 backbone.
The model is fine-tuned on the Kaggle 140K Real and Fake Faces dataset and incorporates five improvements to enhance deepfake detection performance.

## Project Overview

Deepfakes are AI-generated or manipulated images that can be difficult to distinguish from genuine facial images.
This project uses a pretrained FSFM ViT-B/16 model and fine-tunes it for binary classification:
REAL – genuine human face
FAKE – AI-generated face
The original FSFM model was pretrained on approximately 3.3 million faces from VGGFace2 using self-supervised facial representation learning.

## Key Features
   The project includes five improvements over a basic fine-tuning pipeline:
1. Focal Loss
2. Cosine Annealing with Warm Restarts
3. Progressive Unfreezing with Layer-wise Learning Rate Decay (LLRD)
4. Test-Time Augmentation (TTA)
5. Stochastic Weight Averaging (SWA)

    These techniques are implemented to improve generalization and robustness of the deepfake detector.

## Training Pipeline
1. Environment Setup
   The notebook checks:

   Python version
   PyTorch version
   CUDA availability
   GPU type
   GPU memory

Training was performed using a GPU environment.

2. Pretrained Model
The FSFM ViT-B/16 pretrained checkpoint is downloaded from Hugging Face.

3. Dataset Preparation

The Kaggle dataset is downloaded using kagglehub and organized into:

deepfake_subset/

├── train/

│   ├── real/

│   └── fake/ 

├── valid/

│   ├── real/

│   └── fake/

└── test/

    ├── real/
    
    └── fake/

4. Fine-Tuning

   The pretrained model is fine-tuned using:

   Focal Loss
   AdamW optimizer
   Cosine Annealing Warm Restarts
   Progressive layer unfreezing
   Layer-wise learning rate decay
   Mixed precision training

   Training is performed for 15 epochs

5. Stochastic Weight Averaging

   SWA is applied using checkpoints from the later training epochs to obtain a more robust final model.

6. Test-Time Augmentation

   The final model can evaluate an image using multiple transformed views and average the predictions.

   This produces a more robust prediction compared with using a single image transformation.

## Results

   The trained model achieved the following results on the held-out test subset:

    Metric - Result
    Accuracy - 93.25%
    Balanced Accuracy - 93.25%
    AUC-ROC - 98.76%
    EER	- 0.0585

   Using Test-Time Augmentation:

   Metric - Result
   TTA Accuracy	- 93.40%
   TTA AUC-ROC - 98.84%
   TTA EER - 0.0525

   The best validation AUC during training was approximately 99.05%.

## Note: These results are based on the subset used in the notebook and should not be interpreted as performance on the complete 140K dataset.

## Technologies Used

    Python
    PyTorch
    Torchvision
    timm
    Hugging Face Hub
    Scikit-learn
    NumPy
    SciPy
    Matplotlib
    Seaborn
    Pillow
    tqdm
    KaggleHub


## Hardware Requirements

   Training is computationally intensive because FSFM ViT-B/16 is a large vision transformer.

   Recommended:

    Google Colab
    NVIDIA T4 GPU or better
    Approximately 16 GB GPU VRAM
    CUDA-enabled PyTorch

## How to Run
1. Clone the repository - git clone https://github.com/YOUR_USERNAME/FSFM-Deepfake-Detection.git cd FSFM-Deepfake-Detection
2. Install dependencies - pip install -r requirements.txt
3. Open the notebook
   Open:

    FSFM_Deepfake_Detection_Improved.ipynb   using:

      Google Colab
      Jupyter Notebook
      JupyterLab

4. Enable GPU

   For Google Colab:

   Runtime → Change runtime type → T4 GPU

5. Run the notebook

   The notebook automatically:

    Installs/imports required packages
    Downloads the pretrained FSFM checkpoint
    Downloads the Kaggle dataset
    Creates the training subset
    Preprocesses the images
    Fine-tunes the model
    Applies SWA
    Evaluates the model
    Performs TTA
    Generates visualizations

## References
#  FSFM

  Wang, G., Lin, F., Wu, T., Liu, Z., Ba, Z., & Ren, K.
  "FSFM: A Generalizable Face Security Foundation Model via Self-Supervised Facial Representation Learning." CVPR 2025.














