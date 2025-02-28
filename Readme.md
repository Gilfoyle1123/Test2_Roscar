### Readme

#### 任务1：键盘控制小车

**思路**：编写节点`keyboard_ctrl`，读取键盘信息，将键盘输入的字符映射为`msg`消息包的格式，并向话题`/cmd_vel`中发布消息，控制小车运动。

#### 任务2：RGB图像转化为HSV格式

**HSV格式**：HSV 是一种常见的颜色空间模型，全称为 **Hue-Saturation-Value**，即色相（Hue）、饱和度（Saturation）和明度（Value）。HSV格式的图片是基于这种颜色模型编码的图像，与我们更熟悉的RGB颜色模型不同，它更适合处理图像的颜色属性和操作，比如颜色分割和调整。

**HSV三个分量解释**：

1. **Hue（色相）：**
   表示颜色的种类，用角度表示，从 0° 到 360°。
   - 例如，红色对应 0°，绿色对应 120°，蓝色对应 240°。
2. **Saturation（饱和度）：**
   表示颜色的纯度或鲜艳程度，范围是 0 到 1（或 0 到 100%）。
   - 饱和度高的颜色更鲜艳，饱和度低时接近灰色。
3. **Value（明度）：**
   表示颜色的亮度或强度，范围是 0 到 1（或 0 到 100%）。
   - 明度越高，颜色越亮；明度为 0 时就是黑色。

**代码实现**：在回调函数中调用`cv::cvtColor()`函数，将获取到的`RGB`格式图像转化为`HSV`格式，并在窗口中显示。

**HSV格式图像的应用**：利用HSV格式图像，实现颜色识别，降低环境亮度等条件对识别效果的影响。

#### 任务3：融合雷达和imu数据，实现小车定位

**AMCL算法**：

​	AMCL是一种基于粒子滤波的自适应定位算法，用于移动机器人在已知地图中的位置估计。它结合了蒙特卡洛方法和贝叶斯滤波，通过维护一组粒子来表示机器人可能的位姿分布，从而实现机器人在环境中的精确定位。

**代码实现**：

1.利用`hector_mapping`包，实现SLAM建图，保存地图至`/roscar/map/`文件夹中,并发布到话题`/map`中。

2.利用`AMCL`包中的节点，订阅消息话题`/imu`以及`map`,在话题`/amcl_pose`中发布小车的位置信息。

**消息包例子**:

```
header: 
  seq: 5
  stamp: 
    secs: 477
    nsecs: 601000000
  frame_id: "map"
pose: 
  pose: 
    position: 
      x: -1.7324685827882145
      y: -0.03368116914734127
      z: 0.0
    orientation: 
      x: 0.0
      y: 0.0
      z: 0.017028854748203412
      w: 0.9998549985402706
  covariance: [0.09364207272193292, 0.00038567837905811864, 0.0, 0.0, 0.0, 0.0, 0.00038567837905811864, 0.011789416057157387, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.003377776238969184]
---
header: 
  seq: 6
  stamp: 
    secs: 479
    nsecs:  15000000
  frame_id: "map"

```





