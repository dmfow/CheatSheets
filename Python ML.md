

## Multi GPU
Not tested yet

#### Tensorflow (Mirrored Strategy)
https://www.tensorflow.org/guide/distributed_training
https://www.tensorflow.org/tutorials/distribute/multi_worker_with_keras
```python
mirrored_strategy = tf.distribute.MirroredStrategy()
# OR define the GPUs
mirrored_strategy = tf.distribute.MirroredStrategy(devices=["/gpu:0", "/gpu:1"])

with mirrored_strategy.scope():
    model = Model()
    model.compile(loss = …, optimizer = …, …)
    model.fit(x_train, y_train, batch_size, epochs, …)
    
``

#### PyTorch (Data parallel)
https://pytorch.org/tutorials/beginner/blitz/data_parallel_tutorial.html
```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model = nn_model()
model = nn.DataParallel(model)
model.to(device)
gpu_data = torch.tensor(data).cuda()

```
