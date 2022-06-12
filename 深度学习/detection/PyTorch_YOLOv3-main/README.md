# PyTorch_YOLOv3
在小batch size 的情况，如batch size=8，可能会出现nan的问题，经过其他伙伴的调试，
在batch size=8时，可以把学习率lr跳到2e-4，兴许就可以稳定炼丹啦！ 我自己训练的时候，batch size
设置为16或32，比较大，所以训练稳定。

## 实验结果

官方的YOLOv3:

<table><tbody>
<tr><th align="left" bgcolor=#f8f8f8> 模型 </th>     <td bgcolor=white> 输入尺寸 </td><td bgcolor=white> AP </td><td bgcolor=white> AP50 </td><td bgcolor=white> AP75 </td><td bgcolor=white> AP_S </td><td bgcolor=white> AP_M </td><td bgcolor=white> AP_L </td></tr>

<tr><th align="left" bgcolor=#f8f8f8> YOLOv3</th><td bgcolor=white> 320 </td><td bgcolor=white> 28.2 </td><td bgcolor=white> 51.5 </td><td bgcolor=white> - </td><td bgcolor=white> - </td><td bgcolor=white> - </td><td bgcolor=white> - </td></tr>

<tr><th align="left" bgcolor=#f8f8f8> YOLOv3</th><td bgcolor=white> 416 </td><td bgcolor=white> 31.0 </td><td bgcolor=white> 55.3 </td><td bgcolor=white> - </td><td bgcolor=white> - </td><td bgcolor=white> - </td><td bgcolor=white> - </td></tr>

<tr><th align="left" bgcolor=#f8f8f8> YOLOv3</th><td bgcolor=white> 608 </td><td bgcolor=white> 33.0 </td><td bgcolor=white> 57.0 </td><td bgcolor=white> 34.4 </td><td bgcolor=white> 18.3 </td><td bgcolor=white> 35.4 </td><td bgcolor=white> 41.9 </td></tr>
</table></tbody>

我们自己的 YOLOv3:

<table><tbody>
<tr><th align="left" bgcolor=#f8f8f8> 模型 </th>     <td bgcolor=white> 输入尺寸 </td><td bgcolor=white> AP </td><td bgcolor=white> AP50 </td><td bgcolor=white> AP75 </td><td bgcolor=white> AP_S </td><td bgcolor=white> AP_M </td><td bgcolor=white> AP_L </td></tr>

<tr><th align="left" bgcolor=#f8f8f8> YOLOv3</th><td bgcolor=white> 320 </td><td bgcolor=white> 33.1 </td><td bgcolor=white> 54.1 </td><td bgcolor=white> 34.5 </td><td bgcolor=white> 12.1 </td><td bgcolor=white> 34.5 </td><td bgcolor=white> 49.6 </td></tr>

<tr><th align="left" bgcolor=#f8f8f8> YOLOv3</th><td bgcolor=white> 416 </td><td bgcolor=white> 36.0 </td><td bgcolor=white> 57.4 </td><td bgcolor=white> 37.0 </td><td bgcolor=white> 16.3 </td><td bgcolor=white> 37.5 </td><td bgcolor=white> 51.1 </td></tr>

<tr><th align="left" bgcolor=#f8f8f8> YOLOv3</th><td bgcolor=white> 608 </td><td bgcolor=white> 37.6 </td><td bgcolor=white> 59.4 </td><td bgcolor=white> 39.9 </td><td bgcolor=white> 20.4 </td><td bgcolor=white> 39.9 </td><td bgcolor=white> 48.2 </td></tr>
</table></tbody>

## 命令
```
# 训练
python train.py --cuda -ms -d coco 
# 可视化结果
python test.py --cuda -d coco-val --trained_model 权重文件路径
python test.py --cuda -d coco-val --trained_model ./backbone/weights/yolov3_10.pth
# 计算AP
python eval.py --cuda -d coco-test --trained_model 权重文件路径 -size 输入图像尺寸
python eval.py --cuda -d coco-test --trained_model ./backbone/weights/yolov3_10.pth
# 计算AP
# 
```
获得一个名为yolov3.json的文件，然后按照COCO官网所要求的格式将其重命名为：[detections]_[test-dev2017]_[yolov3]_results.json然后将其添加至同名的zip文件中：[detections]_[test-dev2017]_[yolov3]_results.zip将此压缩包上传至官网的测试界面，然后等待测试结果即可。

