# Differentially Private Image Classification

This project explores the application of differential privacy (DP) in image classification tasks, focusing on the trade-off between privacy guarantees and model performance. We demonstrate how transfer learning and efficient gradient accumulation can be leveraged to achieve accuracy levels closer to non-private counterparts while maintaining strong privacy guarantees.

## Features

- Implementation of differentially private training for image classification models
- Utilization of transfer learning with pretrained models on large public datasets
- Comparison of performance across multiple medical image datasets
- Analysis of privacy-utility trade-offs in differentially private deep learning

## Datasets

The project uses the following datasets:

1. Pediatric Pneumonia Chest X-ray
2. DermNet
3. HAM10000

## Models

- BEiT (pretrained on ImageNet22K)
- VGG11 (for comparison with previous work)

## Key Findings

- Significant accuracy improvements achieved through transfer learning with pretrained models
- Consistent advantage of pretrained weights over randomly initialized weights in DP training
- Improved performance when using larger pretraining datasets (e.g., ImageNet22K vs ImageNet1K)
- Demonstration that pretraining advantages may not always be sufficient for all image types

## Results

### Pediatric Pneumonia Chest X-ray

- Achieved ROC-AUC of 0.876 with ε = 0.5 (RDP accounting)
- Accuracy of 82.53% with ε = 0.5 (RDP accounting)
- Non-private baseline accuracy: 93.43%

### DermNet

- Achieved 21.014% accuracy with ε = 0.5 (RDP accounting)

### HAM10000

- Non-private accuracy: 78.75%

## Future Work

- Implement private training on FixCaps for skin lesion classification
- Explore membership inference attacks on semi-private learning approaches
- Conduct in-depth experiments with various hyperparameters and pretraining datasets
- Investigate privacy-preserving techniques for a wider range of image classification tasks

## Contributing

Contributions to this project are welcome. Please fork the repository and submit a pull request with your proposed changes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
