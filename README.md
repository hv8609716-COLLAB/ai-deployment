# AI-deployment

# TensorFlow SavedModel Export & Inference Demo

A simple TensorFlow/Keras project that trains a neural network on custom numeric data, exports the trained model using Keras 3 format, and loads it back using `TFSMLayer` for inference.

## Features

* Train a basic neural network using TensorFlow
* Export model using `model.export()`
* Load exported SavedModel using `TFSMLayer`
* Perform inference on new input values

---

## Project Structure

```bash
project/
│
├── main.py
├── my_save_model/
└── README.md
```

---

## Requirements

Install dependencies:

```bash
pip install tensorflow numpy
```

---

## Code Overview

### Dataset

Input values:

```python
x = [1,2,3,4,5]
```

Target values:

```python
y = [2,4,9,16,25]
```

---

### Model

Single Dense Layer Neural Network:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(units=1, input_shape=[1])
])
```

Compile:

```python
model.compile(
    optimizer="adam",
    loss="mean_squared_error"
)
```

Train:

```python
model.fit(x, y, epochs=50)
```

---

## Export Model

```python
model.export("my_save_model")
```

This creates a TensorFlow SavedModel directory.

---

## Load Exported Model

Since Keras 3 does not directly support loading SavedModel with `load_model()`:

```python
loaded_model = tf.keras.layers.TFSMLayer(
    "my_save_model",
    call_endpoint="serve"
)
```

Run prediction:

```python
result = loaded_model(tf.constant([[6.0]]))
print(result)
```

---

## Example Output

```bash
model saved successfully
tf.Tensor([[prediction]], shape=(1,1), dtype=float32)
```

---

## How to Run

```bash
python main.py
```

---

## Learning Purpose

This project demonstrates:

* TensorFlow basics
* Keras Sequential API
* Model training
* SavedModel export
* Inference using TFSMLayer

---

Made for learning Deep Learning and TensorFlow 🚀
