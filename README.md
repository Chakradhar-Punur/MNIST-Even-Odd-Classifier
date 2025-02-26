# Entropy-Based Gradient Learning for Even/Odd MNIST Classification

## Introduction

In this project, we explore an entropy-based gradient learning framework for classifying MNIST digits as even or odd. Instead of traditional loss-based updates (e.g., cross-entropy loss), I applied entropy gradients and enforced a z constraint to regulate weight updates. The model was trained using a dual-weight structure consisting of primary weights (w1) and auxiliary weights (G1).

## Approach and Methodology

### Entropy-Based Gradient Framework:

Our approach revolves around computing weight updates using entropy gradients rather than standard loss gradients. The entropy gradient was defined as:

![Screenshot 2025-02-26 at 6 09 15 PM](https://github.com/user-attachments/assets/537ee6fb-9352-43e3-ab3f-3d6fdfea072c)

This approach attempts to adjust the model’s knowledge representation dynamically based on entropy changes.

###  Enforcing the z Constraint:

To prevent excessive changes in the knowledge representation, we introduced a constraint on z updates:

![Screenshot 2025-02-26 at 6 10 14 PM](https://github.com/user-attachments/assets/cef7279b-266c-4c0b-88cf-7dff2fcf2f7c)

where δ was dynamically adjusted over epochs. If any update violated this constraint, a global scaling factor was applied to reduce excessive changes.

##  Implementation Details

### Dual-Weight Structure:

Unlike classical models that use a single weight matrix, we used two weight matrices:

* Primary weights (w1) – Represented the core learned knowledge.
* Auxiliary weights (G1) – Helped adjust the updates.

The model’s prediction was computed using:

![Screenshot 2025-02-26 at 6 12 37 PM](https://github.com/user-attachments/assets/96e4b1f7-be87-4249-97fb-1282cb394ca7)

### Custom Update Rules:

Instead of using the binary cross-entropy loss gradient, we applied entropy-based gradients to update weights:

* Compute logit values
* Compute entropy-based gradient updates
* Compute new updates
 
 ![Screenshot 2025-02-26 at 7 01 52 PM](https://github.com/user-attachments/assets/2edb9603-e18b-45ce-be51-b9f067decf45)

* Apply z constraint and scale updates if necessary.

 ## Training Dynamics and Comparison with Classical Updates

| Approach | Entropy-Based learning | Fixed Loss-Based Update |
| ------------------ | ---------------------- | ----------------------- |
| Final Accuracy | ~50% | ~80% |
| Learning Dynamics | No clear learning trend, weights failed to separate even/odd digits. | Accuracy steadily increased, reaching a stable performance. |

### Observations:

* The entropy-based learning framework did not provide meaningful updates, likely because entropy alone is not a reliable optimization target for classification.
* The classical approach (binary cross-entropy loss) learned effectively, showing a clear improvement over epochs.
* The dual-weight structure did not show a significant benefit over a single-weight approach in this case.

## Challenges and Insights

### Challenges:

* Gradient Instability: The entropy-based gradient updates did not effectively push the model toward correct classification.
* Weight Constraints Suppressed Learning: The z constraint limited updates too much, causing learning stagnation.
* Random-Like Training Behavior: Accuracy hovered around 50%, indicating no real learning happened.

### Insights:

* Classical loss-based optimization (cross-entropy) was significantly better for binary classification.
* The z constraint method could be useful in other applications (e.g., adversarial robustness) but was harmful for learning in this setup.
* The dual-weight approach did not provide clear benefits over a standard weight structure.

## Conclusion

While the entropy-based gradient framework was an interesting approach, it failed to learn effectively in this classification task. Switching to traditional cross-entropy loss updates immediately led to significant improvements, reaching an accuracy of 80.6%. Future work could explore hybrid approaches combining entropy-based constraints with standard loss functions for better results. 
