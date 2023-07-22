yolov8官方github仓库

[ultralytics/README.zh-CN.md at main · ultralytics/ultralytics · GitHub](https://github.com/ultralytics/ultralytics/blob/main/README.zh-CN.md)

yolov8官方使用文档

[Home - Ultralytics YOLOv8 Docs](https://docs.ultralytics.com/)

## 1

(Windows)RuntimeError解决方案

[Windows使用PyTorch遇到RuntimeError: Unable to find a valid cuDNN algorithm to run convolution的解决方案 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/590817058)

## 2

```bash
RuntimeError: Dataset 'data\Helmet.yaml' error  
Dataset 'data\Helmet.yaml' images not found , missing paths ['C:\\Users\\Administrator\\datasets\\data\\datasets\\Helmet\\val_list.txt']
Note dataset download directory is 'C:\Users\Administrator\datasets'. You can update this in 'C:\Users\Administrator\AppData\Roaming\Ultralytics\settings.yaml'
```

修改，

可以改成相对路径

```yaml
datasets_dir: ..\
```

## 3

```bash
RuntimeError: 
            Attempt to start a new process before the current process
            has finished its bootstrapping phase.
            This probably means that you are on Windows and you have
            forgotten to use the proper idiom in the main module:
                if __name__ == '__main__':
                    freeze_support()
                    ...
            The "freeze_support()" line can be omitted if the program
            is not going to be frozen to produce a Windows executable.
```

操作：

```python
model = YOLO("yolov8n.pt")  # 加载预训练模型（建议用于训练）

if __name__ == '__main__': # 添加__main__
    # 使用模型
    model.train(data="data/Helmet.yaml", epochs=3, batch=2[, name="Name"])  # 训练模型
```

[python - YOLOv8 : RuntimeError: An attempt has been made to start a new process before the current process has finished its bootstrapping phase - Stack Overflow](https://stackoverflow.com/questions/75111196/yolov8-runtimeerror-an-attempt-has-been-made-to-start-a-new-process-before-th)

## 4

MemoryError 调整 `batch=`

[About Memory Error while Training yolov8x-seg · Issue #2916 · ultralytics/ultralytics (github.com)](https://github.com/ultralytics/ultralytics/issues/2916)

## 5

页面大小不够：

[python - How to efficiently run multiple Pytorch Processes / Models at once ? Traceback: The paging file is too small for this operation to complete - Stack Overflow](https://stackoverflow.com/questions/64837376/how-to-efficiently-run-multiple-pytorch-processes-models-at-once-traceback)

```bash
OSError: [WinError 1455] The paging file is too small for this operation to complete. Error loading "...\cusolver64_xx.dll    ...\cudnn_adv_infer64_8.dll" or one of its dependencies.
```

新建文件 `fixNvPe.py`

[Python Script to disable ASLR and make nv fatbins read-only to reduce memory commit (github.com)](https://gist.github.com/cobryan05/7d1fe28dd370e110a372c4d268dcb2e5)

??? quote "fixNvPe.py"

    ```python
    # Simple script to disable ASLR and make .nv_fatb sections read-only
    # Requires: pefile  ( python -m pip install pefile )
    # Usage:  fixNvPe.py --input path/to/*.dll
    
    import argparse
    import pefile
    import glob
    import os
    import shutil
    
    def main(args):
        failures = []
        for file in glob.glob( args.input, recursive=args.recursive ):
            print(f"\n---\nChecking {file}...")
            pe = pefile.PE(file, fast_load=True)
            nvbSect = [ section for section in pe.sections if section.Name.decode().startswith(".nv_fatb")]
            if len(nvbSect) == 1:
                sect = nvbSect[0]
                size = sect.Misc_VirtualSize
                aslr = pe.OPTIONAL_HEADER.IMAGE_DLLCHARACTERISTICS_DYNAMIC_BASE
                writable = 0 != ( sect.Characteristics & pefile.SECTION_CHARACTERISTICS['IMAGE_SCN_MEM_WRITE'] )
                print(f"Found NV FatBin! Size: {size/1024/1024:0.2f}MB  ASLR: {aslr}  Writable: {writable}")
                if (writable or aslr) and size > 0:
                    print("- Modifying DLL")
                    if args.backup:
                        bakFile = f"{file}_bak"
                        print(f"- Backing up [{file}] -> [{bakFile}]")
                        if os.path.exists( bakFile ):
                            print( f"- Warning: Backup file already exists ({bakFile}), not modifying file! Delete the 'bak' to allow modification")
                            failures.append( file )
                            continue
                        try:
                            shutil.copy2( file, bakFile)
                        except Exception as e:
                            print( f"- Failed to create backup! [{str(e)}], not modifying file!")
                            failures.append( file )
                            continue
                    # Disable ASLR for DLL, and disable writing for section
                    pe.OPTIONAL_HEADER.DllCharacteristics &= ~pefile.DLL_CHARACTERISTICS['IMAGE_DLLCHARACTERISTICS_DYNAMIC_BASE']
                    sect.Characteristics = sect.Characteristics & ~pefile.SECTION_CHARACTERISTICS['IMAGE_SCN_MEM_WRITE']
                    try:
                        newFile = f"{file}_mod"
                        print( f"- Writing modified DLL to [{newFile}]")
                        pe.write( newFile )
                        pe.close()
                        print( f"- Moving modified DLL to [{file}]")
                        os.remove( file )
                        shutil.move( newFile, file )
                    except Exception as e:
                        print( f"- Failed to write modified DLL! [{str(e)}]")
                        failures.append( file )
                        continue
    
        print("\n\nDone!")
        if len(failures) > 0:
            print("***WARNING**** These files needed modification but failed: ")
            for failure in failures:
                print( f" - {failure}")







    def parseArgs():
        parser = argparse.ArgumentParser( description="Disable ASLR and make .nv_fatb sections read-only", formatter_class=argparse.ArgumentDefaultsHelpFormatter )
        parser.add_argument('--input', help="Glob to parse", default="*.dll")
        parser.add_argument('--backup', help="Backup modified files", default=True, required=False)
        parser.add_argument('--recursive', '-r', default=False, action='store_true', help="Recurse into subdirectories")
    
        return parser.parse_args()


    ###############################
    # program entry point
    #
    if __name__ == "__main__":
        args = parseArgs()
        main( args )
    ```

无依赖安装依赖

```bash
python -m pip install pefile
```

运行命令行

```bash
python fixNvPe.py --input=E:\Programs\Anaconda3\envs\yolov7\lib\site-packages\torch\lib\*.dll
```

## 6

用命令行检测

```bash
yolo predict model=yolov8n.pt source='bus.jpg'
```

代码在：

[Python - Ultralytics YOLOv8 Docs](https://docs.ultralytics.com/usage/python/)

-   调用相机 `source="0"`
-   检测整个文件夹的图片/视频，`source=".../folder"`
-   检测单个图片/视频（可以直接写路径，或者用类加载，三种方法）

>   -   `show=`展示图片
>   -   `save=`保存图片(到runs/detect/[predictxx]文件夹中)
>   -   `name=`保存的文件夹的名称

```python
from ultralytics import YOLO
from PIL import Image
import cv2

model = YOLO("model.pt")
# accepts all formats - image/dir/Path/URL/video/PIL/ndarray. 0 for webcam
results = model.predict(source="0")
results = model.predict(source="folder", show=True) # Display preds. Accepts all YOLO predict arguments

# from PIL
im1 = Image.open("bus.jpg")
results = model.predict(source=im1, save=True)  # save plotted images

# from ndarray
im2 = cv2.imread("bus.jpg")
results = model.predict(source=im2, save=True, save_txt=True)  # save predictions as labels

# from list of PIL/ndarray
results = model.predict(source=[im1, im2])

```

支持的文件类型

[Predict - Ultralytics YOLOv8 Docs](https://docs.ultralytics.com/modes/predict/#inference-sources)

参数的作用

[Predict - Ultralytics YOLOv8 Docs](https://docs.ultralytics.com/modes/predict/#inference-arguments)

## 7

`.yaml`文件里面的标签要与`labels.txt`里面的顺序一致

## 8

v8 `.yaml` 文件示例：

```yaml
# Train/val/test sets as 1) dir: path/to/imgs, 2) file: path/to/imgs.txt, or 3) list: [path/to/imgs1, path/to/imgs2, ..]
path: ../datasets/coco8  # dataset root dir
train: images/train  # train images (relative to 'path') 4 images
val: images/val  # val images (relative to 'path') 4 images
test:  # test images (optional)

# Classes (80 COCO classes)
names:
  0: person
  1: bicycle
  2: car
  ...
  77: teddy bear
  78: hair drier
  79: toothbrush
```

>   [Object Detection Datasets Overview - Ultralytics YOLOv8 Docs](https://docs.ultralytics.com/datasets/detect/)

其中 `train:` `val:` 之后的内容有三种写法，

1.   文件夹路径
2.   txt文件路径，txt文件内为各个图片的路径
3.   列表形式的图片路径

## 9

如果detect时使用某个pt模型报错，有可能是因为 训练该模型时使用的ultralytics版本 比 本机安装的版本 新，使用了旧版本 `requirements.txt` 中未安装的包，因此更新ultralytics包即可

