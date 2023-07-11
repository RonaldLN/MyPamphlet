## 1

[(7条消息) YOLOv7保姆级教程（个人踩坑无数）----训练自己的数据集_yolov7代码下载_AmbitionToFree的博客-CSDN博客](https://blog.csdn.net/weixin_55749226/article/details/128480595)

---

## 2

detect.py权重在github官网`Testing`下下载

[(8条消息) YOLOv7（目标检测）入门教程详解---检测，推理，训练_yolov目标检测_螺丝工人的博客-CSDN博客](https://blog.csdn.net/weixin_64524066/article/details/126845366)

可以在`detect.py`中修改

```python
    parser.add_argument('--weights', nargs='+', type=str, default='weights/yolov7.pt', help='model.pt path(s)')
    # parser.add_argument('--weights', nargs='+', type=str, default='yolov7.pt', help='model.pt path(s)')
```

或直接命令行运行指令

```bash
python detect.py --weights weights/yolov7.pt --source inference/images 
```

---

## 3

`split.py`文件放在yolov7根目录下

## 4

gpu只有一个就只用`0`

## 5

 [WinError 1455] 页面文件太小，无法完成操作。

[(8条消息) 多种方法彻底解决pycharm中: OSError: [WinError 1455\] 页面文件太小，无法完成操作 的问题_pycharm运行出现oserror_孤柒「一起学计算机」的博客-CSDN博客]](https://blog.csdn.net/weixin_43959833/article/details/116669523)

[(8条消息) YOLOV7:OSError: [WinError 1455\] 页面文件太小，无法完成操作的 最终解决方案_oserror: [winerror 1455] 页面文件太小,无法完成操作_我追逐落日不休，却不知你在等我回头的博客-CSDN博客](https://blog.csdn.net/xty123abc/article/details/125864462)

以及，调整`--batch-size`大小，

```bash
python train.py --weights weights/yolov7_training.pt --cfg cfg/training/yolov7-Helmet.yaml --data data/Helmet.yaml --device 0 --batch-size 2
```

