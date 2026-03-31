**Chihuahua vs. Muffin: Data-Centric Image Classification**
This repository contains a high-performance image classification pipeline for the Chihuahua vs. Muffin challenge. Unlike traditional model-centric approaches, this project focuses on Data-Centric AI—improving the quality and influence of the training data to achieve superior generalization on unseen test sets.
🚀 **Performance Summary**
 * Model Architecture: ResNet-18 (Trained from scratch)
 * Best Training Accuracy: 99.6%
 * Best Validation Accuracy: 98.5%
 * Best Test Accuracy: 97.46%
🛠️ **Technical Approach**
1. Data-Centric Optimization (via 3LC)
The core of this project’s success was using the 3LC Dashboard to perform surgical data edits:
 * Label Purification: Identified and removed "poisonous" data, such as images containing both a dog and a muffin, which confuse the decision boundary.
 * Strategic Weighting: Applied higher weights (up to 5.0) to "Hard Samples" (images with 0% initial accuracy) and lower weights (0.1) to "Easy Samples" to prevent overfitting and force the model to learn complex textures.
 * Class Balancing: Adjusted weights to compensate for the dataset imbalance (2,000 Chihuahuas vs. 1,500 Muffins).
2. Advanced Training Dynamics
 * Optimizer: SGD with Nesterov Momentum (0.9) for better generalization compared to Adam.
 * Learning Rate Schedule: Utilized CosineAnnealingLR starting at 0.01, allowing the model to settle into the global minimum with a final "surgical" rate of 0.00005.
 * Regularization: Implemented Label Smoothing (0.1) and Weight Decay (1e-3) to bridge the gap between training and test performance.
3. Robust Data Augmentations
To prevent the ResNet-18 from memorizing specific pixel locations, a heavy augmentation pipeline was used:
 * RandomResizedCrop: Forces the model to identify objects from small patches (e.g., a nose or crumb texture).
 * RandomErasing: Drops information to ensure the model finds multiple redundant features.
 * ColorJitter: Removes color-based shortcuts, forcing a focus on morphology and texture.
📁 **Repository Structure**
 * train.py: Main training script integrating the 3LC API and PyTorch.
 * best_model.pth: The highest-performing model checkpoint.
 * requirements.txt: Necessary libraries (torch, torchvision, tlc, etc.).
💻 **How to Run**
 * Install dependencies: pip install -r requirements.txt
 * Register the 3LC tables: python register_tables.py
 * Launch the 3LC service to pick up data edits: 3lc service
 * Run training: python train.py
Author: Tanishq
Project: MNNIT AI Hackathon / Azeotropy Finalist
