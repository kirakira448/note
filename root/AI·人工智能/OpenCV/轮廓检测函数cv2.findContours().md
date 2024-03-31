
```python
cv2.findContours(image, mode, method[, contours[, hierarchy[, offset ]]])  
```
## 参数

image：参数是寻找轮廓的图像；
mode：参数表示轮廓的检索模式，有四种（本文介绍的都是新的cv2接口）：
	cv2.RETR_EXTERNAL：表示只检测外轮廓
	cv2.RETR_LIST：检测的轮廓不建立等级关系
	cv2.RETR_CCOMP：建立两个等级的轮廓，上面的一层为外边界，里面的一层为内孔的边界信息。如果内孔内还有一个连通物体，这个物体的边界也在顶层。
	cv2.RETR_TREE：建立一个等级树结构的轮廓。
method：轮廓的近似办法：
	cv2.CHAIN_APPROX_NONE：存储所有的轮廓点，相邻的两个点的像素位置差不超过1，即`max（abs（x1-x2），abs（y2-y1））==1`
	cv2.CHAIN_APPROX_SIMPLE：压缩水平方向，垂直方向，对角线方向的元素，只保留该方向的终点坐标，例如一个矩形轮廓只需4个点来保存轮廓信息
	cv2.CHAIN_APPROX_TC89_L1，CV_CHAIN_APPROX_TC89_KCOS：使用teh-Chinl chain 近似算法



## 返回值

新版本中只有两个返回值。

### contour  

返回一个list，list中每个元素都是图像中的一个轮廓，用numpy中的ndarray表示。  
### hierarchy

返回一个ndarray，其中的元素个数和轮廓个数相同，
每个轮廓 `contours[i]`对应4个hierarchy元素
`hierarchy[i][0] ~hierarchy[i][3]`，
分别表示后一个轮廓、前一个轮廓、父轮廓、内嵌轮廓的索引编号，如果没有对应项，则该值为负数。