# Walkthrough — Convolutional Neural Networks from First Principles

My recording script for the video. Follows the notebook in order.

## What this notebook is about

CNNs are the architecture that made computer vision work. This notebook builds
one from the ground up — starting with the raw convolution operation, then
layers, then pooling, then a full image classifier trained on CIFAR-10. It's all
in PyTorch.

## Chapter 1 — The convolution operation (code cells 1-4)

Cell 1 is setup/imports. Then I explain why we don't just use a fully connected
network on images: a small image flattened into a vector is enormous, the
network would have millions of weights, and it would have to relearn the same
pattern separately in every corner of the image.

CNNs fix this with three ideas — **local connectivity** (each neuron looks at a
small patch), **parameter sharing** (the same filter slides across the whole
image), and **translation invariance** (a cat is a cat wherever it appears).
Cells 2-4 implement convolution by hand: a small filter slides over the image,
and at each position it multiplies and sums. I show a filter detecting edges so
the audience sees convolution is just pattern-matching.

## Chapter 2 — CNN layers in PyTorch (code cells 5-7)

Cells 5-7 swap the hand-built version for the real thing: `nn.Conv2d`. I explain
the arguments — in/out channels, kernel size, stride, padding — and the **output
size formula** so viewers can predict the shape of every layer. Point out how
the number of channels grows while the spatial size shrinks as you go deeper.

## Chapter 3 — Pooling (code cells 8-9)

Cells 8-9 cover pooling — downsampling the feature maps. **Max pooling** keeps
the strongest signal in each patch, **average pooling** takes the mean. The
purpose: shrink the data, cut computation, and add a bit of robustness to small
shifts.

## Chapter 4 — Building complete CNN architectures (code cells 10-12)

Cells 10-12 assemble the classic pattern: `Conv -> ReLU -> Pool`, repeated, then
flatten and finish with fully connected layers. I describe the **feature
pyramid** idea — early layers catch edges and textures, deeper layers catch
shapes and whole objects.

## Chapter 5 — Training CNNs (code cells 13-18)

This is the longest chapter. Cell 13 onward covers **data augmentation** —
randomly flipping, cropping, rotating the training images so the model sees more
variety and overfits less. Then the full training loop: forward pass, compute
loss, backward pass, optimizer step, repeated over epochs, with accuracy tracked
on a validation set. I narrate one epoch slowly so the loop is clear.

## Chapter 6 — Visualizing what CNNs learn (code cells 19-20)

Cells 19-20 open the black box: they plot the learned filters and the feature
maps a real image produces. Good visual moment — you can literally see the early
layers responding to edges.

## Chapter 7 — A complete image classifier (code cells 21-25)

Cells 21-25 put everything together: a production-style CNN trained on
**CIFAR-10** (10 object categories). I walk through the architecture, the
training run, the accuracy curve, and the final predictions on test images.

## Summary (code cell 26)

Cell 26 recaps the building blocks and the design rules — grow channels as you
go deeper, pool to shrink spatially, use augmentation, end with FC layers.

## How I'll close the video

One line: a CNN is just convolution (find local patterns) plus pooling (shrink
and summarize), stacked deep enough that simple edge detectors compose into
full object detectors.
