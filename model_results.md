# Speaker Verification — Model Results Tracker

This document tracks the experimental results of the various models trained for the term project. 
All evaluations use a static 3-second evaluation window (center-cropped) and calculate accuracy based on the distance between extracted embeddings.

## 📊 Summary of Experiments

| Model Architecture | Loss Function          | Epochs | Params | Training Accuracy | Test Accuracy | Generalisation Gap | Notes / Observations |
| :----------------- | :--------------------- | :----- | :----- | :---------------- | :------------ | :----------------- | :-------------------- |
| **ResNet-18**      | Contrastive Loss (L2)  | 30     | 11M    | *Not Tracked*     | 80.61%        | *N/A*              | Baseline system. Proved viability of 80 Mel-bin spectrograms. |
| **ResNet-34**      | Contrastive Loss (L2)  | 30     | 21M    | 92.42%            | 82.41%        | 10.01%             | Good embedding separation but clear overfitting on training set (10% gap). |
| **ResNet-50**      | Contrastive Loss (L2)  | 30     | 23M    | *Pending*         | *Pending*     | *Pending*          | Bottleneck blocks output 2048 instead of 512. |
| **ResNet-34**      | Triplet Margin Loss    | 30     | 21M    | *Pending*         | *Pending*     | *Pending*          | Should force a hard relative margin and improve generalisation. |

---

## 📈 Detailed Breakdown

### Experiment 1: ResNet-18 Baseline
- **Configuration:** ResNet18 (1-channel input) -> 256 embedding dimension with L2 normalization. Contrastive Loss margin = 1.0. 
- **Learning Rate:** 1e-3 (Adam)
- **Result:** **80.61%** Test Accuracy.
- **Analysis:** A very solid baseline that successfully proved the Siamese architecture and audio preprocessing pipeline worked.

### Experiment 2: Upgrading to ResNet-34
- **Configuration:** ResNet34 -> 256 embedding dimension. Same Contrastive Loss setup.
- **Result:** **92.42%** Training / **82.41%** Testing.
- **Analysis:** Pushed test accuracy up by ~1.8%. However, evaluating the training set revealed a 92%+ training set accuracy, indicating the model memorized the training dataset too much. The distance distributions showed significant overlap on unseen speakers (the "Test" distribution had many False Positives/Negatives between 0.5 and 1.0 distances).

### Experiment 3 & 4 (In Progress)
*(To be filled in when training completes)*
