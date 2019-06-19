# 信用卡识别项目说明
## 开发思路
将模板文件与读入的图片进行匹配。
## 步骤：

1. 模板图片的操作：
    - 读入模板图片 cv2.imread()
    - 将模板图片转换为灰度图 cv2.cvtColor()
    - 然后转换为二值图 cv2.threshold()
    - 做轮廓检测 外轮廓 (要使用图片副本) cv2.findContours()
    - 画出轮廓 cv2.drawContours()
    - 轮廓排序 思路:根据左上角的点坐标进行排序。
    - 遍历每一个模板轮廓。依次将放入集合中。
2. 读入图片的操作：
    - 读入图片 cv2.imread()
    - 重置图片大小 cv2.resize()
    - 将图片转换为灰度图 cv2.cvtColor()
    - 将图片进行礼帽操作,突出更明亮的区域 cv2.morphologyEx(,cv2.MORPH_TOPHAT,)
    - Sobel算子，图像梯度计算，进行边缘检测。cv2.Sobel()
    - 将上一步计算的图像梯度，进行归一化操作。
    - 闭操作 将数字连在一起 cv2.morphologyEx(gradX,cv2.MORPH_CLOSE,rectKernel)
    - 自适应阈值 cv2.threshold(gradX,0,255,cv2.THRESH_BINARY|cv2.THRESH_OTSU)[1]
    - 在进行一个闭操作
    - 计算轮廓
    - 画出轮廓
    - 遍历轮廓（四个数字一组）
    - 遍历每一个轮廓中的数字。计算每一个轮廓中每一个数字的值
3. 匹配结果
    - 匹配每一个数字 matchTemplate
    - 打印结果