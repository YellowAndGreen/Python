# YOLO

## 问题

### 852.jpg用cv2.imread读取出来为none

```python
# 若为none则使用PIL.Image来读取
img = cv2.imread(path.replace("\\", "\\\\"))  # BGR
if img is None:
    img = Image.open(path)
    img = cv2.cvtColor(np.asarray(img), cv2.COLOR_RGB2BGR)
    assert img is not None, 'Image Not Found ' + path.replace("\\", "\\\\")
```

