设备(IPC)网络 SDK 编程指南  

V5.2  

# 声  明  

非常感谢您购买我公司的产品，如果您有什么疑问或需要请随时联系我们。  

 我们已尽量保证手册内容的完整性与准确性，但也不免出现技术上不准确、与产品功能及操作不相符或印刷错误等情况，如有任何疑问或争议，请以我司最终解释为准。  
 产品和手册将实时进行更新，恕不另行通知。  
 本手册中内容仅为用户提供参考指导作用，请以 SDK 实际内容为准。  

## 目  录  

声 明  

目 录  

1 SDK 简介  

2 SDK 版本更新.  

### 3 函数调用顺序 33  

3.1 SDK 基本调用的主要流程 . . 33  
3.2 实时预览模块流程 . 35  
3.3 回放和下载模块流程 .. 36  
3.4 参数配置模块流程 ...37  
3.5 远程设备维护模块流程 ... 38  
3.6 语音对讲转发模块流程 .. 39  
3.7 报警模块流程 . . 40  
3.7.1 报警（布防）流程 . 40  
3.7.2 报警（监听）流程 . 41  

#### 3.8 透明通道模块流程 42  

### 4 函数调用实例 43  

4.1 预览模块的示例代码 43  
4.2 回放和下载模块的示例代码 48  
4.3 参数配置模块的示例代码 . ..55  
4.4 远程设备维护模块的示例代码 ..57  
4.5 语音对讲转发模块的示例代码 . 59  
4.6 报警模块的示例代码 .... . 61  
4.7 透明通道模块的示例代码 .. . 65  

### 函数说明 68  

#### 5.1 SDK 初始化 . 68  

5.1.1 初始化 SDK NET_DVR_Init .. 68  
5.1.2 释放 SDK 资源 NET_DVR_Cleanup . 68  

5.2 SDK 本地功能 . 68  

### SDK 本地参数配置 68  

5.2.1 获取 SDK 本地参数 NET_DVR_GetSDKLocalCfg . ... 68  
5.2.2 设置 SDK 本地参数 NET_DVR_SetSDKLocalCfg, . 69  
连接和接收超时时间及重连设置 ...... ...70  
5.2.3 设置网络连接超时时间和连接尝试次数 NET_DVR_SetConnectTime . ...70  
5.2.4 设置重连功能 NET_DVR_SetReconnect. ..70  
5.2.5 设置接收超时时间 NET_DVR_SetRecvTimeOut... .70  

5.2.8 获取 SDK 的版本号和 build 信息 NET_DVR_GetSDKBuildVersion ......... 71  

5.2.9 获取当前 SDK 的状态信息 NET_DVR_GetSDKState . 71  

5.2.10 获取当前 SDK 的功能信息 NET_DVR_GetSDKAbility ......... 71  
SDK 启用写日志 .. .72  
5.2.11 启用写日志文件 NET_DVR_SetLogToFile.. ..72  
异常消息回调 .. ...72  
5.2.12 注册异常消息回调函数 NET_DVR_SetExceptionCallBack_V30 . ..72  
获取错误信息 ...74  
5.2.13 返回最后操作的错误码 NET_DVR_GetLastError.. .74  
5.2.14 返回最后操作的错误码信息 NET_DVR_GetErrorMsg . . 75  

5.3 用户注册 . 75  

5.3.1 激活设备 NET_DVR_ActivateDevice.. 75  
5.3.2 IPServer 或者 DDNS 域名解析，获取动态 IP 地址和端口号  
NET_DVR_GetDVRIPByResolveSvr_EX... ... 75  
5.3.3 用户注册设备 NET_DVR_Login_V40.. ...76  
5.3.4 用户注销 NET_DVR_Logout.. .76  

5.4 获取设备能力集 . 6  

5.4.1 获取设备能力集 NET_DVR_GetDeviceAbility.. 6  
5.4.2 获取设备能力集 NET_DVR_GetSTDAbility... 78  

#### 5.5 实时预览 . 81  

5.5.1 实时预览 NET_DVR_RealPlay_V40 . 81   
5.5.2 停止预览 NET_DVR_StopRealPlay .. .82   
5.5.3 获取预览时用来解码和显示的播放库句柄 NET_DVR_GetRealPlayerlndex.... ...82  

5.6 强制 I 帧和刷新帧 82  

5.6.1 强制 I 帧 NET_DVR_RemoteControl .. .82  
5.6.2 强制刷新帧(Smart264)NET_DVR_STDControl. 83  

#### 5.7 预览显示视频参数配置 83  

5.7.1 获取预览视频显示参数 NET_DVR_ClientGetVideoEffect .. .. 83  
5.7.2 获取预览视频显示参数 NET_DVR_GetVideoEffect . . 84  
5.7.3 设置预览视频显示参数 NET_DVR_ClientSetVideoEffect.. . 84  
5.7.4 设置预览视频显示参数 NET_DVR_SetVideoEffect ...... . 84  

5.8 预览画面叠加字符和图像 85  

5.8.1 预览画面叠加字符和图像，Linux 下无此接口 NET_DVR_RigisterDrawFun ....................... 85  

5.9 预览时播放声音控制 85  

5.9.1 设置声音播放模式 NET_DVR_SetAudioMode.... .. 85  
5.9.2 独占声卡模式下开启声音 NET_DVR_OpenSound .. . 86  
5.9.3 独占声卡模式下开启声音 NET_DVR_CloseSound .. . 86  
5.9.4 共享声卡模式下开启声音 NET_DVR_OpenSoundShare. . 86  
5.9.5 共享声卡模式下关闭声音 NET_DVR_CloseSoundShare... ... 86  
5.9.6 调节播放音量 NET_DVR_Volume .. . 86  

#### 5.10 实时数据回调和录像 .87  

5.10.1 注册回调函数，捕获实时码流数据 NET_DVR_SetRealDataCallBack .. .87  
5.10.2 注册回调函数，捕获实时码流数据（标准码流）NET_DVR_SetStandardDataCallBack ...87  
5.10.3 捕获数据并保存到指定的文件中 NET_DVR_SaveRealData ....... .... 88  
5.10.4 停止数据捕获 NET_DVR_StopSaveRealData.. 88  

5.11 预览抓图 . 89  

5.11.1 设置抓图模式 NET_DVR_SetCapturePictureMode... 89  

5.11.2 预览时，单帧数据捕获并保存成图片 NET_DVR_CapturePicture. 89  

5.12 设备抓图 . 89  

5.12.1 单帧数据捕获并保存成 JPEG 图片 NET_DVR_CaptureJPEGPicture ...... 895.12.2 单帧数据捕获并保存成 JPEG 存放在指定的内存空间中NET_DVR_CaptureJPEGPicture_NEW... . 90  

5.13 参数配置 .... ..... 90  

系统参数配置 .... .... 90  
5.13.1 获取设备参数 NET_DVR_GetDVRConfig. ..... 90  
5.13.2 设置设备参数 NET_DVR_SetDVRConfig. .... 91  
5.13.3 获取设备参数 NET_DVR_GetSTDConfig .... ......92  
通道参数配置 .. .....92  
5.13.4 获取通道参数 NET_DVR_GetDVRConfig, ...92  
5.13.5 设置通道参数 NET_DVR_SetDVRConfig.... ......... 93  
5.13.6 获取通道参数 NET_DVR_GetSTDConfig ... .... 94  
5.13.7 设置通道参数 NET_DVR_SetSTDConfig .......... .... 95  
5.13.8 批量获取通道参数 NET_DVR_GetDeviceConfig . ..... 95  
5.13.9 批量设置通道参数 NET_DVR_SetDeviceConfig. ....... 96  
网络参数配置 ...... ..97  
5.13.10 获取网络参数 NET_DVR_GetDVRConfig. ..97  
5.13.11 设置网络参数 NET_DVR_SetDVRConfig... ........ 98  
5.13.12 获取网络参数 NET_DVR_GetSTDConfig . ....... 99  
5.13.13 设置网络参数 NET_DVR_SetSTDConfig ..... ....... 99  
5.13.14 批量获取网络参数 NET_DVR_GetDeviceConfig .. ..... 100  
5.13.15 批量设置网络参数 NET_DVR_SetDeviceConfig. ..... 101  
5.13.16 获取 RTSP 协议参数 NET_DVR_GetRtspConfig. .....102  
5.13.17 设置 RTSP 协议参数 NET_DVR_SetRtspConfig ...102  
报警输入输出配置 .. ......102  
5.13.18 获取设备参数 NET_DVR_GetDVRConfig... .....102  
5.13.19 设置设备参数 NET_DVR__SetDVRConfig... ..... 103  
5.13.20 获取设备报警输出 NET_DVR_GetAlarmOut_V30 . .... 103  
5.13.21 设置设备报警输出 NET_DVR_SetAlarmOut ..... .... 104  
用户和安全参数配置 ................ .......... 104  
5.13.22获取设备参数 NET_DVR_GetDVRConfig. .... 104  
5.13.23设置设备参数 NET_DVR_SetDVRConfig. .... 104  
外设参数配置 ..... 105  
5.13.24 获取设备参数 NET_DVR_GetSTDConfig .... ...... 105  
5.13.25 设置设备参数 NET_DVR_SetSTDConfig .... .... 105  
5.13.26 批量获取配置信息 NET_DVR_GetDeviceConfig . ... 106  
5.13.27 批量设置配置信息 NET_DVR_SetDeviceConfig. .107  

5.14 SMART 参数配置. 107参数配置 107  

5.14.1 获取设备的配置信息 NET_DVR_GetDVRConfig ...... ..107  
5.14.2 设置设备的配置信息 NET_DVR_SetDVRConfig. . 108  
5.14.3 获取设备的配置信息(标准协议)NET_DVR_GetSTDConfig ......... .... 109  
5.14.4 获取设备的配置信息(标准协议)NET_DVR_SetSTDConfig ......... .. 112  
批量参数配置 . ....... 116  
5.14.5 批量获取配置信息 NET_DVR_GetDeviceConfig ........... ..... 116  
5.14.6 批量设置配置信息 NET_DVR_SetDeviceConfig.. ...... 118  
长连接参数配置 . ....... 119  
5.14.7 启动长连接远程配置 NET_DVR_StartRemoteConfig .. .... 119  
5.14.8 逐个获取查找到的信息 NET_DVR_GetNextRemoteConfig.... ........ 120  
5.14.9关闭长连接配置 NET_DVR_StopRemoteConfig.. ...... 121  
远程控制 ...... 121  
5.14.10 远程控制(标准协议) NET_DVR_STDControl ........ .... 121  
文件上传下载 .. ... ..... 122  
5.14.11 上传文件 NET_DVR_UploadFile_V40 ... ....... 122  
5.14.12 获取文件上传的进度和状态 NET_DVR_GetUploadState .. ....... 122  
5.14.13 停止文件上传 NET_DVR_UploadClose. ... 122  
5.14.14 开始下载文件 NET_DVR_StartDownload... .......... 123  
5.14.15 获取文件下载的进度和状态 NET_DVR_GetDownloadState ...... 123  
5.14.16 停止文件下载 NET_DVR_StopDownload .. ...... 123  
5.15 长连接参数配置 . .... 124  
5.15.1 启动长连接远程配置 NET_DVR_StartRemoteConfig ... ..... 124  
5.15.2 关闭长连接配置 NET_DVR_StopRemoteConfig... .......... 125  
5.16 远程控制 . . 125  
5.16.1 远程控制 NET_DVR_RemoteControl .. ...... 125  
5.16.2 远程控制(标准协议) NET_DVR_STDControl . .... 125  
5.17 证书管理 . ...... 126  
证书创建、删除 . ...... 126  
5.17.1 远程控制 NET_DVR_RemoteControl . .... 126  
证书信息获取 .. ... 126  
5.17.2 批量获取配置信息 NET_DVR_GetDeviceConfig .. ....... 126  
证书上传下载 .. ..127  
5.17.3 上传文件 NET_DVR_UploadFile_V40 ..... .127  
5.17.4 获取文件上传的进度和状态 NET_DVR_GetUploadState .. .... 128  
5.17.5 停止文件上传 NET_DVR_UploadClose... ......... 128  
5.17.6 开始下载文件 NET_DVR_StartDownload. ........ 128  
5.17.7 获取文件下载的进度和状态 NET_DVR_GetDownloadState . ....... 129  
5.17.8 停止文件下载 NET_DVR_StopDownload .. .... 129  
5.18 存储管理 . ...... 129  
5.18.1 获取设备参数 NET_DVR_GetDVRConfig. ..... 129  
5.18.2 设置设备参数 NET_DVR_SetDVRConfi... ....... 130  
5.18.3 获取设备参数 NET_DVR_GetSTDConfig . ... 130  
5.18.4 设置设备参数 NET_DVR_SetSTDConfig .. . 131  
5.18.5 远程格式化设备硬盘 NET_DVR_FormatDisk . ...... 131  
5.18.6 获取格式化硬盘的进度 NET_DVR_GetFormatProgress.. .... 131  
5.18.7 关闭格式化硬盘句柄，释放资源 NET_DVR_CloseFormatHandle .. . 132  

#### 5.19 布防、撤防 . 132  

设置报警等信息上传的回调函数 . 132  

5.19.1 注册报警消息回调函数 NET_DVR_SetDVRMessageCallBack_V31 ....... ... 132  
布防撤防 . ... 134  
5.19.2 建立报警上传通道，获取报警等信息 NET_DVR_SetupAlarmChan_V41. ... 134  
5.19.3 撤销报警上传通道 NET_DVR_CloseAlarmChan_V30 . . 134  

5.20 监听报警 . 134  

5.20.1 启动监听，．接收设备主上传的报警等信息NET.DVR_.tarListen..V30.... 134.  
5.20.2 停止监听（支持多线程）NET_DVR_StopListen_V30.... ... 136  
5.21 录像文件回放、下载、锁定及备份.. ... 136  
录像文件的查找 . ... 136  
5.21.1 根据文件类型、时间查找设备录像文件 NET_DVR_FindFile_V40. .... 136  
5.21.2 逐个获取查找到的文件信息 NET_DVR_FindNextFile_V40 ........ ..... 136  
5.21.3 关闭文件查找，释放资源 NET_DVR_FindClose_V30.. ...137  
回放录像文件 ..... ...137  
5.21.4 按文件名回放录像文件 NET_DVR_PlayBackByName ... ...137  
5.21.5 按时间回放录像文件 NET_DVR_PlayBackByTime_V40 . . 138  
5.21.6 控制录像回放的状态 NET_DVR_PlayBackControl_V40 .... .... 138  
5.21.7 停止回放录像文件 NET_DVR_StopPlayBack ... ... 140  
回放录像文件时的数据捕获 ..... ....... 140  
5.21.8 捕获回放的录像数据，并保存成文件 NET_DVR_PlayBackSaveData . .... 140  
5.21.9 停止保存录像数据 NET_DVR_StopPlayBackSave ....... ...... 140  
5.21.10 注册回调函数，捕获录像数据 NET_DVR_SetPlayDataCallBack_V40 . .. 141  
回放的其他操作 . . 141  
5.21.11 获取录像回放时显示的 OSD 时间 NET_DVR_GetPlayBackOsdTime. .. 141  
5.21.12 录像回放时抓图，并保存在文件中 NET_DVR_PlayBackCaptureFile . .. 142  
5.21.13 刷新显示回放窗口 NET_DVR_RefreshPlay ............. ..... 142  
5.21.14 获取回放解码显示的播放库句柄 NET_DVR_GetPlayBackPlayerIndex . .... 142  
下载录像文件 ... ... 143  
5.21.15按文件名下载录像文件 NET_DVR_GetFileByName.. .. 143  
5.21.16 按时间下载录像文件 NET_DVR_GetFileByTime_V40. . 143  
5.21.17 控制录像下载的状态 NET_DVR_PlayBackControl_V40 ...... ..... 143  
5.21.18 停止下载录像文件 NET_DVR_StopGetFile.. ... 145  
5.21.19 获取当前下载录像文件的进度 NET_DVR_GetDownloadPos ..... ... 145  
录像文件锁定和解锁 . ... 145  
5.21.20 按文件名锁定录像文件 NET_DVR_LockFileByName ........... ... 145  
5.21.21 按文件名解锁录像文件 NET_DVR_UnlockFileByName ... . 145  

5.22 图片的查找、回放下载 146查找图片 146  

5.22.1 根据类型和时间查找图片 NET_DVR_FindPicture . . 146  
5.22.2 逐个获取查找到的图片 NET_DVR_FindNextPicture_V40. . 146  
5.22.3 关闭图片查找，释放资源 NET_DVR_CloseFindPicture. . 146  
回放（下载）图片 .147  

5.22.4 图片回放 NET_DVR_GetPicture_V30 147  

#### 5.23 云台控制 . 47  

云台控制操作 ...147  
5.23.1 云台控制操作（需先启动图像预览）NET_DVR_PTZControl . ...147  
5.23.2 云台控制操作（不用启动图像预览）NET_DVR_PTZControl_Other.. ...... 149  
5.23.3 带速度的云台控制操作（需先启动图像预览）NET_DVR_PTZControlWithSpeed .......... 149  
5.23.4 带速度的云台控制操作（不用启动图像预览）NET_DVR_PTZControlWithSpeed_Other 149  
云台预置点操作 ... .... 150  
5.23.5 云台预置点操作，需先启动预览 NET_DVR_PTZPreset ..... .... 150  
5.23.6 云台预置点操作 NET_DVR_PTZPreset_Other .... ...... 150  
云台巡航操作 .. ...... 151  
5.23.7 云台巡航操作，需先启动预览 NET_DVR_PTZPCruise .. ..... 151  
5.23.8 云台巡航操作 NET_DVR_PTZPCruise_Other .... .....152  
云台花样扫描操作 . ....152  
5.23.9 云台花样扫描操作，需先启动预览 NET_DVR_PTZTrack.. .......152  
5.23.10 云台花样扫描操作 NET_DVR_PTZTrack_Other ........... ...........152  
透明云台控制 .. ...... 153  
5.23.11 透明云台操作，需先启动预览 NET_DVR_TransPTZ... ...... 153  
5.23.12 透明云台操作 NET_DVR_TransPTZ_Other .. ..... 153  
云台区域缩放控制 .. ...... 153  
5.23.13 云台图象区域选择放大或缩小 NET_DVR_PTZSelZoomIn .... ...... 153  
5.23.14 云台图像区域选择放大或缩小 NET_DVR_PTZSelZoomIn_Ex .. ..... 154  
云台参数配置 .. .... 154  
5.23.15 获取设备的配置信息 NET_DVR_GetDVRConfig .. .... 154  
5.23.16设置设备的配置信息 NET_DVR_SetDVRConfig.. ...... 155  
5.23.17 批量获取配置信息 NET_DVR_GetDeviceConfig ... ...... 156  
5.23.18批量设置配置信息 NET_DVR_SetDeviceConfig.... ..157  
云台参数长连接配置 .. ..... 158  
5.23.19 启动长连接远程配置 NET_DVR_StartRemoteConfig . .... 158  
5.23.20关闭长连接配置 NET_DVR_StopRemoteConfig.. ...... 159  
远程控制... ..... 159  
5.23.21 远程控制 NET_DVR_RemoteControl .. .... 159  
获取巡航路径 . .... 160  
5.23.22 获取 IP 快球云台巡航路径 NET_DVR_GetPTZCruise . .... 160  
辅助聚焦控制 .... ....... 160  
5.23.23 控制一键聚焦 NET_DVR_FocusOnePush .......... ......... 160  
恢复镜头电机默认位置 .... 160  
5.23.24恢复镜头电机默认位置 NET_DVR_ResetLens. ... 160  

5.24 语音对讲、转发及广播 161语音对讲(Windows 32 位系统支持). 161  

5.24.4 启动语音转发，获取编码后的音频数据 NET_DVR_StartVoiceCom_MR_V30 ..................162  

5.24.5 转发语音数据 NET_DVR_VoiceComSendData . .. 163  
5.24.6 停止语音对讲或语音转发 NET_DVR_StopVoiceCom .. ......... 164  
语音广播(Windows 32 位系统支持).. ..... 164  
5.24.7 启动语音广播的 PC 端声音捕获 NET_DVR_ClientAudioStart_V30. ..... 164  
5.24.8 添加设备的某个语音通道到可以接收 PC 端声音的广播组 NET_DVR_AddDVR _V30..... 164  
5.24.9 从可接收 PC 机声音的广播组里删除该设备的语音通道 NET_DVR_DelDVR_V30 .......... 165  
5.24.10停止语音广播的 PC 端声音捕获 NET_DVR_ClientAudioStop.. ...... 165  
音频压缩参数 ............ ....... 165  
5.24.11 获取当前生效的对讲音频压缩参数 NET_DVR_GetCurrentAudioCompress ..................... 165  
5.24.12获取通道参数 NET_DVR_GetDVRConfig.. .......... 165  
5.24.13设置通道参数 NET_DVR_SetDVRConfig. ....... 166  
音频编解码(Windows 32 位系统支持).. ....... 166  
G722 音频编解码 ..... 166  
5.24.14初始化音频编码 NET_DVR_InitG722Encoder.. ....... 166  
5.24.15G722 音频编码 NET_DVR_EncodeG722Frame... ........167  
5.24.16释放音频编码资源 NET_DVR_ReleaseG722Encoder... ......167  
5.24.17 初始化音频解码 NET_DVR_InitG722Decoder .... ....167  
5.24.18 G722 音频解码 NET_DVR_DecodeG722Frame ...... ........167  
5.24.19 释放音频解码资源 NET_DVR_ReleaseG722Decoder ......... ....... 168  
G711 音频编解码... ....... 168  
5.24.20 G711 音频编码 NET_DVR_EncodeG711Frame ............. ......... 168  
5.24.21 G711 音频解码 NET_DVR_DecodeG711Frame .......... ...... 168  
G726 音频编解码... ...... 169  
5.24.22初始化音频编码 NET_DVR_InitG726Encoder.. ...... 169  
5.24.23G726 音频编码 NET_DVR_EncodeG726Frame... ..... 169  
5.24.24 释放音频编码资源 NET_DVR_ReleaseG726Encoder... ..... 169  
5.24.25 初始化音频解码 NET_DVR_InitG726Decoder ..... ...... 169  
5.24.26 G726 音频解码 NET_DVR_DecodeG726Frame ..... ..170  
5.24.27 释放音频解码资源 NET_DVR_ReleaseG726Decoder ...... ..170  
5.25 透明通道 ...... ..170  
5.25.1 建立透明通道 NET_DVR_SerialStart ... ..170  
5.25.2 通过透明通道向设备串口发送数据 NET_DVR_SerialSend . .. 171  
5.25.3 断开透明通道 NET_DVR_SerialStop..... ....... 171  
5.26 向串口发送数据 ........ ............ 171  
5.26.1.直接向串口发送数据，不需要建立透明通道NET_.DVR_.endToSerialPor.......171  
5.26.2直接向232 串口发送数据，不需要建立透明通道NET__DVR_endTo232Por...172  
5.27 设备手动录像 . .1.72  
5.27.1 远程手动启动设备录像 NET_DVR_StartDVRRecord .. .1.7.  
5.27.2 远程手动停止设备录像 NET_DVR_StopDVRRecord . ..72  
5.28 服务器测试 . ......173  
服务器测试 . .....173  
5.28.1 启动长连接远程配置 NET_DVR_StartRemoteConfig ..... .......173  
5.28.2 获取长连接配置的状态 NET_DVR_GetRemoteConfigState .......... ....173  
5.28.3 关闭长连接配置 NET_DVR_StopRemoteConfig.. ..1.74  
Email 测试 .. ...1.74  
5.28.4 测试按已配置的 EMAIL 参数能否收发成功 NET_DVR_StartEmailTest... ...174  
5.28.5 获取邮件测试的进度 NET_DVR_GetEmailTestProgress ...... ...........175  
5.28.6 停止邮件测试 NET_DVR_StopEmailTest ...... .........175  
5.29 鱼眼相关功能 .. ..........175  
鱼眼参数配置 . ......175  
5.29.1 获取设备的配置信息 NET_DVR_GetDVRConfig .. ....175  
5.29.2 设置设备的配置信息 NET_DVR_SetDVRConfig.. ..176  
5.29.3 批量获取配置信息 NET_DVR_GetDeviceConfig ...... ..... 177  
长连接配置 . ..... 177  
5.29.4 启动长连接远程配置 NET_DVR_StartRemoteConfig . . 177  
5.29.5 发送长连接数据 NET_DVR_SendRemoteConfig ..... .1.78  
5.29.6 关闭长连接配置 NET_DVR_StopRemoteConfig.... ........179  
远程控制 .......179  
5.29.7 远程控制 NET_DVR_RemoteControl .. ....179  
获取鱼眼设备状态 . ....179  
5.29.8 获取设备状态 NET_DVR_GetDeviceStatus .. .....179  
5.30 GIS 相关功能 .. ...... 180  
GIS 参数配置 . ..... 180  
5.30.1 获取设备的配置信息 NET_DVR_GetDVRConfig .. . 180  
5.30.2 设置设备的配置信息 NET_DVR_SetDVRConfig. ....... 181  
5.30.3 获取设备的配置信息(标准协议)NET_DVR_GetSTDConfig ..... . 181  
5.30.4 设置设备的配置信息(标准协议)NET_DVR_SetSTDConfig ...... ...... 182  
电子罗盘远程控制 . . 182  
5.30.5 远程控制(标准协议) NET_DVR_STDControl .. ........ 182  
5.31 设备维护管理 . ... 183  
获取设备工作状态 . . 183  
5.31.1 获取设备的工作状态 NET_DVR_GetDVRWorkState_V30 .. ... 183  
5.31.2 获取设备运行状态 NET_DVR_GetDeviceStatus .. .... 183  
5.31.3 设备在线状态检测 NET_DVR_RemoteControl ..... ..... 184  
5.31.4 启动设备状态巡检NET_DVR__StartGetDevState... ...... 185  
5.31.5 停止设备状态巡检 NET_DVR_StopGetDevState .. ...... 185  
5.31.6 启动长连接远程配置 NET_DVR_StartRemoteConfig ...... ....... 185  
5.31.7 关闭长连接 NET_DVR_StopRemoteConfig.. ...... 186  
远程升级 ... 186  
5.31.8 设置远程升级时网络环境 NET_DVR_SetNetworkEnvironment ... ... 186  
5.31.9 远程升级 NET_DVR_Upgrade .. .....187  
5.31.10 获取远程升级的进度 NET_DVR_GetUpgradeProgres.. .....187  
5.31.11 获取远程升级的状态 NET_DVR_GetUpgradeState . ......187  
5.31.12 获取远程升级的阶段信息 NET_DVR_GetUpgradeStep . .....187  
5.31.13 关闭远程升级句柄，释放资源 NET_DVR_CloseUpgradeHandle ........... ....... 188  
日志查找 . ..... 188  
5.31.14 查找设备的日志信息 NET_DVR_FindDVRLog_V30 . ...... 188  
5.31.15 逐条获取查找到的日志信息 NET_DVR_FindNextLog_V30 ....... .... 195  
5.31.16 释放查找日志的资源 NET_DVR_FindLogClose_V30 . ... 196  
恢复设备默认参数 . 196  
5.31.17 恢复设备默认参数 NET_DVR_RestoreConfig ......... ...... 196  
5.31.18 完全恢复出厂默认参数 NET_DVR_RemoteControl . . 196  
导入/导出配置文件. ..197  
5.31.19 导出配置文件 NET_DVR_GetConfigFile_V30.. ...197  
5.31.20 导出配置文件 NET_DVR_GetConfigFile.. ..197  
5.31.21 导入配置文件 NET_DVR_SetConfigFile_EX.. .197  
5.31.22 导入配置文件 NET_DVR_SetConfigFile..... ...197  
关机和重启 ..... .... 198  
5.31.23 重启设备 NET_DVR_RebootDVR ..... . 198  
5.31.24 关闭设备 NET_DVR_ShutDownDVR . . 198  
6 错误代码及说明 ... 199  
6.1 网络通讯库错误码 .. 199  
6.2 RTSP 通讯库错误码 ..202  
6.3 软解码库错误码 ..... .... 204  
6.4 语音对讲库错误码 . 204  

# 1 SDK 简介  

设备网络 SDK 是基于设备私有网络通信协议开发的，为嵌入式网络硬盘录像机、NVR、视频服务器、网络摄像机、网络球机、解码器、报警主机等网络产品服务的配套模块，用于远程访问和控制设备软件的二次开发。  

本文档仅介绍 IPC(网络摄像机)和 IPD（网络球机）支持的功能及相关接口，相关结构体和更多其他功能接口请参考《设备网络 SDK 使用手册.chm》。  

## 适用于但不仅限于以下产品型号：  

网络摄像机：标清、高清、红外、鱼眼等，如 DS-2CD7xx, DS-2CD71xx, DS-2CD72xx, DS-2CD8xx, DS-2CD81xx, DS-2CD82xx, DS-2CD84xx, DS-2CD83xx, DS-2CD11xx, DS-2CD12xx, DS-2CD13xx, DS-2CD20xx, DS-2CD21xx, DS-2CD22xx, DS-2CD23xx, DS-2CD24xx, DS-2CD25xx, DS-2CD26xx, DS-2CD27xx, DS-2CD28xx, DS-2CD29xx, DS-2CD2Axx, DS-2CD2Cxx, DS-2CD2Dxx, DS-2CD2Txx, DS-2CD2Qxx, DS-2CD30xx, DS-2CD31xx, DS-2CD32xx, DS-2CD33xx, DS-2CD34xx, DS-2CD39xx, DS-2CD3Txx, DS-2CD3Qxx, DS-2CD40xx, DS-2CD41xx, DS-2CD42xx, DS-2CD4Axx, DS-2CD62xx, DS-2CD63xx, DS-2CD64xx, DS-2CD65xx 等；  

网络球机：标清、高清、红外等，如 DS-2DF86xx, DS-2DF85xx, DS-2DF82xx, DS-2DF72xx, DS-2DF71xx, DS-2DE71xx, DS-2DE73xx, DS-2DE72xx, DS-2DM72xx, DS-2DM71xx, DS-2DF1-7xx, DS-2DF66xx, DS-2DF62xx, DS-2DF1-6xx, DS-2DE51xx, DS-2DE52xx, DS-2DE53xx, DS-2DM52xx, DS-2DF52xx, DS-2DC52xx, DS-2DC51xx, DS-2DF1-5xx, DS-2DE45xx, DS-2DE42xx, DS-2DE41xx, DS-2DF1-4xx, DS-2DM1-7xx, DS-2DM1-6xx, DS-2DM1-5xx 等；  

一体化网络摄像机：DS-2ZCN3007, DS-2ZCN3006, DS-2DZ216MF, DS-2DZ2116, DS-2ZCN2006, DS-2ZCN2007, DS-2ZMN2007, DS-2ZMN2006 等。  

设备网络 SDK 主要功能 ：  

主要用于实时码流预览、录像文件回放和下载、云台控制、布防/撤防、语音对讲、日志管理、远程升级、格式化硬盘（SD 卡）、参数配置（系统配置、通道配置、串口配置、报警配置、用户配置）和获取设备能力集等。  

设备网络 SDK 包含网络通讯库、播放库等功能组件，我们提供 Windows 和 Linux 两个版本的 SDK，各自所包含的组件如下：  

表 1.1 Windows SDK 组件  


<html><body><table><tr><td rowspan="5">网络通讯库 核心组件</td><td rowspan="5">外部接口</td><td>HCNetSDK.h</td><td>头文件</td><td></td></tr><tr><td>HCNetSDK.lib</td><td>LIB库文件</td><td></td></tr><tr><td>HCNetSDK.dll</td><td>DLL库文件</td><td></td></tr><tr><td>HCCore.lib</td><td>LIB库文件</td><td></td></tr><tr><td>HCCore.dll</td><td>DLL库文件</td><td></td></tr><tr><td rowspan="2">组件库</td><td>设备配置核心组件</td><td>HCCoreDevCfg.dll</td><td>DLL库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>预览组件</td><td>HCPreview.lib</td><td>LIB库文件</td><td>HCNetSDKCom文件夹</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="11"></td><td></td><td>HCPreview.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>回放组件</td><td>HCPlayBack.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>语音组件</td><td>HCVoiceTalk.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td></td><td>HCAlarm.lib</td><td>LIB 库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td rowspan="2">报警组件</td><td>HCAlarm.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>HCDisplay.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>行业应用管理配置组件</td><td>HCIndustry.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td rowspan="2">维护管理配置组件</td><td>HCGeneralCfgMgr.lib</td><td>LIB 库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>HCGeneralCfgMgr.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>RTSP 通讯库</td><td></td><td>StreamTransClient.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>转封装库</td><td></td><td>SystemTransform.dl</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>字符转码库</td><td></td><td>libiconv2.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>模拟能力集</td><td></td><td>LocalXml.zip</td><td>XML文件包</td><td></td></tr><tr><td>帧分析库</td><td></td><td>AnalyzeData.dll</td><td>DLL库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td rowspan="2">语音对讲库</td><td></td><td>Audiolntercom.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td></td><td>OpenAL32.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td rowspan="11">视频渲染库 播放库</td><td rowspan="4">核心库文件</td><td>PlayM4.h、WindowsPlayM4.h</td><td>头文件</td><td></td></tr><tr><td>PlayCtrl.lib</td><td>LIB库文件</td><td></td></tr><tr><td>PlayCtrl.dll</td><td>DLL库文件</td><td></td></tr><tr><td>SuperRender.dll</td><td>DLL库文件</td><td></td></tr><tr><td>音频渲染库</td><td>AudioRender.dll</td><td>DLL库文件</td><td></td></tr><tr><td>小鹰眼库</td><td>EagleEyeRender.dll</td><td>DLL库文件</td><td></td></tr><tr><td>GPU硬解码库</td><td>HWDecode.dll</td><td>DLL库文件</td><td></td></tr><tr><td>鱼眼库</td><td>MP_Render.dll</td><td>DLL库文件</td><td></td></tr><tr><td>视频后处理库</td><td>MP_VIE.dll</td><td>DLL库文件</td><td></td></tr><tr><td>测温信息抓图库</td><td>YUVProcess.dll</td><td>DLL库文件</td><td></td></tr><tr><td>DirectX 组件库</td><td>D3DCompiler_43.dl</td><td>DLL库文件</td><td></td></tr></table></body></html>  

表 1.2 Linux SDK 组件  


<html><body><table><tr><td rowspan="3">网络通讯库</td><td rowspan="2">外部接口</td><td>HCNetSDK.h</td><td>头文件</td><td></td></tr><tr><td>libhcnetsdk.so</td><td>SO库文件</td><td></td></tr><tr><td>核心组件</td><td>libHCCore.so</td><td>SO库文件</td><td></td></tr><tr><td rowspan="3">组件库</td><td>设备配置核心组件</td><td>libHCCoreDevCfg.so</td><td>SO库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>预览组件</td><td>libHCPreview.so</td><td>SO库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>回放组件</td><td>libHCPlayBack.so</td><td>SO库文件</td><td>HCNetSDKCom文件夹</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="7"></td><td>语音组件</td><td>libHCVoiceTalk.so</td><td>SO 库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>报警组件</td><td>libHCAlarm.so</td><td>SO 库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>显示组件</td><td>libHCDisplay.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>行业应用管理配置组件</td><td>libHCIndustry.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>维护管理配置组件</td><td>libHCGeneralCfgMgr.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td></td><td>libhpr.so</td><td>SO库文件</td><td></td></tr><tr><td>hpr库 RTSP 通讯库</td><td>libStreamTransClient.so</td><td>SO 库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>转封装库</td><td></td><td>libSystemTransform.so</td><td>SO 库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>字符转码库</td><td></td><td>libiconv2.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>帧分析库</td><td></td><td>libanalyzedata.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td rowspan="4">播放库</td><td rowspan="2">核心库文件</td><td>PlayM4.h、LinuxPlayM4.h</td><td>头文件</td><td></td></tr><tr><td>libPlayCtrl.so</td><td>SO库文件</td><td></td></tr><tr><td>视频渲染库</td><td>libSuperRender.so</td><td>SO库文件</td><td></td></tr><tr><td>音频渲染库</td><td>libAudioRender.so</td><td>SO库文件</td><td></td></tr></table></body></html>  

本版本的设备网络 SDK开发包中包含以上各个组件,HCNetSDK.dll、HCCore.dIl 必须加载(对于 Linux SDK,即 libhcnetsdk.so、libHCCore.so），其他组件，用户可以根据需要选择其中的一部分或者全部，以下将对各个组件在 SDK 中的作用和使用条件分别说明。  

$\bullet$ 网络通讯库：设备网络 SDK 的主体，主要用于网络客户端与各类产品之间的通讯交互，负责远程功能调控, 远程参数配置及码流数据的获取和处理等。设备网络 SDK V5.0 针对产品应用业务进行细化，对之前版本的 SDK 的功能模块进行组件化，其中外部接口（HCNetSDK.dll）仍然保持和设备网络 SDK V4.x版本保存一致(向下兼容)，其他单独的业务功能（预览、回放等）可以加载单独的模块组件，多个业务功能也可以组合使用。更新 SDK 时，HCNetSDK.dll、HCCore.dll 以及 HCNetSDKCom 文件夹下的功能组件库文件都需要更新加载，且 HCNetSDKCom 文件夹名不能修改。  

 hpr 库：网络通讯库的依赖库，Linux SDK 使用时和网络通讯库同时加载。  
 RTSP 通讯库：支持 RTSP 传输协议的网络库。当需要对支持 RTSP 协议的产品进行取流等操作时就必须加载该项组件。  
 转封装库：库的功能可以分为两种：一种是将标准码流转换成采用我们公司封装格式的码流。当用户需要对支持 RTSP 协议的产品捕获采用本公司封装格式的码流数据时（即当设置 NET_DVR_RealPlay_V40接口中的回调函数捕获数据或者调用 NET_DVR_SetRealDataCallBack 接口捕获数据时）必须加载该组件。另一种功能是能将标准码流转换成其他格式的封装，如 3GPP、PS 等。例如，当用户需要对支持 RTSP协议的产品实时捕获指定封装格式的码流数据（对应的 SDK 接口为 NET_DVR_SaveRealData）时必须加载该项组件。  
$\bullet$ 语音对讲库：用于语音对讲时通过声卡采集数据并按照指定的编码格式编码码流或者解码播放音频码流数据（不带封装格式的码流数据）。V4.2.2.5 及以前版本 SDK 均采用 windows API 实现相关功能。之后版本默认使用语音对讲库的方式，通过接口 NET_DVR_SetSDKLocalCfg 可以选择之前的 windows API模式。OpenAL32.dll 为依赖库，语音对讲库模式下必须加载。Windows64 位或者 Linux 系统下无语音对讲功能。  

$\bullet$ 字符转换库：电脑字符集和设备字符集不一致时,SDK内部需要进行字符编码转换,SDK 默认使用libiconv库进行类型转换。如果用户不想使用 libiconv 编码库，可以调用 NET_DVR_SetSDKLocalCfg (类型:NET_SDK_LOCAL_CFG_TYPE_BYTE_ENCODE)设置字符转码回调函数，将用户自己的字符编码接口告知SDK，然后 SDK 将使用用户提供的字符编码接口进行字符串处理。  

 模拟能力集：如果需要获取设备能力集（NET_DVR_GetDeviceAbility），建议调用 NET_DVR_SetSDKLocalCfg启用模拟能力集，此时需要加载 LocalXml.zip（要求和网络通讯库放在同一个目录下）。  

$\bullet$ 帧分析库：用于分析视音频帧数据，调用 NET_DVR_SetESRealPlayCallBack、NET_DVR_SetPlayBackESCallBack 设置裸码流回调函数等接口时，必须加载该库文件。  

 播放库：主要用于对实时码流数据进行解码显示（实现预览功能）和对录像文件进行回放解码等。用户如果需要在 SDK 内部进行对实时流和录像码流播放显示时（即 NET_DVR_RealPlay_V40 接口的第二个结构体参数的播放句柄设置成有效句柄时）必须加载该组件，而如果用户仅需要用网络通讯库捕获到数据后再外部自行处理就不需要加载该组件，这种情况下用户在外部自行解码将更灵活，可参见软解码库函数说明《播放器 SDK 编程指南》。  

# 2 SDK 版本更新  

## Version 5.2.6.25 (build20170104)  

$\bullet$ 网络摄像机 V5.4.5 安全版本升级  
 NET_DVR_EZVIZ_ACCESS_CFG(EZVIZ 接入参数配置)使用 32 个字节新增参数：byVerificationCode(萤石云验证码)。  
 NET_DVR_FindDVRLog_V30(日志查询)和 NET_DVR_LOG_V30(日志查询结果)中 dwMinorType 新增操作日志次类型：MINOR_REMOTE_MODIFY_VERIFICATION_CODE(修改平台的验证码)。  
$\bullet$ 新增错误码（对应接口：NET_DVR_GetLastError 和 NET_DVR_GetErrorMsg）：1111、1112。  
$\bullet$ 设备协议接入能力集(AccessProtocolAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)扩展，<EzvizParam>(萤石云参数能力)新增子节点：<VerificationCode>(配置验证码能力)。  

### Version 5.2.6.15 (build20161221)  

$\bullet$ 网络摄像机 V5.4.5 FF 车牌  
$\bullet$ NET_DVR_EVENT_TRIGGER(事件联动配置)使用 1 个字节新增参数：byDirection(触发方向)。  
$\bullet$ 事件触发能力集(EventTriggersCap)中<EventTriggerCapType>(事件触发联动类型)新增节点：<direction>(触发方向)。  
 ITS_OVERLAP_ITEM_TYPE(字符叠加类型)新增枚举类型：OVERLAP_ITEM_CAR_VALIDITY(置信度)。  
 NET_DVR_VEHICLE_INFO_CFG(车辆信息查询结果)使用 1 个字节新增参数：byMatchingResult(授权或非授权名单匹配结果)。  
$\bullet$ 车辆信息查询结果能力集(VehicleInfoResultCap)中<VehicleInfoResult>(车辆信息结果)新增子节点：<isSupportMatchingResult>(是否支持授权或非授权名单匹配结果)。  
$\bullet$ 事件能力集(EventAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)中<VehicleDetection>(车辆侦测能力)和<HVTVehicleDetection>(混行检测能力)扩展：1) <GuardCfg>(布防参数能力)新增子节点：<direction>(触发方向)。2) <OverlapCfg>(字符叠加能力)中<OverlapItemParam>- $\cdot\!>\!<$ SingleItem>-><itemType>(字符叠加类型)新增取值：validity(置信度)。  

### Version 5.2.5.40 (build20161102)  

$\bullet$ 网络摄像机 V5.4.4  
$\bullet$ 新增软件服务能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_SOFTWARE_SERVICE_CAPABILITIES。  
$\bullet$ 新增软件服务配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_SOFTWARE_SERVICE、NET_DVR_SET_SOFTWARE_SERVICE。  
 NET_DVR_COMPRESSION_INFO_V30（码流压缩参数）的参数 byResolution(分辨率)新增取值：$150{-}8208^{*}3072$ 、151-4096\*1536、152-6912\*2800、153-3456\*1400。  
$\bullet$ NET_DVR_CAMERAPARAMCFG_EX(前端参数配置)中 byCaptureModeN、byCaptureModeP(视频输入模式)新增取值： $141–2688^{*}1520@12.5\mathsf{f p s}\,$ 。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20，对应接口：NET_DVR_GetDeviceAbility，能力集类型：IPC_FRONT_PARAMETER_V20)扩展，<captureModePWithIndex>和<captureModeNWithIndex>(视频输入模式)增加取值：141-2688\*1520@12.5fps。  

$\bullet$ 设备软硬件能力集(BasicCapability，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_SOFTHARDWARE_ABILITY)扩展，<NeedReboot>(是否需要重启)中新增子节点：<ThirdStream>(开启三码流服务是否需要重启)。  

### Version 5.2.5.35 (build20161024)  

$\bullet$ 网络摄像机 V5.4.30  
$\bullet$ 新增主控版本信息功能（对应接口：NET_DVR_GetSTDConfig）：命令：NET_DVR_GET_FIRMWARE_VERSION。  
$\bullet$ 设备系统总能力集(DeviceCap，对应接口：NET_DVR_GetSTDAbility，能力集类型：NET_DVR_GET_SYSTEM_CAPABILITIES)扩展，新增节点：<isSupportFirmwareVersionInfo>(是否支持获取主控版本信息)。  
 NET_VCA_FACESNAPCFG(人脸抓拍规则参数)使用 12 个保留字节新增参数：dwFaceFilteringTime(人脸停留时间过滤)。  
$\bullet$ 智能通道分析能力集(VcaChanAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)扩展，<FaceSnap>(人脸抓拍能力)新增子节点：<faceFilteringTime>(人脸停留时间过滤)。  
 NET_DVR_FIND_PICTURE_PARAM(图片查找条件)和 NET_DVR_FIND_PICTURE_V40(图片查找结果)中byFileType(图片类型)分别新增取值： $0{\times}25.$ -人脸抓拍。  
$\bullet$ JPEG 抓图能力集(JpegCaptureAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_JPEG_CAP_ABILITY)扩展，<supportFileType>(支持图片类型)新增取值：faceSnap(人脸抓拍)。  
 NET_ITC_POST_MPR_PARAM(卡口多帧检测触发参数)和 NET_IPC_POST_HVT_PARAM(IPC 混行卡口触发参数)分别使用 16 个保留字节新增参数：struSnapLine(抓拍线)。  
$\bullet$ 事件能力集(EventAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)扩展：1) <VehicleDetection>-><TriggerCfg>-> <TriggerParam>中的<PostMPR>(卡口多帧检测触发参数)新增子节点：<SnapLine>(抓拍线)。2) <HVTVehicleDetection>-><TriggerCfg>-> <TriggerParam>中的<PostIPCHVT>(卡口多帧检测触发参数)新增子节点：<SnapLine>(抓拍线)。  
 NET_DVR_ANR_ARMING_HOST(断网续传主机信息)使用 1 个保留字节新增参数：byConfirmMechanismEnabled(是否开启确认机制方式布防连接)。  
 NET_DVR_SETUPALARM_PARAM(报警布防参数)中参数 bySupport 新增取值：Bit1 表示是否启用断网续传数据确认机制。  
 NET_DVR_PDC_ALRAM_INFO(客流量统计结果参数)和 NET_DVR_HEATMAP_RESULT(热度图上传结果)分别使用 1 个保留字节新增参数：byBrokenNetHttp(断网续传标志位)。  
$\bullet$ 设备软硬件能力集(BasicCapability，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_SOFTHARDWARE_ABILITY)扩展，新增节点：<isSupportConfirmMechanism>(断网续传数据确认机制)。  

### Version 5.2.3.5 (build20160622)  

$\bullet$ 网络摄像机 V5.4.20  
$\bullet$ 新增 MAC 地址过滤配置能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_MACFILTER_CAPABILITIES。  
$\bullet$ 新增 MAC 地址过滤配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_MACFILTER_CFG、NET_DVR_SET_MACFILTER_CFG。  

 NET_DVR_PDC_RULE_CFG_V42(客流量规则配置)扩展：  

1) 使用 5 个保留字节新增参数：byInterferenceSuppression(干扰抑制)、byEmailDayReport(客流日报表件上传使能)、byEmailWeekReport(客流周报表邮件上传使能)、byEmailMonthReport(客流月报表邮件传使能)、byEmailYearReport(客流年报表邮件上传使能)。2) byOSDEnable(客流统计 OSD 显示是否启用)新增取值：2-进入、3-离开。$\bullet$ 设备软硬件能力集(BasicCapability，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_SOFTHARDWARE_ABILITY)扩展，新增节点：<HRUDP>(HRUDP 可靠传输能力)。$\bullet$ 智能通道分析能力集(VcaChanAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)，<PDC>(客流量统计能力)扩展：1) <OSD>(OSD 能力)新增子节点：<OSDType>(显示类型)。2) 新增子节点：<EmailReport>(邮件上传报告)。$\bullet$ 新增错误码（对应接口：NET_DVR_GetLastError 和 NET_DVR_GetErrorMsg）：182、834。  

### Version 5.1.6.21 (build20160401)  

$\bullet$ 网络摄像机 V5.4.0  

$\bullet$ 新增获取断网续传主机信息功能（对应接口：NET_DVR_GetSTDConfig）：命令：NET_DVR_GET_ANR_ARMING_HOST。  
$\bullet$ 新增清空前端参数功能（对应接口：NET_DVR_RemoteControl）：命令：NET_DVR_CLEAR_IPC_PARAM。  
 NET_DVR_STORAGE_DETECTION_ALARM(存储智能检测报警信息)使用 1 个保留字节新增参数：fResidualLife(SD 卡预计剩余寿命)。  
$\bullet$ 设备所有编码能力集(AudioVideoCompressInfo)扩展，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ENCODE_ALL_ABILITY_V20，<SmartCodecCap>(Smart 编码能力)新增子节点：<H265>(Smart265能力)，<supportCodeType>新增取值：H.265。  
$\bullet$ 设备通用能力集(对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)，其中前端参数动态能力集输入信息(CameraParaDynamicAbility)扩展：<VbrAverageCapDynamicLinkTo>(平均码率动态获取)中<codeType>新增取值：smart265。  
$\bullet$ 新增错误码：791。  

### Version 5.1.6.20 (build20160322)  

 E 系列网络高清智能球机 V5.3.14  
$\bullet$ 设备图像参数能力集(VideoPicAbility)扩展，<OSD>(OSD 能力)中新增子节点：<OSDCharactersNum >(OSD字符叠加长度限制)、<ChannelNumOverlySize ${>}|$ (通道名称长度限制)。  

### Version 5.1.6.7 (build20160125)  

$\bullet$ 网络摄像机 V5.3.8 FF 车牌识别  
$\bullet$ 新增 FTP 上传信息规整参数配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_FTPUPLOAD_CFG、NET_DVR_SET_FTPUPLOAD_CFG。  
$\bullet$ 新增 FTP 上传能力集（对应接口 NET_DVR_GetSTDAbility）：命令：NET_DVR_GET_FTP_CAPABILITIES。  
$\bullet$ 新增支持非授权名单布防时间配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_BLACKLST_SCHEDULE、NET_DVR_SET_VEHICLE_BLACKLST_SCHEDULE。  
$\bullet$ 新增支持非授权名单布防联动配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_BLACKLIST_EVENT_TRIGGER、NET_DVR_SET_VEHICLE_BLACKLIST_EVENT_TRIGGER。  
$\bullet$ 新增支持授权名单布防时间配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_WHITELST_SCHEDULE、NET_DVR_SET_VEHICLE_WHITELST_SCHEDULE。  
$\bullet$ 新增支持授权名单布防联动配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_WHITELIST_EVENT_TRIGGER、NET_DVR_SET_VEHICLE_WHITELIST_EVENT_TRIGGER。  
$\bullet$ 新增支持导入授权或非授权名单配置文件功能（对应接口：NET_DVR_UploadFile_V40）：文件类型：UPLOAD_VEHICLE_BLACKWHITELST_FILE。  
$\bullet$ 新增支持导出授权或非授权名单配置文件功能（对应接口：NET_DVR_StartDownload）：文件类型：NET_SDK_DOWNLOAD_VEHICLE_BLACKWHITELST_FILE。  
 NET_ITC_POST_MPR_PARAM(卡口多帧检测(MPR)触发参数)使用 3 个保留字节新增参数：byRoadType(道路模式)、wCustomDelayTime(自定义抓拍延时时间)。  
 NET_DVR_DAYNIGHT(日夜转换功能参数)中 byDayNightFilterType(日夜切换模式)新增取值：5-自动模式 2（无光敏）。  
$\bullet$ 事件触发能力集(EventTriggersCap)新增节点：<BlackListTriggerCap>(非授权名单事件触发能力)、<WhiteListTriggerCap>(授权名单事件触发能力)。  
$\bullet$ 设备通用能力集(对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)，其中EventAbility(事件能力集)扩展，<TriggerCfg>(触发参数配置能力)中节点<PostMPR>(卡口多帧检测)新增子节点：RodeType(道路类型)。  
$\bullet$ 设备前端参数能力集(CAMERAPARA)扩展，<DayNightFilter>(日夜切换能力)中<DayNightFilterType>(日夜切换模式)的子节点<Range>(取值范围)新增取值：5-自动模式 2（无光敏）。  

### Version 5.1.5.10 (build20151210)  

 64 分离便携式网络摄像机 DS-2CD6416C1-GLT V5.3.4  
$\bullet$ 新增校时功能（对应接口：NET_DVR_SetDVRConfig）：命令：NET_DVR_SET_TIMECORRECT。  
$\bullet$ 新增 WIFI 热点参数配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_WIRELESSSERVER、NET_DVR_SET_WIRELESSSERVER。  
$\bullet$ 新增获取 WIFI 热点连接设备列表信息功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_GET_CONNECT_LIST。  
$\bullet$ 新增 OSD 电池电量显示配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_OSD_BATTERY_POWER_CFG、NET_DVR_SET_OSD_BATTERY_POWER_CFG。  
$\bullet$ 新增获取热点连接设备列表信息能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_CONNECT_LIST_CAPABILITIES。  
$\bullet$ 新增 OSD 电池电量显示参数能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_OSD_BATTERY_POWER_CFG_CAPABILITIES 。  
 NET_DVR_WIFIETHERNET(无线网口参数)使用 1 个保留字节新增参数：byCloseWifi(是否关闭 wifi 连接)。  
$\bullet$ WIFI 热点配置能力集(WirelessServer)新增节点：<isMutexWithWireless>(互斥能力)。  
$\bullet$ 设备软硬件能力集(BasicCapability)扩展，新增节点<isSupportTimeCorrect >(是否支持NET_DVR_SET_TIMECORRECT 校时操作)。  
$\bullet$ 设备无线设备网络能力集(NetworkSetting)扩展，<WirelessSetting $\times($ (无线网络配置)中新增子节点：<closeWifi >(是否支持关闭 wifi)、<mutexAbility >(和 wifi 热点互斥)。  

### Version 5.1.5.7 (build20151125)  

$\bullet$ 网络摄像机 V5.3.6  
$\bullet$ 新增内置补光灯配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_SUPPLEMENTLIGHT、NET_DVR_SET_SUPPLEMENTLIGHT。  
$\bullet$ 新增获取用户在线信息功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_GET_ONLINEUSER_INFO。  
$\bullet$ 新增存储健康检测联动配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_STORAGEDETECTION_EVENT_TRIGGER、NET_DVR_SET_STORAGEDETECTION_EVENT_TRIGGER。  
$\bullet$ 新增存储健康检测布防时间配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_STORAGEDETECTION_SCHEDULE、NET_DVR_SET_STORAGEDETECTION_SCHEDULE。  
$\bullet$ 新增存储健康状态查询功能（对应接口：NET_DVR_GetSTDConfig）：命令：NET_DVR_GET_STORAGEDETECTION_STATE。  
$\bullet$ 新增存储侦测读写锁配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_STORAGEDETECTION_RWLOCK、NET_DVR_SET_STORAGEDETECTION_RWLOCK。  
$\bullet$ 新增存储侦测解锁配置功能（对应接口：NET_DVR_SetSTDConfig）：命令：NET_DVR_SET_STORAGEDETECTION_UNLOCK。  
$\bullet$ 新增内置补光灯配置能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_SUPPLEMENTLIGHT_CAPABILITIES。  
$\bullet$ 新增存储健康检测布防时间能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_STORAGEDETECTION_SCHEDULE_CAPABILITIES 。  
$\bullet$ 新增存储侦测读写锁配置能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_STORAGEDETECTION_RWLOCK_CAPABILITIES  
$\bullet$ 新增存储侦测解锁配置能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_STORAGEDETECTION_UNLOCK_CAPABILITIES 。  
$\bullet$ 新增存储侦测报警上传功能（对应接口：NET_DVR_SetDVRMessageCallBack_V31 和NET_DVR_StartListen_V30）：COMM_ALARM_STORAGE_DETECTION。  
 NET_DVR_FindDVRLog_V30(日志查询)和 NET_DVR_LOG_V30(日志查询结果)中 dwMinorType 新增异常日志次类型：MINOR_SDCARD_ABNORMAL(SD 卡不健康)、MINOR_SDCARD_DAMAGE(SD 卡损坏)。  
$\bullet$ 新增支持 WIFI 热点连接设备信息查询功能（对应接口 NET_DVR_StartRemoteConfig 和NET_DVR_GetNextRemoteConfig）：命令：NET_DVR_GET_WIFI_CLIENT_LIST_INFO。  
 NET_DVR_GBT28181_ACCESS_CFG(GBT28181 协议接入配置)使用 1 个保留字节新增参数：byProtocolVersion(协议版本)。  
 NET_DVR_JPEG_CAPTURE_CFG 和 NET_DVR_JPEG_CAPTURE_CFG_V40(设备抓图配置)分别使用 1 个保留字节新增参数：byStreamType(抓图码流类型)。  
 FTP 参数配置扩展：1) NET_DVR_FTPCFG(FTP 上传参数)使用 1 个保留字节新增参数：byPicArchivingInterval(图片归档间隔)。2) NET_DVR_FTPCFG_V40(FTP 上传参数扩展)使用 2 个保留字节新增参数：byPicArchivingInterval(图片归档间隔)、byPicNameRuleType(图片命令规则类型)。3) NET_DVR_PICTURE_NAME_EX(图片命名规则)使用 32 个保留字节新增参数：byPicNamePrefix[PICNAME_PREFIX](图片名自定义前缀)。  
 NET_DVR_SUPPLEMENTLIGHT(补光灯参数配置)使用 2 个保留字节新增参数：wFilteringTime(过滤时间)。  
 NET_DVR_SINGLE_HD(设备硬盘信息)扩展，dwHdStatus(硬盘状态)新增取值：16-已锁定，byHDAttr(硬盘  

状态)新增取值：4-不可读写。  
 NET_VCA_DEV_ABILITY(智能设备能力集)使用 3 个保留字节新增参数：bySmartRoadDetectionNum(SMART事件 $\mathbf{+},$ 道路监控通道个数)、bySmartFaceDetectionNum(SMART 事件 $^+,$ 人脸侦测通道个数)、bySmartHeatMapNum(SMART 事件 $^+$ 热度图通道个数)。  
 VCA_CHAN_ABILITY_TYPE(智能通道能力类型)新增枚举类型：VCA_SMART_ROAD_DETECTION(SMART 事件+道路监控)、VCA_SMART_FACE_DETECTION(SMART 事件 $^+.$ 人脸侦测)、VCA_SMART_HEATMAP(SMART 事件 $^+$ 热度图)。  
 NET_DVR_WIFI_CFG_EX(WIFI 无线参数)中 wpa_psk 结构体使用 69 个保留字节新增参数：sNewKeyInfo[WIFI_WPA_PSK_MAX_HEXKEY_LENGTH](新类型密钥)、byKeyType(密钥类型)。  
$\bullet$ JPEG 抓图能力集(JpegCaptureAbility)扩展，<SchedCapture>(抓图计划)新增子节点：<AdvancedParam>(抓图高级参数配置)。  
$\bullet$ 设备软硬件能力集(BasicCapability)新增节点：<isSupportOnLineUser>(设备支持在线用户获取功能)。  
$\bullet$ 设备网络应用参数能力集(NetAppAbility)扩展，<FTP>(FTP 能力)新增子节点：<picNameRuleType>(图片命令规则类型)、<picNamePrefix>(自定义前缀长度)、<notSupportSymbol>(自定义前缀支持符号)。  
$\bullet$ 设备前端参数能力集(CAMERAPARA)扩展，<ISPAdvanceCfg>(ISP 前端参数配置)中子节点<ISPCfgSupport>(支持参数)新增取值：saturationLevel(饱和度)。  
$\bullet$ 设备无线设备网络能力集(NetworkSetting)新增节点：<support64bitKey>(是否支持 64 位十六进制密码)。  
$\bullet$ 协议能力集扩展：1) Smart 能力集(SmartCap)新增节点：<isSupportStorageDetection>(存储健康检测能力)。2) 事件触发能力集(EventTriggerCap)中<EventTriggerCapType>(事件触发联动类型)新增节点：<StorageDetectionTriggerCap>(存储健康检测联动方式)。3) 外设配置能力集(ExternalDevice)新增节点：<filteringTime>(过滤时间)。4) 视频流能力集(StreamingChannel)中<Video>(视频能力)新增子节点：<H265Profile>(H.265 编码)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)扩展：1) EventAbility(事件能力集)扩展，<VehicleDetection>(车辆侦测能力)中节点<mutexAbility>(互斥能力)新增取值：heatMap(热度图)。2) VcaDevAbility(智能设备能力集)扩展，新增节点：<SmartRoadDetectionChanNum>(SMART 事件 $^{+}$ 道路监控通道个数)、<SmartFaceDetectionChanNum>(SMART 事件 $^{\cdot+}$ 人脸侦测通道个数)、<SmartHeatMapChanNum>(SMART 事件 $^+.$ 人脸侦测通道个数)。3)VcaCtrlAbility(智能通道控制能力集)扩展,新增节点：<VcaCtrlTypeEntry>(SMART事件 $^{+}$ 道路监控、SMART事件 $\mathbf{+}.$ 人脸侦测、SMART 事件 $^+$ 热度图)。4) HardDiskAbility(磁盘相关能力集)扩展，<hdAttribute>(硬盘状态)新增取值：4-不可读写。5) 设备 GBT28181 能力集(GBT28181AccessAbility)新增节点：<protocolVersion>(协议版本)。  

### Version 5.1.3.25 (build20150916)  

$\bullet$ 网络摄像机 V5.3.4 FF 车牌识别  
$\bullet$ 新增全部车辆检测名单布防联动配置功能（对应接口：NET_DVR_GetSTDConfig 和NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_ALLLIST_EVENT_TRIGGER、NET_DVR_SET_VEHICLE_ALLLIST_EVENT_TRIGGER。  
$\bullet$ 新增其他车辆检测名单布防联动配置功能（对应接口：NET_DVR_GetSTDConfig 和NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_OTHERLIST_EVENT_TRIGGER、NET_DVR_SET_VEHICLE_OTHERLIST_EVENT_TRIGGER。  
 NET_DVR_FIND_PICTURE_PARAM(图片查找条件)、NET_ITC_PLATE_RECOG_PARAM(牌识参数)和NET_DVR_PLATE_INFO(交通抓拍结果)中分别新增取值：3- 欧洲&俄罗斯(EU&CIS)。  
 NET_DVR_GetUploadState(获取文件上传的进度和状态)返回状态值新增类型：19- 文件格式不正确、20-文件内容不正确。  
$\bullet$ 事件触发能力集(EventTriggersCap)新增节点：<AllVehicleListTriggerCap>(全部车辆检测名单触发能力)、<OtherVehicleListTriggerCap>(其他车辆检测名单触发能力)。  
$\bullet$ JPEG 抓图能力集(DEVICE_JPEG_CAP_ABILITY)扩展，<FindPicInfo>(图片检索)中节点<region>(国家区域)新增取值：EU&CIS(欧洲&俄罗斯)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中事件能力(EventAbility)扩展：1)<VehicleDetection>(车辆侦测能力)中新增节点:<autoBuildRecogArea>(客户端界面自动生成识别区域)、<brokenNetHttp>(车辆识别是否支持断网续传)。2) <VehicleDetection>(车辆侦测能力)中<PlateRecogParam>(牌识参数)的子节点新增取值：EU&CIS(欧洲&俄罗斯)。  
$\bullet$ 复用接口，新增支持：1)非授权名单布防联动配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_BLACKLIST_EVENT_TRIGGER、NET_DVR_SET_VEHICLE_BLACKLIST_EVENT_TRIGGER。2)授权名单布防联动配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_WHITELIST_EVENT_TRIGGER、NET_DVR_SET_VEHICLE_WHITELIST_EVENT_TRIGGER。3)导入授权或非授权名单配置文件功能（对应接口：NET_DVR_UploadFile_V40）：文件类型：UPLOAD_VEHICLE_BLACKWHITELST_FILE。4)导出授权或非授权名单配置文件功能（对应接口：NET_DVR_StartDownload）：文件类型：NET_SDK_DOWNLOAD_VEHICLE_BLACKWHITELST_FILE。5)能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_TRAFFIC_CAP(抓拍相关能力集)。  

### Version 5.1.3.20 (build20150831)  

 E 系列网络高清智能球 V5.3.9  
$\bullet$ NET_DVR_PTZ_BASICPARAMCFG(PTZ 基本参数配置)使用 1 个保留字节新增参数：byPTZMotionTrack(启用运动跟踪)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中 PTZ 能力(PTZAbility)扩展，<BasicParamCfg>(云台基本参数能力)中新增节点：<PTZMotionTrack>(运动跟踪能力)。  

### Version 5.1.3.20 (build20150831)  

$\bullet$ 网络摄像机 V5.3.5  
$\bullet$ 新增获取客流统计表示推荐值功能（对应接口：NET_DVR_GetSTDConfig）：命令：NET_DVR_GET_PDC_RECOMMEND  
$\bullet$ 新增客流数据清除操作功能（对应接口：NET_DVR_STDControl）：命令：NET_DVR_REMOVE_FLASHSTORAGE  
$\bullet$ 新增能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_COUNTING_CAPABILITIES(客流量统计能力集)  
 NET_DVR_SETUPALARM_PARAM(报警布防参数)中参数 byBrokenNetHttp(断网续传类型)新增取值：bit1-客流统计、bit2-热度图统计。  
 NET_DVR_PDC_RULE_CFG_V42(客流量规则配置)使用 2 个保留字节新增参数：byDataUploadCycle(客流量检测数据上传周期)、bySECUploadEnable(每秒上传机制使能)。  
 NET_DVR_HEATMAP_INFO(热度图数据查询结果)使用 8 个保留字节新增参数：dwHeatMapMaxValue(检测区域最高热度点人员活动时间)、dwHeatMapMinValue(检测区域最低热度点人员活动时间)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中智能通道分析能力集(VcaChanAbility)扩展：1) <PDC>(客流量能力)新增子节点：<brokenNetHttp>(是否支持断网续传)、<SecUploadEnable>(每秒上传机制使能)、<DataUploadCycle>(客流量检测数据上传周期)、<isSupportRecommendedValue>(推荐值)、<isSupportFlashRemoveCouting>(清除 Flash 中的客流数据统计)。2) <HeatMapDetection>(热度图能力)新增子节点：<brokenNetHttp>(是否支持断网续传)。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)扩展，新增节点<BrokenNetHttpSupport >(支持断网续传的功能)。  
$\bullet$ 新增错误码：179  

### Version 5.1.3.13 (build20150812)  

$\bullet$ 网络高清球机 V5.3.10DF8523IW、DF8223IW、DE3204SW-D 等  
$\bullet$ 新增温湿度配置能力集（对应接口：NET_DVR_GetSTDAbility）:能力集类型：NET_DVR_GET_THSCREEN_CAPABILITIES。  
$\bullet$ 新增温湿度配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_THSCREEN、NET_DVR_SET_THSCREEN。  
$\bullet$ 新增温湿度屏幕校时功能（对应接口：NET_DVR_STDControl）：命令：NET_DVR_THSCREEN_TIMING。  
$\bullet$ 新增校准 GPS 经纬度能力集（对应接口：NET_DVR_GetSTDAbility）:能力集类型：NET_DVR_GET_REVISE_GPS_CAPABILITIES。  
$\bullet$ 新增校准 GPS 经纬度配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）:能力集类型：NET_DVR_GET_REVISE_GPS、NET_DVR_SET_REVISE_GPS。  
 NET_DVR_EMAILCFG_V30(邮件参数配置)使用 1 个保留字节新增参数：byStartTLS(是否启用 StartTLS)。  
$\bullet$ NET_DVR_PICCFG_V30 和 NET_DVR_PICCFG_V40(通道图像参数)扩展，byFontSize(字体大小)新增取值：$4{-}24^{\ast}24$ (中) $|/12^{*}24|$ (英)，byAlignment(对齐方式)新增取值：2-左对齐。  
$\bullet$ NET_DVR_AUXILIARY_DEV_UPGRADE_PARAM(辅助设备升级条件)中 byDevType(升级设备类型)新增取值：1-机芯。  
$\bullet$ 设备图像参数能力集(DEVICE_VIDEOPIC_ABILITY)扩展，<FontSize>(字体大小)节点新增取值： $24^{*}24$ ，<alignment >(对齐方式)新增取值：alignLeft。  
$\bullet$ 设备网络应用参数能力(DEVICE_NETAPP_ABILITY)扩展，<Email>新增子节点：<enableStartTLS>(邮件支持启用 TSL)。  
$\bullet$ 设备所有编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)扩展，<DynamicAbility>中<dynamicAbilityLinkTo>新增取值：vbrAverageCap(视频平均码率)。  

### Version 5.1.3.10 (build20150720)  

$\bullet$ 网络摄像机 V5.3.4  
$\bullet$ 新增外设配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_EXTERNALDEVICE、NET_DVR_SET_EXTERNALDEVICE。  
$\bullet$ 新增外设配置能力集（对应接口：NET_DVR_GetSTDAbility）:能力集类型：NET_DVR_GET_EXTERNALDEVICE_CAPABILITIES。  
 NET_DVR_CAMERAPARAMCFG_EX(前端参数配置)扩展，byIrisMode(光圈模式)新增取值：6-HIK 11-40mmF1.7 (HV1140P-8MPIR)、7-HIK 2.7-12mm F1.2（TV2712P-MPIR）。  
 NET_DVR_UNATTENDED_BAGGAGE_REGION(物品遗留侦测配置)使用 3 个保留字节新增参数：wTimeThreshold(时间阈值)、byTimeThresholdMode(使用的时间阈值字段类型)。  
 NET_DVR_ATTENDED_BAGGAGE_REGION(物品拿取侦测配置)使用 3 个保留字节新增参数：wTimeThreshold(时间阈值)、byTimeThresholdMode(使用的时间阈值字段类型)。  
$\bullet$ 设备前端参数能力(IPC_FRONT_PARAMETER_V20)扩展：1) <ExposureSet>(曝光时间)中<Range>(取值范围)新增取值：21-1/75、22-1/125、23-1/175、24-1/225、25-1/300、26-1/400。2) <IrisMode>(镜头类型)中<Range>：6-HIK 11-40mm F1.7 (HV1140P-8MPIR)、7-HIK 2.7-12mm F1.2（TV2712P-MPIR）。3) <Piris>(Piris 光圈镜头)中新增节点：<Piris6>、<Piris7>。  

### Version 5.1.1.21 (build20150616)  

$\bullet$ 网络摄像机 V5.3.3  
$\bullet$ 新增智能规则关联颜色设置功能（对应接口：NET_DVR_SetDVRConfig）：命令：NET_DVR_SET_VCA_RULE_COLOR_CFG。  
$\bullet$ 新增智能规则关联颜色查询功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_GET_VCA_RULE_COLOR_CFG。  
$\bullet$ 新增人员统计查询功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_FACECAPTURE_STATISTICS。  
$\bullet$ 新增人员统计报警上传功能（对应接口：NET_DVR_SetDVRMessageCallBack_V31）：COMM_FACECAPTURE_STATISTICS_RESULT。  
 NET_VCA_FACESNAPCFG(人脸抓拍配置)使用 1 个保留字节新增参数：byBackgroundPic(背景图上传使能)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中智能通道分析能力集(VcaChanAbility)扩展：1) 新增节点：<FaceCaptureStatistics>(人员统计能力)、<ColorFilter>(智能规则关联颜色配置能力)。2) <FaceSnap>(人脸抓拍能力)新增子节点：<backgroundPic>(背景图上传使能)。  

### Version 5.1.1.17 (build20150602)  

$\bullet$ 网络摄像机 V5.3.3 FF 车牌识别  

 NET_DVR_FIND_PICTURE_PARAM(图片查找条件)使用 2 个保留字节新增参数：byRegion(区域索引)、byCountry(国家索引)。  
$\bullet$ 触发模式配置(NET_ITC_TRIGGERCFG)中各种触发模式的 NET_ITC_PLATE_RECOG_PARAM(牌识参数)使用 1个保留字节新增参数：byRegion(区域索引)。  
$\bullet$ 交通抓拍结果上传(NET_ITS_PLATE_RESULT)中 NET_DVR_PLATE_INFO(车牌信息)使用 2 个保留字节新增参数：byRegion(区域索引)、byCountry(国家索引)。  
 NET_VCA_DEV_ABILITY(智能设备能力集)使用 2 个保留字节新增参数：bySmartNum(SMART 事件个数)、byVehicleNum(车辆检测通道个数)。  
 VCA_CHAN_ABILITY_TYPE(智能通道能力类型)新增枚举类型：VCA_SMART_EVENT(SMART 事件)、VCA_VEHICLE_DETECTION(车辆检测)。  
$\bullet$ JPEG 抓图能力集(DEVICE_JPEG_CAP_ABILITY)扩展，<FindPicInfo>(图片查找能力)新增节点：<region >(区域索引)、<country>(国家索引)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中事件能力(EventAbility)，<VehicleDetection>(车辆检测)和<HVTVehicleDetection>(混行卡口检测)中节点<PlateRecogParam>(车牌识别参数)分别新增子节点：<region>(区域索引)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中智能通道控制能力(VcaCtrlAbility)扩展:  

1) 新增节点：<VcaCtrlTypeEntry>(“SMART 事件”和“车辆检测事件”能力)。2) <NeedReboot>(是否需要重启)中<smartSwitchVcaType>(智能类型切换)新增取值：smartEvent,vehicleDetection。  

### Version 5.1.1.10 (build20150429)  

$\bullet$ 网络摄像机 V5.3.2  
$\bullet$ 新增取流预览强制刷新帧功能（对应接口：NET_DVR_STDControl）：命令：NET_DVR_STREAMING_REFRESH_FRAME  
$\bullet$ 新增视频流能力集（对应接口：NET_DVR_GetSTDAbility）:能力集类型：NET_DVR_GET_STREAMING_CAPABILITIES  
$\bullet$ 新增刷新帧能力集（对应接口：NET_DVR_GetSTDAbility）:能力集类型：NET_DVR_GET_REFRESHFRAME_CAPABILITIES。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)使用 3 个保留字节新增参数：bySmartCodec(是否启用Smart 编码)、wAverageVideoBitrate(平均码率)。  
 NET_DVR_LITESTORAGE(轻存储配置)使用 4 个保留字节新增参数：byLevel(等级参数)、byDefLowStorageTime(低等级模式下推荐天数)、byDefMediumStorageTime(中等级模式下推荐天数)、byDefHighStorageTime(高等级模式下推荐天数)。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)扩展，<NeedReboot>中新增子节点：<SmartCodec>(Smart 编码切换检测模式是否需要重启)。  
$\bullet$ 设备所有编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)扩展，<MainChannel>、<SubChannelEntry>、<Stream3>中分别新增子节点：<SmartCodecCap>(Smart 编码能力)，<VideoResolutionEntry>中新增子节点：<AverageVideoBitrate>(平均编码码率)。  
$\bullet$ 轻存储能力集(LiteStorage)扩展，新增节点：<level>(等级参数)、<DefStorageTime>(存储时间推荐值)。  

### Version 5.0.3.17 (build20150210)  

$\bullet$ 网络摄像机 V5.3.0、网络球机 V5.3.0  
$\bullet$ 新增物理倍率坐标配置功能（对应接口：NET_DVR_GetDVRConfig）：命令：NET_DVR_GET_PHY_RATIO、NET_DVR_SET_PHY_RATIO。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)中 byResolution(分辨率)新增取值： $86-640^{*}360$ 。  
 NET_DVR_FIND_PICTURE_PARAM(图片查找条件)中 byFileType(查找的图片类型)新增取值：0x1d- 取证事件。  
 NET_DVR_FIND_PICTURE 和 NET_DVR_FIND_PICTURE_V40(图片查找结果)分别使用 18 个保留字节新增参数：byEventSearchStatus(搜索状态，后面是否还有图片)、byRecogResult(车辆识别结果)，sLicense[16](车牌号码)。  
 NET_DVR_PRIVACY_MASKS_CFG(云台隐私遮蔽参数)使用 5 个保留字节新增参数：byCurZoomRatio(当前倍率使用字段)、fActiveZoomRatio(屏蔽倍率，精确到小数点 1 位)。  
 NET_DVR_PTZ_BASICPARAMCFG(PTZ 基本参数)使用 1 个保留字节新增参数：byManualControlSpeed(手控速度模式)。  
 NET_DVR_CHANNELSTATE_V30(通道状态信息)使用 4 个保留字节新增参数：dwAllBitRate(实际码率之和)。  
 VCA_CHAN_ABILITY_TYPE(智能能力类型)新增枚举类型：VCA_SMART_VEHICLE_DETECTION(SMART 事件 $^{\cdot+}$ 车辆检测)、VCA_SMART_HVT_DETECTION(SMART 事件 $^+$ 混行检测)。  
 NET_VCA_DEV_ABILITY(智能设备能力集)使用 2 个保留字节新增参数：bySmartVehicleNum(SMART 事件 $^+$ 车辆检测通道个数)、bySmartHVTNum(SMART 事件 $+$ 混行检测通道个数)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中智能通道控制能力(VcaCtrlAbility)扩展，新增节点：  

<VcaCtrlTypeEntry>(“SMART 事件 $^+$ 车辆检测”和“SMART 事件 $^+$ 混行检测”能力)、<defVcaType>(设备默认支持的异常行为识别类型)、<NeedReboot>(是否需要重启)。  

$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中 PTZ 能力(PTZAbility)扩展:1) <BasicParamCfg>(云台基本参数能力)中新增节点：<manualControlSpeed>(手控速度模式)。2) <PrivacyMaskCfg $>$ (云台隐私遮蔽)中新增节点：<curActiveZoomRatioType>(屏蔽倍率精确到小数点)。  
$\bullet$ JPEG 抓图能力集(DEVICE_JPEG_CAP_ABILITY)扩展，<supportFileType>(图片类型)新增取值：evidence(取证事件)。  
$\bullet$ 设备前端参数能力(IPC_FRONT_PARAMETER_V20)扩展：1) 新增视频制式与宽动态互斥能力节点：<CaptureModeIndex87>(1280\*960@50fps)、<CaptureModeIndex88>(1280\*960@60fps)、<CaptureModeIndex89>(1280\*960@100fps)、<CaptureModeIndex90>(1280\*960@120fps)。2) <WDR>(宽动态)中<mutexAbility >(互斥能力)新增取值：87-1280\*960@50fps,88-1280\*960@60fps,89-1280\*960@100fps,90-1280\*960@120fps。3) <FocusMode>(聚焦模式)新增节点：<physicsRatio>(物理倍率坐标范围)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力(EventAbility)扩展：1) 新增节点：<HVTVehicleDetection>(HVT 混行卡口能力)、<CurVehicleDetection>(获取当前触发模式)。2) <TraversingVirtualPlane>(越界侦测)，新增子节点：<recogRuleType>(运动方向判断方式)、<triggerRecord>(触发录像能力)，<mutexAbility>(互斥能力)新增取值：recordPlan(计划录像)。3) <FieldDetection>(区域入侵)，新增子节点：<triggerRecord>(触发录像能力)，<mutexAbility>(互斥能力)新增取值：recordPlan(计划录像)。  
$\bullet$ 设备网络应用参数能力集(DEVICE_NETAPP_ABILITY)扩展，新增节点：<allBitRate>(所有连接实际码率之和的参数能力)。  
$\bullet$ 设备编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)扩展，<VideoEncodeEfficiency>(视频编码复杂度能力)新增子节点：<EncodeTypeList>(编码类型列表，新增 H.265 类型对应复杂度取值)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中录像相关能力(RecordAbility)扩展，新增节点：<recordPlan>(计划录像互斥能力)。  
$\bullet$ 进入区域侦测能力集(RegionEntrance)、离开区域侦测能力集(RegionExiting)、徘徊侦测能力集(Loitering)、人员聚集侦测能力集(Group)、快速运动侦测能力集(RapidMove)、停车侦测能力集(Parking)、物品遗留侦测能力集(UnattendedBaggage)、物品拿取侦测能力集(AttendedBaggageCap)，<mutexAbility>(互斥能力)新增互斥类型：recordPlan(计划录像)。  

### Version 5.0.2.15 (build20141212)  

$\bullet$ 网络摄像机 V5.2.6、网络球机 V5.2.8  
$\bullet$ 新增监测点信息配置（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_MONITOR_LOCATION_INFO、NET_DVR_SET_MONITOR_LOCATION_INFO  
$\bullet$ 新增抓拍图片参数扩展配置（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_SNAPINFO_CFG_V40、NET_DVR_SET_SNAPINFO_CFG_V40  
$\bullet$ 新增测试功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_CLOUDSTORAGE_SERVER_TEST(云存储服务器测试)、NET_DVR_PHONE_NUM_TEST(电话号码测试)  
$\bullet$ 新增获取无线布防状态功能（对应接口：NET_DVR_GetDeviceStatus）：命令：NET_DVR_GET_REMOTECONTROL_STATUS  
$\bullet$ 新增获取轻存储能力集（对应接口：NET_DVR_GetSTDAbility）：命令：NET_DVR_GET_LITESTORAGE_CAPABILITIES  

$\bullet$ 新增轻存储配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：NET_DVR_GET_LITESTORAGE、NET_DVR_SET_LITESTORAGE  

$\bullet$ 新增获取车俩检测标定能力集（对应接口：NET_DVR_GetSTDAbility）：命令：NET_DVR_GET_VEHICLE_CAPABILITIES$\bullet$ 新增获取车辆检测标定功能（对应接口：NET_DVR_GetSTDConfig）：NET_DVR_GET_VEHICLE_CALIBRATION$\bullet$ 新增错误码：175、176、177 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)扩展：  
1) byAudioEncType(音频编码类型)新增取值：8- PCM。  
2) byEnableSvc(SVC 功能)新增取值：2-自动启用 SVC 功能。  
3) byAudioBitRate(音频码率)新增取值:7-40Kbps、8-48Kbps、9-56Kbps、10-80Kbps、11-96Kbps、12-112Kbps、  
13-144Kbps、14-160Kbps。  
4) byAudioSamplingRate(音频采样率)新增取值：3-48kHZ、4- 44.1kHZ、5-8kHZ。 NET_DVR_COMPRESSION_AUDIO(语音对讲参数)的 byAudioEncType(音频编码类型)新增取值：8- PCM。$\bullet$ 车牌识别扩展：  
1) NET_ITS_PICTURE_INFO(抓拍图片信息)使用 1 个保留字节新增参数：byCloseUpType(特写图类型)，参数 byType(数据类型)新增取值：8- 非机动车、9- 行人。  
2) NET_ITS_PLATE_RESULT(识别结果)的 byDetectType(检测方式)新增取值：0-车辆检测(IPC 内部的多帧识别)、5-混行检测。  
3) ITC_TRIGGERMODE_TYPE(触发模式)新增枚举类型：IPC_POST_HVT_TYPE(IPC 支持的 HVT)。  
4) NET_ITC_TRIGGER_PARAM_UNION(触发参数联合体)新增结构体参数：NET_IPC_POST_HVT_PARAM(IPC混行卡口参数)。  
5) NET_ITC_LANE_MPR_PARAM(多帧检测模式车道参数)使用 1 个保留字节新增参数：byCarDriveDirect(车辆行驶方向)。  
6) NET_DVR_GUARD_COND(车牌侦测计划配置条件)、NET_ITS_OVERLAPCFG_COND(字符叠加配置条件)分别使用 1 个保留字节新增参数：byRelateType(关联类型)。  
7) NET_DVR_FIND_PICTURE_PARAM(图片查找条件)使用 1 个保留字节新增参数：bySubHvtType(混行检测查找子类型)，byFileType(查找类型)新增取值：0x1c- 混行检测。 NET_DVR_CAMERAPARAMCFG_EX(前端参数配置)使用 1 个保留字节新增参数：byLensDistortionCorrection(镜头畸变校正)，byCaptureModeN、byCaptureModeP(视频输入模式)新增取值：  
91- 4000\*3000@20fps。 NET_DVR_SERVER_TEST_PARA(服务器测试参数)的 unionServerPara 新增结构体参数：struCloudStoragePara(云存储服务器测试参数)、struPhoneNumPara(电话号码测试参数)。$\bullet$ 客流量统计功能扩展：  
1) NET_DVR_PDC_RULE_CFG_V42(客流量规则配置)使用 17 个保留字节新增参数：byCurDetectType(当前检测区域类型)、struLine(检测线)。  
2) NET_DVR_RESET_COUNTER_CFG(统计数据清零参数)使用 1 个保留字节新增参数：byMode(生效模式)。  
3) CALIBRATE_TYPE(标定类型)新增枚举类型：PDC_LINE_CALIBRATE(PDC 线标定)。  
4) NET_DVR_CALIBRATION_PRARM_UNION(标定参数联合体)新增结构体参数：NET_DVR_PDC_LINE_CALIBRATION(PDC 线标定参数)。$\bullet$ 智能异常行为识别功能扩展：  
1) VCA_ABILITY_TYPE_EX(异常行为识别能力类型)新增枚举类型：EVENT_COMBINED_ABILITY(组合规则事件)。  
2) VCA_RULE_EVENT_TYPE_EX(异常行为识别事件类型)新增枚举类型：  

ENUM_VCA_EVENT_COMBINED_RULE(组合规则事件)。  

3) NET_VCA_EVENT_UNION(警戒规则参数联合体)新增结构体参数：NET_VCA_COMBINED_RULE(组合规则参数)。4) NET_VCA_TRAVERSE_PLANE(穿越警戒面参数)、NET_VCA_AREA(进入/离开区域参数)、NET_VCA_INTRUSION(入侵参数)、NET_VCA_RUN(快速移动参数)分别使用 1 个保留字节新增参数：byDetectionTarget(检测目标类型)。  
 NET_DVR_SECURITY_CFG(安全认证配置)使用 1 个保留字节新增参数：byIllegalLoginLock(开启登录锁定)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中智能通道分析能力(VcaChanAbility)扩展：1) <Behavior>(异常行为识别)，<EventType>(事件类型)新增子节点<CombinedRule>(组合规则)，<BehaviorRule>(异常行为识别规则)中<eventType>(事件类型)新增取值：combinedRule(组合规则)。2) <PDC>(客流量统计)，新增节点：<resetCounterMode>(重置统计模式)，<PDCRule>中新增子节点<Line>(检测线)，<Calibration>中新增子节点<calibLine>(支持标定线)。3) <TraversePlane>(穿越警戒面)、<EnterArea>(进入区域)、<ExitArea>(离开区域)、<Intrusion>(入侵参数)、<Intrusion>(快速移动参数)新增子节点：<detectionTarget >(检测目标类型)。  
 JPEG 抓图能力集(DEVICE_JPEG_CAP_ABILITY)扩展，<FindPicInfo>(查找图片信息)新增节点：<subHvtType>(混行检测子类型)，<supportFileType>(图片类型)新增取值：HvtVehicleDetection(混行检测)。  
$\bullet$ 设备前端参数能力(IPC_FRONT_PARAMETER_V20)扩展：1) 新增节点：<LensDistortionCorrection>(镜头畸变校正能力)。2) ${\tt{<W D R>}}$ (光圈模式)中<mutexAbility $>$ 新增取值：LensDistortionCorrection,52-2048\*1536@50fps,53-2048\*1536@60fps3) <captureModePWithIndex>、<captureModeNWithIndex>新增取值： $91{-}4000^{*}3000@20\mathsf{f p s}\,$ 。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力(EventAbility)扩展：1) 新增节点：<HVTVehicleDetection>(HVT 混行卡口能力)、<CurVehicleDetection>(获取当前触发模式)。2) <TraversingVirtualPlane>(越界侦测)、<FieldDetection>(区域入侵)中<mutexAbility>(互斥能力)新增取值：videoFrameRate50,videoFrameRate60。3) <VehicleDetection>(车辆侦测能力)，新增节点：<mutexAbility>(互斥能力)，<triggerMode>和<triggerType>新增取值：ipcHVT(IPC 混行卡口)，<LaneParam>中新增子节点：<carDriveDirection>(车辆行驶方向)，<OverlapCond>中新增子节点：<relateType>(关联类型)。  
$\bullet$ 设备网络应用参数能力集(DEVICE_NETAPP_ABILITY)扩展，<CloudStorage>(云存储能力)新增子节点：<Test>(测试能力)。  
$\bullet$ 设备无线网络能力集(DEVICE_NETWORK_ABILITY)扩展，新增节点：<MessageConfig>(短信相关参数配置)、<SendSms>(短信发送能力)，<WirelessSetting>新增子节点：<NotSupportAutoDNS>(DNS 自动能力)。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)，<NeedReboot>(是否需要重启)新增节点：<SwitchVehicleDetection>(车辆检测模式切换)、<SwitchHVTVehicleDetection>(混行车辆检测切换)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中安全认证配置能力(SecurityAbility)扩展，新增节点：<illegalLoginLock>(违法登录锁定)。  
$\bullet$ 设备所有编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)扩展：1) <AudioCompressInfo>新增子节点：<noiseFilterSupportSamplingRate>(环境噪声过滤支持的采样率)。2) <MainAudioEncodeType>、<SubAudioEncodeType>、<EventAudioEncodeType>、<Stream3AudioEncodeType>新增子节点：<MP2L2SamplingRate>、<MP2L2SamplingRate16kHZ>、<MP2L2SamplingRate32kHZ>、<MP2L2SamplingRate44.1kHZ>、<MP2L2SamplingRate48kHZ>、<PCMSamplingRate>。3) <MainChannel>、<SubChannelList>、<EventChannel>、<Stream3>新增子节点：<VideoFrameRate50>(高帧率 50)、<VideoFrameRate60>(高帧率 60)、<VideoFrameRate100>(高帧率 100)、<VideoFrameRate120>(高  

帧率 120)，<SvcFunEnable>(SVC 使能)新增取值：auto。  

$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO),其中 PTZ 能力(PTZAbility)扩展，<Patrol>中<dwelITime $>$ 和<speed>新增字段：default(默认值)，<PTZLOCK>中<supportFunction >新增取值：hvtVehicleDetection(HVT 混行卡口侦测)。  

### Version 4.3.1.3 (build20140912)  

$\bullet$ 网络摄像机 V5.2.2、V5.2.3，网络球机 V5.2.3、V5.2.4  
$\bullet$ 新增人脸侦测报警信息类型（对应接口 NET_DVR_SetDVRMessageCallBack_V30 和NET_DVR_StartListen_V30）：COMM_ALARM_FACE_DETECTION。  
$\bullet$ 新增录像计划配置扩展（对应接口 NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_RECORDCFG_V40、NET_DVR_SET_RECORDCFG_V40。  
$\bullet$ 新增抓拍图片参数配置（对应接口 NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_SNAPINFO_CFG、NET_DVR_SET_SNAPINFO_CFG。  
$\bullet$ 新增车牌识别检测计划配置（对应接口 NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_GUARDCFG、NET_DVR_SET_GUARDCFG。  
$\bullet$ 新增远程控制设备完全恢复出厂值功能（对应接口 NET_DVR_RemoteControl）：命令：NET_DVR_COMPLETE_RESTORE_CTRL。  
$\bullet$ 新增 SMART 参数配置功能：NET_DVR_GetSTDConfig、NET_DVR_SetSTDConfig  
$\bullet$ 新增无线参数配置功能：NET_DVR_GetSTDConfig、NET_DVR_SetSTDConfig  
$\bullet$ 新增远程控制接口：NET_DVR_STDControl  
$\bullet$ 新增获取能力集接口：NET_DVR_GetSTDAbility  
 Smart 人脸侦测功能:1) NET_DVR_SETUPALARM_PARAM(报警布防参数)使用 1 个字节新增参数：byFaceAlarmDetection(人脸侦测报警信息类型)。2) NET_VCA_FACESNAP_RESULT(脸抓拍结果)使用 1 个字节新增参数：byAlarmEndMark(报警结束标记)。  
 Smart 车辆侦测功能:1) NET_DVR_ROI_DETECT_COND(ROI 检测区域信息)中 byRoiDetectTrackType(检测类型)和NET_DVR_ROI_TRACK_RECT_CFG(ROI 动态模式配置)中 byModeType(动态模式)分别新增取值：3-车牌。2) NET_ITS_PLATE_RESULT(车牌识别结果)、NET_DVR_TRIGGER_COND(触发模式配置条件)分别使用 1 个字节新增参数：byDetSceneID(检测场景号)。3) NET_ITC_PLATE_RECOG_PARAM(牌识参数)使用 1 个字节新增参数：byProvince(省份索引值)。4) NET_ITC_POST_MPR_PARAM(卡口多帧检测触发参数)使用 32 个字节新增参数：szSceneName(场景名称)。5) ITS_OVERLAP_ITEM_TYPE(字符叠加类型)新增枚举类型：OVERLAP_ITEM_LICENSE_PLATE_COLOR(车牌颜色)、OVERLAP_ITEM_SCENE_NUMBER(场景编号)、OVERLAP_ITEM_SCENE_NAME(场景名称)。6) NET_DVR_CLOUDSTORAGE_CFG(云存储配置)中 struPoolInfo 新增取值定义：数组 2 表示车辆侦测数据池。  
 NET_DVR_PDC_RULE_CFG_V42(客流量规则配置)使用 9 个字节新增参数：byOSDEnable(客流统计 OSD 显示是否启用)、struOSDPoint(客流统计显示 OSD 显示左上角坐标)。  
 NET_DVR_HEATMAP_COND(热度图配置条件)、NET_DVR_HEATMAP_RESULT(热度图上传结果)、NET_DVR_HEATMAP_QUERY_COND(热度图数据查询条件)分别使用 1 个字节新增参数：byDetSceneID(检测场景号)。  

$\bullet$ 图片、录像相关参数扩展：  

 NET_DVR_FIND_PICTURE_PARAM(图片查找条件)，使用 17 个字节新增参数：byProvince(省份索引值)、sLicense[MAX_LICENSE_LEN](车牌号码)；byFileType(查找的图片类型)新增取值：0x13-进入区域侦测, $.0{\times}14-$ 离开区域侦测,0x15-徘徊侦测,0x16-人员聚集侦测,0x17-快速运动侦测,0x18-停车侦测,0x19-物品遗留侦测,0x1a-物品拿取侦测,0x1b-车牌侦测。  

 NET_DVR_EVENT_CAPTURE(事件抓图参数)中 struRelCaptureChan 新增取值定义：数组 11-进入区域侦测、数组 12-离开区域侦测、数组 13-徘徊侦测、数组 14-人员聚集侦测、数组 15-快速运动侦测、数组 16-停车侦测、数组 17-物品遗留侦测、数组 18-物品拿取侦测。  

 NET_DVR_FILECOND_V40(文件查找条件)中 dwFileType(录象文件类型)新增取值：26-进入区域侦测,27-离开区域侦测,28-徘徊侦测,29-人员聚集侦测,30-快速运动侦测,31-停车侦测,32-物品遗留侦测,33-物品拿取侦测。  

 NET_DVR_CAMERAPARAMCFG_EX(前端参数配置)扩展：  

1) byIrisMode(光圈模式)新增取值：5- HIK 3.8-16mm F1.5（HV3816P-8MPIR）。  

2) byCaptureModeN、byCaptureModeP(视频输入模式)新增取值：44-960\*576@25fps、45-960\*480@30fps、  
46-752\*582@25fps、47-768\*494@30fps、48-2560\*1440@25fps、49-2560\*1440@30fps 、50-720P@100fps、  
51-720P@120fps、52-2048\*1536@50fps、53-2048\*1536@60fps、54-3840\*2160@25fps、  
55-3840\*2160@30fps、56-4096\*2160@25fps、57-4096\*2160@30fps 、8-1280\*1024@50fps、  
59-1280\*1024@60fps、60-3072\*2048@50fps、61-3072\*2048@60fps、62-3072\*1728@25fps、  
63-3072\*1728@30fps、64-3072\*1728@50fps、65-3072\*1728@60fps。  

 NET_DVR_AEMODECFG(曝光、快门等其他参数配置)中 byShutterSet(快门)新增取值：50-1/175、51-1/195、52-1/225、53-1/230。  

 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)扩展：1) byResolution(分辨率)新增取值： $\mathsf{b}68\!-\!2464^{*}1520$ 、69-1280\*1920、70-2560\*1440、71-1024\*1024。2) wIntervalFrameI(I 帧间隔)新增取值：25-3、26-5、27-7、28-9、29-100、30-120、31-24、32-48。  

 NET_DVR_DEVSERVER_CFG(模块服务配置)使用 1 个字节新增参数：byEnableSupplementLight(补光灯控制)。  

 NET_DVR_PTZControl 等云台控制接口中 dwPTZCommand 新增云台控制命令：TILT_DOWN_ZOOM_IN、 TILT_DOWN_ZOOM_OUT、PAN_LEFT_ZOOM_IN、PAN_LEFT_ZOOM_OUT、PAN_RIGHT_ZOOM_IN、 PAN_RIGHT_ZOOM_OUT、UP_LEFT_ZOOM_IN、UP_LEFT_ZOOM_OUT、UP_RIGHT_ZOOM_IN、 UP_RIGHT_ZOOM_OUT、DOWN_LEFT_ZOOM_IN、DOWN_LEFT_ZOOM_OUT、DOWN_RIGHT_ZOOM_IN、 DOWN_RIGHT_ZOOM_OUT、TILT_UP_ZOOM_IN、TILT_UP_ZOOM_OUT。  

 NET_DVR_NETCFG_V30(网络配置)使用 2 个字节新增参数：byEnablePrivateMulticastDiscovery(私有多播搜索使能)、byEnableOnvifMulticastDiscovery(Onvif 多播搜索使能)。  

 NET_DVR_GetUpgradeState 获取远程升级的状态新增取值：7- 升级包类型不匹配、8- 升级包版本不匹配。  

$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中 ROI 能力(ROIAbility)扩展，<MainStream>、<SubStream>和<Stream3>中的子节点<trackROIModeType>均增加取值：licencePlateTrack(车牌)。  

$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中设备通道输入能力(ChannelInputAbility)扩展，新增节点：<RecordPlan>(录像计划配置能力)、<RecordQuery>(录像查询能力)和<RecordSchedule>(支持录像计划的事件类型能力)。  

$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中 PTZ 能力(PTZAbility)扩展：  

1) <controlType>(云台控制类型)新增取值：tiltUpZoomIn, tiltUpZoomOut, tiltDownZoomIn, tiltDownZoomOut, panLeftZoomIn, panLeftZoomOut, panRightZoomIn, panRightZoomOut, upLeftZoomIn, upLeftZoomOut, upRightZoomIn, upRightZoomOut, downLeftZoomIn, downLeftZoomOut, downRightZoomIn,  

downRightZoomOut。2) <PTZLOCK>(云台锁定能力)中<supportFunction>新增取值：regionEntrance, regionExiting, loitering,peopleGathering, fastMoving, parking, unattendedBaggage, objectRemoval, vehicleDetection。$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中智能通道分析能力(VcaChanAbility)扩展：1) <PDC>(客流量能力)中新增节点<OSD>(OSD 能力)、<mutexAbility>(互斥能力)。2) <HeatMapDetection>(热度图侦测能力)中新增节点<detSenceID>(检测场景号)。$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力(EventAbility)扩展：1) 新增节点：<VehicleDetection>(车辆侦测能力)。2) <TraversingVirtualPlane>(越界侦测)中<mutexAbility>(互斥能力)新增取值：PDC。$\bullet$ 设备所有编码能力(DEVICE_ENCODE_ALL_ABILITY_V20)扩展：1) 新增节点<StreamAttachInfo>(码流附加信息能力)。 2) 所有<VideoFrameRate>和<VideoFrameRateN>均增加取值：29-100、30-120、31-24、32-48。$\bullet$ 设备网络应用参数能力(DEVICE_NETAPP_ABILITY)扩展，新增节点<CloudStorage>(云存储能力)、<NetCfg>(网络参数配置能力)。$\bullet$ 设备 JPEG 抓图能力(DEVICE_JPEG_CAP_ABILITY)扩展:1) 新增节点<FindPicInfo>(图片查找能力)。2) <EventCap>(事件抓图)的节点<eventType>新增事件类型：regionEntrance,regionExiting,loitering,group,rapidMove,parking,unattendedBaggage,attendedBaggage。$\bullet$ 设备软硬件能力(DEVICE_SOFTHARDWARE_ABILITY)扩展：1) 新增节点<CompleteRestoreSupport>(支持完全恢复出厂值)。2) <NeedReboot>(重启能力)中新增子节点<CompleteRestoreReboot>(设备完全恢复出厂值是否需要重启)。3) <DevModuleServerCfg>(设备服务配置能力)中新增子节点<supplementLight>(补光灯控制)。$\bullet$ 设备前端参数能力(IPC_FRONT_PARAMETER_V20)扩展：1) 新增节点：<devType>(设备类型)、<AutoExposure>(自动曝光能力)。2) <captureModePWithIndex>、<captureModeNWithIndex>新增取值： $44–960^{*}576@2585$ ,45-960\*480@30fps, 46-752\*582@25fps, 47-768\*494@30fps, 48-2560\*1440@25fps, 49-2560\*1440@30fps,50-720P@100fps, 51-720P@120fps, 52-2048\*1536@50fps, 53-2048\*1536@60fps, 54-3840\*2160@25fps,55-3840\*2160@30fps, 56-4096\*2160@25fps, 57-4096\*2160@30fps, 58-1280\*1024@50fps,59-1280\*1024@60fps, 60-3072\*2048@50fps, 61-3072\*2048@60fps, 62-3072\*1728@25fps,63-3072\*1728@30fps, 64-3072\*1728@50fps, 65-3072\*1728@60fps。$\bullet$ 3) <IrisMode>(光圈模式)中新增子节点<Piris4>。$\bullet$ 新增报警日志次类型：0x1b\~0x1e、0x2a\~0x2f、 $0{\times}3{\mathsf{c}}{\sim}0{\mathsf{x}}41$ $\bullet$ 新增错误码：1103、1104、1105  

### Version 4.3.0.6 (build20140722)  

$\bullet$ 网络球机 V5.2.0  

$\bullet$ 新增 PTZ 配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_PTZ_BASICPARAMCFG(PTZ 基本参数)、NET_DVR_PTZ_OSDCFG(PTZ OSD 配置)、NET_DVR_PTZ_POWEROFFMEMCFG(掉电记忆模式配置)、NET_DVR_PTZ_PRIORITIZECFG(云台优先配置)、NET_DVR_SMARTTRACKCFG(智能运动跟踪配置)、NET_DVR_PTZ_LOCKCFG(云台锁定配置)、NET_DVR_PRIVACY_MASKS_ENABLECFG(云台私遮蔽全局使能配置)。  

$\bullet$ 新增限位参数配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：  

命令：NET_DVR_GET_LIMITCFG、NET_DVR_SET_LIMITCFG。  
$\bullet$ 新增获取巡航路径功能（对应接口：NET_DVR_GetDeviceConfig）：命令：NET_GET_CRUISEPOINT_V40。  
$\bullet$ 新增云台隐私遮蔽参数配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_PRIVACY_MASKSCFG、NET_DVR_SET_PRIVACY_MASKSCFG。  
$\bullet$ 新增云台锁定剩余时间获取功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_GET_PTZLOCKINFO。  
$\bullet$ 新增 PTZ 远程控制功能（对应接口：NET_DVR_RemoteControl）：命令：NET_DVR_PTZLIMIT_CTRL(限位参数控制)、NET_DVR_PTZ_CLEARCTRL(清除配置信息)、NET_DVR_PTZ_INITIALPOSITIONCTRL(零方位角控制)、NET_DVR_PTZ_ZOOMRATIOCTRL(设置跟踪倍率)。  
 NET_DVR_CAMERAPARAMCFG_EX(前端参数配置)的参数 byLocalOutputGate(本地输出开关变量)新增取值：49- SDI_720P25、50- SDI_720P30。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)使用 1 个保留参数新增：byAudioSamplingRate(音频采样率)。  
$\bullet$ 设备所有编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)中<MainAudioEncodeType>、<SubAudioEncodeType>、<EventAudioEncodeType>、<Stream3AudioEncodeType>新增子节点：<AACAudioBitRate>(AAC 音频码率)、<AACSamplingRate>(AAC 音频采样率)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中事件能力(EventAbility)，新增<AlarmIn>新增子节点<notSupportPTZLinkage>(不支持 PTZ 联动)、<notSupportPTZLinkage>(PTZ 联动能力)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中云台能力(PTZAbility)扩展：1) 新增节点：<LinearScanCfg>(线性扫描)、<WiperCfg>(雨刷控制)、<WiperStatus>(雨刷状态)、<PtzBasicCfg>(PTZ 基本参数)、<LimitCfg>(限位参数配置)、<LimitCtrl>(限位控制)、<ClearCfg>(清除配置)、<PtzPrioritizeCfg>(云台优先)、<InitalPostionCtrl>(零方位角控制)、<PrivacyMaskCfg>(云台隐私遮蔽配置)、<SmartTrackCfg>(智能运动跟踪)、<ZoomRatioCtrl>(跟踪倍率控制)、<PTZLOCK>(云台锁定控制)。2) <ParkAction>新增子节点<oneTouchSwitch>(云台守望一键功能使能)、<notSupportPTZLinkage>(PTZ 联动能力)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中智能通道分析能力(VcaChanAbility)扩展，<FaceSnap>新增子节点<PupillaryDistance>(瞳距限制)。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20)，<LOCALOUTPUT>中<Range>新增取值：49–SDI_720P25、50- SDI_720P30。  

### Version 4.3.0.5 (build20140627)  

$\bullet$ 网络摄像机 V5.2.0  

$\bullet$ NET_DVR_GBT28181_ACCESS_CFG(GBT28181 协议接入配置)使用 5 个保留参数新增：byTransProtocol(传输协议)、dwRegisterInterval(注册间隔)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中 GB/T28181 能力(GBT28181AccessAbility)，新增节点：<transProtocol>、<registerInterval>。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)新增节点：<NasMountPara>(NAS 挂载参数)、<GBT28181>(是否支持 GB/T28181 协议)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中事件能力(EventAbility)，新增节点<DetailedExceptionAlarm>(异常联动功能细化)。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20)，新增节点<supportCCDFunc>(支持的前端参数功能项)，<Mirror>(镜像)新增子节点<mutexAbility>(互斥能力)。  
$\bullet$ 新增错误号：1102。  

### Version 4.3.0.3 (build20140520)  

 DS-2CD63xx 系列第二代鱼眼 IPC V5.0.9 build140612  
$\bullet$ 新增参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_TRACK_DEV_PARAM(跟踪设备参数配置)、NET_DVR_PTZ_TRACK_PARAM(PTZ 跟踪参数配置)。  
 NET_DVR_HANDLEEXCEPTION_V40(报警和异常处理)的参数 dwHandleType 新增取值：0x800: PTZ 联动跟踪(球机跟踪目标)。  
$\bullet$ 鱼眼 IPC 能力集(FISHEYE_ABILITY)新增节点：<TrackDevice>(跟踪设备参数)、<PTZTrack>(PTZ 跟踪参数)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中事件能力 EventAbility，节点<TraversingVirtualPlane>和<FieldDetection>中<alarmHandleType>新增类型：”ptztrack”。  

### Version 4.3.0.3 (build20140520)  

$\bullet$ 网络摄像机 V5.1.7  
$\bullet$ 新增安全认证配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_SECURITY_CFG  
$\bullet$ 新增客流量统计规则批量配置功能（对应接口:NET DVR GetDeviceConfig 和NET DVR SetDeviceConfig）：命令：NET_DVR_GET_PDC_RULECFG_V42、NET_DVR_SET_PDC_RULECFG_V42  
$\bullet$ 新增客流量数据查询功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_GET_PDC_RESULT  
$\bullet$ 新增热度图参数批量配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_HEATMAP_CFG、NET_DVR_SET_HEATMAP_CFG  
$\bullet$ 新增热度图数据查询功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_GET_HEATMAP_RESULT  
$\bullet$ 新增热度图结果上传（对应接口：NET_DVR_SetDVRMessageCallBack_V30 和 NET_DVR_StartListen_V30）：NET_DVR_HEATMAP_RESULT  
$\bullet$ 新增能力集（对应接口：NET_DVR_GetDeviceAbility，对应能力集类型：DEVICE_ABILITY_INFO）安全认证配置能力集 SecurityAbility摄像机架设参数能力集 CameraMountAbility  
$\bullet$ 新增错误号：153、1101  
 NET_DVR_DEVSERVER_CFG(模块服务配置)使用 1 个保留字节新增参数：byEnableAutoDefog(自动除雾控制)。  
 NET_DVR_CMS_PARAM(解码通道状态)使用 32 个保留字节新增参数：sPlatformEhomeVersion[NAME_LEN](平台 EHOME 协议版本)。  
 NET_DVR_EZVIZ_ACCESS_CFG(EZVIZ 接入参数配置)和 NET_DVR_GBT28181_ACCESS_CFG(GBT28181 协议接入配置)分别使用 1 个保留字节新增参数：byDeviceStatus(在线状态)。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)的参数 byResolution(分辨率)新增取值：$62\!-\!4000^{\ast}3000$ 、 $63{-}4096{^\ast}2160$ 、 $64{-}3840^{*}2160$ 、 $65\!-\!4000^{\ast}2250$ 、 $66{-}3072^{*}1728$ 。  
 NET_DVR_PDC_ALRAM_INFO(客流量统计结果)使用 1 个保留字节新增参数：bySmart(智能设备类型)。  
$\bullet$ NET_DVR_CAMERA_SETUPCFG(相机架设参数)使用 6 个保留字节新增参数：byCameraViewAngle(摄像机安装视野角度)、dwHorizontalDistance(摄像机与出入口水平距离)、byDetailLensType(镜头类型)。  
$\bullet$ 新增声强陡降侦测功能：1) NET_DVR_AUDIO_EXCEPTION(音频异常配置)使用 8 个保留字节新增参数：struAudioSteepDrop(声强陡降)。2) NET_DVR_AUDIOEXCEPTION_ALARM(声音报警信息)的参数 byAlarmType(报警类型)新增取值：3-声强陡  

降。  

3) 新增报警日志次类型：MINOR_VCA_ALARM_AUDIOSTEEPDROP。  

 NET_DVR_CAMERAPARAMCFG_EX(前端参数配置)扩展：  

1) 参数 byIrisMode(光圈模式)新增取值：3-Union 3-9mm F1.6-2.7 (T5280-PQ1)、4-Union 2.8-12mm F1.6-2.7(T5289-PQ1)。2) byCaptureModeN 和 byCaptureModeP(视频输入模式)新增取值：40-4000\*3000@12.5fps、41-4000\*3000@15fps、42-4096\*2160@20fps、43-3840\*2160@20fps。  
$\bullet$ 人脸抓拍扩展：1) NET_VCA_SINGLE_FACESNAPCFG(人脸抓拍单条规则参数)使用 1 个保留字节新增参数：byAutoROIEnable(人脸自动 ROI 开关使能)。2) NET_VCA_FACESNAPCFG(人脸抓拍规则配置)使用 2 个保留字节新增参数：wFaceExposureMinDuration(人脸曝光最短持续时间)、byFaceExposureMode(人脸曝光使能)。3) NET_VCA_HUMAN_FEATURE(人体属性参数)使用 2 个保留字节新增参数：bySex(性别)、byEyeGlass(是否戴眼镜)。4) NET_VCA_FACESNAP_RESULT(人脸抓拍结果)使用 21 个保留字节新增参数：bySmart(智能设备类型)、struFeature(人体属性)、dwStayDuration(停留画面中时间)。  
$\bullet$ 智能能力扩展：1) NET_VCA_DEV_ABILITY(智能设备能力集)使用 1 个保留字节新增参数：byHeatMapChanNum(热度图通道个数)。2) VCA_CHAN_ABILITY_TYPE(智能能力类型)新增枚举类型：VCA_HEATMAP(热度图)。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)扩展，新增节点：<CameraMountAbility>(摄像机架设配置能力)，<DevModuleServerCfg>(模块服务配置能力)中新增子节点：<autoDefog>、<sshServer>、<webAuthentication>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中协议接入能力(AccessProtocolAbility)：新增节点<deviceStatus>，<mutexAbility>新增取值“ehome”。  
$\bullet$ 设备网络应用参数能力(DEVICE_NETAPP_ABILITY)扩展，新增节点：<CMS>，<HTTPS>中新增子节点<certRequest>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中 GB/T28181 能力(GBT28181AccessAbility)，新增节点：<deviceStatus>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力(EventAbility)，节点<VoiceDetection>新增子节点<audioSteepDrop>，节点<TraversingVirtualPlane>和<FieldDetection>中新增互斥能力类型：19-1920\*1080@50fps、20-1920\*1080@60fps。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20)扩展：1) <CaptureMode>新增子节点：<CaptureModeIndex19>、<CaptureModeIndex20>、<CaptureModeIndex7>、<CaptureModeIndex8>。2) <ExposureSet>新增子节点：<ExposureSetIndex20>、<ExposureSetIndex0>、<ExposureSetIndex2>、<ExposureSetIndex3>。3) <Piris>新增子节点：<Piris2>、<Piris3>。4) <WDR>、<DigitalNoiseReduction>、<Dehaze>、<LightInhibit>和<CorridorMode>新增子节点：<mutexAbility>。5) <captureModePWithIndex>和<captureModeNWithIndex>新增取值：40-4000\*3000@12.5fps、41-4000\*3000@15fps、42-4096\*2160@20fps、43-3840\*2160@20fps。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中智能通道分析能力(VcaChanAbility)扩展：1) 新增节点：<HeatMapDetection>。2) 节点<Behavior>新增子节点<Scene>。  
3) 节点<PDC>新增子节点<PDCType>、<alarmHandleType>、<detecteSensitive>、<generatieSpeedSpace>、<generatieSpeedTime>、<countSpeed>、<detecteType>、<targetSizeCorrect>。  
4) 节点<FaceSnap>新增子节点<autoROI>、<faceExposure>、<faceExposureMinDuration>。  

### Version 4.2.8.7 (build20140408)  

$\bullet$ 网络球机 V5.1.8  
$\bullet$ 新增定时智能跟踪参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_SCHEDULE_AUTO_TRACK_CFG  
$\bullet$ 新增强制 I 帧功能，支持多码流（对应接口：NET_DVR_RemoteControl）：命令：NET_DVR_MAKE_I_FRAME  
 NET_DVR_LASER_PARAM_CFG(激光参数配置)使用 1 个保留字节新增参数：byLimitBrightness(激光灯亮度限制)。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20)新增节点<LaserConfig>。  

### Version 4.2.8.7 (build20140408)  

$\bullet$ 网络摄像机 V5.1.6  
$\bullet$ 新增补光灯参数配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_IOOUT_CFG、NET_DVR_SET_IOOUT_CFG。  
$\bullet$ 新增信号同步配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_SIGNAL_SYNCCFG。  
$\bullet$ 网络硬盘配置扩展（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_NET_DISKCFG_V40(支持域名)。  
$\bullet$ 新增 EZVIZ 接入配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_EZVIZ_ACCESS_CFG。  
$\bullet$ 新增服务器测试功能（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_NTP_SERVER_TEST(NTP 测试)、NET_DVR_NAS_SERVER_TEST(NAS 测试)、NET_DVR_EMAIL_SERVER_TEST(EMAIL 测试)、NET_DVR_FTP_SERVER_TEST(FTP 测试)、NET_DVR_IP_TEST(IP测试)。  
$\bullet$ 新增能力集（对应接口：NET_DVR_GetDeviceAbility，对应能力集类型：DEVICE_ABILITY_INFO）IO 输入输出能力集 IOAbility、协议接入能力集 AccessProtocolAbility。  
 NET_VCA_DEFOCUSPARAM(虚焦侦测配置)使用 1 个保留字节新增参数：bySensitiveLevel(灵敏度)。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)使用 1 个保留字节新增参数：bySteamSmooth(码流平滑)。  
 NET_DVR_DEVSERVER_CFG(模块服务配置)使用 1 个保留字节新增参数：byEnableLEDStatus(状态指示灯控制)。  
 NET_DVR_EMAILCFG_V30(EMAIL 参数)使用 1 个保留字节新增参数：byEnableTLS(是否启用 TLS)。  
 NET_DVR_RECORD_V30(录像参数)中 byStreamType(码流类型)新增取值：3-第三码流。  
●NET_DVR_DEVICEINFO_V30 的参数bySupport4 新增取值:bySupport4& Ox10表示是否支持域名方式挂载网络硬盘。  
$\bullet$ 前端参数配置扩展：1) NET_DVR_SMARTIR_PARAM(SMART IR 配置参数)使用 2 个保留字节新增参数：byShortIRDistance(近光灯距离等级)、byLongIRDistance(远光灯距离等级)。2) NET_DVR_CAMERAPARAMCFG_EX(前端参数配置)使用 16 个保留字节新增参数：struLaserParam(激光参  

数)。  

$\bullet$ 录像类型扩展：NET_DVR_FILECOND_V40(文件查找条件)的 dwFileType、NET_DVR_FINDDATA_V40(文件查找结果信息)的 byFileType、NET_DVR_RECORDDAY(全天录像参数)和 NET_DVR_RECORDSCHED(时间段录像参数)的 byRecordType，均增加类型取值：20-人脸侦测(Smart 报警)。  
$\bullet$ 图像参数配置扩展，NET_DVR_PICCFG_V40、NET_DVR_PICCFG_V30 分别使用 5 个保留字节新增参数：byOSDColorType(OSD 颜色模式)、struOsdColor(OSD 自定义颜色)。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20)中<SmartIR>新增子节点<ShortIRDistance>、<LongIRDistance>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力(EventAbility)扩展：<FaceDetection>新增子节点<triggerRecord>、<mutexAbility>；<TraversingVirtualPlane>、<FieldDetection>新增子节点<holidayTimeSlotNum>、<mutexAbility>；<DefousDetection>新增子节点<sensitivityLevel>。  
$\bullet$ 设备所有编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)中<MainChannel>、<SubChannelEntry>、<EventChannel>、<Stream3>、<TranscodeStream>新增子节点<StreamSmooth>。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)扩展：新增节点<IOAbilitySupport>、<AccessProtocolAbility>、<NetDiskDomain>;<DevModuleServerCfg>新增子节点<LEDStatus>;<NeedReboot>新增子节点<NetworkCardTypeChange>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中录像相关能力(RecordAbility)扩展，新增节点：<faceDetectionRecord>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中 GB/T28181 能力(GBT28181AccessAbility)，新增节点：<mutexAbility>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中通道输入能力(ChannelInputAbility)，新增节点：<recordStreamType>、<recordBackup>、<LockDuration>、<recordArchive>。  
$\bullet$ 设备图像参数能力集(DEVICE_VIDEOPIC_ABILITY)扩展，<OSD>新增子节点<OSDColorType>。  
$\bullet$ 设备网络应用参数能力(DEVICE_NETAPP_ABILITY)扩展，<NTP>、<FTP>、<NAS>新增子节点<serverTest>，<Net>新增子节点<IPTest>，<Email>新增子节点<emailTestWithParam>、<enableTLS>。  

### Version 4.2.8.3 (build20140213)  

 DS-2CD63xx 系列第二代鱼眼 IPC V5.0.9 build140305  
$\bullet$ 远程设置设备登录参数（对应接口：NET_DVR_RemoteControl）：命令：NET_DVR_REMOTECONTROL_DEV_PARAM  
$\bullet$ 新增 PTZ 点坐标配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_PTZ_POINT、NET_DVR_SET_PTZ_POINT  
$\bullet$ 新增鱼眼长连接配置（对应接口：NET_DVR_StartRemoteConfig）：命令：NET_DVR_FISHEYE_CFG  
$\bullet$ 新增鱼眼 PTZ 拖动功能（对应接口：NET_DVR_SendRemoteConfig）：命令：DRAG_PTZ  
$\bullet$ 新增获取鱼眼码流状态功能（对应接口：NET_DVR_GetDeviceStatus）：NET_DVR_FISHEYE_STREAM_STATUS  
 NET_DVR_PREVIEW_DISPLAYCFG(鱼眼预览显示参数)的原参数 byDisplayMode 无效删除，新增参数byRealTimeOutput(实时输出使能控制)。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)中 byResolution(分辨率)新增取值： $50{\cdot}720^{*}720$ ，51-1280\*1280， $52\!-\!2048^{\ast}768$ ， $53\!-\!2048^{\ast}2048$ 。  
$\bullet$ 新增设备类型：IPCAM_FISHEYE(鱼眼摄像机)  

### Version 4.2.7.6 (build20131231)  

$\bullet$ 网络摄像机 V5.1.3  

 NET_DVR_DEVSERVER_CFG(模块服务配置)使用 1 个保留字节新增参数：byABFServer(ABF 使能设置)。  
 NET_VCA_TRAVERSE_PLANE_DETECTION(越界侦测配置)、NET_VCA_FIELDDETECION(区域侦测配置)分别使用 1 个保留字节新增参数：byEnableDualVca(启用支持智能后检索)。  
 NET_DVR_DEVICEINFO_V30(设备参数)使用 2 个保留字节新增参数：bySupport4(能力集扩展)、byLanguageType(语种能力)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力 EventAbility，节点<TraversingVirtualPlane>和<FieldDetection>分别新增子节点：<enableDualVca>(智能后检索能力)  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)，新增节点：<Language>(语种能力)，<DevModuleServerCfg>(模块服务配置能力)新增子节点：<abfServer>(ABF 使能能力)。  

### Version 4.2.6.8 (build20131113)  

$\bullet$ 网络摄像机 V5.1.0  
$\bullet$ 新增(扩展)通道图像参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_PICCFG_V40，主要新增专家模式的多区域移动侦测配置功能（日夜切换模式、占比参数等）。  
$\bullet$ 新增 ISP 前端参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_ISP_CAMERAPARAMCFG。  
$\bullet$ 新增模块服务配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_DEVSERVER_CFG。  
$\bullet$ 新增 GBT28181 协议接入配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_GBT28181_ACCESS_CFG。  
$\bullet$ 新增 GB/T28181 通道配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：GBT28181 协议接入设备的编码通道配置命令：NET_DVR_GET_GBT28181_CHANINFO_CFG、NET_DVR_SET_GBT28181_CHANINFO_CFGGBT28181 协议接入设备的报警输入通道配置命令：NET_DVR_GET_GBT28181_ALARMINCFG、NET_DVR_SET_GBT28181_ALARMINCFG  
$\bullet$ 新增能力集（对应接口：NET_DVR_GetDeviceAbility，对应能力集类型：DEVICE_ABILITY_INFO）前端参数动态能力集、报警触发录像能力集、GB/T28181 能力集  
 NET_DVR_CAMERAPARAMCFG_EX(前端参数配置扩展)使用 2 个保留字节新增参数：byCaptureModeN(N制视频输入模式)、byCaptureModeP(P 制视频输入模式)，参数 bySceneMode 新增取值：2-默认、3-弱光。  
 NET_DVR_COMPRESSION_INFO_V30(通道压缩参数)使用 1 个保留字节新增参数：byAudioBitRate(音频码率)。  
 NET_DVR_HANDLEEXCEPTION_V40(报警和异常处理)中 dwHandleType 新增处理方式类型： $\mathcal{W}_{0\times400}$ : 虚焦侦测联动聚焦”。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20)新增节点：<CaptureMode>、<DynamicAbility>、<ISPAdvanceCfg>，节点<SceneMode>的子节点<Range>新增取值：2,3 (2-默认、3-弱光)。  
$\bullet$ 设备图像参数能力集(DEVICE_VIDEOPIC_ABILITY)，<MotionDetection>的子节点<regionType>新增类型”area”，新增节点、<Area>、<NormalSensitivity>，<VideoInputEffect>中新增子节点<NotSupport>。  
$\bullet$ 设备编码能力(DEVICE_ENCODE_ALL_ABILITY_V20)新增节点、<OggVorbisAudioBitRate >、<G711UaudioBitRate>、<G711AaudioBitRate>、<MP2L2AudioBitRate>、<G726AudioBitRate>、<DynamicAbility>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中事件能力 EventAbility，节点<DefousDetection>的<alarmHandleType>新增类型”focus”。  
$\bullet$ 设备软硬件能力(DEVICE_SOFTHARDWARE_ABILITY)新增节点、<DevModuleServerCfg >、  

<GBT28181AccessAbilitySupport>、<SearchLogAbilitySupport>、<AlarmTriggerRecordAbilitySupport>、 <CameraParaDynamicAbilitySupport>。 $\bullet$ 视频编码类型“5-MPEG2”修正为“8-MPEG2”。  

Version 4.2.6.4 (build20130829)  
$\bullet$ 网络摄像机 V5.0.5、V5.0.8  
$\bullet$ 新增远程配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_AUDIOOUT_VOLUME (输出音量配置)。  
$\bullet$ 新增批量配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：NET_DVR_SCENECHANGE_DETECTION (场景变更报警配置)。  
$\bullet$ 新增上传报警信息（对应接口：NET_DVR_SetDVRMessageCallBack_V30 和 NET_DVR_StartListen_V30）：NET_DVR_SCENECHANGE_DETECTION_RESULT (场景变更报警)。  
 NET_IPC_AUX_ALARMCFG_UNION 中 NET_IPC_PIR_ALARMCFG 扩展为 NET_IPC_PIR_ALARMCFG_EX。  
$\bullet$ 新增报警次类型：0x1a、 $0{\times}20^{\sim}0{\times}27$ 。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)和 NET_DVR_COMPRESSION_AUDIO(语音对讲音频参数)中 byAudioEncType(音频编码类型)新增取值类型：5- MP2L2，6- G726，7- AAC。  
 NET_DVR_DEVICEINFO_V30(设备参数)中 bySupport2 新增能力类型：”bySupport2 & $0{\times}2^{\prime\prime}$ 表示支持FTPV40，”bySupport2 & 0x4”表示支持 ANR(断网录像)。  
 NET_DVR_PREVIEWINFO(预览参数)使用 1 个保留字节新增参数：bPassbackRecord(是否启用 ANR 断网录像功能)。  
 SNMP 协议配置(NET_DVR_SNMPCFG_V30 和 NET_DVR_SNMPCFG)使用 32 个保留字节新增参数：byTrapName[NAME_LEN](Trap 主机名称)。  
 NET_DVR_CAMERAPARAMCFG_EX(前端参数配置扩展)使用 12 个保留字节新增参数：struSmartIRParam(红外过爆配置信息)、struPIrisParam(P-Iris 红外光圈大小等级配置信息)，参数 byIrisMode 新增取值类型：2- P-Iris1，参数 byLocalOutputGate 新增取值类型：40-SDI_720P50、41-SDI_720P60、42-SDI_1080I50、43-SDI_1080I60、44-SDI_1080P24、45-SDI_1080P25、46-SDI_1080P30、47-SDI_1080P50、48-SDI_1080P60。  
 NET_DVR_FIND_PICTURE_PARAM(图片信息)中 byFileType(查找的图片类型)新增取值类型：0x10- 场景变更侦测。  
 NET_DVR_FILECOND_V40(文件查找信息) 中 dwFileType(查找的录像类型)新增取值类型：15-越界侦测、16-区域入侵、17-声音异常、18-场景变更侦测。  
 NET_DVR_RECORDDAY(全天录像参数)中 byRecordType(录象类型)新增取值类型：15-越界侦测、16-区域入侵、17-声音异常、18-场景变更侦测。  
 NET_DVR_FILECOND_V40 和 NET_DVR_FILECOND(录像查找条件)、NET_DVR_FINDDATA_V40 (录像查找结果)、NET_DVR_RECORDDAY(全天录像参数)、NET_DVR_RECORDSCHED(时间段录像参数)中文件类型或者录像类型“13-PIR|无线报警|呼救报警”修改成“13-移动侦测、PIR、无线、呼救等所有报警类型的”或””。  
 NET_DVR_EVENT_CAPTURE(事件抓图参数)中 struRelCaptureChan 新增取值定义：数组 8 表示越界侦测侦测抓图，数组 9 表示区域入侵侦测抓图，数组 10 表示场景变更侦测抓图。  
 NET_DVR_SINGLE_NET_DISK_INFO(单个网络硬盘参数)使用 56 个字节新增参数：uMountMethodParam(网络硬盘挂载方式联合体)，支持 NAS 接入认证功能。  
$\bullet$ 设备报警能力集(DEVICE_ALARM_ABILITY)新增节点：<alarmTime>，各种报警处理方式<alarmHandleType>新增类型：uploadftp。  
$\bullet$ 设备网络应用能力集(DEVICE_NETAPP_ABILITY)新增节点：<FuzzyUpgrade>。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中录像相关能力 RecordAbility 新增节点：<ANR>、<recordPlanAbility>、<findBackupRecordAbility、<MonthlyDistribution、<DailyDistribution、<playbackBackupRecordAbility、<sceneChangeDetectionRecord、<allAlarmTypeRecord。  
$\bullet$ 设备编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)，主码流、子码流、事件码流、码流 3 的音频编码类型新增：5- MP2L2。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中事件能力 EventAbility 新增节点：<SceneChangeDetection>。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20)节点<ExposureSet>新增曝光模式：20-1s-1000000us；节点<IrisMode>新增镜头类型：2- Piris1 “Tamron 2.8-8mm F1.2（M13VP288-IR）”，新增节点<Piris>；节点<LOCALOUTPUT>中新增本地输出类型 $40^{\sim}48$ ；节点<SmartIR>新增<modeType>、<IRDistance>。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)新增节点<SDINumber>、<NetDiskIdentification>、<NASIdentificationChange>。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)新增节点<SDINumber>、<NetDiskIdentification>、<NASIdentificationChange>。  
$\bullet$ 设备 JPEG 抓图能力集(DEVICE_JPEG_CAP_ABILITY)节点<EventCap>中<eventType >新增事件类型：sceneChangeDetection。  

### Version 4.2.6.4 (build20130829)  

$\bullet$ 网络球机 V5.1.0  
$\bullet$ 新增远程配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_PRESET_NAME(预置点名称配置)、NET_DVR_TIME_TASK(云台定时任务配置)。  
$\bullet$ 新增智能控制参数配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：NET_DVR_GET_VCA_CTRLINFO_CFG、NET_DVR_SET_VCA_CTRLINFO_CFG。  
$\bullet$ 新增语音名称配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_AUDIO_NAME、NET_DVR_SET_AUDIO_NAME。  
 NET_DVR_TRACK_PARAMCFG 使用 2 个保留字节新增参数：byStopTrackWhenFindFace(检测到目标后是否停止跟踪)、byStopTrackThreshold（跟踪终止评分阈值）。  
 NET_DVR_PTZ_MANUALTRACE 使用 1 个保留字节新增参数：byTrackType(跟踪类型)。  
 NET_VCA_DEV_ABILITY 使用 5 个保留字节新增参数：byFRecogChanNum(人脸抓拍通道个数)、byBPPerimeterChanNum(行为监狱版通道个数)、byTPSChanNum(交通诱导通道个数)、byTFSChanNum(道路违章取证通道个数)、byFSnapBFullChanNum(人脸抓拍和异常行为识别通道个数)。注：前 4 个参数非针对网络摄像机 V5.1.0 新增的参数。  
●VCA_CHAN_ABILITY_TYPE 新增枚举类型:VCA_FACE_SNAP、VCA_FACE_SNAPRECOG、VCA_FACE_RETRIEVAL、VCA_FACE_RECOG、VCA_BEHAVIOR_PRISON_PERIMETER、VCA_TPS、VCA_TFS、VCA_ BEHAVIOR_FACESNAP。  
 NET_VCA_CTRLINFO 使用 1 个保留字节新增参数：byControlType(控制类型)。  
$\bullet$ 设备用户管理参数能力集(DEVICE_USER_ABILITY):本地权限和远程权限都扩展成 admin、viewer、operator三种用户权限。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中 PTZ 能力集：新增节点<nameLen>、<specialNo>和<SchduleTask<。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力集：新增节点<stopTrackWhenFindFace>、<stopTrackThreshold>、<trackType>。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)：新增节点<QuotaRatio>、<MaxDvcsSubDevNumNum>、<DateUpLoadAndDownLoad>。  

### Version 4.2.3.1 (build20130701)  

$\bullet$ 网络摄像机 V5.0.4  

$\bullet$ 新增批量配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：NET_VCA_TRAVERSE_PLANE_DETECTION(越界侦测配置)、NET_VCA_FIELDDETECION(区域侦测配置)、NET_VCA_DEFOCUSPARAM(虚焦侦测参数配置)、NET_DVR_AUDIO_EXCEPTION(音频异常配置)。  
$\bullet$ 新增配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_CAMERAPARAMCFG_EX(前端参数配置扩展)。  
$\bullet$ 新增上传报警信息（对应接口：NET_DVR_SetDVRMessageCallBack_V30 和 NET_DVR_StartListen_V30）：NET_DVR_AUDIOEXCEPTION_ALARM(声音报警)、NET_DVR_DEFOCUS_ALARM(虚焦报警)。  
$\bullet$ 新增音量实时上传功能（对应接口：NET_DVR_StartRemoteConfig）：NET_DVR_START_GET_INPUTVOLUME(获取声音强度)。  
 NET_DVR_AUDIO_INPUT_PARAM 使用 2 个保留字节新增参数：byVolume(音量)、byEnableNoiseFilter(是否开启声音过滤)。  
 NET_DVR_DEVICEINFO_V30 的参数 byMainProto 和 bySubProto 新增取值：2-同时支持私有协议和 rtsp 协议取流（默认采用私有协议取流）。  
 NET_DVR_FIND_PICTURE_PARAM 的参数 byFileType 新增取值：0xe- 越界侦测、0xf- 入侵区域侦测。  
$\bullet$ 图像参数能力集(DEVICE_VIDEOPIC_ABILITY)，节点<FontSize>字体大小新增 adaptive(自适应)，节点<alarmHandleType>报警处理类型新增 uploadftp(抓图上传 FTP)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)的报警事件处理能力集，新增节点：<VoiceDetection>、<TraversingVirtualPlane>、<FieldDetection>、<DefousDetection>。  
$\bullet$ 前端参数能力集(IPC_FRONT_PARAMETER_V20)，新增节点：<DayNightFilterandGain>，节点<ExposureSet>新增曝光模式：17-1/150、18-1/200。  
$\bullet$ 设备编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)，新增节点：<enableNoiseFilter>、<suportEncodeType>、<SVCSuportEncodeType>。  
$\bullet$ JPEG 抓图能力集(DEVICE_JPEG_CAP_ABILITY)，节点<eventType >新增事件类型：vca,facedDetect ,lineDetection,filedDetection。  

### Version 4.2.2.2 (2013-5-23)  

$\bullet$ 网络摄像机 V5.0.3，新增设备 DS-2CD42xx  
$\bullet$ 新增人脸侦测配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：NET_DVR_DETECT_FACE(人脸侦测配置)。  
$\bullet$ 新增旋转配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_CORRIDOR_MODE(旋转功能配置)。  
$\bullet$ 新增支持报警上传类型（对应接口:NET DVR SetDVRMessageCallBack V30和NET DVR StartListen V30）：NET_VCA_FACESNAP_RESULT(人脸抓拍结果)。  
$\bullet$ 新增报警日志次类型：MINOR_DETECTFACE_ALARM_START、MINOR_DETECTFACE_ALARM_STOP。  
 NET_DVR_FIND_PICTURE_PARAM 参数 byFileType 新增取值类型：9-智能图片，13- 人脸侦测。  
 NET_DVR_EVENT_CAPTURE 参数 struRelCaptureChan[32]新增取值类型：数组 6 表示智能抓图，数组 7 表示人脸侦测抓图。且该结构体使用 1 个保留字节新增参数：byCapTimes(抓图张数)。  
 NET_DVR_PICCFG_V30 参数 byFontSize 取值类型： $0.16^{*}16($ 中) $\lvert\beta^{*}\rvert6($ (英)， $1-32^{*}32\cdot$ (中) $/16^{*}32\$ (英)，2-$64^{*}641$ (中) $\beta2^{*}64$ (英) $3-48^{\ast}481$ (中) $/24^{*}48!$ (英)，0xff- 自适应(adaptive) 。  

### Version 4.2.1.4 (2013-5-9)  

$\bullet$ 网络高清红外球 V5.0.2$\bullet$ 新增远程控制功能（对应接口：NET_DVR_RemoteControl）：NET_DVR_CONTROL_PTZ_PATTERN (云台花样扫描)、NET_DVR_CONTROL_PTZ_MANUALTRACE(手动跟踪定位)。  

$\bullet$ 新增能力集（对应接口：NET_DVR_GetDeviceAbility）：PTZ 能力集：PTZAbility、报警事件处理能力集：EventAbility、ROI 能力集：ROIAbility。  
$\bullet$ 新增配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_PTZ_PARKACTION_CFG(云台守望参数配置)。  
$\bullet$ 新增多码流压缩参数配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：NET_DVR_GET_MULTI_STREAM_COMPRESSIONCFG、NET_DVR_SET_MULTI_STREAM_COMPRESSIONCFG  
$\bullet$ 新增 ROI 相关配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：NET_DVR_GET_ROI_DETECT_NUM、NET_DVR_GET_ROI_DETECT、NET_DVR_SET_ROI_DETECT。  
●NET_DVR_COMPRESSION_INFO_V30 使用1个保留字节新增参数 byEnableSvc(SVC 功能使能),byResolution新增分辨率类型： $46{-}1376{^\ast}768$ ，dwVideoFrameRate 新增帧率类型： 17-25，18-30，19-35，20-40，21-45，22-50，23-55，24-60。  
 DEVICE_ENCODE_ALL_ABILITY_V20 设备编码能力集扩展帧率参数：<VideoFrameRate>和<VideoFrameRateN>节点，新增 SVC 编码能力：<SvcFunEnable 节点>。  
●DEVICE_NETAPP_ABILITY 能力集新增节点:<Ipv6Address>、<DHCPandPPPoE>、<ManualMap>、<SecondFTP>、<Protocol>、<NAS>、<IPSAN>、<NAT>。  
 IPC_FRONT_PARAMETER_V20 能力集新增节点：<WhiteBalanceandBacklight>、<DehazeLevel>。  

### Version 4.2.1.4 (2012-12-17)  

$\bullet$ 鱼眼摄像机  
$\bullet$ 新增配置功能（对应接口：NET_DVR_GetDeviceConfig）NET_DVR_PRESETCFG(鱼眼预置点参数配置)、NET_DVR_PTZCRUISECFG(鱼眼巡航路径参数配置)。  
$\bullet$ 新增鱼眼摄像机预览显示参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）NET_DVR_PREVIEW_DISPLAYCFG。  
$\bullet$ 新增云台参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）NET_DVR_PRESET_INFO、NET_DVR_PTZCRUISE_INFO、NET_DVR_MOTION_TRACK_CFG。  
$\bullet$ 新增远程控制功能（对应接口：NET_DVR_RemoteControl）NET_DVR_REMOTECONTROL_PRESETPOINT、NET_DVR_REMOTECONTROL_CRUISE。  
$\bullet$ 新增能力集（对应接口：NET_DVR_GetDeviceAbility）：FISHEYE_ABILITY。  
 NET_DVR_COMPRESSION_INFO_V30 参数 byResolution 增加分辨率类型：13-576\*576, 23-1536\*1536,$24{-}1920^{\ast}1920$ 。  
 NET_DVR_JPEGPARA 参数 wPicSize 增加抓图分辨率类型：20-576\*576,21-1536\*1536,22-1920\*1920。  

### Version 4.2.1.3 (2012-12-10)  

$\bullet$ 网络球机 V4.2.2  

$\bullet$ 新增球机配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）:NET_DVR_LOW_LIGHT_CFG(低照度参数配置)、NET_DVR_FOCUSMODE_CFG(聚焦模式配置)、NET_DVR_INFRARE_CFG(红外参数配置)、NET_DVR_AEMODECFG(快球曝光模式等其他参数信息)。  
$\bullet$ 新增球机远程控制命令（对应接口:NET DVR RemoteControl):NET_DVR_CONTROL_RESTART_SUPPORT(恢复前端默认参数)、NET_DVR_CONTROL_RESTORE_SUPPORT(球机机芯重启)。  
 NET_DVR_WHITEBALANCE 中参数 byWhiteBalanceMode 增加取值类型：7-钠灯，8-自动跟踪（ATW），9-一次白平衡（One Push），10-室外自动（Outdoor Auto），11-钠灯自动(SodiumLight Auto)，12-水银灯模式(MercuryLight)。  
 NET_DVR_BACKLIGHT 中参数 byBacklightMode 增加取值类型：10-开，11-自动，12-多区域背光补偿。  
 NET_DVR_VIDEOEFFECT 中参数 byEnableFunc 增加取值定义：bit3- 锐度类型：0-自动，1-手动。  
 NET_DVR_NOISEREMOVE 使用 2 个保留字节增加参数：byDigitalNoiseRemove2Denable、byDigitalNoiseRemove2Dlevel。  
 NET_DVR_CAMERAPARAMCFG 中参数 byLocalOutputGate 增加取值定义：11-缩放输出，12-裁剪输出，13-裁剪缩放输出。  

### Version 4.1.9.3 (2012-10-30)  

$\bullet$ 网络摄像机 V4.0.3  
 wifi 配置新增 WPA-personal/WPA2-personal 加密模式参数：NET_DVR_WIFI_CFG_EX。  
$\bullet$ 新增远程控制命令（对应接口：NET_DVR_RemoteControl）：NET_DVR_UPDATE_PIN(更新设备 PIN 码)、NET_DVR_WPS_CONNECT(启用 WPS 连接)。  
$\bullet$ 新增 PIN 码信息获取功能（对应接口：NET_DVR_GetDVRConfig）：命令：NET_DVR_GET_DEVICE_PIN。  
$\bullet$ 新增无线 WPS 参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_WPSCFG、NET_DVR_SET_WPSCFG。  
$\bullet$ 新增文件上传接口：NET_DVR_UploadFile、NET_DVR_GetUploadState、NET_DVR_UploadClose。  
$\bullet$ 新增呼救报警参数配置和报警上传（联合体 NET_IPC_AUX_ALARMCFG_UNION 和NET_IPC_AUXALARM_UPLOAD_UNION 中新增结构体）：NET_IPC_CALLHELP_ALARMCFG(呼救报警配置)。  

### Version 4.1.5 (2012-5-9)  

$\bullet$ 网络摄像机 V4.0  

$\bullet$ 新增接口：NET_DVR_ShutterCompensation、NET_DVR_CorrectDeadPixel、NET_DVR_FocusOnePush、NET_DVR_ResetLens、NET_DVR_RemoteControl。  
$\bullet$ 新增音频输入参数配置功能（对应接口 NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_AUDIO_INPUT、NET_DVR_SET_AUDIO_INPUT。  
$\bullet$ 新增去雾参数配置功能（对应接口 NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_CAMERA_DEHAZE_CFG、NET_DVR_GET_CAMERA_DEHAZE_CFG。  
$\bullet$ 新增辅助报警参数配置功能（对应接口 NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_IPC_GET_AUX_ALARMCFG、NET_IPC_SET_AUX_ALARMCFG。  
$\bullet$ 新增报警上传（对应接口：NET_DVR_StartListen_V30 和 NET_DVR_SetDVRMessageCallBack_V30）：NET_IPC_AUXALARM_RESULT(PIR 报警、无线报警、呼救等辅助报警信息)。  
$\bullet$ 新增能力集（对应接口：NET_DVR_GetDeviceAbility）：DEVICE_ALARM_ABILITY。  
 NET_DVR_CAMERAPARAMCFG 使用 7 个保留字节增加参数 byDimmerMode、byPaletteMode、byEnhancedMode、byFilterSwitch、byFocusSpeed、byAutoCompensationInterval 和 bySceneMode。  
 NET_DVR_EXPOSURE 使用 1 个保留字节增加参数 byAutoApertureLevel。  
 NET_DVR_COMPRESSION_INFO_V30 使用 1 个保留字节增加参数 byVideoEncComplexity。  
 NET_DVR_HANDLEEXCEPTION_V30 参数 dwHandleType 增加定义 $_{0\times20}$ (无线声光报警器联动)。  
 NET_DVR_RECORDDAY 和 NET_DVR_RECORDSCHED 的参数 byRecordType，或者 NET_DVR_FILECOND 和NET_DVR_FILECOND_V40 的参数 dwFileType 增加定义：10-PIR 报警，11-无线报警，12-呼救报警，13-PIR|  

无线报警|呼救报警。  

 NET_DVR_FINDDATA_V30 和 NET_DVR_FIND_PICTURE_PARAM 的参数 byFileType 增加定义：10-PIR 报警，11-无线报警，12-呼救报警。  
$\bullet$ NET_DVR_EVENT_CAPTURE 的参数 struRelCaptureChan 增加定义：数组 3 表示 PIR 报警抓图，数组 4 表示无线报警抓图，数组 5 表示呼救报警抓图。  
$\bullet$ 设备前端参数能力集(IPC_FRONT_PARAMETER_V20)增加节点：<AutoApertureLevel>(自动光圈灵敏度)。  

### Version 4.1.0 (2012-4-5)  

$\bullet$ 新增 G726 音频编解码接口：  

NET_DVR_InitG726Encoder、NET_DVR_EncodeG726Frame、NET_DVR_ReleaseG726Encoder、NET_DVR_InitG726Decoder、NET_DVR_DecodeG726Frame、NET_DVR_ReleaseG726Decoder。  

# 3 函数调用顺序  

## 3.1SDK基本调用的主要流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/32b963bbd2b8cba001fb57bc98c55ee33c2f39f5f2cd76d129073b051321f8de.jpg)  
图 3.1 SDK 基本流程  

其中虚线框的流程是可选部分，不会影响其他流程和模块的功能使用。按实现功能的不同可以分成十个模块，实现每个模块的功能时初始化 SDK、用户注册设备、注销设备和释放 SDK 资源这 4 个流程是必不可少的，解码器功能模块和异常行为识别功能模块是针对解码器和智能设备的，在该文档里我们不做描述。  

$\bullet$ 初始化 SDK（NET_DVR_Init）：对整个网络 SDK 系统的初始化，内存预分配等操作。$\bullet$ 设置连接超时时间（NET_DVR_SetConnectTime）：这部分为可选，用于设置 SDK 中的网络连接超时时间，用户可以根据自己的需要设置该值。在不调用此接口设置超时时间的情况下，将采用 SDK 中的默认值。  

 设置接收异常消息的回调函数（NET_DVR_SetDVRMessage 或 NET_DVR_SetExceptionCallBack_V30）：由于 SDK 中大部分模块的功能都是由异步模式实现，所以我们提供此接口用于接收预览、报警、回放、透明通道和语音对讲等模块发生异常信息。用户可以在初始化 SDK 后就设置该回调函数，在应用层对各个模块异常消息的接收和处理。  

 从解析服务器获得设备的 IP 地址（NET_DVR_GetDVRIPByResolveSvr_Ex）：该接口提供一种在仅知道设备名称和序列号的情况下，从解析服务器获得设备 IP 地址的方法。如：当前设备是通过拨号上网方式获取到动态 IP 地址，而运行了我公司 IPServer 软件的服务器即为解析服务器，我们可以通过此接口输入解析服务器的地址、设备的名称和序列号等信息查询该设备的 IP 地址。IPServer 是我公司提供的一款域名解析服务器软件。  

用户注册设备（NET_DVR_Login_V30）：实现用户的注册功能，注册成功后，返回的用户 ID 作为其他功能操作的唯一标识，SDK 允许最大注册用户数为 512 个。网络摄像机和网络球机允许有 16 个注册用户名，而且同时最多允许 128 个用户注册。  

预览模块：从前端设备取实时码流，解码显示以及播放控制等功能，同时支持软解码和解码卡解码。  
具体流程详见预览模块流程。  

回放和下载模块：可以通过按时间和按文件名的方式远程回放或者下载的录像文件，后续可以进行解码或者存储。同时还支持断点续传功能。具体流程详见回放和下载模块流程。  

 参数配置模块：设置和获取前端设备的参数，主要包括设备参数、网络参数、通道压缩参数、串口参数、报警参数、异常参数、交易信息和用户配置等参数信息。具体流程详见参数配置模块流程。  

远程设备维护模块：实现关闭设备、重启设备、恢复默认值、远程硬盘格式化、远程升级和配置文件导入/导出等维护工作。具体流程详见远程设备维护模块流程。  

语音对讲转发模块：实现和前端设备的语音数据对讲和语音数据获取，音频编码格式可以指定。具体流程详见语音对讲转发模块流程。  

报警模块：处理设备上传的各种报警信号。报警分为“布防”和“监听”两种方式，在采用监听方式并且不需要获取用户 ID 的情况下，报警模块可以无需进行“用户注册”操作步骤。具体流程详见报警模块流程。  

 透明通道模块：透明通道是将 IP 数据报文解析后直接发送到串行口的一种技术。实际上起到了延伸串行设备控制距离的作用。可利用 IP 网络控制多种串行设备，如控制解码器、矩阵、报警主机、门禁、仪器仪表等串行设备，对用户来说，只看到点对点传输，无须关心网络传输过程，所以称为串口透明通道。SDK 提供 485 和 232 串口作为透明通道功能，其中要将 232 串口作为透明通道使用，首先必须在 232 串口的配置信息（NET_DVR_RS232CFG）中将工作模式选为透明通道，这样 232 串口才可作为透明通道使用。具体流程详见透明通道模块流程。  

 云台控制模块：实现对云台的基本操作、预置点、巡航、花样扫描和透明云台的控制。SDK 将云台控制分为两种模式：一种是通过图像预览返回的句柄进行控制；另一种是无预览限制，通过用户注册 ID 号进行云台控制。  

## 3.2实时预览模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/fb7b1e8777feb5b5d4ae56bdddeeaa5b1f61fccbdb067f800a40ba6299851307.jpg)  
图 3.2 实时预览模块流程  

图中虚线框部分的模块是与预览模块相关，必须在启动预览后才能调用，这些模块之间是并列的关系，各自完成相应的功能。  

### 实时流解码方式：  

方式一：在预览接口 NET_DVR_RealPlay_V40 中预览参数的播放窗口句柄赋成有效句柄，则由 SDK 实现解码功能。在初始化 SDK 和注册设备两步骤后，直接调用启动预览和停止预览接口。方式二：用户可以通过设置预览接口 NET_DVR_RealPlay_V40 中预览参数的播放窗口句柄为空值，并通过调用捕获数据的接口（即设置 NET_DVR_RealPlay_V40 接口中的回调函数或调用NET_DVR_SetRealDataCallBack、NET_DVR_SetStandardDataCallBack 接口），获取码流数据进行后续解码播放处理。  

### 相关功能：  

$\bullet$ 声音控制功能主要实现独占、共享声音的打开和关闭；音量的控制。相关接口有：NET_DVR_OpenSound、NET_DVR_CloseSound、NET_DVR_OpenSoundShare、NET_DVR_CloseSoundShare、NET_DVR_Volume 等。  

实时流数据捕获和录像模块主要实现数据回调和本地录像的功能，可以供用户后续处理。相关接口有：NET_DVR_SetRealDataCallBack、NET_DVR_SetStandardDataCallBack、NET_DVR_SaveRealData 等。抓图功能主要实现对当前解码图像的捕获，保存格式为 BMP。相关接口有：NET_DVR_CapturePicture。NET_DVR_CaptureJPEGPicture 支持登录后直接从设备抓取 JPEG 图片。  
云台控制模块主要是在开启预览的前提下实现对云台控制的操作功能，包括云台预置点、巡航、花样扫描和透明云台等。相关接口有：NET_DVR_PTZControl、NET_DVR_PTZPreset、NET_DVR_PTZCruise、NET_DVR_PTZTrack、NET_DVR_TransPTZ。  

调用实例代码  

## 3.3回放和下载模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/d74b5ed58c96d0107d819ae4224076a0d627ee9b2a9fb774d37b7896a550ba4b.jpg)  
图 3.3 回放和下载模块流程  

回放下载网络摄像机或者网络球机 SD 卡中的录像文件：  

按文件回放或下载需要通过查找录像文件功能先获取文件信息（相关接口 NET_DVR_FindFile_V40、NET_DVR_FindNextFile_V40 ）， 然 后 根 据 获 取 到 的 文 件 名 开 始 回 放 或 下 载 （ 相 关 接 口NET_DVR_PlayBackByName、NET_DVR_GetFileByName），特别提醒在调用了回放或下载的接口后，还必须调用控制接口（NET_DVR_PlayBackControl_V40）的开始播放命令（NET_DVR_PLAYSTART）。 按时间回放或下载文件时，用户可以无需调用查找录像文件的相关接口，只要在接口中指定开始和结束时间，调用回放或下载接口（相关接口 NET_DVR_PlayBackByTime_V40、NET_DVR_GetFileByTime_V40）后，还必须调用控制接口（NET_DVR_PlayBackControl_V40）的开始播放命令（NET_DVR_PLAYSTART）。此时，将按照指定时间范围内最近的有录像的时间段开始回放或下载。用户也可以通过调用查找录像文件的相关接口，获取文件的开始和结束时间后，按这个时间范围指定回放或下载接口中的时间参数，最后还必须调用控制接口（NET_DVR_PlayBackControl_V40）的开始播放命令（NET_DVR_PLAYSTART）。  

调用实例代码  

## 3.4参数配置模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/7a8c11848b2579912f7f3f58d0cba7bc3bef681be336bb2673b2aff2baf5e91f.jpg)  
图 3.4 参数配置模块流程  

 实现参数配置首先必须做好初始化 SDK 和用户注册这两个步骤，将用户注册接口返回的 ID 号作为配置接口的首个参数。建议在每次设置某类参数之前，先调用获取参数的接口（NET_DVR_GetDVRConfig 或者 NET_DVR_GetDeviceConfig）得到完整的参数结构，修改需要更改的参数，作为设置参数接口中的输入参数，最后调用设置参数接口（NET_DVR_SetDVRConfig 或者 NET_DVR_SetDeviceConfig），返回成功即设置成功。  

## 3.5远程设备维护模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/d8d2190e00b81403eb2b5617fc3d3b7c5bd96f7e7ac30cc6f8d86bb4457a9a27.jpg)  
图 3.5 设备维护模块流程  

远程设备维护模块包括获取设备工作状态、远程升级、日志查找、恢复设备默认参数和导入、导出配置文件等功能。  

$\bullet$ 获取设备工作状态：可以获取到设备当前的硬盘状态、通道状态、报警输入和输出口状态、本地显示状态和语音通道状态等信息。相关接口有：NET_DVR_GetDVRWorkState_V30 等。  
$\bullet$ 远程升级：对设备进行升级，并且可以获取当前升级的进度和状态。相关接口有：NET_DVR_Upgrade、NET_DVR_GetUpgradeProgress、NET_DVR_GetUpgradeState 等。日志查找：可以搜索到当前设备的日志信息，包括报警、异常、操作和带 S.M.A.R.T 信息的日志。相关接口有：NET_DVR_FindDVRLog_V30、NET_DVR_FindNextLog_V30 等。恢复设备默认参数：调用接口 NET_DVR_RestoreConfig 能将设备的所有参数都恢复成默认值。导入、导出配置文件：将设备目前的所有配置信息导出保存或者将指定的配置信息导入到设备。相关接 口 有 ： NET_DVR_GetConfigFile_V30 、 NET_DVR_GetConfigFile 、 NET_DVR_SetConfigFile_EX 、NET_DVR_SetConfigFile 等。  

## 3.6语音对讲转发模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/f84eb8412c5a42ecec909035ca7ea2fa3a68fdf7dfce690ab891dbe79689f6fc.jpg)  
图 3.6 语音对讲和转发模块流程  

语音对讲功能实现 PC 机与设备间音频的发送和接收。在成功注册设备后调用NET_DVR_StartVoiceCom_V30 接口完成，同时在该接口中用户可以通过设置回调函数获取当前设备发送或者 PC 机采集的数据（按需要选择回调编码后或者 PCM 数据）。  

 语音转发功能实现将待发送的音频数据（编码后）转发给设备。首先，调用 NET_DVR_StartVoiceCom_MR_V30 接口启动与某台设备的语音转发（此时已建立与设备之间的连接，等待发送数据）。第二，准备好待发送的数据（需要经过编码），相对于上图中虚线框部分，如果数据已按本公司的压缩格式处理这部分就可以省略。数据源可以是从 PC 声卡中采集或是从文件中读取，但是需要经过本公司提供的压缩算法进行压缩处理，SDK 提供一套编码接口，方法如下：  

设备语音对讲音频编码格式为 G711：  
调用 NET_DVR_EncodeG711Frame 进行音频编码。  
设备语音对讲音频编码格式为 G722：  
1) NET_DVR_InitG722Encoder 初始化音频编码；  
2) NET_DVR_EncodeG722Frame 进行 G722 音频编码；  
3)当结束所有的编码过程，需要调用 NET_DVR_ReleaseG722Encoder 释放编码音频资源。设备语音对讲音频编码格式为 G726：  
1)NET_DVR_InitG726Encoder 初始化音频编码；  

2)NET_DVR_EncodeG726Frame 进行 G726 音频编码；3)当结束所有的编码过程，需要调用 NET_DVR_ReleaseG726Encoder 释放编码音频资源。第三，经过第二部的编码操作，我们可以每次得到固定大小的且经过编码后的数据，调用NET_DVR_VoiceComSendData 接口发送这些数据给设备。第四，从设备发送给客户端的数据可以通过 NET_DVR_StartVoiceCom_MR_V30 接口设置的回调函数获取，获取到的数据可以通过语音解码接口进行解码，获取 PCM 音频数据，输出到声卡输出或者做其他处理。最后，等所有的转发操作完成后，调用 NET_DVR_StopVoiceCom 接口结束与设备的语音转发连接。Windows 64 位或者 Linux 系统下只支持语音转发功能，语音对讲、语音广播、音频编解码接口均不支持  

## 3.7报警模块流程  

### 3.7.1 报警（布防）流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/281beccff95729efb82d96a0c8a16d0cda7bcf18b3608770b352ecbb9e6428cf.jpg)  
图 3.7 报警布防流程  

“布防”报警方式：是指 SDK 主动连接设备，并发起报警上传命令，设备发生报警立即发送给 SDK。  

$\bullet$ 由“报警（布防）的流程图”中看出，“布防”方式需要先进行用户注册（NET_DVR_Login_V30）。虚线框部分是实现报警信息上传的必要条件，主要完成相关的报警条件和处理方法的配置，参数配置的接口为NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig。支持的报警类型有移动侦测、视频信号丢失、遮挡  

和信号量报警，其中前三种报警类型对应的报警条件和处理方法的配置结构体是  
NET_DVR_PICCFG_V30，而信号量报警的配置结构体是 NET_DVR_ALARMINCFG_V30。这些参数如果已经  
配置完成，那么虚线框部分可以省略。接下来就是设置报警回调函数（NET_DVR_SetDVRMessageCallBack_V30 等），调用成功后还需要设置布防（NET_DVR_SetupAlarmChan_V41）。整个报警上传过程结束后还需要调用撤防接口等操作。  

调用实例代码  

### 3.7.2 报警（监听）流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/42aed2c4278dda6a6b5b26af4926a5e778d199a2e411134016ca912e921705bd.jpg)  
图 3.8 报警监听流程  

“监听”报警方式：是指 SDK 不主动发起连接设备，只是在设定的端口上监听接收设备主动上传的报警信息。  

 这个过程需要远程配置设备的报警主机地址（即 PC 机地址）和报警主机端口（即 PC 的监听端口），报警主机就在该端口上监听接收设备主动上传的报警信息。如果报警主机地址和报警主机端口已配置完成，那么“报警（监听）的流程图”中虚线框“用户注册”和“配置报警主机地址和端口”部分就可以省略，但事先没有配置，就必须调用参数配置接口（NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）对设备的网络参数（NET_DVR_NETCFG_V30）进行配置。而虚线框“配置报警条件和处理方法”部分与“布防”中的一致。对以上需要配置的参数都设置完后，调用 NET_DVR_StartListen_V30 函数，开启 SDK 的监听端口，准备接收设备上传的报警信息。  

$\bullet$ 该方式适用于多个设备向一台客户端上传报警，而且不需要设备登录即可完成，设备重启后不影响报警上传；缺点是设备只支持一个报警主机地址和端口号的配置。  

## 3.8透明通道模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/d0f6c296-efe8-4bba-aae9-d8f4e371986e/5ca5319d6e331c4fcfa7988a74782ac749f36d1706b8343177daccde27b7ccf3.jpg)  
图 3.9 透明通道模块流程  

 SDK 提供将 485 和 232 串口作为透明通道，要将 232 串口作为透明通道使用，首先必须在 232 串口的配 置 信 息 中 将 工 作 模 式 选 为 透 明 通 道 ， 具 体 方 法 是 调 用 接 口 NET_DVR_GetDVRConfig 和NET_DVR_SetDVRConfig 获取和设置参数 NET_DVR_RS232CFG 中的 dwWorkMode 值为透明通道。如果是485 串 口 作 为 透 明 通 道 ， 这 个 步 骤 可 以 省 略 ， 调 用 NET_DVR_SerialStart 建 立 透 明 通 道 和NET_DVR_SerialSend 发送数据。整个过程结束还需要断开透明通道（NET_DVR_SerialStop）等操作。  

# 4 函数调用实例  

## 4.1 预览模块的示例代码  

### 方式一 SDK 直接解码显示  

#include <stdio.h>   
#include <iostream>   
#include “Windows.h”   
#include “HCNetSDK.h”   
#include <time.h>   
using namespace std;   
typedef HWND (WINAPI \*PROCGETCONSOLEWINDOW)();   
PROCGETCONSOLEWINDOW GetConsoleWindow;   
void CALLBACK g_ExceptionCallBack(DWORD dwType, LONG lUserID, LONG lHandle, void \*pUser)   
{ char tempbuf[256] $=\{0\}.$ switch(dwType) { case EXCEPTION_RECONNECT: //预览时重连 printf(“----------reconnect-------- $\cdot\%\mathrm{d}\backslash\mathsf{n}^{\prime\prime}$ , time(NULL)); break; default: break; }   
}   
void main() { //-- //初始化 NET_DVR_Init(); //设置连接时间与重连时间 NET_DVR_SetConnectTime(2000, 1); NET_DVR_SetReconnect(10000, true); //-- // 获取控制台窗口句柄 HMODULE hKernel32 $=$ GetModuleHandle(“kernel32”); GetConsoleWindow $=$ (PROCGETCONSOLEWINDOW)GetProcAddress(hKernel32,”GetConsoleWindow”);  

//--// 注册设备LONG lUserID;NET_DVR_DEVICEINFO_V30 struDeviceInfo;lUserID $=$ NET_DVR_Login_V30(“192.0.0.64”, 8000, “admin”, “12345”, &struDeviceInfo);if (lUserID $<0$ ){printf(“Login error, $\%d\backslash{\mathfrak{n}}^{\prime\prime}$ , NET_DVR_GetLastError());NET_DVR_Cleanup();return;}//--//设置异常消息回调函数NET_DVR_SetExceptionCallBack_V30(0, NULL,g_ExceptionCallBack, NULL);//--//启动预览并设置回调数据流LONG lRealPlayHandle;HWND hWnd $=$ GetConsoleWindow(); //获取窗口句柄NET_DVR_PREVIEWINFO struPlayInfo $=\{0\}.$ ;struPlayInfo.hPlayWnd $=$ hWnd; //需要 SDK 解码时句柄设为有效值，仅取流不解码时可设为空struPlayInfo.lChannel $=1.$ //预览通道号struPlayInfo.dwStreamType $=0$ ; //0-主码流，1-子码流，2-码流 3，3-码流 4，以此类推struPlayInfo.dwLinkMode $=0_{\scriptscriptstyle-}$ ; //0- TCP 方式，1- UDP 方式，2- 多播方式，3- RTP 方式，4-RTP/RTSP，5-RSTP/HTTPstruPlayInfo.bBlocked $=1$ ; //0- 非阻塞取流，1- 阻塞取流lRealPlayHandle $=$ NET_DVR_RealPlay_V40(lUserID, &struPlayInfo, NULL, NULL);if (lRealPlayHandle $<0$ ){printf(“NET_DVR_RealPlay_V40 error\n”);NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;}Sleep(10000);//--//关闭预览NET_DVR_StopRealPlay(lRealPlayHandle);//注销用户NET_DVR_Logout(lUserID);//释放 SDK 资源NET_DVR_Cleanup();return;}  

### 方式二 实时流数据回调，用户自行处理码流数据（此处以软解显示为例）  

#include <stdio.h>  
#include <iostream>  
#include “Windows.h”  
#include “HCNetSDK.h”  
#include “plaympeg4.h”  
#include <time.h>  
using namespace std;  
typedef HWND (WINAPI \*PROCGETCONSOLEWINDOW)();  
PROCGETCONSOLEWINDOW GetConsoleWindow;  
LONG lPort; //全局的播放库 port 号  
void CALLBACK g_RealDataCallBack_V30(LONG lRealHandle, DWORD dwDataType, BYTE \*pBuffer,DWORD dwBufSize,void\* dwUser)  
{HWND hWnd=GetConsoleWindow();switch (dwDataType){case NET_DVR_SYSHEAD: //系统头if (!PlayM4_GetPort(&lPort))  //获取播放库未使用的通道号{break;}//m_iPort $=$ lPort;//第一次回调的是系统头，将获取的播放库 port 号赋值给全局 port，下次回调数据时即使用此 port 号播放if (dwBufSize $>0$ ){if (!PlayM4_SetStreamOpenMode(lPort, STREAME_REALTIME))  //设置实时流播放模式{break;}if (!PlayM4_OpenStream(lPort, pBuffer, dwBufSize, $1024^{*}1024;$ ) //打开流接口{break;}if (!PlayM4_Play(lPort, hWnd)) //播放开始{break;}break;case NET_DVR_STREAMDATA: //码流数据if (dwBufSize $>0$ && lPort $\dag=-1$ ){if (!PlayM4_InputData(lPort, pBuffer, dwBufSize)){break;}}break;default:  //其他数据if (dwBufSize $>0$ && lPort $\dag=-1$ ){if (!PlayM4_InputData(lPort, pBuffer, dwBufSize)){break;}}break;  
}  
void CALLBACK g_ExceptionCallBack(DWORD dwType, LONG lUserID, LONG lHandle, void \*pUser)  
{char tempbuf $[256]=\{0\};$ switch(dwType){case EXCEPTION_RECONNECT: //预览时重连printf(“- -reconnect-- --- $\cdot\%\mathrm{d}\backslash\mathsf{n}^{\prime\prime}$ , time(NULL));break;default:break;}  
}  
void main() {//--// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  
//-  
// 获取控制台窗口句柄  
HMODULE hKernel32 $=$ GetModuleHandle(“kernel32”);  
GetConsoleWindow $=$ (PROCGETCONSOLEWINDOW)GetProcAddress(hKernel32,”GetConsoleWindow”);  

//-// 注册设备LONG lUserID;NET_DVR_DEVICEINFO_V30 struDeviceInfo;lUserID $=$ NET_DVR_Login_V30(“172.0.0.100”, 8000, “admin”, “12345”, &struDeviceInfo);if (lUserID $<0$ ){printf(“Login error, %d\n”, NET_DVR_GetLastError());NET_DVR_Cleanup();return;}//-//设置异常消息回调函数NET_DVR_SetExceptionCallBack_V30(0, NULL,g_ExceptionCallBack, NULL);//-//启动预览并设置回调数据流LONG lRealPlayHandle;NET_DVR_PREVIEWINFO struPlayInfo $=\{0\};$ struPlayInfo.hPlayWnd $=$ hWnd; //需要 SDK 解码时句柄设为有效值，仅取流不解码时可设为空struPlayInfo.lChannel $=1;$ //预览通道号struPlayInfo.dwStreamType $=0$ ; //0-主码流，1-子码流，2-码流 3，3-码流 4，以此类推struPlayInfo.dwLinkMode $=0$ ; //0- TCP 方式，1- UDP 方式，2- 多播方式，3- RTP 方式，4-RTP/RTSP，5-RSTP/HTTPstruPlayInfo.bBlocked $=1$ ; //0- 非阻塞取流，1- 阻塞取流  

lRealPlayHandle $=$ NET_DVR_RealPlay_V40(lUserID, &struPlayInfo, g_RealDataCallBack_V30, NULL);   
if (lRealPlayHandle $<0$ )   
{ printf(“NET_DVR_RealPlay_V40 error\n”); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
Sleep(10000); //--   
//关闭预览   
NET_DVR_StopRealPlay(lRealPlayHandle); //注销用户   
NET_DVR_Logout(lUserID);   
NET_DVR_Cleanup();   
return;  

## 4.2回放和下载模块的示例代码  

### 示例一：查找录像文件并下载  

#include <stdio.h>   
#include <iostream>   
#include “Windows.h”   
#include “HCNetSDK.h”   
using namespace std;   
int saveRecordFile(int userId,char \* srcfile,char \* destfile)   
{ int bRes $=1$ ; int hPlayback $=0$ ; //按文件名下载录像 if( (hPlayback $=$ NET_DVR_GetFileByName(userId, srcfile, destfile)) $<0$ ) { printf( “GetFileByName failed. error[%d]\n”, NET_DVR_GetLastError()); $\mathsf{b R e s}\!=\!-1$ ; return bRes; } //开始下载 if(!NET_DVR_PlayBackControl_V40(hPlayback, NET_DVR_PLAYSTART, NULL,0,NULL,NULL)) { printf(“play back control failed [%d]\n”,NET_DVR_GetLastError()); $\mathsf{b R e s}{=}{-}1$ ; return bRes; } int $\mathsf{n P o s}=0,$ ; for $\mathsf{n P o s}=0;$ nPos < 100&&nPos>=0; nPos $=$ NET_DVR_GetDownloadPos(hPlayback)) { printf(“Be downloading...%d %%\n”, nPos);   //下载进度 Sleep(5000);  //millisecond } printf(“have got %d\n”, nPos); //停止下载 if(!NET_DVR_StopGetFile(hPlayback)) { printf(“failed to stop get file [%d]\n”,NET_DVR_GetLastError()); ${\mathsf{b R e s}}=-1$ ; return bRes; } printf(“%s\n”,srcfile); if(nPos<0||nPos>100) { printf(“download err [%d]\n”,NET_DVR_GetLastError()); $\mathsf{b R e s}{=}{-}1;$ ; return bRes; } else { return 0; }   
}   
void main() { //-- // 初始化 NET_DVR_Init(); //设置连接时间与重连时间 NET_DVR_SetConnectTime(2000, 1); NET_DVR_SetReconnect(10000, true);  

###  

### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30(“192.0.0.64”, 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, %d\n”, NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
} NET_DVR_FILECOND_V40 struFileCond= $\{0\}.$ ;   
struFileCond.dwFileType $=0\times\mathsf{F}\mathsf{F}$ ;   
struFileCond.lChannel $=1$ ;  //通道号   
struFileCond.dwIsLocked $=0\times\mathsf{F}\mathsf{F}$ ;   
struFileCond.dwUseCardNo $=0$ ;   
struFileCond.struStartTime.dwYear $=2011$ ; //开始时间 struFileCond.struStartTime.dwMonth $=3$ ;   
struFileCond.struStartTime.dwDay $=1.$ ;   
struFileCond.struStartTime.dwHour $=10$ ;   
struFileCond.struStartTime.dwMinute $=6$ ;   
struFileCond.struStartTime.dwSecond $=\mathtt{50}$ ;   
struFileCond.struStopTime.dwYear $=2011$ ;  //结束时间 struFileCond.struStopTime.dwMonth $=3$ ;   
struFileCond.struStopTime.dwDay $=1.$   
struFileCond.struStopTime.dwHour $=11.$ ;   
struFileCond.struStopTime.dwMinute $=7$ ;   
struFileCond.struStopTime.dwSecond $=0$ ;  

###  

### //查找录像文件  

int lFindHandle $=$ NET_DVR_FindFile_V40(lUserID, &struFileCond);   
if(lFindHandle $<0$ )   
{ printf(“find file fail,last error %d\n”,NET_DVR_GetLastError()); return;   
}   
NET_DVR_FINDDATA_V40 struFileData;   
while(true)   
{ //逐个获取查找到的文件信息 int result $=$ NET_DVR_FindNextFile_V40(lFindHandle, &struFileData); if(result $==$ NET_DVR_ISFINDING) { continue; } else if(result $==$ NET_DVR_FILE_SUCCESS) //获取文件信息成功 { char strFileName $[256]=\{0\};$ print(strFileName, $\mathbf{\nabla}^{\prime\prime}./\%\mathbf{S}^{\prime\prime}$ , struFileData.sFileName); saveRecordFile(lUserID, struFileData.sFileName,  strFileName); break; } else if(result $==$ NET_DVR_FILE_NOFIND || result $==$ NET_DVR_NOMO  

{ break; } else { printf(“find file fail for illegal get file state”); break; } } //停止查找 if(lFindHandle $>=0$ ) { NET_DVR_FindClose_V30(lFindHandle); } //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return; }  

### 示例二：按时间播放录像文件  

#include <stdio.h>  
#include <iostream>  
#include “Windows.h”  
#include “HCNetSDK.h”  
using namespace std;  
typedef HWND (WINAPI \*PROCGETCONSOLEWINDOW)();  
PROCGETCONSOLEWINDOW GetConsoleWindow;  
void main() {//--// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);//-// 获取控制台窗口句柄HMODULE hKernel32 $=$ GetModuleHandle(“kernel32”);  
GetConsoleWindow $=$ (PROCGETCONSOLEWINDOW)GetProcAddress(hKernel32,”GetConsoleWindow”);  

### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30(“192.0.0.64”, 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, %d\n”, NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

HWND hWnd $=$ GetConsoleWindow(); //获取窗口句柄  

NET_DVR_VOD_PARA struVodPara $=\{0\};$ struVodPara.dwSize $=$ sizeof(struVodPara); struVodPara.struIDInfo.dwChannel=1; //通道号 struVodPara.hWnd=hWnd; //回放窗口 struVodPara.struBeginTime.dwYear $=2013$ ; //开始时间 struVodPara.struBeginTime.dwMonth $=6$ ; struVodPara.struBeginTime.dwDay $=14;$ struVodPara.struBeginTime.dwHour $=9$ ; struVodPara.struBeginTime.dwMinute $=0$ ; struVodPara.struBeginTime.dwSecond $=0$ ; struVodPara.struEndTime.dwYear $=2013$ ; //结束时间 struVodPara.struEndTime.dwMonth $=6;$ ; struVodPara.struEndTime.dwDay $=14;$ struVodPara.struEndTime.dwHour $=10;$ struVodPara.struEndTime.dwMinute $=7$ ; struVodPara.struEndTime.dwSecond $=0$ ;  

###  

### //按时间回放  

int hPlayback;   
hPlayback $=$ NET_DVR_PlayBackByTime_V40(lUserID, &struVodPara);   
if(hPlayback $<0$ )   
{ printf(“NET_DVR_PlayBackByTime_V40 fail,last error %d\n”,NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;  

} //-- //开始 if(!NET_DVR_PlayBackControl_V40(hPlayback, NET_DVR_PLAYSTART,NULL, 0, NULL,NULL)) { printf(“play back control failed [%d]\n”,NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } Sleep(15000);  //millisecond if(!NET_DVR_StopPlayBack(hPlayback)) { printf(“failed to stop file [%d]\n”,NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return; }  

### 示例三：按时间下载录像文件  

<html><body><table><tr><td>#include <stdio.h></td></tr><tr><td>#include <iostream></td></tr><tr><td>#include "Windows.h"</td></tr><tr><td>#include “HCNetSDK.h"</td></tr><tr><td>usingnamespacestd;</td></tr><tr><td></td></tr><tr><td>void main() {</td></tr><tr><td>/1-</td></tr><tr><td>//初始化</td></tr><tr><td>NET_DVR_Init();</td></tr><tr><td>//设置连接时间与重连时间</td></tr><tr><td>NET_DVR_SetConnectTime(2000, 1); NET_DVR_SetReconnect(10000, true);</td></tr><tr><td></td></tr></table></body></html>  

### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30(“192.0.0.64”, 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, %d\n”, NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;  

NET_DVR_PLAYCOND struDownloadCond= $:\{0\};$ struDownloadCond.dwChannel=1; //通道号 struDownloadCond.struStartTime.dwYear $=2013$ ; //开始时间 struDownloadCond.struStartTime.dwMonth $=6.$ ; struDownloadCond.struStartTime.dwDay $=14;$ ; struDownloadCond.struStartTime.dwHour $=9$ ; struDownloadCond.struStartTime.dwMinute $=50$ ; struDownloadCond.struStartTime.dwSecond ${}=0$ ; struDownloadCond.struStopTime.dwYear $=2013$ ; //结束时间 struDownloadCond.struStopTime.dwMonth $=6;$ ; struDownloadCond.struStopTime.dwDay $=14;$ struDownloadCond.struStopTime.dwHour $=10;$ struDownloadCond.struStopTime.dwMinute $=7$ ; struDownloadCond.struStopTime.dwSecond $=0$ ;  

###  

### //按时间下载  

int hPlayback;   
hPlayback $=$ NET_DVR_GetFileByTime_V40(lUserID, “./test.mp4”,&struDownloadCond);   
if(hPlayback $<0$ )   
{ printf(“NET_DVR_GetFileByTime_V40 fail,last error %d\n”,NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
//--   
//开始下载   
if(!NET_DVR_PlayBackControl_V40(hPlayback, NET_DVR_PLAYSTART, NULL, 0, NULL,NULL))   
{ printf(“Play back control failed [%d]\n”,NET_DVR_GetLastError()); NET_DVR_Logout(lUserID);  

NET_DVR_Cleanup(); return; } int $\mathsf{n P o s}=0,$ ; for( $\mathsf{n P o s}=0;$ ; nPos < 100&&nPos> ${\tt s}{=}0$ ; nPos $=$ NET_DVR_GetDownloadPos(hPlayback)) { printf(“Be downloading... %d %%\n”,nPos); //下载进度 Sleep(5000);  //millisecond } if(!NET_DVR_StopGetFile(hPlayback)) { printf(“failed to stop get file [%d]\n”,NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } if(nPos<0||nPos>100) { printf(“download err [%d]\n”,NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } printf(“Be downloading... %d %%\n”,nPos); //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return; }  

## 4.3参数配置模块的示例代码  

配置压缩参数（NET_DVR_COMPRESSIONCFG_V30）  

#include <stdio.h> #include <iostream> #include “Windows.h” #include “HCNetSDK.h” using namespace std;  

void main() {  

###  

// 初始化  
NET_DVR_Init();  
//设置连接时间与重连时间  
NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

###  

### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30(“192.0.0.64”, 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, %d\n”, NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

printt;  

//获取压缩参数   
DWORD dwReturnLen;   
NET_DVR_COMPRESSIONCFG_V30 struParams $=\{0\};$   
iRet $=$ NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_COMPRESSCFG_V30, 1, \ &struParams, sizeof(NET_DVR_COMPRESSIONCFG_V30), &dwReturnLen);   
if (!iRet)   
{ printf(“NET_DVR_GetDVRConfig NET_DVR_GET_COMPRESSCFG_V30 error.\n”); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
//设置压缩参数   
struParams.struNormHighRecordPara.dwVideoBitrate $=22$ ;   
iRet $=$ NET_DVR_SetDVRConfig(lUserID, NET_DVR_SET_COMPRESSCFG_V30, 1, \ &struParams, sizeof(NET_DVR_COMPRESSIONCFG_V30));   
if (!iRet)   
{ printf(“NET_DVR_GetDVRConfig NET_DVR_SET_COMPRESSCFG_V30 error.\n”); NET_DVR_Logout(lUserID); NET_DVR_Cleanup();  

return; } //获取压缩参数 iRet $=$ NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_COMPRESSCFG_V30, 1, \ &struParams, sizeof(NET_DVR_COMPRESSIONCFG_V30), &dwReturnLen); if (!iRet) { printf(“NET_DVR_GetDVRConfig NET_DVR_GET_COMPRESSCFG_V30 error.\n”); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } printf(“Video Bitrate is $\%d\backslash{\mathsf{n}}^{\prime\prime}$ , struParams.struNormHighRecordPara.dwVideoBitrate); //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return; }  

## 4.4远程设备维护模块的示例代码  

### 日志查询  

<html><body><table><tr><td>#include <stdio.h></td></tr><tr><td>#include<iostream></td></tr><tr><td>#include "Windows.h"</td></tr><tr><td>#include"HCNetSDK.h"</td></tr><tr><td>using namespace std;</td></tr><tr><td></td></tr><tr><td>void main() {</td></tr><tr><td>//--</td></tr><tr><td>//初始化</td></tr><tr><td>NET_DVR_Init();</td></tr><tr><td>//设置连接时间与重连时间 NET_DVR_SetConnectTime(2000, 1);</td></tr><tr><td>NET_DVR_SetReconnect(10000, true);</td></tr><tr><td></td></tr><tr><td></td></tr></table></body></html>  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30(“192.0.0.64”, 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, $\%{d}\backslash{\mathfrak{n}}^{\prime\prime}$ , NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;  

NET_DVR_TIME struStartTime, struStopTime; struStartTime.dwYear $=2011$ ; struStartTime.dwMonth $=3$ ; struStartTime.dwDay $=2$ ; struStartTime.dwHour $=9.$ ; struStartTime.dwMinute $=0;$ struStartTime.dwSecond $=0;$  

struStopTime.dwYear $=2011$ ;   
struStopTime.dwMonth $=3$ ;   
struStopTime.dwDay $=2$ ;   
struStopTime.dwHour $=9$ ;   
struStopTime.dwMinute $=10_{\cdot}$ ;   
struStopTime.dwSecond ${\it\Delta\phi}=0;$  

###  

### //查找日志  

int lFindHandle $=$ NET_DVR_FindDVRLog_V30(lUserID, 0, 0, 0, &struStartTime, &struStopTime, FALSE);   
if(lFindHandle $<0$ )   
{ printf(“find log fail,last error %d\n”,NET_DVR_GetLastError()); return;   
}   
NET_DVR_LOG_V30 struLog;   
while(true)   
{ int result $=$ NET_DVR_FindNextLog_V30(lFindHandle, &struLog); if(result $==$ NET_DVR_ISFINDING) { printf(“finding\n”); continue; } else if(result $==$ NET_DVR_FILE_SUCCESS) { char strLog[256] = {0}; prin $\mathbf{tf}(^{\prime\prime}|0\mathbf{g};^{\mathcal{V}_{0}04}\mathbf{d}-^{\mathcal{V}_{0}02}\mathbf{d}-^{\mathcal{V}_{0}02}\mathbf{d}\;^{\mathcal{V}_{0}02}\mathbf{d};^{\mathcal{V}_{0}02}\mathbf{d};^{\mathcal{V}_{0}02}\mathbf{d}\backslash^{\mathfrak{n}^{\prime\prime}}$ , struLog.strLogTime.dwYear, struLog.strLogTime.dwMonth,   
ruLog.strLogTime.dwDay, \ struLog.strLogTime.dwHour,struLog.strLogTime.dwMinute, struLog.strLogTime.dwSecond); } else if(result $==$ NET_DVR_FILE_NOFIND || result $==$ NET_DVR_NOMOREFILE) { printf(“find ending\n”); break; } else { printf(“find log fail for illegal get file state $\setminus\")$ ; break; } } //停止日志查询 if(lFindHandle $>0$ ) { NET_DVR_FindLogClose_V30(lFindHandle); }   
//注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return;  

## 4.5语音对讲转发模块的示例代码  

### 示例一：语音对讲  

#include <stdio.h>  
#include <iostream>  
#include “Windows.h”  
#include “HCNetSDK.h”  
using namespace std;  
void CALLBACK fVoiceDataCallBack(LONG lVoiceComHandle, char \*pRecvDataBuffer, DWORD dwBufSize, BYTE byAudioFlag,void\*pUser)  
{printf(“receive voice data, $\%d\backslash{\mathsf{n}}^{\prime\prime}.$ , dwBufSize);  
}  
void main() {//--// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

###  

### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30( $^{\prime\prime}192.0.0.64^{\prime\prime}$ , 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, %d\n”, NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

### //语音对讲  

LONG lVoiceHanle;   
lVoiceHanle $=$ NET_DVR_StartVoiceCom_V30(lUserID, 1,0, fVoiceDataCallBack, NULL);   
if (lVoiceHanle $<0$ )   
{ printf(“NET_DVR_StartVoiceCom_V30 error, %d!\n”, NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
Sleep(5000);  //millisecond   
//关闭语音对讲   
if (!NET_DVR_StopVoiceCom(lVoiceHanle))   
{ printf(“NET_DVR_StopVoiceCom error, $\%d!\backslash n^{\prime\prime}$ , NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
} //注销用户   
NET_DVR_Logout(lUserID); //释放 SDK 资源   
NET_DVR_Cleanup();   
return;  

## 4.6报警模块的示例代码  

### 布防报警的示例代码：  

#include <stdio.h>  
#include <iostream>  
#include “Windows.h”  
#include “HCNetSDK.h”  
using namespace std;  
void CALLBACK MessageCallback(LONG lCommand, NET_DVR_ALARMER \*pAlarmer, char \*pAlarmInfo, DWORD dwBufLen, void\*  
pUser)  
{int i;NET_DVR_ALARMINFO struAlarmInfo;memcpy(&struAlarmInfo, pAlarmInfo, sizeof(NET_DVR_ALARMINFO));switch(lCommand){case COMM_ALARM:{switch (struAlarmInfo.dwAlarmType){case 3: //移动侦测报警for $(1{=}0;\dot{1}{<}16;\dot{1}{+}+)$ //#define MAX_CHANNUM   16  //最大通道数{if (struAlarmInfo.dwChannel[i] $==1$ ){printf(“发生移动侦测报警的通道号 $\%{d}\backslash{\mathsf{n}}^{\prime\prime},\mathsf{i}{+}1)$ ;}}break;default:break;}}break;default:break;}  
}  
void main() {//--// 初始化  
NET_DVR_Init();  
//设置连接时间与重连时间  
NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

###  

### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30 $^{\prime\prime}192.0.0.64^{\prime\prime}$ , 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, $\%d\backslash{\mathfrak{n}}^{\prime\prime}$ , NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

//设置报警回调函数 NET_DVR_SetDVRMessageCallBack_V30(MessageCallback, NULL);  

### //启用布防  

LONG lHandle;  
NET_DVR_SETUPALARM_PARAM  struAlarmParam $=\{0\};$   
struAlarmParam.dwSize $=$ sizeof(struAlarmParam);  
struAlarmParam.byAlarmInfoType ${=}0$ ;  
//设备是否支持新的报警信息通过登录返回的 NET_DVR_DEVICEINFO_V30 中参数 bySupport1 & 0x80 判断  
lHandle $=$ NET_DVR_SetupAlarmChan_V41(lUserID, & struAlarmParam);  
if (lHandle $<0$ )  
{printf(“NET_DVR_SetupAlarmChan_V41 error, %d\n”, NET_DVR_GetLastError());NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;  

} Sleep(5000); //撤销布防上传通道 if (!NET_DVR_CloseAlarmChan_V30(lHandle)) { printf(“NET_DVR_CloseAlarmChan_V30 error, %d\n”, NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return; }  

### 监听报警的示例代码：  

#include <stdio.h>  
#include <iostream>  
#include “Windows.h”  
#include “HCNetSDK.h”  
using namespace std;  
void CALLBACK MessageCallback(LONG lCommand, NET_DVR_ALARMER \*pAlarmer, char \*pAlarmInfo, DWORD dwBufLen, void\*  
pUser)  
{int i;NET_DVR_ALARMINFO struAlarmInfo;memcpy(&struAlarmInfo, pAlarmInfo, sizeof(NET_DVR_ALARMINFO));switch(lCommand){case COMM_ALARM:{switch (struAlarmInfo.dwAlarmType){case 3: //移动侦测报警for $(1{=}0;\dot{1}{<}16;\dot{1}{+}+)$ //#define MAX_CHANNUM   16  //最大通道数{if (struAlarmInfo.dwChannel[i] $==1$ ){printf(“发生移动侦测报警的通道号 $\%{d}\backslash{\mathsf{n}}^{\prime\prime},\mathsf{i}{+}1)$ ;}}break;default:break;}}break;default:break;}  
}  
void main() {//--// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

### //--  

### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30(“172.0.0.100”, 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, %d\n”, NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

//设置报警回调函数 NET_DVR_SetDVRMessageCallBack_V30(MessageCallback, NULL);  

### //启用监听  

LONG lHandle;   
lHandle $=$ NET_DVR_StartListen_V30(NULL,7200, MessageCallback, NULL);   
if (lHandle $<0$ )   
{ printf(“NET_DVR_StartListen_V30 error, $\%{d}\backslash{\mathfrak{n}}^{\prime\prime}$ , NET_DVR_GetLastError()); NET_DVR_Logout(lUserID);  

NET_DVR_Cleanup(); return; } Sleep(5000); //停止监听 if (!NET_DVR_StopListen_V30(lHandle)) { printf(“NET_DVR_StopListen_V30 error, %d\n”, NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return; }  

## 4.7透明通道模块的示例代码  

#include <stdio.h>  
#include <iostream>  
#include “Windows.h”  
#include “HCNetSDK.h”  
using namespace std;  
//回调透传数据函数的外部实现  
void CALLBACK g_fSerialDataCallBack(LONG lSerialHandle, char \*pRecvDataBuffer, DWORD dwBufSize, DWORD dwUser)  
{//…… 处理接收到的透传数据，pRecvDataBuffer 中存放接收到的数据  
}  
void main() {//--// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

###  

### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30(“192.0.0.64”, 8000, “admin”, “12345”, &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf(“Login error, $\%{d}\backslash{\mathfrak{n}}^{\prime\prime}$ , NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

//设置 232 为透明通道模式（使用 232 透明通道时调用，485 不需要）DWORD dwReturned $=0$ ;NET_DVR_RS232CFG_V30 struRS232Cfg;memset(&struRS232Cfg, 0, sizeof(NET_DVR_RS232CFG_V30));if (!NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_RS232CFG_V30, 0, &struRS232Cfg, sizeof(NET_DVR_RS232CFG_V30),&dwReturned)){printf(“NET_DVR_GET_RS232CFG_V30 error, %d\n”, NET_DVR_GetLastError());NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;}struRS232Cfg.struRs232.dwWorkMode $=2$ ;//设置 232 为透明通道模式；0：窄带传输，1：控制台，2：透明通道if (!NET_DVR_SetDVRConfig(lUserID, NET_DVR_SET_RS232CFG_V30, 0, &(struRS232Cfg), sizeof(NET_DVR_RS232CFG))){printf(“NET_DVR_SET_RS232CFG_V30 error, %d\n”, NET_DVR_GetLastError());NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;}  

//建立透明通道   
LONG lTranHandle;   
int iSelSerialIndex $=1;//1;232$ 串口；2:485 串口   
lTranHandle $=$ NET_DVR_SerialStart(lUserID, iSelSerialIndex, g_fSerialDataCallBack, lUserID);   
//设置回调函数获取透传数据   
if (lTranHandle $<0$ )   
{ printf("NET_DVR_SerialStart error, %d\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID);  

NET_DVR_Cleanup();  

return;}//通过透明通道发送数据LONG lSerialChan $=0;//$ 使用 485 时该值有效，从 1 开始；232 时设置为 0char szSendBuf[ ${}^{1016}]=\{0\};$ if (!NET_DVR_SerialSend(lTranHandle, lSerialChan, szSendBuf, sizeof(szSendBuf)))//szSendBuf 为发送数据的缓冲区{printf("NET_DVR_SerialSend error, $\%d\backslash{\mathsf{n}}^{\prime\prime}$ , NET_DVR_GetLastError());NET_DVR_SerialStop(lTranHandle);NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;}//断开透明通道NET_DVR_SerialStop(lTranHandle);//注销用户NET_DVR_Logout(lUserID);//释放 SDK 资源NET_DVR_Cleanup();return;  

# 5 函数说明  

## 5.1SDK 初始化  

### 5.1.1 初始化 SDK NET_DVR_Init  

函  数： BOOL NET_DVR_Init()  
参  数： 无  
返回值： TRUE 表示成功，FALSE 表示失败。说  明： 调用设备网络 SDK 其他函数的前提。  

### 5.1.2 释放 SDK 资源 NET_DVR_Cleanup  

函  数： BOOL NET_DVR_Cleanup()  
参  数： 无  
返回值： TRUE 表示成功，FALSE 表示失败。在结束之前最后调用。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

## 5.2SDK 本地功能  

### SDK 本地参数配置  

### 5.2.1 获取 SDK 本地参数 NET_DVR_GetSDKLocalCfg  

函  数： BOOL NET_DVR_GetSDKLocalCfg(NET_SDK_LOCAL_CFG_TYPE enumType, void \*lpOutBuff)  
参  数： [in] enumType 配置类型，不同的取值对应不同的 SDK 参数，详见表 5.1[out] lpOutBuff 输出参数，不同的配置类型，输出参数对应不同的结构，详见表5.1  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.1 本地参数类型  


<html><body><table><tr><td>enumType宏定义</td><td>类型值 含义</td><td></td><td>lpOutBuff对应结构体</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_TCP_PORT_BIND</td><td>0</td><td>本地TCP端口绑定配置</td><td>NET_DVR_LOCAL_TCP_PORT_BIND_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_UDP_PORT_BIND</td><td></td><td>本地UDP端口绑定配置</td><td>NET_DVR_LOCAL_UDP_PORT_BIND_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_MEM_POOL</td><td>2</td><td>内存池本地配置</td><td>NET_DVR_LOCAL_MEM_POOL_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_MODULE_RECV_TIMEOUT</td><td>3</td><td>按模块配置超时时间</td><td>NET_DVR_LOCAL_MODULE_RECV_TIMEOUT_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_ABILITY_PARSE</td><td>4</td><td>是否使用能力集解析库</td><td>NET_DVR_LOCAL_ABILITY_PARSE_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_TALK_MODE</td><td>5</td><td>对讲模式配置</td><td>NET_DVR_LOCAL_TALK_MODE_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_CHECK_DEV</td><td>10</td><td>心跳交互间隔时间配置</td><td>NET_DVR_LOCAL_CHECK_DEV</td></tr></table></body></html>  

返回目录  

### 5.2.2 设置 SDK 本地参数 NET_DVR_SetSDKLocalCfg  

函  数： BOOL NET_DVR_SetSDKLocalCfg(NET_SDK_LOCAL_CFG_TYPE enumType, void\* const lpInBuff)  

参  数： [in] enumType 配置类型，不同的取值对应不同的 SDK 参数，详见表 5.2[in] lpInBuff 输入参数，不同的配置类型，输出参数对应不同的结构，详见  

5.2  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.2 本地参数类型  


<html><body><table><tr><td>enumType宏定义</td><td>类型值 含义</td><td></td><td>lplnBuff对应结构体</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_TCP_PORT_BIND</td><td>0</td><td>本地TCP端口绑定配置</td><td>NET_DVR_LOCAL_TCP_PORT_BIND_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_UDP_PORT_BIND</td><td>1</td><td>本地UDP端口绑定配置</td><td>NET_DVR_LOCAL_UDP_PORT_BIND_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_MEM_POOL</td><td>2</td><td>内存池本地配置</td><td>NET_DVR_LOCAL_MEM_POOL_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_MODULE_RECV_TIMEOUT</td><td>3</td><td>按模块配置超时时间</td><td>NET_DVR_LOCAL_MODULE_RECV_TIMEOUT_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_ABILITY_PARSE</td><td>4</td><td>是否使用能力集解析库</td><td>NET_DVR_LOCAL_ABILITY_PARSE_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_TALK_MODE</td><td>5</td><td>对讲模式配置</td><td>NET_DVR_LOCAL_TALK_MODE_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_CHECK_DEV</td><td>10</td><td>心跳交互间隔时间配置</td><td>NET_DVR_LOCAL_CHECK_DEV</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_CHAR_ENCODE</td><td>13</td><td>配置字符编码相关处理回调</td><td>NET_DVR_LOCAL_BYTE_ENCODE_CONVERT</td></tr><tr><td>NET_DVR_LOCAL_CFG_TYPE_LOG</td><td>15</td><td>日志参数配置</td><td>NET_DVR_LOCAL_LOG_CFG</td></tr></table></body></html>  

### 连接和接收超时时间及重连设置  

### 5.2.3 设置网络连接超时时间和连接尝试次数 NET_DVR_SetConnectTime  

函  数： BOOL NET_DVR_SetConnectTime(DWORD dwWaitTime,DWORD dwTryTime)  
参  数： [in]dwWaitTime 超时时间，单位毫秒，取值范围[300,75000]，实际最大超时时间因系统的 connect 超时时间而不同。[in]dwTryTimes 连接尝试次数（保留）  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： SDK 默认建立连接的超时时间为 3 秒。SDK4.0 及以后版本中当设置的超时时间超过或低于限制的值时接口不返回失败，将取最接近的上下限限制值作为实际的超时时间。  

返回目录  

### 5.2.4 设置重连功能 NET_DVR_SetReconnect  

函  数： BOOL NET_DVR_SetReconnect (DWORD dwInterval,BOOL bEnableRecon)  
参  数： [in]dwInterval 重连间隔，单位:毫秒[in]bEnableRecon 是否重连，0-不重连，1-重连，参数默认为 1  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口可以同时控制预览、透明通道和布防的重连功能。不调用该接口时，SDK 默认启动预览、透明通道和布防的重连功能，重连时间间隔为 5 秒。  

返回目录  

### 5.2.5 设置接收超时时间 NET_DVR_SetRecvTimeOut  

函  数： BOOL NET_DVR_SetRecvTimeOut(DWORD nRecvTimeOut)  
参  数： [in] nRecvTimeOut 接收超时时间，单位毫秒，默认为 5000，最小为 3000 毫秒  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口用于设置接收超时时间，例如预览接收实时流数据、回放下载接收录像数据、报警接收报警信息等接收超时时间。  

### 多网卡绑定  

### 5.2.6 获取所有 IP，用于支持多网卡接口 NET_DVR_GetLocalIP  

函  数： BOOL NET_DVR_GetLocalIP(char strIP[16][16], DWORD \*pValidNum, BOOL \*pEnableBind)参  数： [out] strIP 存放 IP 的缓冲区，不能为空  

[out] pValidNum 所有有效 IP 的数量[out] pEnableBind 是否绑定  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口获取客户端本地多网卡的所有 IP 地址，可以通过接口 NET_DVR_SetValidIP 选择要使用的IP 地址。  

返回目录  

### 5.2.7 设置 IP 绑定 NET_DVR_SetValidIP  

函  数： BOOL NET_DVR_SetValidIP(DWORD dwIPIndex, BOOL bEnableBind)  

参  数： [in] dwIPIndex 选择使用的 IP 下标，由 NET_DVR_GetLocalIP 获取[in] bEnableBind 是否绑定  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### SDK 版本、状态和能力  

### 5.2.8 获取 SDK 的版本号和 build 信息 NET_DVR_GetSDKBuildVersion  

函  数： DWORD NET_DVR_GetSDKBuildVersion()  

参  数：  
返回值： 获取 SDK 的版本号和 build 信息。  
说  明： SDK 的版本号和 build 信息。2 个高字节表示版本号 ： $25\sim\!32$ 位表示主版本号， $17^{\sim}24$ 位表示次版本号；2 个低字节表示 build 信息。如 0x03000101：表示版本号为 3.0，build 号是 0101。  

返回目录  

### 5.2.9 获取当前 SDK 的状态信息 NET_DVR_GetSDKState  

函  数： BOOL NET_DVR_GetSDKState( LPNET_DVR_SDKSTATE pSDKState);  
参  数： [out]pSDKState SDK 状态信息，详见结构体：NET_DVR_SDKSTATE  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.2.10 获取当前 SDK 的功能信息 NET_DVR_GetSDKAbility  

函  数： BOOL NET_DVR_GetSDKAbility( LPNET_DVR_SDKABL pSDKAbl)参  数： [out] pSDKAbl SDK 功能信息，详见结构体：NET_DVR_SDKABL返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通  

过错误码判断出错原因。  

说  明：  

### SDK 启用写日志  

### 5.2.11 启用写日志文件 NET_DVR_SetLogToFile  

函  数： BOOL NET_DVR_SetLogToFile(DWORD bLogEnable,char\* strLogDir,BOOL bAutoDel)参  数： [in]bLogEnable 日志的等级（默认为 0）：  

0-表示关闭日志1-表示只输出 ERROR 错误日志2-输出 ERROR 错误信息和 DEBUG 调试信息3-输出 ERROR 错误信息、DEBUG 调试信息和 INFO 普通信息等所有信息[in]strLogDir 日志文件的路径，windows 默认值为"C:\\SdkLog\\"；linux 默认值"/home/sdklog/"[in]bAutoDel 是否删除超出的文件数，默认值为 TRUE  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

：  日志文件路径必须是绝对路径，且以"\\"结尾，例如"C:\\SdkLog\\"，建议用户先手动创建文件。若未指定文件路径，则采用默认路径"C:\\SdkLog\\"。 可多次调用该接口创建新的日志文件，更改目录时到下一次写文件时才会使用新的目录写文件。 bAutoDel 为 TRUE 时表示覆盖模式，日志文件个数超过 SDK 限制个数时将会自动删除超出的文件。SDK 限制个数默认为 10 个，可以调用接口 NET_DVR_SetSDKLocalCfg(配置类型：NET_DVR_LOCAL_CFG_TYPE_LOG)进行修改配置。  

### 异常消息回调  

### 5.2.12 注册异常消息回调函数 NET_DVR_SetExceptionCallBack_V30  

函  数： Windows 系统下：BOOL  NET_DVR_SetExceptionCallBack_V30 (UINT nMessage,HWND hWnd,fExceptionCallBackcbExceptionCallBack,void\* pUser)Linux 系统下：BOOL NET_DVR_SetExceptionCallBack_V30(UINT nMessage,void\* hWnd,fExceptionCallBackcbExceptionCallBack,void\* pUser)  
参  数： [in]nMessage 消息,Linux 下该参数保留[in]hWnd 接收异常消息的窗口句柄，Linux 下该参数保留[in]cbExceptionCallBack 接收异常消息的回调函数，回调当前异常的相关信息  

<html><body><table><tr><td colspan="2">[in]pUser 用户数据</td></tr><tr><td colspan="2">typedef void(CALLBACK* fExceptionCalIBack)(DWORD dwType, LONG IUserID, LONG IHandle, void</td></tr><tr><td>* pUser) [out]dwType</td><td>异常或重连等消息的类型，详见表 5.3</td></tr><tr><td>[out]luserlD</td><td>登录ID</td></tr><tr><td>[out]lHandle</td><td>出现异常的相应类型的句柄</td></tr><tr><td>[out]pUser</td><td>用户数据</td></tr></table></body></html>  

表 5.3 异常消息类型  


<html><body><table><tr><td>dwType 宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>EXCEPTION_EXCHANGE</td><td>0x8000</td><td>用户交互时异常（注册心跳超时，心跳间隔为2分钟)</td></tr><tr><td>EXCEPTION_AUDIOEXCHANGE</td><td>0x8001</td><td>语音对讲异常</td></tr><tr><td>EXCEPTION_ALARM</td><td>0x8002</td><td>报警异常</td></tr><tr><td>EXCEPTION_PREVIEW</td><td>0x8003</td><td>网络预览异常</td></tr><tr><td>EXCEPTION_SERIAL</td><td>0x8004</td><td>透明通道异常</td></tr><tr><td>EXCEPTION_RECONNECT</td><td>0x8005</td><td>预览时重连</td></tr><tr><td>EXCEPTION_ALARMRECONNECT</td><td>0x8006</td><td>报警时重连</td></tr><tr><td>EXCEPTION_SERIALRECONNECT</td><td>0x8007</td><td>透明通道重连</td></tr><tr><td>SERIAL_RECONNECTSUCCESS</td><td>0x8008</td><td>透明通道重连成功</td></tr><tr><td>EXCEPTION_PLAYBACK</td><td>0x8010</td><td>回放异常</td></tr><tr><td>EXCEPTION_DISKFMT</td><td>0x8011</td><td>硬盘格式化</td></tr><tr><td>EXCEPTION_EMAILTEST</td><td>0x8013</td><td>邮件测试异常</td></tr><tr><td>EXCEPTION_BACKUP</td><td>0x8014</td><td>备份异常</td></tr><tr><td>PREVIEW_RECONNECTSUCCESS</td><td>0x8015</td><td>预览时重连成功</td></tr><tr><td>ALARM_RECONNECTSUCCESS</td><td>0x8016</td><td>报警时重连成功</td></tr><tr><td>RESUME_EXCHANGE</td><td>0x8017</td><td>用户交互恢复</td></tr><tr><td>NETWORK_FLOWTEST_EXCEPTION</td><td>0x8018</td><td>网络流量检测异常</td></tr><tr><td>EXCEPTION_PICPREVIEWRECONNECT</td><td>0x8019</td><td>图片预览重连</td></tr><tr><td>PICPREVIEW_RECONNECTSUCCESS</td><td>0x8020</td><td>图片预览重连成功</td></tr><tr><td>EXCEPTION_PICPREVIEW</td><td>0x8021</td><td>图片预览异常</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说明：Windows 下该函数的 hWnd 和 cbExceptionCallBack 不能同时为 NULL,Linux下 cbExceptionCallBack不能设置为 NULL，否则将接收不到异常消息。如果此结构是以回调方式反馈异常消息，那么应用程序中的异常回调函数实现如下，该函数中的参数 dwType 表示异常消息类型（见上表）；lHandle 表示发生异常的相应类型的句柄。  

### 示例代码：  

//注册接收异常消息的回调函数   
NET_DVR_SetExceptionCallBack_V30(WM_NULL, NULL, g_ExceptionCallBack, NULL); //接收异常消息的回调函数的外部实现  

<html><body><table><tr><td colspan="2">void CALLBACK g_ExceptionCalIBack(DWORD dwType, LONG IUserID, LONG IHandle, void *pUser) {</td></tr><tr><td colspan="2">char tempbuf[256];</td></tr><tr><td colspan="2"></td></tr><tr><td colspan="2">ZeroMemory(tempbuf,256);</td></tr><tr><td colspan="2">switch(dwType)</td></tr><tr><td colspan="2">{ caSe EXCEPTION_AUDIOEXCHANGE: //语音对讲时网络异常</td></tr><tr><td colspan="2">sprintf(tempbuf,"语音对讲时网络异常!!!");</td></tr><tr><td colspan="2">TRACE("%s",tempbuf);</td></tr><tr><td colspan="2">//TODO：关闭语音对讲</td></tr><tr><td colspan="2">break;</td></tr><tr><td colspan="2">case EXCEPTION_ALARM: //报警上传时网络异常</td></tr><tr><td colspan="2">sprintf(tempbuf,"报警上传时网络异常!!!");</td></tr><tr><td colspan="2">TRACE("%s",tempbuf);</td></tr><tr><td colspan="2">//TODO：关闭报警上传</td></tr><tr><td colspan="2">break;</td></tr><tr><td colspan="2">case EXCEPTION_PREVIEW: //网络预览时异常</td></tr><tr><td colspan="2">sprintf(tempbuf,"网络预览时网络异常!!");</td></tr><tr><td colspan="2"></td></tr><tr><td colspan="2">TRACE("%s",tempbuf);</td></tr><tr><td colspan="2">//TODO：关闭网络预览</td></tr><tr><td colspan="2">break;</td></tr><tr><td colspan="2">case EXCEPTION_SERIAL: //透明通道传输时异常</td></tr><tr><td colspan="2">sprintf(tempbuf,"透明通道传输时网络异常!!!");</td></tr><tr><td colspan="2">TRACE("%s",tempbuf);</td></tr><tr><td colspan="2">I/TODO：关闭透明通道 break;</td></tr><tr><td colspan="2">//预览时重连</td></tr><tr><td colspan="2">caseEXCEPTION_RECONNECT:</td></tr><tr><td colspan="2">break;</td></tr><tr><td colspan="2">default:</td></tr><tr><td colspan="2">break;</td></tr><tr><td colspan="2"></td></tr><tr><td colspan="2">{</td></tr></table></body></html>  

### 获取错误信息  

### 5.2.13 返回最后操作的错误码 NET_DVR_GetLastError  

函  数： DWORD NET_DVR_GetLastError()  
参  数：  
返回值： 返回最后操作的错误码。详见错误码宏定义  
说  明： 返回值为错误码。错误码主要分为网络通讯库错误码、RTSP 通讯库错误码和软硬解库错误码。  

### 5.2.14 返回最后操作的错误码信息 NET_DVR_GetErrorMsg  

函  数： char\* NET_DVR_GetErrorMsg(LONG   \*pErrorNo)  
参  数： [out]pErrorNo 错误码数值的指针  
返回值： 返回值为错误码信息的指针。错误码主要分为网络通讯库错误码、RTSP 通讯库错误码和软硬解库错误码。详见错误码宏定义  

说  明：  

## 5.3用户注册  

### 5.3.1 激活设备 NET_DVR_ActivateDevice  

函  数： BOOL NET_DVR_ActivateDevice(char\* sDVRIP, WORD wDVRPort, LPNET_DVR_ACTIVATECFGlpActivateCfg)  
参  数： [in]sDVRIP 设备 IP 地址[in]wDVRPort 设备端口[in]lpActivateCfg 激活参数，包括激活使用的初始密码  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 出厂设备需要先激活，然后再使用激活使用的初始密码登录设备。  

### 5.3.2 IPServer 或者 DDNS 域名解析，获取动态 IP 地址和端口号  

NET_DVR_GetDVRIPByResolveSvr_EX  

函  数： BOOL NET_DVR_GetDVRIPByResolveSvr_EX (char\* sServerIP, WORD wServerPort, BYTE\* sDVRName,WORD wDVRNameLen, BYTE\* sDVRSerialNumber, WORD wDVRSerialLen, char\* sGetIP, DWORD\*dwPort)  

参  数： [in]sServerIP 解析服务器的 IP 地址[in]wServerPort 解析服务器的端口号，IP Server 解析服务器端口号为 7071，HiDDNS 服务器的端口号为 80[in]sDVRName 设备名称[in]wDVRNameLen 设备名称的长度[in]sDVRSerialNumber 设备的序列号[in]wDVRSerialLen 设备序列号的长度[out]sGetIP 获取到的设备 IP 地址指针[out]dwPort 获取到的设备端口号指针  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中的设备名称和设备序列号不能同时为空。通过设备域名或者序列号解析出设备当前 IP地址和端口，然后调用 NET_DVR_Login_V40 登录设备。支持的解析服务器有 IPServer 和 hiDDNS。  

### 5.3.3 用户注册设备 NET_DVR_Login_V40  

函  数： LONG NET_DVR_Login_V40(LPNET_DVR_USER_LOGIN_INFO pLoginInfo, LPNET_DVR_DEVICEINFO_V40 lpDeviceInfo)  

参  数： [in]pLoginInfo 登录参数，包括设备地址、登录用户、密码等[out]lpDeviceInfo 设备信息(同步登录即 pLoginInfo 中 bUseAsynLogin 为 0 时有效)  

返回值： 异步登录的状态、用户 ID 和设备信息通过 NET_DVR_USER_LOGIN_INFO 结构体中设置的回调函数(fLoginResultCallBack)返回。对于同步登录，接口返回-1 表示登录失败，其他值表示返回的用户 ID 值。用户 ID 具有唯一性，后续对设备的操作都需要通过此 ID 实现。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

·pLoginlnfo中 bUseAsynLogin为0时登录为同步模式,接口返回成功即表示登录成功;pLoginlnfo中 bUseAsynLogin 为 1 时登录为异步模式，登录是否成功在输入参数设置的回调函数中返回。  
 设备同时最多允许 128 个用户注册。  
 SDK 支持 2048 个注册，返回 UserID 的取值范围为 $0^{\sim}2047$ 。  

### 5.3.4 用户注销 NET_DVR_Logout  

函  数： BOOL NET_DVR_Logout(LONG lUserID)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.4获取设备能力集  

### 5.4.1 获取设备能力集 NET_DVR_GetDeviceAbility  

函  数： BOOL NET_DVR_GetDeviceAbility(LONG lUserID, DWORD dwAbilityType, char\* pInBuf, DWORD dwInLength, char\* pOutBuf, DWORD dwOutLength)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwAbilityType 能力类型，详见表 5.4[in] pInBuf 输入缓冲区指针（按照设备规定的能力参数的描述方式组合，XML 文本或结构体形式，详见表 5.5）[in]dwInLength 输入缓冲区的长度[out]pOutBuf 输出缓冲区指针（按照设备规定的能力集的描述方式，XML 文本或结构体形式，详见表 5.5）  

[in]dwOutLength  

### 接收数据的缓冲区的长度  

表 5.4 设备能力集类型  


<html><body><table><tr><td>dwAbilityType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>DEVICE_SOFTHARDWARE_ABILITY</td><td>0x001</td><td>设备软硬件能力</td></tr><tr><td>DEVICE_NETWORK_ABILITY</td><td>0x002</td><td>设备网络能力</td></tr><tr><td>DEVICE_ENCODE_ALL_ABILITY_V20</td><td>0x008</td><td>设备所有编码能力</td></tr><tr><td>IPC_FRONT_PARAMETER_V20</td><td>0x009</td><td>设备前端参数</td></tr><tr><td>DEVICE_ALARM_ABILITY</td><td>0x00a</td><td>设备报警能力</td></tr><tr><td>DEVICE_USER_ABILITY</td><td>0x00c</td><td>设备用户管理参数能力</td></tr><tr><td>DEVICE_NETAPP_ABILITY</td><td>pOOxO</td><td>设备网络应用参数能力</td></tr><tr><td>DEVICE_VIDEOPIC_ABILITY</td><td>0x00e</td><td>设备图像参数能力</td></tr><tr><td>DEVICE_JPEG_CAP_ABILITY</td><td>Ox0of</td><td>设备 JPEG 抓图能力</td></tr><tr><td>DEVICE_SERIAL_ABILITY</td><td>0x010</td><td>设备RS232和RS485 串口能力</td></tr><tr><td>DEVICE_ABILITY_INFO</td><td>0x011</td><td>设备通用能力类型，具体能力根据发送的能力节点来区分</td></tr><tr><td>VCA_DEV_ABILITY</td><td>0x100</td><td>智能设备的能力</td></tr><tr><td>PIC_CAPTURE_ABILITY</td><td>0x402</td><td>抓图图片分辨率能力集</td></tr><tr><td>FISHEYE_ABILITY</td><td>0x700</td><td>鱼眼IPC 能力集</td></tr></table></body></html>

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取设备能力集时，需要输入参数和输出参数的格式定义如表 5.5 所示。  

表 5.5 设备能力集描述  


<html><body><table><tr><td>能力类型宏定义</td><td>能力类型说明</td><td>plnBuf</td><td>pOutBuf</td></tr><tr><td>DEVICE_SOFTHARDWARE_ABILITY</td><td>获取设备软硬件能力</td><td>无</td><td>设备软硬件能力XML描述</td></tr><tr><td>DEVICE_NETWORK_ABILITY</td><td>获取无线设备网络能力</td><td>无</td><td>设备无线网络能力XML描述</td></tr><tr><td>DEVICE_ENCODE_ALL_ABILITY_V20</td><td>获取设备所有编码能力</td><td>编码能力获取输入描述</td><td>设备所有编码能力XML描述</td></tr><tr><td>IPC_FRONT_PARAMETER_V20</td><td>获取设备前端参数</td><td>前端参数能力获取输入描述</td><td>设备前端参数XML描述</td></tr><tr><td>DEVICE_ALARM_ABILITY</td><td>获取设备报警能力</td><td>报警能力获取输入描述</td><td>设备报警能力XML描述</td></tr><tr><td>DEVICE_USER_ABILITY</td><td>获取设备用户管理参数能力</td><td>用户管理参数能力获取输入描述</td><td>设备用户管理参数能力XML描述</td></tr><tr><td>DEVICE_NETAPP_ABILITY</td><td>获取设备网络应用参数能力</td><td>网络应用参数能力获取输入描述</td><td>设备网络应用参数能力XML描述</td></tr><tr><td>DEVICE_VIDEOPIC_ABILITY</td><td>获取设备图像参数能力</td><td>图像参数能力获取输入描述</td><td>设备图像参数能力XML描述</td></tr><tr><td>DEVICE_JPEG_CAP_ABILITY</td><td>获取设备JPEG抓图能力</td><td>JPEG 抓图能力获取输入描述</td><td>设备JPEG抓图能力XML描述</td></tr><tr><td>DEVICE_SERIAL_ABILITY</td><td>获取设备RS232和RS485串口串口能力获取输入描述 能力</td><td></td><td>设备串口能力XML描述</td></tr><tr><td>DEVICE_ABILITY_INFO</td><td>设备通用能力类型，具体能力</td><td>获取PTZ能力集</td><td>PTZ能力XML描述(PTZAbility)</td></tr><tr><td></td><td>根据发送的能力节点来区分</td><td>获取报警事件处理能力集</td><td>报警事件处理能力XML描述 (EventAbility)</td></tr></table></body></html>  

<html><body><table><tr><td></td><td>获取 ROI 能力集</td><td>ROI能力XML 描述(ROIAbility) 录像相关能力XML描述</td></tr><tr><td></td><td>获取录像相关能力集 NVR前端待接入设备通道能力集</td><td>(RecordAbility) NVR前端待接入设备通道能力XML描</td></tr><tr><td></td><td>获取设备本地预览切换能力集</td><td>述(GetAccessDeviceChannelAbility) 设备本地预览切换能力XML描述</td></tr><tr><td></td><td>获取设备N+1能力集</td><td>(PreviewSwitchAbility) 设备N+1能力XML描述</td></tr><tr><td></td><td>获取设备磁盘相关能力集</td><td>(NPlusOneAbility) 设备磁盘相关能力XML描述</td></tr><tr><td></td><td>获取IPC配置文件导入导出能力</td><td>(HardDiskAbility) IPC配置文件导入导出能力XML描述</td></tr><tr><td></td><td>集 获取IO口输入输出能力集</td><td>(IPAccessConfigFileAbility) 设备IO口输入输出能力XML描述</td></tr><tr><td></td><td>获取协议接入能力集</td><td>(IOAbility)</td></tr><tr><td></td><td></td><td>设备协议接入能力XML描述 (AccessProtocolAbility)</td></tr><tr><td></td><td>获取安全认证配置能力集</td><td>安全认证配置能力XML描述 (SecurityAbility)</td></tr><tr><td></td><td>获取摄像机架设参数能力集</td><td>摄像机架设参数能力XML描述 (CameraMountAbility)</td></tr><tr><td></td><td>获取智能通道控制能力集</td><td>智能通道控制能力XML描述</td></tr><tr><td></td><td>获取智能通道分析能力集</td><td>(VcaCtrlAbility) 智能通道分析能力XML描述</td></tr><tr><td>VCA_DEV_ABILITY 获取智能设备的能力</td><td>无</td><td>(VcaChanAbility) NET_VCA_DEV_ABILITY</td></tr><tr><td>PIC_CAPTURE_ABILITY</td><td>获取图片能力 通道号 (4个字节)</td><td></td></tr><tr><td>FISHEYE_ABILITY 获取鱼眼IPC能力</td><td>鱼眼 IPC 能力获取输入描述</td><td>NET_DVR_COMPRESSIONCFG_ABILITY 鱼眼IPC能力XML描述</td></tr></table></body></html>

注：能力集 XML 描述详细内容请参见《设备网络 SDK 使用手册.chm》。  

### 5.4.2 获取设备能力集 NET_DVR_GetSTDAbility  

函  数： BOOL NET_DVR_GetSTDAbility(LONG lUserID, DWORD dwAbilityType, LPNET_DVR_STD_ABILITYlpAbilityParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwAbilityType 能力类型，具体定义见表 5.6[in&out]lpAbilityParam 设备能力集参数（包括输入和输出参数），不同的能力集对应不同的输入输出参数  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通  

说  明：  

过错误码判断出错原因。  

表 5.6 获取设备能力集  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td><td>IpCondBuffer</td><td>IpOutBuffer</td></tr><tr><td>Smart 智能相关能力集</td><td></td><td></td><td></td><td></td></tr><tr><td>NET_DVR_GET_SMART_CAPABILITIES</td><td>3500</td><td>获取 Smart 能力集</td><td>NULL</td><td>SmartCap</td></tr><tr><td>NET_DVR_GET_EVENT_TRIGGERS_CAPABILITIES</td><td>3501</td><td>获取事件触发能力集</td><td>NULL</td><td>EventTriggerCap</td></tr><tr><td>NET_DVR_GET_REGION_ENTRANCE_CAPABILITIES</td><td>3502</td><td>获取进入区域侦测能 力集</td><td>4个字节（DWORD）通道号</td><td>RegionEntrance</td></tr><tr><td>NET_DVR_GET_REGION_ENTRANCE_SCHEDULE_CAPABILITIES</td><td>3584</td><td>防时间能力集</td><td>获取进入区域侦测布4个字节（DWORD）通道号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_REGION_EXITINT_CAPABILITIES</td><td>3511</td><td>力集</td><td>获取离开区域侦测能4个字节（DWORD）通道号</td><td>RegionExiting</td></tr><tr><td>NET_DVR_GET_REGION_EXITING_SCHEDULE_CAPABILITIES</td><td>3585</td><td>获取离开区域侦测布 防时间能力集</td><td>市4个字节（DWORD）通道号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_LOITERING_CAPABILITIES NET_DVR_GET_LOITERING_SCHEDULE_CAPABILITIES</td><td>3520</td><td>获取徘徊侦测能力集</td><td>4个字节（DWORD）通道号</td><td>Loitering</td></tr><tr><td></td><td>3586</td><td>获取徘徊侦测布防时 间能力集</td><td>4个字节（DWORD）通道号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_GROUPDETECTION_CAPABILITIES</td><td>3529</td><td>力集</td><td>获取人员聚集侦测能4个字节（DWORD）通道号</td><td>Group</td></tr><tr><td>NET_DVR_GET_GROUP_SCHEDULE_CAPABILITIES</td><td>3587</td><td>防时间能力集</td><td>获取人员聚集侦测布4个字节（DWORD）通道号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_CAPABILITIES</td><td>3538</td><td>获取快速运动侦测能 力集</td><td>能4个字节（DWORD）通道号</td><td>RapidMove</td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_SCHEDULE_CAPABILITIES</td><td>3588</td><td>获取快速运动侦测布 防时间能力集</td><td>4个字节（DWORD）通道号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_PATKING_CAPABILITIES</td><td>3547</td><td>获取停车侦测能力集</td><td>4个字节（DWORD）网卡号</td><td>Parking</td></tr><tr><td>NET_DVR_GET_PARKING_SCHEDULE_CAPABILITIES</td><td>3589</td><td>获取停车侦测布防时 间能力集</td><td>4个字节（DWORD）通道号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_CAPABILITIES</td><td>3556</td><td>获取物品遗留侦测能 力集</td><td>4个字节（DWORD）通道号</td><td>UnattendedBaggage</td></tr><tr><td>NET_DVR_GET_UNATTENDEDBAGGAGE_SCHEDULE_CAPABILITIES</td><td>3590</td><td>防时间能力集</td><td>获取物品遗留侦测布4个字节（DWORD）通道号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_CAPABILITIES</td><td>3565</td><td>获取物品拿取侦测能 力集</td><td>4个字节（DWORD）通道号</td><td>AttendedBaggageCap</td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_SCHEDULE_CAPABILITIES</td><td>3591</td><td>防时间能力集</td><td>获取物品拿取侦测布4个字节（DWORD）通道号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_REGIONCLIP_CAPABILITIES</td><td>3574</td><td>获取区域裁剪能力集</td><td>NET_DVR_REGION_CLIP_COND</td><td>RegionClip</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_GET_LITESTORAGE_CAPABILITIES</td><td>3596</td><td>获取轻存储能力集</td><td>4个字节（DWORD）通道号</td><td>LiteStorage</td></tr><tr><td>NET_DVR_GET_VEHICLE_CAPABILITIES</td><td>3597</td><td>获取车俩检测标定能 力集</td><td>4个字节（DWORD）通道号</td><td>Calibration</td></tr><tr><td>NET_DVR_GET_TRAFFIC_CAP</td><td>6630</td><td>获取抓拍相关能力集</td><td>NULL</td><td>TrafficCap</td></tr><tr><td>NET_DVR_GET_VEHICLLE_RESULT_CAPABILITIES</td><td>3951</td><td>获取车辆信息查询结 果能力集</td><td>NULL</td><td>VehiclelnfoResultCap</td></tr><tr><td>NET_DVR_GET_COUNTING_CAPABILITIES</td><td>3757</td><td>获取客流量统计能力4个字节（DWORD）通道号 集</td><td></td><td>CountingCap</td></tr><tr><td>网络相关能力集</td><td></td><td></td><td></td><td></td></tr><tr><td>NET_DVR_GET_NETWORK_CAPABILITIES</td><td>3577</td><td>获取网络能力集</td><td>NULL</td><td>NetworkCap</td></tr><tr><td>NET_DVR_GET_WIRELESSDIAL_CAPABILITIES</td><td>3580</td><td>获取无线拨号参数能 力集</td><td>4个字节（DWORD）网卡号</td><td>Dial</td></tr><tr><td>NET_DVR_GET_WIRELESSDIAL_SCHEDULE_CAPABILITIES</td><td>3592</td><td>获取拨号计划能力集</td><td>4个字节（DWORD）网卡号</td><td>Schedule</td></tr><tr><td>NET_DVR_GET_FTP_CAPABILITIES</td><td>3782</td><td>获取 FTP 上传能力集</td><td>NULL</td><td>FTPNotificationList</td></tr><tr><td>NET_DVR_GET_WIRELESSSERVER_CAPABILITIES</td><td>3716</td><td>获取Wifi热点配置能 力集</td><td>4个字节（DWORD）无线网卡 号</td><td>WirelessServer</td></tr><tr><td>NET_DVR_GET_CONNECT_LIST_CAPABILITIES</td><td>3719</td><td>获取热点连接设备列 表信息能力集</td><td>4个字节（DWORD）无线网卡 号</td><td>accessDeviceList</td></tr><tr><td>NET_DVR_GET_DDNS_COUNTRY_ABILITY</td><td>3800</td><td>获取设备支持的DDNS 国家能力列表</td><td>NULL</td><td>DDNSCountry</td></tr><tr><td>NET_DVR_GET_MACFILTER_CAPABILITIES</td><td>3643</td><td>获取 MAC 地址过滤配 置能力集</td><td>NULL</td><td>MACFilter</td></tr><tr><td>存储相关能力集 NET_DVR_GET_STORAGEDETECTION_SCHEDULE_CAPABILITIES</td><td>6637</td><td>获取存储健康检测布4个字节（DWORD）硬盘号</td><td></td><td>Schedule</td></tr><tr><td>NET_DVR_GET_STORAGEDETECTION_RWLOCK_CAPABILITIES</td><td></td><td>防时间能力集</td><td></td><td></td></tr><tr><td>NET_DVR_GET_STORAGEDETECTION_UNLOCK_CAPABILITIES</td><td>6647</td><td>获取存储侦测读写锁 配置能力集</td><td>NULL</td><td>RWLock</td></tr><tr><td></td><td>6654</td><td>获取存储侦测解锁配 置能力集</td><td>NULL</td><td>UnLock</td></tr><tr><td>外设相关能力集 NET_DVR_GET_THSCREEN_CAPABILITIES</td><td>3720</td><td>获取温湿度配置能力4个字节（DWORD）通道号</td><td></td><td>THScreen</td></tr><tr><td></td><td></td><td>集</td><td></td><td></td></tr><tr><td>NET_DVR_GET_EXTERNALDEVICE_CAPABILITIES NET_DVR_GET_SUPPLEMENTLIGHT_CAPABILITIES</td><td>3722 3727</td><td>获取外设配置能力集 获取内置补光灯配置</td><td>4个字节（DWORD）通道号 4个字节（DWORD）通道号</td><td>ExternalDevice SupplementLight</td></tr><tr><td></td><td></td><td>能力集</td><td></td><td></td></tr><tr><td>其他设备能力集</td><td></td><td></td><td></td><td></td></tr><tr><td>NET_DVR_GET_STREAMING_CAPABILITIES</td><td>3712</td><td>获取视频流能力集</td><td>4个字节（DWORD）通道号</td><td>StreamingChannel</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_GET_REFRESHFRAME_CAPABILITIES</td><td>3713</td><td>获取刷新帧能力集</td><td>4个字节（DWORD）通道号</td><td>RefreshFrame</td></tr><tr><td>NET_DVR_GET_OSD_BATTERY_POWER_CFG_CAPABILITIES</td><td>3743</td><td>获取OSD电池电量显 示参数能力集</td><td>4个字节（DWORD）通道号</td><td>BatteryPowerOverlay</td></tr><tr><td>NET_DVR_GET_OIS_CAPABILITIES</td><td>3640</td><td>置能力集</td><td>获取光学防抖参数配4个字节（DWORD）通道号</td><td>OIS</td></tr><tr><td>NET_DVR_GET_REVISE_GPS_CAPABILITIES</td><td>3752</td><td>能力集</td><td>获取校准GPS经纬度4个字节（DWORD）通道号</td><td>ReviseGPS</td></tr><tr><td>NET_DVR_GET_PTZ_CAPABILITIES</td><td>3619</td><td>球机PTZ控制能力集</td><td>4个字节(DWORD)通道号</td><td>PTZChanelCap</td></tr><tr><td>NET_DVR_GET_EAGLEFOCUS_CALCFG_CAPABILITIES</td><td>3646</td><td>鹰视聚焦标定配置能 力集</td><td>4个字节(DWORD)通道号</td><td>EagleFocusing</td></tr><tr><td>NET_DVR_GET_EAGLEFOCUSING_CFG_CAPABILITIES</td><td>3649</td><td>鹰视聚焦配置能力集</td><td>4个字节(DWORD)通道号</td><td>Control</td></tr><tr><td>NET_DVR_GET_SOFTWARE_SERVICE_CAPABILITIES</td><td>3980</td><td>获取软件服务能力集</td><td>4 个字节(DWORD)通道号</td><td>SoftwareService</td></tr><tr><td>NET_DVR_GET_SYSTEM_CAPABILITIES</td><td>8100</td><td>设备系统能力集</td><td>NULL</td><td>DeviceCap</td></tr></table></body></html>  

## 5.5实时预览  

### 5.5.1 实时预览 NET_DVR_RealPlay_V40  

函  数： LONG NET_DVR_RealPlay_V40(LONG lUserID, LPNET_DVR_PREVIEWINFO lpPreviewInfo,REALDATACALLBACK fRealDataCallBack_V30, void \*pUser)  

参  数： [in] lUserID NET_DVR_Login_V40 的返回值[in] lpPreviewInfo 预览参数，包括码流类型、取流协议、通道号、预览窗口句柄等，详见结构体：NET_DVR_PREVIEWINFO[in] fRealDataCallBack_V30 码流数据回调函数[in] pUser 用户数据  

typedef void(CALLBACK \*REALDATACALLBACK)(LONG lRealHandle, DWORD dwDataType, BYTE \*pBuffer, DWORD dwBufSize, void \*pUser)  

[out] lRealHandle 当前的预览句柄[out] dwDataType 数据类型，详见表 5.7[out] pBuffer 存放数据的缓冲区指针[out] dwBufSize 缓冲区大小[out] pUser 用户数据  

表 5.7 码流数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>1</td><td>系统头数据</td></tr><tr><td>NETDVRSTREAMDATA</td><td>2</td><td>流数据 居（包括复合流或音视频分开的视频流数据）</td></tr><tr><td>NETDVRAUDIOSTREAMDATA</td><td>3</td><td>音频数据</td></tr></table></body></html>

返回值： -1 表示失败，其他值作为 NET_DVR_StopRealPlay 等函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

明：  该接口预览参数结构中可以设置当前预览操作是否阻塞（通过 bBlocked 参数设置），若设为不阻塞，表示发起与设备的连接就认为连接成功，如果发生码流接收失败、播放失败等情况以预览异常的方式通知上层。在循环播放的时候可以减短停顿的时间，与 NET_DVR_RealPlay处理一致。若设为阻塞，表示直到播放操作完成才返回成功与否。 该接口中的回调函数可以置为空，这样该函数将不回调码流数据给用户，不过用户仍可以通过接口 NET_DVR_SetRealDataCallBack 或 NET_DVR_SetStandardDataCallBack 注册捕获码流数据的回调函数以捕获码流数据。 fRealDataCallBack_V30 回调函数中不能执行可能会占用时间较长的接口或操作，不建议调用该SDK（HCNetSDK.dll）本身的接口。 客户端异常离线时，设备端对取流连接的保持时间为 10 秒。  

### 5.5.2 停止预览 NET_DVR_StopRealPlay  

函  数： LONG NET_DVR_StopRealPlay (LONG lRealHandle)  
参  数： [in]lRealHandle 预览句柄，NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.5.3 获取预览时用来解码和显示的播放库句柄 NET_DVR_GetRealPlayerIndex  

函  数： int NET_DVR_GetRealPlayerIndex(LONG lRealHandle)  
参  数： [in]lRealHandle 预览句柄，NET_DVR_RealPlay_V40 的返回值  
返回值： -1 表示失败，其他值表示播放句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 用户可以通过返回的句柄自行实现播放库 SDK 提供的其他功能，详见本公司提供的软解码库函数说明《播放器 SDK 编程指南》。例如使用 PlayM4_GetBMP(LONG nPort,……)、PlayM4_GetJPEG(LONG nPort,……)这两个接口时，即可实现将当前预览图像以 BMP 或 JPEG 格式抓图保存到内存中： PlayM4_GetBMP(NET_DVR_GetRealPlayerIndex(),……)PlayM4_GetJPEG(NET_DVR_GetRealPlayerIndex(),……)  

## 5.6强制！帧和刷新帧  

### 5.6.1 强制 I 帧 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  

[in]dwCommand 控制命令，详见表 5.8  
[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.58  
[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.58 所示NET_DVR_I_FRAME 结构体里面指定强制的通道号、码流类型（主子码流或者其他）。  

表 5.8 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NETDVRMAKEIFRAME</td><td>3402</td><td>强制1帧</td><td>NETDVRIFRAME</td></tr></table></body></html>  

### 5.6.2 强制刷新帧(Smart264) NET_DVR_STDControl  

函  数： BOOL NET_DVR_STDControl(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONTROLlpControlParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.9[in&out]lpControlParam 远程控制输入输出参数，不同的控制功能对应不同的输入输出参数，详见表 5.9  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对于不同的配置功能（dwCommand），lpControlParam中的lpCondBuffer 对应不同的内容，如表 5.9所示。  

 该功能针对启用 Smart264 编码后的码流预览，通过该命令强制设备生成一个深 P 帧。 设备是否支持 Smart264 编码功能，通过能力集(StreamingChannel)中节点<isSupportRefreshFrame>进行判断，相关接口：NET_DVR_GetSTDAbility(能力集类型：NET_DVR_GET_STREAMING_CAPABILITIES)。 设备支持刷新帧的码流类型，通过能力集(RefreshFrame)获取，相关接口：NET_DVR_GetSTDAbility (能力集类型：NET_DVR_GET_REFRESHFRAME_CAPABILITIES)。  

表 5.9 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>含义</td><td>IpCondBuffer对应结构体</td></tr><tr><td>NETDVRSTREAMINGREFRESHFRAME</td><td>3714</td><td>强制刷新帧</td><td>NETDVRSTREAMINGCOND</td></tr></table></body></html>  

## 5.7预览显示视频参数配置  

### 5.7.1 获取预览视频显示参数 NET_DVR_ClientGetVideoEffect  

函  数： BOOL NET_DVR_ClientGetVideoEffect(LONG lRealHandle,DWORD \*pBrightValue, DWORD\*pContrastValue,DWORD \*pSaturationValue,DWORD \*pHueValue)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[out]pBrightValue 亮度指针，取值范围[1,10][out]pContrastValue 对比度指针，取值范围[1,10][out]pSaturationValue 饱和度指针，取值范围[1,10][out]pHueValue 色度指针，取值范围[1,10]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 需要预览才能获取视频参数。  

### 5.7.2 获取预览视频显示参数 NET_DVR_GetVideoEffect  

函  数： BOOL NET_DVR_GetVideoEffect(LONG lUserID, LONG lChannel,DWORD \*pBrightValue, DWORD\*pContrastValue,DWORD \*pSaturationValue,DWORD \*pHueValue)  

参  数： [in]lRealHandle NET_DVR_Login_V40 的返回值[in]lChannel 通道号[out] pBrightValue 亮度指针，取值范围[1,10][out] pContrastValue 对比度指针，取值范围[1,10][out] pSaturationValue 饱和度指针，取值范围[1,10][out] pHueValue 色度指针，取值范围[1,10]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 登录设备获取通道的视频参数。  

### 5.7.3 设置预览视频显示参数 NET_DVR_ClientSetVideoEffect  

函  数： BOOL NET_DVR_ClientSetVideoEffect(LONG lRealHandle,DWORD pBrightValue, DWORDpContrastValue,DWORD pSaturationValue,DWORD pHueValue)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwBrightValue 亮度，取值范围[1,10][in]dwContrastValue 对比度，取值范围[1,10][in]dwSaturationValue 饱和度，取值范围[1,10][in]dwHueValue 色度，取值范围[1,10]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 需要预览才能设置视频参数。  

### 5.7.4 设置预览视频显示参数 NET_DVR_SetVideoEffect  

函  数： BOOL NET_DVR_SetVideoEffect(LONG lUserID, LONG lChannel,DWORD \*pBrightValue, DWORD\*pContrastValue,DWORD \*pSaturationValue,DWORD \*pHueValue)参  数： [in]lRealHandle NET_DVR_Login_V40 的返回值  

[in]lChannel 通道号 [in]dwBrightValue 亮度，取值范围[1,10] [in]dwContrastValue 对比度，取值范围[1,10] [in]dwSaturationValue 饱和度，取值范围[1,10] [in]dwHueValue 色度，取值范围[1,10]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 登录设备设置通道的视频参数。  

## 5.8预览画面叠加字符和图像  

### 5.8.1 预览画面叠加字符和图像，Linux 下无此接口 NET_DVR_RigisterDrawFun  

函  数： BOOL NET_DVR_RigisterDrawFun(LONG lRealHandle, fDrawFun cbDrawFun, DWORD dwUser)返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

<html><body><table><tr><td rowspan="5">参 数：</td><td>[in]IRealHandle</td><td>NET DVR RealPlay_V40 的返回值</td></tr><tr><td>[in]cbDrawFun</td><td>画图回调函数</td></tr><tr><td>[in]dwUser</td><td>用户数据</td></tr><tr><td>typedef void(CALLBACK</td><td>*fDrawFun)(LONG IRealHandle,HDC hDc, DWORD dwUser)</td></tr><tr><td></td><td>[out]IRealHandle 当前的预览句柄</td></tr><tr><td rowspan="2"></td><td>[out]hDc</td><td>画图DC</td></tr><tr><td>[out]dwUser</td><td>用户数据</td></tr></table></body></html>  

说  明： 该接口主要完成注册回调函数，获得当前表面的 device context。用户可以在这个 DC 上画图或写字，就好像在窗口的客户区 DC 上绘图，但这个 DC 不是窗口客户区的 DC，而是播放器 DirectDraw里的 Off-Screen 表面的 DC。 如果调用接口 NET_DVR_RealPlay_V40 进行预览，参数 bBlocked 必须置 1（TRUE），否则该接口调用会失败，获取错误号为 12（调用次序错误）。  

## 5.9预览时播放声音控制  

### 5.9.1 设置声音播放模式 NET_DVR_SetAudioMode  

函  数： BOOL NET_DVR_SetAudioMode(DWORD dwMode)  
参  数： [in]dwMode 声音播放模式：1- 独占声卡，单路音频模式；2- 共享声卡，多路音频模式  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 不调用该接口设置声音播放模式，默认为独占播放。  

### 5.9.2 独占声卡模式下开启声音 NET_DVR_OpenSound  

函  数： BOOL NET_DVR_OpenSound(LONG lRealHandle)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 如果当前是共享模式播放，调用该接口将返回失败。以独占方式只能打开一路通道播放，即依次打开多个通道时仅打开最后一路。  

返回目录  

### 5.9.3 独占声卡模式下开启声音 NET_DVR_CloseSound  

函  数： BOOL NET_DVR_CloseSound()  
参  数： 无  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.9.4 共享声卡模式下开启声音 NET_DVR_OpenSoundShare  

函  数： BOOL NET_DVR_OpenSoundShare(LONG lRealHandle)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.9.5 共享声卡模式下关闭声音 NET_DVR_CloseSoundShare  

函  数： BOOL NET_DVR_CloseSoundShare (LONG lRealHandle)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.9.6 调节播放音量 NET_DVR_Volume  

函  数： BOOL NET_DVR_Volume(LONG lRealHandle,WORD wVolume)参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]wVolume 音量，取值范围[0,0xffff]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.10实时数据回调和录像  

### 5.10.1 注册回调函数，捕获实时码流数据 NET_DVR_SetRealDataCallBack  

函  数： BOOL NET_DVR_SetRealDataCallBack(LONG lRealHandle, fRealDataCallBack cbRealDataCallBack,DWORD dwUser)  

参  数： [in]lRealHandle 预览句柄，NET_DVR_RealPlay_V40 的返回值[in]cbRealDataCallBack 码流数据回调函数[in]dwUser 用户数据  

typedef void(CALLBACK \*fRealDataCallBack)(LONG lRealHandle, DWORD dwDataType, BYTE \*pBuffer, DWORD dwBufSize, DWORD dwUser)  

[out]lRealHandle 当前的预览句柄[out]dwDataType 数据类型，详见表 5.10[out]pBuffer 存放数据的缓冲区指针[out]dwBufSize 缓冲区大小[out]dwUser 用户数据  

表 5.10 码流数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>1</td><td>系统头数据</td></tr><tr><td>NET DVRSTREAMDATA</td><td>2</td><td>流数据 居（包括复合流或音视频分开的视频流数据）</td></tr><tr><td>NETDVRAUDIOSTREAMDATA</td><td>3</td><td>音频数据</td></tr></table></body></html>  

返回值：  

TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

 此函数包括开始和停止用户处理 SDK 捕获的数据，当回调函数 cbRealDataCallBack 设为非 NULL值时，表示回调和处理数据；当设为 NULL 时表示停止回调和处理数据。回调的第一个包是40 个字节的文件头，供后续解码使用，之后回调的是压缩的码流。回调数据最大为 256K 字节。  
 cbRealDataCallBack回调函数中不能执行可能会占用时间较长的接口或操作，不建议调用该SDK（HCNetSDK.dll）本身的接口。  

### 5.10.2 注册回调函数，捕获实时码流数据（标准码流）  

NET_DVR_SetStandardDataCallBack  

函  数： BOOL NET_DVR_SetStandardDataCallBack(LONG lRealHandle, fStdDataCallBackcbStdDataCallBack,DWORD dwUser)  

### 参  数：  

[in]lRealHandle 预览句柄，NET_DVR_RealPlay_V40 的返回值  
[in]cbStdDataCallBack 标准码流回调函数  
[in]dwUser 用户数据  

typedef void(CALLBACK \*fStdDataCallBack)(LONG lRealHandle, DWORD dwDataType, BYTE \*pBuffer, DWORD dwBufSize, DWORD dwUser)  

[out]lRealHandle 当前的预览句柄[out]dwDataType 数据类型，详见表 5.11[out]pBuffer 存放数据的缓冲区指针[out]dwBufSize 缓冲区大小[out]dwUser 用户数据  

表 5.11 标准码流数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>1</td><td>系统头数据</td></tr><tr><td>NET_DVR_STD_VIDEODATA</td><td>4</td><td>标准视频流数据</td></tr><tr><td>NETDVRSTDAUDIODATA</td><td>5</td><td>标准音频流数据</td></tr><tr><td>NETDVRPRIVATEDATA</td><td>2或者112</td><td>私有数据，包括智能信息叠加等</td></tr></table></body></html>  

返回值：  

TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

 此函数包括开始和停止用户处理 SDK 捕获的数据，当回调函数 cbStdDataCallBack 设为非 NULL值时，表示回调和处理数据；当设为 NULL 时表示停止回调和处理数据。回调的第一个包是40 个字节的文件头，供后续解码使用，之后回调的是标准码流（含 12 字节的 RTP 头）。  
 cbStdDataCallBack 回调函数中不能执行可能会占用时间较长的接口或操作，不建议调用该 SDK（HCNetSDK.dll）本身的接口。  
 此函数仅支持对于支持 RTSP 协议取流的设备的标准码流回调。  

### 5.10.3 捕获数据并保存到指定的文件中 NET_DVR_SaveRealData  

函  数： BOOL NET_DVR_SaveRealData(LONG  lRealHandle,char \*sFileName)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]sFileName 文件路径指针，绝对路径，包括文件名  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： V5.0.3.2 或以后版本，通过该接口保存录像，文件最大限制为 1024MB，大于 1024M 时，SDK 自动新建文件进行保存，文件开始将40 字节头自动写入，文件名命名规则为“在接口传入的文件名基础上增加数字标识(例如：\*_1.mp4、\*_2.mp4)”。  

### 5.10.4 停止数据捕获 NET_DVR_StopSaveRealData  

函  数： BOOL NET_DVR_StopSaveRealData(LONG  lRealHandle )  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通  

过错误码判断出错原因。  

说  明：  

## 5.11 预览抓图  

### 5.11.1 设置抓图模式 NET_DVR_SetCapturePictureMode  

函  数： BOOL NET_DVR_SetCapturePictureMode(DWORD dwCaptureMode)参  数： [in]dwCaptureMode 抓图模式  

enum tagPDC_PARAM_KEY{BMP_MODE $=0,$ , // BMP 模式JPEG_MODE $=1$ // JPEG 模式}CAPTURE_MODE  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。说  明： 调用该接口设置抓图模式后，NET_DVR_CapturePicture 可抓取相应的图片。  

返回目录  

### 5.11.2 预览时，单帧数据捕获并保存成图片 NET_DVR_CapturePicture  

函  数： BOOL NET_DVR_CapturePicture(LONG lRealHandle,char \*sPicFileName)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]sPicFileName 保存图象的文件路径。路径长度和操作系统有关，sdk 不做限制，windows 默认路径长度小于等于 256 字节（包括文件名在内）。  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  在调用该接口之前可以调用 NET_DVR_SetCapturePictureMode 设置抓图模式，默认为 BMP 模式。如果抓图模式为 BMP 模式，抓取的是 BMP 图片，保存路径后缀应为.bmp；如果抓图模式为 JPEG 模式，抓取的是 JPEG 图片，保存路径后缀应为.jpg。 若设备的当前分辨率为 2CIF，播放库做了相关处理，抓取的图像为 4CIF。 调用 NET_DVR_CapturePicture 进行抓图，要求在调用 NET_DVR_RealPlay_V40 等接口时传入非空的播放句柄（播放库解码显示），否则时接口会返回失败，调用次序错误。  

## 5.12 设备抓图  

### 5.12.1 单帧数据捕获并保存成 JPEG 图片 NET_DVR_CaptureJPEGPicture  

函  数： BOOL NET_DVR_CaptureJPEGPicture(LONG lUserID, LONG lChannel, LPNET_DVR_JPEGPARAlpJpegPara, char \*sPicFileName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]lpJpegPara JPEG 图像参数，包括抓图分辨率、抓图质量  

[in]sPicFileName  

保存 JPEG 图的文件路径，路径长度和操作系统有关，sdk 不做限制，windows 默认路径长度小于等于 256 字节（包括文件名在内）。  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口用于设备的单帧数据捕获，并保存成 JPEG 图片。抓图分辨率需要设备支持，IPC 设备支持当前视频分辨率的抓取。  

### 5.12.2 单帧数据捕获并保存成 JPEG 存放在指定的内存空间中  

NET_DVR_CaptureJPEGPicture_NEW  

函  数： BOOL NET_DVR_CaptureJPEGPicture_NEW(LONG lUserID, LONG lChannel, LPNET_DVR_JPEGPARA lpJpegPara, char \*sJpegPicBuffer, DWORD dwPicSize, LPDWORD lpSizeReturned)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]lpJpegPara JPEG 图像参数，包括抓图分辨率、抓图质量[in]sJpegPicBuffer 保存 JPEG 数据的缓冲区[in]dwPicSize 输入缓冲区大小[out]lpSizeReturned 返回图片数据的大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口用于设备的单帧数据捕获，并保存成 JPEG 图片。抓图分辨率需要设备支持，IPC 设备支持当前视频分辨率的抓取。  

## 5.13参数配置  

### 系统参数配置  

### 5.13.1 获取设备参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.12 所示。  

表 5.12 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_DEVICECFG_V40</td><td>获取设备参数(扩展)</td><td>无效</td><td>NET_DVR_DEVICECFG_V40</td><td>1100</td></tr><tr><td>NET_DVR_GET_DECODERCFG_V30</td><td>获取RS485云台解码器参数</td><td>通道号</td><td>NET_DVR_DECODERCFG_V30</td><td>1042</td></tr><tr><td>NET_DVR_GET_RS232CFG_V30</td><td>获取RS232串口参数</td><td>无效</td><td>NET_DVR_RS232CFG_V30</td><td>1036</td></tr><tr><td>NETDVRGETEXCEPTIONCFGV40</td><td>获取异常参数</td><td>组号，从0开始， 每组32个用户</td><td>NETDVREXCEPTIONV40</td><td>6177</td></tr><tr><td>NET_DVR_GET_TIMECFG</td><td>获取时间参数</td><td>无效</td><td>NET_DVR_TIME</td><td>118</td></tr><tr><td>NET_DVR_GET_ZONEANDDST</td><td>获取时区和夏时制参数</td><td>无效</td><td>NET_DVR_ZONEANDDST</td><td>128</td></tr><tr><td>NET_DVR_GET_DEVSERVER_CFG</td><td>获取模块服务配置</td><td>无效</td><td>NET_DVR_DEVSERVER_CFG</td><td>3257</td></tr></table></body></html>  

### 返回目录  

### 5.13.2 设置设备参数 NET_DVR_SetDVRConfig  

函  数： BOOL  NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.13 所示。  

表 5.13 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_DEVICECFG_V40</td><td>设置设备参数(扩展)</td><td>无效</td><td>NET_DVR_DEVICECFG_V40</td><td>1101</td></tr><tr><td>NET_DVR_SET_DECODERCFG_V30</td><td>设置RS485云台解码器参数</td><td>通道号</td><td>NET_DVR_DECODERCFG_V30</td><td>1043</td></tr><tr><td>NET_DVR_SET_RS232CFG_V30</td><td>设置RS232串口参数</td><td>无效</td><td>NET_DVR_RS232CFG_V30</td><td>1037</td></tr><tr><td>NET_DVR_SET_EXCEPTIONCFG_V40</td><td>设置异常参数</td><td>组号，从0开始， 每组32个用户</td><td>NET_DVR_EXCEPTION_V40</td><td>6178</td></tr><tr><td>NET_DVR_SET_TIMECFG</td><td>设置时间参数</td><td>无效</td><td>NET_DVR_TIME</td><td>119</td></tr><tr><td>NET_DVR_SET_ZONEANDDST</td><td>设置时区和夏时制参数</td><td>无效</td><td>NET_DVR_ZONEANDDST</td><td>129</td></tr><tr><td>NET_DVR_SET_TIMECORRECT</td><td>校时配置(针对网络摄像机)</td><td>无效</td><td>NET_DVR_TIME</td><td>432</td></tr><tr><td>NET_DVR_SET_DEVSERVER_CFG</td><td>设置模块服务配置</td><td>无效</td><td>NET_DVR_DEVSERVER_CFG</td><td>3258</td></tr></table></body></html>  

### 返回目录  

### 5.13.3 获取设备参数 NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.14[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.14  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.14所示。  

表 5.14 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>lpCondBuffer</td><td>IpOutBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_FIRMWARE_VERSION</td><td>获取主控版本信息</td><td>NULL</td><td>NET_DVR_FIRMWARE_VERSION_IFNO</td><td>3776</td></tr></table></body></html>  

### 通道参数配置  

### 5.13.4 获取通道参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.15 所示。  

$\bullet$ 通道号是指设备视频通道号，通过注册设备（NET_DVR_Login_V30）返回的设备信息（NET_DVR_DEVICEINFO_V30）获取模拟通道个数（byChanNum）、模拟通道起始通道号（byStartChan）和设备支持的最大 IP 通道数（byIPChanNum $^+$ byHighDChanNum $^{*}256$ ）、数字通道起始通道号（byStartDChan）。  
$\bullet$ 对于网络摄像机、网络球机，设备只有一个通道，通道号即为 1。  

表 5.15 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_PICCFG_V40</td><td>获取图像参数</td><td>通道号</td><td>NET_DVR_PICCFG_V40</td><td>6179</td></tr><tr><td>NET_DVR_GET_COMPRESSCFG_V30</td><td>获取压缩参数</td><td>通道号</td><td>NET_DVR_COMPRESSIONCFG_V30</td><td>1040</td></tr><tr><td>NET_DVR_GET_RECORDCFG_V40</td><td>获取录像参数</td><td>通道号</td><td>NET_DVR_RECORD_V40</td><td>1008</td></tr><tr><td>NET_DVR_GET_SHOWSTRING_V30</td><td>获取叠加字符参数</td><td>通道号</td><td>NET_DVR_SHOWSTRING_V30</td><td>1030</td></tr><tr><td>NET_DVR_GET_CCDPARAMCFG</td><td>获取前端参数</td><td>无效</td><td>NET_DVR_CAMERAPARAMCFG</td><td>1067</td></tr><tr><td>NET_DVR_GET_CCDPARAMCFG_EX</td><td>获取前端参数(扩展)</td><td>通道号</td><td>NET_DVR_CAMERAPARAMCFG_EX</td><td>3368</td></tr><tr><td>NET_DVR_GET_AUDIO_INPUT</td><td>获取音频输入参数</td><td>通道号</td><td>NET_DVR_AUDIO_INPUT_PARAM</td><td>3201</td></tr><tr><td>NET_DVR_GET_CAMERA_DEHAZE_CFG</td><td>获取去雾参数</td><td>通道号</td><td>NET_DVR_CAMERA_DEHAZE_CFG</td><td>3203</td></tr><tr><td>NET_DVR_GET_AUDIOOUT_VOLUME</td><td>获取输出音频大小</td><td>通道号</td><td>NET_DVR_AUDIOOUT_VOLUME</td><td>3237</td></tr><tr><td>NET_DVR_GET_ISP_CAMERAPARAMCFG</td><td>获取ISP 前端参数配置</td><td>通道号</td><td>NET_DVR_ISP_CAMERAPARAMCFG</td><td>3255</td></tr><tr><td>NET_DVR_GET_LOW_LIGHTCFG</td><td>获取快球低照度信息</td><td>通道号</td><td>NET_DVR_LOW_LIGHT_CFG</td><td>3303</td></tr><tr><td>NET_DVR_GET_FOCUSMODECFG</td><td>获取快球聚焦模式信息</td><td>通道号</td><td>NET_DVR_FOCUSMODE_CFG</td><td>3305</td></tr><tr><td>NET_DVR_GET_INFRARECFG</td><td>获取快球红外信息</td><td>通道号</td><td>NET_DVR_INFRARE_CFG</td><td>3307</td></tr><tr><td>NET_DVR_GET_AEMODECFG</td><td>获取快球其他参数信息</td><td>通道号</td><td>NET_DVR_AEMODECFG</td><td>3309</td></tr><tr><td>NET_DVR_GET_CORRIDOR_MODE</td><td>获取旋转功能配置</td><td>通道号</td><td>NET_DVR_CORRIDOR_MODE</td><td>3354</td></tr><tr><td>NET_IPC_GET_AUX_ALARMCFG</td><td>获取辅助报警参数</td><td>通道号</td><td>NET_IPC_AUX_ALARMCFG</td><td>3209</td></tr><tr><td>NET_DVR_GET_SIGNAL_SYNC</td><td>获取信号灯同步配置参数</td><td>通道号</td><td>NET_DVR_SIGNAL_SYNCCFG</td><td>3396</td></tr><tr><td>NET_DVR_GET_SNAPINFO_CFG</td><td>获取抓拍图片参数</td><td>通道号</td><td>NET_DVR_SNAPINFOCFG</td><td>3136</td></tr><tr><td>NET_DVR_GET_JPEG_CAPTURE_CFG</td><td>获取设备抓图配置</td><td>通道号</td><td>NET_DVR_JPEG_CAPTURE_CFG</td><td>1280</td></tr><tr><td>NET_DVR_GET_SCHED_CAPTURECFG</td><td>获取抓图计划</td><td>通道号</td><td>NET_DVR_SCHED_CAPTURECFG</td><td>1282</td></tr></table></body></html>  

### 返回目录  

### 5.13.5 设置通道参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.16 所示。  

表 5.16 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_PICCFG_V40</td><td>设置图像参数</td><td>通道号</td><td>NET_DVR_PICCFG_V40</td><td>6180</td></tr><tr><td>NET_DVR_SET_COMPRESSCFG_V30</td><td>设置压缩参数</td><td>通道号</td><td>NET_DVR_COMPRESSIONCFG_V30</td><td>1041</td></tr><tr><td>NET_DVR_SET_RECORDCFG_V40</td><td>设置录像参数</td><td>通道号</td><td>NET_DVR_RECORD_V40</td><td>1009</td></tr><tr><td>NET_DVR_SET_SHOWSTRING_V30</td><td>设置叠加字符参数</td><td>通道号</td><td>NET_DVR_SHOWSTRING_V30</td><td>1031</td></tr><tr><td>NET_DVR_SET_CCDPARAMCFG</td><td>设置前端参数</td><td>无效</td><td>NET_DVR_CAMERAPARAMCFG</td><td>1068</td></tr><tr><td>NET_DVR_SET_CCDPARAMCFG_EX</td><td>设置前端参数(扩展)</td><td>通道号</td><td>NET_DVR_CAMERAPARAMCFG_EX</td><td>3369</td></tr><tr><td>NET_DVR_SET_AUDIO_INPUT</td><td>设置音频输入参数</td><td>通道号</td><td>NET_DVR_AUDIO_INPUT_PARAM</td><td>3202</td></tr><tr><td>NET_DVR_SET_CAMERA_DEHAZE_CFG</td><td>设置去雾参数</td><td>通道号</td><td>NET_DVR_CAMERA_DEHAZE_CFG</td><td>3204</td></tr><tr><td>NET_DVR_SET_AUDIOOUT_VOLUME</td><td>设置输出音频大小</td><td>通道号</td><td>NET_DVR_AUDIOOUT_VOLUME</td><td>3238</td></tr><tr><td>NET_DVR_SET_ISP_CAMERAPARAMCFG</td><td>设置ISP 前端参数配置</td><td>通道号</td><td>NET_DVR_ISP_CAMERAPARAMCFG</td><td>3256</td></tr><tr><td>NET_DVR_SET_LOW_LIGHTCFG</td><td>设置快球低照度参数</td><td>通道号</td><td>NET_DVR_LOW_LIGHT_CFG</td><td>3304</td></tr><tr><td>NET_DVR_SET_FOCUSMODECFG</td><td>设置快球聚焦模式参数</td><td>通道号</td><td>NET_DVR_FOCUSMODE_CFG</td><td>3306</td></tr><tr><td>NET_DVR_SET_INFRARECFG</td><td>设置快球红外参数</td><td>通道号</td><td>NET_DVR_INFRARE_CFG</td><td>3308</td></tr><tr><td>NET_DVR_SET_AEMODECFG</td><td>设置快球其他参数</td><td>通道号</td><td>NET_DVR_AEMODECFG</td><td>3310</td></tr><tr><td>NET_DVR_SET_CORRIDOR_MODE</td><td>设置旋转功能配置</td><td>通道号</td><td>NET_DVR_CORRIDOR_MODE</td><td>3355</td></tr><tr><td>NET_IPC_SET_AUX_ALARMCFG</td><td>设置辅助报警参数</td><td>通道号</td><td>NET_IPC_AUX_ALARMCFG</td><td>3210</td></tr><tr><td>NET_DVR_SET_SIGNAL_SYNC</td><td>设置信号灯同步配置参数</td><td>通道号</td><td>NET_DVR_SIGNAL_SYNCCFG</td><td>3397</td></tr><tr><td>NET_DVR_SET_SNAPINFO_CFG</td><td>设置抓拍图片参数</td><td>通道号</td><td>NET_DVR_SNAPINFOCFG</td><td>3137</td></tr><tr><td>NET_DVR_SET_JPEG_CAPTURE_CFG</td><td>设置设备抓图配置</td><td>通道号</td><td>NET_DVR_JPEG_CAPTURE_CFG</td><td>1281</td></tr><tr><td>NET_DVR_SET_SCHED_CAPTURECFG</td><td>设置抓图计划</td><td>通道号</td><td>NET_DVR_SCHED_CAPTURECFG</td><td>1283</td></tr></table></body></html>  

### 5.13.6 获取通道参数 NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.17[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.17  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.17所示。  

表 5.17 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IpCondBuffer</td><td>lpOutBuffer</td><td>宏定义值</td></tr><tr><td>NETDVRGETOSDBATTERYPOWERCFG</td><td>显示参数</td><td></td><td>NETDVROSDBATTERYPOWERCFG</td><td>3741</td></tr><tr><td>NET_DVR_GET_OIS_CFG</td><td>获取光学防抖配置</td><td>4字节(DWORD)通道号</td><td>NET_DVR_OIS_CFG</td><td>3641</td></tr><tr><td>NETDVRGETSOFTWARE SERVICE</td><td>获取软件服务配置</td><td>4字节(DWORD)通道号</td><td>NET_DVRSOFTWARE SERVICECFG</td><td>3981</td></tr></table></body></html>  

### 返回目录  

### 5.13.7 设置通道参数 NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.18[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.18  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.18 所示。  

表 5.18 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IpCondBuffer</td><td>IplnBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_OSD_BATTERY_POWER_CFG</td><td>显示参数</td><td>设置OSD电池电量4字节(DWORD)通道号</td><td>NETDVROSDBATTERYPOWERCFG</td><td>3742</td></tr><tr><td>NET_DVRSET_OIS_CFG</td><td>设置光学防抖配置</td><td>4字节(DWORD)通道号</td><td>NETDVROISCFG</td><td>3642</td></tr><tr><td>NET_DVR_SET_SOFTWARE_SERVICE</td><td>设置软件服务配置</td><td>4字节(DWORD)通道号</td><td>NETDVRSOFTWARESERVICECFG</td><td>3982</td></tr></table></body></html>  

### 返回目录  

### 5.13.8 批量获取通道参数 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.19[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.20[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，  

[out] lpOutBuffer  

参数值：0 或者 1 表示成功，其他值为失败对应的错误号  
设备返回的参数内容（详见表 5.20），和要查询的监控点一一对  
应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应  
lpOutBuffer 的内容就是无效的  
输出缓冲区大小  

[in] dwOutBufferSize  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.20 所示。  

表 5.19 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_MULTI_STREAM_COMPRESSIONCFG</td><td>远程获取多码流压缩参数</td><td>3216</td></tr><tr><td>NET_DVR_GET_AUDIO_NAME</td><td>获取语音名称</td><td>3385</td></tr></table></body></html>  

表 5.20 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NETDVRGETMULTISTREAMCOMPRESSIONCFG</td><td>dwCount NETDVRMULTISTREAMCOMPRESSIONCFGCOND</td><td>dwCount 个 NETDVRMULTISTREAMCOMPRESSIONCFG</td></tr><tr><td>NET DVRGETAUDION NAME</td><td>dwCount个NET_DVR_CHANNEL_INDEX</td><td>dwCount个NET_D DVRAUDIONAME</td></tr></table></body></html>  

### 返回目录  

### 5.13.9 批量设置通道参数 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.21[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.22[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.22），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错  

原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的获取功能对应不同的结构体和命令号，如表 5.22 所示。  

表 5.21 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_MULTI_STREAM_COMPRESSIONCFG</td><td>远程设置多码流压缩参数</td><td>3217</td></tr><tr><td>NETDVRSETAUDIONAME</td><td>设置语音名称</td><td>3384</td></tr></table></body></html>  

表 5.22 批量设置设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>IplnParamBuffer对应结构体</td></tr><tr><td>NETDVRSETMULTISTREAMCOMPRESSIONCFG</td><td>dwCount</td><td>dwCount 个</td></tr><tr><td></td><td>NETDVRMULTISTREAMCOMPRESSIONCFGCOND</td><td>NETDVRMULTISTREAMCOMPRESSIONCFG</td></tr><tr><td>NETDVRSETAUDIONAME</td><td>dwCount个NET_DVR_CHANNEL_INDEX</td><td>dwCount个 NET_DVRAUDIO_NAME</td></tr></table></body></html>  

### 网络参数配置  

### 5.13.10 获取网络参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.23 所示。  

表 5.23 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_NETCFG_V30</td><td>获取网络参数</td><td>无效</td><td>NET_DVR_NETCFG_V30</td><td>1000</td></tr><tr><td>NET_DVR_GET_NETAPPCFG</td><td>获取网络应用参数(NTP/DDNS)</td><td>无效</td><td>NETDVRNETAPPCFG</td><td>222</td></tr><tr><td>NET_DVR_GET_NTPCFG</td><td>获取网络应用参数(NTP)</td><td>无效</td><td>NET_DVR_NTPPARA</td><td>224</td></tr><tr><td>NET_DVR_GET_DDNSCFG_V30</td><td>获取网络应用参数(DDNS)</td><td>无效</td><td>NET_DVR_DDNSPARA_V30</td><td>1010</td></tr><tr><td>NET_DVR_GET_EMAILCFG_V30</td><td>获取网络应用参数(EMAIL)</td><td>无效</td><td>NET_DVR_EMAILCFG_V30</td><td>1012</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_GET_AP_INFO_LIST</td><td>获取无线网络资源参数</td><td>无效</td><td>NET_DVR_AP_INFO_LIST</td><td>305</td></tr><tr><td>NET_DVR_GET_WIFI_CFG</td><td>获取IP监控设备无线参数</td><td>无效</td><td>NET_DVR_WIFI_CFG</td><td>307</td></tr><tr><td>NET_DVR_GET_WIFI_WORKMODE</td><td>获取IP监控设备网口参数</td><td>无效</td><td>NET_DVR_WIFI_WORKMODE</td><td>309</td></tr><tr><td>NET_DVR_GET_WIFI_STATUS</td><td>获取设备当前wifi连接状态</td><td>无效</td><td>NET_DVR_WIFI_CONNECT_STATUS</td><td>310</td></tr><tr><td>NET_DVR_GET_FTPCFG</td><td>获取首选FTP参数</td><td>无效</td><td>NET_DVR_FTPCFG</td><td>134</td></tr><tr><td>NET_DVR_GET_FTPCFG_SECOND</td><td>获取备用FTP参数</td><td>无效</td><td>NET_DVR_FTPCFG</td><td>6103</td></tr><tr><td>NET_DVR_GET_SNMPCFG</td><td>获取 SNMP参数</td><td>无效</td><td>NET_DVR_SNMPCFG</td><td>1112</td></tr><tr><td>NET_DVR_GET_NAT_CFG</td><td>获取NAT映射参数</td><td>无效</td><td>NET_DVR_NAT_CFG</td><td>6111</td></tr><tr><td>NET_DVR_GET_WPSCFG</td><td>获取无线WPS参数</td><td>无效</td><td>NET_DVR_WPS_PARAM</td><td>3218</td></tr><tr><td>NET_DVR_GET_DEVICE_PIN</td><td>获取设备 PIN 码</td><td>无效</td><td>NET_DVR_PIN_PARAM</td><td>3221</td></tr><tr><td>NET_DVR_GET_GBT28181_ACCESS_CFG</td><td>获取GBT28181协议接入配置</td><td>无效</td><td>NET_DVR_GBT28181_ACCESS_CFG</td><td>3249</td></tr><tr><td>NET_DVR_GET_EZVIZ_ACCESS_CFG</td><td>获取EZVIZ接入参数</td><td>无效</td><td>NET_DVR_EZVIZ_ACCESS_CFG</td><td>3398</td></tr><tr><td>NET_DVR_GET_CMS_CFG</td><td>获取平台参数</td><td>无效</td><td>NET_DVR_CMS_PARAM</td><td>2070</td></tr></table></body></html>  

### 返回目录  

### 5.13.11 设置网络参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.24 所示。  

表 5.24 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_NETCFG_V30</td><td>设置网络参数</td><td>无效</td><td>NET_DVR_NETCFG_V30</td><td>1001</td></tr><tr><td>NET_DVR_SET_NETAPPCFG</td><td>设置网络应用参数(NTP/DDNS)</td><td>无效</td><td>NET_DVR_NETAPPCFG</td><td>223</td></tr><tr><td>NET_DVR_SET_NTPCFG</td><td>设置网络应用参数(NTP)</td><td>无效</td><td>NET_DVR_NTPPARA</td><td>225</td></tr><tr><td>NET_DVR_SET_DDNSCFG_V30</td><td>设置网络应用参数(DDNS)</td><td>无效</td><td>NET_DVR_DDNSPARA_V30</td><td>1011</td></tr><tr><td>NET_DVR_SET_EMAILCFG_V30</td><td>设置网络应用参数（EMAIL）</td><td>无效</td><td>NET_DVR_EMAILCFG_V30</td><td>1013</td></tr><tr><td>NET_DVR_SET_WIFI_CFG</td><td>设置IP监控设备无线参数</td><td>无效</td><td>NET_DVR_WIFI_CFG</td><td>306</td></tr><tr><td>NET_DVR_SET_WIFI_WORKMODE</td><td>设置IP监控设备网口参数</td><td>无效</td><td>NET_DVR_WIFI_WORKMODE</td><td>308</td></tr><tr><td>NET_DVR_SET_FTPCFG</td><td>设置首选FTP参数</td><td>无效</td><td>NET_DVR_FTPCFG</td><td>135</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVRSET_FTPCFG_SECOND</td><td>设置备用FTP参数</td><td>无效</td><td>NETDVRFTPCFG</td><td>6104</td></tr><tr><td>NET_DVR_SET_SNMPCFG</td><td>设置SNMP参数</td><td>无效</td><td>NET_DVR_SNMPCFG</td><td>1113</td></tr><tr><td>NET_DVR_SET_NAT_CFG</td><td>设置NAT映射参数</td><td>无效</td><td>NET_DVR_NAT_CFG</td><td>6112</td></tr><tr><td>NET_DVR_SET_WPSCFG</td><td>设置无线WPS参数</td><td>无效</td><td>NET_DVR_WPS_PARAM</td><td>3219</td></tr><tr><td>NET_DVR_SET_GBT28181_ACCESS_CFG</td><td>设置GBT28181协议接入配置</td><td>无效</td><td>NET_DVR_GBT28181_ACCESS_CFG</td><td>3250</td></tr><tr><td>NET_DVR_SET_EZVIZ_ACCESS_CFG</td><td>设置EZVIZ接入参数</td><td>无效</td><td>NET_DVR_EZVIZ_ACCESS_CFG</td><td>3399</td></tr><tr><td>NET_DVR_SET_CMS_CFG</td><td>设置平台参数</td><td>无效</td><td>NET_DVR_CMS_PARAM</td><td>2071</td></tr></table></body></html>  

### 返回目录  

### 5.13.12 获取网络参数 NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.25[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.25  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.25所示。  

表 5.25 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>lpCondBuffer</td><td>lpOutBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_WIRELESS_DIAL</td><td>获取无线参数配置</td><td>4字节(DWORD)网卡号</td><td>NET_DVR_WIRELESSDIAL_CFG</td><td>3578</td></tr><tr><td>NET_DVR_GET_WIRELESSDIAL_SCHEDULE</td><td>获取拨号计划配置</td><td>4字节(DWORD)网卡号</td><td>NET_DVRWIRELESSDIAL_SCHEDULE</td><td>3581</td></tr><tr><td>NET_DVR_GET_WIRELESSDIAL_STATUS</td><td>获取拨号状态</td><td>4字节(DWORD)网卡号</td><td>NET_DVR_WIRELESSDIAL_STATUS</td><td>3583</td></tr><tr><td>NET_DVR_GET_WIRELESSSERVER</td><td>获取WIFI热点参数 配置</td><td>4字节(DWORD)无线网 卡号</td><td>NET_DVR_WIRELESSSERVER</td><td>3717</td></tr><tr><td>NET_DVR_GET_FTPUPLOAD_CFG</td><td>获取FTP上传信息 规整参数</td><td>NULL</td><td>NET_DVRFTPUPLOADCFG</td><td>3783</td></tr><tr><td>NET_DVR_GET_ANR_ARMING_HOST</td><td>获取断网续传的主 机信息</td><td>NULL</td><td>NET_DVR_ANR_ARMING_HOST</td><td>3773</td></tr><tr><td>NET_DVR_GET_MACFILTER_CFG</td><td>获取 MAC 地址过NULL 滤配置</td><td></td><td>NET_DVRMACFILTER_CFG</td><td>3644</td></tr></table></body></html>  

### 5.13.13 设置网络参数 NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID [in]dwCommand [in&out]lpConfigParam  

用户 ID 号，NET_DVR_Login_V40 的返回值  
设备配置命令，详见表 5.26  
配置输入输出参数，不同的配置功能对应不同的输入输出参数，  
详见表 5.26  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.26 所示。  

表 5.26 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IpCondBuffer</td><td>IplnBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_WIRELESS_DIAL</td><td>设置无线参数配置</td><td>4字节(DWORD)网卡号</td><td>NET_DVR_WIRELESSDIAL_CFG</td><td>3579</td></tr><tr><td>NET_DVR_SET_WIRELESSDIAL_SCHEDULE</td><td>设置拨号计划配置</td><td>4字节(DWORD)网卡号</td><td>NET_DVR_WIRELESSDIAL_SCHEDULE</td><td>3582</td></tr><tr><td>NET_DVR_SET_WIRELESSSERVER</td><td>设置WIFI热点参数 配置</td><td>4字节(DWORD)无线网 卡号</td><td>NET_DVR_WIRELESSSERVER</td><td>3718</td></tr><tr><td>NET_DVR_SET_FTPUPLOAD_CFG</td><td>设置FTP上传信息 规整参数</td><td>NULL</td><td>NET_DVR_FTPUPLOADCFG</td><td>3784</td></tr><tr><td>NET_DVR_SET_MACFILTER_CFG</td><td>设置MAC地址过滤 配置</td><td>NULL</td><td>NET_DVR_MACFILTER_CFG</td><td>3645</td></tr></table></body></html>  

### 5.13.14 批量获取网络参数 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.27[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.28[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.28），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.28 所示。  

表 5.27 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NETD DVR_GET_GBT28181_CHANINFO_CFG</td><td>获取GBT28181 协议接入设备编码通道信息</td><td>3251</td></tr><tr><td>NET_DVR_GET_GBT28181_ALARMINCFG</td><td>获取GBT28181 协议接入设备报警输入通道信息</td><td>3253</td></tr></table></body></html>  

表 5.28 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>lplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_GBT28181_CHANINFO_CFG</td><td>dwCount个NET_DVR_STREAM_INFO</td><td>dwCount个 NET_DVR_GBT28181_CHANINFO_CFG</td></tr><tr><td>NET_DVR_GET_GBT28181_ALARMINCFG</td><td>dwCount个NET_DVR_ALARMIN_INFO</td><td>dwCount个NET_DVR_GBT28181_ALARMINCFG</td></tr></table></body></html>  

### 返回目录  

### 5.13.15 批量设置网络参数 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.29[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.30[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.30），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的获取功能对应不同的结构体和命令号，如表 5.30 所示。  

表 5.29 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET DVR_SET_GBT28181_CHANINFO_CFG</td><td>设置 GBT28181 协议接入设备编码通道</td><td>3252</td></tr><tr><td>NET_DVR_SET_GBT28181_ALARMINCFG</td><td>设置GBT28181 协议接入设备报警输入通道</td><td>3254</td></tr></table></body></html>  

表 5.30 批量设置设备参数  


<html><body><table><tr><td>dwCommand</td><td>lplnBuffer对应结构体</td><td>IplnParamBuffer对应结构体</td></tr><tr><td>NET_DVR_SET_GBT28181_CHANINFO_CFG</td><td>dwCount个NET_DVR_STREAM_INFO</td><td>dwCount个NET_DVR_GBT28181_CHANINFO_CFG</td></tr><tr><td>NETDVRSETGBT28181ALARMINCFG</td><td>dwCount个NET_DVRALARMIN_INFO</td><td>dwCount个NET_DVR_GBT28181_ALARMINCFG</td></tr></table></body></html>  

### 返回目录  

### 5.13.16 获取 RTSP 协议参数 NET_DVR_GetRtspConfig  

函  数： BOOL  NET_DVR_GetRtspConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_RTSPCFGlpOutBuffer, DWORD dwOutBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 保留，置为 0[out]lpOutBuffer 输出缓存[in]dwOutBufferSize 存放输出数据的缓冲区大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.13.17 设置 RTSP 协议参数 NET_DVR_SetRtspConfig  

函  数： BOOL NET_DVR_SetRtspConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_RTSPCFGlpInBuffer, DWORD dwInBufferSize)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 保留，置为 0[in]lpInBuffer 输入缓存[in]dwOutBufferSize 输入缓存的大小，大小为结构体 NET_DVR_RTSPCFG  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 报警输入输出配置  

### 5.13.18 获取设备参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针  

[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.31 所示。  

表 5.31 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_ALARMINCFG_V40</td><td>获取报警输入参数</td><td>报警输入号，从0开始</td><td>NET_DVR_ALARMINCFG_V40</td><td>6181</td></tr><tr><td>NET_DVR_GET_ALARMOUTCFG_V30</td><td>获取报警输出参数</td><td>报警输出号，从0开始</td><td>NET_DVRALARMOUTCFG_V30</td><td>1026</td></tr></table></body></html>  

### 返回目录  

### 5.13.19 设置设备参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.32 所示。  

表 5.32 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_ALARMINCFG_V40</td><td>设置报警输入参数</td><td>报警输入号，从0开始</td><td>NET_DVR_ALARMINCFG_V40</td><td>6182</td></tr><tr><td>NET_DVR_SET_ALARMOUTCFG_V30</td><td>设置报警输出参数</td><td>报警输出号，从0开始</td><td>NET_DVR_ALARMOUTCFG_V30</td><td>1027</td></tr></table></body></html>  

### 返回目录  

### 5.13.20 获取设备报警输出 NET_DVR_GetAlarmOut_V30  

函  数： BOOL  NET_DVR_GetAlarmOut_V30(LONG lUserID, LPNET_DVR_ALARMOUTSTATUS_V30lpAlarmOutState)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[out]lpAlarmOutState 报警输出状态  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.13.21 设置设备报警输出 NET_DVR_SetAlarmOut  

函  数： BOOL  NET_DVR_SetAlarmOut(LONG lUserID, LONG lAlarmOutPort,LONG lAlarmOutStatic)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]lAlarmOutPort 报警输出口。初始输出口从 0 开始，0x00ff 表示全部模拟输出，0xff00 表示全部数字输出。[in]lAlarmOutStatic 报警输出状态：0- 停止输出，1- 输出  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 用户和安全参数配置  

### 5.13.22 获取设备参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.33 所示。  

表 5.33 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRGETUSERCFGV40</td><td>获取用户参数</td><td>组号，从0开始，每组32个用户</td><td>NETDVRUSER_V40</td><td>6187</td></tr><tr><td>NETDVRGETSECURITYCFG</td><td>获取安全认证配置</td><td>无效</td><td>NETDVRSECURITYCFG</td><td>147</td></tr></table></body></html>  

### 返回目录  

### 5.13.23 设置设备参数 NET_DVR_SetDVRConfig  

函  数： BOOL  NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可  

[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.34 所示。  

表 5.34 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVRSET_USERCFG_V40</td><td>设置用户参数</td><td>组号，从0开始，每组32个用户</td><td>NETDVRUSERV40</td><td>6188</td></tr><tr><td>NET_DVR_SET_SECURITY_CFG</td><td>设置安全认证配置</td><td>无效</td><td>NETDVRSECURITY_CFG</td><td>148</td></tr></table></body></html>  

### 外设参数配置  

### 5.13.24 获取设备参数 NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.35[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.35  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.35所示。  

表 5.35 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>lpCondBuffer</td><td>lpOutBuffer</td><td>宏定义值</td></tr><tr><td>NETDVRGETTHSCREEN</td><td>获取温湿度配置参数</td><td>4字节(DWORD)通道号</td><td>NETDVRTHSCREEN</td><td>3721</td></tr><tr><td>NETDVRGETEXTERNALDEVICE</td><td>获取外设（补光灯等）配 置参数</td><td>NULL</td><td>NETDVREXTERNALDEVICE</td><td>3723</td></tr><tr><td>NETDVRGETSUPPLEMENTLIGHT</td><td>获取内置补光灯配置</td><td>4字节(DWORD)通道号</td><td>NETDVRBUILTINSUPPLEMENTLIGHT</td><td>3728</td></tr><tr><td>NET_DVR_GET_REVISE_GPS</td><td>获取校准的GPS经纬度</td><td>4字节(DWORD)通道号</td><td>NETDVRREVISE_GPS_CFG</td><td>3753</td></tr></table></body></html>  

### 返回目录  

### 5.13.25 设置设备参数 NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.36  

[in&out]lpConfigParam  

配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.36  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.36 所示。  

表 5.36 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IpCondBuffer</td><td>IplnBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_THSCREEN</td><td>设置温湿度配置参数</td><td>4字节(DWORD)通道号</td><td>NETDVRTHSCREEN</td><td>3730</td></tr><tr><td>NET_DVRSET_EXTERNALDEVICE</td><td>设置外设（补光灯等）配 置参数</td><td>NULL</td><td>NETDVREXTERNALDEVICE</td><td>3724</td></tr><tr><td>NET_DVR_SET_SUPPLEMENTLIGHT</td><td>设置内置补光灯配置</td><td>4字节(DWORD)通道号</td><td>NET_DVR_BUILTIN_SUPPLEMENTLIGHT</td><td>3729</td></tr><tr><td>NET_DVR_SET_REVISE_GPS</td><td>设置校准的GPS经纬度</td><td>4字节(DWORD)通道号</td><td>NET_DVR_REVISE_GPS_CFG</td><td>3754</td></tr><tr><td>NETDVRSETTHSCREEN</td><td>设置温湿度配置参数</td><td>4字节(DWORD)通道号</td><td>NETDVRTHSCREEN</td><td>3730</td></tr></table></body></html>  

### 5.13.26 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.37[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.37[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.37），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.37 所示。  

表 5.37 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>lplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_IOOUT_CFG</td><td>获取补光灯参数</td><td>dwCount个NET_DVR_IOOUT_COND</td><td>dwCount个NET_DVR_IOOUT_CFG</td><td>3394</td></tr></table></body></html>  

### 5.13.27 批量设置配置信息 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.38[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.38[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.38），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的获取功能对应不同的结构体和命令号，如表 5.38 所示。  

表 5.38 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>IplnBuffer对应结构体</td><td>lplnParamBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_IOOUT_CFG</td><td>设置补光灯参数</td><td>dwCount个NET_DVR_IOOUT_COND</td><td>dwCount个NET_DVR_IOOUT_CFG</td><td>3395</td></tr></table></body></html>  

## 5.14SMART 参数配置  

### 参数配置  

### 5.14.1 获取设备的配置信息 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.39[in]lChannel 通道号，不同的命令对应不同的取值，如果该参数无效则置为0xFFFFFFFF 即可，详见表 5.39[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.39 所示。  

$\bullet$ 通道号是指设备视频通道号，通过注册设备（NET_DVR_Login_V30）返回的设备信息（NET_DVR_DEVICEINFO_V30）获取模拟通道个数（byChanNum）、模拟通道起始通道号（byStartChan）和设备支持的最大 IP 通道数（byIPChanNum $^+$ byHighDChanNum $^{*}256$ ）、数字通道起始通道号（byStartDChan）。  
$\bullet$ 对于网络摄像机、网络球机，设备只有一个通道，通道号即为 1。  

表 5.39 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_VCA_CTRLCFG</td><td>获取智能控制参数</td><td>无效</td><td>NET_VCA_CTRLCFG</td><td>165</td></tr><tr><td>NET_DVR_GET_CALIBRATION</td><td>获取标定信息</td><td>通道号</td><td>NETDVRCALIBRATION_CFG</td><td>183</td></tr><tr><td>NET_DVR_GET_FACESNAPCFG</td><td>获取人脸抓拍参数</td><td>通道号</td><td>NET_VCA_FACESNAPCFG</td><td>5001</td></tr><tr><td>NET_DVR_GET_CURTRIGGERMODE</td><td>获取设备当前触发模式</td><td>无效</td><td>NETDVRCURTRIGGERMODE</td><td>3130</td></tr><tr><td>NET_ITS_GET_IPC_CHAN_CFG</td><td>获取监测点信息配置</td><td>通道号</td><td>NET_ITS_IPC_CHAN_CFG</td><td>5070</td></tr></table></body></html>  

### 返回目录  

### 5.14.2 设置设备的配置信息 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.40[in]lChannel 通道号，不同的命令对应不同的取值，如果该参数无效则置为0xFFFFFFFF 即可，详见表 5.40[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.40 所示。  

表 5.40 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_VCA_CTRLCFG</td><td>设置智能控制参数</td><td>无效</td><td>NET_VCA_CTRLCFG</td><td>164</td></tr><tr><td>NET_DVR_SET_CALIBRATION</td><td>设置标定信息</td><td>通道号</td><td>NETDVRCALIBRATIONCFG</td><td>182</td></tr><tr><td>NET_DVR_SET_FACESNAPCFG</td><td>设置人脸抓拍参数</td><td>通道号</td><td>NET_VCA_FACESNAPCFG</td><td>5002</td></tr><tr><td>NET_ITS_SET_IPC_CHAN_CFG</td><td>设置监测点信息配置</td><td>通道号</td><td>NET_ITS_IPC_CHAN_CFG</td><td>5071</td></tr><tr><td>NET_DVR_SET_VCA_RULE_COLOR_CFG</td><td>设置智能规则关联的颜色参数</td><td>通道号</td><td>NET_DVR_VCA_RULE_COLOR_CFG</td><td>411</td></tr></table></body></html>  

### 返回目录  

### 5.14.3 获取设备的配置信息(标准协议)NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.41[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.42  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.42所示。  

表 5.41 参数获取配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>进入区域侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_REGION_ENTR_DETECTION</td><td>获取进入区域配置</td><td>3503</td></tr><tr><td>NET_DVR_GET_REGION_ENTR_REGION</td><td>获取进入区域的单个区域配置</td><td>3505</td></tr><tr><td>NET_DVR_GET_REGION_ENTR_TRIGGER</td><td>获取进入区域联动配置</td><td>3507</td></tr><tr><td>NET_DVR_GET_REGION_ENTR_SCHEDULE</td><td>获取进入区域布防时间配置</td><td>3509</td></tr><tr><td>离开区域侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_REGION_EXITING_DETECTION</td><td>获取离开区域配置</td><td>3512</td></tr><tr><td>NET_DVR_GET_REGION_EXITING_REGION</td><td>获取离开区域的单个区域配置</td><td>3514</td></tr><tr><td>NET_DVR_GET_REGION_EXIT_TRIGGER</td><td>获取离开区域联动配置</td><td>3516</td></tr><tr><td>NET_DVR_GET_REGION_EXIT_SCHEDULE</td><td>获取离开区域布防时间配置</td><td>3518</td></tr><tr><td>徘徊侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_LOITERING_DETECTION</td><td>获取徘徊侦测配置</td><td>3521</td></tr><tr><td>NET_DVR_GET_LOITERING_REGION</td><td>获取徘徊的单个区域配置</td><td>3523</td></tr><tr><td>NET_DVR_GET_LOITERING_TRIGGER</td><td>获取徘徊联动配置</td><td>3525</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_GET_LOITERING_SCHEDULE</td><td>获取徘徊布防时间配置</td><td>3527</td></tr><tr><td>人员聚集侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_GROUP_DETECTION</td><td>获取人员聚集侦测配置</td><td>3530</td></tr><tr><td>NET_DVR_GET_GROUPDETECTION_REGION</td><td>获取人员聚集的单个区域配置</td><td>3532</td></tr><tr><td>NET_DVR_GET_GROUPDETECTION_TRIGGER</td><td>获取人员聚集联动配置</td><td>3534</td></tr><tr><td>NET_DVR_GET_GROUPDETECTION_SCHEDULE</td><td>获取人员聚集布防时间配置</td><td>3536</td></tr><tr><td>快速运动侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_DETECTION</td><td>获取快速运动侦测配置</td><td>3539</td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_REGION</td><td>获取快速运动的单个区域配置</td><td>3541</td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_TRIGGER</td><td>获取快速运动联动配置</td><td>3543</td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_SCHEDULE</td><td>获取快速运动的布防时间配置</td><td>3545</td></tr><tr><td>停车侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_PARKING_DETECTION</td><td>获取停车侦测配置</td><td>3548</td></tr><tr><td>NET_DVR_GET_PARKING_REGION</td><td>获取停车侦测的单个区域配置</td><td>3550</td></tr><tr><td>NET_DVR_GET_PARKING_TRIGGER</td><td>获取停车侦测联动配置</td><td>3552</td></tr><tr><td>NET_DVR_GET_PARKING_SCHEDULE</td><td>获取停车侦测的布防时间配置</td><td>3554</td></tr><tr><td>物品遗留侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_DETECTION</td><td>获取物品遗留侦测配置</td><td>3557</td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_REGION</td><td>获取物品遗留侦测的单个区域配置</td><td>3559</td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_TRIGGER</td><td>获取物品遗留侦测联动配置</td><td>3561</td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_SCHEDULE</td><td>获取物品遗留侦测的布防时间配置</td><td>3563</td></tr><tr><td>物品拿取侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_DETECTION</td><td>获取物品拿取侦测配置</td><td>3566</td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_REGION</td><td>获取物品拿取侦测的单个区域配置</td><td>3568</td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_TRIGGER</td><td>获取物品拿取侦测联动配置</td><td>3570</td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_SCHEDULE</td><td>获取物品拿取侦测的布防时间配置</td><td>3572</td></tr><tr><td>授权或非授权名单参数配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_VEHICLE_BLACKLST_SCHEDULE</td><td>获取非授权名单布防时间配置</td><td>6622</td></tr><tr><td>NET_DVR_GET_VEHICLE_BLACKLIST_EVENT_TRIGGER</td><td>获取非授权名单布防联动配置</td><td>6626</td></tr><tr><td>NET_DVR_GET_VEHICLE_WHITELST_SCHEDULE</td><td>获取授权名单布防时间配置</td><td>6624</td></tr><tr><td>NET_DVR_GET_VEHICLE_WHITELIST_EVENT_TRIGGER</td><td>获取授权名单布防联动配置</td><td>6628</td></tr><tr><td>NET_DVR_GET_VEHICLE_ALLLIST_EVENT_TRIGGER</td><td>获取全部车辆检测名单布防联动配置</td><td>6631</td></tr><tr><td>NET_DVR_GET_VEHICLE_OTHERLIST_EVENT_TRIGGER</td><td>获取其他车辆检测名单布防联动配置</td><td>6633</td></tr><tr><td>其他参数配置</td><td></td><td></td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_GET_REGION_CLIP</td><td>获取区域裁剪配置</td><td>3575</td></tr><tr><td>NETDVRGETLITESTORAGE</td><td>获取轻存储配置</td><td>3594</td></tr><tr><td>NET_DVR_GET_VEHICLE_CALIBRATION</td><td>获取车辆检测标定</td><td>3598</td></tr><tr><td>NETDVRGETPDCRECOMMEND</td><td>获取客流统计表示推荐值</td><td>3755</td></tr></table></body></html>  

表 5.42 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>IpCondBuffer</td><td>IpOutBuffer</td></tr><tr><td>进入区域侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_REGION_ENTR_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_REGION_ENTRANCE_DETECTION</td></tr><tr><td>NET_DVR_GET_REGION_ENTR_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_REGIONENTRANCE_REGION</td></tr><tr><td>NET_DVR_GET_REGION_ENTR_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_GET_REGION_ENTR_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>离开区域侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_REGION_EXITING_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_REGION_EXITING_DETECTION</td></tr><tr><td>NET_DVR_GET_REGION_EXITING_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_REGIONEXITING_REGION</td></tr><tr><td>NET_DVR_GET_REGION_EXIT_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_GET_REGION_EXIT_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>徘徊侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_LOITERING_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_LOITERING_DETECTION</td></tr><tr><td>NET_DVR_GET_LOITERING_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_LOITERING_REGION</td></tr><tr><td>NET_DVR_GET_LOITERING_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_GET_LOITERING_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>人员聚集侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_GROUP_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_GROUP_DETECTION</td></tr><tr><td>NET_DVR_GET_GROUPDETECTION_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_GROUPDETECTION_REGION</td></tr><tr><td>NET_DVR_GET_GROUPDETECTION_TRIGGER</td><td>4 字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_GET_GROUPDETECTION_SCHEDULE</td><td>4 字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>快速运动侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_RAPIDMOVE_DETECTION</td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_RAPIDMOVE_REGION</td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_GET_RAPIDMOVE_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>停车侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_GET_PARKING_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_PARKING_DETECTION</td></tr></table></body></html>  

<html><body><table><tr><td colspan="4"></td></tr><tr><td>NET_DVR_GET_PARKING_REGION</td><td></td><td>NET_DVR_SMART_REGION_COND NET_DVR_PARKING_REGION</td><td></td></tr><tr><td>NET_DVR_GET_PARKING_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td><td></td></tr><tr><td>NET_DVR_GET_PARKING_SCHEDULE</td><td>4字节(DWORD)通道号</td><td></td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>物品遗留侦测配置</td><td></td><td></td><td></td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_DETECTION</td><td>4字节(DWORD)通道号</td><td></td><td>NET_DVR_UNATTENDED_BAGGAGE_DETECTION</td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td></td><td>NET_DVR_UNATTENDED_BAGGAGE_REGION</td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_TRIGGER</td><td>4字节(DWORD)通道号</td><td></td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_GET_UNATTENDED_BAGGAGE_SCHEDULE</td><td>4字节(DWORD)通道号</td><td></td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>物品拿取侦测配置</td><td></td><td></td><td></td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_DETECTION</td><td>4字节(DWORD)通道号</td><td></td><td>NET_DVR_ATTENDED_BAGGAGE_DETECTION</td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td></td><td>NET_DVR_ATTENDED_BAGGAGE_REGION</td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_TRIGGER</td><td>4 字节(DWORD)通道号</td><td></td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_GET_ATTENDEDBAGGAGE_SCHEDULE</td><td>4 字节(DWORD)通道号</td><td></td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>授权或非授权名单参数配置</td><td></td><td></td><td></td></tr><tr><td>NET_DVR_GET_VEHICLE_BLACKLST_SCHEDULE</td><td>NULL</td><td></td><td>BlackListScheduleList(XML 描述)</td></tr><tr><td>NET_DVR_GET_VEHICLE_BLACKLIST_EVENT_TRIGGER</td><td>NULL</td><td></td><td>EventTrigger(XML 描述)</td></tr><tr><td>NET_DVR_GET_VEHICLE_WHITELST_SCHEDULE</td><td>NULL</td><td></td><td>WhiteListScheduleList(XML 描述)</td></tr><tr><td>NET_DVR_GET_VEHICLE_WHITELIST_EVENT_TRIGGER</td><td>NULL</td><td></td><td>EventTrigger(XML 描述)</td></tr><tr><td>NET_DVR_GET_VEHICLE_ALLLIST_EVENT_TRIGGER</td><td>NULL</td><td></td><td>EventTrigger(XML 描述)</td></tr><tr><td>NET_DVR_GET_VEHICLE_OTHERLIST_EVENT_TRIGGER</td><td>NULL</td><td></td><td>EventTrigger(XML 描述)</td></tr><tr><td>其他参数配置</td><td></td><td></td><td></td></tr><tr><td>NET_DVR_GET_REGION_CLIP</td><td>NET_DVR_REGION_CLIP_COND</td><td></td><td>NET_DVR_REGION_CLIP_CFG</td></tr><tr><td>NET_DVR_GET_LITESTORAGE</td><td>4字节(DWORD)通道号</td><td></td><td>NET_DVR_LITESTORAGE</td></tr><tr><td>NET_DVR_GET_VEHICLE_CALIBRATION</td><td>4字节(DWORD)通道号</td><td></td><td>NET_DVR_CALIBRATION</td></tr><tr><td>NET_DVR_GET_PDC_RECOMMEND</td><td>4字节(DWORD)通道号</td><td></td><td>NET_DVR_PDC_RECOMMEND</td></tr></table></body></html>  

### 5.14.4 获取设备的配置信息(标准协议)NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.43[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.44  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.44 所示。  

表 5.43 设置参数配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>进入区域侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_REGION_ENTR_DETECTION</td><td>设置进入区域配置</td><td>3504</td></tr><tr><td>NET_DVR_SET_REGION_ENTR_REGION</td><td>设置进入区域的单个区域配置</td><td>3506</td></tr><tr><td>NET_DVR_SET_REGION_ENTR_TRIGGER</td><td>设置进入区域联动配置</td><td>3508</td></tr><tr><td>NET_DVR_SET_REGION_ENTR_SCHEDULE</td><td>设置进入区域布防时间配置</td><td>3510</td></tr><tr><td>离开区域侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_REGION_EXITING_DETECTION</td><td>设置离开区域配置</td><td>3513</td></tr><tr><td>NET_DVR_SET_REGION_EXITING_REGION</td><td>设置离开区域的单个区域配置</td><td>3515</td></tr><tr><td>NET_DVR_SET_REGION_EXIT_TRIGGER</td><td>设置离开区域联动配置</td><td>3517</td></tr><tr><td>NET_DVR_SET_REGION_EXIT_SCHEDULE</td><td>设置离开区域布防时间配置</td><td>3519</td></tr><tr><td>徘徊侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_LOITERING_DETECTION</td><td>设置徘徊侦测配置</td><td>3522</td></tr><tr><td>NET_DVR_SET_LOITERING_REGION</td><td>设置徘徊的单个区域配置</td><td>3524</td></tr><tr><td>NET_DVR_SET_LOITERING_TRIGGER</td><td>设置徘徊联动配置</td><td>3526</td></tr><tr><td>NET_DVR_SET_LOITERING_SCHEDULE</td><td>设置徘徊布防时间配置</td><td>3528</td></tr><tr><td>人员聚集侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_GROUP_DETECTION</td><td>设置人员聚集侦测配置</td><td>3531</td></tr><tr><td>NET_DVR_SET_GROUPDETECTION_REGION</td><td>设置人员聚集的单个区域配置</td><td>3533</td></tr><tr><td>NET_DVR_SET_GROUPDETECTION_TRIGGER</td><td>设置人员聚集联动配置</td><td>3535</td></tr><tr><td>NET_DVR_SET_GROUPDETECTION_SCHEDULE</td><td>设置人员聚集布防时间配置</td><td>3537</td></tr><tr><td>快速运动侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_RAPIDMOVE_DETECTION</td><td>设置快速运动侦测配置</td><td>3540</td></tr><tr><td>NET_DVR_SET_RAPIDMOVE_REGION</td><td>设置快速运动的单个区域配置</td><td>3542</td></tr><tr><td>NET_DVR_SET_RAPIDMOVE_TRIGGER</td><td>设置快速运动联动配置</td><td>3544</td></tr><tr><td>NET_DVR_SET_RAPIDMOVE_SCHEDULE</td><td>设置快速运动的布防时间配置</td><td>3546</td></tr><tr><td>停车侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_PARKING_DETECTION</td><td>设置停车侦测配置</td><td>3549</td></tr><tr><td>NET_DVR_SET_PARKING_REGION</td><td>设置停车侦测的单个区域配置</td><td>3551</td></tr><tr><td>NET_DVR_SET_PARKING_TRIGGER</td><td>设置停车侦测联动配置</td><td>3553</td></tr><tr><td>NET_DVR_SET_PARKING_SCHEDULE</td><td>设置停车侦测的布防时间配置</td><td>3555</td></tr></table></body></html>  

<html><body><table><tr><td>进入物品遗留侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_UNATTENDED_BAGGAGE_DETECTION</td><td>设置物品遗留侦测配置</td><td>3558</td></tr><tr><td>NET_DVR_SET_UNATTENDED_BAGGAGE_REGION</td><td>设置物品遗留侦测的单个区域配置</td><td>3560</td></tr><tr><td>NET_DVR_SET_UNATTENDED_BAGGAGE_TRIGGER</td><td>设置物品遗留侦测联动配置</td><td>3562</td></tr><tr><td>NET_DVR_SET_UNATTENDED_BAGGAGE_SCHEDULE</td><td>设置物品遗留侦测的布防时间配置</td><td>3564</td></tr><tr><td>物品拿取侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_ATTENDEDBAGGAGE_DETECTION</td><td>设置物品拿取侦测配置</td><td>3567</td></tr><tr><td>NET_DVR_SET_ATTENDEDBAGGAGE_REGION</td><td>设置物品拿取侦测的单个区域配置</td><td>3569</td></tr><tr><td>NET_DVR_SET_ATTENDEDBAGGAGE_TRIGGER</td><td>设置物品拿取侦测联动配置</td><td>3571</td></tr><tr><td>NET_DVR_SET_ATTENDEDBAGGAGE_SCHEDULE</td><td>设置物品拿取侦测的布防时间配置</td><td>3573</td></tr><tr><td>授权或非授权名单参数配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_VEHICLE_BLACKLST_SCHEDULE</td><td>设置非授权名单布防时间配置</td><td>6623</td></tr><tr><td>NET_DVR_SET_VEHICLE_BLACKLIST_EVENT_TRIGGER</td><td>获取非授权名单布防联动配置</td><td>6627</td></tr><tr><td>NET_DVR_SET_VEHICLE_WHITELST_SCHEDULE</td><td>设置授权名单布防时间配置</td><td>6625</td></tr><tr><td>NET_DVR_SET_VEHICLE_WHITELIST_EVENT_TRIGGER</td><td>获取授权名单布防联动配置</td><td>6629</td></tr><tr><td>NET_DVR_SET_VEHICLE_ALLLIST_EVENT_TRIGGER</td><td>获取全部车辆检测名单布防联动配置</td><td>6632</td></tr><tr><td>NET_DVR_SET_VEHICLE_OTHERLIST_EVENT_TRIGGER</td><td>获取其他车辆检测名单布防联动配置</td><td>6634</td></tr><tr><td>其他参数配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_REGION_CLIP</td><td>设置区域裁剪配置</td><td>3576</td></tr><tr><td>NET_DVR_SET_LITESTORAGE</td><td>设置轻存储配置</td><td>3595</td></tr></table></body></html>  

表 5.44 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>IpCondBuffer</td><td>IplnBuffer</td></tr><tr><td>进入区域侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_REGION_ENTR_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_REGION_ENTRANCE_DETECTION</td></tr><tr><td>NET_DVR_SET_REGION_ENTR_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_REGIONENTRANCE_REGION</td></tr><tr><td>NET_DVR_SET_REGION_ENTR_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_SET_REGION_ENTR_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>离开区域侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_REGION_EXITING_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_REGION_EXITING_DETECTION</td></tr><tr><td>NET_DVR_SET_REGION_EXITING_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_REGIONEXITING_REGION</td></tr><tr><td>NET_DVR_SET_REGION_EXIT_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_SET_REGION_EXIT_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>徘徊侦测配置</td><td></td><td></td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_SET_LOITERING_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_LOITERING_DETECTION</td></tr><tr><td>NET_DVR_SET_LOITERING_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_LOITERING_REGION</td></tr><tr><td>NET_DVR_SET_LOITERING_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_SET_LOITERING_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>人员聚集侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_GROUP_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_GROUP_DETECTION</td></tr><tr><td>NET_DVR_SET_GROUPDETECTION_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_GROUPDETECTION_REGION</td></tr><tr><td>NET_DVR_SET_GROUPDETECTION_TRIGGER</td><td>4 字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_SET_GROUPDETECTION_SCHEDULE</td><td>4 字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>快速运动侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_RAPIDMOVE_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_RAPIDMOVE_DETECTION</td></tr><tr><td>NET_DVR_SET_RAPIDMOVE_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_RAPIDMOVE_REGION</td></tr><tr><td>NET_DVR_SET_RAPIDMOVE_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_SET_RAPIDMOVE_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>停车侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_PARKING_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_PARKING_DETECTION</td></tr><tr><td>NET_DVR_SET_PARKING_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_PARKING_REGION</td></tr><tr><td>NET_DVR_SET_PARKING_TRIGGER</td><td>4 字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_SET_PARKING_SCHEDULE</td><td>4 字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>进入物品遗留侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_UNATTENDED_BAGGAGE_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_UNATTENDED_BAGGAGE_DETECTION</td></tr><tr><td>NET_DVR_SET_UNATTENDED_BAGGAGE_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_UNATTENDED_BAGGAGE_REGION</td></tr><tr><td>NET_DVR_SET_UNATTENDED_BAGGAGE_TRIGGER</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_SET_UNATTENDED_BAGGAGE_SCHEDULE</td><td>4字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>物品拿取侦测配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_ATTENDEDBAGGAGE_DETECTION</td><td>4字节(DWORD)通道号</td><td>NET_DVR_ATTENDED_BAGGAGE_DETECTION</td></tr><tr><td>NET_DVR_SET_ATTENDEDBAGGAGE_REGION</td><td>NET_DVR_SMART_REGION_COND</td><td>NET_DVR_ATTENDED_BAGGAGE_REGION</td></tr><tr><td>NET_DVR_SET_ATTENDEDBAGGAGE_TRIGGER</td><td>4 字节(DWORD)通道号</td><td>NET_DVR_EVENT_TRIGGER</td></tr><tr><td>NET_DVR_SET_ATTENDEDBAGGAGE_SCHEDULE</td><td>4 字节(DWORD)通道号</td><td>NET_DVR_EVENT_SCHEDULE</td></tr><tr><td>授权或非授权名单参数配置</td><td></td><td></td></tr><tr><td>NET_DVR_SET_VEHICLE_BLACKLST_SCHEDULE</td><td>NULL</td><td>BlackListScheduleList(XML 描述)</td></tr><tr><td>NET_DVR_SET_VEHICLE_BLACKLIST_EVENT_TRIGGER</td><td>NULL</td><td>EventTrigger(XML 描述)</td></tr><tr><td>NET_DVR_SET_VEHICLE_WHITELST_SCHEDULE</td><td>NULL</td><td>WhiteListScheduleList(XML 描述)</td></tr><tr><td></td><td></td><td></td></tr><tr><td>NET_DVR_SET_VEHICLE_WHITELIST_EVENT_TRIGGER</td><td>NULL</td><td>EventTrigger(XML 描述)</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVRSET_VEHICLE_ALLLIST_EVENT TRIGGER</td><td>NULL</td><td>EventTrigger(XML描述)</td></tr><tr><td>NETDVRSETVEHICLEOTHERLISTEVENTTRIGGER</td><td>NULL</td><td>EventTrigger(XML描述)</td></tr><tr><td>其他参数配置</td><td></td><td></td></tr><tr><td>NETDVRSETREGION_CLIP</td><td>NETDVRREGIONCLIPCOND</td><td>NETDVRREGION_CLIP_CFG</td></tr><tr><td>NET_DVR_SET_LITESTORAGE</td><td>4字节(DWORD)通道号</td><td>NETDVRLITESTORAGE</td></tr></table></body></html>  

### 批量参数配置  

### 5.14.5 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.45[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.46[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.46），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.46 所示。  

表 5.45 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_VCA_CTRLINFO_CFG</td><td>获取智能控制参数</td><td>5022</td></tr><tr><td>NET_DVR_GET_GUARDCFG</td><td>获取车牌识别检测计划</td><td>3134</td></tr><tr><td>NET_DVR_GET_ROI_DETECT_NUM</td><td>获取ROI检测区域编号数目</td><td>3349</td></tr><tr><td>NET_DVR_GET_ROI_DETECT</td><td>获取ROI检测区域配置</td><td>3350</td></tr><tr><td>NET_DVR_GET_FACE_DETECT</td><td>获取人脸侦测配置</td><td>3352</td></tr><tr><td>NET_DVR_GET_SCENECHANGE_DETECTIONCFG</td><td>获取场景变更报警配置</td><td>3356</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_GET_TRAVERSE_PLANE_DETECTION</td><td>获取越界侦测配置</td><td>3360</td></tr><tr><td>NET_DVR_GET_FIELD_DETECTION</td><td>获取区域侦测配置</td><td>3362</td></tr><tr><td>NET_DVR_GET_DEFOCUSPARAM</td><td>获取虚焦侦测参数配置</td><td>3364</td></tr><tr><td>NET_DVR_GET_AUDIOEXCEPTIONPARAM</td><td>获取音频异常配置</td><td>3366</td></tr><tr><td>NET_DVR_GET_PDC_RULECFG_V42</td><td>获取客流量统计规则</td><td>3405</td></tr><tr><td>NET_DVR_GET_HEATMAP_CFG</td><td>获取热度图参数配置</td><td>3407</td></tr><tr><td>NET_DVR_GET_CLOUDSTORAGE_CFG</td><td>获取云存储配置参数</td><td>5058</td></tr><tr><td>NET_ITS_GET_OVERLAP_CFG</td><td>获取字符叠加参数配置</td><td>5072</td></tr><tr><td>NET_DVR_GET_TRIGGEREX_CFG</td><td>获取触发模式配置</td><td>5074</td></tr><tr><td>NET_DVR_GET_SNAPINFO_CFG_V40</td><td>获取抓拍图片参数扩展</td><td>3138</td></tr><tr><td>NET_DVR_GET_MONITOR_LOCATION_INFO</td><td>获取监测点信息</td><td>3424</td></tr></table></body></html>  

表 5.46 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>lplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_VCA_CTRLINFO_CFG</td><td>dwCount 个 NET_DVR_VCA_CTRLINFO_COND</td><td>dwCount 个 NET_DVR_VCA_CTRLINFO_CFG</td></tr><tr><td>NET_DVR_GET_GUARDCFG</td><td>dwCount 个 NET_DVR_GUARD_COND</td><td>dwCount 个 NET_DVR_GUARD_CFG</td></tr><tr><td>NET_DVR_GET_ROI_DETECT_NUM</td><td>dwCount个</td><td>dwCount 个 NET_DVR_ROI_DETECT_NUM</td></tr><tr><td>NET_DVR_GET_ROI_DETECT</td><td>NET_DVR_MUL_STREAM_CHANNEL_GROUP dwCount 个 NET_DVR_ROI_DETECT_COND</td><td>dwCount 个 NET_DVR_ROI_DETECT_CFG</td></tr><tr><td></td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount 个 NET_DVR_DETECT_FACE</td></tr><tr><td>NET_DVR_GET_FACE_DETECT NET_DVR_GET_SCENECHANGE_DETECTIONCFG</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount 个</td></tr><tr><td></td><td></td><td>NET_DVR_SCENECHANGE_DETECTION</td></tr><tr><td>NET_DVR_GET_TRAVERSE_PLANE_DETECTION</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount 个 NET_VCA_TRAVERSE_PLANE_DETECTION</td></tr><tr><td>NET_DVR_GET_FIELD_DETECTION</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount 个 NET_VCA_FIELDDETECION</td></tr><tr><td>NET_DVR_GET_DEFOCUSPARAM</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount 个 NET_VCA_DEFOCUSPARAM</td></tr><tr><td>NET_DVR_GET_AUDIOEXCEPTIONPARAM</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount 个 NET_DVR_AUDIO_EXCEPTION</td></tr><tr><td>NET_DVR_GET_PDC_RULECFG_V42</td><td>dwCount 个 NET_DVR_PDC_RULE_COND</td><td>dwCount 个 NET_DVR_PDC_RULE_CFG_V42</td></tr><tr><td>NET_DVR_GET_HEATMAP_CFG</td><td>dwCount 个 NET_DVR_HEATMAP_COND</td><td>dwCount 个 NET_DVR_HEATMAP_CFG</td></tr><tr><td>NET_DVR_GET_CLOUDSTORAGE_CFG</td><td>dwCount 个 NET_DVR_CLOUDSTORAGE_COND</td><td>dwCount 个 NET_DVR_CLOUDSTORAGE_CFG</td></tr><tr><td>NET_ITS_GET_OVERLAP_CFG</td><td>dwCount 个 NET_ITS_OVERLAPCFG_COND</td><td>dwCount 个 NET_ITS_OVERLAP_CFG</td></tr><tr><td>NET_DVR_GET_TRIGGEREX_CFG</td><td>dwCount 个 NET_DVR_TRIGGER_COND</td><td>dwCount 个 NET_ITC_TRIGGERCFG</td></tr><tr><td>NET_DVR_GET_SNAPINFO_CFG_V40</td><td>dwCount 个 NET_DVR_SNAPINFO_COND</td><td>dwCount 个 NET_DVR_SNAPINFOCFG</td></tr><tr><td>NET_DVR_GET_MONITOR_LOCATION_INFO</td><td>dwCount个</td><td>dwCount个</td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td>NET_DVR_MONITOR_LOCATION_COND</td><td>NET_DVR_MONITOR_LOCATION_CFG</td></tr></table></body></html>  

### 5.14.6 批量设置配置信息 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.47[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.48[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.48），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的获取功能对应不同的结构体和命令号，如表 5.48 所示。  

表 5.47 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_VCA_CTRLINFO_CFG</td><td>设置智能控制参数</td><td>5023</td></tr><tr><td>NET_DVR_SET_GUARDCFG</td><td>设置车牌识别检测计划</td><td>3135</td></tr><tr><td>NET_DVR_SET_ROI_DETECT</td><td>设置 ROI检测区域配置</td><td>3351</td></tr><tr><td>NET_DVR_SET_FACE_DETECT</td><td>设置人脸侦测配置</td><td>3353</td></tr><tr><td>NET_DVR_SET_SCENECHANGE_DETECTIONCFG</td><td>设置场景变更报警配置</td><td>3357</td></tr><tr><td>NET_DVR_SET_TRAVERSE_PLANE_DETECTION</td><td>设置越界侦测配置</td><td>3361</td></tr><tr><td>NET_DVR_SET_FIELD_DETECTION</td><td>设置区域侦测配置</td><td>3363</td></tr><tr><td>NET_DVR_SET_DEFOCUSPARAM</td><td>设置虚焦侦测参数配置</td><td>3365</td></tr><tr><td>NET_DVR_SET_AUDIOEXCEPTIONPARAM</td><td>设置音频异常配置</td><td>3367</td></tr><tr><td>NET_DVR_SET_PDC_RULECFG_V42</td><td>设置客流量统计规则</td><td>3406</td></tr><tr><td>NET_DVR_SET_HEATMAP_CFG</td><td>设置热度图参数配置</td><td>3408</td></tr><tr><td>NET_DVR_SET_CLOUDSTORAGE_CFG</td><td>设置云存储配置参数</td><td>5059</td></tr><tr><td>NET_ITS_SET_OVERLAP_CFG</td><td>设置字符叠加参数配置</td><td>5073</td></tr><tr><td>NET_DVR_SET_TRIGGEREX_CFG</td><td>设置触发模式配置</td><td>5075</td></tr></table></body></html>  

<html><body><table><tr><td>NETDVRSETSNAPINFOCFGV40</td><td>设置抓拍图片参数扩展</td><td>3139</td></tr><tr><td>NET_DVR_SET_MONITOR_LOCATION_INFO</td><td>设置监测点信息</td><td>3425</td></tr></table></body></html>  

表 5.48 批量设置设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>IplnParamBuffer对应结构体</td></tr><tr><td>NET_DVR_SET_VCA_CTRLINFO_CFG</td><td>dwCount 个 NET_DVR_VCA_CTRLINFO_COND</td><td>dwCount 个 NET_DVR_VCA_CTRLINFO_CFG</td></tr><tr><td>NET_DVR_SET_GUARDCFG</td><td>dwCount 个 NET_DVR_GUARD_COND</td><td>dwCount 个 NET_DVR_GUARD_CFG</td></tr><tr><td>NET_DVR_SET_ROI_DETECT</td><td>dwCount 个 NET_DVR_ROI_DETECT_COND</td><td>dwCount 个 NET_DVR_ROI_DETECT_CFG</td></tr><tr><td>NET_DVR_SET_FACE_DETECT</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount 个 NET_DVR_DETECT_FACE</td></tr><tr><td>NET_DVR_SET_SCENECHANGE_DETECTIONCFG</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount个</td></tr><tr><td>NET_DVR_SET_TRAVERSE_PLANE_DETECTION</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>NET_DVR_SCENECHANGE_DETECTION dwCount 个</td></tr><tr><td>NET_DVR_SET_FIELD_DETECTION</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>NET_VCA_TRAVERSE_PLANE_DETECTION</td></tr><tr><td>NET_DVR_SET_DEFOCUSPARAM</td><td></td><td>dwCount 个 NET_VCA_FIELDDETECION dwCount 个 NET_VCA_DEFOCUSPARAM</td></tr><tr><td>NET_DVR_SET_AUDIOEXCEPTIONPARAM</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td></td></tr><tr><td>NET_DVR_SET_PDC_RULECFG_V42</td><td>dwCount 个 NET_DVR_CHANNEL_GROUP</td><td>dwCount 个 NET_DVR_AUDIO_EXCEPTION</td></tr><tr><td></td><td>dwCount 个 NET_DVR_PDC_RULE_COND</td><td>dwCount 个 NET_DVR_PDC_RULE_CFG_V42</td></tr><tr><td>NET_DVR_SET_HEATMAP_CFG</td><td>dwCount 个 NET_DVR_HEATMAP_COND</td><td>dwCount 个 NET_DVR_HEATMAP_CFG</td></tr><tr><td>NET_DVR_SET_CLOUDSTORAGE_CFG</td><td>dwCount 个 NET_DVR_CLOUDSTORAGE_COND</td><td>dwCount 个 NET_DVR_CLOUDSTORAGE_CFG</td></tr><tr><td>NET_ITS_SET_OVERLAP_CFG</td><td>dwCount 个 NET_ITS_OVERLAPCFG_COND</td><td>dwCount 个 NET_ITS_OVERLAP_CFG</td></tr><tr><td>NET_DVR_SET_TRIGGEREX_CFG</td><td>dwCount 个 NET_DVR_TRIGGER_COND</td><td>dwCount 个 NET_ITC_TRIGGERCFG</td></tr><tr><td>NET_DVR_SET_SNAPINFO_CFG_V40</td><td>dwCount 个 NET_DVR_SNAPINFO_COND</td><td>dwCount 个 NET_DVR_SNAPINFOCFG</td></tr><tr><td>NET_DVR_SET_MONITOR_LOCATION_INFO</td><td>dwCount 个</td><td>dwCount 个</td></tr><tr><td></td><td>NET_DVR_MONITOR_LOCATION_COND</td><td>NET_DVR_MONITOR_LOCATION_CFG</td></tr></table></body></html>  

### 长连接参数配置  

### 5.14.7 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 配置命令，详见表 5.49[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.49[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORD  

### dwBufLen, void \*pUserData)  

[out] dwType 配置状态，详见表 5.50  
[out] lpBuffer 存放数据的缓冲区指针，具体内容跟 dwType 相关，详见表 5.50  
[out] dwBufLen 缓冲区大小  
[out] pUserData 用户数据  

返回值： -1 表示失败，其他值作为 NET_DVR_GetNextRemoteConfig、NET_DVR_StopRemoteConfig 的句柄。获取错误码调用 NET_DVR_GetLastError。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.49 所示。对于客流量数据、热度图、人员统计信息查找功能，该接口指定了要查找的信息，调用成功后，需要调用 NET_DVR_GetNextRemoteConfig 接口来逐个获取信息。查询智能规则关联的颜色参数时，接口里面需要设置回调函数，查询结果直接在回调里面返回。  

表 5.49 长连接参数配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td><td>回调函数</td></tr><tr><td>NETDVRGETHEATMAPRESULT</td><td>5083</td><td>热度图数据查找</td><td>NETDVRHEATMAPQUERYCOND</td><td>NULL</td></tr><tr><td>NET_DVR_GET_PDC_RESULT</td><td>5089</td><td>客流量数据查询</td><td>NET_DVR_GET_PDC_RESULT</td><td>NULL</td></tr><tr><td>NETDVRFACECAPTURESTATISTICS</td><td>3715</td><td>长连接人员统计查询</td><td>NETDVRFACECAPTURESTATISTICS_COND</td><td>NULL</td></tr><tr><td>NET_DVR_GET_VCA_RULE_COLOR_CFG</td><td>410</td><td>智能规则关联的颜色 参数查询</td><td>NET_DVR_VCA_RULE_COLOR_COND</td><td>返回状态、 信息数据</td></tr></table></body></html>  

表 5.50 回调参数内容  


<html><body><table><tr><td>dwType</td><td>dwType值</td><td>含义</td><td>IpBuffer对应内容</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_STATUS</td><td>0</td><td>状态值</td><td>typedef enum NET_SDK_CALLBACK_STATUS_SUCCESS=1000,//成功 NET_SDK_CALLBACK_STATUS_PROCESSING,//处理中</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_PROGRESS</td><td></td><td></td><td>NET_SDK_CALLBACK_STATUS_FAILED//失败 NET_SDK_CALLBACK_STATUS_NORMAL;</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_DATA</td><td>1 2</td><td>进度值 信息数据</td><td>IpBuffer的值表示进度 lpBuffer的值表示信息数据 智能规则关联的颜色参数查询结果对应结构体：</td></tr></table></body></html>  

### 5.14.8 逐个获取查找到的信息 NET_DVR_GetNextRemoteConfig  

函  数： LONG NET_DVR_GetNextRemoteConfig(LONG lHandle, void \*lpOutBuff, DWORD dwOutBuffSize)  

参  数： [in] lHandle 查找句柄，NET_DVR_StartRemoteConfig 的返回值[out] lpOutBuff 输出数据缓冲区，与 NET_DVR_StartRemoteConfig 的命令（dwCommand）有关，详见表 5.52[out] dwOutBuffSize 缓冲区长度  
返回值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.51。获取错误码调用NET_DVR_GetLastError。  

表 5.51 长连接参数获取状态  


<html><body><table><tr><td>宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_SUCCESS</td><td>1000</td><td>成功读取到数据，处理完本次数据后需要再次调用 NET_DVR_GetNextRemoteConfig获取下一条数据</td></tr><tr><td>NET_SDK_GET_NETX_STATUS_NEED_WAIT</td><td>1001</td><td>需等待设备发送数据，继续调用 NET_DVR_GetNextRemoteConfig</td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_FINISH</td><td>1002</td><td>数据全部取完，可调用NET_DVR_StopRemoteConfig 结束长连接</td></tr><tr><td>NET_SDK_GET_NEXT_STATUSFAILED</td><td>1003</td><td>出现异常，可调用NET_DVR_StopRemoteConfig 结束长 连接</td></tr></table></body></html>  

说  明：  

调用 NET_DVR_StartRemoteConfig 时传入不同的命令号(dwCommand)，lpOutBuff 对应不同的结构体，如表 5.52 所示。在调用该接口获取查找之前，必须先调用 NET_DVR_StartRemoteConfig得到当前的查找句柄。此接口用于获取一条已查找到的信息，若要获取全部的已查找到的信息，需要循环调用此接口。  

表 5.52 长连接参数获取  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>lpOutBuff</td></tr><tr><td>NETDVRGET HEATMAP RESULT</td><td>5083</td><td>热度图数据查找</td><td>NET DVRHEATMAP INFO</td></tr><tr><td>NET DVRGETPDCF RESULT</td><td>5089</td><td>客流量数据查询</td><td>NETD DVRPDC RESULT</td></tr><tr><td>NETDVRFACECAPTURESTATISTICS</td><td>3715</td><td>人脸抓拍人员统计查询</td><td>NET DVRFACECAPTURESTATISTICSRESULT</td></tr></table></body></html>  

### 返回目录  

### 5.14.9 关闭长连接配置 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。说  明： 关闭长连接配置接口所创建的句柄，释放资源。  

### 远程控制  

### 5.14.10 远程控制(标准协议) NET_DVR_STDControl  

函  数： BOOL NET_DVR_STDControl(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONTROLlpControlParam)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.53[in&out]lpControlParam 远程控制输入输出参数  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 对于不同的配置功能（dwCommand），lpControlParam 中的 lpCondBuffer 对应不同的内容，详  

见表 5.53。  

表 5.53 控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>dwCommand含义</td><td>lpCondBuffer</td></tr><tr><td>NETDVRREMOVEFLASHSTORAGE</td><td>3756</td><td>客流数据清除操作</td><td>NETDVRFLASHSTORAGEREMOVE</td></tr></table></body></html>  

### 文件上传下载  

### 5.14.11 上传文件 NET_DVR_UploadFile_V40  

函  数： LONG NET_DVR_UploadFile_V40(LONG lUserID, DWORD dwUploadType, LPVOID lpInBuffer,DWORD dwInBufferSize, char \*sFileName, LPVOID lpOutBuffer, DWORD dwOutBufferSize)  

参  数： [in] lUserID NET_DVR_Login_V40 的返回值[in] dwUploadType 上传文件类型，详见表 5.54[in] lpInBuffer 不同的 dwUploadType，输入参数不同，详见表 5.54[in] dwInBufferSize 输入缓冲区大小[in] sFileName 上传文件的绝对路径（包括文件名）[out] lpOutBuffer 输出参数，不同的 dwUploadType，输出参数不同，详见表 5.54[in] dwInBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.54 文件上传类型  


<html><body><table><tr><td>dwUploadType宏定义</td><td>宏定义值</td><td>dwUploadType含义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td></td><td>13</td><td>上传授权或非授权名单配置 文件功能</td><td>NULL</td><td>NULL</td></tr></table></body></html>  

### 返回目录  

### 5.14.12 获取文件上传的进度和状态 NET_DVR_GetUploadState  

函  数： LONG NET_DVR_GetUploadState(LONG lUploadHandle,LPDWORD pProgress)  
参  数： [in] lUploadHandle 文件上传的句柄，NET_DVR_UploadFile 的返回值[out] pProgress 返回的进度值，取值范围： $0^{\sim}100$   
返回值： -1 表示函数调用失败，其他为上传的状态值：1- 上传成功；2- 正在上传；3- 上传失败；4- 网络断开，状态未知；6- 硬盘错误；7- 无审讯文件存放盘；8- 容量不足；9- 设备资源不足；10-文件个数超过 40；19- 文件格式不正确；20- 文件内容不正确。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.14.13 停止文件上传 NET_DVR_UploadClose  

函  数： BOOL NET_DVR_UploadClose(LONG lUploadHandle)  

参  数： [in] lUploadHandle 文件上传的句柄，NET_DVR_UploadFile 的返回值返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.14.14 开始下载文件 NET_DVR_StartDownload  

函  数： LONG NET_DVR_StartDownload(LONG lUserID, DWORD dwDownloadType, LPVOID lpInBuffer,DWORD dwInBufferSize, char const \*sFileName)  

参  数： [in] lUserID 用户 ID，NET_DVR_Login_V40 的返回值[in] dwDownloadType 下载文件类型，详见表 5.55[in] lpInBuffer 输入参数。不同的 dwUploadType，输入参数不同，详见表 5.55[in] dwInBufferSize 输入缓冲区大小[in] sFileName 下载文件的保存路径（绝对路径，包括文件名）  

返回值： -1 表示失败，其他值作为 NET_DVR_StopDownload 和 NET_DVR_GetDownloadState 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.55 文件下载类型  


<html><body><table><tr><td>dwDownloadType</td><td>取值</td><td>含义</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET_SDK_DOWNLOAD_VEHICLE_BLACKWHITELST_FILE</td><td>8</td><td>下载授权或非授权名单配 置文件</td><td>NULL</td></tr></table></body></html>  

### 返回目录  

### 5.14.15 获取文件下载的进度和状态 NET_DVR_GetDownloadState  

函  数： LONG NET_DVR_GetDownloadState(LONG lDownloadHandle, LPDWORD pProgress)  

参  数： [in] lDownloadHandle 文件下载的句柄，NET_DVR_StartDownload 的返回值[out] pProgress 返回的进度值，取值范围： $0^{\sim}100$   
返回值： -1 表示函数调用失败，其他为下载的状态值：1- 下载成功；2- 正在下载；3- 下载失败；4- 网络断开，状态未知。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.14.16 停止文件下载 NET_DVR_StopDownload  

函  数： BOOL NET_DVR_StopDownload(LONG lHandle);  
参  数： [in] lHandle 文件下载的句柄，NET_DVR_StartDownload 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.15长连接参数配置  

### 5.15.1 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 配置命令，详见表 5.56[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.56[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

[out] dwType 配置状态，获取音量时 dwType 状态无效，其他命令对应取值：enum _NET_SDK_CALLBACK_TYPE_{NET_SDK_CALLBACK_TYPE_STATUS $=0_{\scriptscriptstyle-}$ , //回调状态值NET_SDK_CALLBACK_TYPE_PROGRESS, //回调进度值NET_SDK_CALLBACK_TYPE_DATA //回调数据内容}NET_SDK_CALLBACK_TYPE  

[out] lpBuffer 存放数据的缓冲区指针，NET_DVR_START_GET_INPUTVOLUME获取音量时 lpBuffer 对应 4 字节声音强度，其他命令对应取值详见表 5.57  
[out] dwBufLen 缓冲区大小  
[out] pUserData 用户数据  

返回值： -1 表示失败，其他值作为 NET_DVR_StopRemoteConfig 的句柄。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.56 长连接参数配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td><td>cbStateCallback</td></tr><tr><td>NETDVRSTARTGET INPUTVOLUME</td><td>3370</td><td>开始获取音量</td><td>NET DVRINPUTVOLUME</td><td>返回状态、信息数据</td></tr><tr><td>NETDVRGETCONNECTLIST</td><td>433</td><td>获取 Wifi 热点连 接设备列表信息</td><td>NETDVRCONNECTDEV_COND</td><td>返回状态、信息数据</td></tr></table></body></html>  

表 5.57 长连接回调数据  


<html><body><table><tr><td>dwType</td><td>含义</td><td>IpBuffer对应内容</td></tr><tr><td rowspan="5">NET_SDK_CALLBACK_TYPE_STATUS</td><td>状态值</td><td>typedefenum{</td></tr><tr><td></td><td>NET_SDK_CALLBACK_STATUS_SUCCESS=1000,//成功</td></tr><tr><td></td><td>NET_SDK_CALLBACK_STATUS_PROCESSING,//处理中</td></tr><tr><td></td><td>NET_SDK_CALLBACK_STATUS_FAILED//失败</td></tr><tr><td></td><td>}NET_SDK_CALLBACK_STATUS_NORMAL;</td></tr></table></body></html>  

<html><body><table><tr><td>NETSDKCALLBACKTYPEPROGRESS</td><td>进度值</td><td>lpBuffer的值表示进度（DWORD）</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_DATA</td><td>信息数据</td><td>NET_DVR_GET_CONNECT_LIST时，对应结构体：NET_DVR_CONNECTDEV_CFG</td></tr></table></body></html>  

### 返回目录  

### 5.15.2 关闭长连接配置 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。说  明： 关闭长连接配置接口所创建的句柄，释放资源。  

## 5.16远程控制  

### 5.16.1 远程控制 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.58[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.58[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.58 所示。  

表 5.58 远程配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>lplnBuffer对应结构体</td></tr><tr><td>NET_DVR_REMOTECONTROLALARM</td><td>3205</td><td>远程控制遥控器布防</td><td>NET_DVR_REMOTECONTROL_ALARM_PARAM</td></tr><tr><td>NET_DVR_REMOTECONTROL_DISALARM</td><td>3206</td><td>远程控制遥控器撤防</td><td>NETDVRREMOTECONTROLALARMPARAM</td></tr><tr><td>NET_DVR_REMOTECONTROL_STUDY</td><td>3207</td><td>远程控制遥控器学习</td><td>NET_DVR_REMOTECONTROL_STUDY_PARAM</td></tr><tr><td>NET_DVR_WIRELESS_ALARM_STUDY</td><td>3208</td><td>远程控制无线报警学习</td><td>NET_DVR_WIRELESS_ALARM_STUDY_PARAM</td></tr><tr><td>NET_DVR_WPS_CONNECT</td><td>3220</td><td>远程启用WPS连接</td><td>NET_DVR_WPS_CONNECT_PARAM</td></tr><tr><td>NET_DVRUPDATE_PIN</td><td>3223</td><td>更新设备PIN码</td><td>NULL</td></tr></table></body></html>  

### 返回目录  

### 5.16.2 远程控制(标准协议) NET_DVR_STDControl  

函  数： BOOL NET_DVR_STDControl(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONTROLlpControlParam)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.59  

[in&out]lpControlParam 远程控制输入输出参数返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对于不同的配置功能（dwCommand），lpControlParam 中的 lpCondBuffer 对应不同的内容，详见表 5.59。  

表 5.59 控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>dwCommand含义</td><td>IpCondBuffer</td></tr><tr><td>NETDVRWIRELESSDIALCONNECT</td><td>3593</td><td>控制无线网络连网断网</td><td>NETDVRWIRELESSDIALCONNECT_PARAM</td></tr><tr><td>NETDVRTHSCREENTIMING</td><td>3737</td><td>温湿度屏幕校时</td><td>NULL</td></tr></table></body></html>  

设备是否支持温湿度能力，可以通过设备能力集进行判断，对应温湿度配置能力集(THScreen)，相关接口：NET_DVR_GetSTDAbility，能力集类型：NET_DVR_GET_THSCREEN_CAPABILITIES。  

## 5.17 证书管理  

证书创建、删除  

### 5.17.1 远程控制 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.60[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.60[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.60 所示。  

表 5.60 远程配置命令  


<html><body><table><tr><td>dwCommand 宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET DVR_CREATE_CERT</td><td>6138</td><td>创建证书</td><td>NETD DVR_CERT_INFO</td></tr><tr><td>NET DVR_D DELETE_CERT</td><td>6139</td><td>删除证书</td><td>NET_D DVR_CERT PARAM</td></tr></table></body></html>  

### 证书信息获取  

### 5.17.2 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORD  

dwOutBufferSize)参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.61[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.61[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.61），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.61 所示。  

表 5.61 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>IplnBuffer对应结构体</td><td>IpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_CERT</td><td>获取证书信息</td><td>dwCount个NET_DVR_CERT_PARAM</td><td>dwCount个NET_DVR_CERT_INFO</td><td>6142</td></tr></table></body></html>  

### 证书上传下载  

### 5.17.3 上传文件 NET_DVR_UploadFile_V40  

函  数： LONG NET_DVR_UploadFile_V40(LONG lUserID, DWORD dwUploadType, LPVOID lpInBuffer,DWORD dwInBufferSize, char \*sFileName, LPVOID lpOutBuffer, DWORD dwOutBufferSize)  

参  数： [in] lUserID NET_DVR_Login_V40 的返回值[in] dwUploadType 上传文件类型，详见表 5.62[in] lpInBuffer 不同的 dwUploadType，输入参数不同，详见表 5.62[in] dwInBufferSize 输入缓冲区大小[in] sFileName 上传文件的绝对路径（包括文件名）[out] lpOutBuffer 输出参数，不同的 dwUploadType，输出参数不同，详见表 5.62[in] dwInBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.62 文件上传类型  


<html><body><table><tr><td>dwUploadType宏定义</td><td>宏定义值</td><td>含义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>UPLOADCERTIFICATE</td><td>1</td><td>上传证书(WIFI、HTTPS 等）</td><td>NETDVRCERTPARAM</td><td>NULL</td></tr></table></body></html>  

### 返回目录  

### 5.17.4 获取文件上传的进度和状态 NET_DVR_GetUploadState  

函  数： LONG NET_DVR_GetUploadState(LONG lUploadHandle,LPDWORD pProgress)  
参  数： [in] lUploadHandle 文件上传的句柄，NET_DVR_UploadFile 的返回值[out] pProgress 返回的进度值，取值范围： $0^{\sim}100$   
返回值： -1 表示函数调用失败，其他为上传的状态值：1- 上传成功；2- 正在上传；3- 上传失败；4- 网络断开，状态未知；6- 硬盘错误；7- 无审讯文件存放盘；8- 容量不足；9- 设备资源不足；10-文件个数超过 40；19- 文件格式不正确；20- 文件内容不正确。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 返回目录  

### 5.17.5 停止文件上传 NET_DVR_UploadClose  

函  数： BOOL NET_DVR_UploadClose(LONG lUploadHandle)  
参  数： [in] lUploadHandle 文件上传的句柄，NET_DVR_UploadFile 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.17.6 开始下载文件 NET_DVR_StartDownload  

函  数： LONG NET_DVR_StartDownload(LONG lUserID, DWORD dwDownloadType, LPVOID lpInBuffer,DWORD dwInBufferSize, char const \*sFileName)  

参  数： [in] lUserID 用户 ID，NET_DVR_Login_V40 的返回值[in] dwDownloadType 下载文件类型，详见表 5.63[in] lpInBuffer 输入参数。不同的 dwUploadType，输入参数不同，详见表 5.63[in] dwInBufferSize 输入缓冲区大小[in] sFileName 下载文件的保存路径（绝对路径，包括文件名）  

返回值： -1 表示失败，其他值作为 NET_DVR_StopDownload 和 NET_DVR_GetDownloadState 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.63 文件下载类型  


<html><body><table><tr><td>dwDownloadType</td><td>宏定义值</td><td>含义</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET_SDK_DOWNLOAD_CERT</td><td>0</td><td>下载证书</td><td>NET_DVR_CERT_PARAM</td></tr></table></body></html>  

### 5.17.7 获取文件下载的进度和状态 NET_DVR_GetDownloadState  

函  数： LONG NET_DVR_GetDownloadState(LONG lDownloadHandle, LPDWORD pProgress)  
参  数： [in] lDownloadHandle 文件下载的句柄，NET_DVR_StartDownload 的返回值[out] pProgress 返回的进度值，取值范围： $0^{\sim}100$   
返回值： -1 表示函数调用失败，其他为下载的状态值：1- 下载成功；2- 正在下载；3- 下载失败；4- 网络断开，状态未知。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.17.8 停止文件下载 NET_DVR_StopDownload  

函  数： BOOL NET_DVR_StopDownload(LONG lHandle);  
参  数： [in] lHandle 文件下载的句柄，NET_DVR_StartDownload 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.18存储管理  

### 5.18.1 获取设备参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.64 所示。  

表 5.64 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET DVRGET NFSCFG</td><td>获取 NFS(网络文件系统)参数</td><td>无效</td><td>NETDVRNFSCFG</td><td>230</td></tr><tr><td>NET DVRGETHDCFG</td><td>获取硬盘管理参数</td><td>无效</td><td>NETDVRHDCFG</td><td>1054</td></tr><tr><td>NET DVRGETNETDISKCFGV40</td><td>获取网络硬盘接入参数(扩展)</td><td>无效</td><td>NETDVR RNET DISKCFGV40</td><td>3392</td></tr></table></body></html>  

### 返回目录  

### 5.18.2 设置设备参数 NET_DVR_SetDVRConfig  

函  数： BOOL  NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.65 所示。  

表 5.65 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRSET NFSCFG</td><td>设置NFS(网络文件系统)参数</td><td>无效</td><td>NETDVRNFSCFG</td><td>231</td></tr><tr><td>NET_DVR_SET_HDCFG</td><td>设置硬盘管理参数</td><td>无效</td><td>NET_DVR_HDCFG</td><td>1055</td></tr><tr><td>NETDVRSETNET DISKCFGV40</td><td>设置网络硬盘接入参数(扩展)</td><td>无效</td><td>NETDVRNET DISKCFGV40</td><td>3393</td></tr></table></body></html>  

### 返回目录  

### 5.18.3 获取设备参数 NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.66[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.66  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.66所示。  

表 5.66 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IpCondBuffer</td><td>IpOutBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_GETSTORAGEDETECTION_EVENT_TRIGGER</td><td>获取存储健康检测联动配4字节(DWORD)NET_DVR_EVENT_TRIGGER 置</td><td>硬盘号</td><td></td><td>6635</td></tr><tr><td>NET_DVR_GET_STORAGEDETECTION_SCHEDULE</td><td>间配置</td><td>硬盘号</td><td>获取存储健康检测布防时4字节(DWORD)NET_DVR_EVENT_SCHEDULE</td><td>6638</td></tr><tr><td>NET_DVR_GET_STORAGEDETECTION_STATE</td><td>获取存储健康状态</td><td>NULL</td><td>NETDVRSTORAGEDETECTION</td><td>6640</td></tr><tr><td>NET_DVR_GET_STORAGEDETECTION_RWLOCK</td><td>获取存储侦测读写锁配置</td><td>NULL</td><td>NET_DVRSTORAGE_RWLOCK</td><td>6646</td></tr></table></body></html>  

### 5.18.4 设置设备参数 NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.67[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.67  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.67 所示。  

表 5.67 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IpCondBuffer</td><td>IplnBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVRSET_STORAGEDETECTION_EVENT_TRIGGER</td><td>设置存储健康检测联动配 置</td><td>NULL</td><td>NETDVREVENTTRIGGER</td><td>6636</td></tr><tr><td>NET_DVR_SET_STORAGEDETECTION_SCHEDULE</td><td>间配置</td><td>硬盘号</td><td>设置存储健康检测布防时4字节(DWORD）NET_DVR_EVENT_SCHEDULE</td><td>6639</td></tr><tr><td>NETDVRSETSTORAGEDETECTIONRWLOCK</td><td>设置存储侦测读写锁配置</td><td>NULL</td><td>NETDVRSTORAGERWLOCK</td><td>6648</td></tr><tr><td>NETDVRSETSTORAGEDETECTIONUNLOCK</td><td>设置存储侦测解锁配置</td><td>NULL</td><td>NETDVRSTORAGEUNLOCK</td><td>6653</td></tr></table></body></html>  

### 返回目录  

### 5.18.5 远程格式化设备硬盘 NET_DVR_FormatDisk  

函  数： LONG NET_DVR_FormatDisk(LONG lUserID, LONG lDiskNumber)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lDiskNumber 硬盘号，从 0 开始，0xff 表示对所有硬盘有效（不包括只读硬盘）  
返回值： -1 表示失败，其他值作为 NET_DVR_CloseFormatHandle 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 格式化过程中如果网络断了，设备上的格式化操作依然会继续，但是客户端无法收到状态。  

返回目录  

### 5.18.6 获取格式化硬盘的进度 NET_DVR_GetFormatProgress  

函  数： BOOL NET_DVR_GetFormatProgress(LONG lFormatHandle, LONG \*pCurrentFormatDisk,LONG\*pCurrentDiskPos,LONG \*pFormatStatic)  
参  数： [in]lFormatHandle 格式化硬盘句柄，NET_DVR_FormatDisk 的返回值[out]pCurrentFormatDisk 指向保存当前正在格式化的硬盘号的指针，硬盘号从 0 开始，-1为初始状态[out] pCurrentDiskPos 指向保存当前正在格式化的硬盘的进度的指针，进度是 $0{\sim}100$ [out] FormatStatic 指向保存硬盘格式化状态的指针：0- 正在格式化；  

1- 硬盘全部格式化完成；2- 格式化当前硬盘出错，不能继续格式化此硬盘，本地和网络硬盘都会出现此错误；3- 由于网络异常造成网络硬盘丢失而不能开始格式化当前硬盘返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.18.7 关闭格式化硬盘句柄，释放资源 NET_DVR_CloseFormatHandle  

函  数： BOOL NET_DVR_CloseFormatHandle(LONG lFormatHandle)  
参  数： [in]lFormatHandle 格式化硬盘句柄，NET_DVR_FormatDisk 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.19布防、撤防  

设置报警等信息上传的回调函数  

### 5.19.1 注册报警消息回调函数 NET_DVR_SetDVRMessageCallBack_V31  

函  数： BOOL NET_DVR_SetDVRMessageCallBack_V31(MSGCallBack fMessageCallBack, void\* pUser)  

参  数： [in]fMessageCallBack 报警信息回调函数[in]pUser 用户数据typedef BOOL (CALLBACK\* MSGCallBack_V31)(LONG lCommand, NET_DVR_ALARMER \*pAlarmer,char \*pAlarmInfo, DWORD dwBufLen, void \*pUser)  

[out]lCommand 上传的消息类型，详见表 5.68  
[out]pAlarmer 报警设备信息，详见结构体：NET_DVR_ALARMER  
[out]pAlarmInfo 报警信息，详见表 5.69  
[out]dwBufLen 报警信息缓存大小  
[out]pUser 用户数据  

表 5.68 报警信息类型  


<html><body><table><tr><td>ICommand宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>COMM_ALARM</td><td>0x1100</td><td>V3.0以下版本支持的设备的报警信息上传</td></tr><tr><td>COMM_ALARM_RULE</td><td>0x1102</td><td>异常行为识别信息上传</td></tr><tr><td>COMM_ALARM_PDC</td><td>0x1103</td><td>客流量统计报警上传</td></tr><tr><td>COMMUPLOADFACESNAPRESULT</td><td>0x1112</td><td>人脸抓拍结果上传</td></tr><tr><td>COMM_FACECAPTURE_STATISTICS_RESULT</td><td>0x112a</td><td>人脸抓拍人员统计上传</td></tr></table></body></html>  

<html><body><table><tr><td>COMM_ALARM_FACE_DETECTION</td><td>0x4010</td><td>人脸侦测报警上传</td></tr><tr><td>COMM_PEOPLE_DETECTION_UPLOAD</td><td>0x4014</td><td>人员侦测信息上传</td></tr><tr><td>COMM_SCENECHANGE_DETECTION_UPLOAD</td><td>0x1130</td><td>场景变更报警上传</td></tr><tr><td>COMM_ALARM_AUDIOEXCEPTION</td><td>0x1150</td><td>声音报警信息上传</td></tr><tr><td>COMM_ALARM_DEFOCUS</td><td>0x1151</td><td>虚焦报警信息上传</td></tr><tr><td>COMM_IPC_AUXALARM_RESULT</td><td>0x2820</td><td>PIR报警、无线报警、呼救报警上传</td></tr><tr><td>COMM_ITS_PLATE_RESULT</td><td>0x3050</td><td>交通抓拍识别结果上传</td></tr><tr><td>COMM_UPLOAD_HEATMAP_RESULT</td><td>0x4008</td><td>热度图报警上传</td></tr><tr><td>COMM_FIREDETECTION_ALARM</td><td>0x4991</td><td>火点检测报警上传</td></tr><tr><td>COMM_GISINFO_UPLOAD</td><td>0x4012</td><td>GIS 信息上传</td></tr><tr><td>COMM_VANDALPROOF_ALARM</td><td>0x4013</td><td>电子罗盘防破坏报警信息上传</td></tr><tr><td>COMM_ALARM_STORAGE_DETECTION</td><td>0x4015</td><td>存储智能检测报警信息</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中回调函数的第一个参数（lCommand）和第三个参数（pAlarmInfo）是密切关联的，其关系见表 5.69。  

表 5.69 报警信息结构  


<html><body><table><tr><td>消息类型（ICommand）</td><td>上传内容</td><td>pAlarmlnfo对应的结构体</td></tr><tr><td>COMM_ALARM</td><td>设备报警信息</td><td>NET_DVR_ALARMINFO</td></tr><tr><td>COMM_ALARM_RULE</td><td>异常行为识别信息</td><td>NET_VCA_RULE_ALARM</td></tr><tr><td>COMM_ALARM_PDC</td><td>客流量统计报警信息</td><td>NET_DVR_PDC_ALRAM_INFO</td></tr><tr><td>COMM_UPLOAD_FACESNAP_RESULT</td><td>人脸抓拍结果信息</td><td>NET_VCA_FACESNAP_RESULT</td></tr><tr><td>COMM_FACECAPTURE_STATISTICS_RESULT</td><td>人脸抓拍人员统计信息</td><td>NET_DVR_FACECAPTURE_STATISTICS_RESULT</td></tr><tr><td>COMM_ALARM_FACE_DETECTION</td><td>人脸侦测报警信息</td><td>NET_DVR_FACE_DETECTION</td></tr><tr><td>COMM_PEOPLE_DETECTION_UPLOAD</td><td>人员侦测信息</td><td>NET_DVR_PEOPLE_DETECTION_RESULT</td></tr><tr><td>COMM_SCENECHANGE_DETECTION_UPLOAD</td><td>场景变更报警信息</td><td>NET_DVR_SCENECHANGE_DETECTION_RESULT</td></tr><tr><td>COMM_ALARM_AUDIOEXCEPTION</td><td>声音报警信息</td><td>NET_DVR_AUDIOEXCEPTION_ALARM</td></tr><tr><td>COMM_ALARM_DEFOCUS</td><td>虚焦报警信息</td><td>NET_DVR_DEFOCUS_ALARM</td></tr><tr><td>COMM_IPC_AUXALARM_RESULT</td><td>PIR报警、无线报警、呼救报警信息</td><td>NET_IPC_AUXALARM_RESULT</td></tr><tr><td>COMM_ITS_PLATE_RESULT</td><td>交通抓拍识别结果上传</td><td>NET_ITS_PLATE_RESULT</td></tr><tr><td>COMM_UPLOAD_HEATMAP_RESULT</td><td>热度图报警信息</td><td>NET_DVR_HEATMAP_RESULT</td></tr><tr><td>COMM_FIREDETECTION_ALARM</td><td>火点检测报警信息</td><td>NET_DVR_FIREDETECTION_ALARM</td></tr><tr><td>COMM_GISINFO_UPLOAD</td><td>GIS 信息</td><td>NET_DVR_GIS_UPLOADINFO</td></tr><tr><td>COMM_VANDALPROOF_ALARM</td><td>防破坏报警信息</td><td>NET_DVR_VANDALPROOF_ALARM</td></tr><tr><td>COMM_ALARM_STORAGE_DETECTION</td><td>存储智能检测报警信息</td><td>NET_DVR_STORAGE_DETECTION_ALARM</td></tr></table></body></html>  

### 布防撤防  

### 5.19.2 建立报警上传通道，获取报警等信息 NET_DVR_SetupAlarmChan_V41  

函  数： LONG NET_DVR_SetupAlarmChan_V41(LONG lUserID, LPNET_DVR_SETUPALARM_PARAMlpSetupParam)  
参  数： [in] lUserID NET_DVR_Login_V40 的返回值[in] lpSetupParam 报警布防参数，详见结构体：NET_DVR_SETUPALARM_PAR  

返回值： -1 表示失败，其他值作为 NET_DVR_CloseAlarmChan_V30 函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 使用该接口支持上传 V3.0 以上版本支持的设备的报警结构。启动布防前，需要调用注册回调函数的接口（如 NET_DVR_SetDVRMessageCallBack_V30）才能获取到上传的报警等信息。  

返回目录  

### 5.19.3 撤销报警上传通道 NET_DVR_CloseAlarmChan_V30  

函  数： BOOL NET_DVR_CloseAlarmChan_V30(LONG lAlarmHandle)  
参  数： [in]lAlarmHandle NET_DVR_SetupAlarmChan_V41 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.20 监听报警  

### 5.20.1 启动监听，接收设备主动上传的报警等信息 NET_DVR_StartListen_V30  

函  数： LONG NET_DVR_StartListen_V30(char \*sLocalIP, WORD wLocalPort, MSGCallBack DataCallback, void\*pUserData $=$ NULL)  
参  数： [in]sLocalIP PC 机本地 IP 地址，可以置为 NULL[in]wLocalPort PC 本地监听端口号。由用户设置，必须和设备端设置的一致[in]DataCallback 回调函数[in]pUserData 用户数据typedef void(CALLBACK \*MSGCallBack)(LONG lCommand,NET_DVR_ALARMER \*pAlarmer,char\*pAlarmInfo,DWORD dwBufLen,void \*pUser)[out]lCommand 上传的消息类型，详见表 5.70[out]pAlarmer 报警设备信息，详见结构体：NET_DVR_ALARMER[out]pAlarmInfo 报警信息，详见表 5.71[out]dwBufLen 报警信息缓存大小[out]pUser 用户数据  

表 5.70 报警信息类型  


<html><body><table><tr><td>ICommand宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>COMM_ALARM</td><td>0x1100</td><td>V3.0以下版本支持的设备的报警信息上传</td></tr><tr><td>COMM_ALARM_RULE</td><td>0x1102</td><td>异常行为识别信息上传</td></tr><tr><td>COMM_ALARM_PDC</td><td>0x1103</td><td>客流量统计报警上传</td></tr><tr><td>COMM_UPLOAD_FACESNAP_RESULT</td><td>0x1112</td><td>人脸抓拍结果上传</td></tr><tr><td>COMM_SCENECHANGE_DETECTION_UPLOAD</td><td>0x1130</td><td>场景变更报警上传</td></tr><tr><td>COMM_ALARM_AUDIOEXCEPTION</td><td>0x1150</td><td>声音报警信息上传</td></tr><tr><td>COMM_ALARM_DEFOCUS</td><td>0x1151</td><td>虚焦报警信息上传</td></tr><tr><td>COMM_IPC_AUXALARM_RESULT</td><td>0x2820</td><td>PIR 报警、无线报警、呼救报警上传</td></tr><tr><td>COMM_UPLOAD_HEATMAP_RESULT</td><td>0x4008</td><td>热度图报警上传</td></tr><tr><td>COMM_ALARM_FACE_DETECTION</td><td>0x4010</td><td>人脸侦测报警上传</td></tr></table></body></html>  

返回值： -1 表示失败，其他值作为 NET_DVR_CloseAlarmChan_V30 函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中回调函数的第一个参数（lCommand）和第三个参数（pAlarmInfo）是密切关联的，其关系见表 5.71。  

 SDK 最大能支持 512 路监听。  
 要使 PC 能够收到设备主动发过来的报警等信息，必须将设备的网络配置中的“远程管理主机地址”或者“远程报警主机地址”设置成 PC 机的 IP 地址（与接口中的 sLocalIP 参数一致），“远程管理主机端口号”或者“远程报警主机端口号”设置成 PC 机的监听端口号（与接口中的wLocalPort 参数一致）。  
 该接口中的回调函数优先级高于其他回调函数，即设置了该接口中的回调函数，其他回调函数将接收不到报警信息。  

表 5.71 报警信息结构  


<html><body><table><tr><td>消息类型（ICommand）</td><td>上传内容</td><td>pAlarmlnfo对应的结构体</td></tr><tr><td>COMM_ALARM</td><td>设备报警信息</td><td>NET_DVR_ALARMINFO</td></tr><tr><td>COMM_ALARM_RULE</td><td>异常行为识别信息</td><td>NET_VCA_RULE_ALARM</td></tr><tr><td>COMM_ALARM_PDC</td><td>客流量统计报警信息</td><td>NET_DVR_PDC_ALRAM_INFO</td></tr><tr><td>COMM_UPLOAD_FACESNAP_RESULT</td><td>人脸抓拍结果信息</td><td>NET_VCA_FACESNAP_RESULT</td></tr><tr><td>COMM_SCENECHANGE_DETECTION_UPLOAD</td><td>场景变更报警信息</td><td>NET_DVR_SCENECHANGE_DETECTION_RESULT</td></tr><tr><td>COMM_ALARM_AUDIOEXCEPTION</td><td>声音报警信息</td><td>NET_DVR_AUDIOEXCEPTION_ALARM</td></tr><tr><td>COMM_ALARM_DEFOCUS</td><td>虚焦报警信息</td><td>NET_DVR_DEFOCUS_ALARM</td></tr><tr><td>COMM_IPC_AUXALARM_RESULT</td><td>PIR报警、无线报警、呼救报警信息</td><td>NET_IPCAUXALARM_RESULT</td></tr><tr><td>COMM_UPLOAD_HEATMAP_RESULT</td><td>热度图报警信息</td><td>NET_DVR_HEATMAP_RESULT</td></tr><tr><td>COMM_ALARM_FACE_DETECTION</td><td>人脸侦测报警信息</td><td>NET_DVR_FACE_DETECTION</td></tr></table></body></html>  

### 5.20.2 停止监听（支持多线程） NET_DVR_StopListen_V30  

函  数： BOOL NET_DVR_StopListen_V30(LONG lListenHandle)  
参  数： [in]lListenHandle 监听句柄，NET_DVR_StartListen_V30 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.21录像文件回放、下载、锁定及备份  

### 录像文件的查找  

### 5.21.1 根据文件类型、时间查找设备录像文件 NET_DVR_FindFile_V40  

函  数： LONG NET_DVR_FindFile_V40(LONG lUserID,LPNET_DVR_FILECOND_V40 pFindCond)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]pFindCond 待查找的文件信息结构，包括通道号、文件类型、时间等信息，详见结构体：NET_DVR_FILECOND_V40  

返回值： -1 表示失败，其他值作为 NET_DVR_FindClose 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口指定了要查找的录像文件的信息，调用成功后，就可以调用 NET_DVR_FindNextFile_V40接口来获取文件信息。  

### 5.21.2 逐个获取查找到的文件信息 NET_DVR_FindNextFile_V40  

函  数： LONG NET_DVR_FindNextFile_V40(LONG lFindHandle, LPNET_DVR_FINDDATA_V40 lpFindData)  
参  数： [in]lFindHandle 文件查找句柄，NET_DVR_FindFile_V40 的返回值[in]lpFindData 保存查找到的文件信息的指针，包括文件名、文件时间、文件类型等，详见结构体：NET_DVR_FILECOND_V40  

返回值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.72。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

表 5.72 查找状态信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_FILE_SUCCESS</td><td>1000</td><td>获取文件信息成功</td></tr><tr><td>NET_DVR_FILE_NOFIND</td><td>1001</td><td>未查找到文件</td></tr><tr><td>NET_DVR_ISFINDING</td><td>1002</td><td>正在查找请等待</td></tr><tr><td>NET_DVR_NOMOREFILE</td><td>1003</td><td>没有更多的文件，查找结束</td></tr><tr><td>NETDVRFILEEXCEPTION</td><td>1004</td><td>查找文件时异常</td></tr></table></body></html>  

说  明： 在调用该接口获取查找文件之前，必须先调用 NET_DVR_FindFile_V40 得到当前的查找句柄。此接口用于获取一条已查找到的文件信息，若要获取全部的已查找到的文件信息，需要循环调用此接口。通过此接口可以同时获取到与当前录像文件相关的卡号信息和文件是否被锁定的信息。每次可查询文件最大个数为 4000。  

### 5.21.3 关闭文件查找，释放资源 NET_DVR_FindClose_V30  

函  数： BOOL NET_DVR_FindClose_V30(LONG lFindHandle)  
参  数： [in]lFindHandle 文件查找句柄，NET_DVR_FindFile_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 回放录像文件  

### 5.21.4 按文件名回放录像文件 NET_DVR_PlayBackByName  

函  数： LONG NET_DVR_PlayBackByName(LONG lUserID,char \*sPlayBackFileName, HWND hWnd)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sPlayBackFileName 回放的文件名，长度不能超过 100 字节[in]hWnd 回放的窗口句柄，若置为空，SDK 仍能收到码流数据，但不解码显示  

返回值： -1 表示失败，其他值作为 NET_DVR_StopPlayBack 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

：  该接口指定了当前要播放的录像文件，调用成功后，还必须调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现回放。 在调用该接口成功后，可以通过接口 NET_DVR_SetPlayDataCallBack 注册回调函数，捕获录像的码流数据并自行处理。  

### Linux 下：  

 Linux 64 位系统不支持软解码功能，因此需要将窗口句柄传空，设置回调函数，只取流不解码显示。  
 对于 4.1 或者以上的版本的 SDK，HWND 表示播放窗口的句柄，定义为：typedef unsigned int HWND;如果使用 Qt 进行界面开发，示例如下：NET_DVR_CLIENTINFO tmpclientinfo;QWidget m_framePlayWnd;tmpclientinfo.hPlayWnd $=$ (HWND)m_framePlayWnd.GetPlayWndId();  
 对于 4.1 以前的版本的 SDK，HWND 定义如下：typedef struct __PLAYRECT{int $\mathbf{x};$ //显示框左上角横坐标int y; //显示框左上角纵坐标  

int uWidth; //显示框宽度int uHeight; //显示框高度}PLAYRECT;typedef PLAYRECT HWND;NET_DVR_CLIENTINFO 结构中的 hPlayWnd $=\{0\}$ 则 SDK 仍取流，不进行解码显示，所以仍可以录像，但是不能设置 hPlayWnd $=01$ (即 NULL)，否则非法结构地址会导致调用 hPlayWnd.x 等去判断的时候崩溃。  

### 5.21.5 按时间回放录像文件 NET_DVR_PlayBackByTime_V40  

函  数： LONG NET_DVR_PlayBackByTime_V40(LONG lUserID, LPNET_DVR_VOD_PARA pVodPara)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]pVodPara 回放参数，包括回放的通道、起止时间、窗口句柄等，详见结构体：NET_DVR_VOD_PARA  

返回值： -1 表示失败，其他值作为 NET_DVR_StopPlayBack 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  该接口指定了当前要播放的录像文件，调用成功后，还必须调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现回放。当回放的是按事件搜索出的录像文件时，由于每个文件都会有预录和延迟的部分，因此在设置本接口的开始和结束时间参数时可以适当提前开始时间和延长结束时间。建议值：最多 10 分钟，最少 5 秒。 在调用该接口成功后，可以通过接口 NET_DVR_SetPlayDataCallBack 注册回调函数，捕获录像的码流数据并自行处理。  

### 5.21.6 控制录像回放的状态 NET_DVR_PlayBackControl_V40  

函  数： BOOL NET_DVR_PlayBackControl_V40(LONG lPlayHandle, DWORD dwControlCode, LPVOIDlpInBuffer, DWORD dwInLen, LPVOID lpOutBuffer, DWORD \*lpOutLen)  

参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值[in]dwControlCode 控制录像回放状态命令，详见表 5.73[in] lpInBuffer 指向输入参数的指针，详见表 5.74[in]dwInLen 输入参数的长度。未使用，保留。[out]lpOutBuffer 指向输出参数的指针，详见表 5.74[out]lpOutLen 输出参数的长度  

表 5.73 回放控制命令  


<html><body><table><tr><td>dwControlCode宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>NET_DVR_PLAYSTART</td><td>1</td><td>开始播放</td></tr><tr><td>NET_DVR_PLAYPAUSE</td><td>3</td><td>暂停播放</td></tr><tr><td>NET_DVR_PLAYRESTART</td><td>4</td><td>恢复播放</td></tr><tr><td>NET_DVR_PLAYFAST</td><td>5</td><td>快放</td></tr><tr><td>NET_DVR_PLAYSLOW</td><td>6</td><td>慢放</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_PLAYNORMAL</td><td>7</td><td>正常速度播放(在暂停后调用将恢复暂停前的速度播放)</td></tr><tr><td>NET_DVR_PLAYFRAME</td><td>8</td><td>单帧放（恢复正常回放使用NET_DVR_PLAYNORMAL命令）</td></tr><tr><td>NET_DVR_PLAYSTARTAUDIO</td><td>9</td><td>打开声音</td></tr><tr><td>NET_DVR_PLAYSTOPAUDIO</td><td>10</td><td>关闭声音</td></tr><tr><td>NET_DVR_PLAYAUDIOVOLUME</td><td>11</td><td>调节音量，取值范围[0,Oxffff]</td></tr><tr><td>NET_DVR_PLAYSETPOS</td><td>12</td><td>改变文件回放的进度</td></tr><tr><td>NET_DVR_PLAYGETPOS</td><td>13</td><td>获取按文件或者按时间回放的进度</td></tr><tr><td>NET_DVR_PLAYGETTIME</td><td>14</td><td>获取当前已经播放的时间(按文件回放的时候有效)</td></tr><tr><td>NET_DVR_PLAYGETFRAME</td><td>15</td><td>获取当前已经播放的帧数(按文件回放的时候有效)</td></tr><tr><td>NET_DVR_GETTOTALFRAMES</td><td>16</td><td>获取当前播放文件总的帧数(按文件回放的时候有效)</td></tr><tr><td>NET_DVR_GETTOTALTIME</td><td>17</td><td>获取当前播放文件总的时间(按文件回放的时候有效)</td></tr><tr><td>NET_DVR_THROWBFRAME</td><td>20</td><td>丢B帧</td></tr><tr><td>NET_DVR_SETSPEED</td><td>24</td><td>设置码流速度</td></tr><tr><td>NET_DVR_KEEPALIVE</td><td>25</td><td>保持与设备的心跳(如果回调阻塞，建议2秒发送一次)</td></tr><tr><td>NET_DVR_SET_TRANS_TYPE</td><td>32</td><td>设置转封装类型</td></tr><tr><td>NET_DVR_PLAY_CONVERT</td><td>33</td><td>回放转码</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中的第三个参数是否需要输入数值与控制命令有关，详见表 5.74。  

 特别指出，当控制命令是开始播放（即 NET_DVR_PLAYSTART）时，第三个参数的值表示播放当前文件的偏移量，若该值为 0 表示从文件的起始位置播放，若该值不为 0 则表示断点续传的文件位置（Byte）。  
 该接口中的第五个参数表示当前控制命令操作所获取到的相应的参数，控制命令中的NET_DVR_PLAYGETPOS、NET_DVR_PLAYGETTIME、NET_DVR_PLAYGETFRAME、NET_DVR_GETTOTALFRAMES 和 NET_DVR_GETTOTALTIME 都能通过该参数得到对应的值，详见上表。  
 当命令值为 NET_DVR_PLAYGETPOS 时，获取文件回放或者下载进度时，0-100 表示正常的进度值，大于 100 的值表示回放或者下载异常；获取按时间回放或下载进度时，只能获取的进度值是 0、100（结束）、200（异常）。  
 NET_DVR_SET_TRANS_TYPE 设置转封装类型和 NET_DVR_PLAY_CONVERT 回放转码需要在开始播放（即 NET_DVR_PLAYSTART）之前调用。  

表 5.74 回放控制参数  


<html><body><table><tr><td>状态命令宏定义</td><td>状态命令说明</td><td>lplnBuf</td><td>IpOutBuf</td></tr><tr><td>NETDVRPLAYSTART</td><td>开始播放</td><td>一个4字节整型的偏移量</td><td>无</td></tr><tr><td>NET_DVRPLAYSETPOS</td><td>改变回放的进度</td><td>一个4字节整型的进度值（0-100）</td><td>无</td></tr><tr><td>NETDVRPLAYGETPOS</td><td>获取回放的进度</td><td>无</td><td>一个4字节整型的进度值 (0-100)</td></tr><tr><td>NETDVRPLAYGETTIME</td><td>获取当前已播放的时间 （按文件回放有效）</td><td>无</td><td>一个4字节整型的时间值</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_PLAYGETFRAME</td><td>获取当前已播放的帧数 (按文件回放有效)</td><td>无</td><td>一个4字节整型的帧数值</td></tr><tr><td>NETDVRGETTOTALFRAMES</td><td>获取当前播放文件总的帧 数 (按文件回放有效)</td><td>无</td><td>-个4字节整型的帧数值</td></tr><tr><td>NET_DVR_GETTOTALTIME</td><td>获取当前播放文件总的时 间 (按文件回放有效)</td><td>无</td><td>一个4字节整型的时间值</td></tr><tr><td>NET_DVR_THROWBFRAME</td><td>丢B帧</td><td>个4字节整型的B帧个数</td><td>无</td></tr><tr><td>NET_DVR_SETSPEED</td><td>设置码流速度</td><td>个4字节整型的速度值</td><td>无</td></tr><tr><td>NET_DVR_SET_TRANS_TYPE</td><td>设置转封装类型</td><td>-个4字节整型的转码类型：1-PS, 2-TS，3-RTP，5-MP4(3GPP，仅按文件 回放支持)</td><td>无</td></tr><tr><td>NET_DVR_PLAY_CONVERT</td><td>回放转码</td><td>NET_DVR_COMPRESSION_INFO_V30</td><td>无</td></tr></table></body></html>  

### 5.21.7 停止回放录像文件 NET_DVR_StopPlayBack  

函  数： BOOL NET_DVR_StopPlayBack(LONG lPlayHandle)  
参  数： [in]lPlayHandle 回放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 回放录像文件时的数据捕获  

### 5.21.8 捕获回放的录像数据，并保存成文件 NET_DVR_PlayBackSaveData  

函  数： BOOL  NET_DVR_PlayBackSaveData(LONG lPlayHandle,char \*sFileName)  
参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值[in]sFileName 保存数据的文件路径  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： V5.0.3.2 或以后版本，通过该接口保存录像，文件最大限制为 1024MB，大于 1024M 时，SDK 自动新建文件进行保存，文件开始将40 字节头自动写入，文件名命名规则为“在接口传入的文件名基础上增加数字标识(例如：\*_1.mp4、\*_2.mp4)”。  

返回目录  

### 5.21.9 停止保存录像数据 NET_DVR_StopPlayBackSave  

函  数： BOOL  NET_DVR_StopPlayBackSave(LONG lPlayHandle)  

参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.21.10 注册回调函数，捕获录像数据 NET_DVR_SetPlayDataCallBack_V40  

函  数： BOOL NET_DVR_SetPlayDataCallBack_V40(LONG lPlayHandle, fPlayDataCallBack cbPlayDataCallBack,void \*pUser)  

参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值[in]fPlayDataCallBack 录像数据回调函数[in] pUser 用户数据  

typedef void(CALLBACK \*fPlayDataCallBack_V40)(LONG lPlayHandle, DWORD dwDataType, BYTE \*pBuffer, DWORD dwBufSize, void \*pUser)  

[out]lPlayHandle 当前的录像播放句柄[out]dwDataType 数据类型，详见表 5.75[out]pBuffer 存放数据的缓冲区指针[out]dwBufSize 缓冲区大小[out]pUser 用户数据  

表 5.75 回放回调数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>1</td><td>系统头数据</td></tr><tr><td>NETDVRSTREAMDATA</td><td>2</td><td>流数据 （包括复合流或音视频分开的视频流数据）</td></tr></table></body></html>  

返回值：  

TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

 此函数包括开始和停止用户处理 SDK 捕获的数据，当回调函数 cbPlayDataCallBack 设为非 NULL值时，表示回调和处理数据；当设为 NULL 时表示停止回调和处理数据。回调的第一个包是40 个字节的文件头，供后续解码使用，之后回调的是压缩的码流。  
 cbPlayDataCallBack 回调函数中不能执行可能会占用时间较长的接口或操作，不建议调用该SDK（HCNetSDK.dll）本身的接口。  

### 回放的其他操作  

### 5.21.11 获取录像回放时显示的 OSD 时间 NET_DVR_GetPlayBackOsdTime  

函  数： BOOL NET_DVR_GetPlayBackOsdTime(LONG lPlayHandle, LPNET_DVR_TIME lpOsdTime)参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值  

[out]lpOsdTime 获取的 OSD 时间的指针，详见结构体：NET_DVR_TIME返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.21.12 录像回放时抓图，并保存在文件中 NET_DVR_PlayBackCaptureFile  

函  数： BOOL NET_DVR_PlayBackCaptureFile(LONG lPlayHandle,char \*sFileName)  
参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值[in]sFileName 保存图片数据的文件路径  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 回放时抓下来的图片时间要比抓图时间延后，这是因为预览画面上的 OSD 时间是解码完成的显示时间，而解码缓冲区会有将近 1M 左右的数据还没有解出来，要抓取的图片数据是网络缓冲里面的。目前解码库没有直接从解码缓冲区中取出数据的接口。  

返回目录  

### 5.21.13 刷新显示回放窗口 NET_DVR_RefreshPlay  

函  数： BOOL NET_DVR_RefreshPlay(LONG lPlayHandle)参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 当用户暂停或者单帧回放时，如果刷新了窗口，则窗口中的图像因为刷新而消失，此时调用这个接口可以重新显示最后一帧画面。此接口只在暂停和单帧播放时有效。  

返回目录  

### 5.21.14 获取回放解码显示的播放库句柄 NET_DVR_GetPlayBackPlayerIndex  

函  数： int NET_DVR_GetPlayBackPlayerIndex(LONG lPlayHandle)参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值返回值： -1 表示失败，其他值表示播放句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 用户可以通过返回的句柄自行实现播放库 SDK 提供的其他功能，详见本公司提供的软解码库函数说明《播放器 SDK 编程指南》。例如使用 PlayM4_GetBMP(LONG nPort,……)、PlayM4_GetJPEG(LONG nPort,……)这两个接口时，即可实现将当前预览图像以 BMP 或 JPEG 格式抓图保存到内存中：PlayM4_GetBMP(NET_DVR_GetRealPlayerIndex(),……)PlayM4_GetJPEG(NET_DVR_GetRealPlayerIndex(),……) 。  

### 下载录像文件  

### 5.21.15 按文件名下载录像文件 NET_DVR_GetFileByName  

函  数： LONG  NET_DVR_GetFileByName(LONG lUserID,char \*sDVRFileName,char \*sSavedFileName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sDVRFileName 要下载的录像文件名，文件名长度需小于 100 字节[in]sSavedFileName 下载后保存到 PC 机的文件路径，需为绝对路径  
返回值： -1 表示失败，其他值作为 NET_DVR_StopGetFile 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在使用该接口下载录像文件前，可以先调用录像文件查找的接口获取文件名。该接口指定了当前要下载的录像文件，调用成功后，还需要调用 NET_DVR_PlayBackControl_V40 接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现下载。  

返回目录  

### 5.21.16 按时间下载录像文件 NET_DVR_GetFileByTime_V40  

函  数： LONG NET_DVR_GetFileByTime_V40(LONG lUserID, char \*sSavedFileName, LPNET_DVR_PLAYCONDpDownloadCond)  
参  数： [in] lUserID 用户 ID，NET_DVR_Login_V40 的返回值[in] sSavedFileName 下载后保存到 PC 机的文件路径，需为绝对路径，包括文件名[in] pDownloadCond 下载条件，包括通道号、起止时间等，详见结构体：NET_DVR_PLAYCOND  

返回值： -1 表示失败，其他值作为 NET_DVR_StopGetFile 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： $\bullet$ 该接口指定了当前要下载的录像文件，调用成功后，还需要调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现下载。 V5.0.3.2 或以后版本，通过该接口保存录像，文件最大限制为 1024MB，大于 1024M 时，SDK自动新建文件进行保存，文件开始将 40 字节头自动写入，文件名命名规则为“在接口传入的文件名基础上增加数字标识(例如：\*_1.mp4、\*_2.mp4)”。  

返回目录  

### 5.21.17 控制录像下载的状态 NET_DVR_PlayBackControl_V40  

函  数： BOOL NET_DVR_PlayBackControl_V40(LONG lPlayHandle, DWORD dwControlCode, LPVOIDlpInBuffer, DWORD dwInLen, LPVOID lpOutBuffer, DWORD \*lpOutLen)  

参  数： [in]lPlayHandle 下载句柄，NET_DVR_GetFileByName 或NET_DVR_GetFileByTime_V40 的返回值[in]dwControlCode 控制录像下载状态命令，详见表 5.76[in] lpInBuffer 指向输入参数的指针，详见表 5.77[in]dwInLen 输入参数的长度[out]lpOutBuffer 指向输出参数的指针，详见表 5.77[out]lpOutLen 输出参数的长度  

表 5.76 下载控制命令  


<html><body><table><tr><td>dwControlCode宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_PLAYSTART</td><td>1</td><td>开始下载</td></tr><tr><td>NET_DVR_PLAYPAUSE</td><td>3</td><td>暂停下载</td></tr><tr><td>NET_DVR_PLAYRESTART</td><td>4</td><td>恢复下载</td></tr><tr><td>NET_DVR_PLAYSETPOS</td><td>12</td><td>改变文件下载的进度 (按文件下载时有效)</td></tr><tr><td>NET_DVR_PLAYGETPOS</td><td>13</td><td>获取文件下载的进度 (按文件下载时有效)</td></tr><tr><td>NET_DVR_GETTOTALFRAMES</td><td>16</td><td>获取当前下载文件总的帧数(按文件下载时有效)</td></tr><tr><td>NET_DVR_GETTOTALTIME</td><td>17</td><td>获取当前下载文件总的时间(按文件下载时有效)</td></tr><tr><td>NET_DVR_SETSPEED</td><td>24</td><td>设置下载速度，速度单位：kbps，最小为 256kbps，最大为 设备带宽</td></tr><tr><td>NET_DVR_SET_TRANS_TYPE</td><td>32</td><td>设置转封装类型</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中的第三个参数是否需要输入数值与控制命令有关，详见表 5.77。  

 当控制命令是开始下载（即 NET_DVR_PLAYSTART）时，第三个参数的值表示下载当前文件的偏移量，若该值为0 表示从文件的起始位置下载，若该值不为0 则表示断点续传的文件位置（Byte）。断点续传需要设备支持。  
 当命令值为 NET_DVR_PLAYGETPOS 时，获取文件回放或者下载进度时，0-100 表示正常的进度值，大于 100 的值表示回放或者下载异常。  
 按时间下载时，只能获取进度值：0、100（结束）、200（异常）。  
 NET_DVR_SET_TRANS_TYPE 设置转封装类型需在开始播放（即 NET_DVR_PLAYSTART）之前调用。  

表 5.77 下载控制参数  


<html><body><table><tr><td>状态命令宏定义</td><td>状态命令说明</td><td>IplnBuf</td><td>IpOutBuf</td></tr><tr><td>NET_DVR_PLAYSTART</td><td>开始下载</td><td>个4字节整型的偏移量</td><td>无</td></tr><tr><td>NET_DVR_PLAYSETPOS</td><td>改变下载的进度</td><td>个4字节整型的进度值（0-100）</td><td>无</td></tr><tr><td>NET_DVR_PLAYGETPOS</td><td>获取下载的进度</td><td>无</td><td>个4字节整型的进度值（0-100)</td></tr><tr><td>NET_DVR_GETTOTALFRAMES</td><td>获取当前下载文件总的帧 数（按文件回放有效）</td><td>无</td><td>个4字节整型的帧数值</td></tr><tr><td>NET_DVR_GETTOTALTIME</td><td>获取当前下载文件总的时 间 (按文件回放有效)</td><td>无</td><td>-个4字节整型的时间值</td></tr><tr><td>NET_DVR_SETSPEED</td><td>设置下载速度</td><td>个4字节整型的速度值</td><td>无</td></tr><tr><td>NET_DVR_SET_TRANS_TYPE</td><td>设置转封装类型</td><td>个4字节整型的转码类型： 1-PS，2-TS,3-RTP,5-MP4(3GPP, 仅按文件回放支持)</td><td>无</td></tr></table></body></html>  

### 5.21.18 停止下载录像文件 NET_DVR_StopGetFile  

函  数： BOOL NET_DVR_StopGetFile(LONG lFileHandle)  
参  数： [in]lFileHandle 下载句柄，NET_DVR_GetFileByName 或NET_DVR_GetFileByTime_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.21.19 获取当前下载录像文件的进度 NET_DVR_GetDownloadPos  

函  数： int NET_DVR_GetDownloadPos(LONG lFileHandle)  
参  数： [in]lFileHandle 下载句柄，NET_DVR_GetFileByName 或NET_DVR_GetFileByTime_V40 的返回值  
返回值： -1 表示失败； $0{\sim}100$ 表示下载的进度；100 表示下载结束；正常范围 0-100，如返回 200 表明出现网络异常。获取错误码调用 NET_DVR_GetLastError。  
说  明： 该接口用于获取按文件名下载录像文件时的下载进度。  

### 录像文件锁定和解锁  

### 5.21.20 按文件名锁定录像文件 NET_DVR_LockFileByName  

函  数： BOOL NET_DVR_LockFileByName(LONG lUserID, char \*sLockFileName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sLockFileName 要锁定的录像文件名，文件名长度需小于 100 字节  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在使用该接口锁定录像文件前，可以先调用录像文件查找的接口获取文件名。当文件被锁定后，将不会被覆盖。  

### 5.21.21 按文件名解锁录像文件 NET_DVR_UnlockFileByName  

函  数： BOOL NET_DVR_UnlockFileByName(LONG lUserID, char \*sUnlockFileName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sUnlockFileName 要解锁的录像文件名  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在使用该接口锁定录像文件前，可以先调用录像文件查找的接口获取文件名。  

## 5.22 图片的查找、回放下载  

查找图片  

### 5.22.1 根据类型和时间查找图片 NET_DVR_FindPicture  

函  数： LONG NET_DVR_FindPicture(LONG lUserID, NET_DVR_FIND_PICTURE_PARAM\* pFindParam)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]pFindParam 图片查找条件信息  
返回值： -1 表示失败，其他值作为 NET_DVR_CloseFindPicture 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口指定了要查找的图片的类型和查找时间范围，调用成功后，就可以调用NET_DVR_FindNextPicture 接口来获取图片信息。注：该接口查找的是设备本地的图片，可通过NET_DVR_SetDVRConfig 配置设备的抓图计划（NET_DVR_SCHED_CAPTURECFG）。  

返回目录  

### 5.22.2 逐个获取查找到的图片 NET_DVR_FindNextPicture_V40  

函  数： LONG NET_DVR_FindNextPicture_V40(LONG lFindHandle,LPNET_DVR_FIND_PICTURE_V40lpFindData)  

参  数： [in]lFindHandle 图片查找句柄，NET_DVR_FindPicture 的返回值[out]lpFindData 保存图片信息的指针  

返回值： -1 表示失败，其他值表示当前的获取状态等信息，如表 5.78 所示。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

表 5.78 查找状态信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>NET_DVR_FILE_SUCCESS</td><td>1000</td><td>获取图片信息成功</td></tr><tr><td>NET_DVR_FILE_NOFIND</td><td>1001</td><td>未查找到图片</td></tr><tr><td>NET_DVRISFINDING</td><td>1002</td><td>正在查找请等待</td></tr><tr><td>NET_DVR_NOMOREFILE</td><td>1003</td><td>没有更多的图片，查找结束</td></tr><tr><td>NET_DVR_FILE_EXCEPTION</td><td>1004</td><td>查找图片时异常</td></tr></table></body></html>  

说  明： 在调用该接口获取查找图片之前，必须先调用 NET_DVR_FindPicture 得到当前的查找句柄。此接口用于获取一条已查找到的图片信息，若要获取全部的已查找到的图片信息，需要循环调用此接口。  

### 5.22.3 关闭图片查找，释放资源 NET_DVR_CloseFindPicture  

函  数： BOOL NET_DVR_CloseFindPicture(LONG lFindHandle)参  数： [in]lFindHandle 图片查找句柄，NET_DVR_FindPicture 的返回值返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通  

过错误码判断出错原因。  

说  明：  

### 回放（下载）图片  

### 5.22.4 图片回放 NET_DVR_GetPicture_V30  

函  数： BOOL NET_DVR_GetPicture_V30(LONG lUserID, char \*sDVRFileName, char \*sSavedFileBuf, DWORDdwBufLen, DWORD \*lpdwRetLen)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sDVRFileName 图片名称[in]sSavedFileName 保存图片的缓冲区[in]dwBufLen 缓冲区大小[out]lpdwRetLen 实际收到的数据长度指针，不能为 NULL  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 图片为 JPEG 格式，数据保存在缓冲区 sSavedFileName 中，回放显示需要应用层实现。  

## 5.23云台控制  

### 云台控制操作  

### 5.23.1 云台控制操作（需先启动图像预览）NET_DVR_PTZControl  

函  数： BOOL NET_DVR_PTZControl(LONG lRealHandle,DWORD dwPTZCommand,DWORD dwStop)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwPTZCommand 云台控制命令，详见表 5.79[in]dwStop 云台停止动作或开始动作：0- 开始，1- 停止返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对云台实施的每一个动作都需要调用该接口两次，分别是开始和停止控制，由接口中的最后一个参数（dwStop）决定。在调用此接口之前需要先开启预览。与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。云台默认以最大速度动作。  

表 5.79 云台控制命令  


<html><body><table><tr><td>dwPTZCommand宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>LIGHT_PWRON</td><td>2</td><td>接通灯光电源</td></tr><tr><td>WIPER_PWRON</td><td>3</td><td>接通雨刷开关</td></tr><tr><td>FAN_PWRON</td><td>4</td><td>接通风扇开关</td></tr><tr><td>HEATER_PWRON</td><td>５</td><td>接通加热器开关</td></tr><tr><td>AUX_PWRON1</td><td>6</td><td>接通辅助设备开关</td></tr><tr><td>AUX_PWRON2</td><td>7</td><td>接通辅助设备开关</td></tr><tr><td>ZOOM_IN</td><td>11</td><td>焦距变大(倍率变大)</td></tr><tr><td>ZOOM_OUT</td><td>12</td><td>焦距变小(倍率变小)</td></tr><tr><td>FOCUS_NEAR</td><td>13</td><td>焦点前调</td></tr><tr><td>FOCUS_FAR</td><td>14</td><td>焦点后调</td></tr><tr><td>IRIS_OPEN</td><td>15</td><td>光圈扩大</td></tr><tr><td>IRIS_CLOSE</td><td>16</td><td>光圈缩小</td></tr><tr><td>TILT_UP</td><td>21</td><td>云台上仰</td></tr><tr><td>TILT_DOWN</td><td>22</td><td>云台下俯</td></tr><tr><td>PAN_LEFT</td><td>23</td><td>云台左转</td></tr><tr><td>PAN_RIGHT</td><td>24</td><td>云台右转</td></tr><tr><td>UP_LEFT</td><td>25</td><td>云台上仰和左转</td></tr><tr><td>UP_RIGHT</td><td>26</td><td>云台上仰和右转</td></tr><tr><td>DOWN_LEFT</td><td>27</td><td>云台下俯和左转</td></tr><tr><td>DOWN_RIGHT</td><td>28</td><td>云台下俯和右转</td></tr><tr><td>PAN_AUTO</td><td>29</td><td>云台左右自动扫描</td></tr><tr><td>TILT_DOWN_ZOOM_IN</td><td>58</td><td>云台下俯和焦距变大(倍率变大)</td></tr><tr><td>TILT_DOWN_ZOOM_OUT</td><td>59</td><td>云台下俯和焦距变小(倍率变小)</td></tr><tr><td>PAN_LEFT_ZOOM_IN</td><td>60</td><td>云台左转和焦距变大(倍率变大)</td></tr><tr><td>PAN_LEFT_ZOOM_OUT</td><td>61</td><td>云台左转和焦距变小(倍率变小)</td></tr><tr><td>PAN_RIGHT_ZOOM_IN</td><td>62</td><td>云台右转和焦距变大(倍率变大)</td></tr><tr><td>PAN_RIGHT_ZOOM_OUT</td><td>63</td><td>云台右转和焦距变小(倍率变小)</td></tr><tr><td>UP_LEFT_ZOOM_IN</td><td>64</td><td>云台上仰和左转和焦距变大(倍率变大)</td></tr><tr><td>UP_LEFT_ZOOM_OUT</td><td>65</td><td>云台上仰和左转和焦距变小(倍率变小)</td></tr><tr><td>UP_RIGHT_ZOOM_IN</td><td>66</td><td>云台上仰和右转和焦距变大(倍率变大)</td></tr><tr><td>UP_RIGHT_ZOOM_OUT</td><td>67</td><td>云台上仰和右转和焦距变小(倍率变小)</td></tr><tr><td>DOWN_LEFT_ZOOM_IN</td><td>68</td><td>云台下俯和左转和焦距变大(倍率变大)</td></tr><tr><td>DOWN_LEFT_ZOOM_OUT</td><td>69</td><td>云台下俯和左转和焦距变小(倍率变小)</td></tr></table></body></html>  

<html><body><table><tr><td>DOWNRIGHTZOOMIN</td><td>70</td><td>云台下俯和右转和焦距变大(倍率变大)</td></tr><tr><td>DOWNRIGHTZOOMOUT</td><td>71</td><td>云台下俯和右转和焦距变小(倍率变小)</td></tr><tr><td>TILT_UP_ZOOM_IN</td><td>72</td><td>云台上仰和焦距变大(倍率变大)</td></tr><tr><td>TILTUPZOOMOUT</td><td>73</td><td>云台上仰和焦距变小(倍率变小)</td></tr></table></body></html>  

### 5.23.2 云台控制操作（不用启动图像预览）NET_DVR_PTZControl_Other  

函  数： BOOL NET_DVR_PTZControl_Other(LONG lUserID,LONG lChannel,DWORD dwPTZCommand,DWORDdwStop)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZCommand 云台控制命令，详见表 5.79[in]dwStop 云台停止动作或开始动作：0- 开始；1- 停止返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对云台实施的每一个动作都需要调用该接口两次，分别是开始和停止控制，由接口中的最后一个参数（dwStop）决定。在调用此接口之前需要先注册设备。与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。云台默认以最大速度动作。  

### 5.23.3 带速度的云台控制操作（需先启动图像预览）  

NET_DVR_PTZControlWithSpeed  

函  数： BOOL NET_DVR_PTZControlWithSpeed(LONG lRealHandle, DWORD dwPTZCommand, DWORDdwStop, DWORD dwSpeed)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in] dwPTZCommand 云台控制命令，详见表 5.79[in]dwStop 云台停止动作或开始动作：0- 开始；1- 停止[in]dwSpeed 云台控制的速度，用户按不同解码器的速度控制值设置。取值范围[1,7]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

### 5.23.4 带速度的云台控制操作（不用启动图像预览）  

NET_DVR_PTZControlWithSpeed_Other  

函  数： BOOL NET_DVR_PTZControlWithSpeed(LONG lUserID, LONG lChannel, DWORD dwPTZCommand,  

DWORD dwStop, DWORD dwSpeed)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZCommand 云台控制命令，详见表 5.79[in]dwStop 云台停止动作或开始动作：0- 开始，1- 停止[in]dwSpeed 云台控制的速度，用户按不同解码器的速度控制值设置。取值范围：[1,7]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对云台实施的每一个动作都需要调用该接口两次，分别是开始和停止控制，由接口中的最后一个参数（dwStop）决定。在调用此接口之前不需要先开启预览，登录设备后即可实现控制。与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

### 云台预置点操作  

### 5.23.5 云台预置点操作，需先启动预览 NET_DVR_PTZPreset  

函  数： BOOL NET_DVR_PTZPreset(LONG lRealHandle,DWORD dwPTZPresetCmd,DWORD dwPresetIndex)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwPTZPresetCmd 操作云台预置点命令，详见表 5.80[in]dwPresetIndex 预置点的序号（从 1 开始），最多支持 255 个预置点  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

表 5.80 预置点操作命令  


<html><body><table><tr><td>dwPTZPresetCmd宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>SET_PRESET</td><td>8</td><td>设置预置点</td></tr><tr><td>CLE PRESET</td><td>9</td><td>清除预置点</td></tr><tr><td>GOTOPRESET</td><td>39</td><td>转到预置点</td></tr></table></body></html>  

### 5.23.6 云台预置点操作 NET_DVR_PTZPreset_Other  

函  数： BOOL NET_DVR_PTZPreset_Other(LONG lUserID,LONG lChannel,DWORD dwPTZPresetCmd,DWORDdwPresetIndex))  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  

[in]lChannel 通道号[in]dwPTZPresetCmd 操作云台预置点命令，详见表 5.80[in]dwPresetIndex 预置点的序号（从 1 开始），最多支持 255 个预置点返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。通过 NET_DVR_PTZPreset 控制云台，设备接收到控制命令后云台进行相应的动作，如果操作失败则返回错误，运行正常才返回成功。而通过 NET_DVR_PTZPreset_Other 控制云台，设备接收到控制命令后直接返回成功  

### 云台巡航操作  

### 5.23.7 云台巡航操作，需先启动预览 NET_DVR_PTZPCruise  

函  数： BOOL NET_DVR_PTZCruise(LONG lRealHandle,DWORD dwPTZCruiseCmd,BYTE byCruiseRoute, BYTEbyCruisePoint, WORD wInput)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwPTZCruiseCmd 操作云台巡航命令，详见表 5.81[in]byCruiseRoute 巡航路径，最多支持 32 条路径（序号从 1 开始）[in]byCruisePoint 巡航点，最多支持 32 个点（序号从 1 开始）[in]wInput 不同巡航命令时的值不同，预置点(最大 255)、时间(最大 255)、速度(最大 40)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

表 5.81 巡航操作命令  


<html><body><table><tr><td>dwPTZCruiseCmd宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>FILL_PRE_SEQ</td><td>30</td><td>将预置点加入巡航序列</td></tr><tr><td>SET_SEQ_DWELL</td><td>31</td><td>设置巡航点停顿时间</td></tr><tr><td>SET_SEQ_SPEED</td><td>32</td><td>设置巡航速度</td></tr><tr><td>CLE_PRE_SEQ</td><td>33</td><td>将预置点从巡航序列中删除</td></tr><tr><td>RUN_SEQ</td><td>37</td><td>开始巡航</td></tr><tr><td>STOP_SEQ</td><td>38</td><td>停止巡航</td></tr></table></body></html>  

### 5.23.8 云台巡航操作 NET_DVR_PTZPCruise_Other  

函  数： BOOL NET_DVR_PTZCruise_Other(LONG lUserID,LONG lChannel,DWORD dwPTZCruiseCmd,BYbyCruiseRoute, BYTE byCruisePoint, WORD wInput)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZCruiseCmd 操作云台巡航命令，详见表 5.81[in]byCruiseRoute 巡航路径，最多支持 32 条路径（序号从 1 开始）[in]byCruisePoint 巡航点，最多支持 32 个点（序号从 1 开始）[in]wInput 不同巡航命令时的值不同，预置点(最大 255)、时间(最大 25速度(最大 40)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

### 云台花样扫描操作  

### 5.23.9 云台花样扫描操作，需先启动预览 NET_DVR_PTZTrack  

函  数： BOOL NET_DVR_PTZTrack(LONG lRealHandle, DWORD dwPTZTrackCmd)参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwPTZTrackCmd 花样扫描操作命令，详见表 5.82  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

表 5.82 操作命令  


<html><body><table><tr><td>dwPTZTrackCmd宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>STAMEMCRUISE</td><td>34</td><td>开始记录花样扫描路径</td></tr><tr><td>STO_MEM_CRUISE</td><td>35</td><td>停止记录花样扫描路径</td></tr><tr><td>RUNCRUISE</td><td>36</td><td>开始执行花样扫描</td></tr></table></body></html>  

### 5.23.10 云台花样扫描操作 NET_DVR_PTZTrack_Other  

函  数： BOOL NET_DVR_PTZTrack_Other(LONG lUserID, LONG lChannel, DWORD dwPTZTrackCmd)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZTrackCmd 花样扫描操作命令，详见表 5.82返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

### 透明云台控制  

### 5.23.11 透明云台操作，需先启动预览 NET_DVR_TransPTZ  

函  数： BOOL NET_DVR_TransPTZ(LONG lRealHandle, char \*pPTZCodeBuf, DWORD dwBufSize)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]pPTZCodeBuf 存放云台控制码缓冲区的指针[in]dwBufSize 云台控制码的长度  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 使用该接口能直接通过设备将云台控制码信息直接传输给云台设备，而无需配置解码器。  

返回目录  

### 5.23.12 透明云台操作 NET_DVR_TransPTZ_Other  

函  数： BOOL NET_DVR_TransPTZ(LONG lUserID, LONG lChannel, char \*pPTZCodeBuf, DWORD dwBufSize)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]pPTZCodeBuf 存放云台控制码缓冲区的指针[in]dwBufSize 云台控制码的长度  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 使用该接口能直接通过设备将云台控制码信息直接传输给云台设备，而无需配置解码器。  

返回目录  

### 云台区域缩放控制  

### 5.23.13 云台图象区域选择放大或缩小 NET_DVR_PTZSelZoomIn  

函  数： BOOL NET_DVR_PTZSelZoomIn(LONG lRealHandle, LPNET_DVR_POINT_FRAME pStruPointFrame);参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]pStruPointFrame 云台图像区域位置信息，详见结构体：NET_DVR_POINT_FRAME返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口实现 3D 定位功能，需要前端设备的支持。假设当前预览显示图像的框为 $352^{*}288$ ，原点即该显示框的左上角的顶点。参数 pStruPointFrame中各坐标值的计算方法（以 X 轴方向上为例）：xTop=鼠标当前所选区域的左上点的值 $^{*}255/352$ 。缩小条件：xBottom 减去 xTop 的值大于 2。放大条件：xBottom 减去 xTop 的值大于 0，且 yBottom减去 yTop 的值大于 0。  

### 5.23.14 云台图像区域选择放大或缩小 NET_DVR_PTZSelZoomIn_Ex  

函  数： BOOL NET_DVR_PTZSelZoomIn_EX(LONG lUserID, LONG lChannel, LPNET_DVR_POINT_FRAMEpStruPointFrame)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]pStruPointFrame 云台图像区域位置信息，详见结构体：NET_DVR_POINT_FRA  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口实现 3D 定位功能，需要前端设备的支持。假设当前预览显示图像的框为 $352^{*}288$ ，原点即该显示框的左上角的顶点。参数 pStruPointFrame中各坐标值的计算方法（以 X 轴方向上为例）：xTop=鼠标当前所选区域的左上点的值 $^{*}255/352$ 。缩小条件：xBottom 减去 xTop 的值大于 2。放大条件：xBottom 减去 xTop 的值大于 0，且 yBottom减去 yTop 的值大于 0。  

### 云台参数配置  

### 5.23.15 获取设备的配置信息 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.83[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针，详见表 5.83[in]dwOutBufferSize 接收数据的缓冲长度(单位: 字节)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.83 所示。  

表 5.83 云台相关参数获取  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_TRACK_PARAMCFG</td><td>获取球机本地菜单规则</td><td>通道号</td><td>NET_DVR_TRACK_PARAMCFG</td><td>197</td></tr><tr><td>NET_DVR_GET_PTZPOS</td><td>获取IP 快球PTZ参数</td><td>通道号</td><td>NET_DVR_PTZPOS</td><td>293</td></tr><tr><td>NET_DVR_GET_PTZSCOPE</td><td>获取IP快球PTZ范围参数</td><td>通道号</td><td>NET_DVR_PTZSCOPE</td><td>294</td></tr><tr><td>NET_DVR_GET_CRUISE</td><td>获取巡航参数</td><td>通道号</td><td>NET_DVR_CRUISE_PARA</td><td>1020</td></tr><tr><td>NET_DVR_GET_MOTION_TRACK_CFG</td><td>获取网络球机跟踪参数</td><td>通道号</td><td>NET_DVR_MOTION_TRACK_CFG</td><td>3228</td></tr><tr><td>NET_DVR_GET_BASICPARAMCFG</td><td>获取 PTZ 基本参数信息</td><td>通道号</td><td>NET_DVR_PTZ_BASICPARAMCFG</td><td>3270</td></tr><tr><td>NET_DVR_GET_PTZOSDCFG</td><td>获取PTZOSD配置参数</td><td>通道号</td><td>NET_DVR_PTZ_OSDCFG</td><td>3272</td></tr><tr><td>NET_DVR_GET_POWEROFFMEMCFG</td><td>获取掉电记忆模式参数</td><td>通道号</td><td>NET_DVR_PTZ_POWEROFFMEMCFG</td><td>3274</td></tr><tr><td>NET_DVR_GET_PRIORITIZECFG</td><td>获取云台优先配置信息</td><td>通道号</td><td>NET_DVR_PTZ_PRIORITIZECFG</td><td>3281</td></tr><tr><td>NET_DVR_GET_PTZLOCKCFG</td><td>获取云台锁定信息</td><td>通道号</td><td>NET_DVR_PTZ_LOCKCFG</td><td>3287</td></tr><tr><td>NET_DVR_GET_PRIVACY_MASKS_ENABLECFG</td><td>获取云台隐私遮蔽全局使 能</td><td>通道号</td><td>NET_DVR_PRIVACY_MASKS_ENABLECFG</td><td>3291</td></tr><tr><td>NET_DVR_GET_SMARTTRACKCFG</td><td>获取智能运动跟踪配置信 息</td><td>通道号</td><td>NET_DVR_SMARTTRACKCFG</td><td>3293</td></tr><tr><td>NET_DVR_GET_PTZ_PARKACTION_CFG</td><td>获取云台守望参数</td><td>通道号</td><td>NET_DVR_PTZ_PARKACTION_CFG</td><td>3314</td></tr><tr><td>NET_DVR_GET_SCH_TASK</td><td>获取云台定时任务</td><td>通道号</td><td>NET_DVR_TIME_TASK</td><td>3381</td></tr><tr><td>NET_DVR_GET_PRESET_NAME</td><td>获取预置点名称</td><td>通道号</td><td>NET_DVR_PRESET_NAME</td><td>3383</td></tr><tr><td>NET_DVR_GET_SCHEDULE_AUTO_TRACK_CFG</td><td>获取定时智能跟踪参数</td><td>通道号</td><td>NET_DVR_SCHEDULE_AUTO_TRACK_CFG</td><td>3400</td></tr><tr><td>NET_DVR_GET_PHY_RATIO</td><td>获取物理倍率坐标信息</td><td>通道号</td><td>NET_DVR_PHY_RATIO</td><td>3606</td></tr></table></body></html>  

### 返回目录  

### 5.23.16 设置设备的配置信息 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.84[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针，详见表 5.84[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.84 所示。  

表 5.84 云台相关参数设置  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_TRACK_PARAMCFG</td><td>设置球机本地菜单规则</td><td>通道号</td><td>NET_DVR_TRACK_PARAMCFG</td><td>196</td></tr><tr><td>NET_DVR_SET_PTZPOS</td><td>设置 IP 快球 PTZ参数</td><td>通道号</td><td>NET_DVR_PTZPOS</td><td>292</td></tr><tr><td>NET_DVR_SET_CRUISE</td><td>设置巡航参数</td><td>通道号</td><td>NET_DVR_CRUISE_PARA</td><td>1021</td></tr><tr><td>NET_DVR_SET_MOTION_TRACK_CFG</td><td>设置网络球机跟踪参数</td><td>通道号</td><td>NET_DVR_MOTION_TRACK_CFG</td><td>3229</td></tr><tr><td>NET_DVR_SET_BASICPARAMCFG</td><td>设置 PTZ基本参数信息</td><td>通道号</td><td>NET_DVR_PTZ_BASICPARAMCFG</td><td>3271</td></tr><tr><td>NET_DVR_SET_PTZOSDCFG</td><td>设置PTZ OSD配置参数</td><td>通道号</td><td>NET_DVR_PTZ_OSDCFG</td><td>3273</td></tr><tr><td>NET_DVR_SET_POWEROFFMEMCFG</td><td>设置掉电记忆模式参数</td><td>通道号</td><td>NET_DVR_PTZ_POWEROFFMEMCFG</td><td>3275</td></tr><tr><td>NET_DVR_SET_PRIORITIZECFG</td><td>设置云台优先配置信息</td><td>通道号</td><td>NET_DVR_PTZ_PRIORITIZECFG</td><td>3282</td></tr><tr><td>NET_DVR_SET_PTZLOCKCFG</td><td>设置云台锁定信息</td><td>通道号</td><td>NET_DVR_PTZ_LOCKCFG</td><td>3288</td></tr><tr><td>NET_DVR_SET_PRIVACY_MASKS_ENABLECFG</td><td>设置云台隐私遮蔽全局使能</td><td>通道号</td><td>NET_DVR_PRIVACY_MASKS_ENABLECFG</td><td>3292</td></tr><tr><td>NET_DVR_SET_SMARTTRACKCFG</td><td>设置智能运动跟踪配置信息</td><td>通道号</td><td>NET_DVR_SMARTTRACKCFG</td><td>3294</td></tr><tr><td>NET_DVR_SET_PTZ_PARKACTION_CFG</td><td>设置云台守望参数</td><td>通道号</td><td>NET_DVR_PTZ_PARKACTION_CFG</td><td>3315</td></tr><tr><td>NET_DVR_SET_SCH_TASK</td><td>设置云台定时任务</td><td>通道号</td><td>NET_DVR_TIME_TASK</td><td>3380</td></tr><tr><td>NET_DVR_SET_PRESET_NAME</td><td>设置预置点名称</td><td>通道号</td><td>NET_DVR_PRESET_NAME</td><td>3382</td></tr><tr><td>NET_DVR_SET_SCHEDULE_AUTO_TRACK_CFG</td><td>设置定时智能跟踪参数</td><td>通道号</td><td>NET_DVR_SCHEDULE_AUTO_TRACK_CFG</td><td>3401</td></tr><tr><td>NET_DVR_SET_PHY_RATIO</td><td>设置物理倍率坐标信息</td><td>通道号</td><td>NET_DVR_PHY_RATIO</td><td>3607</td></tr></table></body></html>  

### 5.23.17 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.85[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.86[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.86），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.86 所示。  

表 5.85 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NETGETCRUISEPOINTV40</td><td>获取巡航路径配置</td><td>1018</td></tr><tr><td>NETDVRGETLIMITCFG</td><td>获取限位参数配置</td><td>3276</td></tr><tr><td>NETDVRGETPRIVACYMASKSCFG</td><td>获取云台隐私遮蔽参数</td><td>3285</td></tr></table></body></html>  

表 5.86 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NET GET CRUISEPOINT V40</td><td>dwCount个 NETDVRCRUISEPOINT COND</td><td>dwCount个NET_DVR_CRUISEPOINT V40</td></tr><tr><td>NET DVRGETLIMITCFG</td><td>dwCount个 NET DVRPTZ LIMITCOND</td><td>dwCount个 NET DVR RPTZ LIMITCFG</td></tr><tr><td>NET DVRGETPRIVACY MASKSCFG</td><td>dwCount 个 NETDVR PRIVACYMASKS COND</td><td>dwCount 个 NET DVRPRIVACYMASKS CFG</td></tr></table></body></html>  

### 返回目录  

### 5.23.18 批量设置配置信息 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.87[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.88[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.88），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的获取功能对应不同的结构体和命令号，如表 5.88 所示。  

表 5.87 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET DVRSETLIMITCFG</td><td>设置限位参数配置</td><td>3277</td></tr><tr><td>NETD DVR_SET_PRIVACY_MASKSCFG</td><td>设置云台隐私遮蔽参数</td><td>3286</td></tr></table></body></html>  

表 5.88 批量设置设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>IplnParamBuffer对应结构体</td></tr><tr><td>NET_DVR_SET_LIMITCFG</td><td>dwCount个NET_DVR_PTZ_LIMITCOND</td><td>dwCount个NET_DVR_PTZ_LIMITCFG</td></tr><tr><td>NETDVRSETPRIVACYMASKSCFG</td><td>dwCount个NET_DVRPRIVACY_MASKS_COND</td><td>dwCount个 NET_DVR_PRIVACY_MASKS_CFG</td></tr></table></body></html>  

### 返回目录  

### 云台参数长连接配置  

### 5.23.19 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 配置命令，详见表 5.89[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.89[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

<html><body><table><tr><td rowspan="7">[out]dwType</td><td colspan="2">配置状态</td></tr><tr><td>enum _NET_SDK_CALLBACK_TYPE_{</td><td></td></tr><tr><td>NET_SDK_CALLBACK TYPESTATUS</td><td>=0,//回调状态值</td></tr><tr><td>NET_SDK_CALLBACK TYPE PROGRESS</td><td>//回调进度值</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_DATA</td><td>//回调数据内容</td></tr><tr><td></td><td></td></tr><tr><td>}NET_SDK_CALLBACK_TYPE</td><td></td></tr></table></body></html>  

[out] lpBuffer 存放数据的缓冲区指针，详见表 5.90  
[out] dwBufLen 缓冲区大小  
[out] pUserData 用户数据  

返回值： -1 表示失败，其他值作为 NET_DVR_StopRemoteConfig 的句柄。获取错误码调用NET_DVR_GetLastError。  

说  明：  

表 5.89 长连接参数配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td><td>cbStateCallback</td></tr><tr><td>NETDVRGETPTZLOCKINFO</td><td>3290</td><td>获取云台锁定剩余秒数</td><td>NETDVRPTZLOCKINFOCOND</td><td>返回状态、信息数据</td></tr></table></body></html>  

表 5.90 回调参数内容  


<html><body><table><tr><td>dwType</td><td>含义</td><td>IpBuffer对应内容</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_STATUS</td><td>状态值</td><td>typedefenum{ NET_SDK_CALLBACK_STATUS_SUCCESS=1000,//成功 NET_SDK_CALLBACK_STATUS_PROCESSING,//处理中 NET_SDK_CALLBACK_STATUS_FAILED//失败</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_PROGRESS</td><td>进度值</td><td>}NET_SDK_CALLBACK_STATUS_NORMAL; IpBuffer的值表示进度(DWORD)</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_DATA</td><td>信息数据</td><td>对应结构体：NET_DVR_PTZLOCKINFO</td></tr></table></body></html>  

### 返回目录  

### 5.23.20 关闭长连接配置 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。说  明： 关闭长连接配置接口所创建的句柄，释放资源。  

### 远程控制  

### 5.23.21 远程控制 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.91[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.91[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.91 所示。  

表 5.91 远程配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET_DVR_PTZLIMIT_CTRL</td><td>3278</td><td>限位参数控制</td><td>NET_DVR_PTZ_LIMITCTRL</td></tr><tr><td>NET_DVR_PTZLIMIT_CTRL</td><td>3279</td><td>清除云台配置信息</td><td>NET_DVRCLEARCTRL</td></tr><tr><td>NET_DVR_PTZ_INITIALPOSITIONCTRL</td><td>3283</td><td>零方位角控制</td><td>NET_DVR_INITIALPOSITIONCTRL</td></tr><tr><td>NET_DVR_PTZ_ZOOMRATIOCTRL</td><td>3289</td><td>设置跟踪倍率</td><td>NET_DVR_ZOOMRATIOCTRL</td></tr><tr><td>NET_DVR_CONTROL_RESTART_SUPPORT</td><td>3312</td><td>快球机芯重启</td><td>NET_DVR_REMOTECONTROL_STUDY_PARAM</td></tr><tr><td>NET_DVR_CONTROL_PTZ_PATTERN</td><td>3313</td><td>快球云台花样扫描</td><td>NET_DVR_PTZ_PATTERN</td></tr><tr><td>NET_DVR_CONTROL_PTZ_MANUALTRACE</td><td>3316</td><td>手动跟踪定位</td><td>NET_DVR_PTZ_MANUALTRACE</td></tr></table></body></html>  

<html><body><table><tr><td>NETDVRCLEARIPCPARAM</td><td>3230</td><td>清空前端参数</td><td>NETDVRIPCPARAMTYPE</td></tr></table></body></html>  

### 获取巡航路径  

### 5.23.22 获取 IP 快球云台巡航路径 NET_DVR_GetPTZCruise  

函  数： BOOL NET_DVR_GetPTZCruise( LONG lUserID, LONG lChannel, LONG lCruiseRoute,LPNET_DVR_CRUISE_RET  lpCruiseRet)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]lCruiseRoute 巡航路径号[out]dwInBufferSize 巡航路径，详见结构体：NET_DVR_CRUISE_RET  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 辅助聚焦控制  

### 5.23.23 控制一键聚焦 NET_DVR_FocusOnePush  

函  数： BOOL NET_DVR_FocusOnePush(LONG lUserID, LONG lChannel)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]lChannel 通道号  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 恢复镜头电机默认位置  

### 5.23.24 恢复镜头电机默认位置 NET_DVR_ResetLens  

函  数： BOOL NET_DVR_ResetLens( LONG lUserID, LONG  lChannel)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]lChannel 通道号  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.24语音对讲、转发及广播  

### 语音对讲(Windows 32 位系统支持)  

### 5.24.1 启动语音对讲 NET_DVR_StartVoiceCom_V30  

函  数： LONG NET_DVR_StartVoiceCom_V30(LONG lUserID, DWORD dwVoiceChan, BOOLbNeedCBNoEncData, fVoiceDataCallBack cbVoiceDataCallBack, void\* pUser)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwVoiceChan 语音通道号，从 1 开始[in]bNeedCBNoEncData 需要回调的语音数据类型：0- 编码后的语音数据，1- 编码前的PCM 原始数据[in]cbVoiceDataCallBack 音频数据回调函数[in]pUser 用户数据指针  

typedef void(CALLBACK \*fVoiceDataCallBack)(LONG lVoiceComHandle, char \*pRecvDataBuffer,DWORD dwBufSize, BYTE byAudioFlag, void \*pUser)  

[out]lVoiceComHandle NET_DVR_StartVoiceCom_V30 的返回值  
[out]pRecvDataBuffer 存放音频数据的缓冲区指针  
[out]dwBufSize 音频数据大小  
[out]byAudioFlag 音频数据类型：0- 本地采集的数据，1- 设备发送过来的语音数据  
[out]pUser 用户数据指针  

返回值： -1 表示失败，其他值作为 NET_DVR_StopVoiceCom 等函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： Windows 7 操作系统下，如果不外接音频设备，该接口将返回失败。在调用开始语音对讲之前可先配置设备的语音对讲音频编码类型，即可先调用参数配置中的 NET_DVR_COMPRESSION_AUDIO结构配置。  

当前音频为 G722 编码时，音频数据的采样频率为 16000，16 位采样且是单通道的。因此，音频播放格式应如下定义：  

const int SAMPLES_PER_SECOND $=$ 16000;  
const int CHANNEL $=1$ ;  
const int BITS_PER_SAMPLE $=16$ ;  
WAVEFORMATEX m_wavFormatEx;  
m_wavFormatEx.cbSize $=$ sizeof(m_wavFormatEx);  
m_wavFormatEx.nBlockAlign $=$ CHANNEL $^*$ BITS_PER_SAMPLE / 8;  
m_wavFormatEx.nChannels $=$ CHANNEL;  
m_wavFormatEx.nSamplesPerSec $=$ SAMPLES_PER_SECOND;  
m_wavFormatEx.wBitsPerSample $=$ BITS_PER_SAMPLE;  
m_wavFormatEx.nAvgBytesPerSec $=$ SAMPLES_PER_SECOND\*m_wavFormatEx.nBlockAlign  

当前音频为 G711 或者 G726 编码时，音频数据的采样频率为 8000，16 位采样且是单通道的。因此，音频播放格式应如下定义：  

const int SAMPLES_PER_SECOND_G711_MU $=$ 8000;   
const int CHANNEL $=1$ ;   
const int BITS_PER_SAMPLE $=16$ ;   
WAVEFORMATEX m_wavFormatEx;   
m_wavFormatEx.cbSize $=$ sizeof(m_wavFormatEx);   
m_wavFormatEx.nBlockAlign $=$ CHANNEL $^*$ BITS_PER_SAMPLE / 8;   
m_wavFormatEx.nChannels $=$ CHANNEL;   
m_wavFormatEx.nSamplesPerSec $=$ SAMPLES_PER_SECOND_G711_MU;   
m_wavFormatEx.wBitsPerSample $=$ BITS_PER_SAMPLE;   
m_wavFormatEx.nAvgBytesPerSec $=$ SAMPLES_PER_SECOND_G711_MU\* m_wavFormatEx.nBlockAlign;  

### 返回目录  

### 5.24.2 设置语音对讲客户端的音量 NET_DVR_SetVoiceComClientVolume  

函  数： BOOL NET_DVR_SetVoiceComClientVolume(LONG lVoiceComHandle, WORD wVolume)  
参  数： [in]lVoiceComHandle NET_DVR_StartVoiceCom_V30 的返回值[in]wVolume 设置音量，取值范围[0,0xffff]  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 返回目录  

### 5.24.3 停止语音对讲或者语音转发 NET_DVR_StopVoiceCom  

函  数： BOOL NET_DVR_StopVoiceCom(LONG lVoiceComHandle)  
参  数： [in]lVoiceComHandle NET_DVR_StartVoiceCom_V30 或NET_DVR_StartVoiceCom_MR_V30 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError获取错误码，通过错误码判断出错原因。  

说  明：  

### 语音转发  

### 5.24.4 启动语音转发，获取编码后的音频数据 NET_DVR_StartVoiceCom_MR_V30  

函  数： LONG NET_DVR_StartVoiceCom_MR_V30(LONG lUserID, DWORD dwVoiceChan, fVoiceDataCallBackcbVoiceDataCallBack, void\* pUser)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwVoiceChan 语音通道号，从 1 开始[in]cbVoiceDataCallBack 音频数据回调函数，得到的数据是编码以后的音频数据，需调用我们提供的音频解码函数（详见音频编解码章节的说明）后可得到 PCM 数据  

[in]pUser 用户数据指针typedef void(CALLBACK \*fVoiceDataCallBack)(LONG lVoiceComHandle,char \*pRecvDataBuffer,DWORD  dwBufSize,BYTE  byAudioFlag,void\*pUser)[out]lVoiceComHandle NET_DVR_StartVoiceCom_MR_V30 的返回值[out]pRecvDataBuffer 存放音频数据的缓冲区指针[out]dwBufSize 音频数据大小[out]byAudioFlag 音频数据类型：1-设备发送过来的音频数据[out]pUser 用户数据指针返回值： -1 表示失败，其他值作为 NET_DVR_VoiceComSendData、NET_DVR_StopVoiceCom 等函数的句柄参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。明： 在调用开始语音转发之前可先配置设备的音频编码类型，即可先调用参数配置中的NET_DVR_COMPRESSION_AUDIO 结构配置。当前音频为 G722 编码时，音频数据的采样频率为 16000，16 位采样且是单通道的。因此，音频播放格式应如下定义：const int SAMPLES_PER_SECOND $=$ 16000;const int CHANNEL $=1$ ;const int BITS_PER_SAMPLE $=16$ ;WAVEFORMATEX m_wavFormatEx;m_wavFormatEx.cbSize $=$ sizeof(m_wavFormatEx);m_wavFormatEx.nBlockAlign $=$ CHANNEL $^*$ BITS_PER_SAMPLE / 8;m_wavFormatEx.nChannels $=$ CHANNEL;m_wavFormatEx.nSamplesPerSec $=$ SAMPLES_PER_SECOND;m_wavFormatEx.wBitsPerSample $=$ BITS_PER_SAMPLE;m_wavFormatEx.nAvgBytesPerSec $=$ SAMPLES_PER_SECOND\*m_wavFormatEx.nBlockAlign当前音频为 G711 或者 G726 编码时，音频数据的采样频率为 8000，16 位采样且是单通道的。因此，音频播放格式应如下定义：const int SAMPLES_PER_SECOND_G711_MU = 8000;const int CHANNEL $=1$ ;const int BITS_PER_SAMPLE $=16$ ;WAVEFORMATEX m_wavFormatEx;m_wavFormatEx.cbSize $=$ sizeof(m_wavFormatEx);m_wavFormatEx.nBlockAlign $=$ CHANNEL $^*$ BITS_PER_SAMPLE / 8;m_wavFormatEx.nChannels $=$ CHANNEL;m_wavFormatEx.nSamplesPerSec $=$ SAMPLES_PER_SECOND_G711_MU;m_wavFormatEx.wBitsPerSample $=$ BITS_PER_SAMPLE;m_wavFormatEx.nAvgBytesPerSec $=$ SAMPLES_PER_SECOND_G711_MU\*m_wavFormatEx.nBlockAlign;  

### 5.24.5 转发语音数据 NET_DVR_VoiceComSendData  

函  数： BOOL NET_DVR_VoiceComSendData(LONG lVoiceComHandle, char \*pSendBuf, DWORD dwBufSize)参  数： [in]lVoiceComHandle NET_DVR_StartVoiceCom_MR_V30 的返回值[in]pSendBuf 存放语音数据的缓冲区  

[in]dwBufSize  

语音数据大小。当前是 G722 音频编码类型时，每次发送的数据为 80 字节；当前是 G711 音频编码类型时，每次发送的数据为 160 字节。  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口实现将获取到的经过编码后的音频数据转发给设备。  

返回目录  

### 5.24.6 停止语音对讲或语音转发 NET_DVR_StopVoiceCom  

函  数： BOOL NET_DVR_StopVoiceCom (LONG lVoiceComHandle)  
参  数： [in]lVoiceComHandle NET_DVR_StartVoiceCom_V30 或NET_DVR_StartVoiceCom_MR_V30 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 语音广播(Windows 32 位系统支持)  

### 5.24.7 启动语音广播的 PC 端声音捕获 NET_DVR_ClientAudioStart_V30  

函  数： BOOL NET_DVR_ClientAudioStart_V30(fVoiceDataCallBack cbVoiceDataCallBack, void \*pUser)参  数： [in]cbVoiceDataCallBack 音频数据回调函数[in]pUser 用户数据typedef void(CALLBACK \*fVoiceDataCallBack)(char \*pRecvDataBuffer,DWORD dwBufSize, void \*pUser)[out]pRecvDataBuffer 存放 PC 本地采集的音频数据（PCM）的缓冲区指针[out]dwBufSize 音频数据大小[out]pUser 用户数据指针  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： Windows 7 操作系统下，如果不外接音频设备，该接口将返回失败。实现语音广播功能需先调用NET_DVR_ClientAudioStart_V30 接口采集本地 PC 的音频数据，再调用 NET_DVR_AddDVR 或者NET_DVR_AddDVR_V30 逐个添加设备同时将采集到的数据发送给设备。  

### 5.24.8 添加设备的某个语音通道到可以接收 PC 端声音的广播组  

NET_DVR_AddDVR _V30  

函  数： LONG NET_DVR_AddDVR_V30(LONG lUserID, DWORD dwVoiceChan)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwVoiceChan 语音通道号，从 1 开始  
返回值： -1 表示失败，其他值作为 NET_DVR_DelDVR_V30 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 实现语音广播功能需先调用 NET_DVR_ClientAudioStart_V30 接口采集本地 PC 的音频数据，再调用 NET_DVR_AddDVR 或者 NET_DVR_AddDVR_V30 逐个添加设备同时将采集到的数据发送给设备。SDK 最大支持添加 512 个设备。  

返回目录  

### 5.24.9 从可接收 PC 机声音的广播组里删除该设备的语音通道  

NET_DVR_DelDVR_V30  

函  数： LONG NET_DVR_DelDVR_V30(LONG lUserID)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.24.10 停止语音广播的 PC 端声音捕获 NET_DVR_ClientAudioStop  

函  数： BOOL NET_DVR_ClientAudioStop()  
参  数：  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 音频压缩参数  

### 5.24.11 获取当前生效的对讲音频压缩参数 NET_DVR_GetCurrentAudioCompress  

函  数： BOOL NET_DVR_GetCurrentAudioCompress(LONG lUserID, LPNET_DVR_COMPRESSION_AUDIOlpCompressAudio)  
参  数： [in] lUserID 用户 ID，NET_DVR_Login_V40 的返回值[in] lpCompressAudio 音频压缩参数  
返回值： -1 表示失败，其他值为音频编码句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 返回目录  

### 5.24.12 获取通道参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  

[in]dwCommand 设备配置命令，参见配置命令  
[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可  
[out]lpOutBuffer 接收数据的缓冲指针  
[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0  
[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.92 所示。  

表 5.92 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_COMPRESSCFG_AUD</td><td>获取语音对讲音频参数</td><td>无效</td><td>NET_DVR_COMPRESSION_AUDIO</td><td>1058</td></tr></table></body></html>  

### 5.24.13 设置通道参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.93 所示。  

表 5.93 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_COMPRESSCFG_AUD</td><td>设置语音对讲音频参数</td><td>无效</td><td>NET_DVR_COMPRESSION_AUDIO</td><td>1059</td></tr></table></body></html>  

### 音频编解码(Windows 32 位系统支持)  

### G722 音频编解码  

### 5.24.14 初始化音频编码 NET_DVR_InitG722Encoder  

函  数： void\* NET_DVR_InitG722Encoder()  

参  数：  

返回值： -1 表示失败，其他值为音频编码句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

### 说  明：  

### 5.24.15 G722 音频编码 NET_DVR_EncodeG722Frame  

函  数： BOOL NET_DVR_EncodeG722Frame(void \*pEncodeHandle,unsigned char\* pInBuffer, unsigned char\*pOutBuffer)  

参  数： [in]pEncodeHandle 音频编码句柄，NET_DVR_InitG722Encoder 的返回值[in]pInBuffer 输入缓冲区，按采样标准（采样频率为 16000，16 位采样，单通道）获取的 PCM 音频数据，规定输入数据的大小为 1280 字节[out]pOutBuffer 输出缓冲区，编码后的输出数据大小为 80 字节  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 主要为配合语音对讲、转发功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数 NET_DVR_DecodeG722Frame 进行数据解码。在调用编解码函数之前都需要做相应的初始化操作，在结束调用后还需要做释放资源的操作。  

返回目录  

### 5.24.16 释放音频编码资源 NET_DVR_ReleaseG722Encoder  

函  数： void NET_DVR_ReleaseG722Encoder(void \*pEncodeHandle)  
参  数： [in]pEncodeHandle 音频编码句柄，NET_DVR_InitG722Encoder 的返回值  
返回值： 无。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.24.17 初始化音频解码 NET_DVR_InitG722Decoder  

函  数： void\* NET_DVR_InitG722Decoder(int nBitrate $=$ 16000)  
参  数： [in]nBitrate 编码采样频率，这里我们规定采样频率为 16000  
返回值： -1 表示失败，其他值为音频解码句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.24.18 G722 音频解码 NET_DVR_DecodeG722Frame  

函  数： BOOL NET_DVR_DecodeG722Frame(void \*pDecHandle, unsigned char\* pInBuffer, unsigned char\*pOutBuffer)  
参  数： [in]pDecHandle 音频解码句柄，NET_DVR_InitG722Decoder 的返回值[in]pInBuffer 输入缓冲区，编码数据大小为 80 字节[out]pOutBuffer 输出缓冲区，按采样标准（采样频率为 16000，16 位采样，单通  

道）获取的 PCM 音频数据，规定输出数据的大小为 1280 字节返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。  

说  明： 主要为配合语音对讲、转发功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数 NET_DVR_EncodeG722Frame 将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数进行数据解码。在调用编解码函数之前都需要做相应的初始化操作，在结束调用后还需要做释放资源的操作。  

返回目录  

### 5.24.19 释放音频解码资源 NET_DVR_ReleaseG722Decoder  

函  数： void NET_DVR_ReleaseG722Decoder(void \*pDecHandle)参  数： [in]pDecHandle 音频解码句柄，NET_DVR_InitG722Decoder 的返回值返回值： 无返回值。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### G711 音频编解码  

### 5.24.20 G711 音频编码 NET_DVR_EncodeG711Frame  

函  数： BOOL NET_DVR_EncodeG711Frame(unsigned int iType, unsigned char \*pInBuffer, unsigned char\*pOutBuffer)  

参  数： [in]iType 编码类型：0-Mu law 编码，非 0-A law 编码[in]pInBuffer 输入缓冲区，按采样标准（采样频率为 8000，16 位采样，单通道）获取的 PCM 音频数据，规定输入数据的大小为 320 字节[out]pOutBuffer 输出缓冲区，编码后输出数据大小为 160 字节  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 主要为配合语音对讲而设定。当需将客户端的原始音频数据发送至设备端，可采用音频编码函数将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数 NET_DVR_DecodeG711Frame 进行解码。在调用编解码函数之前无需做初始化操作。  

返回目录  

### 5.24.21 G711 音频解码 NET_DVR_DecodeG711Frame  

函  数： BOOL NET_DVR_DecodeG711Frame(unsigned int iType, unsigned char \*pInBuffer, unsigned char\*pOutBuffer)  

参  数： [in]iType 编码类型：0-Mu law 编码，非 0-A law 编码[in]pInBuffer 输入缓冲区，编码数据大小为 160 字节[out]pOutBuffer 输出缓冲区，按采样标准（采样频率为 8000，16 位采样，单通道）获取的 PCM 音频数据，规定输出数据的大小为 320 字节  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 主要为配合语音对讲、转发功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数 NET_DVR_EncodeG711Frame 将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数进行数据解码。在调用编解码函数之前无需做初始化操作。  

### G726 音频编解码  

### 5.24.22 初始化音频编码 NET_DVR_InitG726Encoder  

函  数： void\* NET_DVR_InitG726Encoder(void  \*\*pEncMoudle)  
参  数： [out]pEncMoudle 编码模块句柄，编码时作为输入参数  
返回值： -1 表示失败，其他值为音频编码句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.24.23 G726 音频编码 NET_DVR_EncodeG726Frame  

函  数： BOOL NET_DVR_EncodeG726Frame(void \*pEncMoudle, unsigned char \*pInBuffer, unsigned char\*pOutBuffer, BYTE byReset)  

参  数： [in]pEncMoudle 音频编码句柄，NET_DVR_InitG726Encoder 的输出参数[in]pInBuffer 输入缓冲区，按采样标准（采样频率为 8000，16 位采样，单通道）获取的 PCM 音频数据，规定输入数据的大小为 640 字节[out]pOutBuffer 输出缓冲区，编码后输出数据大小为 80 字节[in]byReset 是否重置，第一帧需要重置  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 主要为配合语音对讲、转发功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数 NET_DVR_DecodeG726Frame 进行数据解码。在调用编解码函数之前都需要做相应的初始化操作，在结束调用后还需要做释放资源的操作。  

返回目录  

### 5.24.24 释放音频编码资源 NET_DVR_ReleaseG726Encoder  

函  数： void NET_DVR_ReleaseG726Encoder(void \*pEncHandle)  
参  数： [in]pEncHandle 音频编码句柄，NET_DVR_InitG726Encoder 的返回值  
返回值： 无。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 返回目录  

### 5.24.25 初始化音频解码 NET_DVR_InitG726Decoder  

函  数： void\* NET_DVR_InitG726Decoder(void \*\*pDecMoudle)参  数： [out]pDecMoudle 解码模块句柄，解码时作为输入参数  

返回值： -1 表示失败，其他值为音频解码句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.24.26 G726 音频解码 NET_DVR_DecodeG726Frame  

函  数： BOOL NET_DVR_DecodeG722Frame(void \*pDecMoudle, unsigned char \*pInBuffer, unsigned char\*pOutBuffer, BYTE  byReset)  

参  数： [in]pDecMoudle 音频解码句柄，NET_DVR_InitG726Decoder 的输出参数[in]pInBuffer 输入缓冲区，编码数据大小为 80 字节[out]pOutBuffer 输出缓冲区，按采样标准（采样频率为 8000，16 位采样，单通道）获取的 PCM 音频数据，规定输出数据的大小为 640 字节[in]byReset 是否重置，第一帧需要重置  

返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。  

说  明： 主要为配合语音对讲、转发功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数 NET_DVR_EncodeG726Frame 将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数进行数据解码。在调用编解码函数之前都需要做相应的初始化操作，在结束调用后还需要做释放资源的操作。  

### 5.24.27 释放音频解码资源 NET_DVR_ReleaseG726Decoder  

函  数： void NET_DVR_ReleaseG726Decoder(void \*pDecHandle)  
参  数： [in]pDecHandle 音频解码句柄，NET_DVR_InitG726Decoder 的返回值  
返回值： 无返回值。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.25透明通道  

### 5.25.1 建立透明通道 NET_DVR_SerialStart  

函  数： LONG NET_DVR_SerialStart(LONG lUserID,LONG lSerialPort, fSerialDataCallBackcbSerialDataCallBack, DWORD dwUser)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lSerialPort 串口号：1- 232 串口，2- 485 串口[in]cbSerialDataCallBack 透明通道数据回调函数[in]dwUser 用户数据  

typedef void(CALLBACK \*fSerialDataCallBack)(LONG lSerialHandle, char \*pRecvDataBuffer, DWORD dwBufSize, DWORD dwUser)  

[out]lSerialHandle NET_DVR_SerialStart 的返回值[out]pRecvDataBuffer 存放数据的缓冲区指针  

[out]dwBufSize 数据大小[out]dwUser 用户数据  
返回值： -1 表示失败，其他值作为 NET_DVR_SerialSend 等函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 需要从回调函数得到数据解码器必须支持数据回传，否则发送成功，回调依然不会有返回。  

返回目录  

### 5.25.2 通过透明通道向设备串口发送数据 NET_DVR_SerialSend  

函  数： BOOL NET_DVR_SerialSend(LONG lSerialHandle, LONG lChannel, char \*pSendBuf, DWORD dwBufSize)  
参  数： [in]lSerialHandle NET_DVR_SerialStart 的返回值[in]lChannel 使用 485 串口时有效，从 1 开始；232 串口作为透明通道时该值设置为 0[in]pSendBuf 发送数据的缓冲区指针[in]dwBufSize 缓冲区的大小，最多 1016 字节  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.25.3 断开透明通道 NET_DVR_SerialStop  

函  数： BOOL NET_DVR_SerialStop (LONG lSerialHandle)  
参  数： [in]lSerialHandle NET_DVR_SerialStart 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.26向串口发送数据  

### 5.26.1 直接向串口发送数据，不需要建立透明通道 NET_DVR_SendToSerialPort  

函  数： BOOL NET_DVR_SendToSerialPort(LONG lUserID, DWORD dwSerialPort, DWORD dwSerialIndex, char\*pSendBuf, DWORD dwBufSize)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwSerialPort 串口类型：1-232，2-485[in]dwSerialIndex 表示第几个 232 或者 485，从 1 开始[in]pSendBuf 发送数据的缓冲区指针[in]dwBufSize 缓冲区的大小，最多 1016 字节  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.26.2 直接向 232 串口发送数据，不需要建立透明通道 NET_DVR_SendTo232Port  

函  数： BOOL NET_DVR_SendTo232Port(LONG lUserID, char \*pSendBuf, DWORD dwBufSize)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]pSendBuf 发送数据的缓冲区指针[in]dwBufSize 缓冲区的大小，最多 1016 字节  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.27设备手动录像  

### 5.27.1 远程手动启动设备录像 NET_DVR_StartDVRRecord  

函  数： BOOL NET_DVR_StartDVRRecord(LONG lUserID,LONG lChannel,LONG lRecordType)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号： $0{\times}00{\dagger}\mathbf{f}$ 表示所有模拟通道，0xff00 表示所有数字通道，0xffff 表示所有模拟和数字通道[in]lRecordType 录像类型：0- 手动，1- 报警，2- 回传，3- 信号，4- 移动，5- 遮挡  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

 录像类型设置需要设备支持，网络摄像机和球机只支持手动录像一种类型。  
 当某通道已经开启定时录像的前提下首次开启手动录像，此次操作未生效，仍保持定时录像状态，且查询设备状态（见 NET_DVR_GetDVRWorkState_V30 和 NET_DVR_GetDVRWorkState；结构体 NET_DVR_WORKSTATE_V30 和 NET_DVR_WORKSTATE）中的录像状态仍为录像；此时关闭手动录像，停止了定时录像，且查询录像状态为不录像；第二次开启手动录像，此时手动录像开始；停止手动录像后，重启设备，定时录像重新打开。  

返回目录  

### 5.27.2 远程手动停止设备录像 NET_DVR_StopDVRRecord  

函  数： BOOL NET_DVR_StopDVRRecord(LONG lUserID,LONG lChannel)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号： $0{\times}00{\dagger}\mathbf{f}$ 表示所有模拟通道，0xff00 表示所有数字通道，0xffff 表示所有模拟和数字通道  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 5.28服务器测试  

### 服务器测试  

### 5.28.1 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 配置命令，详见表 5.94[in] lpInBuffer 输入参数，具体内容跟配置命令相关详见表 5.94[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数，设为 NULL[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

[out] dwType 配置状态，无效 [out] lpBuffer 存放数据的缓冲区指针 [out] dwBufLen 缓冲区大小 [out] pUserData 用户数据  

返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。  

说  明：  通过 NET_DVR_GetDeviceAbility(能力集类型：DEVICE_NETAPP_ABILITY)获取 NTP、NAS、Email、FTP、IP 测试能力。 长连接状态通过 NET_DVR_GetRemoteConfigState 获取。  

表 5.94 服务器测试命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td><td>cbStateCallback</td></tr><tr><td>NET_DVR_NTP_SERVER_TEST</td><td>3387</td><td>NTP服务器测试</td><td rowspan="12">NET_DVR_SERVER_TEST_PARA</td><td>NULL</td></tr><tr><td>NET_DVR_NAS_SERVER_TEST</td><td>3388</td><td>NAS服务器测试</td><td></td></tr><tr><td>NET_DVR_EMAIL_SERVER_TEST</td><td>3389</td><td>Email服务器测试</td><td></td></tr><tr><td>NET_DVR_FTP_SERVER_TEST</td><td>3390</td><td>FTP服务器测试</td><td></td></tr><tr><td>NET_DVR_IP_TEST</td><td>3391</td><td>IP测试</td><td></td></tr><tr><td>NET_DVR_CLOUDSTORAGE_SERVER_TEST</td><td>3421</td><td>云存储服务器测试</td><td></td></tr><tr><td>NET_DVR_PHONE_NUM_TEST</td><td>3422</td><td>电话号码测试(短信测试)</td><td></td></tr></table></body></html>  

### 返回目录  

### 5.28.2 获取长连接配置的状态 NET_DVR_GetRemoteConfigState  

函  数： BOOL NET_DVR_GetRemoteConfigState(LONG lHandle, void \*pState)参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值[out] pState 返回的状态值，详见表 5.95  

返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。说  明：  

表 5.95 长连接状态  


<html><body><table><tr><td>pState 状态值</td><td>含义</td></tr><tr><td>29</td><td>设备操作失败</td></tr><tr><td>55</td><td>IP地址不匹配</td></tr><tr><td>165</td><td>设备连接测试服务器失败</td></tr><tr><td>166</td><td>NAS服务器挂载目录失败，目录无效</td></tr><tr><td>167</td><td>NAS服务器挂载目录失败，没有权限或用户名密码错误</td></tr><tr><td>168</td><td>服务器使用域名，但是没有配置DNS，可能造成域名无效</td></tr><tr><td>169</td><td>没有配置网关，可能造成发送邮件失败</td></tr><tr><td>170</td><td>测试服务器的登陆用户名或密码错误</td></tr><tr><td>171</td><td>设备和 smtp 服务器交互异常</td></tr><tr><td>172</td><td>该用户在服务器上创建目录失败</td></tr><tr><td>173</td><td>该用户没有写入权限</td></tr><tr><td>174</td><td>IP冲突</td></tr><tr><td>175</td><td>存储池空间已满</td></tr><tr><td>176</td><td>云服务器存储池无效，没有配置存储池或者存储池ID 错误</td></tr><tr><td>1461</td><td>端口错误</td></tr></table></body></html>  

### 返回目录  

### 5.28.3 关闭长连接配置 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。说  明： 关闭长连接配置接口所创建的句柄，释放资源。  

### Email 测试  

### 5.28.4 测试按已配置的 EMAIL 参数能否收发成功 NET_DVR_StartEmailTest  

函  数： LONG NET_DVR_StartEmailTest(LONG lUserID)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  
返回值： -1 表示失败，其他值作为 NET_DVR_GetEmailTestProcess 、NET_DVR_StopEmailTest 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在调用此接口测试前，需要配置相关的 EMAIL 参数，详见 NET_DVR_GetDVRConfig、NET_DVR_SetDVRConfig 的网络应用参数（EMAIL）配置。  

### 5.28.5 获取邮件测试的进度 NET_DVR_GetEmailTestProgress  

函  数： BOOL NET_DVR_GetEmailTestProgress(LONG lEmailTestHandle, DWORD\* pState)  
参  数： [in]lEmailTestHandle NET_DVR_StartEmailTest 的返回值[out]pState 邮件测试的进度，进度值的取值范围（0,100），其他值定义如表5.96 所示。  

表 5.96 邮件测试进度  


<html><body><table><tr><td>pState宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>PROCESSING</td><td>0</td><td>正在处理</td></tr><tr><td>PROCESS_SUCCESS</td><td>100</td><td>过程完成</td></tr><tr><td>PROCESS_EXCEPTION</td><td>400</td><td>过程异常</td></tr><tr><td>PROCESS_FAILED</td><td>500</td><td>过程失败</td></tr></table></body></html>  

返回值：  

TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

返回目录  

### 5.28.6 停止邮件测试 NET_DVR_StopEmailTest  

函  数： BOOL NET_DVR_StopEmailTest(LONG lEmailTestHandle)  
参  数： [in]lEmailTestHandle NET_DVR_StartEmailTest 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

## 5.29鱼眼相关功能  

### 鱼眼参数配置  

### 5.29.1 获取设备的配置信息 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.97[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针，详见表 5.97[in]dwOutBufferSize 接收数据的缓冲长度（以字节为单位），不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通  

过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.97 所示。  

表 5.97 获取鱼眼参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_PREVIEW_DISPLAYCFG</td><td>获取鱼眼IPC预览显示参数</td><td>通道号</td><td>NET_DVR_PREVIEW_DISPLAYCFG</td><td>3211</td></tr><tr><td>NET_DVR_GET_PRESET_NUM</td><td>获取鱼眼IPC预置点个数</td><td>通道号</td><td>NET_DVR_PRESET_INFO</td><td>3226</td></tr><tr><td>NET_DVR_GET_PTZCRUISE_NUM</td><td>获取鱼眼IPC巡航路径个数</td><td>通道号</td><td>NET_DVR_PTZCRUISE_INFO</td><td>3227</td></tr><tr><td>NET_DVR_GET_MOTION_TRACK_CFG</td><td>获取鱼眼IPC或者球机跟踪参 数</td><td>通道号</td><td>NET_DVRMOTION_TRACK_CFG</td><td>3228</td></tr><tr><td>NET_DVR_GET_PTZ_POINT</td><td>获取PTZ点坐标</td><td>通道号</td><td>NET_VCA_POINT</td><td>3245</td></tr><tr><td>NET_DVR_GET_TRACK_DEV_PARAM</td><td>获取跟踪设备参数</td><td>通道号</td><td>NET_DVR_TRACK_DEV_PARAM</td><td>3261</td></tr><tr><td>NET_DVR_GET_PTZ_TRACK_PARAM</td><td>获取PTZ跟踪参数</td><td>通道号</td><td>NET_DVR_PTZ_TRACK_PARAM</td><td>3263</td></tr></table></body></html>  

 NET_DVR_GET_PTZ_POINT 获取 PTZ 点坐标时，坐标点的位置相对于预览窗口左上角，值以当前预览窗口的大小为准，采用归一化的坐标值。  

### 返回目录  

### 5.29.2 设置设备的配置信息 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.98[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针，详见表 5.98[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.98 所示。  

表 5.98 设置鱼眼参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_PREVIEW_DISPLAYCFG</td><td>设置鱼眼IPC预览显示参数</td><td>通道号</td><td>NETDVRPREVIEW_DISPLAYCFG</td><td>3212</td></tr><tr><td>NET_DVR_SET_MOTION_TRACK_CFG</td><td>设置鱼眼IPC或者球机跟踪参数</td><td>通道号</td><td>NET_DVR_MOTION_TRACK_CFG</td><td>3229</td></tr><tr><td>NET_DVR_SET_PTZ_POINT</td><td>设置PTZ点坐标</td><td>通道号</td><td>NET_VCAPOINT</td><td>3246</td></tr><tr><td>NET_DVR_SET_TRACK_DEV_PARAM</td><td>设置跟踪设备参数</td><td>通道号</td><td>NET_DVR_TRACK_DEV_PARAM</td><td>3262</td></tr><tr><td>NET_DVR_SET_PTZ_TRACK_PARAM</td><td>设置PTZ跟踪参数</td><td>通道号</td><td>NETDVRPTZTRACKPARAM</td><td>3264</td></tr></table></body></html>  

 NET_DVR_SET_PTZ_POINT 设置 PTZ 点坐标时，坐标点的位置相对于预览窗口左上角，值以当前预览窗口的大小为准，采用归一化的坐标值。  

### 5.29.3 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.99[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.100[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.100），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.100 所示。  

表 5.99 鱼眼参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_PRESETCFG</td><td>获取鱼眼IPC预置点参数</td><td>3224</td></tr><tr><td>NETDVRGETPTZCRUISECFG</td><td>获取鱼眼IPC巡航路径参数</td><td>3225</td></tr></table></body></html>  

表 5.100 批量获取鱼眼参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_PRESETCFG</td><td>dwCount个NET_DVR_PRESET_COND</td><td>dwCount个NET_DVR_PRESETCFG</td></tr><tr><td>NETDVRGETPTZCRUISECFG</td><td>dwCount个NET_DVR_PTZCRUISE_COND</td><td>dwCount个NET_DVRPTZCRUISECFG</td></tr></table></body></html>  

### 返回目录  

### 长连接配置  

### 5.29.4 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  

[in] dwCommand 配置命令，详见表 5.101  
[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.101  
[in] dwInBufferLen 输入缓冲的大小  
[in] cbStateCallback 状态回调函数  
[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

[out] dwType 配置状态，无效  
[out] lpBuffer 存放数据的缓冲区指针，具体内容跟 dwType 相关，详见表5.102  
[out] dwBufLen 缓冲区大小  
[out] pUserData 用户数据  

返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.101 所示。  

表 5.101 鱼眼参数长连接配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td><td>cbStateCallback</td></tr><tr><td>NET_DVR_FISHEYE_CFG</td><td>3244</td><td>鱼眼长连接配置</td><td>NULL</td><td>返回状态或者数据信息</td></tr></table></body></html>  

表 5.102 长连接回调数据  


<html><body><table><tr><td>dwType</td><td>值</td><td>含义</td><td>lpBuffer对应内容</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_STATUS</td><td>0</td><td>状态值</td><td>typedefenum NET_SDK_CALLBACKSTATUS_SUCCESS=1000,//成功 NET_SDK_CALLBACK_STATUS_PROCESSING,//处理中 NET_SDK_CALLBACK_STATUS_FAILED//失败</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_DATA</td><td>2</td><td>信息数据</td><td>}NET_SDK_CALLBACK_STATUS_NORMAL; NET_DVR_CALLBACK_TYPE_DATA</td></tr></table></body></html>  

### 5.29.5 发送长连接数据 NET_DVR_SendRemoteConfig  

函  数： BOOL NET_DVR_SendRemoteConfig(LONG lHandle, DWORD dwDataType, char \*pSendBuf,DWORD dwBufSize)  

参  数： [in] lHandle 长连接句柄，NET_DVR_StartRemoteConfig 的返回值[in] dwDataType 数据类型，详见表 5.103[in] pSendBuf 保存发送数据的缓冲区，与 dwDataType 有关，详见表 5.103[in] dwBufSize 发送数据的长度  

返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。  

说  明： 在调用该接口之前，必须先调用 NET_DVR_StartRemoteConfig 获取长连接句柄。不同的数据类型(dwDataType)，pSendBuf 对应不同的结构体，如下表所示。  

表 5.103 长连接发送数据  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>控制功能</td><td>lpOutBuff对应结构体</td></tr><tr><td>DRAGPTZ</td><td>51</td><td>拖动PTZ</td><td>NETDVRDRAGPOSPARAM</td></tr></table></body></html>  

### 返回目录  

### 5.29.6 关闭长连接配置 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 长连接句柄，NET_DVR_StartRemoteConfig 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。说  明： 关闭长连接配置接口所创建的句柄，释放资源。  

### 远程控制  

### 5.29.7 远程控制 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.104[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.104[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.104 所示。  

表 5.104 鱼眼远程控制  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET DVRREMOTECONTROLPRESETPOINT</td><td>3214</td><td>远程控制预置点</td><td>NETDVRPRESET POINT PARAM</td></tr><tr><td>NET DVRREMOTECONTROLCRUISE</td><td>3215</td><td>远程控制巡航</td><td>NET DVR PTZ CRUISE PARAM</td></tr><tr><td>NETDVRREMOTECONTROLDEVPARAM</td><td>3247</td><td>设置设备登录客户端参数</td><td>NETD DVRLOGIN DEVICEPARAM</td></tr></table></body></html>  

### 返回目录  

### 获取鱼眼设备状态  

### 5.29.8 获取设备状态 NET_DVR_GetDeviceStatus  

函  数： BOOL NET_DVR_GetDeviceStatus(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpOutBuffer, DWORDdwOutBufferSize)  
参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
[in] dwCommand 获取设备状态的命令值，详见表 5.105  
[in] dwCount 要获取的状态个数  
[in] lpInBuffer 状态获取条件缓冲区，详见表 5.105  
[in] dwInBufferSize 缓冲区长度  
[out] lpStatusList 错误信息列表，和要查询的监控点一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节(1 个 32 位无符号整数值)，参数值：0- 成功，大于 0- 失败  
[out] lpOutBuffer 设备返回的状态内容（详见表 5.105），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的  
[out] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取设备状态信息的通用接口。不同的获取功能对应不同的结构体和命令号，如表 5.105 所示。  

表 5.105 鱼眼状态  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>lplnBuffer对应结构体</td><td>IpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_FISHEYE_STREAM_STATUS</td><td>获取鱼眼码流状态</td><td>（DWORD）通道号</td><td>dwCount个 NET_DVR_FISHEYE_STREAM_STATUS</td><td>3248</td></tr></table></body></html>  

## 5.30GIS 相关功能  

### GIS 参数配置  

### 5.30.1 获取设备的配置信息 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.106[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针，详见表 5.106[in]dwOutBufferSize 接收数据的缓冲长度（以字节为单位），不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.106 所示。  

表 5.106 获取鱼眼参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_SATELLITETIME</td><td>获取卫星定位参数配置</td><td>无效</td><td>NET_DVR_SATELLITETIME_CFG</td><td>3709</td></tr></table></body></html>  

### 5.30.2 设置设备的配置信息 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.107[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针，详见表 5.107[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.107 所示。  

表 5.107 设置鱼眼参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_SATELLITETIME</td><td>设置卫星定位参数配置</td><td>无效</td><td>NET_DVR_SATELLITETIME_CFG</td><td>3710</td></tr></table></body></html>  

### 5.30.3 获取设备的配置信息(标准协议)NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.108[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.109  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam中lpCondBuffer、lpOutBuffer分别对应不同的内容，具体如表 5.109所示。  

表 5.108 参数获取配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NETDVRGETCENTRALIZEDCTRL</td><td>获取集中布控参数配置</td><td>3701</td></tr><tr><td>NETDVRGETVANDALPROOFALARM</td><td>获取防破坏报警参数配置</td><td>3704</td></tr><tr><td>NETDVRGETGISINFO</td><td>获取当前球机的GIS信息数据</td><td>3711</td></tr></table></body></html>  

表 5.109 获取设备参数  


<html><body><table><tr><td>dwCommand 宏定义</td><td>pCondBuffer</td><td>lpOutBuffer</td></tr><tr><td>NETDVRGET CENTRALIZEDCTRL</td><td>4字节(DWORD)通道号</td><td>NET TDVRCENTRALIZEDCTRLCFG</td></tr><tr><td>NET DVRGETVANDALPROOFALARM</td><td>4字节(DWORD)通道号</td><td>NET DVR_VANDALPROOFALARM_CFG</td></tr><tr><td>NET DVRGETGISINFO</td><td>4字节(DWORD)通道号</td><td>NET DVRGIS INFO</td></tr></table></body></html>  

### 返回目录  

### 5.30.4 设置设备的配置信息(标准协议)NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.110[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.111  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.111 所示。  

表 5.110 设置参数配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET DVRSET CENTRALIZEDCTRL</td><td>设置集中布控参数配置</td><td>3702</td></tr><tr><td>NETD DVRSETVANDALPROOFALARM</td><td>设置防破坏报警参数配置</td><td>3705</td></tr></table></body></html>  

表 5.111 设置设备参数  


<html><body><table><tr><td>dwCommand 宏定义</td><td>IpCondBuffer</td><td>IplnBuffer</td></tr><tr><td>NET DVR_SET_C CENTRALIZEDCTRL</td><td>4字节(DWORD)通道号</td><td>NET DVR_CENTRALIZEDCTRL_CFG</td></tr><tr><td>NET DVRSET_VANDALPROOFALARM</td><td>4字节(DWORD)通道号</td><td>NET DVR_VANDALPROOFALARM_CFG</td></tr></table></body></html>  

### 电子罗盘远程控制  

### 5.30.5 远程控制(标准协议) NET_DVR_STDControl  

函  数： BOOL NET_DVR_STDControl(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONTROLlpControlParam)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.112[in&out]lpControlParam 远程控制输入输出参数  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对于不同的配置功能（dwCommand），lpControlParam 中的 lpCondBuffer 对应不同的内容，详见表 5.112。  

表 5.112 控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>dwCommand含义</td><td>IpCondBuffer</td></tr><tr><td>NET_DVR_COMPASS_CALIBRATE_CTRL</td><td>3706</td><td>电子罗盘矫正控制</td><td>NET_DVR_COMPASS_COND</td></tr><tr><td>NET_DVR_COMPASS_NORTH_CTRL</td><td>3707</td><td>电子罗盘指向正北控制</td><td>NET_DVR_COMPASS_COND</td></tr></table></body></html>  

 设备是否支持电子罗盘矫正控制功能，对应电子罗盘能力集(CompassCap)中节点<isSupportCalibrate>，接口：NET_DVR_GetSTDAbility(能力集类型：NET_DVR_GET_COMPASS_CAPABILITIES)。  
 设备是否支持电子罗盘指向正北控制功能，对应电子罗盘能力集(CompassCap)中节点<isSupportPointToNorth>，接口：NET_DVR_GetSTDAbility(能力集类型：NET_DVR_GET_COMPASS_CAPABILITIES)。  

## 5.31设备维护管理  

获取设备工作状态  

### 5.31.1 获取设备的工作状态 NET_DVR_GetDVRWorkState_V30  

函  数： BOOL NET_DVR_GetDVRWorkState_V30(LONG lUserID, LPNET_DVR_WORKSTATE_V30 lpWorkState)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[out]lpWorkState 获取的设备工作状态结构体参数  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 此处获取的是 IPC 的硬盘状态，其他设备的硬盘状态通过 NET_DVR_GetDVRConfig 的NET_DVR_GET_HDCFG 命令获取。  

### 5.31.2 获取设备运行状态 NET_DVR_GetDeviceStatus  

函  数： BOOL NET_DVR_GetDeviceStatus(LONG lUserID,DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize,LPVOID lpStatusList, LPVOID lpOutBuffer,DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.113[in] dwCount 要设置的个数，设为 1[in] lpInBuffer 配置条件缓冲区，详见表 5.114[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的监控点一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节  

(1 个 32 位无符号整数值)，参数值：0- 成功，大于 0- 失败[out] lpOutBuffer 设备返回的参数内容（详见表 5.114），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

表 5.113 状态获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>宏定义值</td></tr><tr><td>NETDVRGETREMOTECONTROLSTATUS</td><td>获取无线布防状态</td><td>3423</td></tr><tr><td>NET_DVR_GET_ALARMIN_STATUS</td><td>获取报警输入状态</td><td>9115</td></tr><tr><td>NET_DVR_GET_ALARMOUT_STATUS</td><td>获取报警输出状态</td><td>9116</td></tr><tr><td>NET_DVR_GET_AUDIO_CHAN_STATUS</td><td>获取语音对讲状态</td><td>9117</td></tr></table></body></html>  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取设备状态信息的通用接口。全部获取时 dwCount 置为 0xffffffff，lpInBuffer 置为 NULL，dwInBufferSize 置为 0，lpStatusList 置为 NULL。lpOutBuffer 前面 4 个字节为个数(N)，后面为设备返回的 N 个信息内容（按通道号 $\mathsf{1}^{\sim_{N}}$ 排列），如果设置的 lpOutBuffer 缓冲区不足，仅返回部分信息，可以根据返回的个数（前 4 字节的值）重新获取。不同的获取功能对应不同的结构体和命令号，如表 5.114 所示。  

表 5.114 获取设备状态  


<html><body><table><tr><td>dwCommand宏定义</td><td>lplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NETDVRGETREMOTECONTROLSTATUS</td><td>dwCount个NET_DVR_REMOTECONTROL_COND</td><td>dwCount个NETDVRREMOTECONTROLSTATUS</td></tr><tr><td>NET_DVRGETALARMINSTATUS</td><td>dwCount个4字节报警输入通道号</td><td>dwCount个4字节状态值(0-没有报警，1-有报警）</td></tr><tr><td>NETDVRGETALARMOUTSTATUS</td><td>dwCount个4字节报警输出通道号</td><td>dwCount个4字节状态值(0-没有报警，1-有报警）</td></tr><tr><td>NETDVRGETAUDIOCHANSTATUS</td><td>dwCount为1，4字节语音对讲通道号</td><td>1个4字节状态(0-未开启，1-开启)</td></tr></table></body></html>  

返回目录  

### 5.31.3 设备在线状态检测 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.115[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.115[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该控制命令用于手动检测设备是否在线，接口返回 TRUE 表示在线，FALSE 表示与设备通信失败或者返回错误状态。设备在线状态自动巡检功能通过 NET_DVR_SetSDKLocalCfg（配置类型：NET_SDK_LOCAL_CFG_TYPE_CHECK_DEV）进行配置。  

表 5.115 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET_DVR_CHECK_USERSTATUS</td><td>20005</td><td>检测设备是否在线</td><td>NULL</td></tr></table></body></html>  

### 5.31.4 启动设备状态巡检 NET_DVR_StartGetDevState  

函  数： BOOL NET_DVR_StartGetDevState(LPNET_DVR_CHECK_DEV_STATE pParams)  
参  数： [in] pParams 设备工作状态巡检参数，包括巡检时间、结果回调函数等，详见结构体：NET_DVR_CHECK_DEV_STATE  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 启动后，SDK 定时巡检设备，获取到的设备状态信息在结构体的回调函数中返回。相当于实现定时调用 NET_DVR_GetDeviceConfig(命令：NET_DVR_GET_WORK_STATUS)。  

返回目录  

### 5.31.5 停止设备状态巡检 NET_DVR_StopGetDevState  

函  数： BOOL NET_DVR_StopGetDevState()  
参  数： 无  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 停止巡检设备工作状态，释放资源。  

### 5.31.6 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 配置命令，详见表 5.56[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.56[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

[out] dwType  

配置状态，获取音量时 dwType 状态无效，其他命令对应取值：  

enum _NET_SDK_CALLBACK_TYPE_{NET_SDK_CALLBACK_TYPE_STATUS $=0_{\scriptscriptstyle*}$ //回调状态值NET_SDK_CALLBACK_TYPE_PROGRESS, //回调进度值NET_SDK_CALLBACK_TYPE_DATA //回调数据内容  
}NET_SDK_CALLBACK_TYPE  

[out] lpBuffer  

存放数据的缓冲区指针，NET_DVR_START_GET_INPUTVOLUME获取音量时 lpBuffer 对应 4 字节声音强度，其他命令对应取值详见表 5.57  

[out] dwBufLen 缓冲区大小 [out] pUserData 用户数据  

返回值： -1 表示失败，其他值作为 NET_DVR_StopRemoteConfig 的句柄。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.116 长连接参数配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td><td>cbStateCallback</td></tr><tr><td>NET_DVR_GET_ONLINEUSER_INFO</td><td>3762</td><td>长连接获取用户在线信息</td><td>NET_DVR_ONLINEUSER_COND</td><td>返回状态、信息数据</td></tr></table></body></html>  

表 5.117 长连接回调数据  


<html><body><table><tr><td>dwType</td><td>含义</td><td>IpBuffer对应内容</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_STATUS</td><td>状态值</td><td>typedefenum{ NET_SDK_CALLBACK_STATUS_SUCCESS=1000,//成功</td></tr><tr><td rowspan="2"></td><td rowspan="2"></td><td>NET_SDK_CALLBACK_STATUS_PROCESSING,//处理中</td></tr><tr><td>NET_SDK_CALLBACK_STATUS_FAILED//失败</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_PROGRESS</td><td>进度值</td><td>}NET_SDK_CALLBACK_STATUS_NORMAL; IpBuffer的值表示进度（DWORD）</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_DATA</td><td>信息数据</td><td>对应结构体：NET_DVR_ONLINEUSER_CFG</td></tr></table></body></html>  

### 返回目录  

### 5.31.7 关闭长连接 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。说  明： 关闭长连接配置接口所创建的句柄，释放资源  

### 远程升级  

### 5.31.8 设置远程升级时网络环境 NET_DVR_SetNetworkEnvironment  

函  数： BOOL NET_DVR_SetNetworkEnvironment(DWORD dwEnvironmentLevel) 参  数： [in]dwEnvironmentLevel 网络环境级别  

enum{ LOCAL_AREA_NETWORK $=0_{\scriptscriptstyle*}$ , //局域网环境 WIDE_AREA_NETWORK //广域网环境  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 接口中的网络环境级别参数分为两类：LOCAL_AREA_NETWORK 表示局域网环境(网络环境好，通讯流畅)；WIDE_AREA_NETWORK 表示广域网环境(网络环境差，易阻塞)。在调用远程升级接口之前，可以通过此接口适应不同的升级环境。  

### 5.31.9 远程升级 NET_DVR_Upgrade  

函  数： LONG NET_DVR_Upgrade(LONG lUserID, char \*sFileName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sFileName 升级的文件路径（包括文件名）。路径长度和操作系统有关，sdk不做限制，windows 默认路径长度小于等于 256 字节（包括文件名在内）。  

返回值： -1 表示失败，其他值作为 NET_DVR_GetUpgradeState 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.31.10 获取远程升级的进度 NET_DVR_GetUpgradeProgress  

函  数： int NET_DVR_GetUpgradeProgress(LONG lUpgradeHandle)  
参  数： [in]lUpgradeHandle NET_DVR_Upgrade 的返回值  
返回值： -1 表示失败， $0{\sim}100$ 表示升级进度。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.31.11 获取远程升级的状态 NET_DVR_GetUpgradeState  

函  数： int NET_DVR_GetUpgradeState(LONG lUpgradeHandle)  
参  数： [in]lUpgradeHandle NET_DVR_Upgrade 的返回值  
返回值： -1 表示失败，其他值定义如下：1- 升级成功; 2- 正在升级; 3- 升级失败; 4- 网络断开，状态未知; 5- 升级文件语言版本不匹配; 7- 升级包类型不匹配; 8- 升级包版本不匹配。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 返回目录  

### 5.31.12 获取远程升级的阶段信息 NET_DVR_GetUpgradeStep  

函  数： LONG NET_DVR_GetUpgradeStep(LONG lUpgradeHandle, LONG \*pSubProgress)  

参  数： [in]lUpgradeHandle NET_DVR_Upgrade 的返回值[in]pSubProgress 升级阶段子进度  

返回值： -1 表示失败，其他值定义如表 5.118 所示。  

表 5.118 升级阶段信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>STEP_RECV_DATA</td><td>1</td><td>接收升级包数据</td></tr><tr><td>STEP_UPGRADE</td><td>2</td><td>升级系统</td></tr><tr><td>STEP_BACKUP</td><td>3</td><td>备份系统</td></tr><tr><td>STEP_SEARCH</td><td>255</td><td>设备正在搜索升级文件</td></tr></table></body></html>  

接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.31.13 关闭远程升级句柄，释放资源 NET_DVR_CloseUpgradeHandle  

函  数： BOOL NET_DVR_CloseUpgradeHandle(LONG lUpgradeHandle)  
参  数： [in]lUpgradeHandle NET_DVR_Upgrade 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 日志查找  

### 5.31.14 查找设备的日志信息 NET_DVR_FindDVRLog_V30  

函  数： LONG NET_DVR_FindDVRLog_V30(LONG lUserID, LONG lSelectMode, DWORD dwMajorType,DWORDdwMinorType, LPNET_DVR_TIME lpStartTime, LPNET_DVR_TIME lpStopTime, BOOL bOnlySmart $=$ FALSE)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lSelectMode 查询方式：0- 全部，1- 按类型，2- 按时间，3- 按时间和类型[in]dwMajorType 日志主类型（S.M.A.R.T 搜索时无效），0 表示全部类型，其他类型定义见表 5.119[in]dwMinorType 日志次类型（S.M.A.R.T 搜索时无效），0 表示全部类型，根据不同的主类型的次类型定义如见表 $5.120^{\sim}$ 表 5.123[in]lpStartTime 文件的开始时间[in]lpStopTime 文件结束时间[in]bOnlySmart 是否只搜索带 S.M.A.R.T 信息的日志  

返回值： -1 表示失败，其他值作为 NET_DVR_FindNextLog_V30 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口如果用于搜索普通日志信息，一般日志设备支持 2000 条，而搜索带 S.M.A.R.T 信息的日志最大只支持 500 条。通常不需要搜索详细的 S.M.A.R.T 信息时，置 bOnlySmart 为 FALSE 即可完成所有日志信息的搜索。  

S.M.A.R.T 信息：硬盘运行日志记录。  

表 5.119 日志主类型  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MAJORALARM</td><td>0x1</td><td>报警</td></tr><tr><td>MAJOR_EXCEPTION</td><td>0x2</td><td>异常</td></tr><tr><td>MAJOR_OPERATION</td><td>0x3</td><td>操作</td></tr><tr><td>MAJOR_INFORMATION</td><td>0x4</td><td>日志附加信息</td></tr></table></body></html>  

表 5.120 报警日志次类型  


<html><body><table><tr><td>主类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MAJOR_ALARM</td><td>0x1</td><td>报警</td></tr><tr><td>次类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MINOR_ALARM_IN</td><td>0x1</td><td>报警输入</td></tr><tr><td>MINOR_ALARM_OUT</td><td>0x2</td><td>报警输出</td></tr><tr><td>MINOR_MOTDET_START</td><td>0x3</td><td>移动侦测报警开始</td></tr><tr><td>MINOR_MOTDET_STOP</td><td>0x4</td><td>移动侦测报警结束</td></tr><tr><td>MINOR_HIDE_ALARM_START</td><td>0x5</td><td>遮挡报警开始</td></tr><tr><td>MINOR_HIDE_ALARM_STOP</td><td>0x6</td><td>遮挡报警结束</td></tr><tr><td>MINOR_VCA_ALARM_START</td><td>0x7</td><td>智能报警开始</td></tr><tr><td>MINOR_VCA_ALARM_STOP</td><td>0x8</td><td>智能报警结束</td></tr><tr><td>MINOR_ITS_ALARM_START</td><td>0x09</td><td>交通事件报警开始</td></tr><tr><td>MINOR_ITS_ALARM_STOP</td><td>0x0a</td><td>交通事件报警结束</td></tr><tr><td>MINOR_NETALARM_START</td><td>0x0b</td><td>网络报警开始</td></tr><tr><td>MINOR_NETALARM_STOP</td><td>0x0c</td><td>网络报警结束</td></tr><tr><td>MINOR_NETALARM_RESUME</td><td>pOxO</td><td>网络报警恢复</td></tr><tr><td>MINOR_WIRELESS_ALARM_START</td><td>Ox0e</td><td>无线报警开始</td></tr><tr><td>MINOR_WIRELESS_ALARM_STOP</td><td>OxOf</td><td>无线报警结束</td></tr><tr><td>MINOR_PIR_ALARM_START</td><td>0x10</td><td>人体感应报警开始</td></tr><tr><td>MINOR_PIR_ALARM_STOP</td><td>0x11</td><td>人体感应报警结束</td></tr><tr><td>MINOR_CALLHELP_ALARM_START</td><td>0x12</td><td>呼救报警开始</td></tr><tr><td>MINOR_CALLHELP_ALARM_STOP</td><td>0x13</td><td>呼救报警结束</td></tr><tr><td>MINOR_DETECTFACE_ALARM_START</td><td>0x16</td><td>人脸侦测报警开始</td></tr><tr><td>MINOR_DETECTFACE_ALARM_STOP</td><td>0x17</td><td>人脸侦测报警结束</td></tr><tr><td></td><td></td><td></td></tr><tr><td>MINOR_VCA_SECNECHANGE_DETECTION</td><td>0x1a</td><td>场景侦测报警</td></tr></table></body></html>  

<html><body><table><tr><td>I_REGION_EXITIN</td><td>0x1b</td><td>离并区域侦测并始</td></tr><tr><td>MINOR_SMART_REGION_EXITING_END</td><td>0x1c</td><td>离开区域侦测结束</td></tr><tr><td>MINOR_SMART_LOITERING_BEGIN</td><td>0x1d</td><td>徘徊侦测开始</td></tr><tr><td>MINOR_SMART_LOITERING_END</td><td>0x1e</td><td>徘徊侦测结束</td></tr><tr><td>MINOR_VCA_ALARM_LINE_DETECTION_BEGIN</td><td>0x20</td><td>越界侦测开始</td></tr><tr><td>MINOR_VCA_ALARM_LINE_DETECTION_END</td><td>0x21</td><td>越界侦测结束</td></tr><tr><td>MINOR_VCA_ALARM_INTRUDE_BEGIN</td><td>0x22</td><td>区域侦测开始</td></tr><tr><td>MINOR_VCA_ALARM_INTRUDE_END</td><td>0x23</td><td>区域侦测结束</td></tr><tr><td>MINOR_VCA_ALARM_AUDIOINPUT</td><td>0x24</td><td>音频异常输入</td></tr><tr><td>MINOR_VCA_ALARM_AUDIOABNORMAL</td><td>0x25</td><td>声强突变</td></tr><tr><td>MINOR_VCA_DEFOCUS_DETECTION_BEGIN</td><td>0x26</td><td>虚焦侦测开始</td></tr><tr><td>MINOR_VCA_DEFOCUS_DETECTION_END</td><td>0x27</td><td>虚焦侦测结束</td></tr><tr><td>MINOR_VCA_FACE_ALARM_BEGIN</td><td>0x29</td><td>人脸侦测开始</td></tr><tr><td>MINOR_SMART_REGION_ENTRANCE_BEGIN</td><td>0x2a</td><td>进入区域侦测开始</td></tr><tr><td>MINOR_SMART_REGION_ENTRANCE_END</td><td>0x2b</td><td>进入区域侦测结束</td></tr><tr><td>MINOR_SMART_PEOPLE_GATHERING_BEGIN</td><td>0x2c</td><td>人员聚集侦测开始</td></tr><tr><td>MINOR_SMART_PEOPLE_GATHERING_END</td><td>0x2d</td><td>人员聚集侦测结束</td></tr><tr><td>MINOR_SMART_FAST_MOVING_BEGIN</td><td>0x2e</td><td>快速运动侦测开始</td></tr><tr><td>MINOR_SMART_FAST_MOVING_END</td><td>0x2f</td><td>快速运动侦测结束</td></tr><tr><td>MINOR_VCA_FACE_ALARM_END</td><td>0x30</td><td>人脸侦测结束</td></tr><tr><td>MINOR_VCA_SCENE_CHANGE_ALARM_BEGIN</td><td>0x31</td><td>场景变更侦测开始</td></tr><tr><td>MINOR_VCA_SCENE_CHANGE_ALARM_END</td><td>0x32</td><td>场景变更侦测结束</td></tr><tr><td>MINOR_VCA_ALARM_AUDIOINPUT_BEGIN</td><td>0x33</td><td>音频异常输入开始</td></tr><tr><td>MINOR_VCA_ALARM_AUDIOINPUT_END</td><td>0x34</td><td>音频异常输入结束</td></tr><tr><td>MINOR_VCA_ALARM_AUDIOABNORMAL_BEGIN</td><td>0x35</td><td>声强突变侦测开始</td></tr><tr><td>MINOR_VCA_ALARM_AUDIOABNORMAL_END</td><td>0x36</td><td>声强突变侦测结束</td></tr><tr><td>MINOR_VCA_ALARM_AUDIOSTEEPDROP</td><td>0x39</td><td>声强陡降</td></tr><tr><td>MINOR_SMART_PARKING_BEGIN</td><td>0x3c</td><td>停车侦测开始</td></tr><tr><td>MINOR_SMART_PARKING_END</td><td>0x3d</td><td>停车侦测结束</td></tr><tr><td>MINOR_SMART_UNATTENDED_BAGGAGE_BEGIN</td><td>0x3e</td><td>物品遗留侦测开始</td></tr><tr><td>MINOR_SMART_UNATTENDED_BAGGAGE_END</td><td>0x3f</td><td>物品遗留侦测结束</td></tr><tr><td>MINOR_SMART_OBJECT_REMOVAL_BEGIN</td><td>0x40</td><td>物品拿取侦测开始</td></tr><tr><td>MINOR_SMART_OBJECT_REMOVAL_END</td><td>0x41</td><td>物品拿取侦测结束</td></tr><tr><td>MINOR_SMART_VEHICLE_ALARM_START</td><td>0x46</td><td>车牌检测开始</td></tr><tr><td>MINOR_SMART_VEHICLE_ALARM_STOP</td><td>0x47</td><td>车牌检测结束</td></tr></table></body></html>  

表 5.121 异常日志次类型  


<html><body><table><tr><td>主类型的宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>MAJOR_EXCEPTION</td><td>0x2</td><td>异常</td></tr><tr><td>次类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MINOR_RAID_ERROR</td><td>0x20</td><td>阵列异常</td></tr><tr><td>MINOR_VI_LOST</td><td>0x21</td><td>视频信号丢失</td></tr><tr><td>MINOR_ILLEGAL_ACCESS</td><td>0x22</td><td>非法访问</td></tr><tr><td>MINOR_HD_FULL</td><td>0x23</td><td>硬盘满</td></tr><tr><td>MINOR_HD_ERROR</td><td>0x24</td><td>硬盘错误</td></tr><tr><td>MINOR_DCD_LOST</td><td>0x25</td><td>MODEM 掉线(保留)</td></tr><tr><td>MINOR_IP_CONFLICT</td><td>0x26</td><td>IP地址冲突</td></tr><tr><td>MINOR_NET_BROKEN</td><td>0x27</td><td>网络断开</td></tr><tr><td>MINOR_REC_ERROR</td><td>0x28</td><td>录像出错</td></tr><tr><td>MINOR_IPC_NO_LINK</td><td>0x29</td><td>IPC 连接异常</td></tr><tr><td>MINOR_VI_EXCEPTION</td><td>0x2a</td><td>视频输入异常(只针对模拟通道)</td></tr><tr><td>MINOR_IPC_IP_CONFLICT</td><td>0x2b</td><td>IPC 的IP 地址冲突</td></tr><tr><td>MINOR_SENCE_EXCEPTION</td><td>0x2c</td><td>场景异常</td></tr><tr><td>MINOR_PIC_REC_ERROR</td><td>0x2d</td><td>抓图出错,获取图片文件失败</td></tr><tr><td>MINOR_VI_MISMATCH</td><td>0x2e</td><td>视频制式不匹配</td></tr><tr><td>MINOR_SDCARD_ABNORMAL</td><td>0x4004</td><td>SD 卡不健康</td></tr><tr><td>MINOR_SDCARD_DAMAGE</td><td>0x4005</td><td>SD卡损坏</td></tr></table></body></html>  

表 5.122 操作日志次类型  


<html><body><table><tr><td>主类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MAJOR_OPERATION</td><td>0x3</td><td>操作</td></tr><tr><td>次类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MINOR_START_DVR</td><td>0x41</td><td>开机</td></tr><tr><td>MINOR_STOP_DVR</td><td>0x42</td><td>关机</td></tr><tr><td>MINOR_STOP_ABNORMAL</td><td>0x43</td><td>异常关机</td></tr><tr><td>MINOR_REBOOT_DVR</td><td>0x44</td><td>本地重启设备</td></tr><tr><td>MINOR_LOCAL_LOGIN</td><td>0x50</td><td>本地登陆</td></tr><tr><td>MINOR_LOCAL_LOGOUT</td><td>0x51</td><td>本地注销登陆</td></tr><tr><td>MINOR_LOCAL_CFG_PARM</td><td>0x52</td><td>本地配置参数</td></tr><tr><td>MINOR_LOCAL_PLAYBYFILE</td><td>0x53</td><td>本地按文件回放或下载</td></tr><tr><td>MINOR_LOCAL_PLAYBYTIME</td><td>0x54</td><td>本地按时间回放或下载</td></tr><tr><td>MINOR_LOCAL_START_REC</td><td>0x55</td><td>本地开始录像</td></tr></table></body></html>  

<html><body><table><tr><td>OP_REC</td><td>0X56</td><td>本地停止录像</td></tr><tr><td>MINOR_LOCAL_PTZCTRL</td><td>0x57</td><td>本地云台控制</td></tr><tr><td>MINOR_LOCAL_PREVIEW</td><td>0x58</td><td>本地预览(保留不使用)</td></tr><tr><td>MINOR_LOCAL_MODIFY_TIME</td><td>0x59</td><td>本地修改时间(保留不使用)</td></tr><tr><td>MINOR_LOCAL_UPGRADE</td><td>0x5a</td><td>本地升级</td></tr><tr><td>MINOR_LOCAL_RECFILE_OUTPUT</td><td>0x5b</td><td>本地备份录象文件</td></tr><tr><td>MINOR_LOCAL_FORMAT_HDD</td><td>0x5c</td><td>本地初始化硬盘</td></tr><tr><td>MINOR_LOCAL_CFGFILE_OUTPUT</td><td>0x5d</td><td>导出本地配置文件</td></tr><tr><td>MINOR_LOCAL_CFGFILE_INPUT</td><td>0x5e</td><td>导入本地配置文件</td></tr><tr><td>MINOR_LOCAL_COPYFILE</td><td>0x5f</td><td>本地备份文件</td></tr><tr><td>MINOR_LOCAL_LOCKFILE</td><td>0x60</td><td>本地锁定录像文件</td></tr><tr><td>MINOR_LOCAL_UNLOCKFILE</td><td>0x61</td><td>本地解锁录像文件</td></tr><tr><td>MINOR_LOCAL_DVR_ALARM</td><td>0x62</td><td>本地手动清除和触发报警</td></tr><tr><td>MINOR_IPC_ADD</td><td>0x63</td><td>本地添加IPC</td></tr><tr><td>MINOR_IPC_DEL</td><td>0x64</td><td>本地删除IPC</td></tr><tr><td>MINOR_IPC_SET</td><td>0x65</td><td>本地设置 IPC</td></tr><tr><td>MINOR_LOCAL_START_BACKUP</td><td>0x66</td><td>本地开始备份</td></tr><tr><td>MINOR_LOCAL_STOP_BACKUP</td><td>0x67</td><td>本地停止备份</td></tr><tr><td>MINOR_LOCAL_COPYFILE_START_TIME</td><td>0x68</td><td>本地备份开始时间</td></tr><tr><td>MINOR_LOCAL_COPYFILE_END_TIME</td><td>0x69</td><td>本地备份结束时间</td></tr><tr><td>MINOR_LOCAL_ADD_NAS</td><td>egxo</td><td>本地添加网络硬盘</td></tr><tr><td>MINOR_LOCAL_DEL_NAS</td><td>0x6b</td><td>本地删除 NAS 盘</td></tr><tr><td>MINOR_LOCAL_SET_NAS</td><td>0x6c</td><td>本地设置 NAS 盘</td></tr><tr><td>MINOR_REMOTE_LOGIN</td><td>0x70</td><td>远程登录</td></tr><tr><td>MINOR_REMOTE_LOGOUT</td><td>0x71</td><td>远程注销登陆</td></tr><tr><td>MINOR_REMOTE_START_REC</td><td>0x72</td><td>远程开始录像</td></tr><tr><td>MINOR_REMOTE_STOP_REC</td><td>0x73</td><td>远程停止录像</td></tr><tr><td>MINOR_START_TRANS_CHAN</td><td>0x74</td><td>开始透明传输</td></tr><tr><td>MINOR_STOP_TRANS_CHAN</td><td>0x75</td><td>停止透明传输</td></tr><tr><td>MINOR_REMOTE_GET_PARM</td><td>0x76</td><td>远程获取参数</td></tr><tr><td>MINOR_REMOTE_CFG_PARM</td><td>0x77</td><td>远程配置参数</td></tr><tr><td>MINOR_REMOTE_GET_STATUS</td><td>0x78</td><td>远程获取状态</td></tr><tr><td>MINOR_REMOTE_ARM</td><td>0x79</td><td>远程布防</td></tr><tr><td>MINOR_REMOTE_DISARM</td><td>0x7a</td><td>远程撤防</td></tr><tr><td>MINOR_REMOTE_REBOOT</td><td>0x7b</td><td>远程重启</td></tr></table></body></html>  

<html><body><table><tr><td></td><td></td><td></td></tr><tr><td>MINOR_STOP_VT</td><td>PLx0</td><td>停止语音对讲</td></tr><tr><td>MINOR_REMOTE_UPGRADE</td><td>0x7e</td><td>远程升级</td></tr><tr><td>MINOR_REMOTE_PLAYBYFILE</td><td>0x7f</td><td>远程按文件回放</td></tr><tr><td>MINOR_REMOTE_PLAYBYTIME</td><td>0x80</td><td>远程按时间回放</td></tr><tr><td>MINOR_REMOTE_PTZCTRL</td><td>0x81</td><td>远程云台控制</td></tr><tr><td>MINOR_REMOTE_FORMAT_HDD</td><td>0x82</td><td>远程格式化硬盘</td></tr><tr><td>MINOR_REMOTE_STOP</td><td>0x83</td><td>远程关机</td></tr><tr><td>MINOR_REMOTE_LOCKFILE</td><td>0x84</td><td>远程锁定文件</td></tr><tr><td>MINOR_REMOTE_UNLOCKFILE</td><td>0x85</td><td>远程解锁文件</td></tr><tr><td>MINOR_REMOTE_CFGFILE_OUTPUT</td><td>0x86</td><td>远程导出配置文件</td></tr><tr><td>MINOR_REMOTE_CFGFILE_INTPUT</td><td>0x87</td><td>远程导入配置文件</td></tr><tr><td>MINOR_REMOTE_RECFILE_OUTPUT</td><td>0x88</td><td>远程导出录象文件</td></tr><tr><td>MINOR_REMOTE_DVR_ALARM</td><td>0x89</td><td>远程手动清除和触发报警</td></tr><tr><td>MINOR_REMOTE_IPC_ADD</td><td>0x8a</td><td>远程添加IPC</td></tr><tr><td>MINOR_REMOTE_IPC_DEL</td><td>0x8b</td><td>远程删除IPC</td></tr><tr><td>MINOR_REMOTE_IPC_SET</td><td>0x8c</td><td>远程设置IPC</td></tr><tr><td>MINOR_REBOOT_VCA_LIB</td><td>0x8d</td><td>重启智能库</td></tr><tr><td>MINOR_REMOTE_ADD_NAS</td><td>0x8e</td><td>远程添加NAS 盘</td></tr><tr><td>MINOR_REMOTE_DEL_NAS</td><td>Ox8f</td><td>远程删除 NAS 盘</td></tr><tr><td>MINOR_REMOTE_SET_NAS</td><td>0x90</td><td>远程设置 NAS 盘</td></tr><tr><td>MINOR_LOCAL_START_REC_CDRW</td><td>0x91</td><td>本地开始刻录</td></tr><tr><td>MINOR_LOCAL_STOP_REC_CDRW</td><td>0x92</td><td>本地停止刻录</td></tr><tr><td>MINOR_REMOTE_START_REC_CDRW</td><td>0x93</td><td>远程开始刻录</td></tr><tr><td>MINOR_REMOTE_STOP_REC_CDRW</td><td>0x94</td><td>远程停止刻录</td></tr><tr><td>MINOR_LOCAL_PIC_OUTPUT</td><td>0x95</td><td>本地备份图片文件</td></tr><tr><td>MINOR_REMOTE_SET_NAS</td><td>0x96</td><td>远程备份图片文件</td></tr><tr><td>MINOR_LOCAL_INQUEST_RESUME</td><td>0x97</td><td>本地恢复审讯事件</td></tr><tr><td>MINOR_REMOTE_INQUEST_RESUME</td><td>0x98</td><td>远程恢复审讯事件</td></tr><tr><td>MINOR_REMOTE_BYPASS</td><td>opxo</td><td>远程旁路</td></tr><tr><td>MINOR_REMOTE_UNBYPASS</td><td>0xd1</td><td>远程旁路恢复</td></tr><tr><td>MINOR_REMOTE_SET_ALARMIN_CFG</td><td>0xd2</td><td>远程设置报警输入参数</td></tr><tr><td>MINOR_REMOTE_GET_ALARMIN_CFG</td><td>0xd3</td><td>远程获取报警输入参数</td></tr><tr><td>MINOR_REMOTE_SET_ALARMOUT_CFG</td><td>0xd4</td><td>远程设置报警输出参数</td></tr><tr><td>MINOR_REMOTE_GET_ALARMOUT_CFG</td><td>0xd5</td><td>远程获取报警输出参数</td></tr></table></body></html>  

<html><body><table><tr><td></td><td>gnxo</td><td></td></tr><tr><td>MINOR_REMOTE_ALARMOUT_CLOSE_MAN</td><td>Lpxo</td><td>远程手动关闭报警输出</td></tr><tr><td>MINOR_REMOTE_ALARM_ENABLE_CFG</td><td>0xd8</td><td>远程设置报警主机的RS485串口使能状态</td></tr><tr><td>MINOR_DBDATA_OUTPUT</td><td>6px0</td><td>导出数据库记录</td></tr><tr><td>MINOR_DBDATA_INPUT</td><td>Oxda</td><td>导入数据库记录</td></tr><tr><td>MINOR_MU_SWITCH</td><td>Oxdb</td><td>级联切换</td></tr><tr><td>MINOR_MU_PTZ</td><td>Oxdc</td><td>级联 PTZ 控制</td></tr><tr><td>MINOR_LOCAL_CONF_REB_RAID</td><td>0x101</td><td>本地配置自动重建</td></tr><tr><td>MINOR_LOCAL_CONF_SPARE</td><td>0x102</td><td>本地配置热备</td></tr><tr><td>MINOR_LOCAL_ADD_RAID</td><td>0x103</td><td>本地创建阵列</td></tr><tr><td>MINOR_LOCAL_DEL_RAID</td><td>0x104</td><td>本地删除阵列</td></tr><tr><td>MINOR_LOCAL_MIG_RAID</td><td>0x105</td><td>本地迁移阵列</td></tr><tr><td>MINOR_LOCAL_REB_RAID</td><td>0x106</td><td>本地手动重建阵列</td></tr><tr><td>MINOR_LOCAL_QUICK_CONF_RAID</td><td>0x107</td><td>本地一键配置</td></tr><tr><td>MINOR_LOCAL_ADD_VD</td><td>0x108</td><td>本地创建虚拟磁盘</td></tr><tr><td>MINOR_LOCAL_DEL_VD</td><td>0x109</td><td>本地删除虚拟磁盘</td></tr><tr><td>MINOR_LOCAL_RP_VD</td><td>0x10a</td><td>本地修复虚拟磁盘</td></tr><tr><td>MINOR_LOCAL_FORMAT_EXPANDVD</td><td>0x10b</td><td>本地扩展虚拟磁盘扩容</td></tr><tr><td>MINOR_LOCAL_RAID_UPGRADE</td><td>0x10c</td><td>本地 raid 卡升级</td></tr><tr><td>MINOR_LOCAL_STOP_RAID</td><td>0x10d</td><td>本地暂停 RAID 操作(即安全拔盘)</td></tr><tr><td>MINOR_REMOTE_CONF_REB_RAID</td><td>0x111</td><td>远程配置自动重建</td></tr><tr><td>MINOR_REMOTE_CONF_SPARE</td><td>0x112</td><td>远程配置热备</td></tr><tr><td>MINOR_REMOTE_ADD_RAID</td><td>0x113</td><td>远程创建阵列</td></tr><tr><td>MINOR_REMOTE_DEL_RAID</td><td>0x114</td><td>远程删除阵列</td></tr><tr><td>MINOR_REMOTE_MIG_RAID</td><td>0x115</td><td>远程迁移阵列</td></tr><tr><td>MINOR_REMOTE_REB_RAID</td><td>0x116</td><td>远程手动重建阵列</td></tr><tr><td>MINOR_REMOTE_QUICK_CONF_RAID</td><td>0x117</td><td>远程一键配置</td></tr><tr><td>MINOR_REMOTE_ADD_VD</td><td>0x118</td><td>远程创建虚拟磁盘</td></tr><tr><td>MINOR_REMOTE_DEL_VD</td><td>0x119</td><td>远程删除虚拟磁盘</td></tr><tr><td>MINOR_REMOTE_RP_VD</td><td>0x11a</td><td>远程修复虚拟磁盘</td></tr><tr><td>MINOR_REMOTE_FORMAT_EXPANDVD</td><td>0x11b</td><td>远程虚拟磁盘扩容</td></tr><tr><td>MINOR_REMOTE_RAID_UPGRADE</td><td>0x11c</td><td>远程raid 卡升级</td></tr><tr><td>MINOR_REMOTE_STOP_RAID</td><td>0x11d</td><td>远程暂停 RAID 操作(即安全拔盘)</td></tr><tr><td>MINOR_LOCAL_START_PIC_REC</td><td>0x121</td><td>本地开始抓图</td></tr><tr><td>MINOR_LOCAL_STOP_PIC_REC</td><td>0x122</td><td>本地停止抓图</td></tr></table></body></html>  

<html><body><table><tr><td>MINOR_LOCAL_SET_SNMP</td><td>0x125</td><td>本地配置SNMP</td></tr><tr><td>MINOR_LOCAL_TAG_OPT</td><td>0x126</td><td>本地标签操作</td></tr><tr><td>MINOR_REMOTE_START_PIC_REC</td><td>0x131</td><td>远程开始抓图</td></tr><tr><td>MINOR_REMOTE_STOP_PIC_REC</td><td>0x132</td><td>远程停止抓图</td></tr><tr><td>MINOR_REMOTE_SET_SNMP</td><td>0x135</td><td>远程配置SNMP</td></tr><tr><td>MINOR_REMOTE_TAG_OPT</td><td>0x136</td><td>远程标签操作</td></tr><tr><td>MINOR_REMOTE_TAG_OPT</td><td>0x136</td><td>远程标签操作</td></tr><tr><td>MINOR_LOCAL_VOUT_SWITCH</td><td>0x140</td><td>本地输出口切换操作</td></tr><tr><td>MINOR_REMOTE_MODIFY_VERIFICATION_CODE</td><td>0x157</td><td>修改平台的验证码</td></tr></table></body></html>  

表 5.123 附加日志次类型  


<html><body><table><tr><td>主类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MAJOR_INFORMATION</td><td>0x4</td><td>附加信息</td></tr><tr><td>次类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MINOR_HDD_INFO</td><td>0xa1</td><td>硬盘信息</td></tr><tr><td>MINOR_SMART_INFO</td><td>0xa2</td><td>S.M.A.R.T信息</td></tr><tr><td>MINOR_REC_START</td><td>0xa3</td><td>开始录像</td></tr><tr><td>MINOR_REC_STOP</td><td>0xa4</td><td>停止录像</td></tr><tr><td>MINOR_REC_OVERDUE</td><td>0xa5</td><td>过期录像删除</td></tr><tr><td>MINOR_LINK_START</td><td>0xa6</td><td>连接前端设备</td></tr><tr><td>MINOR_LINK_STOP</td><td>0xa7</td><td>断开前端设备</td></tr><tr><td>MINOR_NET_DISK_INFO</td><td>0xa8</td><td>网络硬盘信息</td></tr><tr><td>MINOR_RAID_INFO</td><td>0xa9</td><td>raid 相关信息</td></tr><tr><td>MINOR_PIC_REC_START</td><td>0xb3</td><td>开始抓图</td></tr><tr><td>MINOR_PIC_REC_STOP</td><td>0xb4</td><td>停止抓图</td></tr><tr><td>MINOR_PIC_REC_OVERDUE</td><td>0xb5</td><td>过期图片文件删除</td></tr></table></body></html>  

### 5.31.15 逐条获取查找到的日志信息 NET_DVR_FindNextLog_V30  

函  数： LONG NET_DVR_FindNextLog_V30(LONG lLogHandle, LPNET_DVR_LOG_V30 lpLogData)  
参  数： [in]lLogHandle 日志查找句柄，NET_DVR_FindDVRLog_V30()的返回值[out]lpLogData 保存日志信息的指针  
返回值： -1 表示失败，其他值表示当前的获取状态等信息。接口返回失败请调用 NET_DVR_GetLastError获取错误码，通过错误码判断出错原因。  
说  明： 在调用该接口获取查找日志之前，必须先调用 NET_DVR_FindDVRLog_V30 得到当前的查找句柄。  

### 5.31.16 释放查找日志的资源 NET_DVR_FindLogClose_V30  

函  数： BOOL  NET_DVR_FindLogClose_V30(LONG lLogHandle)  
参  数： [in]lLogHandle 日志查找句柄，NET_DVR_FindDVRLog_V30 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 恢复设备默认参数  

### 5.31.17 恢复设备默认参数 NET_DVR_RestoreConfig  

函  数： BOOL NET_DVR_RestoreConfig(LONG lUserID)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 返回目录  

### 5.31.18 完全恢复出厂默认参数 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 控制命令，详见表 5.124[in] lpInBuffer 输入参数，跟控制命令相关，详见列表[in] dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.124 所示。  

表 5.124 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>lplnBuffer对应结构体</td></tr><tr><td>NETDVRCOMPLETERESTORECTRL</td><td>3420</td><td>设置完全恢复出厂值</td><td>NETDVRCOMPLETERESTORE_INFO</td></tr><tr><td>NETDVRCONTROLRESTORESUPPORT</td><td>3311</td><td>快球恢复前端默认参数</td><td>NETDVRREMOTECONTROLSTUDY_PARAM</td></tr></table></body></html>  

### 导入/导出配置文件  

### 5.31.19 导出配置文件 NET_DVR_GetConfigFile_V30  

函  数： BOOL NET_DVR_GetConfigFile_V30(LONG lUserID, char \*sOutBuffer, DWORD dwOutSize, DWORD\*pReturnSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[out] sOutBuffer 存放配置参数的缓冲区[in]dwOutSize 缓冲区大小[out]pReturnSize 实际获得的缓冲区大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 当 sOutBuffer $=$ NULL、dwOutSize ${}=0$ 且 pReturnSize $!=$ NULL 时用于获取参数配置文件的所需的缓冲区长度；当 sOutBuffer $!=$ NULL 且 dwOutSize $\mathrel{\mathop:}$ 时用于获取参数配置文件的所需的缓冲区内容。  

### 5.31.20 导出配置文件 NET_DVR_GetConfigFile  

函  数： BOOL NET_DVR_GetConfigFile(LONG lUserID, char \*sFileName)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]sFileName 存放保存配置文件的文件路径（二进制文件）  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.31.21 导入配置文件 NET_DVR_SetConfigFile_EX  

函  数： BOOL NET_DVR_SetConfigFile_EX(LONG lUserID, char \*sInBuffer, DWORD dwInSize)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]sInBuffer 存放配置参数的缓冲区[in]dwInSize 缓冲区大小  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.31.22 导入配置文件 NET_DVR_SetConfigFile  

函  数： BOOL NET_DVR_SetConfigFile(LONG lUserID, char \*sFileName)参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  

[in]sFileName 存放保存配置文件的文件路径（二进制文件）返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 关机和重启  

### 5.31.23 重启设备 NET_DVR_RebootDVR  

函  数： BOOL NET_DVR_RebootDVR(LONG lUserID)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.31.24 关闭设备 NET_DVR_ShutDownDVR  

函  数： BOOL NET_DVR_ShutDownDVR(LONG lUserID)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

# 6 错误代码及说明  

## 6.1 网络通讯库错误码  

<html><body><table><tr><td>错误名称</td><td>错误值</td><td>说明</td></tr><tr><td>NET_DVR_NOERROR</td><td>0</td><td>没有错误。</td></tr><tr><td>NET_DVR_PASSWORD_ERROR</td><td>1</td><td>用户名密码错误。注册时输入的用户名或者密码错误。</td></tr><tr><td>NET_DVR_NOENOUGHPRI</td><td>2</td><td>权限不足。该注册用户没有权限执行当前对设备的操 作，可以与远程用户参数配置做对比。</td></tr><tr><td>NET_DVR_NOINIT</td><td>3</td><td>SDK 未初始化。</td></tr><tr><td>NET_DVR_CHANNEL_ERROR</td><td>4</td><td>通道号错误。设备没有对应的通道号。</td></tr><tr><td>NET_DVR_OVER_MAXLINK</td><td>5</td><td>连接到设备的用户个数超过最大。</td></tr><tr><td>NET_DVR_VERSIONNOMATCH</td><td>6</td><td>版本不匹配。SDK和设备的版本不匹配。</td></tr><tr><td>NET_DVR_NETWORK_FAIL_CONNECT</td><td>7</td><td>连接设备失败。设备不在线或网络原因引起的连接超</td></tr><tr><td>NET_DVR_NETWORK_SEND_ERROR</td><td>8</td><td>时等。 向设备发送失败。</td></tr><tr><td>NET_DVR_NETWORK_RECV_ERROR</td><td>6</td><td>从设备接收数据失败。</td></tr><tr><td>NET_DVR_NETWORK_RECV_TIMEOUT</td><td>10</td><td>从设备接收数据超时。</td></tr><tr><td>NET_DVR_NETWORK_ERRORDATA</td><td>11</td><td>传送的数据有误。发送给设备或者从设备接收到的数</td></tr><tr><td>NET_DVR_ORDER_ERROR</td><td>12</td><td>据错误，如远程参数配置时输入设备不支持的值。 调用次序错误。</td></tr><tr><td>NET_DVR_OPERNOPERMIT</td><td>13</td><td>无此权限。</td></tr><tr><td>NET_DVR_COMMANDTIMEOUT</td><td>14</td><td>设备命令执行超时。</td></tr><tr><td>NET_DVR_ERRORSERIALPORT</td><td>15</td><td>串口号错误。指定的设备串口号不存在。</td></tr><tr><td>NET_DVR_ERRORALARMPORT</td><td>16</td><td>报警端口错误。指定的设备报警输出端口不存在。</td></tr><tr><td>NET_DVR_PARAMETER_ERROR</td><td>17</td><td>参数错误。SDK接口中给入的输入或输出参数为空。</td></tr><tr><td>NET_DVR_CHAN_EXCEPTION</td><td>18</td><td>设备通道处于错误状态</td></tr><tr><td>NET_DVR_NODISK</td><td>19</td><td>设备无硬盘。当设备无硬盘时，对设备的录像文件、</td></tr><tr><td>NET_DVR_ERRORDISKNUM</td><td>20</td><td>硬盘配置等操作失败。 硬盘号错误。当对设备进行硬盘管理操作时，指定的</td></tr><tr><td>NET_DVR_DISK_FULL</td><td>21</td><td>硬盘号不存在时返回该错误。 设备硬盘满。</td></tr><tr><td>NET_DVR_DISK_ERROR</td><td>22</td><td>设备硬盘出错</td></tr><tr><td>NET_DVR_NOSUPPORT</td><td>23</td><td>设备不支持。</td></tr><tr><td>NET_DVR_BUSY</td><td>24</td><td>设备忙。</td></tr><tr><td>NET_DVR_MODIFY_FAIL</td><td>25</td><td>设备修改不成功。</td></tr><tr><td>NET_DVR_PASSWORD_FORMAT_ERROR</td><td>26</td><td>密码输入格式不正确</td></tr><tr><td>NET_DVR_DISK_FORMATING</td><td>27</td><td>硬盘正在格式化，不能启动操作。</td></tr><tr><td>NET_DVR_DVRNORESOURCE</td><td>28</td><td>设备资源不足。</td></tr><tr><td>NET_DVR_DVROPRATEFAILED</td><td>29</td><td>设备操作失败。</td></tr><tr><td>NET_DVR_OPENHOSTSOUND_FAIL</td><td>30</td><td>语音对讲、语音广播操作中采集本地音频或打开音频</td></tr><tr><td></td><td></td><td>输出失败。</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_DVRVOICEOPENED</td><td>31</td><td>设备语音对讲被占用。</td></tr><tr><td>NET_DVR_TIMEINPUTERROR</td><td>32</td><td>时间输入不正确。</td></tr><tr><td>NET_DVR_NOSPECFILE</td><td>33</td><td>回放时设备没有指定的文件。</td></tr><tr><td>NET_DVR_CREATEFILE_ERROR</td><td>34</td><td>创建文件出错。本地录像、保存图片、获取配置文件 和远程下载录像时创建文件失败。</td></tr><tr><td>NET_DVR_FILEOPENFAIL</td><td>35</td><td>打开文件出错。设置配置文件、设备升级、上传审讯</td></tr><tr><td>NET_DVR_OPERNOTFINISH</td><td>36</td><td>文件时打开文件失败。 上次的操作还没有完成</td></tr><tr><td>NET_DVR_GETPLAYTIMEFAIL</td><td>37</td><td>获取当前播放的时间出错。</td></tr><tr><td>NET_DVR_PLAYFAIL</td><td>38</td><td>播放出错。</td></tr><tr><td>NET_DVR_FILEFORMAT_ERROR</td><td>39</td><td>文件格式不正确。</td></tr><tr><td>NET_DVR_DIR_ERROR</td><td>40</td><td>路径错误</td></tr><tr><td>NET_DVR_ALLOC_RESOURCE_ERROR</td><td>41</td><td>SDK资源分配错误。</td></tr><tr><td>NET_DVR_AUDIO_MODE_ERROR</td><td>42</td><td>声卡模式错误。当前打开声音播放模式与实际设置的</td></tr><tr><td>NET_DVR_NOENOUGH_BUF</td><td>43</td><td>模式不符出错。 缓冲区太小。接收设备数据的缓冲区或存放图片缓冲</td></tr><tr><td>NET_DVR_CREATESOCKET_ERROR</td><td>44</td><td>区不足。 创建 SOCKET 出错。</td></tr><tr><td>NET_DVR_SETSOCKET_ERROR</td><td>45</td><td>设置 SOCKET 出错。</td></tr><tr><td>NET_DVR_MAX_NUM</td><td>46</td><td>个数达到最大。分配的注册连接数、预览连接数超过</td></tr><tr><td>NET_DVR_USERNOTEXIST</td><td>47</td><td>SDK支持的最大数。 用户不存在。注册的用户ID已注销或不可用。</td></tr><tr><td>NET_DVR_WRITEFLASHERROR</td><td>48</td><td>写FLASH 出错。设备升级时写FLASH失败。</td></tr><tr><td>NET_DVR_UPGRADEFAIL</td><td>49</td><td>设备升级失败。网络或升级文件语言不匹配等原因升</td></tr><tr><td>NET_DVR_CARDHAVEINIT</td><td>50</td><td>级失败。 解码卡已经初始化过。</td></tr><tr><td>NET_DVR_PLAYERFAILED</td><td>51</td><td>调用播放库中某个函数失败。</td></tr><tr><td>NET_DVR_MAX_USERNUM</td><td>52</td><td>登录设备的用户数达到最大。</td></tr><tr><td>NET_DVR_GETLOCALIPANDMACFAIL</td><td>53</td><td>获得本地 PC的IP地址或物理地址失败。</td></tr><tr><td>NET_DVR_NOENCODEING</td><td>54</td><td>设备该通道没有启动编码。</td></tr><tr><td>NET_DVR_IPMISMATCH</td><td>55</td><td>IP地址不匹配。</td></tr><tr><td>NET_DVR_MACMISMATCH</td><td>56</td><td>MAC地址不匹配。</td></tr><tr><td>NET_DVR_UPGRADELANGMISMATCH</td><td>57</td><td>升级文件语言不匹配。</td></tr><tr><td>NET_DVR_MAX_PLAYERPORT</td><td>58</td><td>播放器路数达到最大。</td></tr><tr><td>NET_DVR_NOSPACEBACKUP</td><td>59</td><td>备份设备中没有足够空间进行备份。</td></tr><tr><td>NET_DVR_NODEVICEBACKUP</td><td>60</td><td>没有找到指定的备份设备。</td></tr><tr><td>NET_DVR_PICTURE_BITS_ERROR</td><td>61</td><td>图像素位数不符，限24色。</td></tr><tr><td>NET_DVR_PICTURE_DIMENSION_ERROR</td><td>62</td><td>图片高*宽超限，限128*256。</td></tr><tr><td>NET_DVR_PICTURE_SIZ_ERROR</td><td>63</td><td>图片大小超限，限100K。</td></tr><tr><td>NET_DVR_LOADPLAYERSDKFAILED</td><td>64</td><td>载入当前目录下PlayerSdk出错。</td></tr><tr><td></td><td></td><td></td></tr><tr><td>NET_DVR_LOADPLAYERSDKPROC_ERROR NET_DVR_LOADDSSDKFAILED</td><td>65 66</td><td>找不到 Player Sdk 中某个函数入口。 载入当前目录下DSsdk出错。</td></tr><tr><td>NET_DVR_LOADDSSDKPROC_ERROR</td><td>67</td><td>找不到DsSdk中某个函数入口。</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_DSSDK_ERROR</td><td>68</td><td>调用硬解码库DsSdk中某个函数失败。</td></tr><tr><td>NET_DVR_VOICEMONOPOLIZE</td><td>69</td><td>声卡被独占。</td></tr><tr><td>NET_DVR_JOINMULTICASTFAILED</td><td>70</td><td>加入多播组失败。</td></tr><tr><td>NET_DVR_CREATEDIR_ERROR</td><td>71</td><td>建立日志文件目录失败。</td></tr><tr><td>NET_DVR_BINDSOCKET_ERROR</td><td>72</td><td>绑定套接字失败。</td></tr><tr><td>NET_DVR_SOCKETCLOSE_ERROR</td><td>73</td><td>socket 连接中断，此错误通常是由于连接中断或目的</td></tr><tr><td>NET_DVR_USERID_ISUSING</td><td>74</td><td>地不可达。 注销时用户ID正在进行某操作。</td></tr><tr><td>NET_DVR_SOCKETLISTEN_ERROR</td><td>75</td><td>监听失败。</td></tr><tr><td>NET_DVR_PROGRAM_EXCEPTION</td><td>76</td><td>程序异常。</td></tr><tr><td>NET_DVR_WRITEFILE_FAILED</td><td>77</td><td>写文件失败。本地录像、远程下载录像、下载图片等</td></tr><tr><td>NET_DVR_FORMAT_READONLY</td><td>78</td><td>操作时写文件失败。 禁止格式化只读硬盘。</td></tr><tr><td>NET_DVR_WITHSAMEUSERNAME</td><td>79</td><td>远程用户配置结构中存在相同的用户名。</td></tr><tr><td>NET_DVR_DEVICETYPE_ERROR</td><td>80</td><td>导入参数时设备型号不匹配。</td></tr><tr><td>NET_DVR_LANGUAGE_ERROR</td><td>81</td><td>导入参数时语言不匹配。</td></tr><tr><td>NET_DVR_PARAVERSION_ERROR</td><td>82</td><td>导入参数时软件版本不匹配。</td></tr><tr><td>NET_DVR_IPCHAN_NOTALIVE</td><td>83</td><td>预览时外接IP 通道不在线。</td></tr><tr><td>NET_DVR_RTSP_SDK_ERROR</td><td>84</td><td>加载标准协议通讯库 StreamTransClient失败。</td></tr><tr><td>NET_DVR_CONVERT_SDK_ERROR</td><td>85</td><td>加载转封装库失败。</td></tr><tr><td>NET_DVR_IPC_COUNT_OVERFLOW</td><td>86</td><td>超出最大的IP接入通道数。</td></tr><tr><td>NET_DVR_MAX_ADD_NUM</td><td>87</td><td>添加录像标签或者其他操作超出最多支持的个数。</td></tr><tr><td>NET_DVR_PARAMMODE_ERROR</td><td>88</td><td>图像增强仪，参数模式错误（用于硬件设置时，客户</td></tr><tr><td>NET_DVR_CODESPITTER_OFFLINE</td><td>89</td><td>端进行软件设置时错误值)。 码分器不在线。</td></tr><tr><td>NET_DVR_BACKUP_COPYING</td><td>90</td><td>设备正在备份。</td></tr><tr><td>NET_DVR_CHAN_NOTSUPPORT</td><td>91</td><td>通道不支持该操作。</td></tr><tr><td>NET_DVR_CALLINEINVALID</td><td>92</td><td>高度线位置太集中或长度线不够倾斜。</td></tr><tr><td>NET_DVR_CALCANCELCONFLICT</td><td>93</td><td>取消标定冲突，如果设置了规则及全局的实际大小尺</td></tr><tr><td>NET_DVR_CALPOINTOUTRANGE</td><td>94</td><td>寸过滤。 标定点超出范围。</td></tr><tr><td>NET_DVR_FILTERRECTINVALID</td><td>95</td><td>尺寸过滤器不符合要求。</td></tr><tr><td>NET_DVR_DDNS_DEVOFFLINE</td><td>96</td><td>设备没有注册到ddns 上。</td></tr><tr><td>NET_DVR_DDNS_INTER_ERROR</td><td>97</td><td>DDNS服务器内部错误。</td></tr><tr><td>NET_DVR_INTERCOM_SDK_ERROR</td><td>100</td><td>加载当前目录下的语音对讲库失败。</td></tr><tr><td>NET_DVR_NO_CURRENT_UPDATEFILE</td><td>101</td><td>没有正确的升级包。</td></tr><tr><td>NET_DVR_ALIAS_DUPLICATE</td><td>150</td><td>别名重复（EasyDDNS的配置）</td></tr><tr><td>NET_ERR_USERNAME_LOCKED</td><td>153</td><td>用户名被锁定。</td></tr><tr><td>NET_DVR_TEST_SERVER_FAIL_CONNECT</td><td>165</td><td>连接测试服务器失败。</td></tr><tr><td>NET_DVR_NAS_SERVER_INVALID_DIR</td><td>166</td><td>NAS服务器挂载目录失败，目录无效或者用户名密码</td></tr><tr><td>NET_DVR_NAS_SERVER_NOENOUGH_PRI</td><td>167</td><td>错误。 NAS服务器挂载目录失败，没有权限。</td></tr><tr><td>NET_DVR_EMAIL_SERVER_NOT_CONFIG_DNS</td><td>168</td><td>服务器使用域名，但是没有配置DNS，可能造成域名 无效。</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_EMAIL_SERVER_NOT_CONFIG_GATEWAY</td><td>169</td><td>没有配置网关，可能造成发送邮件失败。</td></tr><tr><td>NET_DVR_TEST_SERVER_PASSWORD_ERROR</td><td>170</td><td>用户名密码不正确，测试服务器的用户名或密码错误。</td></tr><tr><td>NET_DVR_EMAIL_SERVER_CONNECT_EXCEPTION_WITH_SMTP</td><td>171</td><td>设备和smtp服务器交互异常。</td></tr><tr><td>NET_DVR_FTP_SERVER_FAIL_CREATE_DIR</td><td>172</td><td>FTP服务器创建目录失败。</td></tr><tr><td>NET_DVR_FTP_SERVER_NO_WRITE_PIR</td><td>173</td><td>FTP服务器没有写入权限。</td></tr><tr><td>NET_DVR_IP_CONFLICT</td><td>174</td><td>IP冲突。</td></tr><tr><td>NET_ERR_ANR_ARMING_EXIST</td><td>178</td><td>断网续传布防连接已经存在（私有SDK协议布防连接 已经建立的情况下，重复布防且选择断网续传功能时</td></tr><tr><td>NET_ERR_UPLOADLINK_EXIST</td><td>179</td><td>返回该错误)。 断网续传上传连接已经存在（EHOME协议和私有SDK 协议不能同时支持断网续传，其中一种协议已经建议</td></tr><tr><td>NET_ERR_MAX_HRUDP_LINK</td><td>182</td><td>连接，另外一个连接建立时返回该错误)。 HRUDP连接数超过设备限制。</td></tr><tr><td>NET_DVR_FUNCTION_RESOURCE_USAGE_ERROR</td><td>791</td><td>设备其它功能占用资源，导致该功能无法开启。</td></tr><tr><td>NET_DVR_DEV_NET_OVERFLOW</td><td>800</td><td>网络流量超过设备能力上限</td></tr><tr><td>NET_DVR_STATUS_RECORDFILE_WRITING_NOT_LOCK</td><td>801</td><td>录像文件在录像，无法被锁定</td></tr><tr><td>NET_DVR_STATUS_CANT_FORMAT_LITTLE_DISK</td><td>802</td><td>由于硬盘太小无法格式化</td></tr><tr><td>NET_DVR_CHECK_PASSWORD_MISTAKE_ERROR</td><td>834</td><td></td></tr><tr><td>NET_ERR_TRANS_CHAN_START</td><td>1101</td><td>校验密码错误。</td></tr><tr><td>NET_ERR_DEV_UPGRADING</td><td></td><td>透明通道已打开，当前操作无法完成。</td></tr><tr><td>NET_ERR_MISMATCH_UPGRADE_PACK_TYPE</td><td>1102</td><td>设备正在升级</td></tr><tr><td></td><td>1103</td><td>升级包类型不匹配</td></tr><tr><td>NET_ERR_DEV_FORMATTING</td><td>1104</td><td>设备正在格式化</td></tr><tr><td>NET_ERR_MISMATCH_UPGRADE_PACK_VERSION</td><td>1105</td><td>升级包版本不匹配</td></tr><tr><td>NET_DVR_ERR_ILLEGAL_VERIFICATION_CODE</td><td>1111</td><td>验证码不合法，请修改验证码</td></tr><tr><td>NET_DVR_ERR_LACK_VERIFICATION_CODE</td><td>1112</td><td>缺少验证码，请输入验证码</td></tr><tr><td>能力集错误码</td><td></td><td></td></tr><tr><td>XML_ABILITY_NOTSUPPORT</td><td>1000</td><td>不支持能力节点获取。</td></tr><tr><td>XML_ANALYZE_NOENOUGH_BUF</td><td>1001</td><td>输出内存不足。</td></tr><tr><td>XML_ANALYZE_FIND_LOCALXML_ERROR</td><td>1002</td><td>无法找到对应的本地xml。</td></tr><tr><td>XML_ANALYZE_LOAD_LOCALXML_ERROR</td><td>1003</td><td>加载本地xml 出错。</td></tr><tr><td>XML_NANLYZE_DVR_DATA_FORMAT_ERROR</td><td>1004</td><td>设备能力数据格式错误。</td></tr><tr><td>XML_ANALYZE_TYPE_ERROR</td><td>1005</td><td>能力集类型错误。</td></tr><tr><td>XML_ANALYZE_XML_NODE_ERROR</td><td>1006</td><td>XML能力节点格式错误。</td></tr><tr><td>XML_INPUT_PARAM_ERROR</td><td>1007</td><td>输入的能力XML节点值错误。</td></tr><tr><td>XML_VERSION_MISMATCH</td><td>1008</td><td>XML版本不匹配。</td></tr></table></body></html>  

## 6.2 RTSP 通讯库错误码  

<html><body><table><tr><td>错误名称</td><td>错误值</td><td>说明</td></tr><tr><td>NETDVRRTSPERRORNOENOUGHPRI</td><td>401</td><td>无权限：服务器返回401时，转成这个错误码</td></tr><tr><td>NET_DVR_RTSP_ERRORALLOCRESOURCE</td><td>402</td><td>分配资源失败</td></tr><tr><td>NETDVRRTSPERRORPARAMETER</td><td>403</td><td>参数错误</td></tr><tr><td>NET_DVR_RTSP_ERROR_NO_URL</td><td>404</td><td>指定的URL地址不存在：服务器返回404时，转成这个</td></tr></table></body></html>  

<html><body><table><tr><td></td><td></td><td>错误码，例如请求不可用的通道号预览、请求不支持子 码流的通道预览</td></tr><tr><td>NET_DVR_RTSP_ERROR_FORCE_STOP</td><td>406</td><td>用户中途强行退出</td></tr><tr><td>NET_DVR_RTSP_GETPORTFAILED</td><td>407</td><td>获取RTSP端口错误</td></tr><tr><td>NET_DVR_RTSP_DESCRIBERROR</td><td>410</td><td>RTSPDECRIBE交互错误</td></tr><tr><td>NET_DVR_RTSP_DESCRIBESENDTIMEOUT</td><td>411</td><td>RTSPDECRIBE发送超时</td></tr><tr><td>NET_DVR_RTSP_DESCRIBESENDERROR</td><td>412</td><td>RTSPDECRIBE发送失败</td></tr><tr><td>NET_DVR_RTSP_DESCRIBERECVTIMEOUT</td><td>413</td><td>RTSPDECRIBE接收超时</td></tr><tr><td>NET_DVR_RTSP_DESCRIBERECVDATALOST</td><td>414</td><td>RTSPDECRIBE接收数据错误</td></tr><tr><td>NET_DVR_RTSP_DESCRIBERECVERROR</td><td>415</td><td>RTSPDECRIBE接收失败</td></tr><tr><td>NET_DVR_RTSP_DESCRIBESERVERERR</td><td>416</td><td>RTSPDECRIBE服务器返回错误状态。例如服务器返回 400，可能是不支持子码流</td></tr><tr><td>NET_DVR_RTSP_SETUPERROR</td><td>420</td><td>RTSPSETUP交互错误，一般是服务器返回的码流地址无 法连接上，或者被服务器拒绝。（老版本的SDK可能返</td></tr><tr><td>NET_DVR_RTSP_SETUPSENDTIMEOUT</td><td>421</td><td>回错误号 419，为同样的错误原因) RTSPSETUP发送超时</td></tr><tr><td>NET_DVR_RTSP_SETUPSENDERROR</td><td>422</td><td>RTSPSETUP发送错误</td></tr><tr><td>NET_DVR_RTSP_SETUPRECVTIMEOUT</td><td>423</td><td>RTSPSETUP接收超时</td></tr><tr><td>NET_DVR_RTSP_SETUPRECVDATALOST</td><td>424</td><td>RTSPSETUP接收数据错误</td></tr><tr><td>NET_DVR_RTSP_SETUPRECVERROR</td><td>425</td><td>RTSPSETUP接收失败</td></tr><tr><td>NET_DVR_RTSP_OVER_MAX_CHAN</td><td>426</td><td>超过服务器最大连接数，或者服务器资源不足，服务器</td></tr><tr><td>NET_DVR_RTSP_SETUPSERVERERR</td><td>427</td><td>返回453时，转成这个错误码 RTSPSETUP服务器返回错误状态</td></tr><tr><td>NET_DVR_RTSP_PLAYERROR</td><td>430</td><td>RTSPPLAY交互错误</td></tr><tr><td>NET_DVR_RTSP_PLAYSENDTIMEOUT</td><td>431</td><td>RTSPPLAY发送超时</td></tr><tr><td>NET_DVR_RTSP_PLAYSENDERROR</td><td>432</td><td>RTSP PLAY发送错误</td></tr><tr><td>NET_DVR_RTSP_PLAYRECVTIMEOUT</td><td>433</td><td>RTSPPLAT接收超时</td></tr><tr><td>NET_DVR_RTSP_PLAYRECVDATALOST</td><td>434</td><td>RTSPPLAY接收数据错误</td></tr><tr><td>NET_DVR_RTSP_PLAYRECVERROR</td><td>435</td><td>RTSPPLAY接收失败</td></tr><tr><td>NET_DVR_RTSP_PLAYSERVERERR</td><td>436</td><td>RTSPPLAY服务器返回错误状态</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNERROR</td><td>440</td><td>RTSPTEARDOWN交互错误</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNSENDTIMEOUT</td><td>441</td><td>RTSPTEARDOWN发送超时</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNSENDERROR</td><td>442</td><td>RTSPTEARDOWN发送错误</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNRECVTIMEOUT</td><td>443</td><td>RTSPTEARDOWN接收超时</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNRECVDATALOST</td><td>444</td><td>RTSPTEARDOWN接收数据错误</td></tr><tr><td></td><td>445</td><td>RTSPTEARDOWN 接收失败</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNRECVERROR</td><td></td><td></td></tr><tr><td>NET_DVR_RTSP_TEARDOWNSERVERERR</td><td>446</td><td>RTSPTEARDOWN服务器返回错误状态</td></tr></table></body></html>  

## 6.3 软解码库错误码  

<html><body><table><tr><td>错误名称</td><td>错误值</td><td>说明</td></tr><tr><td>NET_PLAYM4_NOERROR</td><td>500</td><td>没有错误</td></tr><tr><td>NET_PLAYM4_PARA_OVER</td><td>501</td><td>输入参数非法</td></tr><tr><td>NET_PLAYM4_ORDER_ERROR</td><td>502</td><td>调用顺序不对</td></tr><tr><td>NET_PLAYM4_TIMER_ERROR</td><td>503</td><td>多媒体时钟设置失败</td></tr><tr><td>NET_PLAYM4_DEC_VIDEO_ERROR</td><td>504</td><td>视频解码失败</td></tr><tr><td>NET_PLAYM4_DEC_AUDIO_ERROR</td><td>505</td><td>音频解码失败</td></tr><tr><td>NET_PLAYM4_ALLOC_MEMORY_ERROR</td><td>506</td><td>分配内存失败</td></tr><tr><td>NET_PLAYM4_OPEN_FILE_ERROR</td><td>507</td><td>文件操作失败</td></tr><tr><td>NET_PLAYM4_CREATE_OBJ_ERROR</td><td>508</td><td>创建线程事件等失败</td></tr><tr><td>NET_PLAYM4_CREATE_DDRAW_ERROR</td><td>509</td><td>创建directDraw失败</td></tr><tr><td>NET_PLAYM4_CREATE_OFFSCREEN_ERROR</td><td>510</td><td>创建后端缓存失败</td></tr><tr><td>NET_PLAYM4_BUF_OVER</td><td>511</td><td>缓冲区满，输入流失败</td></tr><tr><td>NET_PLAYM4_CREATE_SOUND_ERROR</td><td>512</td><td>创建音频设备失败</td></tr><tr><td>NET_PLAYM4_SET_VOLUME_ERROR</td><td>513</td><td>设置音量失败</td></tr><tr><td>NET_PLAYM4_SUPPORT_FILE_ONLY</td><td>514</td><td>只能在播放文件时才能使用此接口</td></tr><tr><td>NET_PLAYM4_SUPPORT_STREAM_ONLY</td><td>515</td><td>只能在播放流时才能使用此接口</td></tr><tr><td>NET_PLAYM4_SYS_NOT_SUPPORT</td><td>516</td><td>系统不支持，解码器只能工作在 Pentium 3 以上</td></tr><tr><td>NET_PLAYM4_FILEHEADER_UNKNOWN</td><td>517</td><td>没有文件头</td></tr><tr><td>NET_PLAYM4_VERSION_INCORRECT</td><td>518</td><td>解码器和编码器版本不对应</td></tr><tr><td>NET_PALYM4_INIT_DECODER_ERROR</td><td>519</td><td>初始化解码器失败</td></tr><tr><td>NET_PLAYM4_CHECK_FILE_ERROR</td><td>520</td><td>文件太短或码流无法识别</td></tr><tr><td>NET_PLAYM4_INIT_TIMER_ERROR</td><td>521</td><td>初始化多媒体时钟失败</td></tr><tr><td>NET_PLAYM4_BLT_ERROR</td><td>522</td><td>位拷贝失败</td></tr><tr><td>NET_PLAYM4_UPDATE_ERROR</td><td>523</td><td>显示overlay 失败</td></tr><tr><td>NET_PLAYM4_OPEN_FILE_ERROR_MULTI</td><td>524</td><td>打开混合流文件失败</td></tr><tr><td>NET_PLAYM4_OPEN_FILE_ERROR_VIDEO</td><td>525</td><td>打开视频流文件失败</td></tr><tr><td>NET_PLAYM4_JPEG_COMPRESS_ERROR</td><td>526</td><td>JPEG 压缩错误</td></tr><tr><td>NET_PLAYM4_EXTRACT_NOT_SUPPORT</td><td>527</td><td>不支持该文件版本.</td></tr><tr><td>NET_PLAYM4_EXTRACT_DATA_ERROR</td><td>528</td><td>提取文件数据失败</td></tr></table></body></html>  

## 6.4 语音对讲库错误码  

<html><body><table><tr><td>错误名称</td><td>错误值</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></table></body></html>  

<html><body><table><tr><td>NET_AUDIOINTERCOM_OK</td><td>600</td><td>没有错误</td></tr><tr><td>NET_AUDIOINTECOM_ERR_NOTSUPORT</td><td>601</td><td>不支持</td></tr><tr><td>NET_AUDIOINTECOM_ERR_ALLOC_MEMERY</td><td>602</td><td>内存申请错误</td></tr><tr><td>NET_AUDIOINTECOM_ERR_PARAMETER</td><td>603</td><td>参数错误</td></tr><tr><td>NET_AUDIOINTECOM_ERR_CALL_ORDER</td><td>604</td><td>调用次序错误</td></tr><tr><td>NET_AUDIOINTECOM_ERR_FIND_DEVICE</td><td>605</td><td>未发现设备</td></tr><tr><td>NET_AUDIOINTECOM_ERR_OPEN_DEVICE</td><td>606</td><td>不能打开设备</td></tr><tr><td>NET_AUDIOINTECOM_ERR_NO_CONTEXT</td><td>607</td><td>设备上下文出错</td></tr><tr><td>NET_AUDIOINTECOM_ERR_NO_WAVFILE</td><td>608</td><td>WAV文件出错</td></tr><tr><td>NET_AUDIOINTECOM_ERR_INVALID_TYPE</td><td>609</td><td>无效的WAV参数类型</td></tr><tr><td>NET_AUDIOINTECOM_ERR_ENCODE_FAIL</td><td>610</td><td>编码失败</td></tr><tr><td>NET_AUDIOINTECOM_ERR_DECODE_FAIL</td><td>611</td><td>解码失败</td></tr><tr><td>NET_AUDIOINTECOM_ERR_NO_PLAYBACK</td><td>612</td><td>播放失败</td></tr><tr><td>NET_AUDIOINTECOM_ERR_DENOISE_FAIL</td><td>613</td><td>降噪失败</td></tr><tr><td>NET_AUDIOINTECOM_ERR_UNKOWN</td><td>619</td><td>未知错误</td></tr></table></body></html>  