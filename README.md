# PiscTrace

## 什么是PiscTrace
_PiscTrace_ 是一款综合性的视图处理桌面应用，集成了 *OpenCV*、*MiDaS* 和 *YOLO*，为用户提供了全面的计算机视觉处理功能。无论是基础的图像预处理，还是复杂的物体检测、深度估计，PiscTrace 都能轻松应对。

### OpenCV >>> https://github.com/opencv/opencv
### MiDas >>> https://github.com/isl-org/MiDaS
### YOLO >>> https://github.com/ultralytics

![2e9f56fdf13d47ad88c0a69e7d284ae8](https://github.com/user-attachments/assets/9da81336-cdf3-4866-a09e-789ffe97b298)

## PiscTrace特性
### 支持多样的视图文件格式:
  图片，视频，网络视频，摄像头视频流
### 丰富的预设的处理功能：
- 矫正：
滤镜平衡、视图矫正(_鱼眼畸变_、_桶形畸变_、_水平畸变_、_垂直畸变_)
- 调光：
亮度、曝光度、PS曲线
- 增强：
灰度、阈值、色相、MiDaS单目景深
- 降噪：
均值、高斯、中值
- 支持的YOLO检测模式:
检测框、实例分割、姿态、带方向检测框
### 自定义的编码入口
针对一些复杂的视图处理，PiscTrace分别提供了OpenCV预处理的接口和YOLO预测数据分析的接口!
#### 预处理：
```
class FrameObject:
    def __init__(self):
        self.init_parameters()

    def init_parameters(self, *args, **kwargs):
        pass

    def do(self, frame, device):
    
        return frame
```
**注：** 自定义代码需要严格遵循新建检测内的类定义结构

为当前视图帧的像素矩阵，可以在编译器内调通后粘贴到输入框进行运行，例如反色处理`return -frame`
#### 实验室: > https://blog.csdn.net/weixin_43607107/article/details/145441732

### 自定义的YOLO数据分析方法：
在加载YOLO后会出现进阶操作，其中预设了
- 检测框：围栏统计、热力监控、视线检测
- 实例分割：背景虚化
- 姿态：姿态监控(引体向上、俯卧撑)、姿态轨迹(关键点)
- 自定义
视线检测、背景虚化、姿态监控、姿态轨迹为代码形式，自定义代码可以参考代码案例

**注：** 自定义代码需要严格遵循新建检测内的类定义结构
  
```
class Test:
    def obj_exe(self, im0, tracks):
        """
       Generate heatmap based on tracking data.
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
```

## 作者：**那雨倾城**
### 更多详情请关注微信公众号
![qrcode_for_gh_7617a1a74172_258 1](https://github.com/user-attachments/assets/b6d45b3c-a6a7-4b93-900b-07062a8a9aa2)
### CSDN合集：> https://blog.csdn.net/weixin_43607107/category_12885488.html
### **欢迎关注**



