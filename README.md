# Brain Tumor MRI Binary Classification

A ResNet-based convolutional neural network that classifies brain MRI scans as containing a tumor or not, built as a Bachelor's graduation project in Computer Science at the German Jordanian University.

**Supervisor:** Dr. Samer Nofal

## Overview

Brain tumors are a major cause of cancer-related deaths, and MRI is one of the primary tools used to evaluate them. This project trains binary classification models on fluid-attenuated inversion recovery (FLAIR) brain MRI scans, using a custom ResNet architecture built in PyTorch. 24 experiments were carried out, each with fine-tuned parameters and the best performing model was chosen.

The best-performing model reached **97.6% validation accuracy**.

## Dataset

- Source: [Brain Tumor dataset on Kaggle](https://www.kaggle.com/datasets/jakeshbohaju/brain-tumor)
- 3,762 FLAIR MRI images, each cropped to 240×240 pixels
  - 1,683 images with a tumor
  - 2,079 images without a tumor
- Two train/validation splits were tested:
  - 90% train / 10% validation (3,386 / 376 images)
  - 80% train / 20% validation (3,010 / 752 images)
- Data augmentation (random cropping, random horizontal flips) and normalization were applied to compensate for the relatively small dataset size.

## Methodology

- **Language / framework:** Python, PyTorch
- **Key libraries:** NumPy, torchvision, scikit-learn, Matplotlib
- **Environment:** Google Colab (GPU-accelerated)
- **Model:** A custom Convolutional Neural Network based on the ResNet architecture (convolutional blocks with residual connections)
- **Optimizer:** Adam (fixed across experiments)
- Fixed hyperparameters: gradient clipping = 0.1, weight decay = 1e-4
- Varied hyperparameters across experiments:
      1. number of epochs (10/20/30)
      2. batch size (16/32)
      3. learning rate (0.01/0.05)

24 total experiments were run (12 on the 90-10 split and 12 on the 80-20 split) to study how these hyperparameters affect performance.

## Results

The best performing models for each data split are:

| Split | Best Trial | Epochs | Batch Size | Learning Rate | Accuracy | Precision | Recall |
|-------|-----------|--------|------------|----------------|----------|-----------|--------|
| 90-10 | Trial 5   | 30     | 16         | 0.01           | **97.6%** | High | High |
| 80-20 | Trial 18  | 30     | 32         | 0.01           | 97.3%     | High | High |

Overall findings:
- Larger numbers of epochs, larger batch sizes, and a lower learning rate (0.01) produced the best results.
- The 90-10 split slightly outperformed the 80-20 split, suggesting that allocating more data to training (versus validation) benefits the model more.
- Both best trials showed low, stable training/validation loss, indicating a good fit without significant overfitting.

## Conclusions

- The model performs well enough to act as a potential **second reader** or part of a quality-assurance workflow — but not as a replacement for radiologists, given the false positive/negative rates observed.
- Results support the feasibility of using deep learning on MRI scans for tumor classification, while underscoring the need for further validation.

## Limitations

- Model generalizability could not be tested against a second, independent dataset (no other FLAIR datasets were available).
- The dataset was relatively small (3,762 images) for this type of study.
- Only the Adam optimizer was tested; weight decay and gradient clipping values were not swept.
- Training was done on a public Kaggle dataset rather than real-world hospital data (attempts to obtain the latter were unsuccessful).

## References

1. Brain Tumor Dataset, Kaggle — https://www.kaggle.com/datasets/jakeshbohaju/brain-tumor
2. "How to Train Your ResNet" — https://myrtle.ai/learn/how-to-train-your-resnet/
3. "Classifying CIFAR10 images using ResNets, Regularization and Data Augmentation in PyTorch" — https://jovian.ai/aakashns/05b-cifar10-resnet
4. "How to Normalize Image Dataset in PyTorch" — https://www.binarystudy.com/2022/04/how-to-normalize-image-dataset-inpytorch.html

## Disclaimer

This is a research/academic project, not a certified diagnostic tool. It should not be used for actual clinical decision-making.
