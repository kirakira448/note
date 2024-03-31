
## 简介

opencv2人脸检测使用的是detectMultiScale函数，可以检测出图片中的所有人脸，并将vector类型保存各个人脸的位置和大小，用矩形Rect类表示，该函数由分类器的对象进行调用。

detectmultiscale函数可以得到每个人脸的得分。

## 步骤

调用opencv训练好的分类器和自带的检测函数检测人脸人眼等的步骤简单直接：

### 1. 加载分类器

分类器事先要放在工程目录中去。
分类器本来的位置是在*\opencv\sources\data\haarcascades（harr分类器，也有其他的可以用，也可以自己训练）

### 2. 函数检测

调用detectMultiScale()函数检测，
调整函数的参数可以使检测结果更加精确。

### 3. 绘制矩形
把检测到的人脸等用矩形（或者圆形等其他图形）画出来。


## 参数解释

`detectMultiScale(image[, scaleFactor[, minNeighbors[, flags[, minSize[, maxSize]]]]]) -> objects`

*@brief Detects objects of different sizes in the input image. The detected objects are returned as a list of rectangles.*
*此方法的任务是检测不同大小的对象，并返回矩形的列表。*

### image
@param image Matrix of the type CV_8U containing an image where objects are detected.
被检测的图片，需要转换为**灰度图**

### scaleFactor
@param scaleFactor Parameter specifying how much the image size is reduced at each image scale.
scaleFactor 是重点，直接翻译就是“指定每次图像缩小的比例”。

### minNeighbors
@param minNeighbors Parameter specifying how many neighbors each candidate rectangle should have to retain it.
minNeighbors 也是重点，翻译为：指定每个候选矩形有多少个“邻居”。

### flags
@param flags Parameter with the same meaning for an old cascade as in the function cvHaarDetectObjects. It is not used for a new cascade.
flag参数与旧的级联方法cvHaarDetectObjects中一样，新的级联中不用。（没用到这个参数）

### minSize & maxSize
@param minSize Minimum possible object size. Objects smaller than that are ignored.
@param maxSize Maximum possible object size. Objects larger than that are ignored. If `maxSize == minSize` model is evaluated on single scale.
minSize和maxSize 设置检测对象的最大最小值，低于minSize和高于maxSize的话就不会检测出来。


### 详细解释

两个重要的参数：scaleFactor，minNeighbors

Haar cascade的工作原理是一种“滑动窗口”的方法，通过在图像中不断的“滑动检测窗口”来匹配人脸。
#### scaleFactor
图像中的人脸因为远近不同也会有大有小，所以需要设定一个**比例**，对图像进行逐步缩小来检测。
这个**比例**就是**scaleFactor**。
参数设置的越大，计算速度越快，但可能会错过了某个大小的人脸。

#### minNeighbors
经过多次的迭代，实际会检测出很多很多个人脸
可以通过把minNeighbors 设为0来验证。
如何选择正确值呢？
**minNeighbors**规定了：只有“邻居”大于等于**minNeighbors**的结果才认为是正确结果。

### 示例：
首先**scaleFactor=1.1（默认值）**，分别设置**minNeighbors=0,1,3（默认为3）**，观察输出结果。

**minNeighbors=0**，识别出所有人脸：
![[detectMultiScale_1.png]]

**minNeighbors=1**，没有"邻居"<1 的结果被删除：
![[detectMultiScale_2.png]]

**minNeighbors=3**，没有"邻居"<3 的结果被删除：
![[detectMultiScale_3.png]]