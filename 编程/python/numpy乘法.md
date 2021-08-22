- 当进行**标量**的乘法运算或者**element-wise**时，可以通过`np.multiply()`或者`*`
- 当进行**向量**的内积运算时，可以通过`np.dot()`
- 当进行**矩阵**的乘法运算时，可以通过`np.matmul()`或者`@`



#### 1. dot运算

如果参与运算的是两个一维数组，那么得到的结果是两个数组的内积（inner product）：

```python
a = np.array([1,2,3])
b = np.array([1,2,3])
np.dot(a,b)
>> 14
```

如果参与运算的是两个二维数组，那么得到的结果是矩阵乘积（matrix multiplication），但是官方更推荐使用`np.matmul()`和`@`用于乘法矩阵。

```python
A = np.array([1,2,3],
             [4,5,6])
B = np.array([[1,2],
              [3,4],
              [5,6]])
np.dot(A,B) 
>>[[22,28],
   [49,64]]
```

#### 2. `np.multiply()`和`*`

`np.multply()`和`*`方法是针对标量运算，当参与运算的是两个数组时，得到的结果是两个数组进行对应位置的乘积（element-wise product），输出的结果与参与的数组或者矩阵的大小一致。

```python
A = np.array([[1,2,3],
              [4,5,6]])
B = np.array([[1,2,3],
              [4,5,6]])
a = np.array([1,2,3])
b = np.array([1,2,3])

np.multiply(A,B)
>> [[ 1, 4, 9 ],
    [16,25,36]]

np.multiply(a,b)
>> [1,4,9]
```

#### 3. `np.matmul()`和`@`

matmul是matrix multiply的缩写，所以即是专门用于矩阵乘法的函数。另外，`@`运算方法和`matmul()`则是一样的作用，相当于简便写法。

```python
A = np.array([[1,2,3],
              [4,5,6]])
B = np.array([[1,2],
              [3,4],
              [5,6]])

np.matmul(A,B)
>>[[22,28],
   [49,64]]

A@B
>>[[22,28],
   [49,64]]
```

