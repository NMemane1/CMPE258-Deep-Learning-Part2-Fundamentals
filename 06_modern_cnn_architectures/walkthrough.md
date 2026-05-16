# Walkthrough — Modern CNN Architectures & Transfer Learning

My recording script for the video. The assignment says keep this one
high-level, so I'll explain the *ideas* behind each architecture rather than
every implementation detail.

## What this notebook is about

This picks up where the CNN fundamentals notebook ended. Once you can build a
basic CNN, the next question is: how do you go really deep without it breaking,
and how do you avoid training from scratch every time? That's ResNet,
EfficientNet, and transfer learning.

## Chapter 1 — The vanishing gradient problem (code cells 1-2)

Cell 1 is setup. Cell 2 shows the problem: naively stacking more layers actually
makes a network *worse*, not better. During backprop the gradient gets
multiplied through every layer, and in a very deep net it shrinks toward zero
before it reaches the early layers — so those layers never learn. This is the
wall that ResNet was built to break.

## Chapter 2 — ResNet and the residual connection (code cells 3-6)

Cells 3-6 are the core of the notebook. The ResNet idea is beautifully simple:
add a **skip connection** that lets the input jump past a block and get added to
its output. So each block only has to learn the *residual* — the small change —
instead of the whole transformation. The skip connection also gives the gradient
a clean shortcut straight back to the early layers, which kills the vanishing
gradient problem. This one trick is what made 50-, 100-, even 1000-layer
networks trainable. I'll spend the most video time here.

## Chapter 3 — Advanced building blocks (code cells 7-8)

Cells 7-8 cover later refinements at a high level: **bottleneck blocks** (use
1x1 convolutions to cut computation), **depthwise separable convolutions** (the
trick behind MobileNet — same idea, far fewer multiplications), and
**attention/squeeze-and-excitation** blocks that let the network reweight its
own channels.

## Chapter 4 — EfficientNet and compound scaling (code cells 9-10)

Cells 9-10 explain EfficientNet. The question it answers: when you want a bigger
model, do you make it deeper, wider, or feed it higher-resolution images?
EfficientNet's answer is **compound scaling** — scale all three together in a
balanced ratio. That gives better accuracy for the same compute budget than
scaling any one dimension alone.

## Chapter 5 — Transfer learning (code cells 11-13)

Cells 11-13 are the practical payoff. Transfer learning means taking a network
already trained on millions of images (ImageNet) and reusing it for your own,
much smaller dataset. The two modes: **feature extraction** — freeze the
pretrained layers, train only a new final classifier — and **fine-tuning** —
also let some of the pretrained layers update gently. I explain why this works:
the early layers learned generic features (edges, textures) that are useful for
almost any image task.

## Chapter 6 — Fine-tuning strategies (code cells 14-17)

Cells 14-17 cover doing it well: use a smaller learning rate for the pretrained
layers than for the new ones, unfreeze layers gradually, and watch for
overfitting since your dataset is small. High-level in the video — I'll describe
the strategy, not every line.

## Summary (code cell 18)

Cell 18 recaps: use residual connections to go deep, scale models in a balanced
way, and almost always start from a pretrained model instead of training from
scratch.

## How I'll close the video

One line: modern CNNs are mostly two ideas — skip connections so depth stops
hurting, and transfer learning so you never have to start from zero.
