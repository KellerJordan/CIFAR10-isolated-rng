# CIFAR-isolated-rng

This repo provides a CIFAR-10 training script with granular control over sources of randomness.

We split the random seed into three parts:
* The `model_seed`, which controls the model initialization.
* The `order_seed`, which controls the order that data appears during training.
* The `aug_seed`, which controls random image augmentations. This is set so that with a fixed `aug_seed`, the model will see the same set of augmented images in each epoch, with only their order being controlled by `order_seed`.

## Performance
* With 8x NVIDIA A100s, I get 400 50-epoch trainings/hour
* The mean test-set accuracy is 94.11% (+/- 0.01%). The stddev is 0.153% (+/- 0.003%).

## Commands
To do a single training:
```
python train.py --model_seed=42 --order_seed=42 --aug_seed=42
>>> correct=9419
```
(Your results for this seed may differ depending on torch version, hardware, etc., but should be the same every run.)

To run many trainings over a sweep of seeds:
```
python many_train.py
```

