

## Multi GPU
Not tested yet

#### Tensorflow (Mirrored Strategy)
```python
mirrored_strategy = tf.distribute.MirroredStrategy()
with mirrored_strategy.scope():
    model = Model()
    model.compile(loss = …, optimizer = …, …)
    model.fit(x_train, y_train, batch_size, epochs, …)
    
# OR define the GPUs
mirrored_strategy = tf.distribute.MirroredStrategy(devices=["/gpu:0", "/gpu:1"])
```

#### PyTorch (Data parallel)
```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model = nn_model()
model = nn.DataParallel(model)
model.to(device)
gpu_data = torch.tensor(data).cuda()

```
