# PiscTrace使用说明
_PiscTrace_ 是一款使用OpenCV(_跨平台计算机视觉库_)、MiDaS(_单目景深估计_)、YOLO(_CNN视觉检测_)的视图处理桌面应用
## 功能概述
### 输入格式
支持本地图片、本地视频、在线视频流和摄像头视频流的处理
### 处理功能
- 矫正：
滤镜平衡、视图矫正(_鱼眼畸变_、_桶形畸变_、_水平畸变_、_垂直畸变_)
- 调光：
亮度、曝光度、PS曲线
- 增强：
灰度、阈值、色相、MiDaS单目景深
- 降噪：
均值、高斯、中值
- YOLO:
检测框、实例分割、姿态、带方向检测框
## 操作流程
- 处理项目：
支持创建项目、导入已有项目文件包

![预览窗口](https://github.com/user-attachments/assets/910a2782-0d70-4d6b-bcab-f638311257fe)

- 视图处理

![处理窗口](https://github.com/user-attachments/assets/2c377160-47c3-4bea-a6d1-4df424c4c3dc)

- **注：** MiDaS加载需要访问GitHub在线资源
- **注：** 灰度值与阈值共同开启时可选择二值化蒙版处理
- **注：** YOLO处理优先于二值蒙版处理
# 导出并保存
- 支持保存视频的逐帧切片
- 支持导出视图的渲染结果
- 保存路径为：项目文件夹地址/save
  
## 编码插件
针对一些复杂的视图处理，PiscTrace分别提供了OpenCV预处理的接口和YOLO预测数据分析的接口!
## 预处理：
`frame = frame`为当前视图帧的像素矩阵，可以在编译器内调通后粘贴到输入框进行运行，例如反色处理`frame = -frame`
## YOLO数据分析：
  
![处理窗口](https://github.com/user-attachments/assets/a78e65c0-bc87-4bf5-a078-226d03fb97ee)

在加载YOLO后会出现进阶操作，其中预设了
- 检测框：围栏统计、热力监控、视线检测
- 实例分割：背景虚化
- 姿态：姿态监控(引体向上、俯卧撑)、姿态轨迹(关键点)
- 自定义
视线检测、背景虚化、姿态监控、姿态轨迹为代码形式，自定义代码可以参考代码案例
**注：**自定义代码需要严格遵循新建检测内的类定义结构
`class Test:`

    `def obj_exe(self, im0, tracks):`
       ` """`
       `Generate heatmap based on tracking data.`

        Args:
            im0 (ndarray): Image
            tracks (list): List of tracks obtained from the object tracking process.
        """

        self.im0 = im0

        self.result = tracks[0]

        self.orig_img = self.result.orig_img
        self.orig_shape = self.result.orig_img.shape[:2]
        self.boxes = self.result.boxes  # native size boxes
        self.masks = self.result.masks  # native size or imgsz masks
        self.probs = self.result.probs
        self.keypoints = self.result.keypoints
        self.obb = self.result.obb
        self.speed = self.result.speed
        self.names = self.result.names
        self.path = self.result.path
        """
        一些处理逻辑
        """
        return self.im0

# 作者：**那雨倾城**
        

