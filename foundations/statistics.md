---
layout: default
title: Statistics
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Statistics

## Power analysis

The validity of a statistical test is governed by five interdependent parameters (see Table below). 

| Parameter | Notation | Description | Controllability |
| :--- | :--- | :--- | :--- |
| **Minimum detectable effect** | $$\delta=\mu_1 - \mu_2$$ | Magnitude of the expected difference. Larger effects are easier to observe. | Fixed. The target is set by research goals, but the underlying effect magnitude is fixed. |
| **Sample size** | $$n$$ | Number of observations. | High, within budget. This is the primary lever for controlling power. |
| **Variance** | $$\sigma^2$$ | Noise in the data. | Low, via experimental control and measurement precision. |
| **Significance level** | $$\alpha$$ | False positive rate (specificity). | High, specified upfront. Corresponds to the p-value threshold. |
| **Statistical power** | $$1 - \beta$$ | True positive rate (sensitivity). | High, specified upfront. |

Mathematically, these variables exist in a closed system where fixing any four uniquely determines the fifth (see Equation below).

$$n = \frac{2 \sigma^2}{\delta^2} \Big( Z_{1-\alpha/2} + Z_{1-\beta} \Big)^2$$

## Classification

### True positive rate (Sensitivity, Recall) $$\rightarrow$$ Want 1.0

$$\text{True positive rate}~:= \frac{\text{correctly classified positives}}{\text{total actual positives}} = \frac{\text{TP}}{\text{TP} + \text{FN}}$$

### False positive rate $$\rightarrow$$ Want 0.0

$$\text{False positive rate} := (1 - \text{Specificity}) = \frac{\text{incorrectly classified negatives}}{\text{total actual negatives}} =\frac{\text{FP}}{\text{FP} + \text{TN}}$$

### Precision $$\rightarrow$$ Want 1.0

$$\text{Precision} := \frac{\text{correctly classified positives}}{\text{everything classified as positive}} = \frac{\text{TP}}{\text{TP} + \text{FP}}$$

### Accuracy $$\rightarrow$$ Want 1.0

$$\text{Accuracy} := \frac{\text{correct classifications}}{\text{total classifications}} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}}$$

{: .warning-title }
> Warning
>
> We must be careful when interpreting the accuracy: in cases where samples are dominated by a single class, the accuracy may not reflect the correct identification of rarer classes. To give a simplified example, in a two-class scenario with large class imbalance (99 total `A` and 1 total `B`), if the model predicts all pixels are `A`, the accuracy is 99%.

### Dice coefficient $$\rightarrow$$ Want 1.0

$$\mathrm{Dice} := \frac{2 \mid P \cap G \mid}{\mid P \mid + \mid G \mid}$$

### Jaccard index (equivalent to the Intersection over Union) $$\rightarrow$$ Want 1.0

$$J(P, G) := \frac{|P \cap G|}{|P \cup G|} = \frac{|P \cap G|}{|P| + |G| - |P \cap G|}$$

### F1 score (equivalent to the Dice coefficient) $$\rightarrow$$ Want 1.0

$$F1 :=\frac{2 \cdot Precision \cdot Recall}{Precision + Recall} = \frac{2 TP}{2TP + FP + FN}$$


{: .tip-title }
> Tip
>
> We can address class imbalance by calculating the F1 score across each class separately.

### Normalized confusion matrix $$\rightarrow$$ Want a diagonal of ones and zeros elsewhere

$$\bar{C}_{i,j} = \frac{C_{i,j}}{\sum_{k=1}^{n} C_{i,k}}$$

with $$i$$ the true class, $$j$$ the predicted class, and $$C_{i,k}$$ the count of pixels with ground truth class $$i$$ predicted by the model as class $$k$$.

