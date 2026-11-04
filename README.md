# waste-classifier
# Organic vs. Recyclable Waste Classifier

An image classifier that sorts waste photos into organic (O) or recyclable (R), built with transfer learning in TensorFlow/Keras on Google Colab. This is a learning project: I'm new to programming and built it to understand how image classification works.

## Dataset
Public waste classification dataset (https://www.kaggle.com/code/stpeteishii/waste-image-classify-fastai/input): about 22,500 training images and 2,500 test images, split into organic and recyclable. The dataset is not included here because of its size.

## Approach
- Reused a pretrained MobileNetV2 (trained on ImageNet) as a frozen feature extractor
- Trained a small classification layer on top for 3 epochs
- Evaluated on 2,513 held-out test images the model never saw during training

## Results

| Version | Change | Test accuracy | Organic called recyclable | Recyclable called organic |
|---|---|---|---|---|
| 1 | Baseline | 89.97% | 29 | 223 |
| 2 | Added data augmentation (flip, rotation, brightness) | 89.89% | 40 | 214 |

Always guessing the majority class would score about 56%.

## What I found
- Augmentation made no meaningful difference to accuracy.
- The model is biased toward "organic": it catches about 98% of organic photos but only about 80% of recyclable ones.
- Many mistakes involve objects like drinking straws and curtains. Some labels in the dataset are ambiguous or inconsistent, which limits how well any model can do.
- The photos look like clean internet product images, so performance on real-world photos of waste would likely be worse. I haven't tested that.

## Next steps
- Fine-tune the last layers of MobileNetV2
- Test on my own photos of real items

## Tools
Python, TensorFlow/Keras, Google Colab
