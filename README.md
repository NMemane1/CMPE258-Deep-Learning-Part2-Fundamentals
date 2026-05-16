# CMPE 258 — Deep Learning Part 2: Fundamentals

This repo collects six deep learning tutorial notebooks I worked through for
CMPE 258. Each one starts from the basics and builds up to something practical,
and each has been run end to end so the outputs (plots, training curves, metric
tables) are saved right in the notebook — you can read them on GitHub without
running anything yourself.

For every notebook there's also a short **walkthrough** that explains it
section by section.

## Video walkthrough

I recorded one video that walks through all six notebooks, talking through the
code and the outputs:

**[Watch the full walkthrough](https://docs.google.com/videos/d/1mfHPylhUj8DrhpyJAZH_3cu2eN_P5gFBH5c3Az0blXA/edit?usp=sharing)**

## Notebooks

| # | Topic | Notebook | Walkthrough | Video |
|---|-------|----------|-------------|-------|
| 1 | Classification & Regression Metrics | [open](01_classification_metrics/classification_metrics_tutorial.ipynb) · [Colab](https://colab.research.google.com/github/NMemane1/CMPE258-Deep-Learning-Part2-Fundamentals/blob/main/01_classification_metrics/classification_metrics_tutorial.ipynb) | [walkthrough](01_classification_metrics/walkthrough.md) | [watch](https://docs.google.com/videos/d/1mfHPylhUj8DrhpyJAZH_3cu2eN_P5gFBH5c3Az0blXA/edit?usp=sharing) |
| 2 | Hyperparameter Tuning | [open](02_hyperparameter_tuning/hyperparameter_tuning_tutorial.ipynb) · [Colab](https://colab.research.google.com/github/NMemane1/CMPE258-Deep-Learning-Part2-Fundamentals/blob/main/02_hyperparameter_tuning/hyperparameter_tuning_tutorial.ipynb) | [walkthrough](02_hyperparameter_tuning/walkthrough.md) | [watch](https://docs.google.com/videos/d/1mfHPylhUj8DrhpyJAZH_3cu2eN_P5gFBH5c3Az0blXA/edit?usp=sharing) |
| 3 | Optimizers for Deep Learning | [open](03_optimizers/optimizers_deep_learning_tutorial.ipynb) · [Colab](https://colab.research.google.com/github/NMemane1/CMPE258-Deep-Learning-Part2-Fundamentals/blob/main/03_optimizers/optimizers_deep_learning_tutorial.ipynb) | [walkthrough](03_optimizers/walkthrough.md) | [watch](https://docs.google.com/videos/d/1mfHPylhUj8DrhpyJAZH_3cu2eN_P5gFBH5c3Az0blXA/edit?usp=sharing) |
| 4 | Activation Functions | [open](04_activation_functions/activation_functions_tutorial.ipynb) · [Colab](https://colab.research.google.com/github/NMemane1/CMPE258-Deep-Learning-Part2-Fundamentals/blob/main/04_activation_functions/activation_functions_tutorial.ipynb) | [walkthrough](04_activation_functions/walkthrough.md) | [watch](https://docs.google.com/videos/d/1mfHPylhUj8DrhpyJAZH_3cu2eN_P5gFBH5c3Az0blXA/edit?usp=sharing) |
| 5 | CNN Fundamentals | [open](05_cnn_fundamentals/cnn_fundamentals_tutorial.ipynb) · [Colab](https://colab.research.google.com/github/NMemane1/CMPE258-Deep-Learning-Part2-Fundamentals/blob/main/05_cnn_fundamentals/cnn_fundamentals_tutorial.ipynb) | [walkthrough](05_cnn_fundamentals/walkthrough.md) | [watch](https://docs.google.com/videos/d/1mfHPylhUj8DrhpyJAZH_3cu2eN_P5gFBH5c3Az0blXA/edit?usp=sharing) |
| 6 | Modern CNN Architectures & Transfer Learning | [open](06_modern_cnn_architectures/modern_cnn_architectures_tutorial.ipynb) · [Colab](https://colab.research.google.com/github/NMemane1/CMPE258-Deep-Learning-Part2-Fundamentals/blob/main/06_modern_cnn_architectures/modern_cnn_architectures_tutorial.ipynb) | [walkthrough](06_modern_cnn_architectures/walkthrough.md) | [watch](https://docs.google.com/videos/d/1mfHPylhUj8DrhpyJAZH_3cu2eN_P5gFBH5c3Az0blXA/edit?usp=sharing) |

## What's in each notebook

1. **Classification & Regression Metrics** — How to actually judge a model.
   Confusion matrix, accuracy and why it can lie, precision/recall, F1 and
   F-beta, ROC/AUC and PR curves, multi-class and multi-label metrics,
   confidence calibration and thresholds, then a second part on regression
   metrics (MAE, MSE, RMSE, R²).

2. **Hyperparameter Tuning** — The settings you choose instead of learn.
   Learning rate finder, grid search, random search, Bayesian optimization, and
   a hands-on Optuna example.

3. **Optimizers** — Built from scratch: plain gradient descent, then Momentum,
   AdaGrad, RMSprop, Adam and AdamW — each one introduced to fix a specific
   problem with the one before it. Ends with a real PyTorch comparison.

4. **Activation Functions** — Why a network needs non-linearity at all.
   Sigmoid, Tanh, the vanishing gradient problem, ReLU and its variants, modern
   activations like GELU, and how to pick the right output activation.

5. **CNN Fundamentals** — Convolutional networks from first principles. The
   convolution operation, pooling, full architectures, training with data
   augmentation, and a complete CIFAR-10 image classifier.

6. **Modern CNN Architectures** — ResNet and residual connections,
   EfficientNet and compound scaling, and transfer learning / fine-tuning
   (kept high-level, per the assignment).

## Running the notebooks

The saved outputs are already visible on GitHub, so you can just read them.
To run one yourself, click the **Colab** link in the table above — it opens the
notebook straight from this repo in Google Colab. The first cell of each
notebook installs any packages it needs.

## Notes

- All six notebooks were executed before being committed, so every plot and
  result you see was actually produced by the code.
- The walkthrough files double as the scripts for the videos — they explain
  each notebook section by section.
