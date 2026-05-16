# Walkthrough — Hyperparameter Tuning for Deep Learning

My recording script for the video. Follows the notebook in order.

## What this notebook is about

Hyperparameter tuning is the part of deep learning that nobody warns you about:
the model architecture is only half the job, the other half is picking the knob
settings — learning rate, batch size, number of layers, dropout — that you do
*not* learn from data. This notebook walks through every standard way to search
for those settings, from "guess and check" up to Bayesian optimization.

## Part I — Parameters vs hyperparameters (code cells 1-2)

Cell 1 installs and imports everything (including Optuna, which we use later).
Cell 2 makes the core distinction concrete: **parameters** are the weights the
network learns by itself during training; **hyperparameters** are the choices
*you* make before training starts. I demo how changing one hyperparameter swings
the result, so the audience sees why this matters.

## Part II — The hyperparameters that actually matter (code cell 3)

Cell 3 visualizes the search space. I list the big ones in priority order:
learning rate first (it matters more than everything else combined), then batch
size, network width/depth, regularization. The point of the plot is to show how
fast the space explodes once you have several knobs.

## Part III — The learning rate finder (code cell 4)

This is a clever trick: instead of guessing the learning rate, you train for a
few steps while exponentially increasing it, and plot loss against rate. The
spot just before the loss explodes is your good learning rate. Cell 4 implements
and plots it. Good moment in the video to point at the curve and say "pick here."

## Part IV — Grid search (code cells 5-6)

Grid search is the brute-force method: list a few values for each
hyperparameter, try every combination. Cell 5 runs it, cell 6 plots the results
as a heatmap. I explain the catch — the number of runs multiplies with every
knob you add, so grid search dies fast in high dimensions (the "curse of
dimensionality").

## Part V — Random search (code cells 7-8)

Cell 7 has the key visual of the whole notebook: grid vs random search side by
side. The insight from Bergstra & Bengio (2012) is that random search finds good
values *faster* because most hyperparameters barely matter — random sampling
spends less effort on the unimportant ones. Cell 8 runs random search so you can
compare.

## Part VI — Bayesian optimization (concept)

This section is mostly explanation, no heavy code. The idea: instead of
searching blindly, build a probabilistic model of "which settings look
promising" and use it to pick the next thing to try. It learns from every run.

## Part VII — Optuna in practice (code cells 9-10)

Cell 9 is the real-world payoff: Optuna is the modern library that does Bayesian
optimization for you. I show defining an `objective` function, creating a study,
and calling `optimize`. Cell 10 plots the optimization history and which
hyperparameters mattered most. This is the part viewers should actually copy
into their own projects.

## Part VIII — Best practices (no code)

I close on the practical advice: tune learning rate first, use a small data
subset for early experiments, don't tune on the test set, and stop when returns
flatten. The honest message: smart search beats exhaustive search, and exhaustive
search beats random guessing.
