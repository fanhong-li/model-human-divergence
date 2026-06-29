# Training Process

## Task

The evaluation uses Physion binary contact prediction. Each stimulus is observed for the same temporal window as the human benchmark, and the probe predicts whether two designated objects will come into contact.

## Frozen Encoders

The main paper evaluates three frozen ViT-L encoders:

- V-JEPA2
- VideoMAEv2
- DINOv2

The encoders are not fine-tuned. Only lightweight task probes are trained.

## Input Protocol

- 8 input frames per stimulus.
- Fractional frame step 5.75.
- Approximately 1.5 seconds of temporal coverage, matching the human observation window.
- Binary contact/no-contact target.

## Probe Protocol

For each frozen encoder:

- use the same end-to-end attentive probe architecture;
- train probes with 8 random seeds;
- use identical hyperparameter grids across encoders;
- train for 20 epochs;
- select the best head by training accuracy, following the standard Physion probe-selection protocol.

The multiple random seeds are treated as a model population, enabling comparison with the human rater population rather than relying on a single probe instance.

## Evaluation

For each model seed, predictions are collected over all 1,200 Physion test samples. The paper reports:

- seed-mean test accuracy;
- model-human disagreement;
- model-human Cohen's kappa;
- comparison to human majority vote and human-human agreement.

The analysis code used for the full distributional evaluation is under release review and will be added separately.

