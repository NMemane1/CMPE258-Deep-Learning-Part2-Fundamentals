# Walkthrough — Activation Functions for Deep Learning

My recording script for the video. Follows the notebook in order.

## What this notebook is about

An activation function is the small non-linear step applied after each layer of
a network. It sounds minor, but without it a deep network collapses into a
single linear layer — no matter how many layers you stack. This notebook proves
that, then walks through every activation function worth knowing and when to use
each one.

## Part I — Why activation functions matter (code cells 1-2)

Cell 1 imports the stack. Cell 2 is the key demo: it shows that stacking linear
layers with no activation is mathematically identical to one linear layer. So a
"deep" network with no activations can only ever draw a straight line — it can't
learn anything curved. That's the whole reason activations exist: they inject
the non-linearity. I make sure to land this point clearly because everything
else builds on it.

## Part II — Classic activations (code cell 3)

Cell 3 implements and plots **Sigmoid** and **Tanh**. Sigmoid squashes any input
to a 0-1 range; Tanh squashes to -1 to 1. I explain their fatal flaw: at the
extremes the curve goes flat, so the gradient becomes nearly zero. In a deep
network those tiny gradients multiply together and shrink to nothing — the
**vanishing gradient problem** — and the early layers stop learning.

## Part III — The ReLU revolution (code cell 4)

Cell 4 plots **ReLU**: just `max(0, x)`. It's almost too simple, but it solved
the vanishing gradient problem for positive inputs and made truly deep networks
trainable in the 2010s. The cell also shows ReLU's own weakness — the **dying
ReLU problem**: a neuron stuck in the negative region outputs zero forever and
never recovers.

## Part IV — ReLU variants (code cell 5)

Cell 5 implements the fixes for dying ReLU: **Leaky ReLU** (small slope on the
negative side instead of flat zero), **PReLU** (that slope is learned, not
fixed), and **ELU**. The common idea: let a little signal through on the
negative side so neurons can come back to life.

## Part V — Modern activations (code cell 6)

Cell 6 covers **GELU** and **Swish/SiLU** — smooth curves that behave like ReLU
but without the hard corner at zero. GELU is what powers modern transformers
(BERT, GPT). I explain that the smoothness gives slightly nicer gradients.

## Part VI — Output layer activations (code cell 7)

This is a separate job from hidden-layer activations. Cell 7 visualizes:
**Sigmoid** for binary classification (one probability), **Softmax** for
multi-class (a set of probabilities that add up to 1), and **no activation** for
regression (you want the raw number). I stress that mixing these up is a common
beginner bug.

## Part VII — Practical guide (no code)

A decision guide. Short version: use ReLU (or GELU for transformers) in the
hidden layers, and match the output activation to your task — sigmoid, softmax,
or nothing.

## Part VIII — Hands-on comparison (code cells 8-9)

Cell 8 builds a dataset and cell 9 trains the same network with different
activations, plotting the results together. This is the payoff — you can see
ReLU-family functions train faster and reach lower loss than sigmoid/tanh on a
deep network.

## How I'll close the video

One line: activations are what make a network "deep" in any meaningful sense —
pick ReLU or GELU for hidden layers, and let the task decide the output
activation.
