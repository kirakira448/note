#### 函数cv2.dnn.blobFromImage(image[, scalefactor[, size[, mean[, swapRB[, crop[, ddepth]]]]]])

**作用：**
对图像进行预处理，包括减均值，比例缩放，裁剪，交换通道等，返回一个4通道的blob(blob可以简单理解为一个N维的数组，用于神经网络的输入)

**参数：**
- image:输入图像（1、3或者4通道）

*可选参数*

- scalefactor:图像各通道数值的缩放比例
- size:输出图像的空间尺寸,如size=(200,300)表示高h=300,宽w=200
- mean:用于各通道减去的值，以降低光照的影响(e.g. image为bgr3通道的图像，mean=[104.0, 177.0, 123.0],表示b通道的值-104，g-177,r-123)
- swapRB:交换RB通道，默认为False.(cv2.imread读取的是彩图是bgr通道)
- crop:图像裁剪,默认为False.当值为True时，先按比例缩放，然后从中心裁剪成size尺寸
- ddepth:输出的图像深度，可选CV_32F 或者 CV_8U.

**注意：**

  1. 当同时进行scalefactor,size,mean,swapRB操作时，优先按swapRB交换通道，其次按scalefactor比例缩放，然后按mean求减，最后按size进行resize操作

  2. 当进行减均值操作时，ddepth不能选取CV_8U，否则报错
  3. 当crop=True时，先等比例缩放，直至**宽高尺寸一个等于对应的size尺寸，另一个大于或者等于对应的size尺寸**，然后再从中心进行裁剪

 **返回：**

Blob（Binary Large Object）,4维的数组