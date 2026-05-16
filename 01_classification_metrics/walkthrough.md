# Walkthrough — Classification & Regression Metrics

This is my recording script for the video. It follows the notebook top to
bottom so I can talk through it cell by cell while it's open on screen.

## What this notebook is about

This is the big one. It's a full tour of how we *measure* whether a model is
any good — not how we train it, but how we judge it afterward. It starts with
binary classification, walks all the way up to multi-label and semi-supervised
problems, and then has a second part on regression metrics. 62 code cells, 18
"tasks". I'll group my explanation by task so the video stays organized.

## Task 1 — Setup and the classification problem (code cells 1-6)

I open by saying what classification even is — predicting a category instead of
a number. The first code cell installs/imports the usual stack (numpy, pandas,
matplotlib, scikit-learn). Then I build a **synthetic dataset** with
`make_classification` so the whole notebook is reproducible — anyone who runs it
gets the exact same numbers because I set a random seed.

Cell 3 plots the class distribution so you can see how balanced it is. Cell 4
does the train/test split — I explain why we never score a model on data it
trained on. Cells 5-6 train a plain Logistic Regression and look at a few raw
predictions. Point out: at this stage we just have predictions, no judgement yet.

## Task 2 — The confusion matrix (code cells 7-13)

This is the foundation of everything. I explain the four outcomes — True
Positive, True Negative, False Positive, False Negative — using the courtroom
analogy (convicting an innocent person vs letting a guilty one go). Cell 7-8
compute the matrix and pull out the four numbers. Cell 9 is a custom heatmap
function that makes it readable. Cells 10-12 dig into *which* predictions were
wrong and plot the probability distributions for each outcome. Cell 13 verifies
the math relationships by hand. Key line for the video: "every metric after this
is just a different ratio of these four numbers."

## Task 3 — Accuracy and why it lies (code cells 14-18)

Accuracy = how often you're right. Easy. Then I show the **accuracy paradox**:
on a fraud dataset that's 99% legit, a model that predicts "never fraud" scores
99% accuracy and is completely useless. Cells 16-17 demonstrate and plot exactly
that. Cell 18 introduces balanced accuracy as the fix. The takeaway: accuracy is
fine on balanced data and dangerous on imbalanced data.

## Task 4 — Precision and recall (code cells 19-24)

Precision answers "when I say positive, am I right?" Recall answers "did I catch
all the positives?" I use the spam-vs-cancer framing — spam filter wants
precision (don't trash real email), cancer screen wants recall (don't miss a
case). Cells 22-23 are the important ones: they show the **trade-off** by moving
the decision threshold and watching one metric rise as the other falls. Cell 24
adds specificity (recall for the negative class).

## Task 5 — F1, F-beta, MCC, Cohen's Kappa (code cells 25-29)

F1 is the harmonic mean of precision and recall — one number that punishes you
if either is bad. I explain why *harmonic* mean and not regular average (it
refuses to be fooled by one great score). F-beta lets you weight recall heavier
(F2) or precision heavier (F0.5). MCC and Cohen's Kappa are the "honest" metrics
that hold up even on imbalanced data.

## Task 6-7 — ROC/AUC and Precision-Recall curves (code cells 30-31)

ROC sweeps every possible threshold and plots true-positive rate vs
false-positive rate; AUC is the area under it — 1.0 is perfect, 0.5 is a coin
flip. The PR curve does the same idea but is the better choice when classes are
imbalanced. I explain when to reach for each.

## Task 8 — Multi-class metrics (code cells 32-33)

Switches to the Iris dataset (3 classes). The new idea here is **averaging
strategies** — macro (treat every class equally), micro (treat every sample
equally), weighted (account for class size). Cell 33 prints all three side by
side so you can see they disagree.

## Task 9 — Imbalanced data (code cell 34)

A consolidated comparison showing which metrics survive heavy imbalance and
which collapse. Reinforces Task 3's lesson with one clean table.

## Task 10 — MLOps and a metrics dashboard (code cell 35)

Cell 35 defines `comprehensive_classification_report` — one function that prints
every metric at once. I frame this as "what you'd actually wire into a
production monitoring pipeline."

## Tasks 11-13 — Advanced classification (code cells 36-54)

- **Multi-label** (36-42): one sample can have several labels at once. New
  metrics: Hamming loss, subset accuracy, Jaccard/IoU score.
- **Semi-supervised** (43-46): most data is unlabeled. I demo self-training and
  show how to judge the quality of the pseudo-labels it generates.
- **Confidence, thresholds, bucketization** (47-54): calibration curves (does
  "90% confident" actually mean right 90% of the time?), picking a threshold for
  a business goal, and routing low-confidence predictions to a human reviewer.

## Part 2 — Regression metrics (code cells 55-62)

Tasks 14-18 switch to predicting numbers. MAE (average error in real units),
MSE (squares the error so big mistakes hurt more), RMSE (back in real units),
R² (fraction of variance explained), Adjusted R² (R² that doesn't reward you for
adding useless features), and MAPE (error as a percentage). Cell 62 is a final
regression dashboard. I close by saying the same rule applies everywhere: pick
the metric that matches what your project actually cares about.

## How I'll close the video

One sentence: there is no single "best" metric — the right one depends on your
data balance and what a mistake actually costs in the real world.
