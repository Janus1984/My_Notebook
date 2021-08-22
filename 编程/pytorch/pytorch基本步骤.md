### 1. 数据处理

对于数据处理，最为简单的⽅式就是将数据组织成为⼀个。但许多训练需要⽤到mini-batch，直接组织成Tensor不便于我们操作。pytorch为我们提供了**Dataset**和**Dataloader**两个类来方便的构建。

 **`torch.utils.data.Dataset`**

继承Dataset类需要override以下方法：

```python
from troch.utils.data import Dataset

class trainDataset(Dataset):
    def __init__(self):
        ## constructor
        
    def __gititem__(self, index):
        ## 获取第index号的数据和标签
        
    def __len__(self):
        ## 获得数据量
```

**`torch.utils.data.DataLoader`**

```python
torch.utils.data.DataLoader(dataset, batch_size=1, shuffle=False)
```

DataLoader Batch。如果选择shuffle = True，每⼀个epoch 后，mini-Batch batch_size 常⻅的使⽤⽅法如下：
```python
dataLoader = DataLoader(dataset, shuffle=True, batch_size=32)
for i, data in enumerate(dataLoader, 0):
	x, y = data #同时获取数据和标签
```



### 2. 模型构建

所有的模型都需要继承`torch.nn.Module` ， 需要实现以下⽅法：

```python
class MyModel(torch.nn.Module):
    def __init__(self):
        super(MyModel,self).__init__()
        pass
    def forward(self, x):
        pass
```

其中`forward() `⽅法是前向传播的过程。在实现模型时，我们不需要考虑反向传播。



### 3. 定义代价函数和优化器

```python
criterion = torch.nn.BCELoss(reduction='sum') #代价函数
optimizer = torch.optim.Adam(model.parameters(), lr=0.0001, betas=(0.9,0.999),eps=1e-08, weight_decay=0, amsgrad=False) #优化器
```

这部分根据⾃⼰的需求去参照doc



### 4.构建训练过程

```python
def train(epoch): #一个epoch的训练
    for i, data in enumerate(dataLoader, 0):
        x, y = data #取出minibatch数据和标签
        y_pred = model(x) #前向传播
        loss = criterion(y_pred, y) #计算代价函数
        optimizer.zero_grad() #清零梯度准备计算
        loss.backward() #反向传播
        optimizer.step() #更新训练参数
```

