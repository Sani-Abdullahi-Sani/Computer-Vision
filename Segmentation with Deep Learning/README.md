# Segmentation with Deep Learning

## 1. Introduction

In this lab, we aim to investigate the efficacy of various deep learning segmentation models. The main focus is on implementing the U-Net model from scratch using PyTorch, along with exploring more advanced architectures from popular libraries. The goal is to assess their performance in image segmentation tasks.

## 2. Data

The dataset consists of:
- **Training Images**: 10 images (from previous labs)
- **Validation Images**: 4 images
- **Test Images**: 4 images

Data augmentation techniques are recommended to mitigate overfitting and enhance model performance. Built-in PyTorch data loaders and augmentation pipelines can be utilized.

## 3. U-Net Model Construction

### 3.1 Implementation

The U-Net model was implemented from scratch in PyTorch with the following considerations:
- Input: 3x512x512 pixel images (color information is crucial).
- Padding: `(1, 1)` to maintain the original input size.
- Pooling: `MaxPool2d` with kernel size=2 and stride=2 to halve feature map sizes.
- Upsampling: 
  - **Variant 1**: `torch.nn.ConvTranspose2d` with kernel size=(2,2) and stride=(2,2).
  - **Variant 2**: `torch.nn.Upsample` with scale factor=2.
- Output: Two channels, with a softmax layer to indicate background (0) and foreground (1).

### 3.2 Training and Evaluation

- **Loss Function**: Binary Cross-Entropy (BCE) for pixel-wise classification.
- **Optimizer**: Adam optimizer for model parameter updates.
- **Checkpoints**: Regularly save model checkpoints and evaluate on the validation set to prevent overfitting.

### Weights and Biases Integration

Integrated Weights and Biases (wandb) to log and visualize:
- **Training and Validation Loss**: Track BCE loss over epochs.
- **IoU (Intersection-over-Union)**: Calculate IoU for training and validation sets.

Plots to create and submit:
- Loss curves (training and validation loss over epochs).
- IoU curves (training and validation IoU over epochs).

After training, evaluate the model on the test set and report the following metrics:
- Accuracy
- Precision
- Recall
- F1-Score
- IoU

### 3.3 Model Performance

**Best Model**: The U-Net with ResNet34 backbone achieved the highest Validation IoU of around 98.30%. Its test evaluation metrics are as follows:
- **Accuracy**: 0.9945
- **Precision**: 0.9970
- **Recall**: 0.9814
- **F1-Score**: 0.9892
- **IoU**: 0.9785

## 4. Other Architectures

After establishing a baseline with U-Net, we explored more advanced architectures:
- **U-Net Variants**: Experimented with different backbones (e.g., ResNet, EfficientNet) using the Segmentation Models PyTorch library.
- **DeepLab v3+**: Trained models across multiple backbone architectures for performance comparison.

### Comparison

The performance of different models was evaluated using accuracy, precision, recall, F1-score, and IoU, summarised in a comparison table. Visualizations of segmentation masks produced by each model were also created.

## Discussion

### Insights on Model Performance

- The initial U-Net models underperformed compared to pre-built architectures, with the ConvTranspose2d method performing worse than bilinear interpolation using Upsample.
- Custom U-Net models showed better resistance to overfitting, while pre-built models exhibited early signs of overfitting during training.
- All models struggled with class imbalance and similar color patterns between the foreground and background.

### Challenges Faced

1. **Channel Output Mismatch**: The implementation produced two-channel output, which needed adjustment using softmax to resolve discrepancies during training.
2. **Data Augmentation Issue**: Early attempts led to misalignment between images and masks. A function was created to augment both simultaneously.

### Suggestions for Improvement

- **Refining Augmentation Strategies**: Exploring task-specific augmentations may yield better performance.
- **Advanced Model Architectures**: Investigating deeper architectures or attention mechanisms could enhance results.
- **Hyperparameter Tuning**: Further tuning of learning rates, batch sizes, and regularization techniques may improve performance.

## References

- PyTorch Installation: [PyTorch Installation Guide](https://pytorch.org/get-started/locally/)
- PyTorch Basics: [PyTorch Quickstart Tutorial](https://pytorch.org/tutorials/beginner/basics/quickstart_tutorial.html)
- Segmentation Models PyTorch: [GitHub Repository](https://github.com/qubvel-org/segmentation_models.pytorch)


