# Unity Remote 4

Unity Remote(当前版本为4)，是一个帮助开发者开发的应用。当你在编辑器中Play 模式运行时，它可以连接到Unity。可视化的输出到设备屏幕，设备的输入同时实时的发送回Unity。它能够在省去讨厌的打包情况下在真机上有一个比较完整的印象。
版本4完全重写了之前的版本，并且替换了安卓和iOS上之前的版本。

## 0 设备和支持的功能

Unity Remote 当前支持在Windows平台和OSX平台使用USB连接的安卓设备和仅在OSX通过USB连接的iOS设备。
Unity项目的Game视图将会被复制到设备中（帧率会被限制）。以下设备上的输入数据也会被流式传会编辑器
* 触摸
* 加速
* 螺旋
* 设备相机数据
* 指南针
* GPS
注意：Unity Remote 只是把显示放在了真机设备以及从真机设备采集输入。但是游戏本身还是在桌面机器上跑，所以不能反映打包出来的游戏性能。

## 1. 获取/使用Unity Remote

### 1.0 获取

1. 从Asset Store获取Unity 功能，然后自己编译
2. Google Play
3. App Storej

### 1.1 使用

0. 设备上打开Unity Remote，USB连上桌面机器
1. Edit > Project Settings > Editor 选好设备
点击Play按钮，Remote app将会出现你的游戏

## 2. Troubleshooting

### 2.0 多设备

当前不支持多台同样的设备，但是可以同时连上iOS和安卓设备

### 2.1 在Unity Remote中画质差

实际上游戏还是运行在你的Unity编辑器上，只不过把可视化的内容传输到设备上了。所以必然受到设备和编辑器之间带宽的限制，数据会被压缩必然导致图像质量下降。
可以选择压缩模式和分辨率
必须牢记，Unity Remote只是一个在真机设备上快速预览的一个途径，你应该是不是地打个真正的包。

### 2.2 OSX上编辑器不能连接iOS设备

Unity使用了一个不太稳定的第三方库（iproxy)，如果出现问题，可以尝试：
* 重新连接
* 重启设备
* Unity Remote setting中来回切一下选项
* 重启Unity编辑器
* kill all unityproxy
大多数情况 重连或者重启将解决问题

