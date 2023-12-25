# Differentially Private Image Classification

Differential privacy (DP) has emerged as a popular strategy for providing privacy guarantees and preventing data leakage in datasets used for training deep learning models. This is achieved by introducing randomly sampled noise into the neural networks during training. However, the incorporation of such noise impacts the inference capability of the model on the training dataset, leading to a reduction in accuracy when predicting on test data. Less stringent implementations of differential privacy can be adopted to obtain private models with higher accuracy. However, it has been observed that such methods provide weaker privacy guarantees. Additionally, training neural networks with DP is more computationally intensive compared to training normal models. This raises an important consideration regarding the trade-off between privacy and utility when implementing DP for training privacy-preserving deep learning models. Our work addresses this trade-off by demonstrating how transfer learning and efficient gradient accumulation mechanisms can be leveraged to achieve accuracy levels closer to non-private counterparts. Furthermore, recognizing the challenges associated with obtaining pretrained models for various image classification problems, we explore the benefits of using publicly available pretraining datasets that are out of distribution with the private training datasets. Our investigation aims to determine if this approach can be considered a general solution to privacy-preserving problems.

## Comparison with state-of-the-art

### 1) Pediatric Pneumonia Chest X-ray:

For the Pediatric Pneumonia Chest X-ray dataset, previous research employed a VGG11 model with batch normalization using DP for the same binary classification task [30]. Their models were pretrained on a smaller subset of ImageNet known as ImageNet1K [27]. In their strict privacy case of E = 0.64 using RDP accounting, they achieved a ROC-AUC of 0.848. In our experiments, using a larger pretrained dataset with the BEiT model and a stricter privacy budget of E = 0.5 using RDP accounting, we achieved a ROC-AUC of 0.876 (+.028). We obtained our ROC-AUC results using the roc auc score and roc curve functions from scikit-learn [33].

Additionally, other research on this dataset utilized a novel algorithm called PILLAR, employing semi-private learning [22]. In their experiments, treating 10% of the dataset as public, they achieved an accuracy of 83% in their strict case of E = 0.1 using RDP accounting. In comparison, we achieved 82.53% accuracy with a stricter privacy budget of E = 0.5 using RDP accounting. Despite differences in accuracy and privacy levels, our approach did not require treating any images as public. Future work may explore membership inference attacks against the 10% of data that was made public.

Lastly, the original researchers of the dataset achieved an accuracy of 92.8% using a convolutional neural network pretrained on ImageNet1K for the binary classification task. In our non-private baseline, we attained an accuracy of 93.43% (+0.63%) with our BEiT pretrained on ImageNet22K.

### 2) DermNet:

In the context of DermNet, the only identified research applying DP to DermNet using a single neural network was PILLAR [22]. In their strict case of E = 0.1 using RDP accounting, they achieved an accuracy of 19%, compared to our 21.014% with E = 0.5 using RDP accounting. Despite our looser privacy budget, we achieved slightly better accuracy, and notably, we did not treat any samples as public during training.

### 3) HAM10000:

Research by [34] presents state-of-the-art results for non-private training in skin lesion classification using capsule networks for dermatoscopic image classification. While our non-private experiments resulted in a maximum accuracy of 78.75%, FixCaps achieved an accuracy of 96.49% on the HAM10000 dataset. Future work may involve implementing private training on FixCaps to evaluate its performance with differential privacy and explore potential improvements in test accuracy. This would necessitate developing implementations of the privacy engine compatible with layers used in FixCaps.

However, the current literature lacks baselines for comparing our DP training results. Further experiments could be conducted on recent works with high accuracy without differential privacy, developing implementations with DP training to observe the utility vs privacy tradeoff with incorporated differential privacy.

  

In this work, we demonstrated the significant increase in accuracy achievable through the use of pretrained models trained on large publicly available datasets when performing transfer learning with differentially private learning. Our findings indicate that this improvement holds true for datasets out of distribution with the pretraining dataset and having no overlapping classes. Across all experiments, it is evident that utilizing randomly initialized weights for private learning yields consistently poor accuracy, while the use of pretrained weights consistently provides a substantial advantage.

Moreover, in the Pediatric Pneumonia Chest X-ray dataset, our demonstration revealed a substantial improvement in accuracy when using ImageNet22K instead of ImageNet1K. This observation emphasizes the impact of the pretraining dataset's size on the performance of differentially private training.

Despite the pretrained models consistently proving advantageous, our DermNet experiment reveals that this advantage may not always suffice. The accuracy obtained in each of the three private trials was less than half of the accuracy achieved in the non-private trial. This result underscores that while large publicly available datasets for pretraining offer advantages, they may not serve as a universal solution for differentially private training across all image types.

Our experiments highlight the complexity of achieving a universal solution that strikes an ideal balance between privacy and utility. To develop differentially private models with optimal privacy guarantees suitable for real-world applications, additional in-depth experiments exploring a range of hyperparameters and pretraining datasets are imperative across different image classification tasks.

