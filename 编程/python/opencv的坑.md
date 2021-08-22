#### cv2.resize()

- np.shape默认是将对象作为张量处理，格式为(行数，列数，通道数)
- cv2.resize默认将对象当做图像处理，格式为（宽，高）

```python
img_resized=cv2.resize(img,(200,150))
print(img_resized.shape)
>> (150, 200, 3)
```

