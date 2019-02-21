# tensorflow_with_keras
An example of using TensorFlow functions with Keras

After searching for a way to use custom TensorFlow functions within Keras (specifically the cohen_kappa function from tensorflow.contrib.metrics), I finally figured out how to do it.  The key is calling `K.get_session().run(tf.local_variables_initializer())` where `K` is `from keras import backend as K`.  Without this, you'll get an error:
```python
FailedPreconditionError: Attempting to use uninitialized value metrics/cohens_kappa/cohen_kappa/pe_row
```

Additionally this serves as an example for how to use Cohen's Kappa (or other tensorflow metrics) as a metric with Keras models.  Cohen's Kappa is generally a better classification metric than accuracy because it takes into account the "no information rate", or random guessing baseline.  Accuracy can look great for something like fraud detection or spam classification, where 99.9% of the cases are negatives.  However, if your majority class in a binary classification is 99.9% of your data, your model needs to have a higher accuracy than 99.9% to be useful.  Otherwise, you might as well be randomly guessing.
