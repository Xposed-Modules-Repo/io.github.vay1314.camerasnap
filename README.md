<img src="./doc/CameraSnap.svg" width="200" alt="icon">

# CameraSnap
[![Xposed](https://img.shields.io/badge/-Xposed-green?style=flat&logo=Android&logoColor=white)](#)
[![GitHub](https://img.shields.io/github/license/vay1314/CameraSnap)](https://github.com/vay1314/CameraSnap/blob/main/LICENSE)
[![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/vay1314/CameraSnap?label=version)](https://github.com/vay1314/CameraSnap/releases)
[![GitHub all releases](https://img.shields.io/github/downloads/vay1314/CameraSnap/total?label=Downloads)](https://github.com/vay1314/CameraSnap/releases)

在 HyperOS 中实现息屏长按音量下键拍照、录像。

## 测试环境

> 小米 15 Pro  
> Android 15  
> 澎湃 OS 2（HyperOS 2）  
> 相机 6.0.002710.2

## 模块功能

1. 实现街拍模式。
2. 新版相机设置中的“街拍”选项直接打开模块设置，提供拍摄模式、摄像头选择、保存路径和桌面图标隐藏开关。照片和视频默认保存到 `DCIM/Camera/Snap`，可通过系统文件夹选择器选择其他本地目录。

## 使用方法

1. 安装模块，在支持 **libxposed API 102** 的 Xposed 管理器（如支持该 API 的 LSPosed 版本）中激活。
2. 作用域勾选 **相机** 和 **系统框架（system）**，然后重启手机。
3. 从桌面图标或相机设置中的“街拍”进入模块，授予相机权限；录像还需要麦克风权限。
4. 选择“息屏连拍”或“息屏录像”，熄屏后长按音量下键开始，松键停止。
5. 隐藏桌面图标后，可通过相机“街拍”入口进入模块，关闭隐藏开关恢复图标。


## 已知问题

* 目前测试环境为上述设备，其他机型、系统和相机版本仍需验证。

* 相机设置入口依赖相机内部实现，部分版本可能无法显示或跳转，可通过模块桌面图标配置。

* 因新版相机删除内置的街拍服务后，仅解除限制就无法恢复功能，模块使用独立 Camera2 拍摄服务，不包含小米相机的 HDR、徕卡风格、水印等私有处理功能。普通相机或其他应用占用摄像头时，息屏拍摄可能失败。

  

## 无法使用

请先检查模块是否正常激活、框架是否支持 API 102、相机和系统框架作用域是否勾选，以及激活后是否重启。再检查模块页面中的最近系统连接、拍摄状态、模式和权限。

如果排查后仍有错误，请提交 [issue](https://github.com/vay1314/CameraSnap/issues)，附上手机型号、Android / HyperOS 版本、相机和模块版本、具体表现，以及 LSPosed 日志和 Logcat 中标签为 `CameraSnap` 的日志。振动问题可同时提供 `VibratorManagerService` 日志。


## 致谢

基于 [GSWXXN / UnlockMIUICameraSnap](https://github.com/GSWXXN/UnlockMIUICameraSnap) 重建新版息屏拍摄链路。  
使用 [libxposed API](https://github.com/libxposed/api) 构建 API 102 Hook。  
使用 [Miuix](https://github.com/compose-miuix-ui/miuix) 构建 Compose 设置界面。  
