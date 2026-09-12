# Multiclass Semantic Segmentation Using U-Net

This project demonstrates **multiclass semantic segmentation** on the **Semantic Segmentation Drone Dataset** using the **U-Net architecture**.

## Dataset Split

The dataset contains a total of **400 images**, which were divided into three mutually exclusive sets:

* **Training:** 352 images (88%)
* **Validation:** 20 images (5%)
* **Testing:** 28 images (7%)

It was ensured that no image appeared in more than one set. Therefore, the test set consisted entirely of images that were unseen by the model during the training process.

## Model Training

The model was trained for a total of **165 epochs**. During training, the model parameters were saved whenever a lower validation loss was achieved.

The latest best model, with the lowest validation loss of **0.402832955121994**, was obtained at **epoch 124**. This best model was subsequently used for evaluation on the test set.

The U-Net model contains **5 output channels** in its final convolutional layer, corresponding to the five semantic classes in the dataset.

### Semantic Classes

| Class | Meaning  | Mask Color |
| ----- | -------- | ---------- |
| 0     | Obstacle | Purple     |
| 1     | Water    | Blue       |
| 2     | Nature   | Lawn green |
| 3     | Moving   | Deep pink  |
| 4     | Landable | Gray       |

## Optimization and Loss

* **Optimizer:** Adam
* **Learning rate:** `1e-3`
* **Loss function:** CrossEntropyLoss

## Image Preprocessing

Each image, regardless of whether it belonged to the training, validation, or test set, was:

1. Resized to **224 × 224** pixels.
2. Converted to a floating-point tensor.
3. Divided by `255.0` to scale pixel values to `[0, 1]`.
4. Normalized using the following ImageNet mean and standard deviation:

```python
transforms.Normalize(
    [0.485, 0.456, 0.406],
    [0.229, 0.224, 0.225]
)
```

Each input image has **3 channels** and therefore has the shape:

```text
(3, 224, 224)
```

The corresponding segmentation mask has the shape:

```text
(224, 224)
```

where each pixel contains an integer class ID from `0` to `4`.

## Test Results

The test-set predictions are available in the [`results`](./results) directory.

Each test visualization contains:

1. Original image
2. Predicted semantic segmentation mask
3. Ground-truth semantic segmentation mask

## Dataset

The dataset is available on Kaggle:

https://www.kaggle.com/datasets/santurini/semantic-segmentation-drone-dataset
