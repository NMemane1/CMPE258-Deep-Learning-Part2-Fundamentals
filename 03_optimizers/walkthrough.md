# Walkthrough — Optimizers for Deep Learning

My recording script for the video. Follows the notebook in order.

## What this notebook is about

An optimizer is the algorithm that actually updates the network's weights to
make the loss go down. This notebook builds the whole family from scratch —
starting with plain gradient descent, exposing its weaknesses one by one, and
showing how each famous optimizer (Momentum, AdaGrad, RMSprop, Adam, AdamW) was
invented to fix a specific weakness.

## Part I — Why optimizers matter (code cells 1-6)

Cells 1-2 install and import. Cells 3-6 are all visualization: the optimization
"journey", a 3D loss landscape, a contour plot (bird's-eye view of that
landscape), and a plot of why deep learning optimization is genuinely hard. The
mental model for the video: training is a hiker trying to find the lowest valley
in a foggy mountain range.

## Part II — Gradient descent fundamentals (code cells 7-10)

Cell 7 visualizes what a gradient actually is — the direction of steepest
increase, so we step the opposite way. Cell 8 implements vanilla gradient
descent from scratch; cell 9 draws its path down the landscape. Cell 10 is
important: it shows three learning rates side by side — too small (crawls), too
big (overshoots and diverges), just right. This is the single most important
hyperparameter and the plot makes it obvious.

## Part III — Where vanilla gradient descent breaks (code cells 11-12)

Cell 11 shows the **ravine problem**: when the landscape is a long narrow
valley, plain GD bounces side to side and barely moves forward. Cell 12 shows
**saddle points** — flat spots that aren't minima where the gradient nearly
vanishes and training stalls. These two failures motivate everything that
follows.

## Part IV — Stochastic gradient descent (code cell 13)

Cell 13 contrasts batch GD (use all data per step, accurate but slow) with SGD
(use one sample or a mini-batch, noisy but fast). I explain that the noise is
actually a feature — it helps escape the saddle points from Part III.

## Part V — Momentum (code cell 14)

Cell 14 implements SGD with momentum. The physics analogy: instead of
recomputing direction from zero each step, the optimizer is a heavy ball that
accumulates velocity. It powers through ravines and rolls past small bumps. I
also mention Nesterov momentum — momentum that "looks ahead" before stepping.

## Part VI — Adaptive learning rates (code cells 15-16)

The next idea: give every parameter its *own* learning rate. Cell 15 implements
**AdaGrad**, which shrinks the rate for parameters that update a lot — but it
shrinks too aggressively and eventually stalls. Cell 16 implements **RMSprop**,
which fixes that with a moving average so the rate stops collapsing.

## Part VII — Adam and AdamW (code cell 17)

Cell 17 implements **Adam** — the one everyone actually uses. It combines
momentum (Part V) with adaptive rates (Part VI), so it gets the best of both. I
also explain **AdamW**, which fixes how Adam handles weight decay (regularization)
and is now the default for training transformers.

## Part VIII — Learning rate schedules (code cell 18)

Cell 18 plots schedules — step decay, cosine annealing, warmup. The idea: don't
keep the learning rate fixed; start higher to move fast, then lower it to settle
precisely into the minimum.

## Part IX — Real PyTorch comparison (code cells 19-20)

Cells 19-20 train an actual neural network with several optimizers and plot
their loss curves on the same axes. This is the proof: you can *see* Adam
converge faster and smoother than plain SGD. Then a decision guide — Adam/AdamW
as the safe default, SGD+momentum when you have time to tune and want the best
possible generalization.

## Part X — Modern optimizers (code cell 21)

Cell 21 visualizes sharp vs flat minima and explains **SAM** (Sharpness-Aware
Minimization) — the idea that flat minima generalize better. Closes with a
timeline of how optimizers evolved.

## How I'll close the video

One line: every optimizer in this notebook is just gradient descent plus a fix
for one specific problem — momentum for ravines, adaptivity for uneven gradients,
and Adam bundles both, which is why it's the default.
