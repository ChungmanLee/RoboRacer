# COMP47590: Advanced Machine Learning  
## Project 1: RoboRacer

### How to Run
Download zip file, unzip, and open 23205535_ChungmanLee_Project1.ipynb

### Overview
In this project, we aimed to train a neural network model to control a self-driving car in a simulated environment. The prediction task is to output continuous values (X, Y coordinates or steering signals) based on an image input. A regression approach was taken to handle these continuous targets.

### Approaches and Models
1. **Simple CNN**:
   - A custom CNN architecture was implemented from scratch.
   - This CNN performed reasonably well on both training/validation and training/test splits.
   - Notably, the simple CNN achieved the best overall performance when compared to other variants.

2. **Transfer Learning (ResNet18)**:
   - A pre-trained ResNet18 model (with ImageNet weights) was employed, and its final layer was replaced to output X and Y coordinates.
   - The rest of the ResNet layers were frozen to prevent overfitting and to expedite training.
   - Contrary to expectations, the transfer learning approach did not outperform the simple CNN. It showed higher MSE, RMSE, and MAE values on both validation and test sets, indicating potential negative transfer or overfitting on the given task.

3. **Data Augmentation**:
   - The simple CNN approach was also tested with data augmentation techniques (e.g., random flips, rotations, color jitter).
   - While data augmentation typically helps generalization, in this case, the performance did not significantly improve over the baseline simple CNN. Some augmentation techniques like vertical flips may not be realistic for this domain and could have introduced unnecessary variability.

### Results Summary
| Model                      | Set        | MSE    | RMSE   | MAE    |
|----------------------------|------------|--------|--------|--------|
| Simple CNN                 | Train/Val  | 0.0238 | 0.1542 | 0.1107 |
| Transfer CNN (ResNet18)    | Train/Val  | 0.0378 | 0.1944 | 0.1497 |
| Simple CNN w/ Augmentation | Train/Val  | 0.0379 | 0.1946 | 0.1387 |
| Simple CNN                 | Train/Test | 0.0237 | 0.1541 | 0.1093 |
| Transfer CNN (ResNet18)    | Train/Test | 0.0520 | 0.2281 | 0.1720 |
| Simple CNN w/ Augmentation | Train/Test | 0.0429 | 0.2071 | 0.1398 |

The simple CNN without augmentation provided the best generalization performance, as evidenced by consistent performance across the validation and test sets. The Transfer CNN model showed a performance gap, suggesting negative transfer or insufficient adaptation to the new task.

### Challenges and Observations
- **Overfitting and Generalization**:  
  The simple CNN model generalized well from validation to test sets, maintaining similar metrics. In contrast, the Transfer CNN suffered from higher errors on the test set, indicating potential overfitting.
  
- **Augmentation Effects**:  
  Certain augmentation techniques (e.g., vertical flips) may not align with real-world driving scenarios, potentially limiting their effectiveness. More careful selection and tuning of augmentation might be necessary.

- **Implementation Details**:  
  A subtle but significant error occurred when reusing the model class after the optimizer was defined, resulting in unexpected behaviors without clear error messages. Proper code organization and careful initialization order proved essential for reproducible results.

### Future Work
- Experiment with domain-specific augmentations (e.g., brightness or slight horizontal shifts only).
- Fine-tune hyperparameters more systematically, possibly with a more suitable validation protocol.
- Revisit transfer learning with partial fine-tuning of deeper layers or use different pre-trained architectures more aligned with the task domain.
- Investigate more complex architectures or ensemble methods to improve robustness and stability.

Overall, this project demonstrates that a carefully tuned simple CNN can outperform a transfer learning approach when applied to a specialized task like RoboRacer, and that careful experimentation with data augmentation and code structure is crucial for achieving the best results.
