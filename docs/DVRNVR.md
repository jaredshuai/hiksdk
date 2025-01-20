# 设备(DVR&NVR)网络 SDK 编程指南  

V5.2  

## 声  明  

非常感谢您购买我公司的产品，如果您有什么疑问或需要请随时联系我们。  

 我们已尽量保证手册内容的完整性与准确性，但也不免出现技术上不准确、与产品功能及操作不相符或印刷错误等情况，如有任何疑问或争议，请以我司最终解释为准。  

产品和手册将实时进行更新，恕不另行通知。  

本手册中内容仅为用户提供参考指导作用，请以 SDK 实际内容为准。  

## 目  录  

声 明  
目 录 . II  
1 SDK 简介.. 1  
2 SDK 版本更新. .. 5  
3 函数调用顺序 .. 19  
3.1 SDK 基本调用的主要流程 ... 19  
3.2 IP 通道相关说明. . 21  
3.3 实时预览模块流程.. .. 22  
3.4 回放和下载模块流程.. ..... 23  
3.5 参数配置模块流程. ... 24  
3.6 远程设备维护模块流程. ..... 25  
3.7 语音对讲转发模块流程 26  
3.8 报警模块流程. 27  
3.8.1 报警（布防）流程 .... ...... 27  
3.8.2 报警（监听）流程 . 28  
3.9 透明通道模块流程. .. 29  
4 函数调用实例 .. . 30  
4.1 IP 通道资源配置示例代码. ... 30  
4.2 预览模块的示例代码. ..... 34  
4.3 回放和下载模块的示例代码. ... 39  
4.4 参数配置模块的示例代码. ... 47  
4.5 远程设备维护模块的示例代码. ... 49  
4.6 语音对讲转发模块的示例代码， 51  
4.7 报警模块的示例代码-... ...... 52  
4.8 透明通道模块的示例代码， . 57  
5 函数说明. . 60  
5.1 SDK 初始化 .. . 60  
5.1.1 初始化 SDK NET_DVR_Init ... 60  
5.1.2 释放 SDK 资源 NET_DVR_Cleanup . .... 60  
5.2 SDK 本地功能 . 60  
SDK 本地参数配置. . 60  
5.2.1 获取 SDK 本地参数 NET_DVR_GetSDKLocalCfg . . 60  
5.2.2 设置 SDK 本地参数 NET_DVR_SetSDKLocalCfg. . 61  
连接和接收超时时间及重连设置 . . 62  
5.2.3 设置网络连接超时时间和连接尝试次数 NET_DVR_SetConnectTime . 62  
5.2.4 设置重连功能 NET_DVR_SetReconnect... ... 62  
5.2.5 设置接收超时时间 NET_DVR_SetRecvTimeOut .. 62  
多网卡绑定. . 62  
5.2.6 获取所有 IP，用于支持多网卡接口 NET_DVR_GetLocalIP. 62  
5.2.7 设置 IP 绑定 NET_DVR_SetValidIP. 63  

### SDK 版本、状态和能力 63  

5.2.8 获取 SDK 的版本号和 build 信息 NET_DVR_GetSDKBuildVersion ... ... 63  
5.2.9 获取当前 SDK 的状态信息 NET_DVR_GetSDKState . ... 63  
5.2.10 获取当前 SDK 的功能信息 NET_DVR_GetSDKAbility .... ... 63  
SDK启用写日志... .... 64  
5.2.11 启用写日志文件 NET_DVR_SetLogToFfile... .... 64  
异常消息回调 .. .... 64  
5.2.12 注册异常消息回调函数 NET_DVR_SetExceptionCallBack_V30 .... 64  
获取错误信息 ... .... 67  
5.2.13 返回最后操作的错误码 NET_DVR_GetLastError.. . 67  
5.2.14 返回最后操作的错误码信息 NET_DVR_GetErrorMsg . . 67  

### 5.3 用户注册. 67  

5.3.1 激活设备 NET_DVR_ActivateDevice.. ... 67  
5.3.2 IPServer 或者 DDNS 域名解析，获取动态 IP 地址和端口号 NET_DVR_GetDVRIPByResolveSvr_EX 67  
5.3.3 用户注册设备 NET_DVR_Login_V40. ... 68  
5.3.4 用户注销 NET_DVR_Logout. 68  

5.4 获取设备能力集. 69  

5.4.1 获取设备能力集 NET_DVR_GetDeviceAbility ... . 69  
5.4.2 获取设备能力集(标准协议) NET_DVR_GetSTDAbility . 70  
5.4.3 获取设备能力集(透传)NET_DVR_STDXMLConfig ........ 71  

### 5.5 实时预览. 71  

5.5.1 实时预览 NET_DVR_RealPlay_V40 ... 71   
5.5.2 停止预览 NET_DVR_StopRealPlay ........ 72   
5.5.3 获取预览时用来解码和显示的播放库句柄 NET_DVR_GetRealPlayerlndex. 72  

5.6 强制 I 帧. 73  

5.6.1 强制 I 帧 NET_DVR_RemoteControl .. 73  

### 5.7 预览显示视频参数配置. 73  

5.7.1 获取预览视频显示参数 NET_DVR_ClientGetVideoEffect .. .. 73  
5.7.2 获取预览视频显示参数 NET_DVR_GetVideoEffect .. .. 74  
5.7.3 设置预览视频显示参数 NET_DVR_ClientSetVideoEffect.. ... 74  
5.7.4 设置预览视频显示参数 NET_DVR_SetVideoEffect ....... . 74  

5.8 预览画面叠加字符和图像. 75  

5.8.1 预览画面叠加字符和图像，Linux 下无此接口 NET_DVR_RigisterDrawFun ............. ........... 75  

### 5.9 预览时播放声音控制. 75  

5.9.1 设置声音播放模式 NET_DVR_SetAudioMode. 75  
5.9.2 独占声卡模式下开启声音 NET_DVR_OpenSound . .. 75  
5.9.3 独占声卡模式下开启声音 NET_DVR_CloseSound ... .... 76  
5.9.4 共享声卡模式下开启声音 NET_DVR_OpenSoundShare ..... .. 76  
5.9.5 共享声卡模式下关闭声音 NET_DVR_CloseSoundShare .... .. 76  
5.9.6 调节播放音量 NET_DVR_Volume .. 76  

### 5.10 实时预览数据捕获. 77  

5.10.1 注册回调函数，捕获实时码流数据 NET_DVR_SetRealDataCallBack ........ 77  
5.10.2注册回调函数，捕获实时码流数据（RTP 标准码流）NET_DVR_SetStandardDataCallBack.....7  
5.10.3 捕获数据并保存到指定的文件中 NET_DVR_SaveRealData ......... . 78  
5.10.4 停止数据捕获 NET_DVR_StopSaveRealData.. . 78  
5.11 预览抓图.. .... 79  
5.11.1 设置抓图模式 NET_DVR_SetCapturePictureMode . 79  
5.11.2 预览时，单帧数据捕获并保存成图片 NET_DVR_CapturePicture. . 79  
5.12 设备抓图.. ...... 79  
5.12.1 单帧数据捕获并保存成 JPEG 图片 NET_DVR_CaptureJPEGPicture . ..... 79  
5.12.2 单帧数据捕获并保存成 JPEG 存放在指定的内存空间中 NET_DVR_CaptureJPEGPicture_NEW....80  
.13 云台控制.. ..... 80  
云台控制操作 ....... .... 80  
5.13.1 云台控制操作（需先启动图像预览）NET_DVR_PTZControl . ...... 80  
5.13.2 云台控制操作（不用启动图像预览）NET_DVR_PTZControl_Other ..... ..... 81  
5.13.3 带速度的云台控制操作（需先启动图像预览）NET_DVR_PTZControlWithSpeed.... ........ 82  
5.13.4 带速度的云台控制操作（不用启动图像预览）NET_DVR_PTZControlWithSpeed_Other ............... 82  
云台预置点操作 .. ....... 83  
5.13.5 云台预置点操作，需先启动预览 NET_DVR_PTZPreset ...... ...... 83  
5.13.6 云台预置点操作 NET_DVR_PTZPreset_Other.. ...... 83  
云台巡航操作 ...... ..... 84  
5.13.7 云台巡航操作，需先启动预览 NET_DVR_PTZPCruise ...... ...... 84  
5.13.8 云台巡航操作 NET_DVR_PTZPCruise_Other... ......... 84  
云台花样扫描操作 .. ...... 85  
5.13.9 云台花样扫描操作，需先启动预览 NET_DVR_PTZTrack. .. 85  
5.13.10 云台花样扫描操作 NET_DVR_PTZTrack_Other . .... 85  
透明云台控制 ... ..... 86  
5.13.11 透明云台操作，需先启动预览 NET_DVR_TransPTZ.. ...... 86  
5.13.12 透明云台操作 NET_DVR_TransPTZ_Other .. ...... 86  
云台区域缩放控制 .. ...... 86  
5.13.13 云台图象区域选择放大或缩小 NET_DVR_PTZSelZoomIn .. .. 86  
5.13.14 云台图像区域选择放大或缩小 NET_DVR_PTZSelZoomln_Ex.. ...... 87  
获取设备支持的云台协议 .......... ........ 87  
5.13.15获取设备支持的云台协议 NET_DVR_GetPTZProtocol... .. 87  
5.14 录像文件回放、下载、锁定及备份. ....... 87  
获取通道录像起止时间 .. .... 87  
5.14.1 获取通道录像起止时间 NET_DVR_InquiryRecordTimeSpan .. ....... 87  
即时刷新录像索引 .. . 88  
5.14.2 即时刷新录像索引 NET_DVR_UpdateRecordIndex ... ...... 88  
月历录像查询 . .. 88  
5.14.3 获取月历录像分布 NET_DVR_GetDeviceConfig .. .. 88  
录像文件的查找 .. ...... 89  
5.14.4 根据文件类型、时间查找设备录像文件 NET_DVR_FindFile_V40 ........... ....... 89  
5.14.5 逐个获取查找到的文件信息 NET_DVR_FindNextFile_V40 ........ .... 89  
5.14.6 关闭文件查找，释放资源 NET_DVR_FindClose_V30 .. ...... 90  
按事件查找录像文件 ....... .. 90  
5.14.7 根据事件查找录像文件 NET_DVR_FindFileByEvent_V40.. ...... 90  
5.14.8 逐个获取查找到事件录像信息 NET_DVR_FindNextEvent_V40 ... .. 90  

5.14.9 关闭文件查找，释放资源 NET_DVR_FindClose_V30 ... ... 91  
区域移动侦测智能搜索 ............ ...... 91  
5.14.10 开始智能搜索 NET_DVR_SmartSearch_V40 . . 91  
5.14.11 逐个获取查找到的智能录像信息 NET_DVR_SearchNextInfo . ........ 92  
5.14.12停止智能搜索 NET_DVR_StopSearch. ...... 92  
回放（正放或倒放）录像文件 ....... ...... 92  
5.14.13 按文件名回放录像文件 NET_DVR_PlayBackByName ..... ...... 92  
5.14.14 按时间回放录像文件 NET_DVR_PlayBackByTime_V40 ... ...... 93  
5.14.15 按文件名倒放录像文件 NET_DVR_PlayBackReverseByName.. ...... 94  
5.14.16 按时间倒放录像文件 NET_DVR_PlayBackReverseByTime_V40.. .. 94  
5.14.17 控制录像回放的状态 NET_DVR_PlayBackControl_V40... ....... 95  
5.14.18 停止回放录像文件 NET_DVR_StopPlayBack .. ........ 97  
回放录像文件时的数据捕获 ........... ...... 97  
5.14.19 捕获回放的录像数据，并保存成文件 NET_DVR_PlayBackSaveData ..... ...... 97  
5.14.20 停止保存录像数据 NET_DVR_StopPlayBackSave .. ...... 98  
5.14.21 注册回调函数，捕获录像数据 NET_DVR_SetPlayDataCallBack_V40 .. ...... 98  
录像标签的添加和删除 ............ ....... 99  
5.14.22 添加录像标签 NET_DVR_InsertRecordLabel... ......... 99  
5.14.23 修改录像标签 NET_DVR_ModifyRecordLabel... ....... 99  
5.14.24 删除录像标签 NET_DVR_DelRecordLabel. .. 99  
录像标签的查找 .. ....... 100  
5.14.25 搜索录像标签 NET_DVR_FindRecordLabel .. .... 100  
5.14.26 逐个获取搜索到的录像标签 NET_DVR_FindNextLabel. ...... 100  
5.14.27 停止搜索录像标签 NET_DVR_StopFindLabel. .. 100  
回放的其他操作 ....... .......... 101  
5.14.28 获取录像回放时显示的 OSD 时间 NET_DVR_GetPlayBackOsdTime.. ...... 101  
5.14.29 录像回放时抓图，并保存在文件中 NET_DVR_PlayBackCaptureFile . .. 101  
5.14.30 刷新显示回放窗口 NET_DVR_RefreshPlay .... ........ 101  
5.14.31 获取回放时用来解码显示的播放库句柄 NET_DVR_GetPlayBackPlayerIndex......... ........ 101  
下载录像文件 .... ....... 102  
5.14.32 按文件名下载录像文件 NET_DVR_GetFileByName. ... 102  
5.14.33 按时间下载录像文件 NET_DVR_GetFileByTime_V40... .......... 102  
5.14.34 控制录像下载的状态 NET_DVR_PlayBackControl_V40.. ...... 103  
5.14.35 停止下载录像文件 NET_DVR_StopGetFile... ........ 104  
5.14.36 获取当前下载录像文件的进度 NET_DVR_GetDownloadPos ...... ...... 104  
录像文件锁定和解锁 ........ .......... 104  
5.14.37 按文件名锁定录像文件 NET_DVR_LockFileByName .. .. 104  
5.14.38 按文件名解锁录像文件 NET_DVR_UnlockFileByName.. .... 104  
5.14.39 流 ID 方式对某一时间段录像文件进行加锁 NET_DVR_LockStreamFileByTime .......... ............. 105  
5.14.40 流 ID 方式对某一时间段录像文件进行解锁 NET_DVR_UnlockStreamFileByTime ......................... 105  
备份文件 105  
5.14.41 获取设备磁盘列表 NET_DVR_GetDiskList... ...... 105  
5.14.42 按文件名备份录像文件 NET_DVR_BackupByName.. ..... 106  
5.14.43 按时间段备份录像文件 NET_DVR_BackupByTime ...... ....... 106  
5.14.44获取备份的进度 NET_DVR_GetBackupProgres.. .... 106  
5.14.45停止备份 NET_DVR_StopBackup. .. 107  
5.15 图片的查找、回放及备份. .... 107  
查找图片 107  
5.15.1 根据类型和时间查找图片 NET_DVR_FindPicture.. .... 107  
5.15.2 逐个获取查找到的图片 NET_DVR_FindNextPicture_V40. .... 108  
5.15.3 关闭图片查找，释放资源 NET_DVR_CloseFindPicture.. .... 108  
图片智能检索（后检索） ... ...... 108  
5.15.4 开始智能图片检索 NET_DVR_SmartSearchPicture ... ...... 108  
5.15.5 逐个获取搜索到的智能图片信息 NET_DVR_FindNextSmartPicture . ..... 109  
5.15.6关闭图片智能检索，释放资源 NET_DVR_CloseSmartSearchPicture. .... 109  
回放（下载）图片 .. ..... 109  
5.15.7 图片回放 NET_DVR_GetPicture_V30 .. ... 109  
备份图片 110  
5.15.8 备份图片 NET_DVR_BackupPicture.. .... 110  
5.15.9 获取备份的进度 NET_DVR_GetBackupProgress. .... 110  
5.15.10 停止备份 NET_DVR_StopBackup.. ..... 111  
5.16 布防、撤防.. ....... 111  
设置报警等信息上传的回调函数 . ..... 111  
5.16.1 注册回调函数，接收报警消息 NET_DVR_SetDVRMessageCallBack_V30 . ...... 111  
布防撤防 112  
5.16.2建立报警上传通道，获取报警等信息 NET_DVR_SetupAlarmChan_V41... ....... 112  
5.16.3 撤销报警上传通道 NET_DVR_CloseAlarmChan_V30 . ... 113  
5.17 监听报警.. ..... 113  
5.17.1 启动监听，接收设备主动上传的报警等信息NET_DVR_StartListen_V30.... .... 113  
5.17.2 停止监听（支持多线程）NET_DVR_StopListen_V30 .... ....... 114  
5.18 语音对讲、转发及广播. ... 114  
语音对讲 114  
5.18.1 启动语音对讲 NET_DVR_StartVoiceCom_V30.. .... 114  
5.18.2 设置语音对讲客户端的音量 NET_DVR_SetVoiceComClientVolume .. ..... 116  
5.18.3 停止语音对讲或者语音转发 NET_DVR_StopVoiceCom... .. 116  
语音转发 116  
5.18.4 启动语音转发，获取编码后的音频数据 NET_DVR_StartVoiceCom_MR_V30.. ... 116  
5.18.5 转发语音数据 NET_DVR_VoiceComSendData ...... .... 117  
5.18.6 停止语音对讲或语音转发 NET_DVR_StopVoiceCom....... ...... 118  
语音广播 118  
5.18.7 启动语音广播的 PC 端声音捕获 NET_DVR_ClientAudioStart_V30 ... ...... 118  
5.18.8添加设备的某个语音通道到可以接收 PC 端声音的广播组 NET.DVR_AdDVR_.V30.....18  
5.18.9 从可接收 PC 机声音的广播组里删除该设备的语音通道 NET_DVR_DeIDVR_V30... ....... 119  
5.18.10 停止语音广播的 PC 端声音捕获 NET_DVR_ClientAudioStop.. ..... 119  
音频压缩参数 ........ .... 119  
5.18.11获取当前生效的对讲音频压缩参数 NET_DVR_GetCurrentAudioCompress.. ....... 119  
5.18.12 获取通道参数 NET_DVR_GetDVRConfig . ...... 119  
设置通道参数 NET_DVR_SetDVRConfig.. . 120  
音频编解码(Windows 32 位系统支持) ...... . 120  
G722 音频编解码 ... ..... 120  
5.18.14 初始化音频编码 NET_DVR_InitG722Encoder.. ... 120  
5.18.15 G722 音频编码 NET_DVR_EncodeG722Frame... ... 121  
5.18.16 释放音频编码资源 NET_DVR_ReleaseG722Encoder.. ........ 121  
5.18.17 初始化音频解码 NET_DVR_InitG722Decoder .. .. 121  
5.18.18 G722 音频解码 NET_DVR_DecodeG722Frame ... ... 121  
5.18.19 释放音频解码资源 NET_DVR_ReleaseG722Decoder . ... 122  
G711 音频编解码 .... 122  
5.18.20 G711 音频编码 NET_DVR_EncodeG711Frame.. ..... 122  
5.18.21 G711 音频解码 NET_DVR_DecodeG711Frame .... ....... 122  
远程参数配置. ..... 123  
系统参数配置 .. ..... 123  
5.19.1 获取设备参数 NET_DVR_GetDVRConfig .. ...... 123  
5.19.2 设置设备参数 NET_DVR_SetDVRConfig. ...... 124  
通道参数配置 .. .... 124  
5.19.3 获取通道参数 NET_DVR_GetDVRConfig .. .... 124  
5.19.4 设置通道参数 NET_DVR_SetDVRConfig... ....... 125  
5.19.5 批量获取通道参数 NET_DVR_GetDeviceConfig . ...... 126  
5.19.6 批量设置通道参数 NET_DVR_SetDeviceConfig. ...... 127  
5.19.7 远程控制 NET_DVR_RemoteControl . .... 128  
网络参数配置 .. ....... 129  
5.19.8 获取网络参数 NET_DVR_GetDVRConfig .. ...... 129  
5.19.9 设置网络参数 NET_DVR_SetDVRConfig. .... 130  
5.19.10 获取网络参数 NET_DVR_GetSTDConfig. .... 131  
5.19.11 设置网络参数 NET_DVR_SetSTDConfig ..... ...... 131  
5.19.12 批量获取网络参数 NET_DVR_GetDeviceConfig . ....... 131  
5.19.13 批量设置网络参数 NET_DVR_SetDeviceConfig. ..... 132  
5.19.14 获取 RTSP 协议参数 NET_DVR_GetRtspConfig. .... 133  
5.19.15 设置 RTSP 协议参数 NET_DVR_SetRtspConfig . ....... 133  
IP 通道管理. ..... 133  
5.19.16 获取设备的配置信息 NET_DVR_GetDVRConfig . ..... 133  
5.19.17 设置设备的配置信息 NET_DVR_SetDVRConfig. .... 134  
5.19.18 设置设备的配置信息(标准协议)NET_DVR_SetSTDConfig . ..... 135  
5.19.19 远程控制(标准协议)NET_DVR_STDControl ........ .......... 135  
5.19.20 批量获取配置信息 NET_DVR_GetDeviceConfig . ...... 136  
5.19.21 启动长连接远程配置 NET_DVR_StartRemoteConfig . .... 137  
5.19.22 关闭长连接配置 NET_DVR_StopRemoteConfig. .... 138  
5.19.23 远程扫描获取 IPC 信息列表 NET_DVR_GetSadpInfoList ..... ...... 138  
5.19.24 远程修改 IPC 信息 NET_DVR_UpdateSadplnfo... ...... 138  
5.19.25 获取设备支持的 IPC 协议表 NET_DVR_GetIPCProtoList. .... 138  
报警输入输出配置 .. .... 139  
5.19.26 获取设备参数 NET_DVR_GetDVRConfig .. ....... 139  
5.19.27 设置设备参数 NET_DVR_SetDVRConfig. ..... 139  
5.19.28 获取设备报警输出 NET_DVR_GetAlarmOut_V30 . ..... 140  
5.19.29 设置设备报警输出 NET_DVR_SetAlarmOut ... ..... 140  
本地输出(预览)参数配置. ..... 140  
5.19.30 获取设备参数 NET_DVR_GetDVRConfig . ..... 140  
5.19.31 设置设备参数 NET_DVR_SetDVRConfig... ..... 141  
5.19.32 批量获取配置信息 NET_DVR_GetDeviceConfig . .... 142  
5.19.33 批量设置配置信息 NET_DVR_SetDeviceConfig.. .... 142  
5.19.34 获取视频输出缩放信息 NET_DVR_GetScaleCFG_V30 . ..... 143  
5.19.35 设置视频输出缩放参数 NET_DVR_SetScaleCFG_V30. ... 143  
用户和安全参数配置 .. .... 143  
5.19.36 获取设备参数 NET_DVR_GetDVRConfig ... .... 143  
5.19.37 设置设备参数NET_.DVR_SetDVRConfig.... .......... 144  
5.19.38 批量获取配置信息 NET_DVR_GetDeviceConfig . ..... 145  
5.19.39 批量设置配置信息 NET_DVR_SetDeviceConfig... .... 145  
5.19.40 远程控制 NET_DVR_RemoteControl ..... ...... 146  
5.19.41 启动长连接远程配置 NET_DVR_StartRemoteConfig . ...... 146  
5.19.42 逐个获取查找到的信息 NET_DVR_GetNextRemoteConfig. .... 147  
5.19.43 关闭长连接配置 NET_DVR_StopRemoteConfig.. ...... 148  
更多参数配置 . ..... 148  
5.19.44获取设备参数 NET_DVR_GetSTDConfig... ...... 148  
5.20 SMART 参数配置 . ..... 149  
SMART 参数配置 .. .... 149  
5.20.1 批量获取配置信息 NET_DVR_GetDeviceConfig . .... 149  
5.20.2 批量设置配置信息NET_DVR_SetDeviceConfig.. ..... 150  
5.20.3 获取设备的配置信息(标准协议)NET_DVR_GetSTDConfig ... 151  
5.20.4 设置设备的配置信息(标准协议)NET_DVR_SetSTDConfig . ...... 151  
5.20.5 设备参数配置(透传)NET_DVR_STDXMLConfig ....... .... 152  
VQD 视频质量诊断.. ........ 152  
5.20.6 批量获取配置信息 NET_DVR_GetDeviceConfig . ..... 152  
5.20.7 批量设置配置信息 NET_DVR_SetDeviceConfig.. ...... 153  
5.20.8 启动长连接远程配置 NET_DVR_StartRemoteConfig . .. ........ 154  
5.20.9 逐个获取查找到的信息 NET_DVR_GetNextRemoteConfig... ..... 155  
5.20.10 关闭长连接配置接口所创建的句柄，释放资源 NET_DVR_StopRemoteConfig ... 156  

### 5.21 存储管理. 156  

#### 存储参数配置 . 156  

5.21.1 获取设备的配置信息 NET_DVR_GetDVRConfig . .. 156  
5.21.2 设置设备的配置信息 NET_DVR_SetDVRConfig. .. 157  
5.21.3 远程控制 NET_DVR_RemoteControl .. ... 159  
硬盘格式化... ...... 159  
5.21.4 远程格式化设备硬盘 NET_DVR_FormatDisk.. .... 159  
5.21.5 获取格式化硬盘的进度 NET_DVR_GetFormatProgress. .. 159  
5.21.6 关闭格式化硬盘句柄，释放资源 NET_DVR_CloseFormatHandle . .. 160  
NAS 目录查询 .. ... 160  
5.21.7 启动长连接远程配置 NET_DVR_StartRemoteConfig . .. 160  
5.21.8 逐个获取查找到的信息 NET_DVR_GetNextRemoteConfig .. 161  
5.21.9 获取长连接配置的状态 NET_DVR_GetRemoteConfigState . ... 161  
5.21.10 关闭长连接配置 NET_DVR_StopRemoteConfig... ...... 162  
IP SAN 文件目录查找 .... .... 162  
5.21.11 查找 IPSAN 文件目录 NET_DVR_FindIpSanDirectory ......... ..... 162  
5.21.12 逐个获取查找到的目录信息 NET_DVR_FindNextDirectory ..... .... 162  
5.21.13 停止 IPSAN 文件目录搜索，释放资源 NET_DVR_FindDirectoryClose. .... 163  
第三方云功能 .. ... 163  
5.21.14 获取设备能力集(标准协议) NET_DVR_GetSTDAbility . ... 163  
5.21.15 获取设备的配置信息(标准协议)NET_DVR_GetSTDConfig . ...... 164  
5.21.16 设置设备的配置信息(标准协议)NET_DVR_SetSTDConfig . .... 164  
5.22 零通道预览和配置... .... 165  
参数配置 165  
5.22.1 获取设备的配置信息 NET_DVR_GetDVRConfig . .... 165  
5.22.2 设置设备的配置信息 NET_DVR_SetDVRConfig, ... 165  
实时预览 166  
5.22.3 开启零通道预览 NET_DVR_ZeroStartPlay ..... .... 166  
5.22.4 停止预览 NET_DVR_ZeroStopPlay... .. 167  
其他功能 167  
5.22.5 零通道产生一个关键帧 NET_DVR_ZeroMakeKeyFrame. . 167  
5.22.6 零通道预览画面翻页NET_DVR_ZeroTurnOver.. ..... 167  
5.23 POS 功能接口 . ... 167  
获取能力集.. .... 167  
5.23.1 获取设备能力集 NET_DVR_GetDeviceAbility ... .... 167  
5.23.2 获取设备能力集(标准协议) NET_DVR_GetSTDAbility 错误!未定义书签。  
参数配置 168  
5.23.3 获取 POS 相关参数 NET_DVR_GetDVRConfig ..... ...... 168  
5.23.4 设置 POS 相关参数 NET_DVR_SetDVRConfig ...... .... 169  
5.23.5 批量获取配置信息 NET_DVR_GetDeviceConfig ...... ......... 169  
5.23.6 批量设置配置信息 NET_DVR_SetDeviceConfig. ..... 170  
5.23.7 获取 POS 相关参数 NET_DVR_GetSTDConfig . 错误!未定义书签。  
5.23.8 设置 POS 相关参数 NET_DVR_SetSTDConfig... 错误!未定义书签。  
5.24 透明通道. .... 170  
5.24.1 建立透明通道 NET_DVR_SerialStart . ..... 170  
5.24.2 通过透明通道向设备串口发送数据 NET_DVR_SerialSend . ..... 171  
5.24.3 断开透明通道 NET_DVR_SerialStop... .... 171  
.25 向串口发送数据. ..... 171  
5.25.1 直接向串口发送数据，不需要建立透明通道 NET_DVR_SendToSerialIPort. .... 171  
5.25.2 直接向 232 串口发送数据，不需要建立透明通道 NET_DVR_SendTo232Port... .... 172  
5.26 远程控制设备手动录像， .... 172  
5.26.1 远程手动启动设备录像 NET_DVR_StartDVRRecord . .... 172  
5.26.2 远程手动停止设备录像 NET_DVR_StopDVRRecord.. .... 173  
5.26.3 远程控制 NET_DVR_RemoteControl . .... 173  
5.27 远程面板控制. ... 173  
5.27.1 远程控制面板上的按键 NET_DVR_ClickKey... .. 173  
5.27.2 禁用设备本地面板控制 NET_DVR_LockPanel... .. 175  
5.27.3 恢复设备本地面板控制 NET_DVR_UnLockPanel . ..... 175  
5.28 码流加密.. .......... 175  
5.28.1 设置设备码流加密密钥 NET_DVR_InquestStreamEncrypt .. ..... 175  
5.28.2 获取设备码流加密状态 NET_DVR_InquestGetEncryptStat.. ....... 176  
5.29 邮件测试.. ...... 176  
5.29.1 测试按已配置的 EMAIL 参数能否收发成功 NET_DVR_StartEmailTest.. ........ 176  
5.29.2 获取邮件测试的进度 NET_DVR_GetEmailTestProgress .... ....... 176  
5.29.3 停止邮件测试 NET_DVR_StopEmailTest .... ...... 177  
5.30 文件上传下载 ...... 177  
5.30.1 上传文件 NET_DVR_UploadFile_V40 ...... ..... 177  
5.30.2 获取文件上传的进度和状态 NET_DVR_GetUploadState.......... ......... 178  
5.30.3 停止文件上传 NET_DVR_UploadClose.. ...... 178  
5.30.4 开始下载文件 NET_DVR_StartDownload... ...... 178  
5.30.5 获取文件下载的进度和状态 NET_DVR_GetDownloadState.. .. 179  
5.30.6 停止文件下载 NET_DVR_StopDownload . ........ 179  
5.31 设备维护管理. ........ 179  
获取设备工作状态 .. ...... 179  
5.31.1 批量获取配置信息 NET_DVR_GetDeviceConfig ... ..... 179  
5.31.2 获取设备运行状态 NET_DVR_GetDeviceStatus ... ...... 180  
5.31.3 设备在线状态检测 NET_DVR_RemoteControl .......... .......... 181  
5.31.4 启动设备状态巡检 NET_DVR_StartGetDevState.. ..... 181  
5.31.5 停止设备状态巡检 NET_DVR_StopGetDevState ...... ..... 181  
远程升级 182  
5.31.6 设置远程升级时网络环境 NET_DVR_SetNetworkEnvironment . ...... 182  
5.31.7 远程升级 NET_DVR_Upgrade .... .. 182  
5.31.8 获取远程升级的进度 NET_DVR_GetUpgradeProgres... ..... 182  
5.31.9 获取远程升级的状态 NET_DVR_GetUpgradeState ............. ..... 183  
5.31.10 获取远程升级的阶段信息 NET_DVR_GetUpgradeStep ..... ..... 183  
5.31.11 关闭远程升级句柄，释放资源 NET_DVR_CloseUpgradeHandle .......... ........... 183  
在线升级 183  
5.31.12获取在线升级相关信息 NET_DVR_GetSTDConfig... .... 183  
5.31.13 远程控制在线升级 NET_DVR_STDControl. .. 184  
日志查找 185  
5.31.14 查找设备的日志信息（可搜索带 S.M.A.R.T 信息的日志）NET_DVR_FindDVRLog_V30 ............... 185  
5.31.15 逐条获取查找到的日志信息 NET_DVR_FindNextLog_V30 .. ..... 185  
释放查找日志的资源 NET_DVR_FindLogClose_V30 ..... .... 186  
远程备份 186  
5.31.17获取设备磁盘列表 NET_DVR_GetDiskList... ......... 186  
5.31.18 备份统一接口 NET_DVR_Backup . ..... 186  
获取备份的进度 NET_DVR_GetBackupProgress.. ...... 187  
5.31.20 停止备份NET_DVR_StopBackup.. .... 187  
恢复设备默认参数 .... ...... 188  
5.31.21 恢复设备默认参数 NET_DVR_RestoreConfig ... 188  
导入/导出配置文件 .. 188  
5.31.22 导出配置文件 NET_DVR_GetConfigFile_V30.. .... 188  
5.31.23 导出配置文件 NET_DVR_GetConfigFile... ... 188  
5.31.24 导入配置文件 NET_DVR_SetConfigFile_EX. .... 188  
5.31.25 导入配置文件 NET_DVR_SetConfigFile. .. 189  
网流量检测. .... 189  
5.31.26 开始网络流量检测 NET_DVR_StartNetworkFlowTest . ... 189  
5.31.27 停止网络流量检测 NET_DVR_StopNetworkFlowTest. ... 189  
获取 UPNP 端口映射状态 .... 190  
5.31.28 获取 UPNP 端口映射状态 NET_DVR_GetUpnpNatState . ... 190  
关机和重启 ... 190  
5.31.29 重启设备 NET_DVR_RebootDVR . 190  
5.31.30 关闭设备 NET_DVR_ShutDownDVR . ... 190  
6 错误代码和日志类型 . .. 191  
6.1 网络通讯库错误码. .. 191  
6.2 RTSP 通讯库错误码. ..... 197  
6.3 软解码库错误码. ... 198  
6.4 语音对讲库错误码. ... 199  
6.5 日志类型. .. 199  

## 1 SDK 简介  

设备网络 SDK 是基于设备私有网络通信协议开发的，为嵌入式网络硬盘录像机、NVR、视频服务器、网络摄像机、网络球机、解码器、报警主机等网络产品服务的配套模块，用于远程访问和控制设备软件的二次开发。  

本文档仅介绍 DVR、NVR 支持的功能及相关接口，相关结构体和更多其他功能接口请参考《设备网络SDK 使用手册.chm》。  

适用于但不仅限于以下产品型号：  

DVR：DS-9100、DS-8100、DS-8000-S、DS-8800、DS-7800、DS-7300、DS-7200、DS-7100、DS-7000 等系列，包括-ST、-SH、-SE、-SN、-RT、-RH、-XT 等。  

NVR: DS-96000N-I24/16、DS-96000N-F24/F16(/H)(/I)、DS-96000N-H24/H16(/H)(/I)、DS-9600N-I8/H8/F8/ST/XT、DS-8600N-I8/H8/F8/E8/ST/XT、DS-7800N-E1/SN/SNH、DS-7600N-ST/E2/E1、DS-7700N-ST/E4、DS-9500N-ST、DS-9500N-S、DS-9600N-SH、DS-7600N-S、DS-9664N-RX 等。  

XVR：DS-9000HQH-SH、DS-8100HQH(/HGH)-SH、DS-8000HQH-SH、DS-7300HQH(/HGH)-SH、  
DS-7200HQH(/HGH)-SH、DS-8800HQH(/HGH)(/HUH)-SH(/Fx)、DS-7900HQH(/HGH)(/HUH)-SH(/Fx)、  
DS-7800HQH(/HGH)(/HUH)-SH(/Ex/Fx)、DS-7100HGH-E1(/F1)等。HDVR(混合型 DVR)：DS-9000、DS-8000-ST、DS-7600H-ST/-S 系列等。  

### 设备网络 SDK 主要功能 ：  

主要用于实时码流预览、录像文件回放和下载、云台控制、布防/撤防、语音对讲、日志管理、远程升级、格式化硬盘、参数配置（系统配置、通道配置、串口配置、报警配置、用户配置）和获取设备能力集等。  

设备网络 SDK 包含网络通讯库、播放库等功能组件，我们提供 Windows 和 Linux 两个版本的 SDK，各自所包含的组件如下：  

表 1.1 Windows SDK 组件  


<html><body><table><tr><td rowspan="4">网络通讯库 核心组件</td><td rowspan="4">外部接口</td><td>HCNetSDK.h</td><td>头文件</td><td></td></tr><tr><td>HCNetSDK.lib</td><td>LIB库文件</td><td></td></tr><tr><td>HCNetSDK.dll</td><td>DLL库文件</td><td></td></tr><tr><td>HCCore.lib</td><td>LIB库文件</td><td></td></tr><tr><td rowspan="6">组件库</td><td></td><td>HCCore.dll</td><td>DLL库文件</td><td></td></tr><tr><td>设备配置核心组件</td><td>HCCoreDevCfg.dll</td><td>DLL库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td rowspan="2">预览组件</td><td>HCPreview.lib</td><td>LIB库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>HCPreview.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>回放组件</td><td>HCPlayBack.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>语音组件</td><td>HCVoiceTalk.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td rowspan="2">报警组件</td><td>HCAlarm.lib</td><td>LIB库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>HCAlarm.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="5"></td><td>显示组件</td><td>HCDisplay.dll</td><td>DLL库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>行业应用管理配置组件</td><td>HCIndustry.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td rowspan="2">维护管理配置组件</td><td>HCGeneralCfgMgr.lib</td><td>LIB库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>HCGeneralCfgMgr.dll</td><td>DLL库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>RTSP 通讯库</td><td>StreamTransClient.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>转封装库</td><td></td><td>SystemTransform.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>字符转码库</td><td></td><td>libiconv2.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>模拟能力集</td><td></td><td>LocalXml.zip</td><td>XML文件包</td><td></td></tr><tr><td>帧分析库</td><td></td><td>AnalyzeData.dll</td><td>DLL库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td rowspan="2">语音对讲库</td><td></td><td>Audiolntercom.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td></td><td>OpenAL32.dll</td><td>DLL库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td rowspan="11">播放库</td><td rowspan="2">核心库文件</td><td>PlayM4.h、WindowsPlayM4.h</td><td>头文件</td><td></td></tr><tr><td>PlayCtrl.lib</td><td>LIB库文件</td><td></td></tr><tr><td></td><td>PlayCtrl.dll</td><td>DLL库文件</td><td></td></tr><tr><td>视频渲染库</td><td>SuperRender.dll</td><td>DLL库文件</td><td></td></tr><tr><td>音频渲染库</td><td>AudioRender.dll</td><td>DLL库文件</td><td></td></tr><tr><td>小鹰眼库</td><td>EagleEyeRender.dll</td><td>DLL库文件</td><td></td></tr><tr><td>GPU硬解码库</td><td>HWDecode.dll</td><td>DLL库文件</td><td></td></tr><tr><td>鱼眼库</td><td>MP_Render.dll</td><td>DLL库文件</td><td></td></tr><tr><td>视频后处理库</td><td>MP_VIE.dIl</td><td>DLL库文件</td><td></td></tr><tr><td>测温信息抓图库</td><td>YUVProcess.dll</td><td>DLL库文件</td><td></td></tr><tr><td>DirectX 组件库</td><td>D3DCompiler_43.dll</td><td>DLL库文件</td><td></td></tr></table></body></html>  

表 1.2 Linux SDK 组件  


<html><body><table><tr><td rowspan="3">网络通讯库</td><td>外部接口</td><td>HCNetSDK.h</td><td>头文件</td><td></td></tr><tr><td></td><td>libhcnetsdk.so</td><td>SO库文件</td><td></td></tr><tr><td>核心组件</td><td>libHCCore.so</td><td>SO库文件</td><td></td></tr><tr><td rowspan="8">组件库</td><td>设备配置核心组件</td><td>libHCCoreDevCfg.so</td><td>SO库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>预览组件</td><td>libHCPreview.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>回放组件</td><td>libHCPlayBack.so</td><td>SO 库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>语音组件</td><td>libHCVoiceTalk.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>报警组件</td><td>libHCAlarm.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>显示组件</td><td>libHCDisplay.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>行业应用管理配置组件</td><td>libHCIndustry.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr><tr><td>维护管理配置组件</td><td>libHCGeneralCfgMgr.so</td><td>SO库文件</td><td>HCNetSDKCom 文件夹</td></tr></table></body></html>  

<html><body><table><tr><td>hpr库</td><td></td><td>libhpr.so</td><td>SO库文件</td><td></td></tr><tr><td>RTSP通讯库</td><td></td><td>libStreamTransClient.so</td><td>SO库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>转封装库</td><td></td><td>libSystemTransform.so</td><td>SO库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>字符转码库</td><td></td><td>libiconv2.so</td><td>SO库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td>帧分析库</td><td></td><td>libanalyzedata.so</td><td>SO库文件</td><td>HCNetSDKCom文件夹</td></tr><tr><td rowspan="4">播放库</td><td rowspan="2">核心库文件</td><td>PlayM4.h、LinuxPlayM4.h</td><td>头文件</td><td></td></tr><tr><td>libPlayCtrl.so</td><td>SO库文件</td><td></td></tr><tr><td>视频渲染库</td><td>libSuperRender.so</td><td>SO库文件</td><td></td></tr><tr><td>音频渲染库</td><td>libAudioRender.so</td><td>SO库文件</td><td></td></tr></table></body></html>  

本版本的设备网络SDK开发包中包含以上各个组件,HCNetSDK.dIl、HCCore.dIl必须加载（对于LinuxSDK,即 libhcnetsdk.so、libHCCore.so），其他组件，用户可以根据需要选择其中的一部分或者全部，以下将对各个组件在 SDK 中的作用和使用条件分别说明。  

 网络通讯库：设备网络 SDK 的主体，主要用于网络客户端与各类产品之间的通讯交互，负责远程功能调控, 远程参数配置及码流数据的获取和处理等。设备网络 SDK V5.0 针对产品应用业务进行细化，对之前版本的 SDK 的功能模块进行组件化，其中外部接口（HCNetSDK.dll）仍然保持和设备网络 SDK V4.x版本保存一致(向下兼容)，其他单独的业务功能（预览、回放等）可以加载单独的模块组件，多个业务功能也可以组合使用。更新 SDK 时，HCNetSDK.dll、HCCore.dll 以及 HCNetSDKCom 文件夹下的功能组件库文件都需要更新加载，且 HCNetSDKCom 文件夹名不能修改。  

hpr 库：网络通讯库的依赖库，Linux SDK 使用时和网络通讯库同时加载。  

RTSP 通讯库：支持 RTSP 传输协议的网络库。当需要对支持 RTSP 协议的产品进行取流等操作时就必须加载该项组件。  

 转封装库：库的功能可以分为两种：一种是将标准码流转换成采用我们公司封装格式的码流。当用户需要对支持 RTSP 协议的产品捕获采用本公司封装格式的码流数据时（即当设置 NET_DVR_RealPlay_V40接口中的回调函数捕获数据或者调用 NET_DVR_SetRealDataCallBack 接口捕获数据时）必须加载该组件。另一种功能是能将标准码流转换成其他格式的封装，如 3GPP、PS 等。例如，当用户需要对支持 RTSP协议的产品实时捕获指定封装格式的码流数据（对应的 SDK 接口为 NET_DVR_SaveRealData）时必须加载该项组件。  

 语音对讲库：用于语音对讲时通过声卡采集数据并按照指定的编码格式编码码流或者解码播放音频码流数据（不带封装格式的码流数据）。V4.2.2.5 及以前版本 SDK 均采用 windows API 实现相关功能。之后版本默认使用语音对讲库的方式，通过接口 NET_DVR_SetSDKLocalCfg 可以选择之前的 windows API模式。OpenAL32.dll 为依赖库，语音对讲库模式下必须加载。Windows64 位或者 Linux 系统下无语音对讲功能。  

·字符转换库:电脑字符集和设备字符集不一致时,SDK 内部需要进行字符编码转换,SDK 默认使用libiconv库进行类型转换。如果用户不想使用 libiconv 编码库，可以调用 NET_DVR_SetSDKLocalCfg (类型:NET_SDK_LOCAL_CFG_TYPE_BYTE_ENCODE)设置字符转码回调函数，将用户自己的字符编码接口告知SDK，然后 SDK 将使用用户提供的字符编码接口进行字符串处理。  

模拟能力集：如果需要获取设备能力集（NET_DVR_GetDeviceAbility），建议调用 NET_DVR_SetSDKLocalCfg启用模拟能力集，此时需要加载 LocalXml.zip（要求和网络通讯库放在同一个目录下）。  

帧分析库：用于分析视音频帧数据，调用 NET_DVR_SetESRealPlayCallBack、NET_DVR_SetPlayBackESCallBack 设置裸码流回调函数等接口时，必须加载该库文件。  

 播放库：主要用于对实时码流数据进行解码显示（实现预览功能）和对录像文件进行回放解码等。用户如果需要在 SDK 内部进行对实时流和录像码流播放显示时（即 NET_DVR_RealPlay_V40 接口的第二个结构体参数的播放句柄设置成有效句柄时）必须加载该组件，而如果用户仅需要用网络通讯库捕获到数据后再外部自行处理就不需要加载该组件，这种情况下用户在外部自行解码将更灵活，可参见软解码库函数说明《播放器 SDK 编程指南》。  

## 2 SDK 版本更新  

### Version 5.2.5.25 (build20160923)  

$\bullet$ 大路数 NVR DS-96000N-I 系列 V3.6.1  
$\bullet$ 扩展报警结构体：NET_VCA_RULE_ALARM（异常行为识别）、NET_DVR_PDC_ALRAM_INFO（客流量统计）、NET_VCA_FACESNAP_RESULT（人脸抓拍结果）、NET_DVR_FACE_DETECTION（人脸侦测）、NET_DVR_AUDIOEXCEPTION_ALARM（声音）、NET_DVR_DEFOCUS_ALARM（虚焦）、NET_DVR_SCENECHANGE_DETECTION_RESULT（场景变更）、NET_DVR_HEATMAP_RESULT（热度图）、NET_DVR_FIREDETECTION_ALARM（火点检测）、NET_DVR_SHIPSDETECTION_ALARM（船只检测），这些结构体里的 NET_VCA_DEV_INFO 对应的 byIvmsChannel 扩展协议为 4 字节，对应这些结构体的wDevInfoIvmsChannelEx。NET_ITS_PLATE_RESULT（车牌结果检测）增加 byChanIndexEx，与 byChanIndex一起表示通道号。  
 NET_DVR_SINGLE_HD（硬盘管理参数）中 byHDType(硬盘类型)增加索引值：6-minSAS。对应能力在设备软硬件能力集(BasicCapability，对应接口：NET_DVR_GetDeviceAbility， 能力集类型：DEVICE_SOFTHARDWARE_ABILITY)扩展，新增节点：<isSupportMinSAS>(是否支持 minSAS 硬盘类型)。  
$\bullet$ 多网卡配置扩展（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig），新增命令：NET_DVR_GET_NETCFG_MULTI_V50 和 NET_DVR_SET_NETCFG_MULTI_V50，兼容NET_DVR_GET_NETCFG_MULTI 和 NET_DVR_SET_NETCFG_MULTI。  

### Version 5.2.5.15 (build20160906)  

 90/80/81/73/72HQH(HGH)-SH V3.4.80  
$\bullet$ 新增获取功能互斥信息的功能（对应接口：NET_DVR_STDXMLConfig）：获取：GET /ISAPI/System/mutexFunctionErrorMsg。  
$\bullet$ 设备系统总能力集(DeviceCap，对应接口：NET_DVR_STDXMLConfig)扩展，新增节点：<isSupportGetmutexFuncErrMsg>(是否支持获取功能互斥信息)。  
$\bullet$ 新增错误码（对应接口：NET_DVR_GetLastError 和 NET_DVR_GetErrorMsg）：2108。  

### Version 5.2.3.15 (build20160713)  

 I、K、E 系列 NVR 产品 V3.4.80  

$\bullet$ 移动侦测支持多区域配置扩展：1) NET_DVR_MOTION_V40(移动侦测参数)中参数 byConfigurationMode(移动侦测模式)新增取值：2-坐标系区域模式。2) NET_DVR_MOTION_MULTI_AREA(移动侦测多区域配置)使用 1 个保留字节新增参数：byAllMotionSensitive(移动侦测灵敏度)。  
$\bullet$ 用户参数配置扩展，支持密码确认（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_USERCFG_V50、NET_DVR_SET_USERCFG_V50。  
$\bullet$ 新增 DNS 手动设置使能配置功能：1) NET_DVR_NETCFG_V30(网络配置)使用 1 个保留字节新增参数：byEnableDNS(DNS 使能)。2) NET_DVR_ETHERNET_MULTI(单个网卡配置)使用 1 个保留字节新增参数：byEnableDNS(DNS 使能)。  
$\bullet$ 设备鱼眼能力集(FishEyeAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：FISHEYE_IPC_ABILITY)扩展，新增节点：<previewMode>(实时输出模式)。  
$\bullet$ 设备图像参数能力集(VideoPicAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_VIDEOPIC_ABILITY)中移动侦测能力节点<MotionDetection>扩展：<regionType>新增取值：coordinates(坐标系区域模式)；新增子节点：<Coordinates>(坐标系区域参数)。  
$\bullet$ 设备用户管理参数能力集(UserAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_USER_ABILITY)扩展，新增节点：<loginPassword>(登录密码确认)。  
$\bullet$ 设备软硬件能力集(BasicCapability，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_SOFTHARDWARE_ABILITY)扩展，新增节点：<MultiDNSAddress>(支持多 DNS)、<isSupportDNS>(支持 DNS 手动设置使能)。  
$\bullet$ 设备网络应用参数能力集(NetAppAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_NETAPP_ABILITY)扩展，<NetworkInterfaceEntry $>$ 新增子节点：<isSupportDNS>(支持 DNS 手动设置使能)。  
$\bullet$ 新增错误码（对应接口：NET_DVR_GetLastError）：834。  
$\bullet$ 新增日志类型（对应接口：NET_DVR_FindDVRLog_V30）：附加日志次类型：0xcc。  

### Version 5.2.1.15 (build20160608)  

$\bullet$ 大路数 NVR DS-96000N-I 系列 V3.6.0  
$\bullet$ 新增获取配件板信息能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_ACCESSORY_CARD_INFO_CAPABILITIES。  
$\bullet$ 新增获取配件板信息功能（对应接口：NET_DVR_GetSTDConfig）：命令：NET_DVR_GET_ACCESSORY_CARD_INFO。  
 NET_DVR_FindDVRLog_V30(日志查询)和 NET_DVR_LOG_V30(日志查询结果)中 dwMinorType 新增附加信息日志次类型：MINOR_ACCESSORIES_MESSAGE(配件板信息)，新增异常日志次类型：MINOR_ACCESSORIES_PLATE(配件板异常)。  
$\bullet$ 新增错误码：975、976、984\~987。  
$\bullet$ 新增设备类型：DS_96XXXN_IX。  

### Version 5.2.1.5 (build20160506)  

 I 系列 NVR V3.4.8  
$\bullet$ NET_DVR_MONITOR_INFO(网络监听模式配置)使用 144 个保留字节新增参数：struRestrictRemoteIP(限制远程访问 IP)。  
 POS 过滤规则配置协议扩展：1) NET_DVR_POS_FILTER_CFG(POS 过滤规则配置)中参数 byProtocolType(协议类型)新增取值：5-NUCLEUS。2) NET_DVR_POS_PROTOCOL_UNION(POS 协议参数联合体)中新增结构体参数：NET_DVR_POS_NUCLEUS(NUCLEUS 协议参数)。  
 NET_DVR_CHAN_FILTER_CFG(POS 规则与通道关联信息)使用 4 个保留字节新增参数：dwTimeOut(超时时间)。  
$\bullet$ 新增日志类型（对应接口：NET_DVR_FindDVRLog_V30）：报警日志次类型：0x411、0x412。  
$\bullet$ POS 能力集(POSAbility，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)扩展：1) <FilterRule>(过滤规则能力)新增子节点：<NUCLEUS>(NUCLEUS 协议配置)，<protocalType>(协议类型)新增取值：NUCLEUS。2) <ConnectMode>(连接方式能力)中<TCPMonitor>(TCP 网络监听)和<UDPMonitor>(UDP 网络监听)分别新增子节点：<restrictRemoteIPv4>(远程访问 IP 限制)。  

3) <ChanAssociationRule>(通道与规则关联能力)中<timeOut>(POS 数据接收超时时间)。  

$\bullet$ 设备软硬件能力集(BasicCapability，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_SOFTHARDWARE_ABILITY)扩展，<NeedReboot>(是否需要重启)中新增子节点：<NUCLEUSToOther >(nucleus 协议切换到其他协议时是否需要重启)。  

### Version 5.1.6.17 (build20160318)  

 NVR V3.4.6 NET_DVR_VEHICLE_CONTROL_ALARM(车辆报警信息)使用 13 个保留字节新增参数：dwChannel(设备通道号)、dwPicDataLen(图片数据大小)、byPicType(图片类型)、pPicData(图片数据缓冲区)。  

### Version 5.1.6.5 (build20160113)  

 DS-7800HUH-F/N V3.4.50  
$\bullet$ 新增获取云存储 URL 功能（对应接口：NET_DVR_GetSTDConfig）：命令：NET_DVR_GET_CLOUD_URL。  
$\bullet$ 新增获取云存储 URL 能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_CLOUD_URL_CAP。  
$\bullet$ 新增云存储配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_CLOUD_CFG、NET_DVR_SET_CLOUD_CFG。  
$\bullet$ 新增云存储配置能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_CLOUD_CFG_CAP。  
$\bullet$ 新增云存储上传策略配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_CLOUD_UPLOADSTRATEGY、NET_DVR_SET_CLOUD_UPLOADSTRATEGY。  
$\bullet$ 新增云存储上传策略配置能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_CLOUDSTORAGE_UPLOADSTRATEGY_CAP。  
$\bullet$ 新增 POS 过滤规则配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_POS_FILTER_CFG、NET_DVR_SET_POS_FILTER_CFG。  
$\bullet$ 新增 DVR 与 POS 连接方式配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：命令：NET_DVR_GET_CONNECT_POS_CFG、NET_DVR_SET_CONNECT_POS_CFG。  
$\bullet$ 新增规则与通道关联配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_CHAN_FILTER_CFG、NET_DVR_SET_CHAN_FILTER_CFG。  
$\bullet$ 新增 POS 能力集（对应接口：NET_DVR_GetDeviceAbility，对应能力集类型：DEVICE_ABILITY_INFO）：  
$\bullet$ POSAbility。  
$\bullet$ 报警关联处理方式增加联动抓图上传云存储的功能，NET_DVR_MOTION_V40(移动侦测参数)、NET_DVR_HIDEALARM_V40(遮挡报警参数)、NET_DVR_VILOST_V40(信号丢失参数)、NET_DVR_ALARMINCFG_V40(报警输入参数)、NET_DVR_HANDLEEXCEPTION_V40(报警和异常处理参数)、NET_DVR_HANDLEEXCEPTION_V40(报警和异常处理参数)中 dwHandleType(处理方式)分别新增取值：0x1000-抓图上传到云存储。  
$\bullet$ 新增 POS 联动录像和录像搜索功能：1) NET_DVR_RECORDDAY(全天录像参数)中 byRecordType(录像类型)新增取值：21-POS 录像。2) NET_DVR_SEARCH_EVENT_PARAM_V40(按事件搜索的条件参数)扩展，wMajorType(搜索主类型)新增取值：5-pos 录像，uSeniorParam(事件联合体参数)新增结构体参数：struPosAlarm(POS 事件查询参数)。3）NET_DVR_SEARCH_EVENT_RET_V40(按事件搜索结果)中 uSeniorRet(查询结果联合体参数)新增结构体  

参数：struPosRet(POS 事件相关参数)。  

 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)中 byResolution 增加分辨率类型：  

$133{\cdot}3\mathsf{M P}(1920^{\ast}1536/2048^{\ast}1536)$ ，134-5MP(2560\*1944)。  

$\bullet$ 设备通用能力集(对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)，其中通道输入能力(ChannelInputAbility)，<RecordPlan>(录像计划能力)和<RecordQuery>(录像查询能力)的子节点<supportRecordType>新增取值：POS，RecordSchedule>(时间段录像能力)新增子节点：<supportRecordType>(支持的录像能力)。  
$\bullet$ 设备软硬件能力集(BasicCapability，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_SOFTHARDWARE_ABILITY)扩展，新增节点：<UploadCloud>(是否支持抓图上传云存储)、<CloudSupport>(是否支持第三方云)。  
$\bullet$ 设备图像参数能力集(DEVICE_VIDEOPIC_ABILITY，对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_VIDEOPIC_ABILITY)中<alarmHandleType $>$ (处理方式)新增取值：uploadcloud(上传云存储)。  
$\bullet$ 设备通用能力集(对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)，其中事件能力(EventAbility)扩展，<alarmHandleType >(处理方式)新增取值：uploadcloud(上传云存储)。  
$\bullet$ 设备通用能力集(对应接口：NET_DVR_GetDeviceAbility，能力集类型：DEVICE_ABILITY_INFO)，其中录像相关能力(RecordAbility)扩展，<TraversingVirtualPlane >(越界侦测后检索)和<FieldDetection >(区域入侵侦测后检索)中<alarmHandleType >(处理方式)新增取值：uploadcloud(上传云存储)。  

### Version 5.1.3.33 (build20151030)  

$\bullet$ 基线 NVR V3.4.1  

$\bullet$ 新增非授权名单布防时间配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_BLACKLST_SCHEDULE、NET_DVR_SET_VEHICLE_BLACKLST_SCHEDULE。  
$\bullet$ 新增非授权名单布防联动配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_BLACKLIST_EVENT_TRIGGER、NET_DVR_SET_VEHICLE_BLACKLIST_EVENT_TRIGGER。  
$\bullet$ 新增授权名单布防时间配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_WHITELST_SCHEDULE、NET_DVR_SET_VEHICLE_WHITELST_SCHEDULE。  
$\bullet$ 新增支持授权名单布防联动配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_VEHICLE_WHITELIST_EVENT_TRIGGER、NET_DVR_SET_VEHICLE_WHITELIST_EVENT_TRIGGER。  
$\bullet$ 新增导入黑授权名单配置文件功能（对应接口：NET_DVR_UploadFile_V40）：文件类型：UPLOAD_VEHICLE_BLACKWHITELST_FILE。  
$\bullet$ 新增导出黑授权名单配置文件功能（对应接口：NET_DVR_StartDownload）：文件类型：NET_SDK_DOWNLOAD_VEHICLE_BLACKWHITELST_FILE。  
 NET_DVR_SEARCH_EVENT_RET_V40 和 NET_DVR_SEARCH_EVENT_RET(事件录像查询结果)中struStreamIDRet(流 ID 录像查询结果)的参数 dwRecordType(录像类型)新增取值：13-全部事件。  
$\bullet$ 新增错误码： $2101^{\sim}2106$ 。  

### Version 5.1.3.25 (build20150916)  

 90/80/81/73/72HQH(HGH)-SH V3.3.1  

$\bullet$ 新增设备支持 DDNS 国家能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_DDNS_COUNTRY_ABILITY。  
$\bullet$ 录像配置和查找增加支持码流类型：1) NET_DVR_RECORD_V40(通道录像参数)中参数 byStreamType(码流类型)新增取值：2-主码流&子码流。2) NET_DVR_FILECOND_V40(文件查找条件)和 NET_DVR_FINDDATA_V40(文件查找结果)中参数byStreamType(码流类型)分别新增取值：0xff-全部。3) NET_DVR_MRD_SEARCH_PARAM(月历录像分布查询条件)使用 1 个保留字节新增参数：byStreamType(码流类型)。  
 NET_DVR_COMPRESSION_INFO_V30 参数 byResolution 增加分辨率类型：111-960\*1080(1080p Lite)，112-640\*720(half 720p)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中设备通道输入能力(ChannelInputAbility)扩展，节点<recordStreamType>新增取值：2-main_and_sub(主码流&子码流)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中录像相关能力(RecordAbility)扩展，新增节点：<MDRCondStreamType>(月历搜索条件支持的码流类型)。  

### Version 5.1.3.16 (build20150826)  

$\bullet$ 基线 NVR V3.4.0  
$\bullet$ 新增同步 IPC 密码与 NVR 一致功能（对应接口：NET_DVR_STDControl）：命令：NET_DVR_SYNC_IPC_PASSWD。  
$\bullet$ 新增配置字符编码相关处理回调功能（对应接口：NET_DVR_SetSDKLocalCfg）：配置类型：NET_SDK_LOCAL_CFG_TYPE_CHAR_ENCODE。  
$\bullet$ 新增允许在线升级控制功能（对应接口：NET_DVR_STDControl）：命令：NET_DVR_SET_ONLINE_UPGRADE。  
$\bullet$ 新增在线升级相关信息、状态查询功能（对应接口：NET_DVR_GetSTDConfig）：命令：NET_DVR_GET_ONLINEUPGRADE_PROGRESS(在线升级进度)、NET_DVR_GET_FIRMWARECODE(获取识别码)、NET_DVR_GET_ONLINEUPGRADE_SERVER(获取升级服务器状态)、NET_DVR_GET_ONLINEUPGRADE_VERSION(获取新版本信息)、NET_DVR_GET_RECOMMEN_VERSION(检测是否推荐升级到此版本)。  
$\bullet$ 新增能力集（对应接口：NET_DVR_GetSTDAbility）：能力集类型：NET_DVR_GET_TRAFFIC_CAP(抓拍相关能力集)、NET_DVR_GET_ONLINEUPGRADE_ABILITY(在线升级能力集)。  
 NET_DVR_PREVIEWINFO(预览参数)中 dwLinkMode(连接方式)新增取值：6- HRUDP(可靠 UDP 传输)。  
 NET_DVR_DEVICEINFO_V40(设备参数)使用 1 个保留字节新增参数：byCharEncodeType(字符编码格式)。  
 NET_DVR_DIGITAL_CHANNEL_STATE(设备数字通道状态)中的数字通道状态取值新增：NET_SDK_DC_STATUS_POE_PORT_DETECTING(POE 通道检测中)。  
 NET_DVR_VEHICLE_PARA(车辆检测信息)使用 1 个保留字节新增参数：byCountry(国家索引值)。  
$\bullet$ 事件触发能力集(EventTriggersCap)新增节点：<BlackListTriggerCap>(非授权名单事件触发能力)、<WhiteListTriggerCap>(授权名单事件触发能力)。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)新增节点：<isSupportSyncIPCPassword>(是否支持同步 IPC 密码)、<isSupportTransferIPC>(是否支持透传 IPC 协议功能)、<supportPreviewHRUDP>(是否支持HRUDP 预览取流方式)。  
$\bullet$ JPEG 抓图能力集(DEVICE_JPEG_CAP_ABILITY)扩展，<SmartPicSearchInfo>(智能图片检索)中节点<VehicleCond>(车辆检索条件)新增子节点<country>(国家索引)。  
$\bullet$ 设备图像参数能力集(DEVICE_VIDEOPIC_ABILITY)扩展，新增节点：<Sensitivity>(灵敏度节点)。  
$\bullet$ 新增异常日志次类型：MINOR_SYNC_IPC_PASSWD、MINOR_EZVIZ_OFFLINE。  

### Version 5.1.1.3 (build20150318)  

$\bullet$ 更新 V40 登录扩展接口：NET_DVR_Login_V40。  

$\bullet$ 新增设备激活接口：NET_DVR_ActivateDevice。  
$\bullet$ 新增通过 NVR 激活前端设备功能（对应接口：NET_DVR_SetSTDConfig）：命令：NET_DVR_SET_IPDEVICE_ACTIVATED。  
$\bullet$ 新增获取数字通道对应设备安全状态功能（对应接口：NET_DVR_GetDVRConfig）：命令：NET_DVR_GET_DIGITAL_CHAN_SECURITY_STATUS。  
$\bullet$ 新增 NVR 激活前端设备能力集（对应接口：NET_DVR_GetSTDAbility）能力集类型：NET_DVR_GET_ACTIVATE_IPC_ABILITY。  
$\bullet$ 新增设备激活相关错误码：250、251、252。  

### Version 5.0.3.20 (build20150318)  

 NVR V3.3.0  
$\bullet$ 新增 GB28181 服务器参数配置功能（对应接口：NET_DVR_GetSTDConfig 和 NET_DVR_SetSTDConfig）：命令：NET_DVR_GET_GBT28181_SERVICE_CFG、NET_DVR_SET_GBT28181_SERVICE_CFG。  
$\bullet$ 新增 GB28181 服务器能力集（对应接口：NET_DVR_GetSTDAbility）能力集类型：NET_DVR_GET_GBT28181_SERVICE_CAPABILITIES。  
 NET_DVR_SADPINFO(SADP 搜索的 IPC 信息)使用 32 个保留字节新增参数：szGB28181DevID[DEV_ID_LEN](GB28181 协议接入时的设备 ID)。  
 NET_DVR_IPDEVINFO_V31(IP 设备信息)使用 32 个保留字节新增参数：szDeviceID[DEV_ID_LEN](设备 ID)。  
 NET_DVR_DDNSPARA_V30(DDNS 网络应用参数)使用 5 个保留字节新增参数：wCountryID(国家编号)、byStatus(DDNS 运行状态)。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)新增节点：<DDNSStatus>(DDNS 运行状态能力)、<supportGB28181Service>(支持 GB28181 服务参数配置)。  

### Version 5.0.2.15 (build20141212)  

 DS_96XXN_FX、DS_86XXN_FX V3.2.0  

$\bullet$ 按事件查找录像文件接口扩展：NET_DVR_FindFileByEvent_V40、NET_DVR_FindNextEvent_V40。  
$\bullet$ 图片查找接口扩展：NET_DVR_FindNextPicture_V40。  
$\bullet$ 新增智能图片查找接口：NET_DVR_SmartSearchPicture、NET_DVR_FindNextSmartPicture、NET_DVR_CloseSmartSearchPicture。  
$\bullet$ 新增简易智能假日计划配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_SMD_HOLIDAY_HANDLE、NET_DVR_SET_SMD_HOLIDAY_HANDLE。  
$\bullet$ 新增获取所有被锁定信息功能（对应接口：NET_DVR_StartRemoteConfig 和NET_DVR_GetNextRemoteConfig）：命令：NET_DVR_GET_LOCKED_INFO_LIST。  
$\bullet$ 新增用户解锁功能（对应接口：NET_DVR_RemoteControl）：命令：NET_DVR_UNLOCK_USER。  
$\bullet$ 智能搜索扩展：1) NET_DVR_SMART_SEARCH_PARAM(智能搜索条件)的 bySearchCondType(智能查找类型)新增取值：3-人脸侦测。2) NET_DVR_AREA_SMARTSEARCH_COND_UNION(智能查找条件联合体)新增结构体参数：NET_DVR_FACEDETECTION_SEARCHCOND。3) NET_DVR_TRAVERSE_PLANE_SEARCHCOND(越界侦测录像查找条件)和NET_DVR_INTRUSION_SEARCHCOND(区域入侵录像查找条件)分别使用 37 个保留字节新增参数：byAdvanceType(组合方式)、uAdvanceCond(组合属性联合体)。  
 NET_DVR_DISK_RAID_INFO(磁盘 Raid 信息)使用 1 个保留字节新增参数：bySleepStatus(休眠状态)。  
 NET_DVR_CORRIDOR_MODE(旋转功能配置)使用 1 个保留字节新增参数：byMirrorMode(镜像方式)。  
 NET_DVR_GUARD_CFG(车牌侦测计划配置)使用 424 个保留字节新增参数：dwMaxRelRecordChanNum(最大支持触发的录像通道数)、dwRelRecordChanNum(报警触发的录像通道数实际个数)、dwRelRecordChan[MAX_CHANNUM_V30](报警触发的录像通道)、struHolidayTime[MAX_TIMESEGMENT_V30](假日布防时间)。  
 NET_DVR_PHY_DISK_INFO(物理磁盘信息)中 byStatus(硬盘状态)新增取值：9-休眠。  
 NET_DVR_CAPTURE_DAY(全天抓图计划)和 NET_DVR_CAPTURE_SCHED(时间段抓图布防计划)中byCaptureType(抓图类型)新增取值：8-全部事件。  

### Version 4.3.0.5 (build20140627)  

 Netra 平台设备 V3.1.3  

 NET_DVR_INTRUSION_SEARCHCOND(区域入侵录像查找条件)使用 12 字节新增参数：struPTZPosInfo(PTZ坐标信息)。  
 NET_DVR_VCA_DETION_CFG(智能侦测参数)使用 32 字节新增参数：struHolidayTime[MAX_TIMESEGMENT_V30](假日布防时间)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中事件能力(EventAbility)，<VCADetection $>$ 新增子节点<holidaySched>(是否支持假日计划)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中录像相关能力(RecordAbility)，<TraversingVirtualPlane $>$ 和<FieldDetection>新增子节点：<supportPTZInfo>(检索时是否支持带 PTZ 信息)。  
$\bullet$ 新增操作日志的参数类型：PARA_DETECTION(侦测配置)。  
$\bullet$ 新增支持越界侦测和区域侦测配置功能：NET_DVR_GET_TRAVERSE_PLANE_DETECTION、NET_DVR_SET_TRAVERSE_PLANE_DETECTION，NET_DVR_GET_FIELD_DETECTION、NET_DVR_SET_FIELD_DETECTION。  
$\bullet$ 复用按流 ID 方式获取录像状态功能（对应接口：对应接口：NET_DVR_GetDeviceConfig 和NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_STREAM_RECORD_STATUS、NET_DVR_SET_STREAM_RECORD_STATUS  
$\bullet$ 复用流 ID 模式按时间段锁定录像文件功能：NET_DVR_LockStreamFileByTime、NET_DVR_UnlockStreamFileByTime。  

### Version 4.3.0.2 (build20140510)  

 Netra 平台设备 V3.1.2  
$\bullet$ 新增参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_CLOUD_STORAGE_CFG(云存储工作模式配置)。  
$\bullet$ 新增录像上传功能（对应接口：NET_DVR_UploadFile_V40）：命令：UPLOAD_RECORD_FILE。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)中 byResolution(分辨率)新增取值： $67\!-2592^{*}1944$ 。  
 NET_DVR_PREVIEW_SWITCH_CFG(本地预览切换参数)中 byPreviewNumber(预览画面分割模式)新增取值：9- 64 画面。  
 NET_DVR_DISK_QUOTA(磁盘配额信息)，使用 2 个保留字节新增参数：wStoragePeriod(录像存储周期)，byQuotaType(磁盘配额类型)新增取值：2- 按比例、3- 按时间。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中录像相关能力(RecordAbility)扩展，新增节点：<RecordLockTime>(录像锁定时间)。  
$\bullet$ 设备数字通道能力集(DEVICE_DYNCHAN_ABILITY)，新增节点：<ANRCfgReconnect>(ANR 功能配置后设备是否需要重连)。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)扩展，新增节点：<QuotaByTime>(是否支持磁盘配额按时间分配)、<CloudStorageModeChangeReboot>(云存储模式切换是否需要重启)、<VCADetection>(是否支持智能侦测)。  
$\bullet$ 新增异常日志次类型： $0\!\times\!48$ 。  
$\bullet$ 新增操作日志次类型： $0{\times}2110$ 、 $0{\times}211{\bmod{\Omega}}$ 、0x2120\~0x2126。  
$\bullet$ 新增错误号：822、823。  

### Version 4.2.8.7 (build20140408)  

$\bullet$ 经济型 NVR(DS_77XXN_E4 等) V3.0.3  
$\bullet$ 新增设备类型：DS_76XXN_EX、DS_77XXN_E4、DS_86XXN_E8。  
$\bullet$ 异常参数配置，NET_DVR_EXCEPTION_V30 的参数 struExceptionHandleType 和 NET_DVR_EXCEPTION_V40  
的参数 struExceptionHandle，新增取值定义：数组 15-POE 供电异常。  
$\bullet$ 报警信息上传，NET_DVR_ALARMINFO_V30 和 NET_DVR_ALRAM_FIXED_HEADER 的参数 dwAlarmType 新增节点取值定义：16-POE 供电异常。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力(EventAbility)的节点<exceptionType>新增取值：POEPoweException。  

### Version 4.2.8.1 (build20140115)  

$\bullet$ 高新性能 NVR(256 路 NVR) V3.0.2  
$\bullet$ 新增设备类型：DS_96XXX_N_E(256 路)  
$\bullet$ 参数配置扩展（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_ALARMINCFG_V40(报警输入配置)、NET_DVR_USER_V40(用户参数配置)、NET_DVR_EXCEPTION_V40(异常参数配置)、NET_DVR_HDGROUP_CFG_V40(盘组管理配置)，分别扩展报警输入、用户、异常类型、盘组个数。  
 IP 报警输入输出接入信息获取功能扩展（对应接口：NET_DVR_GetDVRConfig）：NET_DVR_IPALARMINCFG_V40、NET_DVR_IPALARMOUTCFG_V40，扩展报警输入输出个数。  
$\bullet$ 新增抓图参数配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_JPEG_CAPTURE_CFG_V40(获取设备抓图配置)、NET_DVR_SET_JPEG_CAPTURE_CFG_V40(设置设备抓图配置)。  
$\bullet$ 新增获取设备工作状态功能（对应接口：NET_DVR_GetDeviceConfig）：命令：NET_DVR_GET_WORK_STATUS。  
$\bullet$ 新增报警信息上传（对应接口：NET_DVR_SetDVRMessageCallBack_V30 和 NET_DVR_StartListen_V30）：NET_DVR_ALARMINFO_V40(移动侦测、视频丢失、遮挡、IO 信号量等报警信息，报警数据可变长)。  
 NET_DVR_SEARCH_EVENT_PARAM(按事件搜索的条件参数)中联合体 uSeniorParam 新增结构参数：struAlarmParamByValue(按值表示的报警输入参数)、struMotionParamByValue(按值表示的移动侦测参数)、struVcaParamByValue(按值表示的异常行为识别参数)。  
 NET_DVR_DEVICECFG_V40(设备参数配置)使用 6 个保留字节新增参数：byStartAlarmInNo(模拟报警输入起始号)、byStartAlarmOutNo(模拟报警输出起始号)、byStartIPAlarmInNo(IP 报警输入起始号)、byStartIPAlarmOutNo(IP 报警输出起始号)、byHighIPChanNum(数字通道个数高 8 位)。  
 NET_DVR_PREVIEW_SWITCH_COND(本地预览输出接口参数)中 byVideoOutType(视频输出接口类型)新增  

取值：7-辅助 HDMI、8-扩展 HDMI1、9-扩展 HDMI2、10-扩展 HDMI3、11--扩展 HDMI4。 NET_DVR_AUXOUTCFG(辅助输出参数配置)中 dwAlarmOutChan(报警弹出画面的输出通道)新增取值：5-HDMI、6-VGA、7- 辅助 HDMI1、8-扩展 HDMI1、9-扩展 HDMI2、10-扩展 HDMI3、11-扩展 HDMI4。 NET_DVR_DIGITAL_CHANNEL_STATE(设备数字通道状态)使用 384 字节新增：byDigitalAudioChanTalkStateEx[192](数字语音通道的对讲状态)、byDigitalChanStateEx[192](数字通道的连接状态)。$\bullet$ 直接从设备取流配置扩展，支持选择取流协议(TCP、UDP、多播等)、码流类型(主码流、子码流)和设备厂家类型：NET_DVR_STREAM_MODE(取流模式)中 byGetStreamType(取流方式)新增取值：6- 直接从设备取流(扩展)；NET_DVR_GET_STREAM_UNION(不同取流方式联合体)新增结构：NET_DVR_IPCHANINFO_V40(直接从设备取流扩展)。$\bullet$ 新增异常日志次类型：0x46、0x47。  

### Version 4.2.7.6 (build20131231)  

 Netra 平台设备 V3.1.0  
$\bullet$ 新增参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_VIDEO_AUDIOIN_CFG(视频的音频输入配置，可绑定语音对讲通道)、NET_DVR_CMS_PARAM(平台参数配置)。  
$\bullet$ 新增批量配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_VCA_DETION_CFG(获取智能侦测参数)、NET_DVR_SET_VCA_DETION_CFG(设置智能侦测参数)。  
$\bullet$ 新增回放转码命令（对应接口：NET_DVR_PlayBackControl_V40）：NET_DVR_PLAY_CONVERT。  
$\bullet$ 新增报警信息上传（对应接口：NET_DVR_SetDVRMessageCallBack_V30 和 NET_DVR_StartListen_V30）：NET_DVR_ALARM_HOT_SPARE $^{\mathrm{N}+1}$ 热备异常报警)。  
 NET_DVR_PREVIEW_SWITCH_CFG(本地预览切换参数配置)中 byPreviewNumber(画面分割模式)新增取值：6- 25 画面、7- 32 画面、8- 36 画面。  
 NET_DVR_MRD_SEARCH_RESULT(月历录像分布查询结果)使用 31 个保留字节新增参数：byHasEventRecode(有无事件录像)。  
 NET_DVR_BACKUP_LOG_PARAM(日志备份参数)使用 1 个保留字节新增参数：byAllLogBackUp(按磁盘号备份还是全部备份)。  
$\bullet$ 获取备份的进度 NET_DVR_GetBackupProgress 中 pState 新增进度值：BACKUP_NO_LOG_FILE(硬盘中无日志)。  
 NET_DVR_RECORDDAY(全天录像参数)中 byRecordType(录像类型)新增取值：19-智能侦测（越界侦测|区域入侵|进入区域|离开区域|人脸抓拍）。  
 NET_DVR_CAPTURE_DAY(全天抓图计划参数)、NET_DVR_CAPTURE_SCHED(时间段抓图计划参数)byCaptureType(抓图类型)新增取值： 7-智能侦测抓图。  
 NET_DVR_FILECOND_V40(录像查找条件)中 dwFileType(文件类型)和NET_DVR_FINDDATA_V40(录像查找结果)中 byFileType(文件类型)分别新增取值：19-智能侦测（越界侦测|区域入侵|进入区域|离开区域|人脸抓拍）。  
 NET_DVR_FIND_PICTURE_PARAM(图片查找条件)byFileType(图片类型)新增取值：0x11-设备本地回放时截图、0x12-智能侦测。  
 NET_DVR_ALARMINFO_V30(设备报警信息)的 dwAlarmType(报警类型)新增取值：15-智能侦测。  
 NET_DVR_SEARCH_EVENT_PARAM(按事件搜索的条件参数)中，使用 1 个保留字节新增参数：byValue(通道号按值还是按位表示)；联合体 uSeniorParam 新增结构参数：struVCADetectByBit(按位表示的智能侦测参数)、struVCADetectByValue(按值表示的智能侦测参数)；MAIN_EVENT_TYPE(事件查找主类型)新增枚举  

类型：EVENT_VCA_DETECTION(智能侦测)，对应次类型取值：VCA_DETECTION_MINOR_TYPE。  

 NET_DVR_SMART_SEARCH_PARAM(智能搜索条件参数)中，使用 1 个保留字节新增参数：bySearchCondType(智能查找类型)，byMotionScope[64][96]更改为NET_DVR_AREA_SMARTSEARCH_COND_UNION(智能查找条件联合体)，支持查询移动侦测，越界侦测、区域入侵等智能录像。  

 NET_SDK_IPC_CFG_FILE_ERR_CODE(导入 IPC 配置文件错误号)新增枚举类型：NET_SDK_IPC_CFG_FILE_ERR_CODE_TRANSPORT_PROTOCOL_INVALID(传输协议错误)。  
 NET_DVR_COMPRESSION_INFO_V30(码流压缩参数)中 byResolution(分辨率)新增取值： $50{\cdot}720^{*}720$ 、51-1280\*1280、52-2048\*768、53-2048\*2048、54-2560x2048、55-3072x2048、 $58–1600^{*}600$ 。  
 NET_DVR_DIGITAL_CHANNEL_STATE(数字通道状态)新增状态类型：NET_SDK_DC_STATUS_RESOLUTION_NOT_SUPPORT(IPC 分辨率不支持)。  
$\bullet$ 获取阵列一键配置的进度(NET_DVR_FastConfigProcess 中 pState)新增取值：PROCESS_QUICK_SETUP_PD_COUNT(一键配置至少需要三块空闲盘)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中本地预览切换能力 PreviewSwitchAbility，新增节点：<VideoOutList>(视频本地输出能力)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中录像相关能力 RecordAbility，新增节点：<monthlyDistributionAndRecodeType>(是否支持月历搜索中的录像类型)、<PlayConvert>(回放转码压缩参数能力)、<TraversingVirtualPlane>(越界侦测后检索能力)、<FieldDetection>(区域入侵侦测后检索能力)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中通道输入能力 ChannelInputAbility，新增节点：<VCAFindFile>(是否支持智能事件查找)。  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，报警事件处理能力 EventAbility，新增节点：<supportLogNotCfg>(支持日志但不支持配置)、<VCADetection>(智能侦测处理能力)。  
$\bullet$ 设备软硬件能力集(DEVICE_SOFTHARDWARE_ABILITY)，新增节点：<AllBackupLog>(是否支持全部日志导出)、<VoiceTalkAsAudioIn>(是否支持语音对讲绑定为音频输入)，<AlarmInTypeChange>(修改报警输入类型)新增能力类型：2-需要提示重启。  
$\bullet$ 设备编码能力集(DEVICE_ENCODE_ALL_ABILITY_V20)中帧率（<VideoFrameRate>、<VideoFrameRateN>）新增取值：25-3、26-5、27-7、28-9。  
$\bullet$ 新增报警日志次类型： $0{\times}29{\sim}0{\times}36$   
$\bullet$ 新增操作日志次类型： $0{\times}2117{\sim}0{\times}2116$   
$\bullet$ 新增附加信息日志次类型： $0{\times}66{\sim}0{\times}6\hat{\mathsf{f}}$   
$\bullet$ 新增错误号：NET_SDK_ERR_CHAN_AUDIO_BIND(821)  

### Version 4.2.3.1 (build20130701)  

 Netra 平台设备 V3.0.0  
$\bullet$ 新增设备类型：DS_96XX_N_RX  
$\bullet$ 新增远程配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_N_PLUS_ONE_WORK_MODE_CFG( $\mathsf{N}\!+\!1$ 工作模式配置)、NET_DVR_HD_STATUS(硬盘休眠状态配置)、NET_DVR_RAID_BTS_CFG(RAID 后台任务速度配置)。  
$\bullet$ 新增长连接远程配置功能（对应接口 NET_DVR_StartRemoteConfig）：命令:NET_DVR_IMPORT_IPC_CFG_FILE(导入 IPC 接入配置文件)、NET_DVR_UPGRADE_IPC(通过 NVR 对 IPC升级)。  
$\bullet$ 新增导出 IPC 接入配置文件功能（对应接口：NET_DVR_StartDownload）：命令：NET_SDK_DOWNLOAD_IPC_CFG_FILE。  
$\bullet$ 新增支持 VQD 功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：  

命令：NET_DVR_GET_VQD_LOOP_DIAGNOSE_CFG、NET_DVR_SET_VQD_LOOP_DIAGNOSE_CFG。$\bullet$ 手动获取 VQD 诊断信息（对应接口：NET_DVR_StartRemoteConfig 和 NET_DVR_GetNextRemoteConfig）：命令：NET_DVR_GET_VQD_DIAGNOSE_INFO。 VQD 诊断报警上传（对应接口：NET_DVR_SetDVRMessageCallBack_V30 和 NET_DVR_StartListen_V30）：NET_DVR_VQD_DIAGNOSE_INFO。$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)新增能力集类型（对应接口：NET_DVR_GetDeviceAbility）：$\mathsf{N}\!+\!1$ 能力 NPlusOneAbility、磁盘相关能力 HardDiskAbility、IPC 配置文件导入导出能力IPAccessConfigFileAbility、通道输入能力 ChannelInputAbility。$\bullet$ 设备新增支持转码码流取流：NET_DVR_MULTI_STREAM_COMPRESSIONCFG(多码流压缩参数)、NET_DVR_MULTI_STREAM_COMPRESSIONCFG_COND(多码流压缩参数配置条件)中 dwStreamType 新增取值 4-转码码流；NET_DVR_PREVIEWINFO(预览参数)中 dwStreamType 新增取值 3-虚拟码流。 NET_DVR_FILECOND_V40(文件查找条件)使用 16 个保留字节新增参数：byWorkingDeviceGUID[16](工作机GUID)，其参数 byFindType 增加类型取值：2- 查询 $\mathsf{N}\!+\!1$ 录像文件。 NET_DVR_DIGITAL_CHANNEL_STATE(设备数字通道状态)使用 64 个保留字节新增参数：byDigitalChanState[64](数字通道状态)。 NET_DVR_MOTION_V30(移动侦测参数)使用 1 个保留字节新增参数：byEnableDisplay(启用移动侦测高亮显示)。 NET_DVR_DEVICEINFO_V30(设备参数信息)使用 3 个保留字节新增参数：byStartDChan(起始数字通道号)、byStartDTalkChan(起始数字对讲通道号)、byHighDChanNum(数字通道个数高 8 位)。 NET_DVR_EXCEPTION_V30(异常参数)中 struExceptionHandleType[MAX_EXCEPTIONNUM_V30]取数组 10、11 新增异常类型：10- 行车超速（车载专用），11- 热备异常（ $\mathsf{N}\!+\!1$ 使用）。$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中录像相关能力集(RecordAbility)，新增节点：<findWorkingDeviceRecord>。$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)，其中报警事件处理能力集(EventAbility)，节点<exceptionType>新增取值：spareException。$\bullet$ 设备数字通道能力集(DEVICE_DYNCHAN_ABILITY)，新增节点：<IPCUpgradeAbility>、<ChannelRecordStatus>、<DigitalChanState>。$\bullet$ 设备 RAID 能力集(DEVICE_RAID_ABILITY)，新增节点：<RaidInfo>。$\bullet$ 新增异常日志次类型：MINOR_ANR_RECORD_FAIED、MINOR_SPARE_WORK_DEVICE_EXCEPT、MINOR_START_IPC_MAS_FAILED。$\bullet$ 新增 $\mathsf{N}\!+\!1$ 功能错误号： $803^{\sim}814$ 。  

### Version 4.2.2.2(2013-5-21)  

$\bullet$ Netra 平台 NVR V2.3.1  
$\bullet$ 新增批量参数获取功能（对应接口：NET_DVR_GetDeviceConfig）：命令：NET_DVR_GET_MONTHLY_RECORD_DISTRIBUTION(获取月历录像分布)、NET_DVR_GET_ACCESS_DEVICE_CHANNEL_INFO(获取待接入设备通道信息)  
$\bullet$ 设备本地预览切换参数配置（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：命令：NET_DVR_GET_PREVIEW_SWITCH_CFG、NET_DVR_SET_PREVIEW_SWITCH_CFG  
$\bullet$ 扩展文件查找接口：NET_DVR_FindNextFile_V40，支持日历查询功能  
$\bullet$ 设备通用能力集(DEVICE_ABILITY_INFO)新增能力集类型（对应接口：NET_DVR_GetDeviceAbility）：录像相关能力 RecordAbility、NVR 前端待接入设备通道能力 AccessDeviceChannelAbility、设备本地预览切换能力 PreviewSwitchAbility  
 NET_DVR_FILECOND_V40(文件查找条件)使用 6 个保留字节新增参数：byFindType(存储卷类型)、  

byQuickSearch(查询类型)、dwVolumeNum(存档卷号)。 NET_DVR_VOD_PARA(按时间回放参数)使用 6 个保留字节新增参数：byVolumeType(存储卷类型)、byVolumeNum(存档卷号)、dwFileIndex(存档卷上的录像文件索引)。  

### Version 4.2.1.6(2012-12-26)  

 NETRA 平台设备 V2.3.0  
$\bullet$ 新增设备类型：DS_72XXHF_SV、DS_72XXHW_SV。  
$\bullet$ 新增配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_WD1_CFG(WD1 使能配置)、NET_DVR_RECORD_PACK(录像打包参数)。  
$\bullet$ 新增批量配置功能（对应接口：NET_DVR_GetDeviceConfig 和 NET_DVR_SetDeviceConfig）：NET_DVR_FTPCFG_V40(FTP 扩展配置)。  
$\bullet$ 新增远程控制功能（对应接口：NET_DVR_RemoteControl）：NET_DVR_CMD_TRIGGER_PERIOD_RECORD_PARA。  
$\bullet$ 新增 NAS 目录查找功能（新增接口：NET_DVR_StartRemoteConfig、NET_DVR_GetNextRemoteConfig、NET_DVR_GetRemoteConfigState、NET_DVR_StopRemoteConfig）：对应命令：NET_DVR_FIND_NAS_DIRECTORY。  
$\bullet$ 新增 IPSAN 目录查找接口：NET_DVR_FindIpSanDirectory、NET_DVR_FindNextDirectory、NET_DVR_FindDirectoryClose。  
$\bullet$ 新增日志类型：MINOR_RUN_STATUS_INFO、MINOR_REMOTE_DELETE_HDISK、MINOR_REMOTE_LOAD_HDISK、MINOR_REMOTE_UNLOAD_HDISK、MINOR_LOCAL_OPERATE_LOCK、MINOR_LOCAL_OPERATE_UNLOCK。  
 NET_DVR_SINGLE_HD(设备硬盘信息)中 dwHdStatus(硬盘状态)新增取值：15-正在删除（网络硬盘）。  
 NET_DVR_PU_STREAM_URL(URL 取流配置)使用 4 个保留字节增加参数：byTransPortocol(传输协议类型wIPID(设备 ID 号)和 byChannel(设备通道号)。  
 NET_DVR_GET_STREAM_UNION(不同取流方式联合体)新增通过 hkDDNS 连接设备然后从设备取流的方式：NET_DVR_HKDDNS_STREAM struHkDDNSStream。  

### Version 4.2.1.6(2012-12-25)  

 DS-6700 系列 DVS V1.0.0  
$\bullet$ 新增设备类型：DS_67XXHF_SATA、DS_67XXHW、DS_67XXHW_SATA、DS_67XXHF  
$\bullet$ 新增配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_BONJOUR_CFG(Bonjour 参数配置)、NET_DVR_SOCKS_CFG(SOCKS 参数配置)、NET_DVR_QOS_CFG(QoS 参数配置)、NET_DVR_HTTPS_CFG(HTTPS 参数配置)。  
$\bullet$ 新增远程控制功能（对应接口：NET_DVR_RemoteControl 和 NET_DVR_GetDeviceConfig）：命令：NET_DVR_CREATE_CERT(创建证书)、NET_DVR_DELETE_CERT(删除证书)。  
$\bullet$ 新增获取证书信息的功能（对应接口：NET_DVR_GetDeviceConfig）：命令：NET_DVR_GET_CERT  
$\bullet$ 新增上传证书功能（对应接口：NET_DVR_UploadFile）：命令：UPLOAD_CERTIFICATE  
$\bullet$ 新增文件下载接口：NET_DVR_StartDownload、NET_DVR_GetDownloadState、NET_DVR_StopDownload，下载证书命令：NET_SDK_DOWNLOAD_CERT。  
 NET_DVR_UPNP_CFG、NET_DVR_UPNP_PORT 复用为：NET_DVR_NAT_CFG、NET_DVR_NAT_PORT。  

### Version 4.1.9.3（2012-10-30）  

 Netra 平台 NVR V2.2.2  

$\bullet$ 新增远程控制磁盘操作功能（对应接口：NET_DVR_RemoteControl）：命令：NET_DVR_MOUNT_DISK(加载磁盘)、NET_DVR_UNMOUNT_DISK(卸载磁盘)NET_DVR_DEL_INVALID_DISK(删除无效磁盘)。  
$\bullet$ 新增设置通道视频输入图像参数功能（对应接口：NET_DVR_RemoteControl）：命令：NET_DVR_SET_VIDEO_EFFECT(设置通道视频输入图像参数)。  
$\bullet$ 新增日志类型（对应接口：NET_DVR_FindDVRLog_V30）：异常日志次类型：MINOR_RECORD_OVERFLOW、MINOR_DSP_ABNORMAL，操作日志次类型：MINOR_LOCAL_LOAD_HDISK、MINOR_LOCAL_DELETE_HDISK。  

### Version 4.1.7（2012-8-3）  

$\bullet$ 新增设备类型：DS_76XX_N_SE  
$\bullet$ 获取视频输入图像效果参数默认值（对应接口：NET_DVR_GetDeviceConfig）：命令：NET_DVR_GET_DEFAULT_VIDEO_EFFECT。  
 NET_DVR_VIDEO_EFFECT 保留字节数错误修改，并且增加参数 dwHueValue(色度)、dwSharpness(锐度)、dwDenoising(去噪)。  

### Version 4.1.6（2012-6-28）  

NETRA 平台 V2.2.0  
$\bullet$ 新增设备类型：DS90XXHW_ST、DS72XXHX_SH、DS_92XX_HF_ST、DS_91XX_HF_XT、DS_90XX_HF_XT、DS_77XXN_ST、DS_95XX_N_ST、DS_85XX_N_ST、DS_96XX_N_XT。  
$\bullet$ 新增远程录像文件倒放接口：NET_DVR_PlayBackReverseByName、NET_DVR_PlayBackReverseByTime_V40。  
$\bullet$ 新增获取通道录像起止时间的接口：NET_DVR_InquiryRecordTimeSpan。  
$\bullet$ 新增即时刷新录像索引的接口：NET_DVR_UpdateRecordIndex。  
$\bullet$ 新增录像文件查找扩展接口：NET_DVR_FindFile_V40。  
$\bullet$ 新增 UPNP 端口映射状态查询接口：NET_DVR_GetUpnpNatState。  
$\bullet$ 新增统一备份接口：NET_DVR_Backup。  
$\bullet$ 新增配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_DRAWFRAME_DISK_QUOTA_CFG(抽帧通道磁盘配额)、NET_DVR_UPNP_CFG(UPNP 端口映射配置)、NET_DVR_POE_CFG(POE 参数配置)、NET_DVR_CUSTOM_PROTOCAL(自定义协议配置)、NET_DVR_STREAM_CABAC(码流压缩性能 CABAC 选项配置)、NET_DVR_POE_CHANNEL_ADD_MODE(POE通道添加方式配置) 、NET_DVR_ESATA_MINISAS_USAGE(eSATA 和 miniSAS 用途配置)。  
$\bullet$ 新增配置命令（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_GET_FTPCFG_SECOND、NET_DVR_SET_FTPCFG_SECOND、NET_DVR_GET_HDCFG_V40、NET_DVR_SET_HDCFG_V40。  
$\bullet$ 新增获取设备数字通道状态功能（对应接口：NET_DVR_GetDVRConfig）：NET_DVR_DIGITAL_CHANNEL_STATE。  
$\bullet$ 新增支持加密配置接口：NET_DVR_InquestStreamEncrypt、NET_DVR_InquestGetEncryptState。  
$\bullet$ 新增操作日志的次类型：MINOR_LOCAL_TAG_OPT、MINOR_LOCAL_VOUT_SWITCH、MINOR_STREAM_CABAC。  
 NET_DVR_PlayBackControl_V40 的控制命令 dwControlCode 新增：NET_DVR_PLAY_FORWARD(倒放切换为正放)和 NET_DVR_PLAY_REVERSE(正放切换为倒放)。  
 NET_DVR_DEVICEINFO_V30(设备参数信息)和 NET_DVR_DEVICECFG_V40(设备参数配置)中 bySupport1 新增能力：bySupport1 & 0x2，表示是否支持下载/回放流量区分。  

 NET_DVR_DEVICECFG_V40(设备参数配置)中 byStorageMode(存储模式)新增取值：2- 抽帧模式。 NET_DVR_BACKUP_TIME_PARAM(按时间备份参数)和 NET_DVR_FIND_LABEL(录像标签查找条件)使用 1 个保留字节增加参数 byDrawFrame(是否抽帧)。  

### Version 4.0.9（2011-9-1）  

 NETRA 平设备 V2.1.0  
$\bullet$ 新增设备类型：DS96XXN_ST、DS86XXN_ST、DS80XXHF_ST、DS90XXHF_ST、DS76XXN_ST。  
$\bullet$ 新增参数获取功能（对应接口：NET_DVR_GetDVRConfig）：NET_DVR_SYNCHRONOUS_IPC(是否同步前端 IPC 设备参数)、NET_DVR_DEVICE_NET_USING_INFO (获取当前设备网络资源使用情况)  
$\bullet$ 新增参数设置功能（对应接口：NET_DVR_SetDVRConfig）：NET_DVR_SYNCHRONOUS_IPC(是否同步前端IPC 设备参数)、NET_DVR_IPC_PASSWD(设置 IPC用户名密码)NET_DVR_IPC_NETCFG(设置前端 IPC 的网络地址)。  

### Version 4.0.7（2011-06-13）  

 DS-81/91HW-S(T)系列 V2.0.0  
$\bullet$ 新增设备类型：DS81XXHW_S、DS81XXHW_ST、DS91XXHW_ST。  
$\bullet$ 新增抓图图片分辨率能力集（对应接口：NET_DVR_GetDeviceAbility）：PIC_CAPTURE_ABILITY。  

## Version 4.0.5（2011-06-13）  

$\bullet$ NETRA 平台 V2.0.0  
$\bullet$ 新增设备类型：DS-91XXHF-ST  
$\bullet$ 新增参数配置功能（对应接口：NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）：NET_DVR_HOLIDAY_PARAM_CFG(假日参数配置)、NET_DVR_HOLIDAY_HANDLE(假日报警处理方式配置)、NET_DVR_HOLIDAY_RECORD(假日录像配置)、NET_DVR_NETCFG_MULTI(多网卡网络配置)、NET_DVR_NETWORK_BONDING(网卡 BONDING 配置)、NET_DVR_JPEG_CAPTURE_CFG(抓图参数配置)、NET_DVR_SCHED_CAPTURECFG(抓图计划配置)、NET_DVR_FTPCFG(FTP 参数配置)、NET_DVR_DISK_QUOTA_CFG(磁盘配额配置)、NET_DVR_SNMPCFG(SNMP 协议配置)、NET_DVR_VIDEO_INPUT_EFFECT(通道视频输入图像参数配置)。  
$\bullet$ 新增获取通道设备工作状态的功能（对应接口：NET_DVR_GetDVRConfig）：NET_DVR_LINK_STATUS。  
$\bullet$ 新增网络流量检测功能：NET_DVR_StartNetworkFlowTest、NET_DVR_StopNetworkFlowTest。  
$\bullet$ 新增加录像标签功能：NET_DVR_InsertRecordLabel、NET_DVR_DelRecordLabel、NET_DVR_FindRecordLabel、NET_DVR_FindNextLabel、NET_DVR_StopFindLabel。  
$\bullet$ 新增图片回放备份功能：NET_DVR_FindPicture、NET_DVR_FindNextPicture、NET_DVR_CloseFindPicture、NET_DVR_GetPicture_V30、NET_DVR_BackupPicture。  

### 3 函数调用顺序  

#### 3.1SDK基本调用的主要流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/06b7103869257406f1be4f9a11e19f53b749465b0b8f73dac373b2a0503935e7.jpg)  
图 3.1 SDK 基本流程  

图 3.1 中虚线框的流程是可选部分，不会影响其他流程和模块的功能使用。按实现功能的不同可以分成十个模块，实现每个模块的功能时初始化 SDK、用户注册设备、注销设备和释放 SDK 资源这 4 个流程是必不可少的，解码器功能模块和异常行为识别功能模块是针对解码器和智能设备的，在该文档里我们不做描述。  

 初始化 SDK（NET_DVR_Init）：对整个网络 SDK 系统的初始化，内存预分配等操作。设置连接超时时间（NET_DVR_SetConnectTime）：这部分为可选，用于设置 SDK 中的网络连接超时时间，用户可以根据自己的需要设置该值。在不调用此接口设置超时时间的情况下，将采用 SDK 中的默认值。  

 设置接收异常消息的回调函数（NET_DVR_SetDVRMessage 或 NET_DVR_SetExceptionCallBack_V30）：由于 SDK 中大部分模块的功能都是由异步模式实现，所以我们提供此接口用于接收预览、报警、回放、透明通道和语音对讲等模块发生异常信息。用户可以在初始化 SDK 后就设置该回调函数，在应用层对各个模块异常消息的接收和处理。  

 从解析服务器获得设备的 IP 地址（NET_DVR_GetDVRIPByResolveSvr_EX）：该接口提供一种在仅知道设备名称（或 DDNS 域名）或者序列号的情况下，从解析服务器获得设备 IP 地址的方法。如：当前设备是通过拨号上网方式获取到动态 IP 地址，而运行了我公司 IPServer 软件的服务器即为解析服务器或者设备注册到我公司 DDNS 服务器上，我们可以通过此接口输入服务器的地址、设备的名称或序列号等信息查询该设备的 IP 地址。  

 用户注册设备（NET_DVR_Login_V30）：实现用户的注册功能，注册成功后，返回的用户 ID 作为其他功能操作的唯一标识，SDK 允许最大注册用户数为 512 个。就设备而言，V3.0 以上版本支持的设备允许有 32 个注册用户名，而且同时最多允许 128 个用户注册；V3.0 以下版本支持的设备允许有 16 个注册用户名，而且同时最多允许 128 个用户注册。  

预览模块：从设备取实时码流，解码显示以及播放控制等功能，同时支持软解码和解码卡解码。具体流程详见预览模块流程。  

回放和下载模块：可以通过按时间和按文件名的方式远程回放或者下载设备的录像文件，后续可以进行解码或者存储。同时还支持断点续传功能（需要设备支持）。具体流程详见回放和下载模块流程。  

参数配置模块：设置和获取设备的参数，主要包括设备参数、网络参数、通道压缩参数、串口参数、报警参数、异常参数、交易信息和用户配置等参数信息。具体流程详见参数配置模块流程。  

远程设备维护模块：实现关闭设备、重启设备、恢复默认值、远程硬盘格式化、远程升级和配置文件导入/导出等维护工作。具体流程详见远程设备维护模块流程。  

语音对讲转发模块：实现和设备的语音数据对讲和语音数据获取，音频编码格式可以指定。具体流程详见语音对讲转发模块流程。  

报警模块：处理设备上传的各种报警信号。报警分为“布防”和“监听”两种方式，在采用监听方式并且不需要获取用户 ID 的情况下，报警模块可以无需进行“用户注册”操作步骤。具体流程详见报警模块流程。  

 透明通道模块：透明通道是将 IP 数据报文解析后直接发送到串行口的一种技术。实际上起到了延伸串行设备控制距离的作用。可利用 IP 网络控制多种串行设备，如控制解码器、矩阵、报警主机、门禁、仪器仪表等串行设备，对用户来说，只看到点对点传输，无须关心网络传输过程，所以称为串口透明通道。 SDK 提供 485 和 232 串口作为透明通道功能，其中要将 232 串口作为透明通道使用，首先必须在 232 串口的配置信息（NET_DVR_RS232CFG）中将工作模式选为透明通道，这样 232 串口才可作为透明通道使用。具体流程详见透明通道模块流程。  

云台控制模块：实现对云台的基本操作、预置点、巡航、花样扫描和透明云台的控制。SDK 将云台控制分为两种模式：一种是通过图像预览返回的句柄进行控制；另一种是无预览限制，通过用户注册 ID 号  

进行云台控制。  

#### 3.2IP 通道相关说明  

DVR 视频输入接模拟摄像机，其通道称为模拟通道；混合型 DVR、NVR 等设备支持 IPC 接入，通道称为IP 通道（或者数字通道），配置相关参数时需调用 IP 接入配置参数来进行资源的获取和重新分配。  

 客户端通过注册设备（NET_DVR_Login_V30）返回的设备信息 NET_DVR_DEVICEINFO_V30 获取模拟通道个数（byChanNum）、模拟通道起始通道号（byStartChan）和设备支持的最大 IP 通道数（byIPChanNum $^+$ byHighDChanNum $^{*}256$ ）、数字通道起始通道号（byStartDChan）。  

 从 byStartChan 到 byStartChan $^+$ byChanNum-1 对应为模拟通道的通道号，IP 通道的通道号为 byStartDChan到 byStartDChan $^+$ (byIPChanNum $^+$ byHighDChanNum $^{*}256$ ) -1。DVR 只有模拟通道，NVR 只有 IP 通道，混合型 DVR 同时支持模拟通道和 IP 通道。  

 如果设备支持 IP 通道个数大于 0，则可以通过远程参数配置接口 NET_DVR_GetDVRConfig（配置命令：NET_DVR_GET_IPPARACFG_V40）可以获取得到设备详细的 IP 资源信息（NET_DVR_IPPARACFG_V40），包括模拟通道是否禁用（byAnalogChanEnable）、IP 通道个数（dwDChanNum）、IP 通道起始通道号（dwStartDChan）、IP 通道取流模式、IP 通道有效状态和在线状态等。通过远程参数配置接口NET_DVR_SetDVRConfig（配置命令：NET_DVR_SET_IPPARACFG_V40）可对设备进行 IP 资源配置，包括添加、修改、删除 IP 通道等。  

 混合型 DVR 或 NVR 的 IP 报警输入和报警输出的通道是在音视频 IP 通道资源分配好后，由设备自动分配的。如果要对 IP 报警参数进行配置，首先通过命令 NET_DVR_GET_IPALARMINCFG_V40 和NET_DVR_GET_IPALARMOUTCFG_V40 获取 IP 报警输入资源（NET_DVR_IPALARMINCFG_V40）和 IP 报警输出资源（NET_DVR_IPALARMOUTCFG_V40）。然后通过命令 NET_DVR_SET_ALARMINCFG_V40 可以配置报警数相关参数(NET_DVR_ALARMINCFG_V40)，包括报警输入名称、报警器类型、布防时间、联动方式等，通过命令 NET_DVR_SET_ALARMOUTCFG_V30 可以配置报警输出相关参数(NET_DVR_ALARMOUTCFG_V30)，比如报警输出名称、布防时间、输出报警延时等。 相关接口：NET_DVR_GetDVRConfig、NET_DVR_SetDVRConfig。  

#### 3.3实时预览模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/0d03e2add064c514c20cd830b71a6d8cc85e2dc6afdf2e0943ca49f423d72353.jpg)  
图 3.2 实时预览模块流程  

图 3.2 中虚线框部分的模块是与预览模块相关，必须在启动预览后才能调用，这些模块之间是并列的关系，各自完成相应的功能。  

声音控制功能主要实现独占、共享声音的打开和关闭；音量的控制。相关接口有：NET_DVR_OpenSound、NET_DVR_CloseSound、NET_DVR_OpenSoundShare、NET_DVR_CloseSoundShare、NET_DVR_Volume 等。实时流数据捕获和录像模块主要实现数据回调和本地录像的功能，可以供用户后续处理。相关接口有：NET_DVR_SetRealDataCallBack、NET_DVR_SetStandardDataCallBack、NET_DVR_SaveRealData 等。抓图功能主要实现对当前解码图像的捕获，保存格式为 BMP。相关接口有：NET_DVR_CapturePicture。NET_DVR_CaptureJPEGPicture 支持登录后直接从设备抓取 JPEG 图片。  
云台控制模块主要是在开启预览的前提下实现对云台控制的操作功能，包括云台预置点、巡航、花样扫描和透明云台等。相关接口有：NET_DVR_PTZControl、NET_DVR_PTZPreset、NET_DVR_PTZCruise、NET_DVR_PTZTrack、NET_DVR_TransPTZ。  

#### 实时流解码方式  

 方式一：在预览接口 NET_DVR_RealPlay_V40 中预览参数的播放窗口句柄赋成有效句柄，则由 SDK 实现解码功能。在初始化 SDK 和注册设备两步骤后，直接调用启动预览和停止预览接口。  

方式二：用户可以通过设置预览接口 NET_DVR_RealPlay_V40 中预览参数的播放窗口句柄为空值，并通过调用捕获数据的接口（即设置 NET_DVR_RealPlay_V40 接口中的回调函数或调用NET_DVR_SetRealDataCallBack、NET_DVR_SetStandardDataCallBack 接口），获取码流数据进行后续解码播放处理。  

#### 3.4回放和下载模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/41cfc70e6997ba509f9ad0411445510232025eda43164548f140b8242b9a6f11.jpg)  
图 3.3 回放和下载模块流程  

按文件回放或下载需要通过查找录像文件功能先获取文件信息（相关接口 NET_DVR_FindFile_V40、NET_DVR_FindNextFile_V40 ）， 然 后 根 据 获 取 到 的 文 件 名 开 始 回 放 或 下 载 （ 相 关 接 口  

NET_DVR_PlayBackByName、NET_DVR_GetFileByName），特别提醒在调用了回放或下载的接口后，还必须调用控制接口（NET_DVR_PlayBackControl_V40）的开始播放命令（NET_DVR_PLAYSTART）。  

 按时间回放或下载文件时，用户可以无需调用查找录像文件的相关接口，只要在接口中指定开始和结束时间，调用回放或下载接口（相关接口 NET_DVR_PlayBackByTime_V40、NET_DVR_GetFileByTime_V40）后，还必须调用控制接口（NET_DVR_PlayBackControl_V40）的开始播放命令（NET_DVR_PLAYSTART）。此时，将按照指定时间范围内最近的有录像的时间段开始回放或下载。用户也可以通过调用查找录像文件的相关接口，获取文件的开始和结束时间后，按这个时间范围指定回放或下载接口中的时间参数，最后还必须调用控制接口（NET_DVR_PlayBackControl_V40）的开始播放命令（NET_DVR_PLAYSTART）。  

 回 放 或 下 载 文 件 时 ， 在 调 用 控 制 接 口 （ NET_DVR_PlayBackControl_V40 ） 的 开 始 播 放 命 令（NET_DVR_PLAYSTART）之前，可以调用控制接口（NET_DVR_PlayBackControl_V40）的设置转码类型的命令（NET_DVR_SET_TRANS_TYPE）。这样回放回调函数或下载获取的录像数据为转封装之后的数据，支持的转封装格式有：PS、TS、RTP。  

#### 3.5参数配置模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/2f20a42ebf1e253be51454b2e58fe53bbd1b88125e8812661ce7edc6bbb43112.jpg)  
图 3.4 参数配置模块流程  

 实现参数配置首先必须做好初始化 SDK 和用户注册这两个步骤，将用户注册接口返回的 ID 号作为配置接口的参数。建议在每次设置某类参数之前，先调用获取参数的接口（NET_DVR_GetDVRConfig）得到完整的参数结构，修改需要更改的参数，作为设置参数接口中的输入参数，最后调用设置参数接口（NET_DVR_SetDVRConfig），返回成功即设置成功。  

#### 3.6远程设备维护模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/94cc18fb1c4f23cfb11db571682dcf6ec4d6314af7a7e5c80b9907268535c357.jpg)  
图 3.5 设备维护模块流程  

远程设备维护模块包括获取设备工作状态、远程升级、日志查找、恢复设备默认参数和导入、导出配置文件等功能。  

获取设备工作状态：可以获取到设备当前的硬盘状态、通道状态、报警输入和输出口状态、本地显示状态和语音通道状态等信息。相关接口有:NET DVR GetDeviceConfig(命令:NET_DVR_GET_WORK_STATUS)等。远程升级：对设备进行升级，并且可以获取当前升级的进度和状态。相关接口有：NET_DVR_Upgrade、NET_DVR_GetUpgradeProgress、NET_DVR_GetUpgradeState 等。日志查找：可以搜索到当前设备的日志信息，包括报警、异常、操作和带 S.M.A.R.T 信息的日志。相关接口有：NET_DVR_FindDVRLog_V30、NET_DVR_FindNextLog_V30 等。  
 恢复设备默认参数：调用接口 NET_DVR_RestoreConfig 能将设备的所有参数都恢复成默认值。  
 导入、导出配置文件：将设备目前的所有配置信息导出保存或者将指定的配置信息导入到设备。相关接口有：NET_DVR_GetConfigFile_V30、NET_DVR_GetConfigFile、NET_DVR_SetConfigFile_EX、NET_DVR_SetConfigFile 等。网络流量检测：检测设备当前的发送和接收的网络流量（kbps）。相关接口：NET_DVR_StartNetworkFlowTest、NET_DVR_StopNetworkFlowTest  

#### 3.7语音对讲转发模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/33216b696863c8deba285252919399a5b5acc3cc6d2773b074ae0dd4a8c9f0ba.jpg)  
图 3.6 语音对讲和转发模块流程  

语音对讲功能实现 PC 机与设备间音频的发送和接收。在成功注册设备后调用  
NET_DVR_StartVoiceCom_V30 接口完成，同时在该接口中用户可以通过设置回调函数获取当前设备发送或者 PC 机采集的数据（按需要选择回调编码后或者 PCM 数据）。  
语音转发功能实现将待发送的音频数据（编码后）转发给设备。首先调用  
NET_DVR_StartVoiceCom_MR_V30 接口启动与设备的语音转发（此时已建立与设备之间的连接，等待发送数据）。第二，准备好待发送的数据（需要经过编码），相对于上图中虚线框部分，如果数据已按本公司的压缩格式处理这部分就可以省略。数据源可以是从 PC 声卡中采集或是从文件中读取，但是需要经过本公司提供的压缩算法进行压缩处理，SDK 提供一套编码接口，方法如下：  
设备语音对讲音频编码格式为 G711：调用 NET_DVR_EncodeG711Frame 进行音频编码。  
设备语音对讲音频编码格式为 G722：1）NET_DVR_InitG722Encoder 初始化音频编码；2）NET_DVR_EncodeG722Frame 进行 G722 音频编码；3）当结束所有的编码过程，需要调用 NET_DVR_ReleaseG722Encoder 释放编码音频资源。设备语音对讲音频编码格式为 G726：1）NET_DVR_InitG726Encoder 初始化音频编码；2）NET_DVR_EncodeG726Frame 进行 G726 音频编码；3）当结束所有的编码过程，需要调用 NET_DVR_ReleaseG726Encoder 释放编码音频资源。经过第二部的编码操作，我们可以每次得到固定大小的且经过编码后的数据，调用  
NET_DVR_VoiceComSendData 接口发送这些数据给设备。等所有的转发操作完成后，调用  
NET_DVR_StopVoiceCom 接口结束与设备的语音转发连接。  
Windows 64 位或者 Linux 系统下只支持语音转发功能，语音对讲、语音广播、音频编解码接口均不支持  

#### 3.8报警模块流程  

#### 3.8.1 报警（布防）流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/d00fe09a228304b22372e74fd20b0aaef5185bb79f800a0ddb2a64b7759d1d26.jpg)  
图 3.7 报警布防流程  

“布防”报警方式：是指 SDK 主动连接设备，并发起报警上传命令，设备发生报警立即发送给 SDK。  

 由“报警（布防）的流程图”中看出，“布防”方式需要先进行用户注册（NET_DVR_Login_V30）。虚线框部分是实现报警信息上传的必要条件，主要完成相关的报警条件和处理方法的配置，参数配置的接口为NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig。支持的报警类型有移动侦测、视频信号丢失、遮挡和信号量报警，其中前三种报警类型对应的报警条件和处理方法的配置结构体是NET_DVR_PICCFG_V40，而信号量报警的配置结构体是 NET_DVR_ALARMINCFG_V40。这些参数如果已经配置完成，那么虚线框部分可以省略。接下来就是设置报警回调函数（NET_DVR_SetDVRMessageCallBack_V30 等），调用成功后还需要设置布防（NET_DVR_SetupAlarmChan_V41）。整个报警上传过程结束后还需要调用撤防接口等操作。  

#### 3.8.2 报警（监听）流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/70fb662c3efbbdf8908990f7f4f302ce1bb43011dd47f8d82bacb0dd273ef0a6.jpg)  
图 3.8 报警监听流程  

“监听”报警方式：是指 SDK 不主动发起连接设备，只是在设定的端口上监听接收设备主动上传的报警信息。  

 这个过程需要远程配置设备的报警主机地址（即 PC 机地址）和报警主机端口（即 PC 的监听端口），报警主机就在该端口上监听接收设备主动上传的报警信息。如果报警主机地址和报警主机端口已配置完成，那么“报警（监听）的流程图”中虚线框“用户注册”和“配置报警主机地址和端口”部分就可以省略，但事先没有配置，就必须调用参数配置接口（NET_DVR_GetDVRConfig 和 NET_DVR_SetDVRConfig）对设备的网络参数（NET_DVR_NETCFG_V30）进行配置。而虚线框“配置报警条件和处理方法”部分与“布防”中的一致。对以上需要配置的参数都设置完后，调用 NET_DVR_StartListen_V30 函数，开启 SDK 的监听端口，准备接收设备上传的报警信息。  

 该方式适用于多个设备向一台客户端上传报警，而且不需要设备登录即可完成，设备重启后不影响报警上传；缺点是设备只支持一个报警主机地址和端口号的配置。  

#### 3.9透明通道模块流程  

![](https://cdn-mineru.openxlab.org.cn/extract/a3bd49b8-00d0-42fe-8988-4fbd24aaac9c/20903298dc1cca22f6c9fdd0032e4a5a56fb301d90bd1fb862bde35ca31d3e53.jpg)  
图 3.9 透明通道模块流程  

SDK 提供将 485 和 232 串口作为透明通道，要将 232 串口作为透明通道使用，首先必须在 232 串口的配置信息中将工作模式选为透明通道，具体方法是调用接口 NET_DVR_GetDVRConfig 和NET_DVR_SetDVRConfig 获取和设置参数 NET_DVR_RS232CFG 中的 dwWorkMode 值为透明通道。如果是485 串口作为透明通道，这个步骤可以省略，调用 NET_DVR_SerialStart 建立透明通道和NET_DVR_SerialSend 发送数据。整个过程结束还需要断开透明通道（NET_DVR_SerialStop）等操作。  

## 4 函数调用实例  

### 4.1 IP 通道资源配置示例代码  

#include <stdio.h> #include <iostream> #include "Windows.h" #include "string.h" #include "HCNetSDK.h" using namespace std;  

void main() { int $\mathrm{i}{=}0$ ; BYTE byIPID,byIPIDHigh; int iDevInfoIndex, iGroupNO, iIPCh, iDevID; DWORD dwReturned $=0$ ; //-  

// 初始化  
NET_DVR_Init();  
//设置连接时间与重连时间  
NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

####  

#### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30("172.6.22.165", 8000, "admin", "12345", &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

printf("The max number of analog channels: %d\n",struDeviceInfo.byChanNum); //模拟通道个数 printf("The max number of IP channels: %d\n",struDeviceInfo.byIPChanNum);//IP 通道个数  

//获取 IP 通道参数信息   
NET_DVR_IPPARACFG_V40 IPAccessCfgV40;   
memset(&IPAccessCfgV40, 0, sizeof(NET_DVR_IPPARACFG)); iGroupNO=0; if (!NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_IPPARACFG_V40, iGroupNO, &IPAccessCfgV40,   
sizeof(NET_DVR_IPPARACFG_V40), &dwReturned)) { printf("NET_DVR_GET_IPPARACFG_V40 error, %d\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } else { for (i=0;i<IPAccessCfgV40.dwDChanNum;i++) { switch (IPAccessCfgV40.struStreamMode[i].byGetStreamType) { case 0: //直接从设备取流 if (IPAccessCfgV40.struStreamMode[i].uGetStream.struChanInfo.byEnable) { byIPID=IPAccessCfgV40.struStreamMode[i].uGetStream.struChanInfo.byIPID; byIPIDHigh=IPAccessCfgV40.struStreamMode[i].uGetStream.struChanInfo.byIPIDHigh; iDevInfoIndex=byIPIDHigh $^{*}256+$ byIPID-1-iGroupNO $^{*}64$ ; printf("IP channel no.%d is online, $|\mathsf{P}\colon\mathcal{\%}\backslash\mathsf{n}^{\prime\prime},\mathsf{i}\!+\!1,\backslash$   
IPAccessCfgV40.struIPDevInfo[iDevInfoIndex].struIP.sIpV4); } break; case 1: //从流媒体取流 if (IPAccessCfgV40.struStreamMode[i].uGetStream.struPUStream.struStreamMediaSvrCfg.byValid) { printf("IP channel %d connected with the IP device by stream server.\n", i+1); printf("IP of stream server: %s, IP of IP device: %s\n", \   
IPAccessCfgV40.struStreamMode[i].uGetStream.struPUStream.struStreamMediaSvrCfg.struDevIP.sIpV4, \   
PAccessCfgV40.struStreamMode[i].uGetStream.struPUStream.struDevChanInfo.struIP.sIpV4); } break; default: break; } //获取 IP 通道相关参数(以获取 IP 通道图像参数为例) DWORD iIPChanIndex $=$ IPAccessCfgV40.dwStartDChan; //起始通道，即 IP 通道 01 NET_DVR_PICCFG_V40 m_struPicCfg; //存放通道图像参数的结构体 memset(&m_struPicCfg, 0, sizeof(NET_DVR_PICCFG_V40)); if (!NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_PICCFG_V40, iIPChanIndex, &m_struPicCfg,   
sizeof(NET_DVR_PICCFG_V40), &dwReturned)) { printf("NET_DVR_GET_PICCFG_V40 error, %d\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } printf("The channel name of IP channel01: %s\n", m_struPicCfg.sChanName); //-- //支持自定义协议 NET_DVR_CUSTOM_PROTOCAL struCustomPro; //获取自定义协议 1 if (!NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_CUSTOM_PRO_CFG, 1, &struCustomPro,   
sizeof(NET_DVR_CUSTOM_PROTOCAL), &dwReturned)) { printf("NET_DVR_GET_CUSTOM_PRO_CFG error, %d\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } struCustomPro.dwEnabled $=\!1$ ;   //启用主码流 struCustomPro.dwEnableSubStream $=\!1$ ; //启用子码流 strcpy((char \*)struCustomPro.sProtocalName,"Protocal_RTSP");  //自定义协议名称:Protocal_RTSP,最大 16 字节 struCustomPro.byMainProType $^{=1}$ ; //主码流协议类型: 1- RTSP struCustomPro.byMainTransType $^{=2}$ ;  //主码流传输协议: 0- Auto, 1- udp, 2- rtp over rtsp struCustomPro.wMainPort ${\tt=}554$ ; //主码流取流端口 strcpy((char \*)struCustomPro.sMainPath,"rtsp://192.168.1.65/h264/ch1/main/av_stream");//主码流取流 URL struCustomPro.bySubProType $_{\cdot=1}$ ; //子码流协议类型: 1- RTSP struCustomPro.bySubTransType $_{:=2}$ ;  //子码流传输协议: 0- Auto, 1- udp, 2- rtp over rtsp struCustomPro.wSubPor $\mathtt{=}554$ ;     //子码流取流端口 strcpy((char \*)struCustomPro.sSubPath,"rtsp://192.168.1.65/h264/ch1/sub/av_stream");//子码流取流 URL  

#### //设置自定义协议 1  

if (!NET_DVR_SetDVRConfig(lUserID, NET_DVR_SET_CUSTOM_PRO_CFG, 1, &struCustomPro,  
sizeof(NET_DVR_CUSTOM_PROTOCAL)))  
{printf("NET_DVR_SET_CUSTOM_PRO_CFG error, %d\n", NET_DVR_GetLastError());NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;  
}  
printf("Set the custom protocol: %s\n", "Protocal_RTSP");  
NET_DVR_IPC_PROTO_LIST m_struProtoList;  
if (!NET_DVR_GetIPCProtoList(lUserID, &m_struProtoList)) //获取设备支持的前端  
{printf("NET_DVR_GetIPCProtoList error, %d\n", NET_DVR_GetLastError());NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;  
}  
//--  
//添加 IP 设备  
for( $\dot{\mathsf{I}}=\mathsf{0}\,$ ; i<MAX_IP_DEVICE_V40; $\dot{1}++$ )  
{if (IPAccessCfgV40.struIPDevInfo[i].byEnable ${\tt=}{\tt=}0$ ) //选择空闲的设备 ID{iDevID=i+1;break;}  
}  
//添加 IP 通道 5  
$\therefore\vert P C h=5$ ;  
IPAccessCfgV40.struIPDevInfo[iDevID-1].byEnable $^{=1}$ ; //启用  
for $(\mathfrak{i}=0_{\cdot}$ ; i<m_struProtoList.dwProtoNum; $\dot{1}+\dot{+}$ )  
{if(strcmp((char \*)struCustomPro.sProtocalName,(char \*)m_struProtoList.struProto[i].byDescribe) $\scriptstyle{|==0}$ ){IPAccessCfgV40.struIPDevInfo[iDevID-1].byProType=m_struProtoList.struProto[i].dwType; //选择自定义协议break;}  
}  
//IPAccessCfgV40.struIPDevInfo[iIPCh].byProType ${}=0$ ;  //厂家私有协议  
strcpy((char \*)IPAccessCfgV40.struIPDevInfo[iDevID-1].struIP.sIpV4,"172.6.22.225"); //前端 IP 设备的 IP 地址  
IPAccessCfgV40.struIPDevInfo[iDevID-1].wDVRPort=8000;  //前端 IP 设备服务端口  
strcpy((char \*)IPAccessCfgV40.struIPDevInfo[iDevID-1].sUserName,"admin");  //前端 IP 设备登录用户名  
strcpy((char \*)IPAccessCfgV40.struIPDevInfo[iDevID-1].sPassword,"12345");  //前端 IP 设备登录密码  
IPAccessCfgV40.struStreamMode[iIPCh-1].byGetStreamType ${=}0$ ; //直接从设备取流  
IPAccessCfgV40.struStreamMode[iIPCh-1].uGetStream.struChanInfo.byChanne $\left|=\right|1$ ; //前端 IP 设备的通道号  
IPAccessCfgV40.struStreamMode[iIPCh-1].uGetStream.struChanInfo.byIPID $^1=$ Dev $1\bar{1}\%256$ ; //通道对应前端 IP 设备 ID 的低 8 位  
IPAccessCfgV40.struStreamMode[iIPCh-1].uGetStream.struChanInfo.byIPIDHigh ${\mathsf{=i}}$ DevID/256;//通道对应前端 IP 设备 ID 的高 8 位  
//IP 通道配置，包括添加、删除、修改 IP 通道等  
if (!NET_DVR_SetDVRConfig(lUserID, NET_DVR_SET_IPPARACFG_V40, iGroupNO, &IPAccessCfgV40,  
sizeof(NET_DVR_IPPARACFG_V40)))  
{printf("NET_DVR_SET_IPPARACFG_V40 error, %d\n", NET_DVR_GetLastError());  

NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } else { printf("Set IP channel no.%d, IP: %s\n", iIPCh, IPAccessCfgV40.struIPDevInfo[iDevID-1].struIP.sIpV4); } //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return;  

### 4.2预览模块的示例代码  

#### 方式一 SDK 直接解码显示  

#include <stdio.h>   
#include <iostream>   
#include "Windows.h"   
#include "HCNetSDK.h"   
#include <time.h>   
using namespace std;   
typedef HWND (WINAPI \*PROCGETCONSOLEWINDOW)();   
PROCGETCONSOLEWINDOW GetConsoleWindow;   
void CALLBACK g_ExceptionCallBack(DWORD dwType, LONG lUserID, LONG lHandle, void \*pUser)   
{ char tempbuf[256] $=\{0\};$ switch(dwType) { case EXCEPTION_RECONNECT: //预览时重连 printf("----------reconnect--------%d\n", time(NULL)); break; default: break; }  

void main() {  

//初始化   
NET_DVR_Init();   
//设置连接时间与重连时间   
NET_DVR_SetConnectTime(2000, 1); NET_DVR_SetReconnect(10000, true);  

####  

// 获取控制台窗口句柄   
HMODULE hKernel32 $=$ GetModuleHandle("kernel32");   
GetConsoleWindow $=$ (PROCGETCONSOLEWINDOW)GetProcAddress(hKernel32,"GetConsoleWindow");  

####  

#### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}   
//--   
//设置异常消息回调函数   
NET_DVR_SetExceptionCallBack_V30(0, NULL,g_ExceptionCallBack, NULL);  

####  

#### //启动预览  

LONG lRealPlayHandle;  
HWND hWnd $=$ GetConsoleWindow(); //获取窗口句柄  
NET_DVR_PREVIEWINFO struPlayInfo $=\{0\}$ ;  
struPlayInfo.hPlayWnd $=$ hWnd; //需要 SDK 解码时句柄设为有效值，仅取流不解码时可设为空  
struPlayInfo.lChannel $=1$ ; //预览通道号  
struPlayInfo.dwStreamType $=0$ ; //0-主码流，1-子码流，2-码流 3，3-码流 4，以此类推  
struPlayInfo.dwLinkMode $=0_{\scriptscriptstyle-}$ ; //0- TCP 方式，1- UDP 方式，2- 多播方式，3- RTP 方式，4-RTP/RTSP，5-RSTP/HTTPstruPlayInfo.bBlocked $=1$ ; //0- 非阻塞取流，1- 阻塞取流lRealPlayHandle $=$ NET_DVR_RealPlay_V40(lUserID, &struPlayInfo, NULL, NULL);if (lRealPlayHandle $<0$ )  
{  

printf("NET_DVR_RealPlay_V40 error\n"); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } Sleep(10000); // //关闭预览 NET_DVR_StopRealPlay(lRealPlayHandle); //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return;  

#### 方式二 实时流数据回调，用户自行处理码流数据（此处以软解显示为例）  

#include <stdio.h>   
#include <iostream>   
#include "Windows.h"   
#include "HCNetSDK.h"   
#include "plaympeg4.h"   
#include <time.h>   
using namespace std;   
typedef HWND (WINAPI \*PROCGETCONSOLEWINDOW)();   
PROCGETCONSOLEWINDOW GetConsoleWindow;   
LONG lPort; //全局的播放库 port 号   
void CALLBACK g_RealDataCallBack_V30(LONG lRealHandle, DWORD dwDataType, BYTE \*pBuffer,DWORD dwBufSize,void\* dwUser)   
{ HWND hWnd=GetConsoleWindow(); switch (dwDataType) { case NET_DVR_SYSHEAD: //系统头 if (!PlayM4_GetPort(&lPort))  //获取播放库未使用的通道号 { break;  

}//m_iPort $=$ lPort;//第一次回调的是系统头，将获取的播放库 port 号赋值给全局 port，下次回调数据时即使用此 port 号播放if (dwBufSize > 0){if (!PlayM4_SetStreamOpenMode(lPort, STREAME_REALTIME))  //设置实时流播放模式{break;}if (!PlayM4_OpenStream(lPort, pBuffer, dwBufSize, $1024^{*}1024_{,}$ )) //打开流接口{break;}if (!PlayM4_Play(lPort, hWnd)) //播放开始{break;}}break;case NET_DVR_STREAMDATA:   //码流数据if (dwBufSize $>0$ && lPort $\dag=-1$ ){if (!PlayM4_InputData(lPort, pBuffer, dwBufSize)){break;}}break;default:  //其他数据if (dwBufSize $>0$ && lPort != -1){if (!PlayM4_InputData(lPort, pBuffer, dwBufSize)){break;}}break;}BACK g_ExceptionCallBack(DWORD dwType, LONG lUserID, LONG lHandle, void \*pUser){  

char tempbuf[256] = {0};switch(dwType){case EXCEPTION_RECONNECT: //预览时重连printf("-- --reconnect--------%d\n", time(NULL));break;default:break;}  
}  
void main() {//--// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

####  

// 获取控制台窗口句柄   
HMODULE hKernel32 $=$ GetModuleHandle("kernel32");   
GetConsoleWindow $=$ (PROCGETCONSOLEWINDOW)GetProcAddress(hKernel32,"GetConsoleWindow");  

### // 注册设备  

LONG lUserID;  
NET_DVR_DEVICEINFO_V30 struDeviceInfo;  
lUserID $=$ NET_DVR_Login_V30("172.0.0.100", 8000, "admin", "12345", &struDeviceInfo);  
if (lUserID $<0$ )  
{printf("Login error, %d\n", NET_DVR_GetLastError());NET_DVR_Cleanup();return;  
}  
//  
//设置异常消息回调函数  
NET_DVR_SetExceptionCallBack_V30(0, NULL,g_ExceptionCallBack, NULL);  
//-  
//启动预览并设置回调数据流  
LONG lRealPlayHandle;NET_DVR_PREVIEWINFO struPlayInfo $=\{0\}$ ;  
struPlayInfo.hPlayWnd $=$ hWnd; //需要 SDK 解码时句柄设为有效值，仅取流不解码时可设为空  
struPlayInfo.lChannel $=1.$ //预览通道号  
struPlayInfo.dwStreamType $=0$ ; //0-主码流，1-子码流，2-码流 3，3-码流 4，以此类推  
struPlayInfo.dwLinkMode $=0$ ; //0- TCP 方式，1- UDP 方式，2- 多播方式，3- RTP 方式，4-RTP/RTSP，5-RSTP/HTTPstruPlayInfo.bBlocked $=1$ ; //0- 非阻塞取流，1- 阻塞取流  
lRealPlayHandle $=$ NET_DVR_RealPlay_V40(lUserID, &struPlayInfo, g_RealDataCallBack_V30, NULL);  
if (lRealPlayHandle $<0$ )  
{  
printf("NET_DVR_RealPlay_V40 error\n");  
NET_DVR_Logout(lUserID);  
NET_DVR_Cleanup();  
return;  
}  
Sleep(10000);  
//--  
//关闭预览  
NET_DVR_StopRealPlay(lRealPlayHandle);  
//注销用户  
NET_DVR_Logout(lUserID);  
NET_DVR_Cleanup();  
return;  

#### 4.3回放和下载模块的示例代码  

#### 示例一：查找录像文件并下载  

#include <stdio.h>   
#include <iostream>   
#include "Windows.h"   
#include "HCNetSDK.h"   
using namespace std;   
int saveRecordFile(int userId,char \* srcfile,char \* destfile)   
{ int bRes $=1$ ; int hPlayback = 0;   
//按文件名下载录像   
if( (hPlayback $=$ NET_DVR_GetFileByName(userId, srcfile, destfile)) $<0$ )   
{ printf( "GetFileByName failed. error[%d]\n", NET_DVR_GetLastError()); $\mathsf{b R e s}\!=\!-1,$ ; return bRes;   
}   
//开始下载   
if(!NET_DVR_PlayBackControl_V40(hPlayback, NET_DVR_PLAYSTART, NULL,0,NULL,NULL))   
{ printf("play back control failed [%d]\n",NET_DVR_GetLastError()); $\mathsf{b R e s}{=}{-}1$ ; return bRes;   
}   
int $\mathsf{n P o s}=0,$ ;   
for $\mathsf{n P o s}=0,$ ;  nPos < 100&&nPos> ${\tt=}0$ ; nPos $=$ NET_DVR_GetDownloadPos(hPlayback))   
{ printf("Be downloading...%d %%\n", nPos);   //下载进度 Sleep(5000);  //millisecond   
}   
printf("have got %d\n", nPos);   
//停止下载   
if(!NET_DVR_StopGetFile(hPlayback))   
{ printf("failed to stop get file [%d]\n",NET_DVR_GetLastError()); ${\mathsf{b R e s}}=-1$ ; return bRes;   
}   
printf("%s\n",srcfile);   
if(nPos<0||nPos>100)   
{ printf("download err [%d]\n",NET_DVR_GetLastError()); $\mathsf{b R e s}{=}{-}1$ ; return bRes;   
}   
else   
{ return 0;   
}  

void main() {  

####  

// 初始化  
NET_DVR_Init();  
//设置连接时间与重连时间  
NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

#### //--  

#### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
} NET_DVR_FILECOND_V40 struFileCond $=\{0\}$ ;   
struFileCond.dwFileType $=0\mathsf{x}\mathsf{F}\mathsf{F}$ ;   
struFileCond.lChannel $=1$ ;  //通道号 struFileCond.dwIsLocked $=0\times\mathsf{F}\mathsf{F}$ ;   
struFileCond.dwUseCardNo $=0$ ;   
struFileCond.struStartTime.dwYear $=2011$ ;  //开始时间 struFileCond.struStartTime.dwMonth $=3$ ;   
struFileCond.struStartTime.dwDay $=1$ ;   
struFileCond.struStartTime.dwHour $=10$ ;   
struFileCond.struStartTime.dwMinute $=6$ ;   
struFileCond.struStartTime.dwSecond $=\mathtt{50}$ ;   
struFileCond.struStopTime.dwYear $=2011$ ;  //结束时间 struFileCond.struStopTime.dwMonth $=3$ ;   
struFileCond.struStopTime.dwDay $=1.$ ;   
struFileCond.struStopTime.dwHour $=11$ ;   
struFileCond.struStopTime.dwMinute $=7.$ ;   
struFileCond.struStopTime.dwSecond $=0$ ;  

#### //查找录像文件  

int lFindHandle $=$ NET_DVR_FindFile_V40(lUserID, &struFileCond); if(lFindHandle $<0$ )   
{  

printf("find file fail,last error %d\n",NET_DVR_GetLastError()); return; } NET_DVR_FINDDATA_V40 struFileData; while(true) { //逐个获取查找到的文件信息 int result $=$ NET_DVR_FindNextFile_V40(lFindHandle, &struFileData); if(result $==$ NET_DVR_ISFINDING) { continue; } else if(result $==$ NET_DVR_FILE_SUCCESS) //获取文件信息成功 { char strFileName $[256]=\{0\};$ sprintf(strFileName, ". $1\%5^{\prime\prime}$ , struFileData.sFileName); saveRecordFile(lUserID, struFileData.sFileName,  strFileName); break; } else if(result $==$ NET_DVR_FILE_NOFIND || result $==$ NET_DVR_NOMOREFILE) //未查找到文件或者查找结束 { break; } else { printf("find file fail for illegal get file state"); break; } } //停止查找 if(lFindHandle $>=0$ ) { NET_DVR_FindClose_V30(lFindHandle); //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return; }  

#### 示例二：按时间播放录像文件  

#include <stdio.h>   
#include <iostream>   
#include "Windows.h"   
#include "HCNetSDK.h"   
using namespace std;   
typedef HWND (WINAPI \*PROCGETCONSOLEWINDOW)(); PROCGETCONSOLEWINDOW GetConsoleWindow;   
void main() {   
//-- // 初始化   
NET_DVR_Init();   
//设置连接时间与重连时间   
NET_DVR_SetConnectTime(2000, 1); NET_DVR_SetReconnect(10000, true);  

#### //--  

// 获取控制台窗口句柄   
HMODULE hKernel32 $=$ GetModuleHandle("kernel32");   
GetConsoleWindow $=$ (PROCGETCONSOLEWINDOW)GetProcAddress(hKernel32,"GetConsoleWindow");  

####  

#### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

HWND hWnd $=$ GetConsoleWindow(); //获取窗口句柄  

NET_DVR_VOD_PARA struVodPara $=\{0\};$ struVodPara.dwSize=sizeof(struVodPara); struVodPara.struIDInfo.dwChannel=1; //通道号 struVodPara.hWnd=hWnd; //回放窗口 struVodPara.struBeginTime.dwYear $=2013$ ; //开始时间 struVodPara.struBeginTime.dwMonth $=6$ ; struVodPara.struBeginTime.dwDay $=14;$ struVodPara.struBeginTime.dwHour $=9$ ;  

struVodPara.struBeginTime.dwMinute $=0$ ; struVodPara.struBeginTime.dwSecond ${=}0$ ; struVodPara.struEndTime.dwYear $=2013$ ; //结束时间 struVodPara.struEndTime.dwMonth $=6.$ ; struVodPara.struEndTime.dwDay $=14;$ struVodPara.struEndTime.dwHour $=10$ ; struVodPara.struEndTime.dwMinute $=7$ ; struVodPara.struEndTime.dwSecond $=0_{\cdot}$ ;  

//-   
//按时间回放   
int hPlayback;   
hPlayback $=$ NET_DVR_PlayBackByTime_V40(lUserID, &struVodPara);   
if(hPlayback $<0$ )   
{ printf("NET_DVR_PlayBackByTime_V40 fail,last error %d\n",NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
//--   
//开始   
if(!NET_DVR_PlayBackControl_V40(hPlayback, NET_DVR_PLAYSTART,NULL, 0, NULL,NULL))   
{ printf("play back control failed [%d]\n",NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
Sleep(15000);  //millisecond   
if(!NET_DVR_StopPlayBack(hPlayback))   
{ printf("failed to stop file [%d]\n",NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
//注销用户   
NET_DVR_Logout(lUserID);  

//释放 SDK 资源NET_DVR_Cleanup();  

<html><body><table><tr><td>return;</td></tr><tr><td></td></tr></table></body></html>  

#### 示例三：按时间下载录像文件  

#include <stdio.h> #include <iostream> #include "Windows.h" #include "HCNetSDK.h" using namespace std;  

void main() {  

// 初始化  
NET_DVR_Init();  
//设置连接时间与重连时间  
NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

####  

#### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
}  

NET_DVR_PLAYCOND struDownloadCond $=\{0\}$ ; struDownloadCond.dwChannel=1; //通道号 struDownloadCond.struStartTime.dwYear $=2013$ ; //开始时间 struDownloadCond.struStartTime.dwMonth $=6$ ; struDownloadCond.struStartTime.dwDay $=14.$ ; struDownloadCond.struStartTime.dwHour $=9$ ; struDownloadCond.struStartTime.dwMinute $=50$ ; struDownloadCond.struStartTime.dwSecond ${}=0$ ; struDownloadCond.struStopTime.dwYear $=2013$ ; //结束时间 struDownloadCond.struStopTime.dwMonth $=6.$ ; struDownloadCond.struStopTime.dwDay $=14;$ struDownloadCond.struStopTime.dwHour $=10;$ struDownloadCond.struStopTime.dwMinute $=7;$  

struDownloadCond.struStopTime.dwSecond $=0$ ;  

####  

#### //按时间下载  

int hPlayback;   
hPlayback $=$ NET_DVR_GetFileByTime_V40(lUserID, "./test.mp4",&struDownloadCond);   
if(hPlayback $<0$ )   
{ printf("NET_DVR_GetFileByTime_V40 fail,last error %d\n",NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;  

####  

### //开始下载  

if(!NET_DVR_PlayBackControl_V40(hPlayback, NET_DVR_PLAYSTART, NULL, 0, NULL,NULL))   
{ printf("Play back control failed [%d]\n",NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
int $\mathsf{n P o s}=0$ ;   
for $\mathsf{n P o s}=0,$ ; nPos < 100&&nPos> ${>}{=}0$ ; nPos $=$ NET_DVR_GetDownloadPos(hPlayback))   
{ printf("Be downloading... %d %%\n",nPos); //下载进度 Sleep(5000);  //millisecond   
}   
if(!NET_DVR_StopGetFile(hPlayback))   
{ printf("failed to stop get file [%d]\n",NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
if(nPos<0||nPos>100)   
{ printf("download err [%d]\n",NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; printf("Be downloading... %d %%\n",nPos); //注销用户   
NET_DVR_Logout(lUserID);   
//释放 SDK 资源   
NET_DVR_Cleanup();   
return;  

#### 4.4参数配置模块的示例代码  

配置压缩参数（NET_DVR_COMPRESSIONCFG_V30）  

#include <stdio.h> #include <iostream> #include "Windows.h" #include "HCNetSDK.h" using namespace std; void main() {  

####  

// 初始化  
NET_DVR_Init();  
//设置连接时间与重连时间  
NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

####  

#### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
int iRet;   
//获取压缩参数  

DWORD dwReturnLen; NET_DVR_COMPRESSIONCFG_V30 struParams $=\{0\}.$ iRet $=$ NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_COMPRESSCFG_V30, struDeviceInfo.byStartChan, &struParams, \ sizeof(NET_DVR_COMPRESSIONCFG_V30), &dwReturnLen); if (!iRet) { printf("NET_DVR_GetDVRConfig NET_DVR_GET_COMPRESSCFG_V30 error.\n"); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; }  

//设置压缩参数   
struParams.struNormHighRecordPara.dwVideoBitrate $=22$ ;   
iRet $=$ NET_DVR_SetDVRConfig(lUserID, NET_DVR_SET_COMPRESSCFG_V30, struDeviceInfo.byStartChan, \ &struParams, sizeof(NET_DVR_COMPRESSIONCFG_V30));   
if (!iRet)   
{ printf("NET_DVR_GetDVRConfig NET_DVR_SET_COMPRESSCFG_V30 error.\n"); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}  

####  

//获取压缩参数   
iRet $=$ NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_COMPRESSCFG_V30, struDeviceInfo.byStartCha &struParams, sizeof(NET_DVR_COMPRESSIONCFG_V30), &dwReturnLen);   
if (!iRet)   
{ printf("NET_DVR_GetDVRConfig NET_DVR_GET_COMPRESSCFG_V30 error.\n"); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}   
printf("Video Bitrate is %d\n", struParams.struNormHighRecordPara.dwVideoBitrate);   
//注销用户   
NET_DVR_Logout(lUserID);   
//释放 SDK 资源   
NET_DVR_Cleanup();   
return;  

### 4.5远程设备维护模块的示例代码  

#### 日志查询  

#include <stdio.h> #include <iostream> #include "Windows.h" #include "HCNetSDK.h" using namespace std;  

void main() {  

####  

// 初始化  
NET_DVR_Init();  
//设置连接时间与重连时间  
NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

####  

#### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;   
} NET_DVR_TIME struStartTime, struStopTime;   
struStartTime.dwYear $=2011$ ;   
struStartTime.dwMonth $=3$ ;   
struStartTime.dwDay $=2$ ;   
struStartTime.dwHour $=9$ ;   
struStartTime.dwMinute $=0.$ ;   
struStartTime.dwSecond $=0.$ ;  

struStopTime.dwYear $=2011$ ; struStopTime.dwMonth $=3$ ; struStopTime.dwDay $=2;$ struStopTime.dwHour $=9$ ; struStopTime.dwMinute $=10;$ struStopTime.dwSecond ${\it\Delta\phi}=0;$  

####  

//查找日志 int lFindHandle $=$ NET_DVR_FindDVRLog_V30(lUserID, 0, 0, 0, &struStartTime, &struStopTime, FALSE); if(lFindHandle $<0$ ) { printf("find log fail,last error %d\n",NET_DVR_GetLastError()); return; } NET_DVR_LOG_V30 struLog; while(true) { int result $=$ NET_DVR_FindNextLog_V30(lFindHandle, &struLog); if(result $==$ NET_DVR_ISFINDING) { printf("finding\n"); continue; } else if(result $==$ NET_DVR_FILE_SUCCESS) { char strLog[256] $=\{0\}$ ; printf( $"10\mathrm{g}{\cdot}9\mathrm{60}4\mathrm{d}{\cdot}9\mathrm{60}2\mathrm{d}{\cdot}9\mathrm{60}2\mathrm{d}\ 9\mathrm{60}2\mathrm{d}{\cdot}9\mathrm{60}2\mathrm{d}{\cdot}9\mathrm{60}2\mathrm{d}{\cdot}\mathrm{r}\mathrm{_{0}}2\mathrm{d}{\cdot}\mathrm{n}"$ , struLog.strLogTime.dwYear, struLog.strLogTime.dwMonth, struLog.strLogTime.dwDay, \ struLog.strLogTime.dwHour,struLog.strLogTime.dwMinute, struLog.strLogTime.dwSecond); } else if(result $==$ NET_DVR_FILE_NOFIND || result $==$ NET_DVR_NOMOREFILE) { printf("find ending\n"); break; } else { printf("find log fail for illegal get file state\n"); break; } } //停止日志查询 if(lFindHandle $>0$ )  

{ NET_DVR_FindLogClose_V30(lFindHandle);  

}  

//注销用户  
NET_DVR_Logout(lUserID);//释放 SDK 资源  
NET_DVR_Cleanup();  
return;  

### 4.6语音对讲转发模块的示例代码  

#### 示例一：语音对讲  

#include <stdio.h>   
#include <iostream>   
#include "Windows.h"   
#include "HCNetSDK.h"   
using namespace std;   
void CALLBACK fVoiceDataCallBack(LONG lVoiceComHandle, char \*pRecvDataBuffer, DWORD dwBufSize, BYTE byAudioFlag, void\*   
pUser)   
{ printf("receive voice data, $\%d\backslash{\mathfrak n}^{"}$ , dwBufSize);   
}   
void main() { //-- // 初始化 NET_DVR_Init(); //设置连接时间与重连时间 NET_DVR_SetConnectTime(2000, 1); NET_DVR_SetReconnect(10000, true); //-- // 注册设备 LONG lUserID; NET_DVR_DEVICEINFO_V30 struDeviceInfo; lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo); if (lUserID $<0$ ) { printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup();  

return; } //语音对讲 LONG lVoiceHanle; lVoiceHanle $=$ NET_DVR_StartVoiceCom_V30(lUserID, 1,0, fVoiceDataCallBack, NULL); if (lVoiceHanle $<0$ ) { printf("NET_DVR_StartVoiceCom_V30 error, %d!\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } Sleep(5000);  //millisecond //关闭语音对讲 if (!NET_DVR_StopVoiceCom(lVoiceHanle)) { printf("NET_DVR_StopVoiceCom error, %d!\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } //注销用户 NET_DVR_Logout(lUserID); //释放 SDK 资源 NET_DVR_Cleanup(); return;  

### 4.7报警模块的示例代码  

#### 布防报警的示例代码：  

<html><body><table><tr><td></td></tr><tr><td>#include<stdio.h></td></tr><tr><td>#include<iostream></td></tr><tr><td>#include"Windows.h'</td></tr><tr><td>#include"HCNetSDK.h'</td></tr><tr><td>usingnamespacestd;</td></tr><tr><td></td></tr><tr><td>voidCALLBACKMessageCallback(LONGICommand,NET_DVR_ALARMER*pAlarmer,char*pAlarmlnfo,DWORDdwBufLen,void*</td></tr></table></body></html>  

pUser)  
{int i;NET_DVR_ALARMINFO struAlarmInfo;memcpy(&struAlarmInfo, pAlarmInfo, sizeof(NET_DVR_ALARMINFO));switch(lCommand){case COMM_ALARM:{switch (struAlarmInfo.dwAlarmType){case 3: //移动侦测报警for $(\mathsf{i}{=}0;\mathsf{i}{<}16;\mathsf{i}{+}+)$ //#define MAX_CHANNUM   16  //最大通道数{if (struAlarmInfo.dwChannel[i] $==1$ ){printf("发生移动侦测报警的通道号 $\%\mathsf{d}\backslash\mathsf{n}^{\prime\prime},\mathsf{i}\!+\!1)$ ;}}break;default:break;}}break;default:break;}  
}  
void main() {//--// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);//--// 注册设备LONG lUserID;NET_DVR_DEVICEINFO_V30 struDeviceInfo;lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo);  
if (lUserID < 0)  
{printf("Login error, %d\n", NET_DVR_GetLastError());NET_DVR_Cleanup();return;  
//设置报警回调函数  
NET_DVR_SetDVRMessageCallBack_V30(MessageCallback, NULL);  
//启用布防  
LONG lHandle;  
NET_DVR_SETUPALARM_PARAM  struAlarmParam $=\{0\};$   
struAlarmParam.dwSize $=$ sizeof(struAlarmParam);  
struAlarmParam.byAlarmInfoType ${}=0$ ;  
//设备是否支持新的报警信息通过登录返回的 NET_DVR_DEVICEINFO_V30 中参数 bySupport1 & 0x80 判断  
lHandle $=$ NET_DVR_SetupAlarmChan_V41(lUserID, & struAlarmParam);  
if (lHandle $<0$ )  
{printf("NET_DVR_SetupAlarmChan_V41 error, %d\n", NET_DVR_GetLastError());NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;  
}  
Sleep(5000);  
//撤销布防上传通道  
if (!NET_DVR_CloseAlarmChan_V30(lHandle))  
{printf("NET_DVR_CloseAlarmChan_V30 error, %d\n", NET_DVR_GetLastError());NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;  
//注销用户  
NET_DVR_Logout(lUserID);  
//释放 SDK 资源  
NET_DVR_Cleanup();  
return;  

}  

#### 监听报警的示例代码：  

#include <stdio.h>  
#include <iostream>  
#include "Windows.h"  
#include "HCNetSDK.h"  
using namespace std;  
void CALLBACK MessageCallback(LONG lCommand, NET_DVR_ALARMER \*pAlarmer, char \*pAlarmInfo, DWORD dwBufLen, void\*  
pUser)  
{int i;NET_DVR_ALARMINFO struAlarmInfo;memcpy(&struAlarmInfo, pAlarmInfo, sizeof(NET_DVR_ALARMINFO));switch(lCommand){case COMM_ALARM:{switch (struAlarmInfo.dwAlarmType){case 3: //移动侦测报警for $(\mathsf{i}{=}0;\mathsf{i}{<}16;\mathsf{i}{+}+)$ //#define MAX_CHANNUM   16  //最大通道数{if (struAlarmInfo.dwChannel[i] $==1$ ){printf("发生移动侦测报警的通道号 $\%\mathsf{d}\backslash\mathsf{n}^{\prime\prime},\mathsf{i}\!+\!1)$ ;}}break;default:break;}}break;default:break;}  
}  
void main() {//--// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);  
NET_DVR_SetReconnect(10000, true);  
//--  
// 注册设备  
LONG lUserID;  
NET_DVR_DEVICEINFO_V30 struDeviceInfo;  
lUserID $=$ NET_DVR_Login_V30("172.0.0.100", 8000, "admin", "12345", &struDeviceInfo);  
if (lUserID $<0$ )  
{printf("Login error, %d\n", NET_DVR_GetLastError());NET_DVR_Cleanup();return;  
}  

//设置报警回调函数 NET_DVR_SetDVRMessageCallBack_V30(MessageCallback, NULL);  

#### //启用监听  

LONG lHandle;   
lHandle $=$ NET_DVR_StartListen_V30(NULL,7200, MessageCallback, NULL);   
if (lHandle $<0$ )   
{ printf("NET_DVR_StartListen_V30 error, %d\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
}  

Sleep(5000);  

#### //停止监听  

if (!NET_DVR_StopListen_V30(lHandle))   
{ printf("NET_DVR_StopListen_V30 error, %d\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return;   
} //注销用户   
NET_DVR_Logout(lUserID); //释放 SDK 资源   
NET_DVR_Cleanup();   
return;  

### 4.8透明通道模块的示例代码  

#include <stdio.h> #include <iostream> #include "Windows.h" #include "HCNetSDK.h" using namespace std;  

//回调透传数据函数的外部实现  
void CALLBACK g_fSerialDataCallBack(LONG lSerialHandle, char \*pRecvDataBuffer, DWORD dwBufSize, DWORD dwUser)  
{//…… 处理接收到的透传数据，pRecvDataBuffer 中存放接收到的数据  
void main() {//-// 初始化NET_DVR_Init();//设置连接时间与重连时间NET_DVR_SetConnectTime(2000, 1);NET_DVR_SetReconnect(10000, true);  

####  

#### // 注册设备  

LONG lUserID;   
NET_DVR_DEVICEINFO_V30 struDeviceInfo;   
lUserID $=$ NET_DVR_Login_V30("192.0.0.64", 8000, "admin", "12345", &struDeviceInfo);   
if (lUserID $<0$ )   
{ printf("Login error, %d\n", NET_DVR_GetLastError()); NET_DVR_Cleanup(); return;  

//设置 232 为透明通道模式（使用 232 透明通道时调用，485 不需要）DWORD dwReturned $=0$ ;NET_DVR_RS232CFG_V30 struRS232Cfg;memset(&struRS232Cfg, 0, sizeof(NET_DVR_RS232CFG_V30));if (!NET_DVR_GetDVRConfig(lUserID, NET_DVR_GET_RS232CFG_V30, 0, &struRS232Cfg, sizeof(NET_DVR_RS232CFG_V30),&dwReturned)){printf("NET_DVR_GET_RS232CFG_V30 error, %d\n", NET_DVR_GetLastError());  

NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; } struRS232Cfg.struRs232.dwWorkMode $=2$ ; //设置 232 为透明通道模式；0：窄带传输，1：控制台，2：透明通道 if (!NET_DVR_SetDVRConfig(lUserID, NET_DVR_SET_RS232CFG_V30, 0, &(struRS232Cfg), sizeof(NET_DVR_RS232CFG))) { printf("NET_DVR_SET_RS232CFG_V30 error, %d\n", NET_DVR_GetLastError()); NET_DVR_Logout(lUserID); NET_DVR_Cleanup(); return; }  

//建立透明通道  
LONG lTranHandle;  
int iSelSerialIndex $=1;//1;232$ 串口；2:485 串口  
lTranHandle $=$ NET_DVR_SerialStart(lUserID, iSelSerialIndex, g_fSerialDataCallBack, lUserID);  
//设置回调函数获取透传数据  
if (lTranHandle $<0$ )  
{printf("NET_DVR_SerialStart error, %d\n", NET_DVR_GetLastError());NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;  
}  
//通过透明通道发送数据  
LONG lSerialChan $=0;//$ 使用 485 时该值有效，从 1 开始；232 时设置为 0  
char szSendBuf $[1016]=\{0\};$   
if (!NET_DVR_SerialSend(lTranHandle, lSerialChan, szSendBuf, sizeof(szSendBuf)))  
//szSendBuf 为发送数据的缓冲区  
{printf("NET_DVR_SerialSend error, %d\n", NET_DVR_GetLastError());NET_DVR_SerialStop(lTranHandle);NET_DVR_Logout(lUserID);NET_DVR_Cleanup();return;  
}  
//断开透明通道NET_DVR_SerialStop(lTranHandle);  
//注销用户  

<html><body><table><tr><td>NET DVR_Logout(IUserID);</td></tr><tr><td>//释放SDK <资源</td></tr><tr><td>NETD DVR_Cleanup();</td></tr><tr><td>return;</td></tr><tr><td>~</td></tr></table></body></html>  

## 5 函数说明  

### 5.1SDK 初始化  

#### 5.1.1 初始化 SDK NET_DVR_Init  

函  数： BOOL NET_DVR_Init()  
参  数： 无  
返回值： TRUE 表示成功，FALSE 表示失败。说  明： 调用设备网络 SDK 其他函数的前提。  

#### 5.1.2 释放 SDK 资源 NET_DVR_Cleanup  

函  数： BOOL NET_DVR_Cleanup()  
参  数： 无  
返回值： TRUE 表示成功，FALSE 表示失败。在结束之前最后调用。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

返回目录  

### 5.2SDK 本地功能  

#### SDK 本地参数配置  

#### 5.2.1 获取 SDK 本地参数 NET_DVR_GetSDKLocalCfg  

函  数： BOOL NET_DVR_GetSDKLocalCfg(NET_SDK_LOCAL_CFG_TYPE enumType, void \*lpOutBuff)  
参  数： [in] enumType 配置类型，不同的取值对应不同的 SDK 参数，详见表 5.1[out] lpOutBuff 输出参数，不同的配置类型，输出参数对应不同的结构，详见表5.1  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.1 本地参数类型  


<html><body><table><tr><td>enumType宏定义</td><td>类型值 含义</td><td></td><td>lpOutBuff对应结构体</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_TCP_PORT_BIND</td><td>0</td><td>本地TCP端口绑定配置</td><td>NET_DVR_LOCAL_TCP_PORT_BIND_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_UDP_PORT_BIND</td><td></td><td>本地UDP端口绑定配置</td><td>NET_DVR_LOCAL_UDP_PORT_BIND_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_MEM_POOL</td><td>2</td><td>内存池本地配置</td><td>NET_DVR_LOCAL_MEM_POOL_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_MODULE_RECV_TIMEOUT</td><td>3</td><td>按模块配置超时时间</td><td>NET_DVR_LOCAL_MODULE_RECV_TIMEOUT_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_ABILITY_PARSE</td><td>4</td><td>是否使用能力集解析库</td><td>NET_DVR_LOCAL_ABILITY_PARSE_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_TALK_MODE</td><td>5</td><td>对讲模式配置</td><td>NET_DVR_LOCAL_TALK_MODE_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_CHECK_DEV</td><td>10</td><td>心跳交互间隔时间配置</td><td>NET_DVR_LOCAL_CHECK_DEV</td></tr></table></body></html>  

#### 5.2.2 设置 SDK 本地参数 NET_DVR_SetSDKLocalCfg  

函  数： BOOL NET_DVR_SetSDKLocalCfg(NET_SDK_LOCAL_CFG_TYPE enumType, void\* const lpInBuff)  

参  数： [in] enumType 配置类型，不同的取值对应不同的 SDK 参数，详见表 5.2[in] lpInBuff 输入参数，不同的配置类型，输出参数对应不同的结构，详见  

5.2  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.2 本地参数类型  


<html><body><table><tr><td>enumType宏定义</td><td>类型值</td><td>含义</td><td>lplnBuff对应结构体</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_TCP_PORT_BIND</td><td>0</td><td>本地TCP端口绑定配置</td><td>NET_DVR_LOCAL_TCP_PORT_BIND_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_UDP_PORT_BIND</td><td>1</td><td>本地UDP端口绑定配置</td><td>NET_DVR_LOCAL_UDP_PORT_BIND_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_MEM_POOL</td><td>2</td><td>内存池本地配置</td><td>NET_DVR_LOCAL_MEM_POOL_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_MODULE_RECV_TIMEOUT</td><td>3</td><td>按模块配置超时时间</td><td>NET_DVR_LOCAL_MODULE_RECV_TIMEOUT_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_ABILITY_PARSE</td><td>4</td><td>是否使用能力集解析库</td><td>NET_DVR_LOCAL_ABILITY_PARSE_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_TALK_MODE</td><td>5</td><td>对讲模式配置</td><td>NET_DVR_LOCAL_TALK_MODE_CFG</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_CHECK_DEV</td><td>10</td><td>心跳交互间隔时间配置</td><td>NET_DVR_LOCAL_CHECK_DEV</td></tr><tr><td>NET_SDK_LOCAL_CFG_TYPE_CHAR_ENCODE</td><td>13</td><td>配置字符编码相关处理回调</td><td>NET_DVR_LOCAL_BYTE_ENCODE_CONVERT</td></tr><tr><td>NET_DVR_LOCAL_CFG_TYPE_LOG</td><td>15</td><td>日志参数配置</td><td>NET_DVR_LOCAL_LOG_CFG</td></tr></table></body></html>  

#### 连接和接收超时时间及重连设置  

#### 5.2.3 设置网络连接超时时间和连接尝试次数 NET_DVR_SetConnectTime  

函  数： BOOL NET_DVR_SetConnectTime(DWORD dwWaitTime,DWORD dwTryTime)  
参  数： [in]dwWaitTime 超时时间，单位毫秒，取值范围[300,75000]，实际最大超时时间因系统的 connect 超时时间而不同。[in]dwTryTimes 连接尝试次数（保留）  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： SDK 默认建立连接的超时时间为 3 秒。SDK4.0 及以后版本中当设置的超时时间超过或低于限制的值时接口不返回失败，将取最接近的上下限限制值作为实际的超时时间。  

返回目录  

#### 5.2.4 设置重连功能 NET_DVR_SetReconnect  

函  数： BOOL NET_DVR_SetReconnect (DWORD dwInterval,BOOL bEnableRecon)  
参  数： [in]dwInterval 重连间隔，单位:毫秒[in]bEnableRecon 是否重连，0-不重连，1-重连，参数默认为 1  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口可以同时控制预览、透明通道和布防的重连功能。不调用该接口时，SDK 默认启动预览、透明通道和布防的重连功能，重连时间间隔为 5 秒。  

返回目录  

#### 5.2.5 设置接收超时时间 NET_DVR_SetRecvTimeOut  

函  数： BOOL NET_DVR_SetRecvTimeOut(DWORD nRecvTimeOut)  
参  数： [in] nRecvTimeOut 接收超时时间，单位毫秒，默认为 5000，最小为 3000 毫秒  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口用于设置接收超时时间，例如预览接收实时流数据、回放下载接收录像数据、报警接收报警信息等接收超时时间。  

#### 多网卡绑定  

#### 5.2.6 获取所有 IP，用于支持多网卡接口 NET_DVR_GetLocalIP  

函  数： BOOL NET_DVR_GetLocalIP(char strIP[16][16], DWORD \*pValidNum, BOOL \*pEnableBind)参  数： [out] strIP 存放 IP 的缓冲区，不能为空  

[out] pValidNum 所有有效 IP 的数量[out] pEnableBind 是否绑定  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口获取客户端本地多网卡的所有 IP 地址，可以通过接口 NET_DVR_SetValidIP 选择要使用的IP 地址。  

返回目录  

#### 5.2.7 设置 IP 绑定 NET_DVR_SetValidIP  

函  数： BOOL NET_DVR_SetValidIP(DWORD dwIPIndex, BOOL bEnableBind)  

参  数： [in] dwIPIndex 选择使用的 IP 下标，由 NET_DVR_GetLocalIP 获取[in] bEnableBind 是否绑定  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### SDK 版本、状态和能力  

#### 5.2.8 获取 SDK 的版本号和 build 信息 NET_DVR_GetSDKBuildVersion  

函  数： DWORD NET_DVR_GetSDKBuildVersion()  

参  数：  
返回值： 获取 SDK 的版本号和 build 信息。  
说  明： SDK 的版本号和 build 信息。2 个高字节表示版本号 ： $25\sim\!32$ 位表示主版本号， $17^{\sim}24$ 位表示次版本号；2 个低字节表示 build 信息。如 0x03000101：表示版本号为 3.0，build 号是 0101。  

返回目录  

#### 5.2.9 获取当前 SDK 的状态信息 NET_DVR_GetSDKState  

函  数： BOOL NET_DVR_GetSDKState( LPNET_DVR_SDKSTATE pSDKState);  
参  数： [out]pSDKState SDK 状态信息，详见结构体：NET_DVR_SDKSTATE  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.2.10 获取当前 SDK 的功能信息 NET_DVR_GetSDKAbility  

函  数： BOOL NET_DVR_GetSDKAbility( LPNET_DVR_SDKABL pSDKAbl)  

参  数： [out] pSDKAbl SDK 功能信息，详见结构体：NET_DVR_SDKABL返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### SDK 启用写日志  

#### 5.2.11 启用写日志文件 NET_DVR_SetLogToFile  

函  数： BOOL NET_DVR_SetLogToFile(DWORD bLogEnable,char\* strLogDir,BOOL bAuto参  数： [in]bLogEnable 日志的等级（默认为 0）：  

0-表示关闭日志1-表示只输出 ERROR 错误日志2-输出 ERROR 错误信息和 DEBUG 调试信息3-输出 ERROR 错误信息、DEBUG 调试信息和 INFO 普通信息等所有信息[in]strLogDir 日志文件的路径，windows 默认值为"C:\\SdkLog\\"；linux 默认值"/home/sdklog/"[in]bAutoDel 是否删除超出的文件数，默认值为 TRUE  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

 日志文件路径必须是绝对路径，且以"\\"结尾，例如"C:\\SdkLog\\"，建议用户先手动创建文件。若未指定文件路径，则采用默认路径"C:\\SdkLog\\"。  
 可多次调用该接口创建新的日志文件，更改目录时到下一次写文件时才会使用新的目录写文件。  
 bAutoDel 为 TRUE 时表示覆盖模式，日志文件个数超过 SDK 限制个数时将会自动删除超出的文件。SDK 限制个数默认为 10 个，可以调用接口 NET_DVR_SetSDKLocalCfg(配置类型：NET_DVR_LOCAL_CFG_TYPE_LOG)进行修改配置。  

#### 异常消息回调  

#### 5.2.12 注册异常消息回调函数 NET_DVR_SetExceptionCallBack_V30  

函  数： Windows 系统下：  

BOOL NET_DVR_SetExceptionCallBack_V30 (UINT nMessage,HWND hWnd,fExceptionCallBack  
cbExceptionCallBack,void\* pUser)  
Linux 系统下：  
BOOL NET_DVR_SetExceptionCallBack_V30(UINT nMessage,void\* hWnd,fExceptionCallBack  
cbExceptionCallBack,void\* pUser)  
[in]nMessage 消息,Linux 下该参数保留  
[in]hWnd 接收异常消息的窗口句柄，Linux 下该参数保留  
[in]cbExceptionCallBack 接收异常消息的回调函数，回调当前异常的相关信息  
[in]pUser 用户数据  

typedef void(CALLBACK\* fExceptionCallBack)(DWORD dwType, LONG lUserID, LONG lHandle, void \*pUser)  

<html><body><table><tr><td>[out]dwType</td><td>异常或重连等消息的类型， 详见表 5.3</td></tr><tr><td>[out]luserlD</td><td>登录ID</td></tr><tr><td>[out]lHandle</td><td>出现异常的相应类型的句柄</td></tr><tr><td>[out]pUser</td><td>用户数据</td></tr></table></body></html>  

表 5.3 异常消息类型  


<html><body><table><tr><td>dwType 宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>EXCEPTION_EXCHANGE</td><td>0x8000</td><td>用户交互时异常（注册心跳超时，心跳间隔为2分钟)</td></tr><tr><td>EXCEPTION_AUDIOEXCHANGE</td><td>0x8001</td><td>语音对讲异常</td></tr><tr><td>EXCEPTION_ALARM</td><td>0x8002</td><td>报警异常</td></tr><tr><td>EXCEPTION_PREVIEW</td><td>0x8003</td><td>网络预览异常</td></tr><tr><td>EXCEPTION_SERIAL</td><td>0x8004</td><td>透明通道异常</td></tr><tr><td>EXCEPTION_RECONNECT</td><td>0x8005</td><td>预览时重连</td></tr><tr><td>EXCEPTION_ALARMRECONNECT</td><td>0x8006</td><td>报警时重连</td></tr><tr><td>EXCEPTION_SERIALRECONNECT</td><td>0x8007</td><td>透明通道重连</td></tr><tr><td>SERIAL_RECONNECTSUCCESS</td><td>0x8008</td><td>透明通道重连成功</td></tr><tr><td>EXCEPTION_PLAYBACK</td><td>0x8010</td><td>回放异常</td></tr><tr><td>EXCEPTION_DISKFMT</td><td>0x8011</td><td>硬盘格式化</td></tr><tr><td>EXCEPTION_EMAILTEST</td><td>0x8013</td><td>邮件测试异常</td></tr><tr><td>EXCEPTION_BACKUP</td><td>0x8014</td><td>备份异常</td></tr><tr><td>PREVIEW_RECONNECTSUCCESS</td><td>0x8015</td><td>预览时重连成功</td></tr><tr><td>ALARM_RECONNECTSUCCESS</td><td>0x8016</td><td>报警时重连成功</td></tr><tr><td>RESUME_EXCHANGE</td><td>0x8017</td><td>用户交互恢复</td></tr><tr><td>NETWORK_FLOWTEST_EXCEPTION</td><td>0x8018</td><td>网络流量检测异常</td></tr><tr><td>EXCEPTION_PICPREVIEWRECONNECT</td><td>0x8019</td><td>图片预览重连</td></tr><tr><td>PICPREVIEW_RECONNECTSUCCESS</td><td>0x8020</td><td>图片预览重连成功</td></tr><tr><td>EXCEPTION_PICPREVIEW</td><td>0x8021</td><td>图片预览异常</td></tr><tr><td>EXCEPTION_MAX_ALARM_INFO</td><td>0x8022</td><td>报警信息缓存已达上限</td></tr><tr><td>EXCEPTION_LOST_ALARM</td><td>0x8023</td><td>报警丢失</td></tr><tr><td>EXCEPTION_RELOGIN</td><td>0x8040</td><td>用户重登陆</td></tr><tr><td>RELOGIN_SUCCESS</td><td>0x8041</td><td>用户重登陆成功</td></tr></table></body></html>

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说明：Windows 下该函数的 hWnd 和 cbExceptionCallBack 不能同时为 NULL,Linux 下 cbExceptionCallBack不能设置为 NULL，否则将接收不到异常消息。如果此结构是以回调方式反馈异常消息，那么应用程序中的异常回调函数实现如下，该函数中的参数 dwType 表示异常消息类型（见上表）；lHandle 表示发生异常的相应类型的句柄。  

//注册接收异常消息的回调函数   
NET_DVR_SetExceptionCallBack_V30(WM_NULL, NULL, g_ExceptionCallBack, NULL);   
//接收异常消息的回调函数的外部实现   
void CALLBACK g_ExceptionCallBack(DWORD dwType, LONG lUserID, LONG lHandle, void \*pUser)   
{ char tempbuf[256]; ZeroMemory(tempbuf,256); switch(dwType) { case EXCEPTION_AUDIOEXCHANGE: //语音对讲时网络异常 sprintf(tempbuf,"语音对讲时网络异常!!!"); TRACE("%s",tempbuf); //TODO: 关闭语音对讲 break; case EXCEPTION_ALARM: //报警上传时网络异常 sprintf(tempbuf,"报警上传时网络异常!!!"); TRACE("%s",tempbuf); //TODO: 关闭报警上传 break; case EXCEPTION_PREVIEW: //网络预览时异常 sprintf(tempbuf,"网络预览时网络异常!!!"); TRACE("%s",tempbuf); //TODO: 关闭网络预览 break; case EXCEPTION_SERIAL: //透明通道传输时异常 sprintf(tempbuf,"透明通道传输时网络异常!!!"); TRACE("%s",tempbuf); //TODO: 关闭透明通道 break; case EXCEPTION_RECONNECT: //预览时重连 break; default: break; }  

#### 获取错误信息  

#### 5.2.13 返回最后操作的错误码 NET_DVR_GetLastError  

函  数： DWORD NET_DVR_GetLastError()  
参  数：  
返回值： 返回最后操作的错误码。详见错误码宏定义  
说  明： 返回值为错误码。错误码主要分为网络通讯库错误码、RTSP 通讯库错误码和软硬解库错误码。  

返回目录  

### 5.2.14 返回最后操作的错误码信息 NET_DVR_GetErrorMsg  

函  数： char\* NET_DVR_GetErrorMsg(LONG   \*pErrorNo)  
参  数： [out]pErrorNo 错误码数值的指针  
返回值： 返回值为错误码信息的指针。错误码主要分为网络通讯库错误码、RTSP 通讯库错误码和软硬解库错误码。详见错误码宏定义  

说  明：  

#### 5.3用户注册  

#### 5.3.1 激活设备 NET_DVR_ActivateDevice  

函  数： BOOL NET_DVR_ActivateDevice(char\* sDVRIP, WORD wDVRPort, LPNET_DVR_ACTIVATECFGlpActivateCfg)  
参  数： [in]sDVRIP 设备 IP 地址[in]wDVRPort 设备端口[in]lpActivateCfg 激活参数，包括激活使用的初始密码  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 出厂设备需要先激活，然后再使用激活使用的初始密码登录设备。  

#### 5.3.2 IPServer 或者 DDNS 域名解析，获取动态 IP 地址和端口号  

NET_DVR_GetDVRIPByResolveSvr_EX  

函  数： BOOL NET_DVR_GetDVRIPByResolveSvr_EX (char\* sServerIP, WORD wServerPort, BYTE\* sDVRName,WORD wDVRNameLen, BYTE\* sDVRSerialNumber, WORD wDVRSerialLen, char\* sGetIP, DWORD\*dwPort)  

参  数： [in]sServerIP 解析服务器的 IP 地址[in]wServerPort 解析服务器的端口号，IP Server 解析服务器端口号为 7071，HiDDNS 服务器的端口号为 80[in]sDVRName 设备名称[in]wDVRNameLen 设备名称的长度[in]sDVRSerialNumber 设备的序列号[in]wDVRSerialLen 设备序列号的长度[out]sGetIP 获取到的设备 IP 地址指针[out]dwPort 获取到的设备端口号指针  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中的设备名称和设备序列号不能同时为空。通过设备域名或者序列号解析出设备当前 IP地址和端口，然后调用 NET_DVR_Login_V40 登录设备。支持的解析服务器有 IPServer 和 hiDDNS。  

#### 5.3.3 用户注册设备 NET_DVR_Login_V40  

函  数： LONG NET_DVR_Login_V40(LPNET_DVR_USER_LOGIN_INFO pLoginInfo, LPNET_DVR_DEVICEINFO_V40 lpDeviceInfo)  

参  数： [in]pLoginInfo 登录参数，包括设备地址、登录用户、密码等[out]lpDeviceInfo 设备信息(同步登录即 pLoginInfo 中 bUseAsynLogin返回值： 异步登录的状态、用户 ID 和设备信息通过 NET_DVR_USER_LOGIN_INFO 结构体中设置的回调函数(fLoginResultCallBack)返回。对于同步登录，接口返回-1 表示登录失败，其他值表示返回的用户 ID 值。用户 ID 具有唯一性，后续对设备的操作都需要通过此 ID 实现。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

·pLoginlnfo中 bUseAsynLogin为0时登录为同步模式,接口返回成功即表示登录成功;pLoginlnfo中 bUseAsynLogin 为 1 时登录为异步模式，登录是否成功在输入参数设置的回调函数中返回。  
 设备同时最多允许 128 个用户注册。  
 SDK 支持 2048 个注册，返回 UserID 的取值范围为 $0^{\sim}2047$ 。  

#### 5.3.4 用户注销 NET_DVR_Logout  

函  数： BOOL NET_DVR_Logout(LONG lUserID)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 建议使用此接口实现注销功能。  

### 5.4获取设备能力集  

#### 5.4.1 获取设备能力集 NET_DVR_GetDeviceAbility  

函  数： BOOL  NET_DVR_GetDeviceAbility(LONG lUserID, DWORD dwAbilityType, char\* pInBuf, DWORD dwInLength, char\* pOutBuf, DWORD dwOutLength)  

数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwAbilityType 能力集类型，具体定义见表 5.4。[in] pInBuf 输入缓冲区指针（按照设备规定的能力参数的描述方式组合，可以是 XML 文本或结构体形式，详见表 5.5）[in]dwInLength 输入缓冲区的长度[out]pOutBuf 输出缓冲区指针（按照设备规定的能力集的描述方式，可以是XML 文本或结构体形式，详见表 5.5）[in]dwOutLength 接收数据的缓冲区的长度  

表 5.4 设备能力集类型  


<html><body><table><tr><td>dwAbilityType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>DEVICE_SOFTHARDWARE_ABILITY</td><td>0x001</td><td>设备软硬件能力</td></tr><tr><td>DEVICE_NETWORK_ABILITY</td><td>0x002</td><td>设备网络能力</td></tr><tr><td>DEVICE_ENCODE_ALL_ABILITY_V20</td><td>0x008</td><td>设备所有编码能力</td></tr><tr><td>DEVICE_RAID_ABILITY</td><td>0x007</td><td>设备 RAID 能力</td></tr><tr><td>DEVICE_ALARM_ABILITY</td><td>0x00a</td><td>设备报警能力</td></tr><tr><td>DEVICE_USER_ABILITY</td><td>0x00c</td><td>设备用户管理参数能力</td></tr><tr><td>DEVICE_NETAPP_ABILITY</td><td>pOOxO</td><td>设备网络应用参数能力</td></tr><tr><td>DEVICE_VIDEOPIC_ABILITY</td><td>0x00e</td><td>设备图像参数能力</td></tr><tr><td>DEVICE_JPEG_CAP_ABILITY</td><td>Ox00f</td><td>设备 JPEG 抓图能力</td></tr><tr><td>DEVICE_SERIAL_ABILITY</td><td>0x010</td><td>设备RS232和RS485串口能力</td></tr><tr><td>DEVICE_ABILITY_INFO</td><td>0x011</td><td>设备通用能力类型，具体能力根据发送的能力节点来区分</td></tr><tr><td>PIC_CAPTURE_ABILITY</td><td>0x402</td><td>抓图图片分辨率能力集</td></tr><tr><td>FISHEYE_ABILITY</td><td>0x700</td><td>鱼眼能力集</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取设备能力集时，需要输入参数和输出参数的格式定义如表 5.5 所示。  

表 5.5 设备能力集描述  


<html><body><table><tr><td>dwAbilityType宏定义</td><td>plnBuf</td><td>pOutBuf</td></tr><tr><td>DEVICESOFTHARDWAREABILITY</td><td>无</td><td>设备软硬件能力XML描述</td></tr><tr><td>DEVICENETWORKABILITY</td><td>无</td><td>设备网络能力XML描述</td></tr><tr><td>DEVICEENCODEALLABILITYV20</td><td>编码能力获取输入描述</td><td>设备所有编码能力XML描述</td></tr></table></body></html>  

<html><body><table><tr><td>DEVICE_RAID_ABILITY</td><td>无</td><td>设备RAID能力XML描述</td></tr><tr><td>DEVICE_ALARM_ABILITY</td><td>报警能力获取输入描述</td><td>设备报警能力XML描述</td></tr><tr><td>DEVICE_USER_ABILITY</td><td>用户管理参数能力获取输入描述</td><td>设备用户管理参数能力XML描述</td></tr><tr><td>DEVICE_NETAPP_ABILITY</td><td>网络应用参数能力获取输入描述</td><td>设备网络应用参数能力XML描述</td></tr><tr><td>DEVICE_VIDEOPIC_ABILITY</td><td>图像参数能力获取输入描述</td><td>设备图像参数能力XML描述</td></tr><tr><td>DEVICE_JPEG_CAP_ABILITY</td><td>JPEG 抓图能力获取输入描述</td><td>设备JPEG抓图能力XML描述</td></tr><tr><td>DEVICE_SERIAL_ABILITY</td><td>串口能力获取输入描述</td><td>设备串口能力XML描述</td></tr><tr><td rowspan="15">DEVICE_ABILITY_INFO</td><td>获取 PTZ 能力集</td><td>PTZ能力XML描述(PTZAbility)</td></tr><tr><td>获取报警事件处理能力集</td><td>报警事件处理能力XML描述(EventAbility)</td></tr><tr><td>获取 ROI能力集</td><td>ROI能力XML描述(ROIAbility)</td></tr><tr><td>获取录像相关能力集</td><td>录像相关能力XML描述(RecordAbility)</td></tr><tr><td>NVR前端待接入设备通道能力集</td><td>NVR前端待接入设备通道能力XML描述 (GetAccessDeviceChannelAbility)</td></tr><tr><td>获取设备本地预览切换能力集</td><td>设备本地预览切换能力XML描述(PreviewSwitchAbility)</td></tr><tr><td>获取设备 N+1能力集</td><td>设备N+1能力XML描述(NPlusOneAbility)</td></tr><tr><td>获取设备磁盘相关能力集</td><td>设备磁盘相关能力XML描述(HardDiskAbility)</td></tr><tr><td>获取IPC配置文件导入导出能力 集</td><td>IPC配置文件导入导出能力XML描述</td></tr><tr><td>获取设备通道输入能力集</td><td>(IPAccessConfigFileAbility) 设备通道输入能力XML描述(ChannellnputAbility)</td></tr><tr><td>获取报警触发录像能力集</td><td>设备报警触发录像能力XML描述</td></tr><tr><td>获取GB/T28181能力集</td><td>(AlarmTriggerRecordAbility) 设备 GB/T28181能力XML 描述(GBT28181AccessAbility)</td></tr><tr><td>通道号 （4个字节)</td><td>NET_DVR_COMPRESSIONCFG_ABILITY</td></tr><tr><td>PIC_CAPTURE_ABILITY FISHEYE_ABILITY</td><td>鱼眼能力集获取输入描述 鱼眼能力集XML描述(FishEyeAbility)</td></tr></table></body></html>

注：能力集结构和 XML 描述请参见《设备网络 SDK 使用手册.chm》  

#### 5.4.2 获取设备能力集(标准协议) NET_DVR_GetSTDAbility  

函  数： BOOL NET_DVR_GetSTDAbility(LONG lUserID, DWORD dwAbilityType, LPNET_DVR_STD_ABILITYlpAbilityParam)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwAbilityType 能力类型，具体定义见表 5.6[in&out]lpAbilityParam 设备能力集参数（包括输入和输出参数）  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.6 获取设备能力集  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td><td>IpCondBuffer IpOutBuffer</td><td></td></tr><tr><td>NET_DVR_GET_ACTIVATE_IPC_ABILITY</td><td>13003</td><td>获取NVR激活前端设备能 力集</td><td>NULL</td><td>VideoSourceActivationCapability</td></tr><tr><td>NET_DVR_GET_EVENT_TRIGGERS_CAPABILITIES</td><td>3501</td><td>获取事件触发能力集</td><td>NULL</td><td>EventTriggerCap</td></tr><tr><td>NET_DVR_GET_GBT28181_SERVICE_CAPABILITIES</td><td>6505</td><td>获取GB28181服务器能力 集</td><td>NULL</td><td>GB28181ServiceCap</td></tr><tr><td>NET_DVR_GET_TRAFFIC_CAP</td><td>6630</td><td>获取抓拍相关能力集</td><td>NULL</td><td>TrafficCap</td></tr><tr><td>NET_DVR_GET_ONLINEUPGRADE_ABILITY</td><td>9309</td><td>获取在线升级能力集</td><td>NULL</td><td>OnlineUpgradeCap</td></tr><tr><td>NET_DVR_GET_DDNS_COUNTRYABILITY</td><td>3800</td><td>获取设备支持的DDNS国 家能力列表</td><td>NULL</td><td>DDNSCountry</td></tr><tr><td></td><td>6709</td><td>获取配件板信息能力集</td><td>NULL</td><td>AccessoryCardlnfo</td></tr></table></body></html>

返回目录  

#### 5.4.3 获取设备能力集(透传)NET_DVR_STDXMLConfig  

函  数： BOOL NET_DVR_STDXMLConfig(LONG lUserID, NET_DVR_XML_CONFIG_INPUT \*lpInputParam,NET_DVR_XML_CONFIG_OUTPUT \*lpOutputParam)  

参  数： [in] lUserID 登录主控板，NET_DVR_Login_V40 返回值[in] lpInputParam 输入参数，详见表 5.7[out] lpOutputParam 输出参数，详见表 5.7  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  通过该接口可以直接透传 ISAPI 协议命令，实现参数配置、能力集等功能。调用该接口需要设备支持 ISAPI 协议（PUT、GET、POST、DELETE 等命令），不同功能对应不同的输入输出参数，具体内容可以参考 ISAPI 协议文档。  

表 5.7 获取设备能力集  


<html><body><table><tr><td>能力集类型</td><td>IplnputParam->lpRequestUrl</td><td>IplnputParam->lplnBuffer</td><td>pOutputParam->lpOutBuffer</td></tr><tr><td>设备系统总能力集</td><td>GET/ISAPI/System/capabilities</td><td>NULL</td><td>DeviceCap</td></tr></table></body></html>  

### 5.5 实时预览  

#### 5.5.1 实时预览 NET_DVR_RealPlay_V40  

函  数： LONG NET_DVR_RealPlay_V40(LONG lUserID, LPNET_DVR_PREVIEWINFO lpPreviewInfo,REALDATACALLBACK  fRealDataCallBack_V30, void \*pUser)  
参  数： [in] lUserID NET_DVR_Login_V40 的返回值[in] lpPreviewInfo 预览参数，包括通道号、码流类型、取流协议[in] fRealDataCallBack_V30 码流数据回调函数  
[in] pUser 用户数据  
typedef void(CALLBACK \*REALDATACALLBACK) (LONG lRealHandle, DWORD dwDataType, BYTE\*pBuffer, DWORD dwBufSize, void \*pUser);  

[out] lRealHandle 当前的预览句柄[out] dwDataType 数据类型，详见表 5.8[out] pBuffer 存放数据的缓冲区指针[out] dwBufSize 缓冲区大小[out] pUser 用户数据  

表 5.8 码流数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>1</td><td>系统头数据</td></tr><tr><td>NET_DVR_STREAMDATA</td><td>2</td><td>流数据 居（包括复合流或音视频分开的视频流数据）</td></tr><tr><td>NETDVRAUDIOSTREAMDATA</td><td>3</td><td>音频数据</td></tr></table></body></html>  

返回值：  

-1 表示失败，其他值作为 NET_DVR_StopRealPlay 等函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

 该接口预览参数结构中可以设置当前预览操作是否阻塞（通过 bBlocked 参数设置），若设为不阻塞，表示发起与设备的连接就认为连接成功，如果发生码流接收失败、播放失败等情况以预览异常的方式通知上层。在循环播放的时候可以减短停顿的时间，与 NET_DVR_RealPlay处理一致。若设为阻塞，表示直到播放操作完成才返回成功与否。  
 该接口中的回调函数可以置为空，这样该函数将不回调码流数据给用户，不过用户仍可以通过接口 NET_DVR_SetRealDataCallBack 或 NET_DVR_SetStandardDataCallBack 注册捕获码流数据的回调函数以捕获码流数据。  
 fRealDataCallBack_V30 回调函数中不能执行可能会占用时间较长的接口或操作，不建议调用该SDK（HCNetSDK.dll）本身的接口。  
 客户端异常离线时，设备端对取流连接的保持时间为 10 秒。  

#### 5.5.2 停止预览 NET_DVR_StopRealPlay  

函  数： LONG NET_DVR_StopRealPlay (LONG lRealHandle)  
参  数： [in]lRealHandle 预览句柄，NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.5.3 获取预览时用来解码和显示的播放库句柄 NET_DVR_GetRealPlayerIndex  

函  数： int NET_DVR_GetRealPlayerIndex(LONG  lRealHandle)  
参  数： [in]lRealHandle 预览句柄，NET_DVR_RealPlay_V40 的返回值  
返回值： -1 表示失败，其他值表示播放句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 用户可以通过返回的句柄自行实现播放库 SDK 提供的其他功能，详见本公司提供的软解码库函  

数说明《播放器 SDK 编程指南》。例如使用 PlayM4_GetBMP(LONG nPort,……)、PlayM4_GetJPEG(LONG nPort,……)这两个接口时，即可实现将当前预览图像以 BMP 或 JPEG 格式抓图保存到内存中： PlayM4_GetBMP(NET_DVR_GetRealPlayerIndex(),……)PlayM4_GetJPEG(NET_DVR_GetRealPlayerIndex(),……)  

### 5.6强制！帧  

#### 5.6.1 强制 I 帧 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.9[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.9[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.9 所示NET_DVR_I_FRAME 结构体里面指定强制的通道号、码流类型（主子码流或者其他）。  

表 5.9 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>lplnBuffer对应结构体</td></tr><tr><td>NETDVRMAKEIFRAME</td><td>3402</td><td>强制1帧</td><td>NETDVRIFRAME</td></tr></table></body></html>  

### 5.7预览显示视频参数配置  

#### 5.7.1 获取预览视频显示参数 NET_DVR_ClientGetVideoEffect  

函  数： BOOL NET_DVR_ClientGetVideoEffect(LONG lRealHandle,DWORD \*pBrightValue, DWORD\*pContrastValue,DWORD \*pSaturationValue,DWORD \*pHueValue)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[out]pBrightValue 亮度指针，取值范围[1,10][out]pContrastValue 对比度指针，取值范围[1,10][out]pSaturationValue 饱和度指针，取值范围[1,10][out]pHueValue 色度指针，取值范围[1,10]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 需要预览才能获取视频参数。  

#### 5.7.2 获取预览视频显示参数 NET_DVR_GetVideoEffect  

函  数： BOOL NET_DVR_GetVideoEffect(LONG lUserID, LONG lChannel,DWORD \*pBrightValue, DWORD\*pContrastValue,DWORD \*pSaturationValue,DWORD \*pHueValue)  

参  数： [in]lRealHandle NET_DVR_Login_V40 的返回值[in]lChannel 通道号[out] pBrightValue 亮度指针，取值范围[1,10][out] pContrastValue 对比度指针，取值范围[1,10][out] pSaturationValue 饱和度指针，取值范围[1,10][out] pHueValue 色度指针，取值范围[1,10]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 登录设备获取通道的视频参数。  

#### 5.7.3 设置预览视频显示参数 NET_DVR_ClientSetVideoEffect  

函  数： BOOL NET_DVR_ClientSetVideoEffect(LONG lRealHandle,DWORD pBrightValue, DWORDpContrastValue,DWORD pSaturationValue,DWORD pHueValue)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwBrightValue 亮度，取值范围[1,10][in]dwContrastValue 对比度，取值范围[1,10][in]dwSaturationValue 饱和度，取值范围[1,10][in]dwHueValue 色度，取值范围[1,10]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 需要预览才能设置视频参数。  

#### 5.7.4 设置预览视频显示参数 NET_DVR_SetVideoEffect  

函  数： BOOL NET_DVR_SetVideoEffect(LONG lUserID, LONG lChannel,DWORD \*pBrightValue, DWORD\*pContrastValue,DWORD \*pSaturationValue,DWORD \*pHueValue)  

参  数： [in]lRealHandle NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwBrightValue 亮度，取值范围[1,10][in]dwContrastValue 对比度，取值范围[1,10][in]dwSaturationValue 饱和度，取值范围[1,10][in]dwHueValue 色度，取值范围[1,10]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 登录设备设置通道的视频参数。  

### 5.8预览画面叠加字符和图像  

#### 5.8.1 预览画面叠加字符和图像，Linux 下无此接口 NET_DVR_RigisterDrawFun  

函  数： BOOL NET_DVR_RigisterDrawFun(LONG lRealHandle, fDrawFun cbDrawFun, DWORD dwUser)参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]cbDrawFun 画图回调函数[in]dwUser 用户数据typedef void(CALLBACK \*fDrawFun)(LONG lRealHandle, HDC hDc, DWORD dwUser)[out]lRealHandle 当前的预览句柄[out]hDc 画图 DC[out]dwUser 用户数据  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口主要完成注册回调函数，获得当前表面的 device context。用户可以在这个 DC 上画图或写字，就好像在窗口的客户区 DC 上绘图，但这个 DC 不是窗口客户区的 DC，而是播放器 DirectDraw里的 Off-Screen 表面的 DC。 如果调用接口 NET_DVR_RealPlay_V40 进行预览，参数 bBlocked 必须置 1（TRUE），否则该接口调用会失败，获取错误号为 12（调用次序错误）。  

返回目录  

### 5.9预览时播放声音控制  

#### 5.9.1 设置声音播放模式 NET_DVR_SetAudioMode  

函  数： BOOL NET_DVR_SetAudioMode(DWORD dwMode)  

参  数： [in]dwMode  

声音播放模式：1- 独占声卡，单路音频模式；2- 共享声卡，多路音频模式  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不调用该接口设置声音播放模式，默认为独占播放。  

#### 5.9.2 独占声卡模式下开启声音 NET_DVR_OpenSound  

函  数： BOOL NET_DVR_OpenSound(LONG lRealHandle)参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 如果当前是共享模式播放，调用该接口将返回失败。以独占方式只能打开一路通道播放，即依次打开多个通道时仅打开最后一路。  

#### 5.9.3 独占声卡模式下开启声音 NET_DVR_CloseSound  

函  数： BOOL NET_DVR_CloseSound()  
参  数： 无  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.9.4 共享声卡模式下开启声音 NET_DVR_OpenSoundShare  

函  数： BOOL NET_DVR_OpenSoundShare(LONG lRealHandle)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.9.5 共享声卡模式下关闭声音 NET_DVR_CloseSoundShare  

函  数： BOOL NET_DVR_CloseSoundShare (LONG lRealHandle)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

返回目录  

#### 5.9.6 调节播放音量 NET_DVR_Volume  

函  数： BOOL NET_DVR_Volume(LONG lRealHandle,WORD wVolume)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]wVolume 音量，取值范围[0,0xffff]  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.10实时预览数据捕获  

#### 5.10.1 注册回调函数，捕获实时码流数据 NET_DVR_SetRealDataCallBack  

函  数： BOOL NET_DVR_SetRealDataCallBack(LONG lRealHandle, fRealDataCallBackcbRealDataCallBack,DWORD dwUser)  

参  数： [in]lRealHandle 预览句柄，NET_DVR_RealPlay_V40 的返回值[in]cbRealDataCallBack 码流数据回调函数[in]dwUser 用户数据  

typedef void(CALLBACK \*fRealDataCallBack)(LONG lRealHandle, DWORD dwDataType, BYTE \*pBuffer, DWORD dwBufSize, DWORD dwUser)  

[out]lRealHandle 当前的预览句柄 [out]dwDataType 数据类型，详见表 5.10 [out]pBuffer 存放数据的缓冲区指针 [out]dwBufSize 缓冲区大小 [out]dwUser 用户数据  

表 5.10 码流数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>1</td><td>系统头数据</td></tr><tr><td>NET_DVRSTREAMDATA</td><td>2</td><td>流数据（包括复合流或音视频分开的视频流数据）</td></tr><tr><td>NETDVRAUDIOSTREAMDATA</td><td>3</td><td>音频数据</td></tr><tr><td>NET_DVR_PRIVATE_DATA</td><td>2或者112</td><td>私有数据，包括智能信息叠加等</td></tr></table></body></html>  

返回值：  

TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

 此函数包括开始和停止用户处理 SDK 捕获的数据，当回调函数 cbRealDataCallBack 设为非 NULL值时，表示回调和处理数据；当设为 NULL 时表示停止回调和处理数据。回调的第一个包是40 个字节的文件头，供后续解码使用，之后回调的是压缩的码流。回调数据最大为 256K 字节。  
 cbRealDataCallBack回调函数中不能执行可能会占用时间较长的接口或操作，不建议调用该SDK（HCNetSDK.dll）本身的接口。  

#### 5.10.2 注册回调函数，捕获实时码流数据（RTP 标准码流）  

#### NET_DVR_SetStandardDataCallBack  

函  数： BOOL NET_DVR_SetStandardDataCallBack(LONG lRealHandle, fStdDataCallBack cbStdDataCallBack,DWORD dwUser)  
参  数： [in]lRealHandle 预览句柄，NET_DVR_RealPlay_V40 的返回值[in]cbStdDataCallBack 标准码流回调函数[in]dwUser 用户数据typedef void(CALLBACK \*fStdDataCallBack)(LONG lRealHandle, DWORD dwDataType, BYTE \*pBuffer,DWORD dwBufSize, DWORD dwUser)  

[out]lRealHandle 当前的预览句柄[out]dwDataType 数据类型，详见表 5.11[out]pBuffer 存放数据的缓冲区指针[out]dwBufSize 缓冲区大小[out]dwUser 用户数据  

表 5.11 标准码流数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>1</td><td>系统头数据</td></tr><tr><td>NET_DVR_STD_VIDEODATA</td><td>4</td><td>标准视频流数据</td></tr><tr><td>NETDVRSTDAUDIODATA</td><td>5</td><td>标准音频流数据</td></tr><tr><td>NETDVRPRIVATEDATA</td><td>2 或者112</td><td>私有数据，包括智能信息叠加等</td></tr></table></body></html>  

返回值：  

TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

 此函数包括开始和停止用户处理 SDK 捕获的数据，当回调函数 cbStdDataCallBack 设为非 NULL值时，表示回调和处理数据；当设为 NULL 时表示停止回调和处理数据。回调的第一个包是40 个字节的文件头，供后续解码使用，之后回调的是标准码流（含 12 字节的 RTP 头）。  
 cbStdDataCallBack 回调函数中不能执行可能会占用时间较长的接口或操作，不建议调用该 SDK（HCNetSDK.dll）本身的接口。  
 此函数仅支持对于支持 RTSP 协议取流的设备的标准码流回调。  

#### 5.10.3 捕获数据并保存到指定的文件中 NET_DVR_SaveRealData  

函  数： BOOL  NET_DVR_SaveRealData(LONG  lRealHandle,char \*sFileName)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]sFileName 文件路径指针  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： V5.0.3.2 或以后版本，通过该接口保存录像，文件最大限制为 1024MB，大于 1024M 时，SDK 自动新建文件进行保存，文件开始将40 字节头自动写入，文件名命名规则为“在接口传入的文件名基础上增加数字标识(例如：\*_1.mp4、\*_2.mp4)”。  

#### 5.10.4 停止数据捕获 NET_DVR_StopSaveRealData  

函  数： BOOL  NET_DVR_StopSaveRealData(LONG  lRealHandle )  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.11 预览抓图  

#### 5.11.1 设置抓图模式 NET_DVR_SetCapturePictureMode  

函  数： BOOL NET_DVR_SetCapturePictureMode(DWORD dwCaptureMode)参  数： [in]dwCaptureMode 抓图模式：  

enum tagPDC_PARAM_KEY{BMP_MODE $=0,$ // BMP 模式JPEG_MODE $=1$ // JPEG 模式  
}CAPTURE_MODE  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。说  明： 调用该接口设置抓图模式后，NET_DVR_CapturePicture 可抓取相应的图片。  

#### 5.11.2 预览时，单帧数据捕获并保存成图片 NET_DVR_CapturePicture  

函  数： BOOL  NET_DVR_CapturePicture(LONG lRealHandle,char \*sPicFileName)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]sPicFileName 保存图象的文件路径。路径长度和操作系统有关，sdk 不做限制，windows 默认路径长度小于等于 256 字节（包括文件名在内）。  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

明：  在调用该接口之前可以调用 NET_DVR_SetCapturePictureMode 设置抓图模式，默认为 BMP 模式。如果抓图模式为 BMP 模式，抓取的是 BMP 图片，保存路径后缀应为.bmp；如果抓图模式为 JPEG 模式，抓取的是 JPEG 图片，保存路径后缀应为.jpg。 若设备的当前分辨率为 2CIF，播放库做了相关处理，抓取的图像为 4CIF。 调用 NET_DVR_CapturePicture 进行抓图，实际是播放库解码抓图，要求在调用NET_DVR_RealPlay_V40 等接口时传入非空的播放句柄（播放库解码显示），否则时接口会返回失败（调用次序错误）。  

### 5.12 设备抓图  

#### 5.12.1 单帧数据捕获并保存成 JPEG 图片 NET_DVR_CaptureJPEGPicture  

函  数： BOOL NET_DVR_CaptureJPEGPicture(LONG lUserID, LONG lChannel, LPNET_DVR_JPEGPARAlpJpegPara, char \*sPicFileName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]lpJpegPara JPEG 图像参数  

#### 保存 JPEG 图的文件路径  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口用于设备的单帧数据捕获：SDK 发送命令给设备，设备抓图之后返回客户端，然后 SDK将接收到的 JPEG 图片数据保存成文件。JPEG 抓图功能或者抓图分辨率需要设备支持，如果不支持接口返回失败，错误号 23 或者 29。  

#### 5.12.2 单帧数据捕获并保存成 JPEG 存放在指定的内存空间中  

NET_DVR_CaptureJPEGPicture_NEW  

函  数： BOOL NET_DVR_CaptureJPEGPicture_NEW(LONG lUserID, LONG lChannel, LPNET_DVR_JPEGPARA lpJpegPara, char \*sJpegPicBuffer, DWORD dwPicSize, LPDWORD lpSizeReturned)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]lpJpegPara JPEG 图像参数[in]sJpegPicBuffer 保存 JPEG 数据的缓冲区[in]dwPicSize 输入缓冲区大小[out]lpSizeReturned 返回图片数据的大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口用于设备的单帧数据捕获：SDK 发送命令给设备，设备抓图之后返回客户端，然后 SDK将接收到的 JPEG 图片数据保存在 sJpegPicBuffer 缓冲区里。JPEG 抓图功能或者抓图分辨率需要设备支持，如果不支持接口返回失败，错误号 23 或者 29。  

### 5.13云台控制  

#### 云台控制操作  

#### 5.13.1 云台控制操作（需先启动图像预览）NET_DVR_PTZControl  

函  数： BOOL NET_DVR_PTZControl(LONG lRealHandle,DWORD dwPTZCommand,DWORD dwStop)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwPTZCommand 云台控制命令，详见表 5.12[in]dwStop 云台停止动作或开始动作：0- 开始，1- 停止  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对云台实施的每一个动作都需要调用该接口两次，分别是开始和停止控制，由接口中的最后一个参数（dwStop）决定。在调用此接口之前需要先开启预览。与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台  

发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。  
如果云台设备所需的解码器设备不支持，则无法用该接口控制。  
云台默认以最大速度动作。  

表 5.12 云台控制命令  


<html><body><table><tr><td>wPTZCommand 宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>LIGHT_PWRON</td><td>2</td><td>接通灯光电源</td></tr><tr><td>WIPER_PWRON</td><td>3</td><td>接通雨刷开关</td></tr><tr><td>FAN_PWRON</td><td>4</td><td>接通风扇开关</td></tr><tr><td>HEATER_PWRON</td><td>５</td><td>接通加热器开关</td></tr><tr><td>AUX_PWRON1</td><td>6</td><td>接通辅助设备开关</td></tr><tr><td>AUX_PWRON2</td><td>7</td><td>接通辅助设备开关</td></tr><tr><td>ZOOM_IN</td><td>11</td><td>焦距变大(倍率变大)</td></tr><tr><td>ZOOM_OUT</td><td>12</td><td>焦距变小(倍率变小)</td></tr><tr><td>FOCUS_NEAR</td><td>13</td><td>焦点前调</td></tr><tr><td>FOCUS_FAR</td><td>14</td><td>焦点后调</td></tr><tr><td>IRIS_OPEN</td><td>15</td><td>光圈扩大</td></tr><tr><td>IRIS_CLOSE</td><td>16</td><td>光圈缩小</td></tr><tr><td>TILT_UP</td><td>21</td><td>云台上仰</td></tr><tr><td>TILT_DOWN</td><td>22</td><td>云台下俯</td></tr><tr><td>PAN_LEFT</td><td>23</td><td>云台左转</td></tr><tr><td>PAN_RIGHT</td><td>24</td><td>云台右转</td></tr><tr><td>UP_LEFT</td><td>25</td><td>云台上仰和左转</td></tr><tr><td>UP_RIGHT</td><td>26</td><td>云台上仰和右转</td></tr><tr><td>DOWN_LEFT</td><td>27</td><td>云台下俯和左转</td></tr><tr><td>DOWN_RIGHT</td><td>28</td><td>云台下俯和右转</td></tr><tr><td>PAN_AUTO</td><td>29</td><td>云台左右自动扫描</td></tr></table></body></html>  

#### 5.13.2 云台控制操作（不用启动图像预览）NET_DVR_PTZControl_Other  

函  数： BOOL NET_DVR_PTZControl_Other(LONG lUserID, LONG lChannel, DWORD dwPTZCommand,DWORD dwStop)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZCommand 云台控制命令，详见表 5.12[in]dwStop 云台停止动作或开始动作：0- 开始；1- 停止  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对云台实施的每一个动作都需要调用该接口两次，分别是开始和停止控制，由接口中的最后一个参数（dwStop）决定。在调用此接口之前需要先注册设备。与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。云台默认以最大速度动作。  

#### 5.13.3 带速度的云台控制操作（需先启动图像预览）  

NET_DVR_PTZControlWithSpeed  

函  数： BOOL NET_DVR_PTZControlWithSpeed(LONG lRealHandle, DWORD dwPTZCommand, DWORDdwStop, DWORD dwSpeed)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in] dwPTZCommand 云台控制命令，详见表 5.12[in]dwStop 云台停止动作或开始动作：0- 开始；1- 停止[in]dwSpeed 云台控制的速度，用户按不同解码器的速度控制值设置。取值范围[1.7]  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对云台实施的每一个动作都需要调用该接口两次，分别是开始和停止控制，由接口中的最后一个参数（dwStop）决定。在调用此接口之前需要先开启预览。与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

#### 5.13.4 带速度的云台控制操作（不用启动图像预览）  

NET_DVR_PTZControlWithSpeed_Other  

函  数： BOOL NET_DVR_PTZControlWithSpeed(LONG lUserID, LONG lChannel, DWORD dwPTZCommand,DWORD dwStop, DWORD dwSpeed)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZCommand 云台控制命令，详见表 5.12[in]dwStop 云台停止动作或开始动作：0- 开始；1- 停止[in]dwSpeed 云台控制的速度，用户按不同解码器的速度控制值设置。取值返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对云台实施的每一个动作都需要调用该接口两次，分别是开始和停止控制，由接口中的最后一个参数（dwStop）决定。在调用此接口之前不需要先开启预览，登录设备后即可实现控制。与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

#### 云台预置点操作  

#### 5.13.5 云台预置点操作，需先启动预览 NET_DVR_PTZPreset  

函  数： BOOL NET_DVR_PTZPreset(LONG lRealHandle,DWORD dwPTZPresetCmd,DWORD dwPresetIndex)参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwPTZPresetCmd 操作云台预置点命令，详见表 5.13[in]dwPresetIndex 预置点的序号（从 1 开始），最多支持 255 个预置点返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

表 5.13 预置点操作命令  


<html><body><table><tr><td>dwPTZPresetCmd宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>SETPRESET</td><td>8</td><td>设置预置点</td></tr><tr><td>CLE PRESET</td><td>9</td><td>清除预置点</td></tr><tr><td>GOTOPRESET</td><td>39</td><td>转到预置点</td></tr></table></body></html>  

#### 5.13.6 云台预置点操作 NET_DVR_PTZPreset_Other  

函  数： BOOL NET_DVR_PTZPreset_Other(LONG lUserID,LONG lChannel,DWORD dwPTZPresetCmd,DWORDdwPresetIndex))  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZPresetCmd 操作云台预置点命令，详见表 5.13[in]dwPresetIndex 预置点的序号（从 1 开始），最多支持 255 个预置点返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。通过 NET_DVR_PTZPreset 控制云台，设备接收到控制命令后云台进行相应的动作，如果操作失败则返回错误，运行正常才返回成功。而通过 NET_DVR_PTZPreset_Other 控制云台，设备接收到控制命令后直接返回成功  

#### 云台巡航操作  

#### 5.13.7 云台巡航操作，需先启动预览 NET_DVR_PTZPCruise  

函  数： BOOL NET_DVR_PTZCruise(LONG lRealHandle,DWORD dwPTZCruiseCmd,BYTE byCruiseRoute, BYTEbyCruisePoint, WORD wInput)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwPTZCruiseCmd 操作云台巡航命令，详见表 5.14[in]byCruiseRoute 巡航路径，最多支持 32 条路径（序号从 1 开始）巡航点，最多支持 32 个点（序号从 1 开始）[in]byCruisePoint 不同巡航命令时的值不同，预置点(最大 255)、时间(最大 255)、[in]wInput 速度(最大 40)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

表 5.14 巡航操作命令  


<html><body><table><tr><td>dwPTZCruiseCmd宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>FILL_PRE_SEQ</td><td>30</td><td>将预置点加入巡航序列</td></tr><tr><td>SET_SEQ_DWELL</td><td>31</td><td>设置巡航点停顿时间</td></tr><tr><td>SET_SEQ_SPEED</td><td>32</td><td>设置巡航速度</td></tr><tr><td>CLE_PRE_SEQ</td><td>33</td><td>将预置点从巡航序列中删除</td></tr><tr><td>RUN_SEQ</td><td>37</td><td>开始巡航</td></tr><tr><td>STOP_SEQ</td><td>38</td><td>停止巡航</td></tr></table></body></html>  

#### 5.13.8 云台巡航操作 NET_DVR_PTZPCruise_Other  

函  数： BOOL NET_DVR_PTZCruise_Other(LONG lUserID,LONG lChannel,DWORD dwPTZCruiseCmd,BYTEbyCruiseRoute, BYTE byCruisePoint, WORD wInput)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZCruiseCmd 操作云台巡航命令，详见表 5.14[in]byCruiseRoute 巡航路径，最多支持 32 条路径（序号从 1 开始）  

巡航点，最多支持 32 个点（序号从 1 开始）  

[in]byCruisePoint [in]wInput  

不同巡航命令时的值不同，预置点(最大 255)、时间(最大 255)、速度(最大 40)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

#### 云台花样扫描操作  

#### 5.13.9 云台花样扫描操作，需先启动预览 NET_DVR_PTZTrack  

函  数： BOOL NET_DVR_PTZTrack(LONG lRealHandle, DWORD dwPTZTrackCmd)参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]dwPTZTrackCmd 花样扫描操作命令，详见表 5.15  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

表 5.15 操作命令  


<html><body><table><tr><td>dwPTZTrackCmd宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>STAMEMCRUISE</td><td>34</td><td>开始记录花样扫描路径</td></tr><tr><td>STO_MEM_CRUISE</td><td>35</td><td>停止记录花样扫描路径迹</td></tr><tr><td>RUNCRUISE</td><td>36</td><td>开始执行花样扫描</td></tr></table></body></html>  

#### 5.13.10 云台花样扫描操作 NET_DVR_PTZTrack_Other  

函  数： BOOL NET_DVR_PTZTrack_Other(LONG lUserID, LONG lChannel, DWORD dwPTZTrackCmd)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]dwPTZTrackCmd 操作云台花样扫描命令，详见表 5.15  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 与设备之间的云台各项操作的命令都对应于设备与云台之间的控制码，设备会根据目前设置的解码器种类和解码器地址向云台发送控制码。如果目前设备上设置的解码器与云台设备的不匹配，需要重新配置设备的解码器。如果云台设备所需的解码器设备不支持，则无法用该接口控制。  

#### 透明云台控制  

#### 5.13.11 透明云台操作，需先启动预览 NET_DVR_TransPTZ  

函  数： BOOL NET_DVR_TransPTZ(LONG lRealHandle,char \*pPTZCodeBuf,DWORD dwBufSize)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]pPTZCodeBuf 存放云台控制码缓冲区的指针[in]dwBufSize 云台控制码的长度  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 使用该接口能直接通过设备将云台控制码信息直接传输给云台设备，而无需配置解码器。  

返回目录  

#### 5.13.12 透明云台操作 NET_DVR_TransPTZ_Other  

函  数： BOOL NET_DVR_TransPTZ(LONG lUserID,LONG lChannel,char \*pPTZCodeBuf,DWORD dwBufSize)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]pPTZCodeBuf 存放云台控制码缓冲区的指针[in]dwBufSize 云台控制码的长度  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 使用该接口能直接通过设备将云台控制码信息直接传输给云台设备，而无需配置解码器。  

#### 云台区域缩放控制  

#### 5.13.13 云台图象区域选择放大或缩小 NET_DVR_PTZSelZoomIn  

函  数： BOOL NET_DVR_PTZSelZoomIn(LONG lRealHandle, LPNET_DVR_POINT_FRAME pStruPointFrame);  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]pStruPointFrame 云台图像区域位置信息  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口实现 3D 定位功能，需要前端设备的支持。假设当前预览显示图像的框为 $352^{*}288$ ，原点即该显示框的左上角的顶点。参数 pStruPointFrame中各坐标值的计算方法（以 $\mathsf{X}$ 轴方向上为例）：xTop=鼠标当前所选区域的左上点的值 $^{*}255/352$ 。  

缩小条件：xBottom 减去 xTop 的值大于 2。放大条件：xBottom 减去 xTop 的值大于 0，且 yBottom减去 yTop 的值大于 0。  

#### 5.13.14 云台图像区域选择放大或缩小 NET_DVR_PTZSelZoomIn_Ex  

函  数： BOOL NET_DVR_PTZSelZoomIn_EX(LONG lUserID, LONG lChannel, LPNET_DVR_POINT_FRAMEpStruPointFrame)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号[in]pStruPointFrame 云台图像区域位置信息  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口实现 3D 定位功能，需要前端设备的支持。假设当前预览显示图像的框为 $352^{*}288$ ，原点即该显示框的左上角的顶点。参数 pStruPointFrame中各坐标值的计算方法（以 X 轴方向上为例）：xTop $\lvert=$ 鼠标当前所选区域的左上点的值 $^{*}255/352$ 。缩小条件：xBottom 减去 xTop 的值大于 2。放大条件：xBottom 减去 xTop 的值大于 0，且 yBottom减去 yTop 的值大于 0。  

#### 获取设备支持的云台协议  

#### 5.13.15 获取设备支持的云台协议 NET_DVR_GetPTZProtocol  

BOOL  NET_DVR_GetPTZProtocol(LONG lUserID, NET_DVR_PTZCFG \*pPtzcfg)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[out]pPtzcfg 设备的云台协议结构  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在早前的设备中规定了一系列云台协议，但在后期的设备（如 DS-90xx、DS-91xx、DS-81xx 等）仅保留一部分常用的协议，所以在配置前端云台协议时必须调用该接口获取当前设备支持的云  

台协议。  

### 5.14录像文件回放、下载、锁定及备份  

获取通道录像起止时间  

#### 5.14.1 获取通道录像起止时间 NET_DVR_InquiryRecordTimeSpan  

函  数： BOOL NET_DVR_InquiryRecordTimeSpan(LONG lUserID, DWORD dwChannel,LPNET_DVR_RECORD_TIME_SPAN_INQUIRY  lpInquiry, LPNET_DVR_RECORD_TIME_SPAN  

lpResult)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwChannel 通道号[in]lpInquiry 通道录像起止时间查询条件[in]lpResult 通道录像起止时间查询结果  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 即时刷新录像索引  

#### 5.14.2 即时刷新录像索引 NET_DVR_UpdateRecordIndex  

函  数： BOOL NET_DVR_UpdateRecordIndex(LONG lUserID, DWORD dwChannel)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwChannel 通道号  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 录像索引刷新后，即可回放刷新前的录像文件。  

#### 月历录像查询  

#### 5.14.3 获取月历录像分布 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.16[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.17[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.17），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.17 所示。  

表 5.16 月历录像查询命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_MONTHLY_RECORD_DISTRIBUTION</td><td>获取月历录像分布，dwCount为0</td><td>6164</td></tr></table></body></html>  

表 5.17 月历录像查询  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>IpOutBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_MONTHLY_RECORD_DISTRIBUTION</td><td>NET_DVR_MRD_SEARCH_PARAM</td><td>NET_DVR_MRD_SEARCH_RESULT</td></tr></table></body></html>  

#### 录像文件的查找  

#### 5.14.4 根据文件类型、时间查找设备录像文件 NET_DVR_FindFile_V40  

函  数： LONG NET_DVR_FindFile_V40(LONG lUserID,LPNET_DVR_FILECOND_V40  pFindCond)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]pFindCond 文件查找条件，包括设备通道号、文件类型、查找起止时间等  
返回值： -1 表示失败，其他值作为 NET_DVR_FindClose 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口指定了要查找的录像文件的信息，调用成功后，就可以调用 NET_DVR_FindNextFile_V40接口来获取文件信息。  

#### 5.14.5 逐个获取查找到的文件信息 NET_DVR_FindNextFile_V40  

函  数： LONG NET_DVR_FindNextFile_V40(LONG lFindHandle, LPNET_DVR_FINDDATA_V40 lpFindData)参  数： [in]lFindHandle 文件查找句柄，NET_DVR_FindFile_V40 的返回值[in]lpFindData 保存文件信息的指针，包括查找到的文件名、文件起止时间、文件类型等  

返回值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.18。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

表 5.18 查找状态信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>NET_DVR_FILE_SUCCESS</td><td>1000</td><td>获取文件信息成功</td></tr><tr><td>NET_DVR_FILE_NOFIND</td><td>1001</td><td>未查找到文件</td></tr><tr><td>NET_DVR_ISFINDING</td><td>1002</td><td>正在查找请等待</td></tr><tr><td>NET_DVR_NOMOREFILE</td><td>1003</td><td>没有更多的文件，查找结束</td></tr><tr><td>NET_DVR_FILE_EXCEPTION</td><td>1004</td><td>查找文件时异常</td></tr></table></body></html>  

说  明： 在调用该接口获取查找文件之前，必须先调用 NET_DVR_FindFile_V40 得到当前的查找句柄。此接口用于获取一条已查找到的文件信息，若要获取全部的已查找到的文件信息，需要循环调用此接口。通过此接口可以同时获取到与当前录像文件相关的卡号信息和文件是否被锁定的信息。每次可查询文件最大个数为 4000。  

#### 5.14.6 关闭文件查找，释放资源 NET_DVR_FindClose_V30  

函  数： BOOL  NET_DVR_FindClose_V30(LONG lFindHandle)  
参  数： [in]lFindHandle 文件查找句柄，NET_DVR_FindFile_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 按事件查找录像文件  

#### 5.14.7 根据事件查找录像文件 NET_DVR_FindFileByEvent_V40  

函  数： LONG NET_DVR_FindFileByEvent_V40(LONG lUserID, LPNET_DVR_SEARCH_EVENT_PARAM_V40lpSearchEventParam)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in] lpSearchEventParam 待查找的文件信息结构，包括事件类型、查找时间、通道等  
返回值： -1 表示 失败， 其他值作为 NET_DVR_FindNextEvent 等函数 的参数。获 取错误 码调用NET_DVR_GetLastError。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口指定了要查找的录像文件的信息，调用成功后，就可以调用 NET_DVR_FindNextFile 接口来获取文件信息。按事件查找出的录像文件针对开始时间和停止时间，因此只支持按时间回放NET_DVR_PlayBackByTime。该功能需要设备的支持，若设备不支持则接口返回失败，错误号为 23。  

#### 5.14.8 逐个获取查找到事件录像信息 NET_DVR_FindNextEvent_V40  

函  数： LONG NET_DVR_FindNextEvent_V40(LONG lFindHandle, LPNET_DVR_SEARCH_EVENT_RET_V40lpSearchEventRet)  
参  数： [in]lSearchHandle NET_DVR_Login_V40 的返回值[out]lpSearchEventRet 查找到的事件录像结果信息，包括事件类型、录像时间等  
返回值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.19。  

表 5.19 查找状态信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_FILE_SUCCESS</td><td>1000</td><td>获取文件信息成功</td></tr><tr><td>NET_DVR_FILE_NOFIND</td><td>1001</td><td>未查找到文件</td></tr><tr><td>NET_DVR_ISFINDING</td><td>1002</td><td>正在查找请等待</td></tr><tr><td>NET_DVR_NOMOREFILE</td><td>1003</td><td>没有更多的文件，查找结束</td></tr><tr><td>NET_DVR_FILE_EXCEPTION</td><td>1004</td><td>查找文件时异常</td></tr></table></body></html>  

接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。说  明： 在调用该接口获取查找文件之前，必须先调用 NET_DVR_FindFileByEvent 得到当前的查找句柄。按事件查找出的录像文件针对开始时间和停止时间，因此只支持按时间回放NET_DVR_PlayBackByTime()。  

#### 5.14.9 关闭文件查找，释放资源 NET_DVR_FindClose_V30  

函  数： BOOL  NET_DVR_FindClose_V30(LONG lFindHandle)  
参  数： [in]lFindHandle 文件查找句柄，NET_DVR_FindFileByEvent 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 区域移动侦测智能搜索  

#### 5.14.10 开始智能搜索 NET_DVR_SmartSearch_V40  

函  数： LONG NET_DVR_SmartSearch_V40(LONG lUserID, LPNET_DVR_SMART_SEARCH_PARAM_V40lpSmartSearchParam)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lpSmartSearchParam 智能搜索参数结构  

返回值： -1 表示失败，其他值作为 NET_DVR_SearchNextInfo、NET_DVR_StopSearch 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口指定了要搜索条件信息，调用成功后，就可以调用 NET_DVR_SearchNextInfo 接口来获取搜索结果。搜索出的录像文件针对开始时间和停止时间，因此只支持按时间回放NET_DVR_PlayBackByTime_V40。该功能需要设备的支持，若设备不支持则接口返回失败，错误号为 23。  

#### 5.14.11 逐个获取查找到的智能录像信息 NET_DVR_SearchNextInfo  

函  数： LONG NET_DVR_SearchNextInfo(LONG lSearchHandle, LPNET_DVR_SMART_SEARCH_RETlpSmartSearchRet)  
参  数： [in]lSearchHandle NET_DVR_SmartSearch_V40 的返回值[out]lpSmartSearchRet 保存搜索结果信息的指针  
返回值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.20。  

表 5.20 查找状态信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_FILE_SUCCESS</td><td>1000</td><td>获取文件信息成功</td></tr><tr><td>NET_DVR_FILE_NOFIND</td><td>1001</td><td>未查找到文件</td></tr><tr><td>NET_DVR_ISFINDING</td><td>1002</td><td>正在查找请等待</td></tr><tr><td>NET_DVR_NOMOREFILE</td><td>1003</td><td>没有更多的文件，查找结束</td></tr><tr><td>NET_DVR_FILE_EXCEPTION</td><td>1004</td><td>查找文件时异常</td></tr></table></body></html>  

接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。说  明： 在调用该接口前，必须先调用 NET_DVR_SmartSearch_V40 得到当前的搜索句柄。按搜索出的录像文件针对开始时间和停止时间，因此只支持按时间回放 NET_DVR_PlayBackByTime_V40。  

返回目录  

#### 5.14.12 停止智能搜索 NET_DVR_StopSearch  

函  数： BOOL NET_DVR_StopSearch(LONG lSearchHandle)  
参  数： [in]lSearchHandle NET_DVR_SmartSearch_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 回放（正放或倒放）录像文件  

#### 5.14.13 按文件名回放录像文件 NET_DVR_PlayBackByName  

函  数： LONG NET_DVR_PlayBackByName(LONG lUserID,char \*sPlayBackFileName, HWND hWnd)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sPlayBackFileName 回放的文件名，长度不能超过 100 字节[in]hWnd 回放的窗口句柄，若置为空，SDK 仍能收到码流数据，但不解码显示  

返回值： -1 表示失败，其他值作为 NET_DVR_StopPlayBack 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。说  明： 该接口指定了当前要播放的录像文件，调用成功后，还必须调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现回放。在调用该接口成功后，可以通过接口 NET_DVR_SetPlayDataCallBack 注册回调函数，捕获录像的码流数据并自行处理。  

#### Linux 下：  

对于 4.1 或者以上的版本的 SDK，HWND 表示播放窗口的句柄，定义为：  
typedef unsigned int HWND;  
如果使用 Qt 进行界面开发，示例如下：  
NET_DVR_CLIENTINFO tmpclientinfo;  
QWidget m_framePlayWnd;  
tmpclientinfo.hPlayWnd $=$ (HWND)m_framePlayWnd.GetPlayWndId();  
对于 4.1 以前的版本的 SDK，HWND 定义如下：  
typedef struct __PLAYRECT  
{int $\times;$ //显示框左上角横坐标int y; //显示框左上角纵坐标int uWidth;   //显示框宽度int uHeight;  //显示框高度  
}PLAYRECT;  
typedef PLAYRECT HWND;  
NET_DVR_CLIENTINFO 结构中的 $\mathsf{h P l a y W n d}=\{0\}$ 则 SDK 仍取流，不进行解码显示，  
以仍可以录像，但是不能设置 hPlayWnd ${}=0$ (即 NULL)，否则非法结构地址会导致调用  
hPlayWnd.x 等去判断的时候崩溃。  

#### 5.14.14 按时间回放录像文件 NET_DVR_PlayBackByTime_V40  

函  数： LONG NET_DVR_PlayBackByTime_V40(LONG lUserID, LPNET_DVR_VOD_PARA  pVodPara)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]pVodPara 回放参数  
返回值： -1 表示失败，其他值作为 NET_DVR_StopPlayBack 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口指定了当前要播放的录像文件，调用成功后，还必须调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现回放。当回放的是按事件搜索出的录像文件时，由于每个文件都会有预录和延迟的部分，因此在设置本接口的开始和结束时间参数时可以适当提前开始时间和延长结束时间。建议值：最多 10 分钟，最少 5 秒。在调用该接口成功后，可以通过接口 NET_DVR_SetPlayDataCallBack 注册回调函数，捕获录像的码流数据并自行处理。  

#### Linux 下：  

对于 4.1 或者以上的版本的 SDK，HWND 表示播放窗口的句柄，定义为：typedef unsigned int HWND;  
如果使用 Qt 进行界面开发，示例如下：  
NET_DVR_CLIENTINFO tmpclientinfo;  
QWidget m_framePlayWnd;  
tmpclientinfo.hPlayWnd $=$ (HWND)m_framePlayWnd.GetPlayWndId();  
对于 4.1 以前的版本的 SDK，HWND 定义如下：  
typedef struct __PLAYRECT  
{int x; //显示框左上角横坐标int y; //显示框左上角纵坐标int uWidth; //显示框宽度int uHeight;  //显示框高度  
}PLAYRECT;  
typedef PLAYRECT HWND;  
NET_DVR_CLIENTINFO 结构中的 $\mathsf{h P l a y W n d}=\{0\}$ 则 SDK 仍取流，不进行解码显示，所  
以仍可以录像，但是不能设置 hPlayWnd ${}=0$ (即 NULL)，否则非法结构地址会导致调用  
hPlayWnd.x 等去判断的时候崩溃。  

#### 5.14.15 按文件名倒放录像文件 NET_DVR_PlayBackReverseByName  

函  数： LONG NET_DVR_PlayBackReverseByName(LONG  lUserID, char  \*sPlayBackFileName, HWNDhWnd)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sPlayBackFileName 回放的文件名，长度不能超过 100 字节[in]hWnd 回放的窗口句柄，若置为空，SDK 仍能收到码流数据，但不解码显示  

返回值： -1 表示失败，其他值作为 NET_DVR_StopPlayBack 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口指定了当前要播放的录像文件，调用成功后，还必须调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现回放。在调用该接口成功后，可以通过接口 NET_DVR_SetPlayDataCallBack 注册回调函数，捕获录像的码流数据并自行处理。  

#### Linux 下：  

HWND 表示播放窗口的句柄，定义为：  
typedef unsigned int HWND;  
如果使用 Qt 进行界面开发，示例如下：  
NET_DVR_CLIENTINFO tmpclientinfo;  
QWidget m_framePlayWnd;  
tmpclientinfo.hPlayWnd $=$ (HWND)m_framePlayWnd.GetPlayWndId();  

#### 5.14.16 按时间倒放录像文件 NET_DVR_PlayBackReverseByTime_V40  

函  数： LONG NET_DVR_PlayBackReverseByTime_V40(LONG  lUserID,HWNDhWnd,LPNET_DVR_PLAYCOND pPlayCond)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]hWnd 回放文件的窗口句柄[in]pPlayCond 回放条件参数  
返回值： -1 表示失败，其他值作为 NET_DVR_StopPlayBack 等函数的参数。接口返回失败请调用  

NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

#### 说  明：  

该接口指定了当前要播放的录像文件，调用成功后，还必须调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现回放。  
当回放的是按事件搜索出的录像文件时，由于每个文件都会有预录和延迟的部分，因此在设置本接口的开始和结束时间参数时可以适当提前开始时间和延长结束时间。建议值：最多 10 分钟，最少 5 秒。  
在调用该接口成功后，可以通过接口 NET_DVR_SetPlayDataCallBack 注册回调函数，捕获录像的码流数据并自行处理。  

#### Linux 下：  

HWND 表示播放窗口的句柄，定义为：  
typedef unsigned int HWND;  
如果使用 Qt 进行界面开发，示例如下：  
NET_DVR_CLIENTINFO tmpclientinfo;  
QWidget m_framePlayWnd;  
tmpclientinfo.hPlayWnd $=$ (HWND)m_framePlayWnd.GetPlayWndId();  

#### 5.14.17 控制录像回放的状态 NET_DVR_PlayBackControl_V40  

函  数： BOOL NET_DVR_PlayBackControl_V40(LONG lPlayHandle,DWORD dwControlCode, LPVOIDlpInBuffer, DWORD dwInLen, LPVOID lpOutBuffer, DWORD \*lpOutLen)  

参  数： [in]lPlayHandle  

播放句柄，NET_DVR_PlayBackByName、NET_DVR_PlayBackReverseByName 或NET_DVR_PlayBackByTime_V40、NET_DVR_PlayBackReverseByTime_V40 的返回值[in]dwControlCode 控制录像回放状态命令，详见表 5.21[in] lpInBuffer 指向输入参数的指针，详见表 5.22[in]dwInLen 输入参数的长度。未使用，保留。[out]lpOutBuffer 指向输出参数的指针，详见表 5.22[out]lpOutLen 输出参数的长度  

表 5.21 回放控制命令  


<html><body><table><tr><td>dwControlCode宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_PLAYSTART</td><td>1</td><td>开始播放</td></tr><tr><td>NET_DVR_PLAYPAUSE</td><td>3</td><td>暂停播放</td></tr><tr><td>NET_DVR_PLAYRESTART</td><td>4</td><td>恢复播放</td></tr><tr><td>NET_DVR_PLAYFAST</td><td>5</td><td>快放</td></tr><tr><td>NET_DVR_PLAYSLOW</td><td>6</td><td>慢放</td></tr><tr><td>NET_DVR_PLAYNORMAL</td><td>7</td><td>正常速度播放（在暂停后调用将恢复暂停前的速度播放）</td></tr><tr><td>NET_DVR_PLAYFRAME</td><td>8</td><td>单帧放（恢复正常回放使用NET_DVR_PLAYNORMAL命令）</td></tr><tr><td>NET_DVR_PLAYSTARTAUDIO</td><td>6</td><td>打开声音</td></tr><tr><td>NET_DVR_PLAYSTOPAUDIO</td><td>10</td><td>关闭声音</td></tr><tr><td>NET_DVR_PLAYAUDIOVOLUME</td><td>11</td><td>调节音量，取值范围[0,Oxfff]</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_PLAYSETPOS</td><td>12</td><td>改变文件回放的进度</td></tr><tr><td>NET_DVR_PLAYGETPOS</td><td>13</td><td>获取按文件或者按时间回放的进度</td></tr><tr><td>NET_DVR_PLAYGETTIME</td><td>14</td><td>获取当前已经播放的时间(按文件回放的时候有效)</td></tr><tr><td>NET_DVR_PLAYGETFRAME</td><td>15</td><td>获取当前已经播放的帧数(按文件回放的时候有效)</td></tr><tr><td>NET_DVR_GETTOTALFRAMES</td><td>16</td><td>获取当前播放文件总的帧数(按文件回放的时候有效)</td></tr><tr><td>NET_DVR_GETTOTALTIME</td><td>17</td><td>获取当前播放文件总的时间(按文件回放的时候有效)</td></tr><tr><td>NET_DVR_THROWBFRAME</td><td>20</td><td>丢B帧</td></tr><tr><td>NET_DVR_SETSPEED</td><td>24</td><td>设置码流速度</td></tr><tr><td>NET_DVR_KEEPALIVE</td><td>25</td><td>保持与设备的心跳(如果回调阻塞，建议2秒发送一次)</td></tr><tr><td>NET_DVR_PLAYSETTIME</td><td>26</td><td>按绝对时间定位</td></tr><tr><td>NET_DVR_PLAYGETTOTALLEN</td><td>27</td><td>获取按时间回放对应时间段内的所有文件的总长度</td></tr><tr><td>NET_DVR_PLAY_FORWARD</td><td>29</td><td>倒放切换为正放</td></tr><tr><td>NET_DVR_PLAY_REVERSE</td><td>30</td><td>正放切换为倒放</td></tr><tr><td>NET_DVR_SET_TRANS_TYPE</td><td>32</td><td>设置转封装类型</td></tr><tr><td>NET_DVR_PLAY_CONVERT</td><td>33</td><td>回放转码</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中的第三个参数是否需要输入数值与控制命令有关，详见表 5.22 所示。  

 特别指出，当控制命令是开始播放（即 NET_DVR_PLAYSTART）时，第三个参数的值表示播放当前文件的偏移量，若该值为 0 表示从文件的起始位置播放，若该值不为 0 则表示断点续传的文件位置（Byte）。  
 该接口中的第五个参数表示当前控制命令操作所获取到的相应的参数，控制命令中的NET_DVR_PLAYGETPOS、NET_DVR_PLAYGETTIME、NET_DVR_PLAYGETFRAME、NET_DVR_GETTOTALFRAMES、NET_DVR_GETTOTALTIME、NET_DVR_PLAYSETTIME 和 NET_DVR_PLAYGETTOTALLEN 都能通过该参数得到对应的值，详见上表。  
 当命令值为 NET_DVR_PLAYGETPOS 时，获取文件回放或者下载进度时，0-100 表示正常的进度值，大于100 的值表示回放或者下载异常。倒放的进度为 ${100}^{\sim}0$ 。  
 按时间回放或下载时，只能获取进度值：0、100（结束）、200（异常）。  
 NET_DVR_SETSPEED 设置码流速率、NET_DVR_PLAYSETTIME 按绝对时间定位等命令需要设备支持，如果接口返回失败获取错误号为 23 则说明设备不支持该命令。  
 NET_DVR_SET_TRANS_TYPE 设置转封装类型和 NET_DVR_PLAY_CONVERT 回放转码需要在开始播放（即NET_DVR_PLAYSTART）之前调用。  

表 5.22 回放控制参数  


<html><body><table><tr><td>dwControlCode宏定义</td><td>状态命令说明</td><td>lplnBuf</td><td>IpOutBuf</td></tr><tr><td>NETDVRPLAYSTART</td><td>开始播放</td><td>一个4字节整型的偏移量</td><td>无</td></tr><tr><td>NETDVRPLAYSETPOS</td><td>改变回放的进度</td><td>一个4字节整型的进度值（0-100）</td><td>无</td></tr><tr><td>NETDVRPLAYGETPOS</td><td>获取回放的进度</td><td>无</td><td>一个4字节整型的进度值 (0-100)</td></tr><tr><td>NET_DVRPLAYGETTIME</td><td>获取当前已播放的时间（按无 文件回放有效）</td><td></td><td>一个4字节整型的时间值</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_PLAYGETFRAME</td><td>获取当前已播放的帧数（按无 文件回放有效)</td><td></td><td>个4字节整型的帧数值</td></tr><tr><td>NET_DVR_GETTOTALFRAMES</td><td>获取当前播放文件总的帧 数（按文件回放有效）</td><td>无</td><td>-个4字节整型的帧数值</td></tr><tr><td>NET_DVR_GETTOTALTIME</td><td>获取当前播放文件总的时 间 (按文件回放有效)</td><td>无</td><td>-个4字节整型的时间值</td></tr><tr><td>NET_DVR_THROWBFRAME</td><td>丢B帧</td><td>一个4字节整型的B帧个数</td><td>无</td></tr><tr><td>NET_DVR_SETSPEED</td><td>设置码流速度</td><td>-个4字节整型的速度值</td><td>无</td></tr><tr><td>NET_DVR_PLAYSETTIME</td><td>按绝对时间定位回放</td><td>NET_DVR_TIME</td><td>无</td></tr><tr><td>NET_DVR_PLAYGETTOTALLEN</td><td>获取按时间回放对应时间 段内的所有文件的总长度 倒放切换为正放</td><td>无</td><td>一个8字节整型的长度值 (单位字节)</td></tr><tr><td>NET_DVR_PLAY_FORWARD NET_DVR_PLAY_REVERSE</td><td>正放切换为倒放</td><td>应用层解码时需在IplnBuffer 输入 NET_DVR_TIME 表示当前的播放时 间,SDK 解码可将 IplnBuffer 置为 NULL 应用层解码时需在IplnBuffer输入</td><td>无</td></tr><tr><td></td><td></td><td>NET_DVR_TIME表示当前的播放时 间,SDK解码可将IplnBuffer 置为 NULL</td><td>无</td></tr><tr><td>NET_DVR_SET_TRANS_TYPE</td><td>设置转封装类型</td><td>一个4字节整型的转码类型：1-PS, 2-TS,3-RTP, 5-MP4</td><td>无</td></tr><tr><td>NET_DVR_PLAY_CONVERT</td><td>回放转码</td><td>NET_DVR_COMPRESSION_INFO_V30</td><td>无</td></tr></table></body></html>  

#### 5.14.18 停止回放录像文件 NET_DVR_StopPlayBack  

函  数： BOOL NET_DVR_StopPlayBack(LONG lPlayHandle)  
参  数： [in]lPlayHandle 回放句柄，NET_DVR_PlayBackByName、NET_DVR_PlayBackReverseByName 或NET_DVR_PlayBackByTime_V40、NET_DVR_PlayBackReverseByTime_V40 的返回值  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 回放录像文件时的数据捕获  

#### 5.14.19 捕获回放的录像数据，并保存成文件 NET_DVR_PlayBackSaveData  

函  数： BOOL  NET_DVR_PlayBackSaveData(LONG lPlayHandle,char \*sFileName)  

参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值[in]sFileName 保存数据的文件路径（包括文件名的绝对路径）  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： V5.0.3.2 或以后版本，通过该接口保存录像，文件最大限制为 1024MB，大于 1024M 时，SDK 自动新建文件进行保存，文件开始将40 字节头自动写入，文件名命名规则为“在接口传入的文件名基础上增加数字标识(例如：\*_1.mp4、\*_2.mp4)”。  

返回目录  

#### 5.14.20 停止保存录像数据 NET_DVR_StopPlayBackSave  

函  数： BOOL  NET_DVR_StopPlayBackSave(LONG lPlayHandle)  
参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.14.21 注册回调函数，捕获录像数据 NET_DVR_SetPlayDataCallBack_V40  

函  数： BOOL NET_DVR_SetPlayDataCallBack_V40(LONG lPlayHandle, fPlayDataCallBackcbPlayDataCallBack, void \*pUser)  

参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByTime_V40 或NET_DVR_PlayBackReverseByTime_V40 的返回值[in]cbPlayDataCallBack 录像数据回调函数[in]dwUser 用户数据  

typedef void(CALLBACK \*fPlayDataCallBack)(LONG lPlayHandle, DWORD dwDataType,BYTE \*pBuffer,DWORD dwBufSize, DWORD dwUser)  

[out]lPlayHandle 当前的录像播放句柄[out]dwDataType 数据类型，详见表 5.23[out]pBuffer 存放数据的缓冲区指针[out]dwBufSize 缓冲区大小[out]dwUser 用户数据  

表 5.23 回放回调数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>工</td><td>系统头数据</td></tr><tr><td>NETDVRSTREAMDATA</td><td>2</td><td>流数据（包括复合流或音视频分开的视频流数据）</td></tr><tr><td>NETDVRCHANGEFORWARD</td><td>10</td><td>码流改变为正放</td></tr><tr><td>NETDVRCHANGEREVERSE</td><td>11</td><td>码流改变为倒放</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

明：  此函数包括开始和停止用户处理 SDK 捕获的数据，当回调函数 cbPlayDataCallBack 设为非 NULL值时，表示回调和处理数据；当设为 NULL 时表示停止回调和处理数据。回调的第一个包是40 个字节的文件头，供后续解码使用，之后回调的是压缩的码流。 cbPlayDataCallBack 回调函数中不能执行可能会占用时间较长的接口或操作，不建议调用该SDK（HCNetSDK.dll）本身的接口。  

#### 录像标签的添加和删除  

#### 5.14.22 添加录像标签 NET_DVR_InsertRecordLabel  

函  数： BOOL NET_DVR_InsertRecordLabel(LONG lPlayHandle, NET_DVR_RECORD_LABEL\* lpRecordLabel,NET_DVR_LABEL_IDENTIFY \*lpLableIdentify)  
参  数： [in]lPlayHandle NET_DVR_PlayBackByName 或 NET_DVR_PlayBackByTime_V40 的返回值[in]lpRecordLabel 录像标签[out]lpLableIdentify 添加录像标签后的标识  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 录像标签功能可帮助用户在回放录像时记录下某一时间点的相关人员或现场等信息，以便后续随时根据标签信息，进行搜索和定位录像资料。  

返回目录  

#### 5.14.23 修改录像标签 NET_DVR_ModifyRecordLabel  

函  数： BOOL NET_DVR_ModifyRecordLabel(LONG lUserID, NET_DVR_MOD_LABEL_PARAM \*lpModLabelParam)  
参  数： [in]lUserID NET_DVR_PlayBackByName 或 NET_DVR_PlayBackByTime_V40 的返回值[in]lpModLabelParam 标签修改结构体  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.14.24 删除录像标签 NET_DVR_DelRecordLabel  

函  数： BOOL NET_DVR_DelRecordLabel(LONG lUserID, NET_DVR_DEL_LABEL_PARAM\* lpDelLabelParam)参  数： [in]lUserID NET_DVR_PlayBackByName 或 NET_DVR_PlayBackByTime_V40 的返回值  

[in]lpDelLabelParam 要删除的标签信息返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 录像标签的查找  

#### 5.14.25 搜索录像标签 NET_DVR_FindRecordLabel  

函  数： LONG NET_DVR_FindRecordLabel(LONG lUserID, LPNET_DVR_FIND_LABEL lpFindLabel)  
参  数： [in]lUserID NET_DVR_PlayBackByName 或 NET_DVR_PlayBackByTime_V40 的返回值[in]lpFindLabel 欲查找的标签信息结构  
返回值： -1 表示失败，其他值作为 NET_DVR_FindNextLabel 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 回放时，可根据查找到的标签（时间）信息通过 NET_DVR_PlayBackControl_V40 实现定位操作。每次最多搜索 4000 条标签条。  

#### 5.14.26 逐个获取搜索到的录像标签 NET_DVR_FindNextLabel  

函  数： LONG  NET_DVR_FindNextLabel(LONG lFindHandle, LPNET_DVR_FINDLABEL_DATA lpFindData)  

参  数： [in]lFindHandle NET_DVR_FindRecordLabel 的返回值[in]lpFindData 标签信息  

返回值： -1 表示失败，其他值表示当前的获取状态等信息。接口返回失败请调用 NET_DVR_GetLastError获取错误码，通过错误码判断出错原因。  

说  明： 在调用该接口获取查找录像标签之前，必须先调用 NET_DVR_FindRecordLabel 得到当前的查找句柄。此接口用于获取一条已查找到的标签信息，若要获取全部的已查找到的标签信息，需要循环调用此接口。  

返回目录  

#### 5.14.27 停止搜索录像标签 NET_DVR_StopFindLabel  

函  数： BOOL  NET_DVR_StopFindLabel(LONG lFindHandle)  
参  数： [in]lFindHandle NET_DVR_FindRecordLabel 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 回放的其他操作  

#### 5.14.28 获取录像回放时显示的 OSD 时间 NET_DVR_GetPlayBackOsdTime  

函  数： BOOL NET_DVR_GetPlayBackOsdTime(LONG lPlayHandle, LPNET_DVR_TIME lpOsdTime)  
参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值[out]lpOsdTime 获取的 OSD 时间的指针  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

返回目录  

#### 5.14.29 录像回放时抓图，并保存在文件中 NET_DVR_PlayBackCaptureFile  

函  数： BOOL NET_DVR_PlayBackCaptureFile(LONG lPlayHandle,char \*sFileName)  
参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值[in]sFileName 保存图片数据的文件路径  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 回放时抓下来的图片时间要比抓图时间延后，这是因为预览画面上的 OSD 时间是解码完成的显示时间，而解码缓冲区会有将近 1M 左右的数据还没有解出来，要抓取的图片数据是网络缓冲里面的。目前解码库没有直接从解码缓冲区中取出数据的接口。  

返回目录  

#### 5.14.30 刷新显示回放窗口 NET_DVR_RefreshPlay  

函  数： BOOL NET_DVR_RefreshPlay(LONG lPlayHandle)  
参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 当用户暂停或者单帧回放时，如果刷新了窗口，则窗口中的图像因为刷新而消失，此时调用这个接口可以重新显示最后一帧画面。此接口只在暂停和单帧播放时有效。  

返回目录  

#### 5.14.31 获取回放时用来解码显示的播放库句柄  

NET_DVR_GetPlayBackPlayerIndex函  数： int NET_DVR_GetPlayBackPlayerIndex(LONG lPlayHandle)参  数： [in]lPlayHandle 播放句柄，NET_DVR_PlayBackByName 或NET_DVR_PlayBackByTime_V40 的返回值返回值： -1 表示失败，其他值表示播放句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 用户可以通过返回的句柄自行实现播放库 SDK 提供的其他功能，详见本公司提供的软解码库函数说明《播放器 SDK 编程指南》。例如使用 PlayM4_GetBMP(LONG nPort,……)、PlayM4_GetJPEG(LONG nPort,……)这两个接口时，即可实现将当前预览图像以 BMP 或 JPEG 格式抓图保存到内存中：PlayM4_GetBMP(NET_DVR_GetRealPlayerIndex(),……)PlayM4_GetJPEG(NET_DVR_GetRealPlayerIndex(),……) 。  

#### 下载录像文件  

#### 5.14.32 按文件名下载录像文件 NET_DVR_GetFileByName  

函  数： LONG NET_DVR_GetFileByName(LONG lUserID,char \*sDVRFileName,char \*sSavedFileName)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sDVRFileName 要下载的录像文件名，文件名长度需小于 100 字节[in]sSavedFileName 下载后保存到 PC 机的文件路径，需为绝对路径  

返回值： -1 表示失败，其他值作为 NET_DVR_StopGetFile 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 在使用该接口下载录像文件前，可以先调用录像文件查找的接口获取文件名。该接口指定了当前要下载的录像文件，调用成功后，还需要调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现下载。  

#### 5.14.33 按时间下载录像文件 NET_DVR_GetFileByTime_V40  

函  数： LONG NET_DVR_GetFileByTime_V40(LONG lUserID, char \*sSavedFileName, LPNET_DVR_PLAYCONDpDownloadCond)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sSavedFileName 下载后保存到 PC 机的文件路径，需为绝对路径（包括文件名），比如：”C:\\test.mp4”[in]pDownloadCond 下载条件，包括通道号、开始时间、结束时间等  

返回值： -1 表示失败，其他值作为 NET_DVR_StopGetFile 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： $\bullet$ 该接口指定了当前要下载的录像文件，调用成功后，还需要调用 NET_DVR_PlayBackControl_V40接口的开始播放控制命令（NET_DVR_PLAYSTART）才能实现下载。 V5.0.3.2 或以后版本，通过该接口保存录像，文件最大限制为 1024MB，大于 1024M 时，SDK自动新建文件进行保存，文件开始将 40 字节头自动写入，文件名命名规则为“在接口传入的文件名基础上增加数字标识(例如：\*_1.mp4、\*_2.mp4)”。  

#### 5.14.34 控制录像下载的状态 NET_DVR_PlayBackControl_V40  

函  数： BOOL NET_DVR_PlayBackControl_V40(LONG lPlayHandle,DWORD dwControlCode, LPVOIDlpInBuffer, DWORD dwInLen, LPVOID lpOutBuffer, DWORD \*lpOutLen)  

参  数： [in]lPlayHandle 播放句柄，NET_DVR_GetFileByName 或NET_DVR_GetFileByTime_V40 的返回值[in]dwControlCode 控制录像回放状态命令，详见表 5.24[in] lpInBuffer 指向输入参数的指针，详见表 5.25[in]dwInLen 输入参数的长度。未使用，保留。[out]lpOutBuffer 指向输出参数的指针，详见表 5.25[out]lpOutLen 输出参数的长度  

表 5.24 下载控制命令  


<html><body><table><tr><td>dwControlCode 宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_PLAYSTART</td><td>1</td><td>开始下载</td></tr><tr><td>NET_DVR_PLAYPAUSE</td><td>3</td><td>暂停下载</td></tr><tr><td>NET_DVR_PLAYRESTART</td><td>4</td><td>恢复下载</td></tr><tr><td>NET_DVRPLAYSETPOS</td><td>12</td><td>改变文件下载的进度（按文件下载时有效)</td></tr><tr><td>NET_DVR_PLAYGETPOS</td><td>13</td><td>获取文件下载的进度 (按文件下载时有效)</td></tr><tr><td>NET_DVR_GETTOTALFRAMES</td><td>16</td><td>获取当前下载文件总的帧数(按文件下载时有效)</td></tr><tr><td>NET_DVR_GETTOTALTIME</td><td>17</td><td>获取当前下载文件总的时间(按文件下载时有效)</td></tr><tr><td>NET_DVR_SETSPEED</td><td>24</td><td>设置下载速度，速度单位：kbps，最小为256kbps，最 大为设备带宽</td></tr><tr><td>NET_DVR_SET_TRANS_TYPE</td><td>32</td><td>设置转封装类型</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中的第三个参数是否需要输入数值与控制命令有关，如表 5.25 所示。  

 当控制命令是开始下载（即 NET_DVR_PLAYSTART）时，第三个参数的值表示下载当前文件的偏移量，若该值为0 表示从文件的起始位置下载，若该值不为0 则表示断点续传的文件位置（Byte）。  
 当命令值为 NET_DVR_PLAYGETPOS 时，获取文件回放或者下载进度时，0-100 表示正常的进度值，大于 100 的值表示回放或者下载异常。  
 按时间下载时，只能获取进度值：0、100（结束）、200（异常）。  
 NET_DVR_SET_TRANS_TYPE 设置转封装类型需要在开始播放（即 NET_DVR_PLAYSTART）之前调用。  

表 5.25 下载控制参数  


<html><body><table><tr><td>状态命令宏定义</td><td>状态命令说明</td><td>IplnBuf</td><td>lpOutBuf</td></tr><tr><td>NETDVRPLAYSTART</td><td>开始下载</td><td>一个4字节整型的偏移量</td><td>无</td></tr><tr><td>NETDVRPLAYSETPOS</td><td>改变下载的进度</td><td>一个4字节整型的进度值（0-100）</td><td>无</td></tr><tr><td>NETDVRPLAYGETPOS</td><td>获取下载的进度</td><td>无</td><td>一个4字节整型的 进度值（0-100）</td></tr><tr><td>NETDVRGETTOTALFRAMES</td><td>获取当前下载文件总的</td><td>无</td><td>一个4字节整型的</td></tr></table></body></html>  

<html><body><table><tr><td></td><td>帧数（按文件回放有效）</td><td></td><td>帧数值</td></tr><tr><td>NETDVRGETTOTALTIME</td><td>获取当前下载文件总的 时间（按文件回放有效）</td><td>无</td><td>一个4字节整型的 时间值</td></tr><tr><td>NETDVRSETSPEED</td><td>设置下载速度</td><td>一个4字节整型的速度值</td><td>无</td></tr><tr><td>NETDVRSETTRANSTYPE</td><td>设置转封装类型</td><td>一个4字节整型的转码类型： 1-PS，2-TS，3-RTP，5-MP4</td><td>无</td></tr></table></body></html>  

#### 5.14.35 停止下载录像文件 NET_DVR_StopGetFile  

函  数： BOOL NET_DVR_StopGetFile(LONG lFileHandle)  
参  数： [in]lFileHandle 下载句柄，NET_DVR_GetFileByName 或NET_DVR_GetFileByTime_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.14.36 获取当前下载录像文件的进度 NET_DVR_GetDownloadPos  

函  数： int NET_DVR_GetDownloadPos(LONG lFileHandle)  
参  数： [in]lFileHandle 下载句柄，NET_DVR_GetFileByName 或NET_DVR_GetFileByTime_V40 的返回值  
返回值： -1 表示失败， $0{\sim}100$ 表示下载的进度，100 表示下载结束。正常范围 0-100，返回 200 表明出现网络异常。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口用于获取按文件名下载录像文件时的下载进度。  

#### 录像文件锁定和解锁  

#### 5.14.37 按文件名锁定录像文件 NET_DVR_LockFileByName  

函  数： BOOL NET_DVR_LockFileByName(LONG lUserID, char \*sLockFileName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sLockFileName 要锁定的录像文件名，文件名长度需小于 100 字节  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在使用该接口锁定录像文件前，可以先调用录像文件查找的接口获取文件名。当文件被锁定后，将不会被覆盖。  

#### 5.14.38 按文件名解锁录像文件 NET_DVR_UnlockFileByName  

函  数： BOOL NET_DVR_UnlockFileByName(LONG lUserID, char \*sUnlockFileName)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sUnlockFileName 要解锁的录像文件名  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在使用该接口锁定录像文件前，可以先调用录像文件查找的接口获取文件名。  

返回目录  

#### 5.14.39 流 ID 方式对某一时间段录像文件进行加锁  

NET_DVR_LockStreamFileByTime  

函  数： BOOL NET_DVR_LockStreamFileByTime(LONG lUserID, LPNET_DVR_STREAM_TIME_LOCK lpLockPara,LPNET_DVR_LOCK_RETURN lpLockReturn)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lpLockPara 录像加锁参数，包括流信息（ID 或通道号）、录像类型、开始和结束时间、锁定持续时间等[out]lpLockReturn 录像加锁结果，包括实际锁定的开始时间和结束时间  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.14.40 流 ID 方式对某一时间段录像文件进行解锁  

#### NET_DVR_UnlockStreamFileByTime  

函  数： BOOL NET_DVR_UnlockStreamFileByTime(LONG lUserID, LPNET_DVR_STREAM_TIME_LOCKlpLockPara, LPNET_DVR_LOCK_RETURN lpLockReturn)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lpLockPara 录像解锁参数，包括流信息（ID 或通道号）、录像类型、开始和结束时间、锁定持续时间等[in]lpLockReturn 录像解锁结果，包括实际解锁的开始时间和结束时间TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 备份文件  

#### 5.14.41 获取设备磁盘列表 NET_DVR_GetDiskList  

函  数： BOOL NET_DVR_GetDiskList(LONG lUserID, LPNET_DVR_DISKABILITY_LIST lpDiskList)参  数： [in]lUserID NET_DVR_Login_V40 的返回值  

[out]lpDiskList 设备可用备份磁盘信息结构  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口用于获取设备可用备份文件的磁盘资源信息，在备份文件功能接口的输入参数中需要用到。  

#### 5.14.42 按文件名备份录像文件 NET_DVR_BackupByName  

函  数： LONG NET_DVR_BackupByName(LONG lUserID, LPNET_DVR_BACKUP_NAME_PARAMlpBackupByName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lpBackupByName 备份文件参数结构  
返回值： -1 表示失败，其他值作为 NET_DVR_GetBackupProgress，NET_DVR_StopBackup 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在调用该接口开始文件备份前必须调用接口 NET_DVR_GetDiskList 获取当前设备可用的磁盘列表信息，返回的磁盘描述字段用于指定此接口中 lpBackupByName 参数中的备份磁盘描述字段。其中参数 byDiskDes 是由接口 NET_DVR_GetDiskList 获取的参数得到。  

#### 5.14.43 按时间段备份录像文件 NET_DVR_BackupByTime  

函  数： LONG NET_DVR_BackupByTime(LONG lUserID, LPNET_DVR_BACKUP_TIME_PARAMlpBackupBytime)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lpBackupByName 备份文件参数结构  
返回值： -1 表示失败，其他值作为 NET_DVR_GetBackupProgress，NET_DVR_StopBackup 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在调用该接口开始文件备份前必须调用接口 NET_DVR_GetDiskList 获取当前设备可用的磁盘列表信息，返回的磁盘描述字段用于指定此接口中 lpBackupByTime 参数中的备份磁盘描述字段。对于审讯机设备 byDiskDes 和 byWithPlayer 参数无效，其他设备参数 byDiskDes 是由接口NET_DVR_GetDiskList 获取  

返回目录  

#### 5.14.44 获取备份的进度 NET_DVR_GetBackupProgress  

函  数： BOOL NET_DVR_GetBackupProgress(LONG lHandle, DWORD\* pState)  
参  数： [in]lHandle NET_DVR_BackupByName 或 NET_DVR_BackupByTime 的返回值[out] pState 当前备份的进度，进度值的取值范围为[0,100)，其他值的定义见表 5.26  

表 5.26 备份进度  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>BACKUP_SUCCESS</td><td>100</td><td>备份完成</td></tr><tr><td>BACKUP_CHANGE_DEVICE</td><td>101</td><td>备份设备已满，更换设备继续备份</td></tr><tr><td>BACKUP_SEARCH_DEVICE</td><td>300</td><td>正在搜索备份设备</td></tr><tr><td>BACKUP_SEARCH_FILE</td><td>301</td><td>正在搜索录像文件或者图片</td></tr><tr><td>BACKUP_EXCEPTION</td><td>400</td><td>备份异常</td></tr><tr><td>BACKUP_FAIL</td><td>500</td><td>备份失败</td></tr><tr><td>BACKUP_TIME_SEG_NO_FILE</td><td>501</td><td>时间段内无录像文件或者图片</td></tr><tr><td>BACKUP_NO_RESOURCE</td><td>502</td><td>申请不到资源</td></tr><tr><td>BACKUP_DEVICE_LOW_SPACE</td><td>503</td><td>备份设备容量不足</td></tr><tr><td>BACKUP_DISK_FINALIZED</td><td>504</td><td>刻录光盘封盘</td></tr><tr><td>BACKUP_DISK_EXCEPTION</td><td>505</td><td>刻录光盘异常</td></tr><tr><td>BACKUP_DEVICE_NOT_EXIST</td><td>506</td><td>备份设备不存在</td></tr><tr><td>BACKUP_OTNER_BACKUP_WORK</td><td>507</td><td>有其他备份操作在进行</td></tr><tr><td>BACKUP_USER_NO_RIGHT</td><td>508</td><td>用户没有操作权限</td></tr><tr><td>BACKUP_OPERATE_FAIL</td><td>509</td><td>操作失败</td></tr></table></body></html>

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。说  明： 在进度为 100 或者备份出错时, 需调用 NET_DVR_StopBackup()停止备份。  

#### 5.14.45 停止备份 NET_DVR_StopBackup  

函  数： BOOL NET_DVR_StopBackup(LONG lHandle)  
参  数： [in]lHandle NET_DVR_BackupByName 或 NET_DVR_BackupByTime 的返回值，或者 NET_DVR_BackupPicture 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

### 5.15 图片的查找、回放及备份  

#### 查找图片  

#### 5.15.1 根据类型和时间查找图片 NET_DVR_FindPicture  

函  数： LONG NET_DVR_FindPicture(LONG lUserID, NET_DVR_FIND_PICTURE_PARAM\* pFindParam)参  数： [in]lUserID NET_DVR_Login_V40 的返回值  

[in]pFindParam 图片查找条件信息，包括查找的通道号、图片类型和起止时间等  
返回值： -1 表示失败，其他值作为 NET_DVR_CloseFindPicture 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口指定了要查找的图片的类型和查找时间范围，调用成功后，就可以调用NET_DVR_FindNextPicture 接口来获取图片信息。注：该接口查找的是设备本地的图片，可通过NET_DVR_SetDVRConfig 配置设备的抓图计划（NET_DVR_SCHED_CAPTURECFG）。  

返回目录  

#### 5.15.2 逐个获取查找到的图片 NET_DVR_FindNextPicture_V40  

函  数： LONG NET_DVR_FindNextPicture_V40(LONG lFindHandle, LPNET_DVR_FIND_PICTURE_V40lpFindData)  
参  数： [in]lFindHandle 图片查找句柄，NET_DVR_FindPicture 的返回值[out]lpFindData 查找到的图片结果信息，包括图片名称、时间、类  
返回值： -1 表示失败，其他值表示当前的获取状态等信息，如表 5.27 所示。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

表 5.27 查找状态信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_FILE_SUCCESS</td><td>1000</td><td>获取图片信息成功</td></tr><tr><td>NET_DVR_FILE_NOFIND</td><td>1001</td><td>未查找到图片</td></tr><tr><td>NET_DVR_ISFINDING</td><td>1002</td><td>正在查找请等待</td></tr><tr><td>NET_DVR_NOMOREFILE</td><td>1003</td><td>没有更多的图片，查找结束</td></tr><tr><td>NETDVRFILEEXCEPTION</td><td>1004</td><td>查找图片时异常</td></tr></table></body></html>  

说  明： 在调用该接口获取查找图片之前，必须先调用 NET_DVR_FindPicture 得到当前的查找句柄。此接口用于获取一条已查找到的图片信息，若要获取全部的已查找到的图片信息，需要循环调用此接口。  

#### 5.15.3 关闭图片查找，释放资源 NET_DVR_CloseFindPicture  

函  数： BOOL NET_DVR_CloseFindPicture(LONG lFindHandle)  
参  数： [in]lFindHandle 图片查找句柄，NET_DVR_FindPicture 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 图片智能检索（后检索）  

#### 5.15.4 开始智能图片检索 NET_DVR_SmartSearchPicture  

函  数： LONG NET_DVR_SmartSearchPicture(LONG lUserID, NET_DVR_SMART_SEARCH_PIC_PARA\*pFindParam)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]pFindParam 智能图片搜索信息，包括智能查找类型、通道号和起止时间等  
返回值： -1 表示失败，其他值作为 NET_DVR_CloseSmartSearchPicture 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口指定了要查找的图片的类型和查找时间范围，调用成功后，就可以调用NET_DVR_FindNextSmartPicture 接口来获取图片信息。  

#### 5.15.5 逐个获取搜索到的智能图片信息 NET_DVR_FindNextSmartPicture  

函  数： LONG NET_DVR_FindNextSmartPicture(LONG lFindHandle, LPNET_DVR_SMART_SEARCH_PIC_RETlpFindData)  
参  数： [in]lFindHandle 图片智能检索句柄，NET_DVR_SmartSearchPicture 的返回值[out]lpFindData 查找到的智能图片结果信息，包括图片名称、时间、事件类型等  
返回值： -1 表示失败，其他值表示当前的获取状态等信息，如表 5.28 所示。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

表 5.28 查找状态信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_FILE_SUCCESS</td><td>1000</td><td>获取图片信息成功</td></tr><tr><td>NET_DVR_FILE_NOFIND</td><td>1001</td><td>未查找到图片</td></tr><tr><td>NET_DVR_ISFINDING</td><td>1002</td><td>正在查找请等待</td></tr><tr><td>NET_DVR_NOMOREFILE</td><td>1003</td><td>没有更多的图片，查找结束</td></tr><tr><td>NETDVRFILEEXCEPTION</td><td>1004</td><td>查找图片时异常</td></tr></table></body></html>  

说  明： 在调用该接口获取查找图片之前，必须先调用 NET_DVR_FindPicture 得到当前的查找句柄。此接口用于获取一条已查找到的图片信息，若要获取全部的已查找到的图片信息，需要循环调用此接口。  

#### 5.15.6 关闭图片智能检索，释放资源 NET_DVR_CloseSmartSearchPicture  

函  数： BOOL NET_DVR_CloseSmartSearchPicture(LONG lFindHandle)  
参  数： [in]lFindHandle 图片智能检索句柄，NET_DVR_SmartSearchPicture 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 回放（下载）图片  

#### 5.15.7 图片回放 NET_DVR_GetPicture_V30  

函  数： BOOL NET_DVR_GetPicture_V30(LONG lUserID, char \*sDVRFileName, char \*sSavedFileBuf, DWORD  

dwBufLen, DWORD \*lpdwRetLen)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sDVRFileName 图片名称[in]sSavedFileName 保存图片的缓冲区[in]dwBufLen 缓冲区大小[out]lpdwRetLen 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 图片为 JPEG 格式，数据保存在缓冲区 sSavedFileName 中。  

#### 备份图片  

#### 5.15.8 备份图片 NET_DVR_BackupPicture  

函  数： LONG NET_DVR_BackupPicture(LONG lUserID, NET_DVR_BACKUP_PICTURE_PARAM\*lpBackupPicture)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lpBackupPicture 图片备份参数  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.15.9 获取备份的进度 NET_DVR_GetBackupProgress  

函  数： BOOL NET_DVR_GetBackupProgress(LONG lHandle, DWORD\* pState)  
参  数： [in]lHandle NET_DVR_BackupPicture 的返回值[out]pState 当前备份的进度，进度值的取值范围为[0,100)，其他值的定义见表 5.29  

表 5.29 备份进度  


<html><body><table><tr><td>pState宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>BACKUP_SUCCESS</td><td>100</td><td>备份完成</td></tr><tr><td>BACKUP_CHANGE_DEVICE</td><td>101</td><td>备份设备已满，更换设备继续备份</td></tr><tr><td>BACKUP_SEARCH_DEVICE</td><td>300</td><td>正在搜索备份设备</td></tr><tr><td>BACKUP_SEARCH_FILE</td><td>301</td><td>正在搜索录像文件或者图片</td></tr><tr><td>BACKUP_EXCEPTION</td><td>400</td><td>备份异常</td></tr><tr><td>BACKUP_FAIL</td><td>500</td><td>备份失败</td></tr><tr><td>BACKUP_TIME_SEG_NO_FILE</td><td>501</td><td>时间段内无录像文件或者图片</td></tr><tr><td>BACKUP_NO_RESOURCE</td><td>502</td><td>申请不到资源</td></tr><tr><td>BACKUP_DEVICE_LOW_SPACE</td><td>503</td><td>备份设备容量不足</td></tr></table></body></html>  

<html><body><table><tr><td>BACKUPDISKFINALIZED</td><td>504</td><td>刻录光盘封盘</td></tr><tr><td>BACKUP_DISK_EXCEPTION</td><td>505</td><td>刻录光盘异常</td></tr><tr><td>BACKUP_DEVICE_NOT_EXIST</td><td>506</td><td>备份设备不存在</td></tr><tr><td>BACKUP_OTNER_BACKUP_WORK</td><td>507</td><td>有其他备份操作在进行</td></tr><tr><td>BACKUP_USER_NO_RIGHT</td><td>508</td><td>用户没有操作权限</td></tr><tr><td>BACKUPOPERATEFAIL</td><td>509</td><td>操作失败</td></tr></table></body></html>

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。说  明： 在进度为 100 或者备份出错时, 需调用 NET_DVR_StopBackup()停止备份。  

#### 5.15.10 停止备份 NET_DVR_StopBackup  

函  数： BOOL NET_DVR_StopBackup(LONG lHandle)  
参  数： [in]lHandle NET_DVR_BackupPicture 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.16布防、撤防  

设置报警等信息上传的回调函数  

#### 5.16.1 注册回调函数，接收报警消息 NET_DVR_SetDVRMessageCallBack_V30  

函  数： BOOL NET_DVR_SetDVRMessageCallBack_V30(MSGCallBack fMessageCallBack, void\* pUser)  

参  数： [in]fMessageCallBack 报警信息回调函数[in]pUser 用户数据typedef void(CALLBACK \*MSGCallBack)(LONG lCommand, NET_DVR_ALARMER \*pAlarmer, char\*pAlarmInfo, DWORD dwBufLen, void \*pUser)  

[out]lCommand 上传的消息类型，详见表 5.30  
[out]pAlarmer 报警设备信息  
[out]pAlarmInfo 报警信息，详见表 5.31  
[out]dwBufLen 报警信息缓存大小  
[out]pUser 用户数据  

表 5.30 报警信息类型  


<html><body><table><tr><td>ICommand宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>COMMALARM</td><td>0x1100</td><td>V3.0以下版本支持的设备的报警信息上传</td></tr><tr><td>COMMALARMV30</td><td>0x4000</td><td>V3.0以上版本支持的设备的报警信息上传</td></tr><tr><td>COMMIPCCFG</td><td>0x4001</td><td>混合型DVR在IPC接入配置改变时的报警信息上传</td></tr></table></body></html>  

<html><body><table><tr><td>COMM_IPCCFG_V31</td><td>0x4002</td><td>混合型DVR在IPC接入配置改变时的报警信息上传（扩展）</td></tr><tr><td>COMM_ALARM_HOTSPARE</td><td>0x4006</td><td>热备异常报警（N+1模式异常报警）</td></tr><tr><td>COMMALARMV40</td><td>0x4007</td><td>移动侦测、视频丢失、遮挡、IO信号量等报警信息主动上传， 报警数据为可变长</td></tr><tr><td>COMM_ALARM_VQD</td><td>0x6000</td><td>VQD诊断报警信息上传</td></tr><tr><td>COMMVEHICLECONTROLALARM</td><td>0x3059</td><td>黑授权名单车辆报警上传</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中回调函数的第一个参数（lCommand）和第三个参数（pAlarmInfo）是密切关联的，其关系见表 5.31。  

表 5.31 报警信息结构  


<html><body><table><tr><td>消息类型ICommand</td><td>上传内容</td><td>pAlarmlnfo对应的结构体</td></tr><tr><td>COMM_ALARM</td><td>V3.0以下版本支持的设备的报警信息</td><td>NET_DVR_ALARMINFO</td></tr><tr><td>COMM_ALARM_V30</td><td>V3.0以上版本支持的设备的报警信息</td><td>NET_DVR_ALARMINFO_V30</td></tr><tr><td>COMM_IPCCFG</td><td>混合型DVR在IPC接入配置改变时的报警信息</td><td>NET_DVR_IPALARMINFO</td></tr><tr><td>COMM_IPCCFG_V31</td><td>混合型DVR在IPC接入配置改变时的报警信息（扩展</td><td>NET_DVR_IPALARMINFO_V31</td></tr><tr><td>COMM_ALARM_HOT_SPARE</td><td>热备异常报警（N+1模式异常报警）信息</td><td>NET_DVR_ALARM_HOT_SPARE</td></tr><tr><td>COMM_ALARM_V40</td><td>移动侦测、视频丢失、遮挡、IO信号量等报警信息</td><td>NET_DVR_ALARMINFO_V40</td></tr><tr><td>COMM_ALARM_VQD</td><td>VQD诊断报警信息</td><td>NET_DVR_VQD_DIAGNOSE_INFO</td></tr><tr><td>COMM_VEHICLE_CONTROL_ALARM</td><td>黑授权名单车辆报警上传</td><td>NET_DVRVEHICLE_CONTROLALARM</td></tr></table></body></html>  

#### 布防撤防  

#### 5.16.2 建立报警上传通道，获取报警等信息 NET_DVR_SetupAlarmChan_V41  

函  数： LONG NET_DVR_SetupAlarmChan_V41(LONG lUserID, LPNET_DVR_SETUPALARM_PARAMlpSetupParam)  
参  数： [in] lUserID NET_DVR_Login_V40 的返回值[in] lpSetupParam 报警布防参数  
返回值： -1 表示失败，其他值作为 NET_DVR_CloseAlarmChan_V30 函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 使用该接口支持上传 V3.0 以上版本支持的设备的报警结构。启动布防前，需要调用注册回调函数的接口（如 NET_DVR_SetDVRMessageCallBack_V30）才能获取到上传的报警等信息。  

#### 5.16.3 撤销报警上传通道 NET_DVR_CloseAlarmChan_V30  

函  数： BOOL NET_DVR_CloseAlarmChan_V30(LONG lAlarmHandle)  
参  数： [in]lAlarmHandle NET_DVR_SetupAlarmChan_V41 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.17 监听报警  

#### 5.17.1 启动监听，接收设备主动上传的报警等信息 NET_DVR_StartListen_V30  

函  数： LONG NET_DVR_StartListen_V30(char \*sLocalIP, WORD wLocalPort, MSGCallBack DataCallback, void\*pUserData $=$ NULL)  

参  数： [in]sLocalIP PC 机本地 IP 地址，可以置为 NULL[in]wLocalPort PC 本地监听端口号。由用户设置，必须和设备端设置的一致[in]DataCallback 回调函数[in]pUserData 用户数据  

typedef void(CALLBACK \*MSGCallBack)(LONG lCommand,NET_DVR_ALARMER \*pAlarmer,char \*pAlarmInfo,DWORD dwBufLen,void \*pUser)  

[out]lCommand 上传的消息类型，详见表 5.32  
[out]pAlarmer 报警设备信息  
[out]pAlarmInfo 报警信息，详见表 5.32  
[out]dwBufLen 报警信息缓存大小  
[out]pUser 用户数据  

表 5.32 报警信息类型  


<html><body><table><tr><td>ICommand宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>COMM_ALARM</td><td>0x1100</td><td>V3.0以下版本支持的设备的报警信息上传</td></tr><tr><td>COMM_ALARM_V30</td><td>0x4000</td><td>V3.0以上版本支持的设备的报警信息上传</td></tr><tr><td>COMM_IPCCFG</td><td>0x4001</td><td>混合型DVR在IPC接入配置改变时的报警信息上传</td></tr><tr><td>COMM_IPCCFG_V31</td><td>0x4002</td><td>混合型DVR在IPC接入配置改变时的报警信息上传（扩展）</td></tr><tr><td>COMM_ALARM_HOT_SPARE</td><td>0x4006</td><td>热备异常报警（N+1模式异常报警）</td></tr><tr><td>COMM_ALARM_V40</td><td>0x4007</td><td>移动侦测、视频丢失、遮挡、1O信号量等报警信息主动上传 报警数据为可变长</td></tr><tr><td>COMM_ALARM_VQD</td><td>0x6000</td><td>VQD诊断报警信息上传</td></tr></table></body></html>  

返回值： -1 表示失败，其他值作为 NET_DVR_CloseAlarmChan_V30 函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中回调函数的第一个参数（lCommand）和第三个参数（pAlarmInfo）是密切关联的，其关系见表 5.33。  

表 5.33 报警信息结构  


<html><body><table><tr><td>消息类型ICommand</td><td>上传内容</td><td>pAlarmlnfo对应的结构体</td></tr><tr><td>COMM_ALARM</td><td>V3.0以下版本支持的设备的报警信息</td><td>NET_DVR_ALARMINFO</td></tr><tr><td>COMM_ALARM_V30</td><td>V3.0以上版本支持的设备的报警信息</td><td>NET_DVR_ALARMINFO_V30</td></tr><tr><td>COMM_IPCCFG</td><td>混合型DVR在IPC接入配置改变时的报警信息</td><td>NETDVRIPALARMINFO</td></tr><tr><td>COMM_IPCCFG_V31</td><td>混合型DVR 在IPC 接入配置改变时的报警信息 （扩展）</td><td>NETDVRIPALARMINFO_V31</td></tr><tr><td>COMM_ALARM_HOT_SPARE</td><td>热备异常报警（N+1模式异常报警）信息</td><td>NET_DVR_ALARM_HOT_SPARE</td></tr><tr><td>COMM_ALARM_V40</td><td>移动侦测、视频丢失、遮挡、IO信号量等报警信NET_DVR_ALARMINFO_V40 息</td><td></td></tr><tr><td>COMM_ALARM_VQD</td><td>VQD诊断报警信息</td><td>NET_DVR_VQD_DIAGNOSE_INFO</td></tr></table></body></html>  

SDK 最大能支持 512 路监听。  

要使 PC 能够收到设备主动发过来的报警等信息，必须将设备的网络配置中的“远程管理主机地址”或者“远程报警主机地址”设置成 PC 机的 IP 地址（与接口中的 sLocalIP 参数一致），“远程管理主机端口号”或者“远程报警主机端口号”设置成 PC 机的监听端口号（与接口中的wLocalPort 参数一致）。  

该接口中的回调函数优先级高于其他回调函数，即设置了该接口中的回调函数，其他回调函数将接收不到报警信息。  

返回目录  

#### 5.17.2 停止监听（支持多线程） NET_DVR_StopListen_V30  

函  数： BOOL  NET_DVR_StopListen_V30(LONG lListenHandle)  
参  数： [in]lListenHandle 监听句柄，NET_DVR_StartListen_V30 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.18语音对讲、转发及广播  

#### 语音对讲  

#### 5.18.1 启动语音对讲 NET_DVR_StartVoiceCom_V30  

函  数： LONG NET_DVR_StartVoiceCom_V30(LONG lUserID, DWORD dwVoiceChan, BOOLbNeedCBNoEncData, fVoiceDataCallBack cbVoiceDataCallBack, void\* pUser)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwVoiceChan 语音通道号，从 1 开始[in]bNeedCBNoEncData 需要回调的语音数据类型：0- 编码后的语音数据，1- 编码前的  

PCM 原始数据[in]cbVoiceDataCallBack 音频数据回调函数[in]pUser 用户数据指针typedef void(CALLBACK \*fVoiceDataCallBack)(LONG lVoiceComHandle, char \*pRecvDataBuffer,DWORD dwBufSize, BYTE byAudioFlag, void \*pUser)[out]lVoiceComHandle NET_DVR_StartVoiceCom_V30 的返回值[out]pRecvDataBuffer 存放音频数据的缓冲区指针[out]dwBufSize 音频数据大小[out]byAudioFlag 音频数据类型：0-本地采集的数据；1-设备发送过来的语音数据[out]pUser 用户数据指针  

返回值： -1 表示失败，其他值作为 NET_DVR_StopVoiceCom 等函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

Windows 7 操作系统下，如果不外接音频设备，该接口将返回失败。  
在调用开始语音对讲之前可先配置设备的语音对讲音频编码类型，即可先调用参数配置中的NET_DVR_COMPRESSION_AUDIO 结构配置。  
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
m_wavFormatEx.nAvgBytesPerSec $=$ SAMPLES_PER_SECOND\*m_wavFormatEx.nBlockAlign当前音频为 G711 编码时，音频数据的采样频率为 8000，16 位采样且是单通道的。因此，音频播放格式应如下定义：  
const int SAMPLES_PER_SECOND_G711_MU $=$ 8000;  
const int CHANNEL $=1$ ;  
const int BITS_PER_SAMPLE $=16$ ;  
WAVEFORMATEX m_wavFormatEx;  
m_wavFormatEx.cbSize $=$ sizeof(m_wavFormatEx);  
m_wavFormatEx.nBlockAlign $=$ CHANNEL $^*$ BITS_PER_SAMPLE / 8;  
m_wavFormatEx.nChannels $=$ CHANNEL;  
m_wavFormatEx.nSamplesPerSec $=$ SAMPLES_PER_SECOND_G711_MU;  
m_wavFormatEx.wBitsPerSample $=$ BITS_PER_SAMPLE;  
m_wavFormatEx.nAvgBytesPerSec $=$ SAMPLES_PER_SECOND_G711_MU\*  
m_wavFormatEx.nBlockAlign;  

#### 5.18.2 设置语音对讲客户端的音量 NET_DVR_SetVoiceComClientVolume  

函  数： BOOL NET_DVR_SetVoiceComClientVolume(LONG lVoiceComHandle, WORD wVolume)  
参  数： [in]lVoiceComHandle NET_DVR_StartVoiceCom_V30 的返回值[in]wVolume 设置音量，取值范围[0,0xffff]  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.18.3 停止语音对讲或者语音转发 NET_DVR_StopVoiceCom  

函  数： BOOL  NET_DVR_StopVoiceCom(LONG lVoiceComHandle)  
参  数： [in]lVoiceComHandle NET_DVR_StartVoiceCom_V30 或NET_DVR_StartVoiceCom_MR_V30 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 语音转发  

#### 5.18.4 启动语音转发，获取编码后的音频数据 NET_DVR_StartVoiceCom_MR_V30  

函  数： LONG NET_DVR_StartVoiceCom_MR_V30(LONG lUserID, DWORD dwVoiceChan, fVoiceDataCallBackcbVoiceDataCallBack, void\* pUser)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwVoiceChan 语音通道号，从 1 开始[in]cbVoiceDataCallBack 音频数据回调函数，得到的数据是编码以后的音频数据，需调用我们提供的音频解码函数（详见音频编解码章节的说明）后可得到 PCM 数据[in]pUser 用户数据指针typedef void(CALLBACK \*fVoiceDataCallBack)(LONG lVoiceComHandle, char \*pRecvDataBuffer,DWORD dwBufSize, BYTE byAudioFlag, void\*pUser)[out]lVoiceComHandle NET_DVR_StartVoiceCom_MR_V30 的返回值[out]pRecvDataBuffer 存放音频数据的缓冲区指针[out]dwBufSize 音频数据大小[out]byAudioFlag 音频数据类型：1-设备发送过来的音频数据[out]pUser 用户数据指针  

返回值： -1 表示失败，其他值作为 NET_DVR_VoiceComSendData、NET_DVR_StopVoiceCom 等函数的句柄参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

： 在调用开始语音转发之前可先配置设备的音频编码类型，即可先调用参数配置中的NET_DVR_COMPRESSION_AUDIO 结构配置。当前音频为 G722 编码时，音频数据的采样频率为 16000，16 位采样且是单通道的。因此，音频播放格式应如下定义：const int SAMPLES_PER_SECOND $=$ 16000;const int CHANNEL $=1$ ;const int BITS_PER_SAMPLE $=16$ ;WAVEFORMATEX m_wavFormatEx;m_wavFormatEx.cbSize $=$ sizeof(m_wavFormatEx);m_wavFormatEx.nBlockAlign $=$ CHANNEL $^*$ BITS_PER_SAMPLE / 8;m_wavFormatEx.nChannels $=$ CHANNEL;m_wavFormatEx.nSamplesPerSec $=$ SAMPLES_PER_SECOND;m_wavFormatEx.wBitsPerSample $=$ BITS_PER_SAMPLE;m_wavFormatEx.nAvgBytesPerSec $=$ SAMPLES_PER_SECOND\*m_wavFormatEx.nBlockAlign  

当前音频为 G711 编码时，音频数据的采样频率为 8000，16 位采样且是单通道的。因此，音频播放格式应如下定义：  
const int SAMPLES_PER_SECOND_G711_MU $=$ 8000;  
const int CHANNEL $=1$ ;  
const int BITS_PER_SAMPLE $=16$ ;  
WAVEFORMATEX m_wavFormatEx;  
m_wavFormatEx.cbSize $=$ sizeof(m_wavFormatEx);  
m_wavFormatEx.nBlockAlign $=$ CHANNEL $^*$ BITS_PER_SAMPLE / 8;  
m_wavFormatEx.nChannels $=$ CHANNEL;  
m_wavFormatEx.nSamplesPerSec $=$ SAMPLES_PER_SECOND_G711_MU;  
m_wavFormatEx.wBitsPerSample $=$ BITS_PER_SAMPLE;  
m_wavFormatEx.nAvgBytesPerSec $=$ SAMPLES_PER_SECOND_G711_MU\*  
m_wavFormatEx.nBlockAlign;  

#### 5.18.5 转发语音数据 NET_DVR_VoiceComSendData  

函  数： BOOL NET_DVR_VoiceComSendData(LONG lVoiceComHandle, char \*pSendBuf, DWORD dwBufSize)  

参  数： [in]lVoiceComHandle NET_DVR_StartVoiceCom_MR_V30 的返回值[in]pSendBuf 存放语音数据的缓冲区[in]dwBufSize 语音数据大小。当前是 G722 音频编码类型时，每次发送的数据为 80 字节；当前是 G711 音频编码类型时，每次发送的数据为 160 字节。  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口实现将获取到的经过编码后的音频数据转发给设备。  

#### 5.18.6 停止语音对讲或语音转发 NET_DVR_StopVoiceCom  

函  数： BOOL NET_DVR_StopVoiceCom (LONG lVoiceComHandle)参  数： [in]lVoiceComHandle NET_DVR_StartVoiceCom_V30 或NET_DVR_StartVoiceCom_MR_V30 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。  

说  明：  

#### 语音广播  

#### 5.18.7 启动语音广播的 PC 端声音捕获 NET_DVR_ClientAudioStart_V30  

函  数： BOOL NET_DVR_ClientAudioStart_V30(fVoiceDataCallBack  cbVoiceDataCallBack, void \*pUser)  

参  数： [in]cbVoiceDataCallBack 音频数据回调函数[in]pUser 用户数据typedef void(CALLBACK \*fVoiceDataCallBack)(char \*pRecvDataBuffer, DWORD dwBufSize, void\*pUser)[out]pRecvDataBuffer 存放 PC 本地采集的音频数据（PCM）的缓冲区指针[out]dwBufSize 音频数据大小[out]pUser 用户数据指针  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： Windows 7 操作系统下，如果不外接音频设备，该接口将返回失败。实现语音广播功能需先调用 NET_DVR_ClientAudioStart_V30 接口采集本地 PC 的音频数据，再调用 NET_DVR_AddDVR 或者 NET_DVR_AddDVR_V30 逐个添加设备同时将采集到的数据发送给设备。  

#### 5.18.8 添加设备的某个语音通道到可以接收 PC 端声音的广播组  

NET_DVR_AddDVR _V30  

函  数： LONG NET_DVR_AddDVR_V30(LONG lUserID, DWORD dwVoiceChan)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwVoiceChan 语音通道号，从 1 开始  
返回值： -1 表示失败，其他值作为 NET_DVR_DelDVR_V30 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 实现语音广播功能需先调用 NET_DVR_ClientAudioStart_V30 接口采集本地 PC 的音频数据，再调用 NET_DVR_AddDVR 或者 NET_DVR_AddDVR_V30 逐个添加设备同时将采集到的数据发送给设备。SDK 最大支持添加 512 个设备。  

#### 5.18.9 从可接收 PC 机声音的广播组里删除该设备的语音通道  

NET_DVR_DelDVR_V30  

函  数： LONG NET_DVR_DelDVR_V30(LONG lUserID)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.18.10 停止语音广播的 PC 端声音捕获 NET_DVR_ClientAudioStop  

函  数： BOOL NET_DVR_ClientAudioStop()  
参  数：  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError获取错误码，通过错误码判断出错原因。  

说  明：  

#### 音频压缩参数  

#### 5.18.11 获取当前生效的对讲音频压缩参数 NET_DVR_GetCurrentAudioCompress  

函  数： BOOL NET_DVR_GetCurrentAudioCompress(LONG lUserID, LPNET_DVR_COMPRESSION_AUDIOlpCompressAudio)  
参  数： [in] lUserID 用户 ID，NET_DVR_Login_V40 的返回值[in] lpCompressAudio 音频压缩参数  
返回值： -1 表示失败，其他值为音频编码句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

返回目录  

#### 5.18.12 获取通道参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可  

[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.34 所示。  

表 5.34 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_COMPRESSCFG_AUD</td><td>获取语音对讲音频参数</td><td>无效</td><td>NET_DVR_COMPRESSION_AUDIO</td><td>1058</td></tr></table></body></html>  

#### 5.18.13 设置通道参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.35 所示。  

表 5.35 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_COMPRESSCFG_AUD</td><td>设置语音对讲音频参数</td><td>无效</td><td>NET_DVR_COMPRESSION_AUDIO</td><td>1059</td></tr></table></body></html>  

#### 音频编解码(Windows 32 位系统支持)  

#### G722 音频编解码  

#### 5.18.14 初始化音频编码 NET_DVR_InitG722Encoder  

函  数： void\* NET_DVR_InitG722Encoder()  
参  数：  
返回值： -1 表示失败，其他值为音频编码句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.18.15 G722 音频编码 NET_DVR_EncodeG722Frame  

函  数： BOOL NET_DVR_EncodeG722Frame(void \*pEncodeHandle,unsigned char\* pInBuffer, unsigned char\*pOutBuffer)  

参  数： [in]pEncodeHandle 音频编码句柄，NET_DVR_InitG722Encoder 的返回值[inpInBuffer 输入缓冲区，按采样标准（采样频率为 16000，16 位采样，单通道）获取的 PCM 音频数据，规定输入数据的大小为 1280 字节[out]pOutBuffer 输出缓冲区，编码后的输出数据大小为 80 字节  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 主要为配合语音对讲、转发功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数 NET_DVR_DecodeG722Frame 进行数据解码。在调用编解码函数之前都需要做相应的初始化操作，在结束调用后还需要做释放资源的操作。  

返回目录  

#### 5.18.16 释放音频编码资源 NET_DVR_ReleaseG722Encoder  

函  数： void NET_DVR_ReleaseG722Encoder(void \*pEncodeHandle)参  数： [in]pEncodeHandle 音频编码句柄，NET_DVR_InitG722Encoder 的返回值返回值： 无。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.18.17 初始化音频解码 NET_DVR_InitG722Decoder  

函  数： void\* NET_DVR_InitG722Decoder(int nBitrate $=$ 16000)  
参  数： [in]nBitrate 编码采样频率，这里我们规定采样频率为 16000  
返回值： -1 表示失败，其他值为音频解码句柄。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.18.18 G722 音频解码 NET_DVR_DecodeG722Frame  

函  数： BOOL NET_DVR_DecodeG722Frame(void \*pDecHandle, unsigned char\* pInBuffer, unsigned char\*pOutBuffer)  

参  数： [in]pDecHandle 音频解码句柄，NET_DVR_InitG722Decoder 的返回值[in]pInBuffer 输入缓冲区，编码数据大小为 80 字节[out]pOutBuffer 输出缓冲区，按采样标准（采样频率为 16000，16 位采样，单通道）获取的 PCM 音频数据，规定输出数据的大小为 1280 字节返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 主要为配合语音对讲、转发功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数 NET_DVR_EncodeG722Frame 将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数进行数据解码。在调用编解码函数之前都需要做相应的初始化操作，在结束调用后还需要做释放资源的操作。  

返回目录  

#### 5.18.19 释放音频解码资源 NET_DVR_ReleaseG722Decoder  

函  数： void NET_DVR_ReleaseG722Decoder(void \*pDecHandle)参  数： [in]pDecHandle 音频解码句柄，NET_DVR_InitG722Decoder 的返回值返回值： 无返回值。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### G711 音频编解码  

#### 5.18.20 G711 音频编码 NET_DVR_EncodeG711Frame  

函  数： BOOL NET_DVR_EncodeG711Frame(unsigned int iType, unsigned char \*pInBuffer, unsigned char\*pOutBuffer)  

参  数： [in]iType 编码类型：0-Mu law 编码，非 0-A law 编码[in]pInBuffer 输入缓冲区，按采样标准（采样频率为 8000，16 位采样，单通道）获取的 PCM 音频数据，规定输入数据的大小为 320 字节[out]pOutBuffer 输出缓冲区，编码后输出数据大小为 160 字节  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 主要为配合语音对讲功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数 NET_DVR_DecodeG711Frame 进行数据解码。在调用编解码函数之前无需做初始化操作。  

#### 5.18.21 G711 音频解码 NET_DVR_DecodeG711Frame  

函  数： BOOL NET_DVR_DecodeG711Frame(unsigned int iType, unsigned char \*pInBuffer, unsigned char\*pOutBuffer)  

参  数： [in]iType 编码类型：0-Mu law 编码，非 0-A law 编码[in]pInBuffer 输入缓冲区，编码数据大小为 160 字节[out]pOutBuffer 输出缓冲区，按采样标准（采样频率为 8000，16 位采样，单通  

道）获取的 PCM 音频数据，规定输出数据的大小为 320 字节返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 主要为配合语音对讲、转发功能而设定，当需将客户端的原始音频数据发送至设备端，可采用音频编码函数 NET_DVR_EncodeG711Frame 将原始数据压缩编码后再发往设备端；客户端获取设备端发送过来的压缩码流，可调用音频解码函数进行数据解码。在调用编解码函数之前无需做初始化操作。  

### 5.19 远程参数配置  

#### 系统参数配置  

#### 5.19.1 获取设备参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.36 所示。  

表 5.36 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_DEVICECFG_V40</td><td>获取设备参数(扩展)</td><td>无效</td><td>NET_DVR_DEVICECFG_V40</td><td>1100</td></tr><tr><td>NET_DVR_GET_DECODERCFG_V30</td><td>获取RS485云台解码器 参数</td><td>通道号</td><td>NET_DVR_DECODERCFG_V30</td><td>1042</td></tr><tr><td>NET_DVR_GET_RS232CFG_V30</td><td>获取RS232串口参数</td><td>无效</td><td>NET_DVR_RS232CFG_V30</td><td>1036</td></tr><tr><td>NET_DVR_GET_EXCEPTIONCFG_V40</td><td>获取异常参数</td><td>组号，从0开始， 每组32个用户</td><td>NET_DVR_EXCEPTION_V40</td><td>6177</td></tr><tr><td>NET_DVR_GET_TIMECFG</td><td>获取时间参数</td><td>无效</td><td>NET_DVR_TIME</td><td>118</td></tr><tr><td>NET_DVR_GET_ZONEANDDST</td><td>获取时区和夏时制参数</td><td>无效</td><td>NET_DVR_ZONEANDDST</td><td>128</td></tr><tr><td>NET_DVR_GET_DEVSERVER_CFG</td><td>获取模块服务配置</td><td>无效</td><td>NET_DVR_DEVSERVER_CFG</td><td>3257</td></tr><tr><td>NET_DVR_GET_HOLIDAY_PARAM_CFG</td><td>获取节假日参数</td><td>无效</td><td>NET_DVR_HOLIDAY_PARAM_CFG</td><td>1240</td></tr></table></body></html>  

#### 5.19.2 设置设备参数 NET_DVR_SetDVRConfig  

函  数： BOOL  NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.37 所示。  

表 5.37 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_DEVICECFG_V40</td><td>设置设备参数(扩展)</td><td>无效</td><td>NET_DVR_DEVICECFG_V40</td><td>1101</td></tr><tr><td>NET_DVR_SET_DECODERCFG_V30</td><td>设置RS485云台解码器参 数</td><td>通道号</td><td>NET_DVR_DECODERCFG_V30</td><td>1043</td></tr><tr><td>NET_DVR_SET_RS232CFG_V30</td><td>设置RS232串口参数</td><td>无效</td><td>NET_DVR_RS232CFG_V30</td><td>1037</td></tr><tr><td>NET_DVR_SET_EXCEPTIONCFG_V40</td><td>设置异常参数</td><td>组号，从0开始， 每组32个用户</td><td>NET_DVR_EXCEPTION_V40</td><td>6178</td></tr><tr><td>NET_DVR_SET_TIMECFG</td><td>设置时间参数</td><td>无效</td><td>NET_DVR_TIME</td><td>119</td></tr><tr><td>NET_DVR_SET_ZONEANDDST</td><td>设置时区和夏时制参数</td><td>无效</td><td>NET_DVR_ZONEANDDST</td><td>129</td></tr><tr><td>NET_DVR_SET_DEVSERVER_CFG</td><td>设置模块服务配置</td><td>无效</td><td>NET_DVR_DEVSERVER_CFG</td><td>3258</td></tr><tr><td>NET_DVR_SET_HOLIDAY_PARAM_CFG</td><td>设置节假日参数</td><td>无效</td><td>NET_DVR_HOLIDAY_PARAM_CFG</td><td>1241</td></tr></table></body></html>  

#### 通道参数配置  

#### 5.19.3 获取通道参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.38 所示。  

 通道号是指设备视频通道号，通过注册设备（NET_DVR_Login_V30）返回的设备信息（NET_DVR_DEVICEINFO_V30）获取模拟通道个数（byChanNum）、模拟通道起始通道号（byStartChan）和设备支持的最大 IP 通道数（byIPChanNum+byHighDChanNum $^{*}256$ ）、数字通道起始通道号（byStartDChan）。  

表 5.38 获取设备通道参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_PICCFG_V40</td><td>获取图像参数</td><td>通道号</td><td>NET_DVR_PICCFG_V40</td><td>6179</td></tr><tr><td>NET_DVR_GET_COMPRESSCFG_V30</td><td>获取压缩参数</td><td>通道号</td><td>NET_DVR_COMPRESSIONCFG_V30</td><td>1040</td></tr><tr><td>NET_DVR_GET_RECORDCFG_V40</td><td>获取录像参数</td><td>通道号</td><td>NET_DVR_RECORD_V40</td><td>1008</td></tr><tr><td>NET_DVR_GET_SHOWSTRING_V30</td><td>获取叠加字符参数</td><td>通道号</td><td>NET_DVR_SHOWSTRING_V30</td><td>1030</td></tr><tr><td>NET_DVR_GET_JPEG_CAPTURE_CFG</td><td>获取设备抓图配置</td><td>通道号</td><td>NET_DVR_JPEG_CAPTURE_CFG</td><td>1280</td></tr><tr><td>NET_DVR_GET_SCHED_CAPTURECFG</td><td>获取抓图计划</td><td>通道号</td><td>NET_DVR_SCHED_CAPTURECFG</td><td>1282</td></tr><tr><td>NET_DVR_GET_VIDEO_INPUT_EFFECT</td><td>获取通道视频输入图像参数</td><td>通道号</td><td>NET_DVR_VIDEO_INPUT_EFFECT</td><td>1286</td></tr><tr><td>NET_DVR_GET_MOTION_HOLIDAY_HANDLE</td><td>获取移动侦测假日报警处理方式</td><td>通道号</td><td>NET_DVR_HOLIDAY_HANDLE</td><td>1242</td></tr><tr><td>NET_DVR_GET_VILOST_HOLIDAY_HANDLE</td><td>获取视频信号丢失假日报警处理方式</td><td>通道号</td><td>NET_DVR_HOLIDAY_HANDLE</td><td>1244</td></tr><tr><td>NET_DVR_GET_HIDE_HOLIDAY_HANDLE</td><td>获取遮盖假日报警处理方式</td><td>通道号</td><td>NET_DVR_HOLIDAY_HANDLE</td><td>1246</td></tr><tr><td>NET_DVR_GET_HOLIDAY_RECORD</td><td>获取假日录像参数</td><td>通道号</td><td>NET_DVR_HOLIDAY_RECORD</td><td>1252</td></tr><tr><td>NET_DVR_GET_LINK_STATUS</td><td>获取通道的工作状态</td><td>组号</td><td>NET_DVR_LINK_STATUS</td><td>1256</td></tr><tr><td>NET_DVR_GET_WD1_CFG</td><td>获取WD1使能开关状态</td><td>通道号</td><td>NET_DVR_WD1_CFG</td><td>6136</td></tr><tr><td>NET_DVR_GET_STREAM_CABAC</td><td>获取码流压缩性能选项</td><td>通道号</td><td>NET_DVR_STREAM_CABAC</td><td>6118</td></tr><tr><td>NET_DVR_GET_ACCESS_CAMERA_INFO</td><td>获取通道对应的前端相机信息</td><td>通道号</td><td>NET_DVR_ACCESS_CAMERA_INFO</td><td>6201</td></tr><tr><td>NET_DVR_GET_VIDEO_AUDIOIN_CFG</td><td>获取视频的音频输入参数</td><td>通道号</td><td>NET_DVR_VIDEO_AUDIOIN_CFG</td><td>9118</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.4 设置通道参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.39 所示。  

表 5.39 设置设备通道参数  


<html><body><table><tr><td>dwCommand 宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>IplnBuffer 对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_PICCFG_V40</td><td>设置图像参数</td><td>通道号</td><td>NET_DVR_PICCFG_V40</td><td>6180</td></tr><tr><td>NET_DVR_SET_COMPRESSCFG_V30</td><td>设置压缩参数</td><td>通道号</td><td>NET_DVR_COMPRESSIONCFG_V30</td><td>1041</td></tr><tr><td>NET_DVR_SET_RECORDCFG_V40</td><td>设置录像参数</td><td>通道号</td><td>NET_DVR_RECORD_V40</td><td>1009</td></tr><tr><td>NET_DVR_SET_SHOWSTRING_V30</td><td>设置叠加字符参数</td><td>通道号</td><td>NET_DVR_SHOWSTRING_V30</td><td>1031</td></tr><tr><td>NET_DVR_SET_JPEG_CAPTURE_CFG</td><td>设置设备抓图配置</td><td>通道号</td><td>NET_DVR_JPEG_CAPTURE_CFG</td><td>1281</td></tr><tr><td>NET_DVR_SET_SCHED_CAPTURECFG</td><td>设置抓图计划</td><td>通道号</td><td>NET_DVR_SCHED_CAPTURECFG</td><td>1283</td></tr><tr><td>NET_DVR_SET_VIDEO_INPUT_EFFECT</td><td>设置通道视频输入图像参数</td><td>通道号</td><td>NET_DVR_VIDEO_INPUT_EFFECT</td><td>1287</td></tr><tr><td>NET_DVR_SET_MOTION_HOLIDAY_HANDLE</td><td>设置移动侦测假日报警处理方式</td><td>通道号</td><td>NET_DVR_HOLIDAY_HANDLE</td><td>1243</td></tr><tr><td>NET_DVR_SET_VILOST_HOLIDAY_HANDLE</td><td>设置视频信号丢失假日报警处理方式</td><td>通道号</td><td>NET_DVR_HOLIDAY_HANDLE</td><td>1245</td></tr><tr><td>NET_DVR_SET_HIDE_HOLIDAY_HANDLE</td><td>设置遮盖假日报警处理方式</td><td>通道号</td><td>NET_DVR_HOLIDAY_HANDLE</td><td>1247</td></tr><tr><td>NET_DVR_SET_HOLIDAY_RECORD</td><td>设置假日录像参数</td><td>通道号</td><td>NET_DVR_HOLIDAY_RECORD</td><td>1253</td></tr><tr><td>NET_DVR_SET_WD1_CFG</td><td>设置WD1 使能开关</td><td>通道号</td><td>NET_DVR_WD1_CFG</td><td>6137</td></tr><tr><td>NET_DVR_SET_STREAM_CABAC</td><td>设置码流压缩性能选项</td><td>通道号</td><td>NET_DVR_STREAM_CABAC</td><td>6119</td></tr><tr><td>NET_DVR_SET_ACCESS_CAMERA_INFO</td><td>设置通道对应的前端相机信息</td><td>通道号</td><td>NET_DVR_ACCESS_CAMERA_INFO</td><td>6202</td></tr><tr><td>NET_DVR_SET_VIDEO_AUDIOIN_CFG</td><td>设置视频的音频输入参数</td><td>通道号</td><td>NET_DVR_VIDEO_AUDIOIN_CFG</td><td>9119</td></tr></table></body></html>  

#### 5.19.5 批量获取通道参数 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.40[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.41[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.41），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原  

因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.41 所示。  

表 5.40 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_MULTI_STREAM_COMPRESSIONCFG</td><td>远程获取多码流压缩参数</td><td>3216</td></tr><tr><td>NET_DVR_GET_STREAM_RECORD_STATUS</td><td>获取流录像状态信息</td><td>6021</td></tr><tr><td>NET_DVR_GET_DEFAULT_VIDEO_EFFECT</td><td>获取默认视频效果</td><td>6136</td></tr><tr><td>NET_DVR_GET_JPEG_CAPTURE_CFG_V40</td><td>获取设备抓图配置，dwCount为0</td><td>6190</td></tr></table></body></html>  

表 5.41 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_MULTI_STREAMCOMPRESSIONCFG</td><td>dwCount个 NET_DVR_MULTI_STREAM_COMPRESSIONCFG_COND</td><td>dwCount个 NET_DVR_MULTI_STREAM_COMPRESSIONCFG</td></tr><tr><td>NET_DVR_GET_STREAM_RECORD_STATUS</td><td>dwCount个 NET_DVR_STREAM_INFO</td><td>dwCount个 NET_DVR_STREAM_RECORD_STATUS</td></tr><tr><td>NETDVRGETDEFAULTVIDEOEFFECT</td><td>dwCount个NET_DVR_DEFAULT_VIDEO_COND</td><td>dwCount个NET_DVR_VIDEO_EFFECT</td></tr><tr><td>NET_DVR_GET_JPEG_CAPTURE_CFG_V40</td><td>NET_DVR_CHANNEL_GROUP</td><td>NET_DVR_JPEG_CAPTURE_CFG_V40</td></tr></table></body></html>  

#### 5.19.6 批量设置通道参数 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.42[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.43[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.43），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的获取功能对应不同的结构体和命令号，如表 5.43 所示。  

表 5.42 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NETDVRSET MULTISTREAMCOMPRESSIONCFG</td><td>远程设置多码流压缩参数</td><td>3217</td></tr><tr><td>NET_DVR_SET_STREAM_RECORD_STATUS</td><td>设置流录像状态信息</td><td>6022</td></tr><tr><td>NETDVRSETJPEGCAPTURE CFG_V40</td><td>设置设备抓图配置，dwCount为0</td><td>6191</td></tr></table></body></html>  

表 5.43 批量设置设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>lplnParamBuffer对应结构体</td></tr><tr><td>NET_DVR_SET_MULTI_STREAM_COMPRESSIONCFG</td><td>dwCount个 NET_DVR_MULTI_STREAM_COMPRESSIONCFG_COND</td><td>dwCount个 NETDVRMULTISTREAM_COMPRESSIONCFG</td></tr><tr><td>NET_DVRSETSTREAMRECORD_STATUS</td><td>dwCount 个 NET_DVR STREAM_INFO</td><td>dwCount 个 NET_DVR_STREAMRECORD_STATUS</td></tr><tr><td>NET_DVR_SET_JPEG_CAPTURE_CFG_V40</td><td>NET_DVR_CHANNEL_GROUP</td><td>NET_DVR_JPEG_CAPTURE_CFG_V40</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.7 远程控制 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.44[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.44[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，详见表 5.44。  

表 5.44 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NETDVRSETVIDEOEFFECT</td><td>6106</td><td>设置通道视频输入图像参数</td><td>NET_DVR_VIDEOPARA_V40</td></tr></table></body></html>  

#### 网络参数配置  

#### 5.19.8 获取网络参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.45 所示。  

表 5.45 获取设备参数  


<html><body><table><tr><td>dwCommand 宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>IpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_NETCFG_V30</td><td>获取网络参数</td><td>无效</td><td>NET_DVR_NETCFG_V30</td><td>1000</td></tr><tr><td>NET_DVR_GET_NETAPPCFG</td><td>获取网络应用参数(NTP/DDNS)</td><td>无效</td><td>NET_DVR_NETAPPCFG</td><td>222</td></tr><tr><td>NET_DVR_GET_NTPCFG</td><td>获取网络应用参数(NTP)</td><td>无效</td><td>NET_DVR_NTPPARA</td><td>224</td></tr><tr><td>NET_DVR_GET_DDNSCFG_V30</td><td>获取网络应用参数(DDNS)</td><td>无效</td><td>NET_DVR_DDNSPARA_V30</td><td>1010</td></tr><tr><td>NET_DVR_GET_EMAILCFG_V30</td><td>获取网络应用参数(EMAIL)</td><td>无效</td><td>NET_DVR_EMAILCFG_V30</td><td>1012</td></tr><tr><td>NET_DVR_GET_NETCFG_MULTI_V50</td><td>获取多网卡配置参数</td><td>组号， 从1开 始，每 组4个</td><td>NET_DVR_NETCFG_MULTI</td><td>1163</td></tr><tr><td>NET_DVR_GET_NETWORK_BONDING</td><td>获取BONDING网卡参数</td><td>网卡 无效</td><td>NET_DVR_NETWORK_BONDING</td><td>1254</td></tr><tr><td>NET_DVR_GET_FTPCFG</td><td>获取首选FTP参数</td><td>无效</td><td>NET_DVR_FTPCFG</td><td>134</td></tr><tr><td>NET_DVR_GET_FTPCFG_SECOND</td><td>获取备用FTP参数</td><td>无效</td><td>NET_DVR_FTPCFG</td><td>6103</td></tr><tr><td>NET_DVR_GET_SNMPCFG</td><td>获取 SNMP参数</td><td>无效</td><td>NET_DVR_SNMPCFG</td><td>1112</td></tr><tr><td>NET_DVR_GET_NAT_CFG</td><td>获取NAT映射参数</td><td>无效</td><td>NET_DVR_NAT_CFG</td><td>6111</td></tr><tr><td>NET_DVR_GET_POE_CFG</td><td>获取POE参数</td><td>无效</td><td>NET_DVR_POE_CFG</td><td>6114</td></tr><tr><td>NET_DVR_GET_BONJOUR_CFG</td><td>获取 Bonjour 信息</td><td>无效</td><td>NET_DVR_BONJOUR_CFG</td><td>6127</td></tr><tr><td>NET_DVR_GET_SOCKS_CFG</td><td>获取 SOCKS 信息</td><td>无效</td><td>NET_DVR_SOCKS_CFG</td><td>6130</td></tr><tr><td>NET_DVR_GET_QOS_CFG</td><td>获取Qos信息</td><td>无效</td><td>NET_DVR_QOS_CFG</td><td>6132</td></tr><tr><td>NET_DVR_GET_HTTPS_CFG</td><td>获取 HTTPS 信息</td><td>无效</td><td>NET_DVR_HTTPS_CFG</td><td>6134</td></tr><tr><td>NET_DVR_GET_DEVICE_NET_USING_INFO</td><td>获取当前设备网络资源使用情况</td><td>无效</td><td>NET_DVR_DEVICE_NET_USING_INFO</td><td>6009</td></tr></table></body></html>  

<html><body><table><tr><td>NETDVRGETCMSCFG</td><td>获取平台参数</td><td>无效</td><td>NETDVRCMSPARAM</td><td>2070</td></tr></table></body></html>  

#### 5.19.9 设置网络参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.46 所示。  

表 5.46 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>lplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_NETCFG_V30</td><td>设置网络参数</td><td>无效</td><td>NET_DVR_NETCFG_V30</td><td>1001</td></tr><tr><td>NET_DVR_SET_NETAPPCFG</td><td>设置网络应用参数(NTP/DDNS)</td><td>无效</td><td>NET_DVR_NETAPPCFG</td><td>223</td></tr><tr><td>NET_DVR_SET_NTPCFG</td><td>设置网络应用参数(NTP)</td><td>无效</td><td>NET_DVR_NTPPARA</td><td>225</td></tr><tr><td>NET_DVR_SET_DDNSCFG_V30</td><td>设置网络应用参数(DDNS)</td><td>无效</td><td>NET_DVR_DDNSPARA_V30</td><td>1011</td></tr><tr><td>NET_DVR_SET_EMAILCFG_V30</td><td>设置网络应用参数(EMAIL)</td><td>无效</td><td>NET_DVR_EMAILCFG_V30</td><td>1013</td></tr><tr><td>NET_DVR_SET_NETCFG_MULTI_V50</td><td>设置多网卡配置参数</td><td>组号，从 1开始， 每组4</td><td>NET_DVR_NETCFG_MULTI</td><td>1164</td></tr><tr><td>NET_DVR_SET_NETWORK_BONDING</td><td>设置BONDING网卡参数</td><td>个网卡 无效</td><td>NET_DVR_NETWORK_BONDING</td><td>1255</td></tr><tr><td>NET_DVR_SET_FTPCFG</td><td>设置首选 FTP参数</td><td>无效</td><td>NET_DVR_FTPCFG</td><td>135</td></tr><tr><td>NET_DVR_SET_FTPCFG_SECOND</td><td>设置备用FTP参数</td><td>无效</td><td>NET_DVR_FTPCFG</td><td>6104</td></tr><tr><td>NET_DVR_SET_SNMPCFG</td><td>设置 SNMP 参数</td><td>无效</td><td>NET_DVR_SNMPCFG</td><td>1113</td></tr><tr><td>NET_DVR_SET_NAT_CFG</td><td>设置 NAT映射参数</td><td>无效</td><td>NET_DVR_NAT_CFG</td><td>6112</td></tr><tr><td>NET_DVR_SET_POE_CFG</td><td>设置 POE 参数</td><td>无效</td><td>NET_DVR_POE_CFG</td><td>6115</td></tr><tr><td>NET_DVR_SET_BONJOUR_CFG</td><td>设置 Bonjour 信息</td><td>无效</td><td>NET_DVR_BONJOUR_CFG</td><td>6128</td></tr><tr><td>NET_DVR_SET_SOCKS_CFG</td><td>设置 SOCKS 信息</td><td>无效</td><td>NET_DVR_SOCKS_CFG</td><td>6131</td></tr><tr><td>NET_DVR_SET_QOS_CFG</td><td>设置QoS信息</td><td>无效</td><td>NET_DVR_QOS_CFG</td><td>6133</td></tr><tr><td>NET_DVR_SET_HTTPS_CFG</td><td>设置 HTTPS 信息</td><td>无效</td><td>NET_DVR_HTTPS_CFG</td><td>6135</td></tr><tr><td>NET_DVR_SET_CMS_CFG</td><td>设置平台参数</td><td>无效</td><td>NET_DVR_CMS_PARAM</td><td>2071</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.10 获取网络参数 NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.47[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.47  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.47所示。  

表 5.47 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IpCondBuffer</td><td>lpOutBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_GBT28181_SERVICE_CFG</td><td>获取GB28181服务器参数</td><td>NULL</td><td>NET_DVR_GB28181_SERVICE_CFG</td><td>6503</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.11 设置网络参数 NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.48[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.48  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.48 所示。  

表 5.48 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IpCondBuffer</td><td>IplnBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_GBT28181_SERVICE_CFG</td><td>设置GB28181服务器参数</td><td>NULL</td><td>NET_DVR_GB28181_SERVICE_CFG</td><td>6504</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.12 批量获取网络参数 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.49  

[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个  
[in] lpInBuffer 配置条件缓冲区，详见表 5.49  
[in] dwInBufferSize 缓冲区长度  
[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号  
[out] lpOutBuffer 设备返回的参数内容（详见表 5.49），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的  
[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.49 所示。  

表 5.49 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>lplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRGETCERT</td><td>获取证书信息</td><td>dwCount个NET_DVR_CERT_PARAM</td><td>dwCount个NET_DVR_CERT_INFO</td><td>6142</td></tr><tr><td>NETDVRGETFTPCFGV40</td><td>获取FTP信息</td><td>dwCount个NETDVRFTP_TYPE</td><td>dwCount个NET_DVR_FTPCFG_V406162</td><td></td></tr></table></body></html>  

#### 返回目录  

#### 5.19.13 批量设置网络参数 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.50[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.50[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.50），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的获取功能对应不同的结构体和命令号，如表 5.50 所示。  

表 5.50 参数批量设置  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>IplnBuffer对应结构体</td><td>IplnParamBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_FTPCFG_V40</td><td>设置FTP信息</td><td>dwCount个NET_DVR_FTP_TYPE</td><td>dwCount个NET_DVR_FTPCFG_V40</td><td>6163</td></tr></table></body></html>  

#### 5.19.14 获取 RTSP 协议参数 NET_DVR_GetRtspConfig  

函  数： BOOL  NET_DVR_GetRtspConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_RTSPCFGlpOutBuffer, DWORD dwOutBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 保留，置为 0[out]lpOutBuffer 输出缓存[in]dwOutBufferSize 存放输出数据的缓冲区大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.19.15 设置 RTSP 协议参数 NET_DVR_SetRtspConfig  

函  数： BOOL NET_DVR_SetRtspConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_RTSPCFGlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 保留，置为 0[in]lpInBuffer 输入缓存[in]dwOutBufferSize 输入缓存的大小，大小为结构体 NET_DVR_RTSPCFG 的大返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### IP 通道管理  

#### 5.19.16 获取设备的配置信息 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.51[in]lChannel 通道号，不同的命令对应不同的取值，如果该参数无效则置为0xFFFFFFFF 即可，详见表 5.51  

[out]lpOutBuffer 接收数据的缓冲指针，详见表 5.51[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.51 所示。  

 通道号是指设备视频通道号，通过注册设备（NET_DVR_Login_V30）返回的设备信息（NET_DVR_DEVICEINFO_V30）获取模拟通道个数（byChanNum）、模拟通道起始通道号（byStartChan）和设备支持的最大 IP 通道数（byIPChanNum+byHighDChanNum $^{*}256$ ）、数字通道起始通道号（byStartDChan）。  

表 5.51 IP 通道参数获取  


<html><body><table><tr><td>dwCommand 宏定义</td><td>dwCommand 含义</td><td>IChannel</td><td>IpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_IPPARACFG_V40</td><td>获取IP接入配置参数</td><td>组号，从ONET_DVR_IPPARACFG_V40 开始，每组 64个通道</td><td></td><td>1062</td></tr><tr><td>NET_DVR_GET_POE_CHANNEL_ADD_MODE</td><td>获取POE通道添加方式</td><td>通道号</td><td>NET_DVR_POE_CHANNEL_ADD_MODE</td><td>6124</td></tr><tr><td>NET_DVR_GET_DIGITAL_CHANNEL_STATE</td><td>获取设备数字通道状态</td><td>无效</td><td>NET_DVR_DIGITAL_CHANNEL_STATE</td><td>6126</td></tr><tr><td>NET_DVR_GET_IPALARMINCFG_V40</td><td>获取IP报警输入接入配 置参数</td><td>无效</td><td>NET_DVR_IPALARMINCFG_V40</td><td>6183</td></tr><tr><td>NET_DVR_GET_IPALARMOUTCFG_V40</td><td>获取IP报警输出接入配 置参数</td><td>无效</td><td>NET_DVR_IPALARMOUTCFG_V40</td><td>6185</td></tr><tr><td>NET_DVR_GET_DVR_SYNCHRONOUS_IPC</td><td>获取是否为前端 IPC 同通道号 步设备参数</td><td></td><td>NET_DVR_SYNCHRONOUS_IPC</td><td>6005</td></tr><tr><td>NET_DVR_GET_CUSTOM_PRO_CFG</td><td>获取自定义协议参数</td><td>协议序号， 从1开始</td><td>NET_DVR_CUSTOM_PROTOCAL</td><td>6116</td></tr><tr><td>NET_DVR_GET_DIGITAL_CHAN_SECURITY_STATUS</td><td>获取数字通道对应设备 安全状态</td><td>通道号</td><td>NET_DVR_DIGITAL_CHANNEL_SECURITY_STATUS 13001</td><td></td></tr></table></body></html>  

#### 5.19.17 设置设备的配置信息 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.52[in]lChannel 通道号，不同的命令对应不同的取值，如果该参数无效则置为0xFFFFFFFF 即可，详见表 5.52[in]lpInBuffer 输入数据的缓冲指针，详见表 5.52[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.52 所示。  

 通道号是指设备视频通道号，通过注册设备（NET_DVR_Login_V30）返回的设备信息（NET_DVR_DEVICEINFO_V30）获取模拟通道个数（byChanNum）、模拟通道起始通道号（byStartChan）和设备支持的最大 IP 通道数（byIPChanNum+byHighDChanNum $^{*}256$ ）、数字通道起始通道号（byStartDChan）。  

表 5.52 IP 通道参数设置  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IChannel</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_IPPARACFG_V40</td><td>设置IP接入配置参数</td><td>组号，从0开始，每 组64个通道</td><td>NET_DVR_IPPARACFG_V40</td><td>1063</td></tr><tr><td>NET_DVR_SET_POE_CHANNEL_ADD_MODE</td><td>设置POE通道添加方式</td><td>通道号</td><td>NET_DVR_POE_CHANNEL_ADD_MODE</td><td>6125</td></tr><tr><td>NET_DVR_SET_DVR_SYNCHRONOUS_IPC</td><td>设置是否为前端IPC同步 设备参数</td><td>通道号</td><td>NET_DVR_SYNCHRONOUS_IPC</td><td>6006</td></tr><tr><td>NET_DVR_SET_DVR_IPC_PASSWD</td><td>设置IPC用户名密码</td><td>通道号</td><td>NET_DVR_IPC_PASSWD</td><td>6008</td></tr><tr><td>NET_DVR_SET_DVR_IPC_NET</td><td>设置前端IPC的网络地址</td><td>通道号</td><td>NET_DVR_IPC_NETCFG</td><td>6012</td></tr><tr><td>NET_DVR_SET_CUSTOM_PRO_CFG</td><td>设置自定义协议参数</td><td>协议序号，从1开始</td><td>NET_DVR_CUSTOM_PROTOCAL</td><td>6117</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.18 设置设备的配置信息(标准协议)NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.53[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.53  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.53 所示。  

表 5.53 IP 通道设置  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>lpCondBuffer</td><td>lpOutBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_IPDEVICE_ACTIVATED</td><td>通过NVR激活前端设备</td><td>NULL</td><td>NET_DVR_IPDEVICE_ACTIVATE_CFG</td><td>13000</td></tr></table></body></html>  

#### 5.19.19 远程控制(标准协议)NET_DVR_STDControl  

函  数： BOOL NET_DVR_STDControl(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONTROLlpControlParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.54[in&out]lpControlParam 远程控制输入输出参数，不同的控制功能对应不同的输入输出参数，详见表 5.54  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通  

过错误码判断出错原因。  

#### 说  明：  

对于不同的配置功能（dwCommand），lpControlParam 中的 lpCondBuffer 对应不同的内容，如表5.54 所示。  

表 5.54 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>含义</td><td>lpCondBuffer对应结构体</td></tr><tr><td>NETDVRSYNCIPCPASSWD</td><td>6621</td><td>同步IPC密码与NVR一致</td><td>NULL</td></tr></table></body></html>  

 设备是否支持同步 IPC 密码功能，对应设备软硬件能力集(BasicCapability)中节点<isSupportSyncIPCPassword>，接口：NET_DVR_GetDeviceAbility(能力集类型：DEVICE_SOFTHARDWARE_ABILITY)。  

返回目录  

#### 5.19.20 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.55[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.56[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.56），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.56 所示。  

表 5.55 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_ACCESS_DEVICE_CHANNEL_INFO</td><td>获取待接入设备通道信息，dwCount为0</td><td>6165</td></tr></table></body></html>  

表 5.56 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_ACCESS_DEVICE_CHANNEL_INFO</td><td>NET_DVR_ACCESS_DEVICE_INFO</td><td>NET_DVR_ACCESS_DEVICE_CHANNEL_INFO</td></tr></table></body></html>  

#### 5.19.21 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V30 返回值[in] dwCommand 配置命令，详见表 5.57[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.57[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

[out] dwType 配置状态，详见表 5.58  
[out] lpBuffer dwType 状态为失败时的错误信息，不同的配置命令对应不同的结构体，详见表 5.58  
[out] dwBufLen 缓冲区大小  
[out] pUserData 用户数据  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 调用该接口实现长连接远程配置，如果 dwCommand 对应参数获取或者信息查询功能，该接口调用成功后，还需要调用 NET_DVR_GetNextRemoteConfig 接口来逐个获取对应内容。不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.57 所示。  

表 5.57 长连接参数配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>lplnBuffer对应结构</td><td>cbStateCallback</td></tr><tr><td>NET_DVR_IMPORT_IPC_CFG_FILE</td><td>6172</td><td>导入IPC配置文件</td><td>NET_DVR_IPC_CFG_FILE_PARAM</td><td>返回成功或失败相应的错误信息</td></tr><tr><td>NET_DVR_UPGRADE_IPC</td><td>6174</td><td>升级IP通道</td><td>NET_DVR_UPGRADE_IPC_PARAM</td><td>返回成功或失败相应的错误信息</td></tr></table></body></html>  

表 5.58 长连接回调数据  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwType</td><td>回调IpBuffer对应结构</td></tr><tr><td>NET_DVR_IMPORT_IPC_CFG_FILE</td><td rowspan="2">typedefenum{ NET_SDK_CALLBACK_STATUS_SUCCESS=1000,//成功 NET_SDK_CALLBACK_STATUS_PROCESSING,//处理中 NET_SDK_CALLBACK_STATUS_FAILED,//失败 NET_SDK_CALLBACK_STATUS_EXCEPTION,</td><td>dwType为1002时有效，对应： NET_DVR_IPC_CFG_FILE_ERR_INFO</td></tr><tr><td>NET_DVR_UPGRADE_IPC NET_SDK_CALLBACK_STATUS_LANGUAGE_MISMATCH, NET_SDK_CALLBACK_STATUS_DEV_TYPE_MISMATCH }NET_SDK_CALLBACK_STATUS_NORMAL;</td><td>dwType为1002时有效，对应： NET_DVR_UPGRADE_IPC_ERR_INFO I/(IPC配置文件导入)设备类型不匹配</td></tr></table></body></html>  

#### 5.19.22 关闭长连接配置 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。说  明： 关闭长连接配置接口所创建的句柄，释放资源。  

#### 5.19.23 远程扫描获取 IPC 信息列表 NET_DVR_GetSadpInfoList  

函  数： BOOL NET_DVR_GetSadpInfoList(LONG lUserID, LPNET_DVR_SADPINFO_LIST lpSadpInfoList)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[out]lpSadpInfoList IPC 信息列表结构  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

返回目录  

#### 5.19.24 远程修改 IPC 信息 NET_DVR_UpdateSadpInfo  

函  数： BOOL NET_DVR_UpdateSadpInfo(LONG lUserID, LPNET_DVR_SADP_VERIFY lpSadpVerify,LPNET_DVR_SADPINFO lpSadpInfo)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lpSadpVerify 校验信息[in]lpSadpInfo 修改的 IPC 信息列表结构  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.19.25 获取设备支持的 IPC 协议表 NET_DVR_GetIPCProtoList  

函  数： BOOL NET_DVR_GetIPCProtoList(LONG lUserID, LPNET_DVR_IPC_PROTO_LIST lpProtoList)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[out]lpProtoList IPC 协议列表结构  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口用于获取当前设备所支持的外接 IPC 的协议。  

### 报警输入输出配置  

#### 5.19.26 获取设备参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.59 所示。  

表 5.59 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_ALARMINCFG_V40</td><td>获取报警输入参数</td><td>报警输入号，从0开始</td><td>NET_DVR_ALARMINCFG_V40</td><td>6181</td></tr><tr><td>NET_DVR_GET_ALARMOUTCFG_V30</td><td>获取报警输出参数</td><td>报警输出号，从0开始</td><td>NET_DVR_ALARMOUTCFG_V30</td><td>1026</td></tr><tr><td>NET_DVR_GET_ALARMIN_HOLIDAY_HANDLE</td><td>获取报警输入假日 报警处理方式</td><td>报警输入号，从0开始</td><td>NETDVRHOLIDAYHANDLE</td><td>1248</td></tr><tr><td>NETDVRGETALARMOUTHOLIDAYHANDLE</td><td>获取报警输出假日 报警处理方式</td><td>报警输出号，从0开始</td><td>NETDVRHOLIDAYHANDLE</td><td>1250</td></tr></table></body></html>  

#### 5.19.27 设置设备参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.60 所示。  

表 5.60 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_ALARMINCFG_V40</td><td>设置报警输入参数</td><td>报警输入号，从0开始</td><td>NET_DVR_ALARMINCFG_V40</td><td>6182</td></tr><tr><td>NET_DVR_SET_ALARMOUTCFG_V30</td><td>设置报警输出参数</td><td>报警输出号，从0开始</td><td>NET_DVR_ALARMOUTCFG_V30</td><td>1027</td></tr><tr><td>NET_DVR_SET_ALARMIN_HOLIDAY_HANDLE</td><td>设置报警输入假日 报警处理方式</td><td>报警输入号，从0开始</td><td>NETDVRHOLIDAYHANDLE</td><td>1249</td></tr><tr><td>NET_DVRSETALARMOUT_HOLIDAY_HANDLE</td><td>设置报警输出假日 报警处理方式</td><td>报警输出号，从0开始</td><td>NETDVRHOLIDAYHANDLE</td><td>1251</td></tr></table></body></html>  

#### 5.19.28 获取设备报警输出 NET_DVR_GetAlarmOut_V30  

函  数： BOOL  NET_DVR_GetAlarmOut_V30(LONG lUserID, LPNET_DVR_ALARMOUTSTATUS_V30lpAlarmOutState)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[out]lpAlarmOutState 报警输出状态  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.19.29 设置设备报警输出 NET_DVR_SetAlarmOut  

函  数： BOOL  NET_DVR_SetAlarmOut(LONG lUserID, LONG lAlarmOutPort,LONG lAlarmOutStatic)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]lAlarmOutPort 报警输出口。初始输出口从 0 开始， $0{\times}00\dag\mathbf{f}$ 表示全部模拟输出，0xff00 表示全部数字输出。[in]lAlarmOutStatic 报警输出状态：0- 停止输出，1- 输出  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 本地输出(预览)参数配置  

#### 5.19.30 获取设备参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可  

[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.61 所示。  

表 5.61 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRGETPREVIEWCFGV30</td><td>获取设备本地主CVBS输出预览参数</td><td>无效</td><td>NETDVRPREVIEWCFGV30</td><td>1044</td></tr><tr><td>NET_DVRGET_PREVIEWCFGAUXV30</td><td>获取设备本地HDMI或辅CVBS输出预无效 览参数</td><td></td><td>NETDVRPREVIEWCFG_V30</td><td>1046</td></tr><tr><td>NET_DVR_GET_VGA_PREVIEWCFG</td><td>获取设备本地VGA预览配置参数</td><td>无效</td><td>NET_DVR_PREVIEWCFG_V30</td><td>1284</td></tr><tr><td>NET_DVR_GET_VIDEOOUTCFG_V30</td><td>获取视频输出参数</td><td>无效</td><td>NET_DVR_VIDEOOUT_V30</td><td>1028</td></tr><tr><td>NET_DVR_GET_AUXOUTCFG</td><td>获取报警触发辅助输出参数</td><td>无效</td><td>NETDVRAUXOUTCFG</td><td>140</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.31 设置设备参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.62 所示。  

表 5.62 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_PREVIEWCFG_V30</td><td>设置设备本地主CVBS输出预览参数</td><td>无效</td><td>NET_DVRPREVIEWCFG_V30</td><td>1045</td></tr><tr><td>NET_DVR_SET_PREVIEWCFG_AUX_V30</td><td>设置设备本地HDMI或辅CVBS输出预无效 览参数</td><td></td><td>NET_DVR_PREVIEWCFG_V30</td><td>1047</td></tr><tr><td>NET_DVR_SET_VGA_PREVIEWCFG</td><td>设置设备本地VGA预览配置参数</td><td>无效</td><td>NET_DVR_PREVIEWCFG_V30</td><td>1285</td></tr><tr><td>NET_DVR_SET_VIDEOOUTCFG_V30</td><td>设置视频输出参数</td><td>无效</td><td>NET_DVR_VIDEOOUT_V30</td><td>1029</td></tr><tr><td>NETDVRSETAUXOUTCFG</td><td>设置报警触发辅助输出参数</td><td>无效</td><td>NETDVRAUXOUTCF</td><td>141</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.32 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.63[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.63[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.63），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.63 所示。  

表 5.63 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>含义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_PREVIEW_SWITCH_CFG</td><td>获取设备本地预览切 换参数，dwCount为0</td><td>NETDVRPREVIEWSWITCHCOND</td><td>NET_DVR_PREVIEW_SWITCH_CFG</td><td>6166</td></tr></table></body></html>  

#### 5.19.33 批量设置配置信息 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.64[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.64[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，  

[in] lpInParamBuffer  

参数值：0 或者 1 表示成功，其他值为失败对应的错误号  
需要设置给设备的参数内容（详见表 5.64），和 lpInBuffer 一一对  
应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应  
的 lpInBuffer 设置失败，为 0 则设置成功  
设置内容缓冲区大小  

[in] dwInParamBufferSize  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的设置功能对应不同的结构体和命令号，如表 5.64 所示。  

表 5.64 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_PREVIEW_SWITCH_CFG</td><td>设置设备本地预览切 换参数，dwCount为0</td><td>NET_DVR_PREVIEW_SWITCH_COND</td><td>NET_DVR_PREVIEW_SWITCH_CFG</td><td>6167</td></tr></table></body></html>  

#### 5.19.34 获取视频输出缩放信息 NET_DVR_GetScaleCFG_V30  

函  数： BOOL NET_DVR_GetScaleCFG(LONG lUserID, LPNET_DVR_SCALECFG pScalecfg)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[out]pScalecfg 缩放参数信息  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.19.35 设置视频输出缩放参数 NET_DVR_SetScaleCFG_V30  

函  数： BOOL NET_DVR_SetScaleCFG_V30(LONG lUserID, LPNET_DVR_SCALECFG pScalecfg)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]pScalecfg 缩放参数配置结构体  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 用户和安全参数配置  

#### 5.19.36 获取设备参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[out]lpOutBuffer 接收数据的缓冲指针[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.65 所示。  

表 5.65 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRGETUSERCFGV50</td><td>获取用户参数(支 持密码确认)</td><td>组号，从0开始，每组32个用户</td><td>NETDVRUSERV50</td><td>6246</td></tr><tr><td>NETDVRGETUSERCFGV40</td><td>获取用户参数</td><td>组号，从0开始，每组32个用户</td><td>NETDVRUSERV40</td><td>6187</td></tr><tr><td>NETDVRGETSECURITYCFG</td><td>获取安全认证配置</td><td>无效</td><td>NET_DVR_SECURITY_CFG</td><td>147</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.37 设置设备参数 NET_DVR_SetDVRConfig  

函  数： BOOL  NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，参见配置命令[in]lChannel 通道号，如果命令不需要通道号，该参数无效，置为 0xFFFFFFFF即可[in]lpInBuffer 输入数据的缓冲指针[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.66 所示。  

表 5.66 设置设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRSETUSERCFG_V50</td><td>设置用户参数(支 持密码确认)</td><td>组号，从0开始，每组32个用户</td><td>NETDVRUSERV50</td><td>6247</td></tr><tr><td>NET_DVR_SET_USERCFG_V40</td><td>设置用户参数</td><td>组号，从0开始，每组32个用户</td><td>NETDVRUSERV40</td><td>6188</td></tr><tr><td>NETDVRSETSECURITYCFG</td><td>设置安全认证配置</td><td>无效</td><td>NET_DVRSECURITY_CFG</td><td>148</td></tr></table></body></html>  

#### 5.19.38 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.67[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.67[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.67），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.67 所示。  

表 5.67 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>含义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRGETUSERRIGHTCFG</td><td>获取用户权限，dwCount为1</td><td>NETDVRUSERCOND</td><td>NETDVRUSERRIGHTCFG</td><td>6210</td></tr></table></body></html>  

#### 返回目录  

#### 5.19.39 批量设置配置信息 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.68[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详表 5.68[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号  

[in] lpInParamBuffer  

需要设置给设备的参数内容（详见表 5.68），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功  

[in] dwInParamBufferSize 设置内容缓冲区大小返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的设置功能对应不同的结构体和命令号，如表 5.68 所示。  

表 5.68 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_USER_RIGHT_CFG</td><td>设置用户权限，dwCount为1</td><td>NETDVRUSERCOND</td><td>NETDVRUSERRIGHTCFG</td><td>6211</td></tr></table></body></html>  

#### 5.19.40 远程控制 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.69[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.69[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，详见表 5.69。  

表 5.69 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET_DVR_UNLOCK_USER</td><td>146</td><td>用户解锁</td><td>NET_DVR_UNLOCK_INFO</td></tr></table></body></html>  

返回目录  

#### 5.19.41 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V30 返回值[in] dwCommand 配置命令，详见表 5.70[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.70[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

[out] dwType 配置状态  
[out] lpBuffer 存放数据的缓冲区指针，具体内容跟 dwCommand、dwType 相关  
[out] dwBufLen 缓冲区大小  
[out] pUserData 用户数据  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 调用该接口启动长连接远程配置后，还需要调用其他接口获取、设置相关参数或获取状态，如表 5.71 所示。  

表 5.70 长连接参数配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构</td><td>cbStateCallback</td></tr><tr><td>NET_DVR_GET_LOCKED_INFO_LIST</td><td>149</td><td>获取所有被锁定信息</td><td>NULL</td><td>NULL</td></tr></table></body></html>  

表 5.71 后续接口调用  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>后续接口调用</td></tr><tr><td>NETDVRGETLOCKEDINFOLIST</td><td>获取所有被锁定信息</td><td>NET_DVR_GetNextRemoteConfig</td></tr></table></body></html>  

返回目录  

#### 5.19.42 逐个获取查找到的信息 NET_DVR_GetNextRemoteConfig  

函  数： LONG NET_DVR_GetNextRemoteConfig(LONG lHandle, void \*lpOutBuff, DWORD dwOutBuffSize)参  数： [in] lHandle 查找句柄，NET_DVR_StartRemoteConfig 的返回值[out] lpOutBuff 输出数据缓冲区，与 NET_DVR_StartRemoteConfig 的命令（dwCommand）有关，详见表 5.73[out] dwOutBuffSize 缓冲区长度  

返回值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.72。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

表 5.72 长连接参数获取状态  


<html><body><table><tr><td>宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_SUCCESS</td><td>1000</td><td>成功读取到数据，处理完本次数据后需要再次调用 NET_DVR_GetNextRemoteConfig获取下一条数据</td></tr><tr><td>NET_SDK_GET_NETX_STATUS_NEED_WAIT</td><td>1001</td><td>需等待设备发送数据，继续调用 NET_DVR_GetNextRemoteConfig</td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_FINISH</td><td>1002</td><td>数据全部取完，可调用NET_DVR_StopRemoteConfig 结束长连接</td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_FAILED</td><td>1003</td><td>出现异常，可调用NET_DVR_StopRemoteConfig 结束长 连接</td></tr></table></body></html>  

说  明： 在调用该接口获取查找之前，必须先调用 NET_DVR_StartRemoteConfig 得到当前的查找句柄。此接口用于获取一条已查找到的信息，若要获取全部的已查找到的信息，需要循环调用此接口。调用 NET_DVR_StartRemoteConfig 时传入不同的命令号(dwCommand)，lpOutBuff 对应不同的结构体，如表 5.73 所示。  

表 5.73 长连接参数获取  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td></tr><tr><td>NETDVRGETLOCKEDINFOLIST</td><td>149</td><td>获取所有被锁定信息</td><td>NETDVRLOCKEDINFO</td></tr></table></body></html>  

#### 5.19.43 关闭长连接配置 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 关闭长连接配置接口所创建的句柄，释放资源。  

#### 更多参数配置  

#### 5.19.44 获取设备参数 NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.74[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.74  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.74所示。  

表 5.74 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>lpCondBuffer</td><td>IpOutBuffer</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_ACCESSORY_CARD_INFO</td><td>获取配件板信息</td><td>NULL</td><td>NET_DVR_ACCESSORY_CARD_INFO</td><td>6710</td></tr></table></body></html>  

### 5.20 SMART 参数配置  

#### SMART 参数配置  

#### 5.20.1 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.75[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.76[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.76），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.76 所示。  

表 5.75 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_VCA_DETION_CFG</td><td>获取智能移动参数配置</td><td>5041</td></tr><tr><td>NET_DVR_GET_GUARDCFG</td><td>获取车牌识别检测计划</td><td>3134</td></tr><tr><td>NET_DVR_GET_TRAVERSE_PLANE_DETECTION</td><td>获取越界侦测配置</td><td>3360</td></tr><tr><td>NET_DVR_GET_FIELD_DETECTION</td><td>获取区域侦测配置</td><td>3362</td></tr><tr><td>NET_DVR_GET_SMD_HOLIDAY_HANDLE</td><td>获取简易智能假日计划</td><td>6194</td></tr></table></body></html>  

表 5.76 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_VCA_DETION_CFG</td><td>dwCount个NET_DVR_CHANNEL_GROUP</td><td>dwCount个NET_DVR_VCA_DETION_CFG</td></tr><tr><td>NETDVRGETGUARDCFG</td><td>dwCount个 NET_DVR_GUARD_COND</td><td>dwCount 个 NET_DVR_GUARD_CFG</td></tr><tr><td>NET_DVR_GET_SCENECHANGE_DETECTIONCFG</td><td>dwCount个NET_DVR_CHANNEL_GROUP</td><td>dwCount个NET_VCA_TRAVERSE_PLANE_DETECTION</td></tr><tr><td>NETDVRGETTRAVERSEPLANEDETECTION</td><td>dwCount个NET_DVR_CHANNEL_GROUP</td><td>dwCount个NET_VCA_FIELDDETECION</td></tr><tr><td>NET_DVR_GET_SMD_HOLIDAY_HANDLE</td><td>dwCount个NET_DVR_HOLIDAY_HANDLE_COND</td><td>dwCount个NET_DVR_HOLIDAY_HANDLE</td></tr></table></body></html>  

#### 返回目录  

#### 5.20.2 批量设置配置信息 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.77[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.78[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.78），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的设置功能对应不同的结构体和命令号，如表 5.78 所示。  

表 5.77 参数批量设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_VCA_DETION_CFG</td><td>设置智能移动参数配置</td><td>5040</td></tr><tr><td>NET_DVRSET_GUARDCFG</td><td>设置车牌识别检测计划</td><td>3135</td></tr><tr><td>NET_DVR_SET_TRAVERSE_PLANE_DETECTION</td><td>设置越界侦测配置</td><td>3361</td></tr><tr><td>NET_DVR_SET_FIELD_DETECTION</td><td>设置区域侦测配置</td><td>3363</td></tr><tr><td>NET_DVR_SET_SMD_HOLIDAY_HANDLE</td><td>设置简易智能假日计划</td><td>6195</td></tr></table></body></html>  

表 5.78 批量设置设备参数  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>IplnParamBuffer对应结构体</td></tr><tr><td>NET_DVR_SET_VCA_DETION_CFG</td><td>dwCount个NET_DVR_CHANNEL_GROUP</td><td>dwCount个NET_DVR_VCA_DETION_CFG</td></tr><tr><td>NETDVRSETGUARDCFG</td><td>dwCount 个 NET_DVR_GUARD_COND</td><td>dwCount 个 NET_DVR_GUARD_CFG</td></tr><tr><td>NET_DVR_SET_SCENECHANGE_DETECTIONCFG</td><td>dwCount个 NET_DVR_CHANNEL_GROUP</td><td>dwCount个NET_VCA_TRAVERSE_PLANE_DETECTION</td></tr><tr><td>NETDVRSETTRAVERSEPLANEDETECTION</td><td>dwCount个NET_DVR_CHANNEL_GROUP</td><td>dwCount个NET_VCA_FIELDDETECION</td></tr><tr><td>NET_DVR_SET_SMD_HOLIDAY_HANDLE</td><td>dwCount个NET_DVR_HOLIDAY_HANDLE_COND</td><td>dwCount个NET_DVR_HOLIDAY_HANDLE</td></tr></table></body></html>  

#### 返回目录  

#### 5.20.3 获取设备的配置信息(标准协议)NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.79[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.79  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中 lpCondBuffer、lpOutBuffer 分别对应不同的内容，具体如表 5.79所示。  

表 5.79 参数获取配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td><td>IpCondBuffer IpOutBuffer</td><td></td></tr><tr><td>NETDVRGETVEHICLEBLACKLSTSCHEDULE</td><td>获取非授权名单布防时间配 置</td><td>6622</td><td>NULL</td><td>BlackListScheduleList (XML描述)</td></tr><tr><td>NETDVRGETVEHICLEBLACKLISTEVENTTRIGGER</td><td>获取非授权名单布防联动配 置</td><td>6626</td><td>NULL</td><td>EventTrigger(XML描述）</td></tr><tr><td>NETDVRGETVEHICLEWHITELSTSCHEDULE</td><td>获取授权名单布防时间配置</td><td>6624</td><td>NULL</td><td>WhiteListScheduleList (XML描述)</td></tr><tr><td>NET_DVR_GET_VEHICLE_WHITELIST_EVENT_TRIGGER</td><td>获取授权名单布防联动配置</td><td>6628</td><td>NULL</td><td>EventTrigger(XML描述）</td></tr></table></body></html>

返回目录  

#### 5.20.4 设置设备的配置信息(标准协议)NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.80[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.80  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.80 所示。  

表 5.80 设置参数配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td><td>IpCondBuffer</td><td>IplnBuffer</td></tr><tr><td>NET_DVRSET_VEHICLE_BLACKLST_SCHEDULE</td><td>设置非授权名单布防时间 配置</td><td>6623</td><td>NULL</td><td>BlackListScheduleList (XML描述)</td></tr><tr><td>NET_DVRSET_VEHICLE_BLACKLIST_EVENT_TRIGGER</td><td>获取非授权名单布防联动 配置</td><td>6627</td><td>NULL</td><td>EventTrigger(XML描述）</td></tr><tr><td>NET_DVRSETVEHICLEWHITELSTSCHEDULE</td><td>设置授权名单布防时间配6625 置</td><td></td><td>NULL</td><td>WhiteListScheduleList (XML描述)</td></tr><tr><td>NET_DVRSETVEHICLEWHITELISTEVENTTRIGGER</td><td>获取授权名单布防联动配6629 置</td><td></td><td>NULL</td><td>EventTrigger(XML描述）</td></tr></table></body></html>  

#### 5.20.5 设备参数配置(透传)NET_DVR_STDXMLConfig  

函  数： BOOL NET_DVR_STDXMLConfig(LONG lUserID, NET_DVR_XML_CONFIG_INPUT \*lpInputParam,NET_DVR_XML_CONFIG_OUTPUT \*lpOutputParam)  

参  数： [in] lUserID 登录主控板，NET_DVR_Login_V40 返回值[in] lpInputParam 输入参数，详见表 5.81[out] lpOutputParam 输出参数，详见表 5.81  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  通过该接口可以直接透传 ISAPI 协议命令，实现参数配置、能力集等功能。调用该接口需要设备支持 ISAPI 协议（PUT、GET、POST、DELETE 等命令），不同功能对应不同的输入输出参数，具体内容可以参考 ISAPI 协议文档。  

表 5.81 设备参数配置  


<html><body><table><tr><td>功能描述</td><td>IplnputParam->lpRequestUrl</td><td>IplnputParam->lplnBuffer</td><td>lpOutputParam->lpOutBuffer</td></tr><tr><td>获取功能互斥信息</td><td>GET/ISAPl/System/mutexFunctionErrorMsg</td><td>NULL</td><td>MutexFunctionErrorMsg</td></tr></table></body></html>  

#### VQD 视频质量诊断  

#### 5.20.6 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand,  DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.82[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.83[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.83），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.83 所示。  

表 5.82 VQD 参数获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_VQD_LOOP_DIAGNOSE_CFG</td><td>获取VQD循环诊断配置参数</td><td>6406</td></tr></table></body></html>  

表 5.83 VQD 参数获取结构  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>IpOutBuffer对应结构体</td></tr><tr><td>NET DVR GET_VQD_LOOP DIAGNOSE CFG</td><td>dwCount 个</td><td>dwCount 个</td></tr><tr><td></td><td>NET DVR RCHANNEL GROUP</td><td>NET DVR_VQD_LOOP DIAGNOSE CFG</td></tr><tr><td></td><td></td><td></td></tr></table></body></html>  

#### 返回目录  

#### 5.20.7 批量设置配置信息 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID,DWORD dwCommand,DWORD dwCount,LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，参见表 5.84[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.85[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号  

[in] lpInParamBuffer  

需要设置给设备的参数内容（详见表 5.85），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功  
设置内容缓冲区大小  

[in] dwInParamBufferSize  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的获取功能对应不同的结构体和命令号，如表 5.85 所示。  

表 5.84 VQD 参数设置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_VQD_LOOP_DIAGNOSE_CFG</td><td>设置VQD循环诊断配置参数</td><td>6407</td></tr></table></body></html>  

表 5.85 VQD 参数设置结构  


<html><body><table><tr><td>dwCommand</td><td>IplnBuffer对应结构体</td><td>IplnParamBuffer对应结构体</td></tr><tr><td>NETDVRSETVQDLOOPDIAGNOSECFG</td><td>dwCount个NET_DVR_CHANNEL_GROUP</td><td>dwCount个NET_DVR_VQD_LOOP_DIAGNOSE_CFG</td></tr></table></body></html>  

#### 5.20.8 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V30 返回值[in] dwCommand 配置命令，详见表 5.86[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.86[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

[out] dwType 配置状态  
[out] lpBuffer 存放数据的缓冲区指针，具体内容跟 dwType 相关，详见表 5.87  
[out] dwBufLen 缓冲区大小  
[out] pUserData 用户数据  

返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。  

说  明： 接口中不同的控制功能对应不同的命令号(dwCommand)，同时 lpInBuffer 对应不同的结构体，如表 5.87 所示。  

表 5.86 VQD 长连接配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_VQD_DIAGNOSE_INFO</td><td>6408</td><td>手动获取VQD诊断信息</td><td>通道号（DWORD 类型)数组</td></tr></table></body></html>  

表 5.87 长连接回调数据  


<html><body><table><tr><td>dwType</td><td>值</td><td>含义</td><td>IpBuffer对应内容</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_STATUS</td><td>0</td><td>状态值</td><td>typedefenum NET_SDK_CALLBACK_STATUS_SUCCESS=1000,//成功 NET_SDK_CALLBACK_STATUS_PROCESSING,//处理中 NET_SDK_CALLBACK_STATUS_FAILED//失败</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_PROGRESS</td><td>1</td><td>进度值</td><td>NET_SDK_CALLBACK_STATUS_NORMAL; lpBuffer的值表示进度</td></tr><tr><td>NET_SDK_CALLBACK_TYPE_DATA</td><td>2</td><td>信息数据</td><td>lpBuffer的值表示信息数据</td></tr></table></body></html>  

调用该接口实现长连接远程配置，如果 dwCommand 对应参数获取或者信息查询功能，该接口调用成功后，还需要调用 NET_DVR_GetNextRemoteConfig 接口来逐个获取对应内容。  

#### 5.20.9 逐个获取查找到的信息 NET_DVR_GetNextRemoteConfig  

函  数： LONG NET_DVR_GetNextRemoteConfig(LONG lHandle, void \*lpOutBuff, DWORD dwOutBuffSize)  

参  数： [in] lHandle 查找句柄，NET_DVR_StartRemoteConfig 的返回值[out] lpOutBuff 输出数据缓冲区，与 NET_DVR_StartRemoteConfig 的命令（dwCommand）有关，详见表 5.89[out] dwOutBuffSize 缓冲区长度  

返回值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.88。获取错误码调用NET_DVR_GetLastError。  

表 5.88 长连接参数获取状态  


<html><body><table><tr><td>宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_SUCCESS</td><td>1000</td><td>成功读取到数据，处理完本次数据后需要再次调用 NET_DVR_GetNextRemoteConfig获取下一条数据</td></tr><tr><td>NET_SDK_GET_NETX_STATUS_NEED_WAIT</td><td>1001</td><td>需等待设备发送数据，继续调用 NET_DVR_GetNextRemoteConfig</td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_FINISH</td><td>1002</td><td>数据全部取完，可调用NET_DVR_StopRemoteConfig 结束长连接</td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_FAILED</td><td>1003</td><td>出现异常，可调用NET_DVR_StopRemoteConfig 结束长 连接</td></tr></table></body></html>  

说  明： 调用 NET_DVR_StartRemoteConfig 时传入不同的命令号(dwCommand)，lpOutBuff 对应不同的结构体，如表 5.89 所示。在调用该接口获取查找之前，必须先调用 NET_DVR_StartRemoteConfig得到当前的查找句柄。此接口用于获取一条已查找到的信息，若要获取全部的已查找到的信息，需要循环调用此接口。  

表 5.89 长连接参数获取  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td></tr><tr><td>NET_DVR_GET_VQD_DIAGNOSE_INFO</td><td>6408</td><td>手动获取VQD诊断信息</td><td>NET_DVR_VQD_DIAGNOSE_INFO</td></tr></table></body></html>  

#### 返回目录  

#### 5.20.10 关闭长连接配置接口所创建的句柄，释放资源  

NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值返回值： TRUE 表示成功，FALSE 表示失败。获取错误码调用 NET_DVR_GetLastError。  

说  明：  

### 5.21 存储管理  

#### 存储参数配置  

#### 5.21.1 获取设备的配置信息 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.90[in]lChannel 通道号，不同的命令对应不同的取值，如果该参数无效则置为0xFFFFFFFF 即可，详见表 5.91[out]lpOutBuffer 接收数据的缓冲指针，详见表 5.91[in]dwOutBufferSize 接收数据的缓冲长度(以字节为单位)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.91 所示。  

表 5.90 参数获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_NFSCFG</td><td>获取NFS（网络文件系统）参数</td><td>230</td></tr><tr><td>NET_DVR_GET_HDCFG</td><td>获取硬盘管理参数</td><td>1054</td></tr><tr><td>NET_DVR_GET_HDCFG_V40</td><td>获取硬盘管理参数</td><td>6122</td></tr><tr><td>NET_DVR_GET_HDGROUP_CFG_V40</td><td>获取盘组管理参数</td><td>6192</td></tr><tr><td>NET_DVR_GET_NET_DISKCFG</td><td>获取网络硬盘接入参数</td><td>1038</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_GET_DISK_QUOTA_CFG</td><td>获取磁盘配额信息</td><td>1278</td></tr><tr><td>NET_DVR_GET_DISK_RAID_INFO</td><td>获取磁盘Raid信息</td><td>6001</td></tr><tr><td>NET_DVR_GET_DRAWFRAME_DISK_QUOTA_CFG</td><td>获取抽帧通道磁盘配额</td><td>6109</td></tr><tr><td>NET_DVR_GET_ESATA_MINISAS_USAGE_CFG</td><td>获取eSATA和miniSAS用途</td><td>6120</td></tr><tr><td>NET_DVR_GET_HD_STATUS</td><td>获取硬盘状态</td><td>6170</td></tr><tr><td>NET_DVR_GET_RAID_BACKGROUND_TASK_SPEED</td><td>获取RAID后台任务速度</td><td>6175</td></tr><tr><td>NET_DVR_GET_RECORD_PACK</td><td>获取录像打包参数</td><td>6301</td></tr><tr><td>NET_DVR_GET_CLOUD_STORAGE_CFG</td><td>获取云存储工作模式</td><td>6303</td></tr></table></body></html>  

表 5.91 获取设备参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>IChannel 取值</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NET_DVR_GET_NFSCFG</td><td>无效</td><td>NET_DVR_NFSCFG</td></tr><tr><td>NET_DVR_GET_HDCFG</td><td>无效</td><td>NET_DVR_HDCFG</td></tr><tr><td>NET_DVR_GET_HDCFG_V40</td><td>组号，从0开始，每组33个硬 盘</td><td>NET_DVR_HDCFG</td></tr><tr><td>NET_DVR_GET_HDGROUP_CFG_V40</td><td>组号，从0开始，每组16个硬 盘组</td><td>NET_DVR_HDGROUP_CFG_V40</td></tr><tr><td>NET_DVR_GET_NET_DISKCFG</td><td>无效</td><td>NET_DVR_NET_DISKCFG</td></tr><tr><td>NET_DVR_GET_DISK_QUOTA_CFG</td><td>通道号</td><td>NET_DVR_DISK_QUOTA_CFG</td></tr><tr><td>NET_DVR_GET_DISK_RAID_INFO</td><td>无效</td><td>NET_DVR_DISK_RAID_INFO</td></tr><tr><td>NET_DVR_GET_DRAWFRAME_DISK_QUOTA_CFG</td><td>无效</td><td>NET_DVR_DRAWFRAME_DISK_QUOTA_CFG</td></tr><tr><td>NET_DVR_GET_ESATA_MINISAS_USAGE_CFG</td><td>无效</td><td>NET_DVR_ESATA_MINISAS_USAGE</td></tr><tr><td>NET_DVR_GET_HD_STATUS</td><td>无效</td><td>NET_DVR_HD_STATUS</td></tr><tr><td>NET_DVR_GET_RAID_BACKGROUND_TASK_SPEED</td><td>无效</td><td>NET_DVR_RAID_BTS_CFG</td></tr><tr><td>NET_DVR_GET_RECORD_PACK</td><td>无效</td><td>NET_DVR_RECORD_PACK</td></tr><tr><td>NET_DVR_GET_CLOUD_STORAGE_CFG</td><td>无效</td><td>NET_DVR_CLOUD_STORAGE_CFG</td></tr></table></body></html>  

#### 5.21.2 设置设备的配置信息 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.92[in]lChannel 通道号，不同的命令对应不同的取值，如果该参数无效则置为0xFFFFFFFF 即可，详见表 5.93[in]lpInBuffer 输入数据的缓冲指针，详见表 5.93[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.93 所示。  

表 5.92 参数设置命令  


<html><body><table><tr><td>dwCommand 宏定义</td><td>dwCommand 含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_NFSCFG</td><td>设置NFS（网络文件系统）参数</td><td>231</td></tr><tr><td>NET_DVR_SET_HDCFG</td><td>设置硬盘管理参数</td><td>1055</td></tr><tr><td>NET_DVR_SET_HDCFG_V40</td><td>设置硬盘管理参数</td><td>6123</td></tr><tr><td>NET_DVR_SET_HDGROUP_CFG_V40</td><td>设置盘组管理参数</td><td>6193</td></tr><tr><td>NET_DVR_SET_NET_DISKCFG</td><td>设置网络硬盘接入参数</td><td>1039</td></tr><tr><td>NET_DVR_SET_DISK_QUOTA_CFG</td><td>设置磁盘配额信息</td><td>1279</td></tr><tr><td>NET_DVR_SET_DISK_RAID_INFO</td><td>设置磁盘 Raid 信息</td><td>6002</td></tr><tr><td>NET_DVR_SET_DRAWFRAME_DISK_QUOTA_CFG</td><td>设置抽帧通道磁盘配额</td><td>6110</td></tr><tr><td>NET_DVR_SET_ESATA_MINISAS_USAGE_CFG</td><td>设置eSATA和miniSAS用途</td><td>6121</td></tr><tr><td>NET_DVR_SET_HD_STATUS</td><td>设置硬盘状态</td><td>6171</td></tr><tr><td>NET_DVR_SET_RAID_BACKGROUND_TASK_SPEED</td><td>设置 RAID后台任务速度</td><td>6176</td></tr><tr><td>NET_DVR_SET_RECORD_PACK</td><td>设置录像打包参数</td><td>6302</td></tr><tr><td>NET_DVR_SET_CLOUD_STORAGE_CFG</td><td>设置云存储工作模式</td><td>6304</td></tr></table></body></html>  

表 5.93 设置设备参数  


<html><body><table><tr><td>dwCommand 宏定义</td><td>IChannel 取值</td><td>IplnBuffer对应结构体</td></tr><tr><td>NET_DVR_SET_NFSCFG</td><td>无效</td><td>NET_DVR_NFSCFG</td></tr><tr><td>NET_DVR_SET_HDCFG</td><td>无效</td><td>NET_DVR_HDCFG</td></tr><tr><td>NET_DVR_SET_HDCFG_V40</td><td>组号，从0开始，每组33个 硬盘</td><td>NET_DVR_HDCFG</td></tr><tr><td>NET_DVR_SET_HDGROUP_CFG_V40</td><td>组号，从0开始，每组 16个NET_DVR_HDGROUP_CFG_V40 硬盘组</td><td></td></tr><tr><td>NET_DVR_SET_NET_DISKCFG</td><td>无效</td><td>NET_DVR_NET_DISKCFG</td></tr><tr><td>NET_DVR_SET_DISK_QUOTA_CFG</td><td>通道号</td><td>NET_DVR_DISK_QUOTA_CFG</td></tr><tr><td>NET_DVR_SET_DISK_RAID_INFO</td><td>无效</td><td>NET_DVR_DISK_RAID_INFO</td></tr><tr><td>NET_DVR_SET_DRAWFRAME_DISK_QUOTA_CFG</td><td>无效</td><td>NET_DVR_DRAWFRAME_DISK_QUOTA_CFG</td></tr><tr><td>NET_DVR_SET_ESATA_MINISAS_USAGE_CFG</td><td>无效</td><td>NET_DVR_ESATA_MINISAS_USAGE</td></tr><tr><td>NET_DVR_SET_HD_STATUS</td><td>无效</td><td>NET_DVR_HD_STATUS</td></tr><tr><td>NET_DVR_SET_RAID_BACKGROUND_TASK_SPEED</td><td>无效</td><td>NET_DVR_RAID_BTS_CFG</td></tr><tr><td>NET_DVR_SET_RECORD_PACK</td><td>无效</td><td>NET_DVR_RECORD_PACK</td></tr><tr><td>NET_DVR_SET_CLOUD_STORAGE_CFG</td><td>无效</td><td>NET_DVR_CLOUD_STORAGE_CFG</td></tr></table></body></html>  

#### 5.21.3 远程控制 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.94[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.94[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，详见表 5.94。  

表 5.94 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NETDVRMOUNT DISK</td><td>6015</td><td>加载磁盘</td><td>NETDVRMOUNT DISKPARAM</td></tr><tr><td>NETD DVR RUNMOUNT DISK</td><td>6016</td><td>卸载磁盘</td><td>NET DVRMOUNT DISKPARAM</td></tr><tr><td>NETDVR DELINVALIDDISK</td><td>6107</td><td>删除无效磁盘</td><td>NET DVRINVALID DISKPARAM</td></tr></table></body></html>  

#### 返回目录  

#### 硬盘格式化  

#### 5.21.4 远程格式化设备硬盘 NET_DVR_FormatDisk  

函  数： LONG NET_DVR_FormatDisk(LONG lUserID,LONG lDiskNumber)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lDiskNumber 硬盘号，从 0 开始，0xff 表示对所有硬盘有效（不包括只读硬盘）  
返回值： -1 表示失败，其他值作为 NET_DVR_CloseFormatHandle 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 格式化过程中如果网络断了，设备上的格式化操作依然会继续，但是客户端无法收到状态。  

返回目录  

#### 5.21.5 获取格式化硬盘的进度 NET_DVR_GetFormatProgress  

函  数： BOOL NET_DVR_GetFormatProgress(LONG lFormatHandle, LONG \*pCurrentFormatDisk,LONG\*pCurrentDiskPos,LONG \*pFormatStatic)  

参  数： [in]lFormatHandle 格式化硬盘句柄，NET_DVR_FormatDisk 的返回值[out]pCurrentFormatDisk 指向保存当前正在格式化的硬盘号的指针，硬盘号从 0 开始，-1为初始状态[out] pCurrentDiskPos 指向保存当前正在格式化的硬盘的进度的指针，进度是 $0{\sim}100$ [out] FormatStatic 指向保存硬盘格式化状态的指针：0-正在格式化；1-硬盘全部格式化完成；2-格式化当前硬盘出错，不能继续格式化此硬盘，本地和网络硬盘都会出现此错误；3-由于网络异常造成网络硬盘丢失而不能开始格式化当前硬盘  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通  

过错误码判断出错原因。  

说  明：  

#### 5.21.6 关闭格式化硬盘句柄，释放资源 NET_DVR_CloseFormatHandle  

函  数： BOOL NET_DVR_CloseFormatHandle(LONG lFormatHandle)  
参  数： [in]lFormatHandle 格式化硬盘句柄，NET_DVR_FormatDisk 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### NAS 目录查询  

#### 5.21.7 启动长连接远程配置 NET_DVR_StartRemoteConfig  

函  数： LONG NET_DVR_StartRemoteConfig(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer,DWORD dwInBufferLen, fRemoteConfigCallback cbStateCallback, LPVOID pUserData)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V30 返回值[in] dwCommand 配置命令，详见表 5.95[in] lpInBuffer 输入参数，具体内容跟配置命令相关，详见表 5.95[in] dwInBufferLen 输入缓冲的大小[in] cbStateCallback 状态回调函数[in] pUserData 用户数据  

typedef void(CALLBACK \*fRemoteConfigCallback)(DWORD dwType, void \*lpBuffer, DWORDdwBufLen, void \*pUserData)  

[out] dwType 配置状态  
[out] lpBuffer dwType 状态为失败时的错误信息，不同的配置命令对应不同的结构体，详见表 5.95  
[out] dwBufLen 缓冲区大小  
[out] pUserData 用户数据  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 调用该接口实现长连接远程配置，如果 dwCommand 对应参数获取或者信息查询功能，该接口调用成功后，还需要调用 NET_DVR_GetNextRemoteConfig 接口来逐个获取对应内容。不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，如表 5.95 所示。  

表 5.95 长连接参数配置  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构</td><td>cbStateCallback</td></tr><tr><td rowspan="2">NET_DVR_FIND_NAS_DIRECTORY</td><td rowspan="2">6161</td><td rowspan="2">查找NAS目录</td><td rowspan="2">NET_DVR_NET_DISK_SERACH_PARAM</td><td>NULL，获取状态请调用</td></tr><tr><td>NETDVR_GetRemoteConfigState</td></tr></table></body></html>  

#### 5.21.8 逐个获取查找到的信息 NET_DVR_GetNextRemoteConfig  

函  数： LONG NET_DVR_GetNextRemoteConfig(LONG lHandle, void \*lpOutBuff, DWORD dwOutBuffSize)参  数： [in] lHandle 查找句柄，NET_DVR_StartRemoteConfig 的返回值[out] lpOutBuff 输出数据缓冲区，与 NET_DVR_StartRemoteConfig 的命令（dwCommand）有关，详见表 5.97[out] dwOutBuffSize 缓冲区长度  

返回值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.96。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

表 5.96 长连接参数获取状态  


<html><body><table><tr><td>宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>NETSDKGETNEXTSTATUSSUCCESS</td><td>1000</td><td>成功读取到数据，处理完本次数据后需要再次调用 NET_DVR_GetNextRemoteConfig获取下一条数据</td></tr><tr><td>NET_SDK_GET_NETX_STATUS_NEED_WAIT</td><td>1001</td><td>需等待设备发送数据，继续调用 NET_DVR_GetNextRemoteConfig</td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_FINISH</td><td>1002</td><td>数据全部取完，可调用NET_DVR_StopRemoteConfig 结束长连接</td></tr><tr><td>NET_SDK_GET_NEXT_STATUS_FAILED</td><td>1003</td><td>出现异常，可调用NET_DVR_StopRemoteConfig 结束长 连接</td></tr></table></body></html>  

说  明： 调用 NET_DVR_StartRemoteConfig 时传入不同的命令号(dwCommand)，lpOutBuff 对应不同的结构体，如表 5.97 所示。在调用该接口获取查找之前，必须先调用 NET_DVR_StartRemoteConfig 得到当前的查找句柄。此接口用于获取一条已查找到的信息，若要获取全部的已查找到的信息，需要循环调用此接口。  

表 5.97 长连接参数获取  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer</td></tr><tr><td>NETDVRFINDNASDIRECTORY</td><td>6161</td><td>查找NAS目录</td><td>NET_DVR_NET_DISKSERACH_RET</td></tr></table></body></html>  

#### 5.21.9 获取长连接配置的状态 NET_DVR_GetRemoteConfigState  

函  数： BOOL NET_DVR_GetRemoteConfigState(LONG lHandle, void \*pState)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值[out] pState 返回的状态值，不同的配置命令对应不同的状态取值，详见表5.98  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说明：调用 NET_DVR_StartRemoteConfig 时传入不同的命令号(dwCommand),pState 对应不同的取值,如表 5.98 所示。  

表 5.98 长连接配置状态  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_FIND_NAS_DIRECTORY</td><td>6161</td><td>查找NAS目录</td></tr><tr><td>pState状态宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_SDK_CALLBACK_STATUS_SUCCESS</td><td>1000</td><td>查找成功</td></tr><tr><td>NET_SDK_CALLBACKSTATUS_PROCESSING</td><td>1001</td><td>处理中</td></tr><tr><td>NET_SDK_CALLBACK_STATUS_FAILED</td><td>1002</td><td>查找失败</td></tr></table></body></html>  

#### 5.21.10 关闭长连接配置 NET_DVR_StopRemoteConfig  

函  数： BOOL NET_DVR_StopRemoteConfig(LONG lHandle)  
参  数： [in] lHandle 句柄，NET_DVR_StartRemoteConfig 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 关闭长连接配置接口所创建的句柄，释放资源。  

#### IP SAN 文件目录查找  

#### 5.21.11 查找 IPSAN 文件目录 NET_DVR_FindIpSanDirectory  

函  数： LONG NET_DVR_FindIpSanDirectory(LONG lUserID, LPNET_DVR_IPSAN_SERACH_PARAMlpIpsanSearchParam)  
参  数： [in] lUserID NET_DVR_Login_V40 的返回值[in] lpIpsanSearchParam IPSAN 文件目录查找参数，包括 IPSAN 的 IP 地址和端口  
返回值： -1 表示失败，其他值作为 NET_DVR_FindNextDirectory 等接口的句柄。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口指定了要查找的 IPSAN，调用成功后，就可以调用 NET_DVR_FindNextDirectory 接口来逐个获取该 IPSAN 的目录信息。  

#### 5.21.12 逐个获取查找到的目录信息 NET_DVR_FindNextDirectory  

函  数： LONG NET_DVR_FindNextDirectory(LONG lFindHandle, LPNET_DVR_IPSAN_SERACH_RET lpFindData)  
参  数： [in] lFindHandle 查找句柄，NET_DVR_FindIpSanDirectory 的返回值[out] lpFindData 保存文件目录信息的指针  
返回 值： -1 表示失败，其他值表示当前的获取状态等信息，详见表 5.99。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

表 5.99 查找状态信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NET_DVR_FILE_SUCCESS</td><td>1000</td><td>获取目录信息成功</td></tr><tr><td>NET_DVR_FILE_NOFIND</td><td>1001</td><td>未查找到目录</td></tr><tr><td>NET_DVR_ISFINDING</td><td>1002</td><td>正在查找请等待</td></tr><tr><td>NET_DVR_NOMOREFILE</td><td>1003</td><td>没有更多的目录，查找结束</td></tr><tr><td>NET_DVR_FILE_EXCEPTION</td><td>1004</td><td>查找目录时异常</td></tr></table></body></html>  

说  明： 在调用该接口获取查找目录之前，必须先调用NET_DVR_FindIpSanDirectory得到当前的查找句柄。此接口用于获取一条已查找到的目录信息，若要获取全部的已查找到的目录信息，需要循环调用此接口。  

#### 5.21.13 停止 IPSAN 文件目录搜索，释放资源 NET_DVR_FindDirectoryClose  

函  数： BOOL NET_DVR_FindDirectoryClose(LONG lFindHandle)  
参  数： [in] lFindHandle 查找句柄，NET_DVR_FindIpSanDirectory 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 第三方云功能  

#### 5.21.14 获取设备能力集(标准协议) NET_DVR_GetSTDAbility  

函  数： BOOL NET_DVR_GetSTDAbility(LONG lUserID, DWORD dwAbilityType, LPNET_DVR_STD_ABILITYlpAbilityParam)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwAbilityType 能力类型，具体定义见表 5.100[in&out]lpAbilityParam 设备能力集参数（包括输入和输出参数）  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.100 获取设备能力集  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td><td>IpCondBuffer</td><td>lpOutBuffer</td></tr><tr><td>NET_DVR_GET_CLOUD_URL_CAP</td><td>6507</td><td>获取云存储URL能力集</td><td>NULL</td><td>CloudURL</td></tr><tr><td>NETDVRGETCLOUDCFG_CAP</td><td>6510</td><td>获取云存储配置能力集</td><td>NULL</td><td>Cloud</td></tr><tr><td>NET_DVR_GET_CLOUDSTORAGE_UPLOADSTRATEGY_CAP</td><td>6513</td><td>获取云存储上传策略配置 能力集</td><td>NULL</td><td>UploadStrategy</td></tr></table></body></html>  

#### 5.21.15 获取设备的配置信息(标准协议)NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.101[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.102  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam中lpCondBuffer、lpOutBuffer分别对应不同的内容，具体如表 5.102所示。  

表 5.101 参数获取配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NETDVRGETCLOUDURL</td><td>获取云存储URL</td><td>6506</td></tr><tr><td>NETDVRGETCLOUD_CFG</td><td>获取云存储配置参数</td><td>6508</td></tr><tr><td>NETDVRGETCLOUDUPLOADSTRATEGY</td><td>获取云存储上传策略</td><td>6511</td></tr></table></body></html>  

表 5.102 获取第三方云参数  


<html><body><table><tr><td>dwCommand宏定义</td><td>IpCondBuffer</td><td>lpOutBuffer</td></tr><tr><td>NET TDVRGETCLOUDURL</td><td>NETDVRCLOUDURLCOND</td><td>NETDVRCLOUDURL</td></tr><tr><td>NET DVR_GET_CLOUD_CFG</td><td>NULL</td><td>NET DVR_CLOUD_CFG</td></tr><tr><td>NET DVRGETCLOUDUPLOADSTRATEGY</td><td>NETDVRCLOUD UPLOADSTRATEGYCOND</td><td>NETDVRCLOUDUPLOADSTRATEGY</td></tr></table></body></html>  

#### 返回目录  

#### 5.21.16 设置设备的配置信息(标准协议)NET_DVR_SetSTDConfig  

函  数： BOOL NET_DVR_SetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.103[in&out]lpConfigParam 配置输入输出参数，不同的配置功能对应不同的输入输出参数，详见表 5.104  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 设置配置参数时，lpConfigParam 结构体里面的 lpOutBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam 中的 lpCondBuffer、lpInBuffer 分别对应不同的内容，具体如表 5.104 所示。  

表 5.103 设置参数配置命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET DVR_SET_CLOUD_CFG</td><td>设置云存储配置参数</td><td>6509</td></tr><tr><td>NETD DVR_SET_CLOUD_UPLOADSTRATEGY</td><td>设置云存储上传策略</td><td>6512</td></tr></table></body></html>  

表 5.104 设置第三方云参数  


<html><body><table><tr><td>dwCommand 宏定义</td><td>IpCondBuffer</td><td>IplnBuffer</td></tr><tr><td>NET DVR_SET_C CLOUD_CFG</td><td>NULL</td><td>NET DVR_CLOUD_CFG</td></tr><tr><td>NET DVR_SET_CLOUD_UPLOADSTRATEGY</td><td>NET_D DVR_CLOUD_UPLOADSTRATEGY_COND</td><td>NET DVR_CLOUD_UPLOADSTRATEGY</td></tr></table></body></html>  

#### 返回目录  

### 5.22零通道预览和配置  

#### 参数配置  

#### 5.22.1 获取设备的配置信息 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.105[in]lChannel 设备只有一个零通道，其中通道号设为1[out]lpOutBuffer 接收数据的缓冲指针，详见表 5.105[in]dwOutBufferSize 接收数据的缓冲长度(单位：字节)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.105 所示。  

表 5.105 零通道相关参数获取  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>IChannel取值</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRGETZEROCHANCFG</td><td>获取零通道压缩参数</td><td>通道号</td><td>NETDVRZEROCHANCFG</td><td>1102</td></tr><tr><td>NET DVR_GET_Z ZEROPREVIEWCFG_V30</td><td>获取零通道本地预览参数</td><td>通道号</td><td>NET DVRPREVIEWCFGV30</td><td>1104</td></tr><tr><td>NETDVRGETZEROZOOM</td><td>获取零通道缩放参数</td><td>通道号</td><td>NETDVRZEROZOOMCFG</td><td>1107</td></tr></table></body></html>  

#### 返回目录  

#### 5.22.2 设置设备的配置信息 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  

[in]dwCommand 设备配置命令，详见表 5.106[in]lChanne 设备只有一个零通道，其中通道号设为1[in]lpInBuffer 输入数据的缓冲指针，详见表 5.106[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.106 所示。  

表 5.106 零通道相关参数设置  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand 含义</td><td>通道号</td><td>lplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRSET ZEROCHANCFG</td><td>设置零通道压缩参数</td><td>通道号</td><td>NETDVRZEROCHANCFG</td><td>1103</td></tr><tr><td>NET_DVR_SET_ZERO_PREVIEWCFG_V30</td><td>设置零通道本地预览参数</td><td>通道号</td><td>NET_DVR R_PREVIEWCFG_V30</td><td>1105</td></tr><tr><td>NET_DVR_SET_ZERO_ZOOM</td><td>设置零通道缩放参数</td><td>通道号</td><td>NETDVRZEROZOOMCFG</td><td>1106</td></tr></table></body></html>  

#### 返回目录  

#### 实时预览  

#### 5.22.3 开启零通道预览 NET_DVR_ZeroStartPlay  

函  数： LONG NET_DVR_ZeroStartPlay(LONG lUserID, LPNET_DVR_CLIENTINFO lpClientInfo,fRealDataCallBack_V30 cbRealDataCallBack, void\* pUser, BOOL bBlocked)  

参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值[in]lpClientInfo 预览参数（设备只有一个零通道，其中通道号设为1）[in]cbRealDataCallBack 码流数据回调函数[in]pUser 用户数据[in]bBlocked 请求码流过程是否阻塞：0- 否，1- 是  

typedef void(CALLBACK \*fRealDataCallBack_V30)(LONG lRealHandle, DWORD dwDataType, BYTE \*pBuffer, DWORD dwBufSize, void \*pUser)  

[out]lRealHandle 当前的预览句柄[out]dwDataType 数据类型，详见表 5.107[out]pBuffer 存放数据的缓冲区指针[out]dwBufSize 缓冲区大小[out]pUser 用户数据  

表 5.107 码流数据类型  


<html><body><table><tr><td>dwDataType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>NETDVRSYSHEAD</td><td>1</td><td>系统头数据</td></tr><tr><td>NET DVRSTREAMDATA</td><td>乙</td><td>流数据 居（包括复合流或音视频分开的视频流数据）</td></tr><tr><td>NETDVRAUDIOSTREAMDATA</td><td>3</td><td>音频数据</td></tr></table></body></html>  

返回值： -1 表示失败，其他值作为 NET_DVR_ZeroStopPlay 等函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口中可以设置当前预览操作是否阻塞（通过 bBlocked 参数设置）。若设为不阻塞，表示发起与设备的连接就认为连接成功，如果发生码流接收失败、播放失败等情况以预览异常的方式通知上层。若设为阻塞，表示直到播放操作完成才返回成功与否。  

该接口中的回调函数可以置为空，此时该函数将不回调码流数据给用户，但用户仍可以通过接口 NET_DVR_SetRealDataCallBack 或 NET_DVR_SetStandardDataCallBack 注册捕获码流数据的回调函数以捕获码流数据。  

#### 5.22.4 停止预览 NET_DVR_ZeroStopPlay  

函  数： BOOL NET_DVR_ZeroStopPlay(LONG lPlayHandle)  
参  数： [in]lRealHandle NET_DVR_RealPlay_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

返回目录  

#### 其他功能  

#### 5.22.5 零通道产生一个关键帧 NET_DVR_ZeroMakeKeyFrame  

函  数： BOOL NET_DVR_ZeroMakeKeyFrame(LONG lUserID, LONG lZeroChan)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lZeroChan 零通道号，加上起始通道号（即从 1 开始）  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

返回目录  

#### 5.22.6 零通道预览画面翻页 NET_DVR_ZeroTurnOver  

函  数： BOOL NET_DVR_ZeroTurnOver(LONG lUserID, LONG lChannel, BOOL bNextPreview)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 零通道号，加上起始通道号（即从 1 开始）[in]bNextPreview 向下或向上翻页：TRUE-下一页；FALSE-上一页  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.23POS 功能接口  

#### 获取能力集  

#### 5.23.1 获取设备能力集 NET_DVR_GetDeviceAbility  

函  数： BOOL  NET_DVR_GetDeviceAbility(LONG lUserID, DWORD dwAbilityType, char\* pInBuf, DWORD  

dwInLength, char\* pOutBuf, DWORD dwOutLength)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwAbilityType 能力集类型，具体定义见表 5.109。[in] pInBuf 输入缓冲区指针（按照设备规定的能力参数的描述方式组合，可以是 XML 文本或结构体形式，详见表 5.109）[in]dwInLength 输入缓冲区的长度[out]pOutBuf 输出缓冲区指针（按照设备规定的能力集的描述方式，可以是XML 文本或结构体形式，详见表 5.109）[in]dwOutLength 接收数据的缓冲区的长度  

表 5.108 设备能力集类型  


<html><body><table><tr><td>dwAbilityType宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>DEVICEABILITYINFO</td><td>0x011</td><td>设备通用能力类型，具体能力根据发送的能力节点来区分</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取设备能力集时，需要输入参数和输出参数的格式定义如表 5.109 所示。  

表 5.109 设备能力集描述  


<html><body><table><tr><td>dwAbilityType宏定义</td><td>plnBuf</td><td>pOutBuf</td></tr><tr><td>DEVICEABILITYINFO</td><td>获取POS能力集输入描述</td><td>POS能力集(POSAbility)</td></tr></table></body></html>

注：能力集结构和 XML 描述请参见《设备网络 SDK 使用手册.chm》  

#### 参数配置  

#### 5.23.2 获取 POS 相关参数 NET_DVR_GetDVRConfig  

函  数： BOOL NET_DVR_GetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpOutBuffer, DWORD dwOutBufferSize, LPDWORD lpBytesReturned)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.110[in]lChannel 通道号，不同的命令对应不同的取值，如果该参数无效则置为0xFFFFFFFF 即可，详见表 5.110[out]lpOutBuffer 接收数据的缓冲指针，详见表 5.110[in]dwOutBufferSize 接收数据的缓冲长度(单位：字节)，不能为 0[out]lpBytesReturned 实际收到的数据长度指针，不能为 NULL  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.110 所示。  

表 5.110 POS 参数获取  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>IChannel取值</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NETDVRGETPOSFILTERCFG</td><td>获取POS过滤规则</td><td>规则ID号，从1开始</td><td>NETDVRPOSFILTERCFG</td><td>6148</td></tr><tr><td>NETDVRGETCONNECTPOSCFG</td><td>获取DVR与POS连接方式</td><td>规则ID号,从1开始</td><td>NETDVRCONNECTPOSCFG</td><td>6150</td></tr></table></body></html>  

#### 5.23.3 设置 POS 相关参数 NET_DVR_SetDVRConfig  

函  数： BOOL NET_DVR_SetDVRConfig(LONG lUserID, DWORD dwCommand,LONG lChannel, LPVOIDlpInBuffer, DWORD dwInBufferSize)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]dwCommand 设备配置命令，详见表 5.111[in]lChanne 通道号，不同的命令对应不同的取值，如果该参数无效则置为0xFFFFFFFF 即可，详见表 5.111[in]lpInBuffer 输入数据的缓冲指针，详见表 5.111[in]dwInBufferSize 输入数据的缓冲长度(以字节为单位)  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的获取功能对应不同的结构体和命令号，如表 5.111 所示。  

表 5.111 POS 参数设置  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>通道号</td><td>IplnBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVRSET_POS_FILTER_CFG</td><td>设置POS过滤规则</td><td>规则ID号，从1开始</td><td>NET_DVR_POS_FILTER_CFG</td><td>6149</td></tr><tr><td>NETDVRSETCONNECTPOSCFG</td><td>设置DVR与POS连接方式</td><td>规则ID号，从1开始</td><td>NETDVRCONNECTPOSCFG</td><td>6151</td></tr></table></body></html>  

#### 返回目录  

#### 5.23.4 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.112[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.112[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.112），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.112 所示。  

表 5.112 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_CHAN_FILTER_CFG</td><td>获取规则与通道关联 信息，dwCount为1</td><td>NET_DVR_CHANNEL_GROUP</td><td>NET_DVR_CHAN_FILTER_CFG</td><td>6152</td></tr></table></body></html>  

#### 5.23.5 批量设置配置信息 NET_DVR_SetDeviceConfig  

函  数： BOOL NET_DVR_SetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize, LPVOID lpStatusList, LPVOID lpInParamBuffer, DWORDdwInParamBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.113[in] dwCount 一次要设置的配置参数个数，0 和 1 都表示 1 个，2 表示 2 个，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.113[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要设置的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[in] lpInParamBuffer 需要设置给设备的参数内容（详见表 5.113），和 lpInBuffer 一一对应。如果某个配置对应的 lpStatusList 信息为大于 0 值，表示对应的 lpInBuffer 设置失败，为 0 则设置成功[in] dwInParamBufferSize 设置内容缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量设置子设备配置信息的通用接口，lpInBuffer 指定需要设置哪dwCount 个，lpInParamBuffer 是设置 dwCount 个配置的参数信息。不同的设置功能对应不同的结构体和命令号，如表 5.113 所示。  

表 5.113 参数批量获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>lplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVR_SET_CHAN_FILTER_CFG</td><td>设置规则与通道关联 信息，dwCount为1</td><td>NET_DVR_CHANNEL_GROUP</td><td>NET_DVR_CHAN_FILTER_CFG</td><td>6153</td></tr></table></body></html>  

### 5.24透明通道  

#### 5.24.1 建立透明通道 NET_DVR_SerialStart  

函  数： LONG NET_DVR_SerialStart(LONG lUserID, LONG lSerialPort, fSerialDataCallBackcbSerialDataCallBack, DWORD dwUser)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lSerialPort 串口号：1- 232 串口；2- 485 串口[in]cbSerialDataCallBack 透明通道数据回调函数[in]dwUser 用户数据  

typedef void(CALLBACK \*fSerialDataCallBack)(LONG lSerialHandle, char \*pRecvDataBuffer, DWORD dwBufSize, DWORD dwUser)  

[out]lSerialHandle NET_DVR_SerialStart 的返回值  
[out]pRecvDataBuffer 存放数据的缓冲区指针  
[out]dwBufSize 数据大小  
[out]dwUser 用户数据  

返回值： -1 表示失败，其他值作为 NET_DVR_SerialSend 等函数的句柄参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 需要从回调函数得到数据解码器必须支持数据回传，否则发送成功，回调依然不会有返回。  

返回目录  

#### 5.24.2 通过透明通道向设备串口发送数据 NET_DVR_SerialSend  

函  数： BOOL NET_DVR_SerialSend(LONG lSerialHandle, LONG lChannel, char \*pSendBuf,DWORD dwBufSize)  
参  数： [in]lSerialHandle NET_DVR_SerialStart 的返回值[in]lChannel 使用 485 串口时有效，从 1 开始；232 串口作为透明通道时该值设置为 0[in]pSendBuf 发送数据的缓冲区指针[in]dwBufSize 缓冲区的大小，最多 1016 字节  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.24.3 断开透明通道 NET_DVR_SerialStop  

函  数： BOOL NET_DVR_SerialStop (LONG lSerialHandle)  
参  数： [in]lSerialHandle NET_DVR_SerialStart 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.25向串口发送数据  

#### 5.25.1 直接向串口发送数据，不需要建立透明通道 NET_DVR_SendToSerialPort  

函  数： BOOL NET_DVR_SendToSerialPort(LONG lUserID, DWORD dwSerialPort, DWORD dwSerialIndex, char\*pSendBuf, DWORD dwBufSize)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  

[in]dwSerialPort 串口类型：1-232，2-485[in]dwSerialIndex 表示第几个 232 或者 485，从 1 开始[in]pSendBuf 发送数据的缓冲区指针[in]dwBufSize 缓冲区的大小，最多 1016 字节  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.25.2 直接向 232 串口发送数据，不需要建立透明通道 NET_DVR_SendTo232Port  

函  数： BOOL NET_DVR_SendTo232Port(LONG lUserID, char \*pSendBuf, DWORD dwBufSize)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]pSendBuf 发送数据的缓冲区指针[in]dwBufSize 缓冲区的大小，最多 1016 字节  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.26远程控制设备手动录像  

#### 5.26.1 远程手动启动设备录像 NET_DVR_StartDVRRecord  

函  数： BOOL NET_DVR_StartDVRRecord(LONG lUserID,LONG lChannel,LONG lRecordType)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号： $0{\times}00{\dagger}\mathbf{f}$ 表示所有模拟通道，0xff00 表示所有数字通道，0xffff 表示所有模拟和数字通道[in]lRecordType 录像类型：0- 手动，1- 报警，2- 回传，3- 信号，4- 移动，5- 遮挡  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 录像类型设置需要设备支持，不支持默认为手动录像。  

当某通道已经开启定时录像的前提下首次开启手动录像，此次操作未生效，仍保持定时录像状态，且查询设备状态（见 NET_DVR_GetDVRWorkState_V30 和 NET_DVR_GetDVRWorkState；结构体 NET_DVR_WORKSTATE_V30 和 NET_DVR_WORKSTATE）中的录像状态仍为录像；此时关闭手动录像，停止了定时录像，且查询录像状态为不录像；第二次开启手动录像，此时手动录像开始；停止手动录像后，重启设备，定时录像重新打开。  

#### 5.26.2 远程手动停止设备录像 NET_DVR_StopDVRRecord  

函  数： BOOL NET_DVR_StopDVRRecord(LONG lUserID,LONG lChannel)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lChannel 通道号： $0{\times}00{\dagger}\mathbf{f}$ 表示所有模拟通道，0xff00 表示所有数字通道，0xffff 表示所有模拟和数字通道  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.26.3 远程控制 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.114[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.114[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 不同的控制功能对应不同的命令号，同时 lpInBuffer 对应不同的结构体，详见表 5.114。  

表 5.114 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NETDVRCMDTRIGGERPERIOD_RECORD</td><td>6144</td><td>外部命令触发录像</td><td>NETDVRCMDTRIGGERPERIODRECORDPARA</td></tr></table></body></html>  

### 5.27 远程面板控制  

#### 5.27.1 远程控制面板上的按键 NET_DVR_ClickKey  

函  数： BOOL NET_DVR_ClickKey(LONG lUserID, LONG lKeyIndex)参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lKeyIndex 面板上的按键，详见表 5.115  

表 5.115 远程控制面板按键  


<html><body><table><tr><td>IKeylndex 宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>KEY_CODE_1</td><td>1</td><td>按钮1</td></tr><tr><td>KEY_CODE_2</td><td>2</td><td>按钮2</td></tr><tr><td>KEY_CODE_3</td><td>3</td><td>按钮3</td></tr></table></body></html>  

<html><body><table><tr><td>KEY_CODE_4</td><td>4</td><td>按钮4</td></tr><tr><td>KEY_CODE_5</td><td>5</td><td>按钮5</td></tr><tr><td>KEY_CODE_6</td><td>6</td><td>按钮6</td></tr><tr><td>KEY_CODE_7</td><td>7</td><td>按钮7</td></tr><tr><td>KEY_CODE_8</td><td>8</td><td>按钮8</td></tr><tr><td>KEY_CODE_9</td><td>6</td><td>按钮9</td></tr><tr><td>KEY_CODE_0</td><td>10</td><td>按钮0</td></tr><tr><td>KEY_CODE_POWER</td><td>11</td><td>POWER</td></tr><tr><td>KEY_CODE_MENU</td><td>12</td><td>MENU</td></tr><tr><td>KEY_CODE_ENTER</td><td>13</td><td>ENTER</td></tr><tr><td>KEY_CODE_CANCEL</td><td>14</td><td>ESCS</td></tr><tr><td>KEY_CODE_UP/KEY_PTZ_UP_START</td><td>15</td><td>"上"或者"云台上开始"或者云台上开始</td></tr><tr><td>KEY_CODE_DOWN/KEY_PTZ_DOWN_START</td><td>16</td><td>"下"或者"云台下开始"或者云台下开始</td></tr><tr><td>KEY_CODE_LEFT/KEY_PTZ_LEFT_START</td><td>17</td><td>"左"或者"云台左开始"或者云台左开始</td></tr><tr><td>KEY_CODE_RIGHT/KEY_PTZ_RIGHT_START</td><td>18</td><td>"右"或者"云台右开始"或者云台右开始</td></tr><tr><td>KEY_CODE_EDIT/KEY_PTZ_AP1_START</td><td>19</td><td>"EDIT"或者"光圈+开始"</td></tr><tr><td>KEY_CODE_ADD</td><td>20</td><td>增加</td></tr><tr><td>KEY_CODE_MINUS</td><td>21</td><td>减小</td></tr><tr><td>KEY_CODE_PLAY</td><td>22</td><td>"PLAY"</td></tr><tr><td>KEY_CODE_REC</td><td>23</td><td>"REC"</td></tr><tr><td>KEY_CODE_PAN/KEY_PTZ_AP2_START</td><td>24</td><td>"PAN"或者"光圈-开始"</td></tr><tr><td>KEY_CODE_M/KEY_PTZ_FOCUS2_START</td><td>25</td><td>"多画面"或者"聚焦-开始"</td></tr><tr><td>KEY_CODE_A/KEY_PTZ_FOCUS1_START</td><td>26</td><td>"输入法"或者"聚焦+开始"</td></tr><tr><td>KEY_CODE_F1</td><td>27</td><td>"对讲"</td></tr><tr><td>KEY_CODE_F2</td><td>28</td><td>"系统信息"</td></tr><tr><td>KEY_PTZ_UP_STOP</td><td>32</td><td>"云台上结束"</td></tr><tr><td>KEY_PTZ_DOWN_STOP</td><td>33</td><td>"云台下结束"</td></tr><tr><td>KEY_PTZ_LEFT_STOP</td><td></td><td>"云台左结束"</td></tr><tr><td>KEY_PTZ_RIGHT_STOP</td><td>35</td><td>"云台右结束"</td></tr><tr><td>KEY_PTZ_AP1_STOP</td><td>36</td><td>"光圈+结束"</td></tr><tr><td>KEY_PTZ_AP2_STOP</td><td>37</td><td>"光圈-结束"</td></tr><tr><td>KEY_PTZ_FOCUS1_STOP</td><td>38</td><td>"聚焦+结束"</td></tr><tr><td>KEY_PTZ_FOCUS2_STOP</td><td>39</td><td>"聚焦-结束"</td></tr><tr><td>KEY_PTZ_B1_START</td><td>40</td><td>"变倍+开始"</td></tr><tr><td>KEY_PTZ_B1_STOP</td><td>41</td><td>"变倍+结束"</td></tr></table></body></html>  

<html><body><table><tr><td>KEY_PTZ_B2_START</td><td>42</td><td>'变倍-开始"</td></tr><tr><td>KEY_PTZ_B2_STOP</td><td>43</td><td>'变倍-结束"</td></tr><tr><td>KEY_CODE_11</td><td>44</td><td>按钮11</td></tr><tr><td>KEY_CODE_12</td><td>45</td><td>按钮12</td></tr><tr><td>KEY_CODE_13</td><td>46</td><td>按钮13</td></tr><tr><td>KEY_CODE_14</td><td>47</td><td>按钮14</td></tr><tr><td>KEY_CODE_15</td><td>48</td><td>按钮15</td></tr><tr><td>KEY_CODE_16</td><td>49</td><td>按钮16</td></tr></table></body></html>

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.27.2 禁用设备本地面板控制 NET_DVR_LockPanel  

函  数： BOOL NET_DVR_LockPanel(LONG lUserID)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.27.3 恢复设备本地面板控制 NET_DVR_UnLockPanel  

函  数： BOOL NET_DVR_UnLockPanel(LONG lUserID))  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.28码流加密  

#### 5.28.1 设置设备码流加密密钥 NET_DVR_InquestStreamEncrypt  

函  数： BOOL NET_DVR_InquestStreamEncrypt(LONG lUserID, LONG lChannel, BOOL   bEncrypt)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in] lChannel 通道号[in] bEncrypt 加密标记：TRUE-加密；FALSE-不加密  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

#### 说  明：  

#### 5.28.2 获取设备码流加密状态 NET_DVR_InquestGetEncryptState  

函  数： BOOL NET_DVR_InquestGetEncryptState(LONG lUserID, LONG lChannel, BOOL \*bEncrypt)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in] lChannel 通道号[out] bEncrypt 加密标记：TRUE-加密；FALSE-不加密  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.29 邮件测试  

#### 5.29.1 测试按已配置的 EMAIL 参数能否收发成功 NET_DVR_StartEmailTest  

函  数： LONG NET_DVR_StartEmailTest(LONG lUserID)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值  
返回值： -1 表示失败，其他值作为 NET_DVR_GetEmailTestProcess 、NET_DVR_StopEmailTest 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 在调用此接口测试前，需要配置相关的 EMAIL 参数，详见 NET_DVR_GetDVRConfig、NET_DVR_SetDVRConfig 的网络应用参数（EMAIL）配置。  

#### 5.29.2 获取邮件测试的进度 NET_DVR_GetEmailTestProgress  

函  数： BOOL NET_DVR_GetEmailTestProgress(LONG lEmailTestHandle, DWORD\* pState)  

参  数： [in]lEmailTestHandle NET_DVR_StartEmailTest 的返回值[out]pState 邮件测试的进度，进度值的取值范围（0,100），其他值定义如表5.116 所示。  

表 5.116 邮件测试进度  


<html><body><table><tr><td>pState 宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>PROCESSING</td><td>0</td><td>正在处理</td></tr><tr><td>PROCESS_SUCCESS</td><td>100</td><td>过程完成</td></tr><tr><td>PROCESS_EXCEPTION</td><td>400</td><td>过程异常</td></tr><tr><td>PROCESS_FAILED</td><td>500</td><td>过程失败</td></tr></table></body></html>  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.29.3 停止邮件测试 NET_DVR_StopEmailTest  

函  数： BOOL  NET_DVR_StopEmailTest(LONG lEmailTestHandle)  
参  数： [in]lEmailTestHandle NET_DVR_StartEmailTest 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.30文件上传下载  

#### 5.30.1 上传文件 NET_DVR_UploadFile_V40  

函  数： LONG NET_DVR_UploadFile_V40(LONG lUserID, DWORD dwUploadType, LPVOID lpInBuffer, DWORDdwInBufferSize, char \*sFileName, LPVOID lpOutBuffer, DWORD dwOutBufferSize)  

参  数： [in] lUserID NET_DVR_Login_V40 的返回值[in] dwUploadType 上传文件类型，详见表 5.117[in] lpInBuffer 不同的 dwUploadType，输入参数不同，详见表 5.117[in] dwInBufferSize 输入缓冲区大小[in] \*sFileName 上传文件的绝对路径（包括文件名），最多 128 字节，文件名最多32 字节（含最后的'\0'）[out] lpOutBuffer 输出参数。不同的 dwUploadType，输出参数不同，具体参见下文列表[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.117 文件上传类型  


<html><body><table><tr><td>dwUploadType宏定义</td><td>宏定义值</td><td>dwUploadType含义</td><td>IplnBuffer对应结构体</td><td>IpOutBuffer对应结构体</td></tr><tr><td>UPLOADCERTIFICATE</td><td>1</td><td>上传证书</td><td>NETDVRCERTPARAM</td><td></td></tr><tr><td>UPLOADRECORDFILE</td><td>4</td><td>上传录像文件(云存 储模式)</td><td>NETDVRUPLOADRECORDINFO</td><td>NETDVRUPLOADFILERET</td></tr><tr><td>UPLOADVEHICLEBLACKWHITELSTFILE</td><td>13</td><td>上传黑授权名单配 置文件功能</td><td>NULL</td><td>NULL</td></tr></table></body></html>  

#### 5.30.2 获取文件上传的进度和状态 NET_DVR_GetUploadState  

函  数： LONG NET_DVR_GetUploadState(LONG lUploadHandle,LPDWORD pProgress)  
参  数： [in] lUploadHandle 文件上传的句柄，NET_DVR_UploadFile_V40 的返回值[out] pProgress 返回的进度值，取值范围： $0^{\sim}100$   
返回值： -1 表示函数调用失败，其他为上传的状态值：1- 上传成功；2- 正在上传；3- 上传失败；4- 网络断开，状态未知。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.30.3 停止文件上传 NET_DVR_UploadClose  

函  数： BOOL NET_DVR_UploadClose(LONG lUploadHandle)  
参  数： [in] lUploadHandle 文件上传的句柄，NET_DVR_UploadFile_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.30.4 开始下载文件 NET_DVR_StartDownload  

函  数： LONG NET_DVR_StartDownload(LONG lUserID, DWORD dwDownloadType, LPVOID lpInBuffer,DWORD dwInBufferSize, char const \*sFileName)  

参  数： [in] lUserID 用户 ID，NET_DVR_Login_V40 的返回值[in] dwDownloadType 下载文件类型，详见表 5.118[in] lpInBuffer 输入参数。不同的 dwUploadType，输入参数不同，详见表 5.118[in] dwInBufferSize 输入缓冲区大小[in] sFileName 下载文件的保存路径（绝对路径，包括文件名）  

返回值： -1 表示失败，其他值作为 NET_DVR_StopDownload 和 NET_DVR_GetDownloadState 等函数的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

表 5.118 文件下载类型  


<html><body><table><tr><td>dwDownloadType</td><td>取值</td><td>含义</td><td>IplnBuffer对应结构体</td></tr><tr><td>NETSDKDOWNLOADCERT</td><td>0</td><td>下载证书</td><td>NETDVRCERT PARAM</td></tr><tr><td>NET_SDK_DOWNLOAD_IPC_CFG_FILE</td><td>1</td><td>下载IPC配置文件</td><td>NULL</td></tr><tr><td></td><td>8</td><td>下载黑授权名单配置文件</td><td>NULL</td></tr></table></body></html>  

#### 5.30.5 获取文件下载的进度和状态 NET_DVR_GetDownloadState  

函  数： LONG NET_DVR_GetDownloadState(LONG lDownloadHandle, LPDWORD pProgress)  
参  数： [in] lDownloadHandle 文件下载的句柄，NET_DVR_StartDownload 的返回值[out] pProgress 返回的进度值，取值范围： $0^{\sim}100$   
返回值： -1 表示函数调用失败，其他为下载的状态值：1- 下载成功；2- 正在下载；3- 下载失败；4- 网络断开，状态未知。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.30.6 停止文件下载 NET_DVR_StopDownload  

函  数： BOOL NET_DVR_StopDownload(LONG lHandle);  
参  数： [in] lHandle 文件下载的句柄，NET_DVR_StartDownload 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

### 5.31设备维护管理  

#### 获取设备工作状态  

#### 5.31.1 批量获取配置信息 NET_DVR_GetDeviceConfig  

函  数： BOOL NET_DVR_GetDeviceConfig(LONG lUserID, DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer,DWORD dwInBufferSize,LPVOID lpStatusList,LPVOID lpOutBuffer, DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in] dwCommand 设备配置命令，详见表 5.119[in] dwCount 一次要获取配置参数的个数，0 和 1 都表示 1 个信息，2 表示 2 个信息，最大 64 个[in] lpInBuffer 配置条件缓冲区，详见表 5.119[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的配置一一对应，例如 lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节，参数值：0 或者 1 表示成功，其他值为失败对应的错误号[out] lpOutBuffer 设备返回的参数内容（详见表 5.119），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取配置信息的通用接口。lpInBuffer 指定需要获取的信息，lpOutBuffer 保存获取得到的 dwCount 个配置信息。不同的 dwCommand 对应不同的结构体和命令号，如表 5.119 所示。  

表 5.119 批量获取设备参数  


<html><body><table><tr><td>dwCommand</td><td>含义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td><td>宏定义值</td></tr><tr><td>NET_DVRGETWORKSTATUS</td><td>获取设备工作状态，dwCount为ONET_DVR_GETWORKSTATE_COND</td><td></td><td>NET_DVR_WORKSTATE_V40</td><td>6189</td></tr></table></body></html>  

#### 返回目录  

#### 5.31.2 获取设备运行状态 NET_DVR_GetDeviceStatus  

函  数： BOOL NET_DVR_GetDeviceStatus(LONG lUserID,DWORD dwCommand, DWORD dwCount, LPVOIDlpInBuffer, DWORD dwInBufferSize,LPVOID lpStatusList, LPVOID lpOutBuffer,DWORDdwOutBufferSize)  

参  数： [in] lUserID 用户 ID 号，NET_DVR_Login_V30 返回值[in] dwCommand 设备配置命令，详见表 5.120[in] dwCount 要设置的个数，设为 1[in] lpInBuffer 配置条件缓冲区，详见表 5.121[in] dwInBufferSize 缓冲区长度[out] lpStatusList 错误信息列表，和要查询的监控点一一对应，例如lpStatusList[2]就对应 lpInBuffer[2]，由用户分配内存，每个错误信息为 4 个字节(1 个 32 位无符号整数值)，参数值：0- 成功，大于 0- 失败[out] lpOutBuffer 设备返回的参数内容（详见表 5.121），和要查询的监控点一一对应。如果某个监控点对应的 lpStatusList 信息为大于 0 值，对应 lpOutBuffer 的内容就是无效的[in] dwOutBufferSize 输出缓冲区大小  

表 5.120 状态获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>dwCommand含义</td><td>宏定义值</td></tr><tr><td>NETDVRGETALARMINSTATUS</td><td>获取报警输入状态</td><td>9115</td></tr><tr><td>NET DVR_GET_ALARMOUT_STATUS</td><td>获取报警输出状态</td><td>9116</td></tr><tr><td>NETDVRGETAUDIOCHANSTATUS</td><td>获取语音对讲状态</td><td>9117</td></tr></table></body></html>  

返回值： TRUE 表示成功，但不代表每一个配置都成功，哪一个成功，对应查看 lpStatusList[n]值；FALSE表示全部失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口是带有发送数据的批量获取设备状态信息的通用接口。全部获取时 dwCount 置为 0xffffffff，lpInBuffer 置为 NULL，dwInBufferSize 置为 0，lpStatusList 置为 NULL。lpOutBuffer 前面 4 个字节为个数(N)，后面为设备返回的 N 个信息内容（按通道号 $\mathsf{1}^{\sim_{N}}$ 排列），如果设置的 lpOutBuffer 缓冲区不足，仅返回部分信息，可以根据返回的个数（前 4 字节的值）重新获取。不同的获取功能对应不同的结构体和命令号，如表 5.121 所示。  

表 5.121 获取设备状态  


<html><body><table><tr><td>dwCommand宏定义</td><td>IplnBuffer对应结构体</td><td>lpOutBuffer对应结构体</td></tr><tr><td>NETDVRGETALARMINSTATUS</td><td>dwCount个4字节报警输入通道号</td><td>dwCount个4字节状态值(0-没有报警，1-有报警)</td></tr><tr><td>NETDVRGETALARMOUTSTATUS</td><td>dwCount个4字节报警输出通道号</td><td>dwCount个4字节状态值(0-没有报警，1-有报警)</td></tr><tr><td>NETDVRGETAUDIOCHANSTATUS</td><td>dwCount t为1，4字节语音对讲通道号</td><td>1个4字节状态(0-未开启，1-开启)</td></tr></table></body></html>  

#### 5.31.3 设备在线状态检测 NET_DVR_RemoteControl  

函  数： BOOL NET_DVR_RemoteControl(LONG lUserID, DWORD dwCommand, LPVOID lpInBuffer, DWORDdwInBufferSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.122[in]lpInBuffer 输入参数，具体内容跟控制命令相关，详见表 5.122[in]dwInBufferSize 输入参数长度  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该控制命令用于手动检测设备是否在线，接口返回 TRUE 表示在线，FALSE 表示与设备通信失败或者返回错误状态。设备在线状态自动巡检功能通过 NET_DVR_SetSDKLocalCfg（配置类型：NET_SDK_LOCAL_CFG_TYPE_CHECK_DEV）进行配置。  

表 5.122 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>控制功能</td><td>IplnBuffer对应结构体</td></tr><tr><td>NETDVRCHECKUSERSTATUS</td><td>20005</td><td>检测设备是否在线</td><td>NULL</td></tr></table></body></html>  

#### 5.31.4 启动设备状态巡检 NET_DVR_StartGetDevState  

函  数： BOOL NET_DVR_StartGetDevState(LPNET_DVR_CHECK_DEV_STATE pParams)  
参  数： [in] pParams 设备工作状态巡检参数，包括巡检时间、结果回调函数等，详见结构体：NET_DVR_CHECK_DEV_STATE  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 启动后，SDK 定时巡检设备，获取到的设备状态信息在结构体的回调函数中返回。相当于实现定时调用 NET_DVR_GetDeviceConfig(命令：NET_DVR_GET_WORK_STATUS)。  

#### 5.31.5 停止设备状态巡检 NET_DVR_StopGetDevState  

函  数： BOOL NET_DVR_StopGetDevState()参  数： 无  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 停止巡检设备工作状态，释放资源。  

#### 远程升级  

#### 5.31.6 设置远程升级时网络环境 NET_DVR_SetNetworkEnvironment  

函  数： BOOL NET_DVR_SetNetworkEnvironment(DWORD dwEnvironmentLevel)  

参  数： [in]dwEnvironmentLevel 网络环境级别enum{LOCAL_AREA_NETWORK $=0$ ,//局域网环境WIDE_AREA_NETWORK //广域网环境返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 接口中的网络环境级别参数分为两类，LOCAL_AREA_NETWORK 表示局域网环境(网络环境好，通讯流畅)；WIDE_AREA_NETWORK  表示广域网环境(网络环境差，易阻塞)。在调用远程升级接口之前，可以通过此接口适应不同的升级环境。  

返回目录  

#### 5.31.7 远程升级 NET_DVR_Upgrade  

函  数： LONG NET_DVR_Upgrade(LONG lUserID, char \*sFileName)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]sFileName 升级的文件路径（包括文件名）。路径长度和操作系统有关，sdk不做限制，windows 默认路径长度小于等于 256 字节（包括文件名在内）。  

返回值： -1 表示失败，其他值作为 NET_DVR_GetUpgradeState 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.31.8 获取远程升级的进度 NET_DVR_GetUpgradeProgress  

函  数： int NET_DVR_GetUpgradeProgress(LONG lUpgradeHandle)  
参  数： [in]lUpgradeHandle NET_DVR_Upgrade 的返回值  
返回值： -1 表示失败， $0{\sim}100$ 表示升级进度。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.31.9 获取远程升级的状态 NET_DVR_GetUpgradeState  

函  数： int NET_DVR_GetUpgradeState(LONG lUpgradeHandle)  
参  数： [in]lUpgradeHandle NET_DVR_Upgrade 的返回值  
返回值： -1 表示失败，其他值定义：1- 升级成功；2- 正在升级；3- 升级失败；4- 网络断开，状态未知；5- 升级文件语言版本不匹配。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.31.10 获取远程升级的阶段信息 NET_DVR_GetUpgradeStep  

函  数： LONG NET_DVR_GetUpgradeStep(LONG lUpgradeHandle, LONG \*pSubProgress)  
参  数： [in]lUpgradeHandle NET_DVR_Upgrade 的返回值[in]pSubProgress 升级阶段子进度  
返回值： -1 表示失败，其他值定义如表 5.123 所示。  

表 5.123 升级阶段信息  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>STEP_RECV_DATA</td><td>1</td><td>接收升级包数据</td></tr><tr><td>STEPUPGRADE</td><td>2</td><td>升级系统</td></tr><tr><td>STEPBACKUP</td><td>3</td><td>备份系统</td></tr><tr><td>STEP_SEARCH</td><td>255</td><td>设备正在搜索升级文件</td></tr></table></body></html>

接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.31.11 关闭远程升级句柄，释放资源 NET_DVR_CloseUpgradeHandle  

函  数： BOOL  NET_DVR_CloseUpgradeHandle(LONG lUpgradeHandle)  
参  数： [in]lUpgradeHandle NET_DVR_Upgrade 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 在线升级  

#### 5.31.12 获取在线升级相关信息 NET_DVR_GetSTDConfig  

函  数： BOOL NET_DVR_GetSTDConfig(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONFIGlpConfigParam)  

参  数： [in]lUserID [in]dwCommand [in&out]lpConfigParam  

用户 ID 号，NET_DVR_Login_V40 的返回值  
设备配置命令，详见表 5.124  
配置输入输出参数，不同的配置功能对应不同的输入输出参数，  
详见表 5.125  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 获取配置参数时，lpConfigParam 结构体中的 lpInBuffer 无效，设为 NULL。对于不同的配置功能（dwCommand），lpConfigParam中lpCondBuffer、lpOutBuffer分别对应不同的内容，具体如表 5.125示。  

表 5.124 参数获取命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>含义</td><td>宏定义值</td></tr><tr><td>NET_DVR_GET_ONLINEUPGRADE_PROGRESS</td><td>获取在线升级状态和进度</td><td>9302</td></tr><tr><td>NET_DVR_GET_FIRMWARECODE</td><td>获取识别码</td><td>9303</td></tr><tr><td>NET_DVR_GET_ONLINEUPGRADE_SERVER</td><td>获取升级服务器状态</td><td>9304</td></tr><tr><td>NET_DVR_GET_ONLINEUPGRADE_VERSION</td><td>获取新版本信息</td><td>9305</td></tr><tr><td>NET_DVR_GET_RECOMMEN_VERSION</td><td>检测是否推荐升级到此版本</td><td>9306</td></tr></table></body></html>  

表 5.125 参数获取结构  


<html><body><table><tr><td>dwCommand宏定义</td><td>pCondBuffer</td><td>lpOutBuffer</td></tr><tr><td>NET_DVR_GET_ONLINEUPGRADE_PROGRESS</td><td>NULL</td><td>NET_DVR_ONLINEUPGRADE_STATUS</td></tr><tr><td>NETDVRGETFIRMWARECODE</td><td>NETDVRFIRMWARECODECOND</td><td>NETDVRFIRMWARECODELIST</td></tr><tr><td>NET_DVR_GET_ONLINEUPGRADE_SERVER</td><td>NULL</td><td>NET_DVRONLINEUPGRADESERVER</td></tr><tr><td>NET_DVR_GET_ONLINEUPGRADE_VERSION</td><td>NET_DVR_ONLINEUPGRADE_VERSION_COND</td><td>NET_DVR_ONLINEUPGRADE_VERSION_RET</td></tr><tr><td>NET_DVR_GET_RECOMMEN_VERSION</td><td>NETDVRRECOMMENVERSIONCOND</td><td>NET_DVR_RECOMMEN_VERSION_RET</td></tr></table></body></html>  

#### 返回目录  

#### 5.31.13 远程控制在线升级 NET_DVR_STDControl  

函  数： BOOL NET_DVR_STDControl(LONG lUserID, DWORD dwCommand, LPNET_DVR_STD_CONTROLlpControlParam)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwCommand 控制命令，详见表 5.126[in&out]lpControlParam 远程控制输入输出参数，不同的控制功能对应不同的输入输出参数，详见表 5.126  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 对于不同的配置功能（dwCommand），lpControlParam 中的 lpCondBuffer 对应不同的内容，如表5.126 所示。  

表 5.126 远程控制命令  


<html><body><table><tr><td>dwCommand宏定义</td><td>宏定义值</td><td>含义</td><td>IpCondBuffer对应结构体</td></tr></table></body></html>  

<html><body><table><tr><td>NETDVRSETONLINEUPGRADE</td><td>9301</td><td>允许在线升级</td><td>NULL</td></tr></table></body></html>  

 设备是否支持在线升级功能或者支持的参数能力，可以通过设备能力集进行判断，对应在线升级能力集(OnlineUpgradeCap)，相关接口：NET_DVR_GetSTDAbility，能力集类型：NET_DVR_GET_ONLINEUPGRADE_ABILITY。  

$\bullet$ 在线升级过程：  

1）设备注册到服务器，从服务器上获取新版本信息。  
2）客户端登录设备后在通过接口 NET_DVR_GetSTDConfig 获取可以升级的服务器、版本等信息，然后调用该接口下发命令允许在线升级，升级过程中可以定时获取升级进度。  
3）设备收到可在线升级命令后从服务器下载升级包自行升级。  

返回目录  

#### 日志查找  

#### 5.31.14 查找设备的日志信息（可搜索带 S.M.A.R.T 信息的日志）  

#### NET_DVR_FindDVRLog_V30  

函  数： LONG  NET_DVR_FindDVRLog_V30(LONG lUserID, LONG lSelectMode, DWORD dwMajorType,DWORD dwMinorType, LPNET_DVR_TIME lpStartTime, LPNET_DVR_TIME lpStopTime, BOOLbOnlySmart $=$ FALSE)  

参  数： [in]lUserID NET_DVR_Login_V40 的返回值[in]lSelectMode 查询方式：0- 全部，1- 按类型，2- 按时间，3- 按时间和类型[in]dwMajorType 日志主类型（S.M.A.R.T 搜索时无效），0 表示全部类型，其他类型定义见表 6.1[in]dwMinorType 日志次类型（S.M.A.R.T 搜索时无效），0 表示全部类型，根据不同的主类型的次类型定义见表 $6.2^{\sim}$ 表 6.5[in]lpStartTime 文件的开始时间[in]lpStopTime 文件结束时间[in]bOnlySmart 是否只搜索带 S.M.A.R.T 信息的日志  

返回值： -1 表示失败，其他值作为 NET_DVR_FindNextLog_V30 等函数的参数。接口返回失败请调用NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 该接口如果用于搜索普通日志信息，一般设备（81xx，80xx 等）支持 2000 条， $9000\ v2.0$ 支持 4000条，81xxST 支持 1000 条，而搜索带 S.M.A.R.T 信息的日志最大只支持 500 条。通常不需要搜索详细的 S.M.A.R.T 信息时，置 bOnlySmart 为 FALSE 即可完成所有日志信息的搜索。S.M.A.R.T 信息：硬盘运行日志记录。  

#### 5.31.15 逐条获取查找到的日志信息 NET_DVR_FindNextLog_V30  

函  数： LONG  NET_DVR_FindNextLog_V30(LONG lLogHandle, LPNET_DVR_LOG_V30 lpLogData)参  数： [in]lLogHandle 日志查找句柄，NET_DVR_FindDVRLog_V30()的返回值[out]lpLogData 保存日志信息的指针返回值： -1 表示失败，其他值表示当前的获取状态等信息。接口返回失败请调用 NET_DVR_GetLastError  

获取错误码，通过错误码判断出错原因。说  明： 在调用该接口获取查找日志之前，必须先调用 NET_DVR_FindDVRLog_V30 得到当前的查找句柄。  

#### 5.31.16 释放查找日志的资源 NET_DVR_FindLogClose_V30  

函  数： BOOL  NET_DVR_FindLogClose_V30(LONG lLogHandle)  
参  数： [in]lLogHandle 日志查找句柄，NET_DVR_FindDVRLog_V30 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 远程备份  

#### 5.31.17 获取设备磁盘列表 NET_DVR_GetDiskList  

函  数： BOOL  NET_DVR_GetDiskList(LONG lUserID, LPNET_DVR_DISKABILITY_LIST lpDiskList)  
参  数： [in]lUserID NET_DVR_Login_V40 的返回值[out]lpDiskList 设备可用备份磁盘信息结构  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 该接口用于获取设备可用备份文件的磁盘资源信息，在备份文件功能接口的输入参数中需要用到。  

#### 5.31.18 备份统一接口 NET_DVR_Backup  

函  数： DWORD NET_DVR_Backup(long lUserID,DWORD dwBackupType,void\* lpBackupBuff,DWORDdwBackupBuffSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]dwBackupType 备份类型：1- 按文件名备份录像文件，2- 按时间段备份录像文件，3- 备份图片，4- 恢复审讯事件，5- 备份日志[in]lpBackupBuff 指向备份参数指针，详见表 5.127[in]dwBackupBuffSize 备份参数大小  

返回值： -1 失败，0-510 的返回句柄值作为 NET_DVR_GetBackupProgress，NET_DVR_StopBackup 的参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  
说  明： 不同的备份类型（dwBackupType）对应不同的备份参数结构体（lpBackupBuff），详见表 5.127。  

表 5.127 备份操作类型  


<html><body><table><tr><td>dwBackupType</td><td>含义</td><td>IpBackupBuff</td></tr><tr><td>1</td><td>按文件名备份录像文件</td><td>NETDVRBACKUP NAME PARAM</td></tr></table></body></html>  

<html><body><table><tr><td>2</td><td>按时间段备份录像文件</td><td>NET DVRE BACKUP TIME PARAM</td></tr><tr><td>3</td><td>备份图片</td><td>NET DVRBACKUPPICTUREPARAM</td></tr><tr><td>5</td><td>备份日志</td><td>NET_DVR_E BACKUP_LOG_PARAM</td></tr></table></body></html>  

#### 5.31.19 获取备份的进度 NET_DVR_GetBackupProgress  

函  数： BOOL  NET_DVR_GetBackupProgress(LONG lHandle, DWORD\* pState)  
参  数： [in]lHandle NET_DVR_Backup 的返回值[out] pState 当前备份的进度，进度值的取值范围为[0,100)，其他值的定义见表 5.128  

表 5.128 磁盘备份进度  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>BACKUP_SUCCESS</td><td>100</td><td>备份完成</td></tr><tr><td>BACKUP_CHANGE_DEVICE</td><td>101</td><td>备份设备已满，更换设备继续备份</td></tr><tr><td>BACKUP_SEARCH_DEVICE</td><td>300</td><td>正在搜索备份设备</td></tr><tr><td>BACKUP_SEARCH_FILE</td><td>301</td><td>正在搜索录像文件或者图片</td></tr><tr><td>BACKUP_EXCEPTION</td><td>400</td><td>备份异常</td></tr><tr><td>BACKUP_FAIL</td><td>500</td><td>备份失败</td></tr><tr><td>BACKUP_TIME_SEG_NO_FILE</td><td>501</td><td>时间段内无录像文件或者图片</td></tr><tr><td>BACKUP_NO_RESOURCE</td><td>502</td><td>申请不到资源</td></tr><tr><td>BACKUP_DEVICE_LOW_SPACE</td><td>503</td><td>备份设备容量不足</td></tr><tr><td>BACKUP_DISK_FINALIZED</td><td>504</td><td>刻录光盘封盘</td></tr><tr><td>BACKUP_DISK_EXCEPTION</td><td>505</td><td>刻录光盘异常</td></tr><tr><td>BACKUP_DEVICE_NOT_EXIST</td><td>506</td><td>备份设备不存在</td></tr><tr><td>BACKUP_OTNER_BACKUP_WORK</td><td>507</td><td>有其他备份操作在进行</td></tr><tr><td>BACKUP_USER_NO_RIGHT</td><td>508</td><td>用户没有操作权限</td></tr><tr><td>BACKUP_OPERATE_FAIL</td><td>509</td><td>操作失败</td></tr></table></body></html>

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。说  明： 在进度为 100 或者备份出错时, 需调用 NET_DVR_StopBackup()停止备份。  

#### 5.31.20 停止备份 NET_DVR_StopBackup  

函  数： BOOL  NET_DVR_StopBackup(LONG lHandle)  
参  数： [in]lHandle NET_DVR_Backup 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

#### 恢复设备默认参数  

#### 5.31.21 恢复设备默认参数 NET_DVR_RestoreConfig  

函  数： BOOL  NET_DVR_RestoreConfig(LONG lUserID)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 导入/导出配置文件  

#### 5.31.22 导出配置文件 NET_DVR_GetConfigFile_V30  

函  数： BOOL  NET_DVR_GetConfigFile_V30(LONG lUserID, char \*sOutBuffer, DWORD dwOutSize, DWORD\*pReturnSize)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[out] sOutBuffer 存放配置参数的缓冲区[in]dwOutSize 缓冲区大小[out]pReturnSize 实际获得的缓冲区大小  

返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明： 当 sOutBuffer $=$ NULL、dwOutSize ${}=0$ 且 pReturnSize $!=$ NULL 时用于获取参数配置文件的所需的缓冲区长度；当 sOutBuffer $!=$ NULL 且 dwOutSize $\mathrel{\mathop:}$ 时用于获取参数配置文件的所需的缓冲区内容。  

返回目录  

#### 5.31.23 导出配置文件 NET_DVR_GetConfigFile  

函  数： BOOL  NET_DVR_GetConfigFile(LONG lUserID, char \*sFileName)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]sFileName 存放保存配置文件的文件路径（二进制文件）  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.31.24 导入配置文件 NET_DVR_SetConfigFile_EX  

函  数： BOOL NET_DVR_SetConfigFile_EX(LONG lUserID, char \*sInBuffer, DWORD dwInSize)  

参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]sInBuffer 存放配置参数的缓冲区[in]dwInSize 缓冲区大小  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.31.25 导入配置文件 NET_DVR_SetConfigFile  

函  数： BOOL  NET_DVR_SetConfigFile(LONG lUserID, char \*sFileName)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值[in]sFileName 存放保存配置文件的文件路径（二进制文件）  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 网流量检测  

#### 5.31.26 开始网络流量检测 NET_DVR_StartNetworkFlowTest  

函  数： LONG NET_DVR_StartNetworkFlowTest(LONG lUserID, NET_DVR_FLOW_TEST_PARAM\* pFlowTest,FLOWTESTCALLBACK fFlowTestCallback, void \*pUser)  
参  数： [in]lUserID NET_DVR_Login_V30 的返回[in]pFlowTest 网络流量参数[in]fFlowTestCallback 网络流量检测回调函数[in]pUser 用户数据typedef void(CALLBACK \*fFlowTestCallback)(LONG lFlowHandle, LPNET_DVR_FLOW_INFOpFlowInfo, void \*pUser)[out]lFlowHandle 当前的检测句柄[out]pFlowInfo 网络流量检测结果[out]pUser 用户数据  

返回值： -1 表示失败，其他值作为 NET_DVR_StopNetworkFlowTest 等函数的句柄参数。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.31.27 停止网络流量检测 NET_DVR_StopNetworkFlowTest  

函  数： BOOL NET_DVR_StopNetworkFlowTest(LONG lHandle)参  数： [in]lHandle NET_DVR_StartNetworkFlowTest 的返回值返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通  

过错误码判断出错原因。  

说  明：  

#### 获取 UPNP 端口映射状态  

#### 5.31.28 获取 UPNP 端口映射状态 NET_DVR_GetUpnpNatState  

函  数： BOOL NET_DVR_GetUpnpNatState(LONG  lUserID, LPNET_DVR_UPNP_NAT_STATE   lpState)  
参  数： [in]lUserID NET_DVR_Login_V30 的返回[out]lpState UPNP 端口映射状态  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 关机和重启  

#### 5.31.29 重启设备 NET_DVR_RebootDVR  

函  数： BOOL  NET_DVR_RebootDVR(LONG lUserID)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

#### 5.31.30 关闭设备 NET_DVR_ShutDownDVR  

函  数： BOOL NET_DVR_ShutDownDVR(LONG lUserID)  
参  数： [in]lUserID 用户 ID 号，NET_DVR_Login_V40 的返回值  
返回值： TRUE 表示成功，FALSE 表示失败。接口返回失败请调用 NET_DVR_GetLastError 获取错误码，通过错误码判断出错原因。  

说  明：  

## 6 错误代码和日志类型  

### 6.1 网络通讯库错误码  

<html><body><table><tr><td>错误名称</td><td>错误值</td><td>说明</td></tr><tr><td>NET_DVR_NOERROR</td><td>0</td><td>没有错误</td></tr><tr><td>NET_DVR_PASSWORD_ERROR</td><td>1</td><td>用户名密码错误注册时输入的用户名或者密码错误</td></tr><tr><td>NET_DVR_NOENOUGHPRI</td><td>2</td><td>权限不足该注册用户没有权限执行当前对设备的操</td></tr><tr><td>NET_DVR_NOINIT</td><td>3</td><td>作，可以与远程用户参数配置做对比 SDK 未初始化</td></tr><tr><td>NET_DVR_CHANNEL_ERROR</td><td>4</td><td>通道号错误设备没有对应的通道号</td></tr><tr><td>NET_DVR_OVER_MAXLINK</td><td>5</td><td>连接到设备的用户个数超过最大</td></tr><tr><td>NET_DVR_VERSIONNOMATCH</td><td>6</td><td>版本不匹配SDK和设备的版本不匹配</td></tr><tr><td>NET_DVR_NETWORK_FAIL_CONNECT</td><td>7</td><td>连接设备失败设备不在线或网络原因引起的连接超</td></tr><tr><td>NET_DVR_NETWORK_SEND_ERROR</td><td>8</td><td>时等 向设备发送失败</td></tr><tr><td>NET_DVR_NETWORK_RECV_ERROR</td><td>9</td><td>从设备接收数据失败</td></tr><tr><td>NET_DVR_NETWORK_RECV_TIMEOUT</td><td>10</td><td>从设备接收数据超时</td></tr><tr><td>NET_DVR_NETWORK_ERRORDATA</td><td>11</td><td>传送的数据有误发送给设备或者从设备接收到的数</td></tr><tr><td>NET_DVR_ORDER_ERROR</td><td>12</td><td>据错误，如远程参数配置时输入设备不支持的值 调用次序错误</td></tr><tr><td>NET_DVR_OPERNOPERMIT</td><td>13</td><td>无此权限</td></tr><tr><td>NET_DVR_COMMANDTIMEOUT</td><td>14</td><td>设备命令执行超时</td></tr><tr><td>NET_DVR_ERRORSERIALPORT</td><td>15</td><td>串口号错误指定的设备串口号不存在</td></tr><tr><td>NET_DVR_ERRORALARMPORT</td><td>16</td><td>报警端口错误指定的设备报警输出端口不存在</td></tr><tr><td>NET_DVR_PARAMETER_ERROR</td><td>17</td><td>参数错误SDK接口中给入的输入或输出参数为空</td></tr><tr><td>NET_DVR_CHAN_EXCEPTION</td><td>18</td><td>设备通道处于错误状态</td></tr><tr><td>NET_DVR_NODISK</td><td>19</td><td>设备无硬盘当设备无硬盘时，对设备的录像文件、</td></tr><tr><td>NET_DVR_ERRORDISKNUM</td><td>20</td><td>硬盘配置等操作失败 硬盘号错误当对设备进行硬盘管理操作时，指定的</td></tr><tr><td>NET_DVR_DISK_FULL</td><td>21</td><td>硬盘号不存在时返回该错误 设备硬盘满</td></tr><tr><td>NET_DVR_DISK_ERROR</td><td>22</td><td>设备硬盘出错</td></tr><tr><td>NET_DVR_NOSUPPORT</td><td>23</td><td>设备不支持</td></tr><tr><td>NET_DVR_BUSY</td><td>24</td><td>设备忙</td></tr><tr><td>NET_DVR_MODIFY_FAIL</td><td>25</td><td>设备修改不成功</td></tr><tr><td>NET_DVR_PASSWORD_FORMAT_ERROR</td><td>26</td><td>密码输入格式不正确</td></tr><tr><td>NET_DVR_DISK_FORMATING</td><td>27</td><td>硬盘正在格式化，不能启动操作</td></tr><tr><td>NET_DVR_DVRNORESOURCE</td><td>28</td><td>设备资源不足</td></tr><tr><td>NET_DVR_DVROPRATEFAILED</td><td>29</td><td>设备操作失败</td></tr><tr><td>NET_DVR_OPENHOSTSOUND_FAIL</td><td>30</td><td>语音对讲、语音广播操作中采集本地音频或打开音</td></tr><tr><td></td><td></td><td>频输出失败</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_DVRVOICEOPENED</td><td>31</td><td>设备语音对讲被占用</td></tr><tr><td>NET_DVR_TIMEINPUTERROR</td><td>32</td><td>时间输入不正确</td></tr><tr><td>NET_DVR_NOSPECFILE</td><td>33</td><td>回放时设备没有指定的文件</td></tr><tr><td>NET_DVR_CREATEFILE_ERROR</td><td>34</td><td>创建文件出错本地录像、保存图片、获取配置文件 和远程下载录像时创建文件失败</td></tr><tr><td>NET_DVR_FILEOPENFAIL</td><td>35</td><td>打开文件出错设置配置文件、设备升级、上传审讯 文件时打开文件失败</td></tr><tr><td>NET_DVR_OPERNOTFINISH</td><td>36</td><td>上次的操作还没有完成</td></tr><tr><td>NET_DVR_GETPLAYTIMEFAIL</td><td>37</td><td>获取当前播放的时间出错</td></tr><tr><td>NET_DVR_PLAYFAIL</td><td>38</td><td>播放出错</td></tr><tr><td>NET_DVR_FILEFORMAT_ERROR</td><td>39</td><td>文件格式不正确</td></tr><tr><td>NET_DVR_DIR_ERROR</td><td>40</td><td>路径错误</td></tr><tr><td>NET_DVR_ALLOC_RESOURCE_ERROR</td><td>41</td><td>SDK资源分配错误</td></tr><tr><td>NET_DVR_AUDIO_MODE_ERROR</td><td>42</td><td>声卡模式错误当前打开声音播放模式与实际设置的 模式不符出错</td></tr><tr><td>NET_DVR_NOENOUGH_BUF</td><td>43</td><td>缓冲区太小接收设备数据的缓冲区或存放图片缓冲 区不足</td></tr><tr><td>NET_DVR_CREATESOCKET_ERROR</td><td>44</td><td>创建 SOCKET 出错</td></tr><tr><td>NET_DVR_SETSOCKET_ERROR</td><td>45</td><td>设置 SOCKET 出错</td></tr><tr><td>NET_DVR_MAX_NUM</td><td>46</td><td>个数达到最大分配的注册连接数、预览连接数超过 SDK支持的最大数</td></tr><tr><td>NET_DVR_USERNOTEXIST</td><td>47</td><td>用户不存在注册的用户ID 已注销或不可用</td></tr><tr><td>NET_DVR_WRITEFLASHERROR</td><td>48</td><td>写FLASH出错设备升级时写FLASH失败</td></tr><tr><td>NET_DVR_UPGRADEFAIL</td><td>49</td><td>设备升级失败网络或升级文件语言不匹配等原因升</td></tr><tr><td>NET_DVR_CARDHAVEINIT</td><td>50</td><td>级失败 解码卡已经初始化过</td></tr><tr><td>NET_DVR_PLAYERFAILED</td><td>51</td><td>调用播放库中某个函数失败</td></tr><tr><td>NET_DVR_MAX_USERNUM</td><td>52</td><td>登录设备的用户数达到最大</td></tr><tr><td>NET_DVR_GETLOCALIPANDMACFAIL</td><td>53</td><td>获得本地PC的IP地址或物理地址失败</td></tr><tr><td>NET_DVR_NOENCODEING</td><td>54</td><td>设备该通道没有启动编码</td></tr><tr><td>NET_DVR_IPMISMATCH</td><td>55</td><td>IP地址不匹配</td></tr><tr><td>NET_DVR_MACMISMATCH</td><td>56</td><td>MAC地址不匹配</td></tr><tr><td>NET_DVR_UPGRADELANGMISMATCH</td><td>57</td><td>升级文件语言不匹配</td></tr><tr><td>NET_DVR_MAX_PLAYERPORT</td><td>58</td><td>播放器路数达到最大</td></tr><tr><td>NET_DVR_NOSPACEBACKUP</td><td>59</td><td>备份设备中没有足够空间进行备份</td></tr><tr><td>NET_DVR_NODEVICEBACKUP</td><td>60</td><td>没有找到指定的备份设备</td></tr><tr><td>NET_DVR_PICTURE_BITS_ERROR</td><td>61</td><td>图像素位数不符，限24色</td></tr><tr><td>NET_DVR_PICTURE_DIMENSION_ERROR</td><td>62</td><td>图片高*宽超限，限128*256</td></tr><tr><td>NET_DVR_PICTURE_SIZ_ERROR</td><td>63</td><td>图片大小超限，限100K</td></tr><tr><td>NET_DVR_LOADPLAYERSDKFAILED</td><td>64</td><td>载入当前目录下 Player Sdk 出错</td></tr><tr><td>NET_DVR_LOADPLAYERSDKPROC_ERROR</td><td>65</td><td>找不到 Player Sdk 中某个函数入口</td></tr><tr><td>NET_DVR_LOADDSSDKFAILED</td><td>66</td><td>载入当前目录下DSsdk出错</td></tr><tr><td>NET_DVR_LOADDSSDKPROC_ERROR</td><td>67</td><td>找不到DsSdk中某个函数入口</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_DSSDK_ERROR</td><td>68</td><td>调用硬解码库DsSdk中某个函数失败</td></tr><tr><td>NET_DVR_VOICEMONOPOLIZE</td><td>69</td><td>声卡被独占</td></tr><tr><td>NET_DVR_JOINMULTICASTFAILED</td><td>70</td><td>加入多播组失败</td></tr><tr><td>NET_DVR_CREATEDIR_ERROR</td><td>71</td><td>建立日志文件目录失败</td></tr><tr><td>NET_DVR_BINDSOCKET_ERROR</td><td>72</td><td>绑定套接字失败</td></tr><tr><td>NET_DVR_SOCKETCLOSE_ERROR</td><td>73</td><td>socket连接中断，此错误通常是由于连接中断或目的 地不可达</td></tr><tr><td>NET_DVR_USERID_ISUSING</td><td>74</td><td>注销时用户ID正在进行某操作</td></tr><tr><td>NET_DVR_SOCKETLISTEN_ERROR</td><td>75</td><td>监听失败</td></tr><tr><td>NET_DVR_PROGRAM_EXCEPTION</td><td>76</td><td>程序异常</td></tr><tr><td>NET_DVR_WRITEFILE_FAILED</td><td>77</td><td>写文件失败本地录像、远程下载录像、下载图片等 操作时写文件失败</td></tr><tr><td>NET_DVR_FORMAT_READONLY</td><td>78</td><td>禁止格式化只读硬盘</td></tr><tr><td>NET_DVR_WITHSAMEUSERNAME</td><td>79</td><td>远程用户配置结构中存在相同的用户名</td></tr><tr><td>NET_DVR_DEVICETYPE_ERROR</td><td>80</td><td>导入参数时设备型号不匹配</td></tr><tr><td>NET_DVR_LANGUAGE_ERROR</td><td>81</td><td>导入参数时语言不匹配</td></tr><tr><td>NET_DVR_PARAVERSION_ERROR</td><td>82</td><td>导入参数时软件版本不匹配</td></tr><tr><td>NET_DVR_IPCHAN_NOTALIVE</td><td>83</td><td>预览时外接IP通道不在线</td></tr><tr><td>NET_DVR_RTSP_SDK_ERROR</td><td>84</td><td>加载标准协议通讯库 StreamTransClient失败</td></tr><tr><td>NET_DVR_CONVERT_SDK_ERROR</td><td>85</td><td>加载转封装库失败</td></tr><tr><td>NET_DVR_IPC_COUNT_OVERFLOW</td><td>86</td><td>超出最大的IP接入通道数</td></tr><tr><td>NET_DVR_MAX_ADD_NUM</td><td>87</td><td>添加录像标签或者其他操作超出最多支持的个数</td></tr><tr><td>NET_DVR_PARAMMODE_ERROR</td><td>88</td><td>图像增强仪，参数模式错误（用于硬件设置时，客</td></tr><tr><td>NET_DVR_CODESPITTER_OFFLINE</td><td>89</td><td>户端进行软件设置时错误值) 码分器不在线</td></tr><tr><td>NET_DVR_BACKUP_COPYING</td><td>90</td><td>设备正在备份</td></tr><tr><td>NET_DVR_CHAN_NOTSUPPORT</td><td>91</td><td>通道不支持该操作</td></tr><tr><td>NET_DVR_CALLINEINVALID</td><td>92</td><td>高度线位置太集中或长度线不够倾斜</td></tr><tr><td>NET_DVR_CALCANCELCONFLICT</td><td>93</td><td>取消标定冲突，如果设置了规则及全局的实际大小</td></tr><tr><td>NET_DVR_CALPOINTOUTRANGE</td><td>94</td><td>尺寸过滤 标定点超出范围</td></tr><tr><td>NET_DVR_FILTERRECTINVALID</td><td>95</td><td>尺寸过滤器不符合要求</td></tr><tr><td>NET_DVR_DDNS_DEVOFFLINE</td><td>96</td><td>设备没有注册到ddns上</td></tr><tr><td>NET_DVR_DDNS_INTER_ERROR</td><td>97</td><td>DDNS服务器内部错误</td></tr><tr><td>NET_DVR_INTERCOM_SDK_ERROR</td><td>100</td><td>加载当前目录下的语音对讲库失败</td></tr><tr><td>NET_DVR_NO_CURRENT_UPDATEFILE</td><td>101</td><td>没有正确的升级包</td></tr><tr><td>NET_DVR_USER_NOT_SUCC_LOGIN</td><td>102</td><td>用户还没登录成功</td></tr><tr><td>NET_DVR_USE_LOG_SWITCH_FILE</td><td>103</td><td>正在使用日志开关文件</td></tr><tr><td>NET_DVR_POOL_PORT_EXHAUST</td><td>104</td><td>端口池中用于绑定的端口已耗尽</td></tr><tr><td>NET_DVR_PACKET_TYPE_NOT_SUPPORT</td><td>105</td><td>码流封装格式错误</td></tr><tr><td>NET_DVR_IPPARA_IPID_ERROR</td><td>106</td><td>IP接入配置时IPID有误</td></tr><tr><td>NET_DVR_LOAD_HCPREVIEW_SDK_ERROR</td><td>107</td><td>预览组件加载失败</td></tr><tr><td>NET_DVR_LOAD_HCVOICETALK_SDK_ERROR</td><td>108</td><td>语音组件加载失败</td></tr><tr><td>NET_DVR_LOAD_HCALARM_SDK_ERROR</td><td>109</td><td>报警组件加载失败</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_LOAD_HCPLAYBACK_SDK_ERROR</td><td>110</td><td>回放组件加载失败</td></tr><tr><td>NET_DVR_LOAD_HCDISPLAY_SDK_ERROR</td><td>111</td><td>显示组件加载失败</td></tr><tr><td>NET_DVR_LOAD_HCINDUSTRY_SDK_ERROR</td><td>112</td><td>行业应用组件加载失败</td></tr><tr><td>NET_DVR_LOAD_HCGENERALCFGMGR_SDK_ERROR</td><td>113</td><td>通用配置管理组件加载失败</td></tr><tr><td>NET_DVR_CORE_VER_MISMATCH</td><td>121</td><td>单独加载组件时，组件与 core 版本不匹配</td></tr><tr><td>NET_DVR_CORE_VER_MISMATCH_HCPREVIEW</td><td>122</td><td>预览组件与 core版本不匹配</td></tr><tr><td>NET_DVR_CORE_VER_MISMATCH_HCVOICETALK</td><td>123</td><td>语音组件与 core版本不匹配</td></tr><tr><td>NET_DVR_CORE_VER_MISMATCH_HCALARM</td><td>124</td><td>报警组件与 core 版本不匹配</td></tr><tr><td>NET_DVR_CORE_VER_MISMATCH_HCPLAYBACK</td><td>125</td><td>回放组件与 core 版本不匹配</td></tr><tr><td>NET_DVR_CORE_VER_MISMATCH_HCDISPLAY</td><td>126</td><td>显示组件与 core 版本不匹配</td></tr><tr><td>NET_DVR_CORE_VER_MISMATCH_HCINDUSTRY</td><td>127</td><td>行业应用组件与 core 版本不匹配</td></tr><tr><td>NET_DVR_CORE_VER_MISMATCH_HCGENERALCFGMGR</td><td>128</td><td>通用配置管理组件与core版本不匹配</td></tr><tr><td>NET_DVR_COM_VER_MISMATCH_HCPREVIEW</td><td>136</td><td>预览组件与HCNetSDK版本不匹配</td></tr><tr><td>NET_DVR_COM_VER_MISMATCH_HCVOICETALK</td><td>137</td><td>语音组件与HCNetSDK版本不匹配</td></tr><tr><td>NET_DVR_COM_VER_MISMATCH_HCALARM</td><td>138</td><td>报警组件与HCNetSDK版本不匹配</td></tr><tr><td>NET_DVR_COM_VER_MISMATCH_HCPLAYBACK</td><td>139</td><td>回放组件与HCNetSDK 版本不匹</td></tr><tr><td>NET_DVR_COM_VER_MISMATCH_HCDISPLAY</td><td>140</td><td>显示组件与HCNetSDK版本不匹配</td></tr><tr><td>NET_DVR_COM_VER_MISMATCH_HCINDUSTRY</td><td>141</td><td>行业应用组件与HCNetSDK版本不匹配</td></tr><tr><td>NET_DVR_COM_VER_MISMATCH_HCGENERALCFGMGR</td><td>142</td><td>通用配置管理组件与HCNetSDK版本不匹配</td></tr><tr><td>NET_DVR_ALIAS_DUPLICATE</td><td>150</td><td>别名重复（EasyDDNS 的配置）</td></tr><tr><td>NET_DVR_USERNAME_NOT_EXIST</td><td>152</td><td>用户名不存在（V5.1.7~V5.3.1版本的IPC、IPD的错</td></tr><tr><td>NET_ERR_USERNAME_LOCKED</td><td>153</td><td>误码) 用户名被锁定</td></tr><tr><td>NET_DVR_INVALID_USERID</td><td>154</td><td>无效用户ID</td></tr><tr><td>NET_DVR_LOW_LOGIN_VERSION</td><td>155</td><td>登录版本低</td></tr><tr><td>NET_DVR_LOAD_LIBEAY32_DLL_ERROR</td><td>156</td><td>加载libeay32.dll库失败</td></tr><tr><td>NET_DVR_LOAD_SSLEAY32_DLL_ERROR</td><td>157</td><td>加载 ssleay32.dll库失败</td></tr><tr><td>NET_DVR_TEST_SERVER_FAIL_CONNECT</td><td>165</td><td>连接测试服务器失败</td></tr><tr><td>NET_DVR_DEV_NET_OVERFLOW</td><td>800</td><td>网络流量超过设备能力上限</td></tr><tr><td>NET_DVR_STATUS_RECORDFILE_WRITING_NOT_LOCK</td><td>801</td><td>录像文件在录像，无法被锁定</td></tr><tr><td>NET_DVR_STATUS_CANT_FORMAT_LITTLE_DISK</td><td>802</td><td>由于硬盘太小无法格式化</td></tr><tr><td>NET_SDK_ERR_CHAN_AUDIO_BIND</td><td>821</td><td>通道未绑定或绑定语音对讲失败</td></tr><tr><td>NET_DVR_N_PLUS_ONE_MODE</td><td>822</td><td>设备当前处于 N+1 模式，不支持设置云存储</td></tr><tr><td>NET_DVR_CLOUD_STORAGE_OPENED</td><td>823</td><td>云存储模式已开启</td></tr><tr><td>NET_DVR_CHECK_PASSWORD_MISTAKE_ERROR</td><td>834</td><td>校验密码错误</td></tr><tr><td>阵列错误码</td><td></td><td></td></tr><tr><td>NET_DVR_NAME_NOT_ONLY</td><td>200</td><td>名称已存在</td></tr><tr><td>NET_DVR_OVER_MAX_ARRAY</td><td>201</td><td>阵列达到上限</td></tr><tr><td>NET_DVR_OVER_MAX_VD</td><td>202</td><td>虚拟磁盘达到上限</td></tr><tr><td>NET_DVR_VD_SLOT_EXCEED</td><td>203</td><td>虚拟磁盘槽位已满</td></tr><tr><td>NET_DVR_PD_STATUS_INVALID</td><td>204</td><td>重建阵列所需物理磁盘状态错误</td></tr><tr><td>NET_DVR_PD_BE_DEDICATE_SPARE</td><td>205</td><td>重建阵列所需物理磁盘为指定热备</td></tr><tr><td>NET_DVR_PD_NOT_FREE</td><td>206</td><td>重建阵列所需物理磁盘非空闲</td></tr><tr><td>NET_DVR_CANNOT_MIG2NEWMODE</td><td>207</td><td>不能从当前的阵列类型迁移到新的阵列类型</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_MIG_PAUSE</td><td>208</td><td>迁移操作已暂停</td></tr><tr><td></td><td>209</td><td>正在执行的迁移操作已取消</td></tr><tr><td>NET_DVR_MIG_CANCEL NET_DVR_EXIST_VD</td><td>210</td><td>阵列上存在虚拟磁盘，无法删除阵列</td></tr><tr><td>NET_DVR_TARGET_IN_LD_FUNCTIONAL</td><td>211</td><td>对象物理磁盘为虚拟磁盘组成部分且工作正常</td></tr><tr><td>NET_DVR_HD_IS_ASSIGNED_ALREADY</td><td>212</td><td>指定的物理磁盘被分配为虚拟磁盘</td></tr><tr><td>NET_DVR_INVALID_HD_COUNT</td><td>213</td><td>物理磁盘数量与指定的RAID等级不匹配</td></tr><tr><td>NET_DVR_LD_IS_FUNCTIONAL</td><td>214</td><td>阵列正常，无法重建</td></tr><tr><td>NET_DVR_BGA_RUNNING</td><td>215</td><td>存在正在执行的后台任务</td></tr><tr><td>NET_DVR_LD_NO_ATAPI</td><td>216</td><td>无法用 ATAPI盘创建虚拟磁盘</td></tr><tr><td>NET_DVR_MIGRATION_NOT_NEED</td><td></td><td></td></tr><tr><td>NET_DVR_HD_TYPE_MISMATCH</td><td>217</td><td>阵列无需迁移</td></tr><tr><td>NET_DVR_NO_LD_IN_DG</td><td>218</td><td>物理磁盘不属于同意类型</td></tr><tr><td>NET_DVR_NO_ROOM_FOR_SPARE</td><td>219</td><td>无虚拟磁盘，无法进行此项操作</td></tr><tr><td>NET_DVR_SPARE_IS_IN_MULTI_DG</td><td>220</td><td>磁盘空间过小，无法被指定为热备盘</td></tr><tr><td>NET_DVR_DG_HAS_MISSING_PD</td><td>221</td><td>磁盘已被分配为某阵列热备盘</td></tr><tr><td>NET_DVR_NAME_EMPTY</td><td>222</td><td>阵列缺少盘</td></tr><tr><td>NET_DVR_INPUT_PARAM</td><td>223</td><td>名称为空</td></tr><tr><td>NET_DVR_PD_NOT_AVAILABLE</td><td>224</td><td>输入参数有误</td></tr><tr><td>NET_DVR_ARRAY_NOT_AVAILABLE</td><td>225 226</td><td>物理磁盘不可用</td></tr><tr><td>NET_DVR_PD_COUNT</td><td>227</td><td>阵列不可用</td></tr><tr><td>NET_DVR_VD_SMALL</td><td>228</td><td>物理磁盘数不正确</td></tr><tr><td>NET_DVR_NO_EXIST</td><td>229</td><td>虚拟磁盘太小</td></tr><tr><td>NET_DVR_NOT_SUPPORT</td><td>230</td><td>不存在</td></tr><tr><td>NET_DVR_NOT_FUNCTIONAL</td><td>231</td><td>不支持该操作</td></tr><tr><td>NET_DVR_DEV_NODE_NOT_FOUND</td><td>232</td><td>阵列状态不是正常状态</td></tr><tr><td>NET_DVR_SLOT_EXCEED</td><td>233</td><td>虚拟磁盘设备节点不存在</td></tr><tr><td>NET_DVR_NO_VD_IN_ARRAY</td><td>234</td><td>槽位达到上限</td></tr><tr><td>NET_DVR_VD_SLOT_INVALID</td><td></td><td>阵列上不存在虚拟磁盘</td></tr><tr><td>NET_DVR_PD_NO_ENOUGH_SPACE</td><td>235</td><td>虚拟磁盘槽位无效</td></tr><tr><td>NET_DVR_ARRAY_NONFUNCTION</td><td>236</td><td>所需物理磁盘空间不足</td></tr><tr><td></td><td>237</td><td>只有处于正常状态的阵列才能进行迁移</td></tr><tr><td>NET_DVR_ARRAY_NO_ENOUGH_SPACE</td><td>238</td><td>阵列空间不足</td></tr><tr><td>NET_DVR_STOPPING_SCANNING_ARRAY</td><td>239</td><td>正在执行安全拔盘或重新扫描</td></tr><tr><td>NET_DVR_NOT_SUPPORT_16T 安全激活相关错误码</td><td>240</td><td>不支持创建大于 16T 的阵列</td></tr><tr><td>NET_DVR_ERROR_DEVICE_NOT_ACTIVATED</td><td>250</td><td>设备未激活（设备未激活时，登录失败，返回错误</td></tr><tr><td>NET_DVR_ERROR_RISK_PASSWORD</td><td>251</td><td>码） 有风险的密码（设置用户密码或者激活的时候为风</td></tr><tr><td>NET_DVR_ERROR_DEVICE_HAS_ACTIVATED</td><td>252</td><td>险密码) 设备已激活 （已激活的设备，再次激活时返回错误)</td></tr><tr><td>N+1功能错误码</td><td></td><td></td></tr><tr><td>NET_SDK_ERR_REMOTE_DISCONNEC</td><td>803</td><td>远端无法连接</td></tr><tr><td>NET_SDK_ERR_RD_ADD_RD</td><td>804</td><td>备机不能添加备机</td></tr><tr><td>NET_SDK_ERR_BACKUP_DISK_EXCEPT</td><td>805</td><td>备份盘异常</td></tr><tr><td>NET_SDK_ERR_RD_LIMIT</td><td>806</td><td>备机数已达上限</td></tr></table></body></html>  

<html><body><table><tr><td>NET_SDK_ERR_ADDED_RD_IS_WD</td><td>807</td><td>添加的备机是工作机</td></tr><tr><td>NET_SDK_ERR_ADD_ORDER_WRONG</td><td>808</td><td>添加顺序出错，比如没有被工作机添加为备机，就 添加工作机</td></tr><tr><td>NET_SDK_ERR_WD_ADD_WD</td><td>809</td><td>工作机不能添加工作机</td></tr><tr><td>NET_SDK_ERR_WD_SERVICE_EXCETP</td><td>810</td><td>工作机CVR服务异常</td></tr><tr><td>NET_SDK_ERR_RD_SERVICE_EXCETP</td><td>811</td><td>备机CVR服务异常</td></tr><tr><td>NET_SDK_ERR_ADDED_WD_IS_RD</td><td>812</td><td>添加的工作机是备机</td></tr><tr><td>NET_SDK_ERR_PERFORMANCE_LIMIT</td><td>813</td><td>性能达到上限</td></tr><tr><td>NET_SDK_ERR_ADDED_DEVICE_EXIST</td><td>814</td><td>添加的设备已经存在</td></tr><tr><td>解码器错误</td><td></td><td></td></tr><tr><td>NET_ERR_WINDOW_SIZE_OVERLIMIT</td><td>943</td><td>窗口大小超限</td></tr><tr><td>NET_ERR_MAX_WIN_OVERLAP</td><td>951</td><td>达到最大窗口重叠数</td></tr><tr><td>NET_ERR_STREAMID_CHAN_BOTH_VALID</td><td>952</td><td>streamID和通道号同时有效</td></tr><tr><td>NET_DVR_ERR_WINDOW_SIZE_PLACE</td><td>975</td><td>窗口位置错误</td></tr><tr><td>NET_DVR_ERR_RGIONAL_RESTRICTIONS</td><td>976</td><td>屏幕距离超限</td></tr><tr><td>NET_DVR_ERR_CLOSE_WINDOWS</td><td>984</td><td>操作失败，请先关闭窗口</td></tr><tr><td>NET_DVR_ERR_MATRIX_LOOP_ABILITY</td><td>985</td><td>超出轮巡解码能力限制</td></tr><tr><td>NET_DVR_ERR_MATRIX_LOOP_TIME</td><td>986</td><td>轮巡解码时间不支持</td></tr><tr><td>NET_DVR_ERR_LINKED_OUT_ABILITY</td><td>987</td><td>联动通道数超过上限</td></tr><tr><td>能力集错误码</td><td></td><td></td></tr><tr><td>XML_ABILITY_NOTSUPPORT</td><td>1000</td><td>不支持能力节点获取</td></tr><tr><td>XML_ANALYZE_NOENOUGH_BUF</td><td>1001</td><td>输出内存不足</td></tr><tr><td>XML_ANALYZE_FIND_LOCALXML_ERROR</td><td>1002</td><td>无法找到对应的本地xml</td></tr><tr><td>XML_ANALYZE_LOAD_LOCALXML_ERROR</td><td>1003</td><td>加载本地 xml 出错</td></tr><tr><td>XML_NANLYZE_DVR_DATA_FORMAT_ERROR</td><td>1004</td><td>设备能力数据格式错误</td></tr><tr><td>XML_ANALYZE_TYPE_ERROR</td><td>1005</td><td>能力集类型错误</td></tr><tr><td>XML_ANALYZE_XML_NODE_ERROR</td><td>1006</td><td>XML能力节点格式错误</td></tr><tr><td>XML_INPUT_PARAM_ERROR</td><td>1007</td><td>输入的能力XML节点值错误</td></tr><tr><td>XML_VERSION_MISMATCH</td><td>1008</td><td>XML版本不匹配</td></tr><tr><td>VQD错误码</td><td></td><td></td></tr><tr><td>NET_ERR_VQD_TIME_CONFLICT</td><td>1500</td><td>VQD诊断时间段冲突</td></tr><tr><td>NET_ERR_VQD_PLAN_NO_EXIST</td><td>1501</td><td>VQD 诊断计划不存在</td></tr><tr><td>NET_ERR_VQD_CHAN_NO_EXIST</td><td>1502</td><td>VQD监控点不存在</td></tr><tr><td>NET_ERR_VQD_CHAN_MAX</td><td>1503</td><td>VQD计划数已达上限</td></tr><tr><td>NET_ERR_VQD_TASK_MAX</td><td>1504</td><td>VQD任务数已达上限</td></tr><tr><td>其他错误码</td><td></td><td></td></tr><tr><td>NET_DVR_ERR_FILE_NOT_COMPLETE</td><td>2100</td><td>下载的文件不完整</td></tr><tr><td>NET_DVR_ERR_IPC_EXIST</td><td>2101</td><td>该 IPC 已经存在</td></tr><tr><td>NET_DVR_ERR_ADD_IPC</td><td>2102</td><td>该通道已添加IPC</td></tr><tr><td>NET_DVR_ERR_OUT_OF_RES</td><td>2103</td><td>网络带宽能力不足</td></tr><tr><td>NET_DVR_ERR_CONFLICT_TO_LOCALIP</td><td>2104</td><td>IPC 的ip 地址跟 DVR 的IP 地址冲突</td></tr><tr><td>NET_DVR_ERR_IP_SET</td><td>2105</td><td>非法IP 地址</td></tr><tr><td>NET_DVR_ERR_PORT_SET</td><td>2106</td><td>非法的端口号</td></tr><tr><td>NET_ERR_MUTEX_FUNCTION</td><td>2108</td><td>功能互斥</td></tr></table></body></html>  

6.2 RTSP 通讯库错误码  


<html><body><table><tr><td>错误名称</td><td>错误值</td><td>说明</td></tr><tr><td>NET_DVR_RTSP_ERROR_NOENOUGHPRI</td><td>401</td><td>无权限：服务器返回401时，转成这个错误码</td></tr><tr><td>NET_DVR_RTSP_ERROR_ALLOC_RESOURCE</td><td>402</td><td>分配资源失败</td></tr><tr><td>NET_DVR_RTSP_ERROR_PARAMETER</td><td>403</td><td>参数错误</td></tr><tr><td>NET_DVR_RTSP_ERROR_NO_URL</td><td>404</td><td>指定的URL地址不存在：服务器返回404时，转成这个错 误码，例如请求不可用的通道号预览、请求不支持子码流 的通道预览</td></tr><tr><td>NET_DVR_RTSP_ERROR_FORCE_STOP</td><td>406</td><td>用户中途强行退出</td></tr><tr><td>NET_DVR_RTSP_GETPORTFAILED</td><td>407</td><td>获取RTSP端口错误</td></tr><tr><td>NET_DVR_RTSP_DESCRIBERROR</td><td>410</td><td>RTSPDECRIBE交互错误</td></tr><tr><td>NET_DVR_RTSP_DESCRIBESENDTIMEOUT</td><td>411</td><td>RTSPDECRIBE 发送超时</td></tr><tr><td>NET_DVR_RTSP_DESCRIBESENDERROR</td><td>412</td><td>RTSPDECRIBE发送失败</td></tr><tr><td>NET_DVR_RTSP_DESCRIBERECVTIMEOUT</td><td>413</td><td>RTSPDECRIBE接收超时</td></tr><tr><td>NET_DVR_RTSP_DESCRIBERECVDATALOST</td><td>414</td><td>RTSPDECRIBE接收数据错误</td></tr><tr><td>NET_DVR_RTSP_DESCRIBERECVERROR</td><td>415</td><td>RTSPDECRIBE接收失败</td></tr><tr><td>NET_DVR_RTSP_DESCRIBESERVERERR</td><td>416</td><td>RTSPDECRIBE服务器返回错误状态。例如服务器返回 400，可能是不支持子码流</td></tr><tr><td>NET_DVR_RTSP_SETUPERROR</td><td>420</td><td>RTSPSETUP交互错误，一般是服务器返回的码流地址无法 连接上，或者被服务器拒绝。（老版本的SDK可能返回错 误号419，为同样的错误原因)</td></tr><tr><td>NET_DVR_RTSP_SETUPSENDTIMEOUT</td><td>421</td><td>RTSPSETUP发送超时</td></tr><tr><td>NET_DVR_RTSP_SETUPSENDERROR</td><td>422</td><td>RTSPSETUP发送错误</td></tr><tr><td>NET_DVR_RTSP_SETUPRECVTIMEOUT</td><td>423</td><td>RTSP SETUP接收超时</td></tr><tr><td>NET_DVR_RTSP_SETUPRECVDATALOST</td><td>424</td><td>RTSPSETUP接收数据错误</td></tr><tr><td>NET_DVR_RTSP_SETUPRECVERROR</td><td>425</td><td>RTSPSETUP接收失败</td></tr><tr><td>NET_DVR_RTSP_OVER_MAX_CHAN</td><td>426</td><td>超过服务器最大连接数，或者服务器资源不足，服务器返 回453时，转成这个错误码</td></tr><tr><td>NET_DVR_RTSP_SETUPSERVERERR</td><td>427</td><td>RTSPSETUP服务器返回错误状态</td></tr><tr><td>NET_DVR_RTSP_PLAYERROR</td><td>430</td><td>RTSPPLAY交互错误</td></tr><tr><td>NET_DVR_RTSP_PLAYSENDTIMEOUT</td><td>431</td><td>RTSPPLAY发送超时</td></tr><tr><td>NET_DVR_RTSP_PLAYSENDERROR</td><td>432</td><td>RTSPPLAY发送错误</td></tr><tr><td>NET_DVR_RTSP_PLAYRECVTIMEOUT</td><td>433</td><td>RTSP PLAT接收超时</td></tr><tr><td>NET_DVR_RTSP_PLAYRECVDATALOST</td><td>434</td><td>RTSPPLAY接收数据错误</td></tr><tr><td>NET_DVR_RTSP_PLAYRECVERROR</td><td>435</td><td>RTSPPLAY接收失败</td></tr><tr><td>NET_DVR_RTSP_PLAYSERVERERR</td><td>436</td><td>RTSPPLAY服务器返回错误状态</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNERROR</td><td>440</td><td>RTSPTEARDOWN交互错误</td></tr></table></body></html>  

<html><body><table><tr><td>NET_DVR_RTSP_TEARDOWNSENDTIMEOUT</td><td>441</td><td>RTSPTEARDOWN发送超时</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNSENDERROR</td><td>442</td><td>RTSPTEARDOWN发送错误</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNRECVTIMEOUT</td><td>443</td><td>RTSPTEARDOWN接收超时</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNRECVDATALOST</td><td>444</td><td>RTSPTEARDOWN接收数据错误</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNRECVERROR</td><td>445</td><td>RTSPTEARDOWN接收失败</td></tr><tr><td>NET_DVR_RTSP_TEARDOWNSERVERERR</td><td>446</td><td>RTSPTEARDOWN服务器返回错误状态</td></tr></table></body></html>  

### 6.3 软解码库错误码  

<html><body><table><tr><td>错误名称</td><td>错误值</td><td>说明</td></tr><tr><td>NET_PLAYM4_NOERROR</td><td>500</td><td>没有错误</td></tr><tr><td>NET_PLAYM4_PARA_OVER</td><td>501</td><td>输入参数非法</td></tr><tr><td>NET_PLAYM4_ORDER_ERROR</td><td>502</td><td>调用顺序不对</td></tr><tr><td>NET_PLAYM4_TIMER_ERROR</td><td>503</td><td>多媒体时钟设置失败</td></tr><tr><td>NET_PLAYM4_DEC_VIDEO_ERROR</td><td>504</td><td>视频解码失败</td></tr><tr><td>NET_PLAYM4_DEC_AUDIO_ERROR</td><td>505</td><td>音频解码失败</td></tr><tr><td>NET_PLAYM4_ALLOC_MEMORY_ERROR</td><td>506</td><td>分配内存失败</td></tr><tr><td>NET_PLAYM4_OPEN_FILE_ERROR</td><td>507</td><td>文件操作失败</td></tr><tr><td>NET_PLAYM4_CREATE_OBJ_ERROR</td><td>508</td><td>创建线程事件等失败</td></tr><tr><td>NET_PLAYM4_CREATE_DDRAW_ERROR</td><td>509</td><td>创建 directDraw失败</td></tr><tr><td>NET_PLAYM4_CREATE_OFFSCREEN_ERROR</td><td>510</td><td>创建后端缓存失败</td></tr><tr><td>NET_PLAYM4_BUF_OVER</td><td>511</td><td>缓冲区满，输入流失败</td></tr><tr><td>NET_PLAYM4_CREATE_SOUND_ERROR</td><td>512</td><td>创建音频设备失败</td></tr><tr><td>NET_PLAYM4_SET_VOLUME_ERROR</td><td>513</td><td>设置音量失败</td></tr><tr><td>NET_PLAYM4_SUPPORT_FILE_ONLY</td><td>514</td><td>只能在播放文件时才能使用此接口</td></tr><tr><td>NET_PLAYM4_SUPPORT_STREAM_ONLY</td><td>515</td><td>只能在播放流时才能使用此接口</td></tr><tr><td>NET_PLAYM4_SYS_NOT_SUPPORT</td><td>516</td><td>系统不支持，解码器只能工作在 Pentium 3 以上</td></tr><tr><td>NET_PLAYM4_FILEHEADER_UNKNOWN</td><td>517</td><td>没有文件头</td></tr><tr><td>NET_PLAYM4_VERSION_INCORRECT</td><td>518</td><td>解码器和编码器版本不对应</td></tr><tr><td>NET_PALYM4_INIT_DECODER_ERROR</td><td>519</td><td>初始化解码器失败</td></tr><tr><td>NET_PLAYM4_CHECK_FILE_ERROR</td><td>520</td><td>文件太短或码流无法识别</td></tr><tr><td>NET_PLAYM4_INIT_TIMER_ERROR</td><td>521</td><td>初始化多媒体时钟失败</td></tr><tr><td>NET_PLAYM4_BLT_ERROR</td><td>522</td><td>位拷贝失败</td></tr><tr><td>NET_PLAYM4_UPDATE_ERROR</td><td>523</td><td>显示 overlay 失败</td></tr><tr><td>NET_PLAYM4_OPEN_FILE_ERROR_MULTI</td><td>524</td><td>打开混合流文件失败</td></tr><tr><td>NET_PLAYM4_OPEN_FILE_ERROR_VIDEO</td><td>525</td><td>打开视频流文件失败</td></tr><tr><td></td><td></td><td></td></tr><tr><td>NET_PLAYM4JPEG_COMPRESS_ERROR</td><td>526</td><td>JPEG 压缩错误</td></tr></table></body></html>  

<html><body><table><tr><td>NET_PLAYM4_EXTRACT_NOT_SUPPORT</td><td>527 不支持该文件版本</td><td></td></tr><tr><td>NET_PLAYM4_EXTRACT_DATA_ERROR</td><td>528</td><td>提取文件数据失败</td></tr></table></body></html>  

### 6.4 语音对讲库错误码  

<html><body><table><tr><td>错误名称</td><td>错误值</td><td>说明</td></tr><tr><td>NET_AUDIOINTERCOM_OK</td><td>600</td><td>没有错误</td></tr><tr><td>NET_AUDIOINTECOM_ERR_NOTSUPORT</td><td>601</td><td>不支持</td></tr><tr><td>NET_AUDIOINTECOM_ERR_ALLOC_MEMERY</td><td>602</td><td>内存申请错误</td></tr><tr><td>NET_AUDIOINTECOM_ERR_PARAMETER</td><td>603</td><td>参数错误</td></tr><tr><td>NET_AUDIOINTECOM_ERR_CALL_ORDER</td><td>604</td><td>调用次序错误</td></tr><tr><td>NET_AUDIOINTECOM_ERR_FIND_DEVICE</td><td>605</td><td>未发现设备</td></tr><tr><td>NET_AUDIOINTECOM_ERR_OPEN_DEVICE</td><td>606</td><td>不能打开设备</td></tr><tr><td>NET_AUDIOINTECOM_ERR_NO_CONTEXT</td><td>607</td><td>设备上下文出错</td></tr><tr><td>NET_AUDIOINTECOM_ERR_NO_WAVFILE</td><td>608</td><td>WAV文件出错</td></tr><tr><td>NET_AUDIOINTECOM_ERR_INVALID_TYPE</td><td>609</td><td>无效的WAV参数类型</td></tr><tr><td>NET_AUDIOINTECOM_ERR_ENCODE_FAIL</td><td>610</td><td>编码失败</td></tr><tr><td>NET_AUDIOINTECOM_ERR_DECODE_FAIL</td><td>611</td><td>解码失败</td></tr><tr><td>NET_AUDIOINTECOM_ERR_NO_PLAYBACK</td><td>612</td><td>播放失败</td></tr><tr><td>NET_AUDIOINTECOM_ERR_DENOISE_FAIL</td><td>613</td><td>降噪失败</td></tr><tr><td>NET_AUDIOINTECOM_ERR_UNKOWN</td><td>619</td><td>未知错误</td></tr></table></body></html>  

### 6.5 日志类型  

表 6.1 日志主类型  


<html><body><table><tr><td>宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MAJOR_ALARM</td><td>0x1</td><td>报警</td></tr><tr><td>MAJOR_EXCEPTION</td><td>0x2</td><td>异常</td></tr><tr><td>MAJOR_OPERATION</td><td>0x3</td><td>操作</td></tr><tr><td>MAJOR_INFORMATION</td><td>0x4</td><td>日志附加信息</td></tr></table></body></html>  

表 6.2 报警日志次类型  


<html><body><table><tr><td>主类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MAJORALARM</td><td>0x1</td><td>报警</td></tr><tr><td>次类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MINORALARMIN</td><td>0x1</td><td>报警输入</td></tr></table></body></html>  

<html><body><table><tr><td>MINOR_ALARM_OUT</td><td>0x2</td><td>报警输出</td></tr><tr><td>MINOR_MOTDET_START</td><td>0x3</td><td>移动侦测报警开始</td></tr><tr><td>MINOR_MOTDET_STOP</td><td>0x4</td><td>移动侦测报警结束</td></tr><tr><td>MINOR_HIDE_ALARM_START</td><td>0x5</td><td>遮挡报警开始</td></tr><tr><td>MINOR_HIDE_ALARM_STOP</td><td>0x6</td><td>遮挡报警结束</td></tr><tr><td>MINOR_VCA_ALARM_START</td><td>0x7</td><td>智能报警开始</td></tr><tr><td>MINOR_VCA_ALARM_STOP</td><td>0x8</td><td>智能报警结束</td></tr><tr><td>MINOR_ITS_ALARM_START</td><td>0x09</td><td>交通事件报警开始</td></tr><tr><td>MINOR_ITS_ALARM_STOP</td><td>eoxo</td><td>交通事件报警结束</td></tr><tr><td>MINOR_NETALARM_START</td><td>0x0b</td><td>网络报警开始</td></tr><tr><td>MINOR_NETALARM_STOP</td><td>Ox0c</td><td>网络报警结束</td></tr><tr><td>MINOR_NETALARM_RESUME</td><td>pOxO</td><td>网络报警恢复</td></tr></table></body></html>  

表 6.3 异常日志次类型  


<html><body><table><tr><td>主类型的宏定义</td><td>宏定义值 含义</td><td></td></tr><tr><td>MAJOR_EXCEPTION</td><td>0x2</td><td>异常</td></tr><tr><td>次类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MINOR_RAID_ERROR</td><td>0x20</td><td>阵列异常</td></tr><tr><td>MINOR_VI_LOST</td><td>0x21</td><td>视频信号丢失</td></tr><tr><td>MINOR_ILLEGAL_ACCESS</td><td>0x22</td><td>非法访问</td></tr><tr><td>MINOR_HD_FULL</td><td>0x23</td><td>硬盘满</td></tr><tr><td>MINOR_HD_ERROR</td><td>0x24</td><td>硬盘错误</td></tr><tr><td>MINOR_DCD_LOST</td><td>0x25</td><td>MODEM掉线(保留)</td></tr><tr><td>MINOR_IP_CONFLICT</td><td>0x26</td><td>IP地址冲突</td></tr><tr><td>MINOR_NET_BROKEN</td><td>0x27</td><td>网络断开</td></tr><tr><td>MINOR_REC_ERROR</td><td>0x28</td><td>录像出错</td></tr><tr><td>MINOR_IPC_NO_LINK</td><td>0x29</td><td>IPC连接异常</td></tr><tr><td>MINOR_VI_EXCEPTION</td><td>0x2a</td><td>视频输入异常(只针对模拟通道)</td></tr><tr><td>MINOR_IPC_IP_CONFLICT</td><td>0x2b</td><td>IPC 的IP 地址冲突</td></tr><tr><td>MINOR_SENCE_EXCEPTION</td><td>0x2c</td><td>场景异常</td></tr><tr><td>MINOR_PIC_REC_ERROR</td><td>0x2d</td><td>抓图出错,获取图片文件失败</td></tr><tr><td>MINOR_VI_MISMATCH</td><td>0x2e</td><td>视频制式不匹配</td></tr><tr><td>MINOR_RECORD_OVERFLOW</td><td>0x41</td><td>缓冲区溢出</td></tr><tr><td>MINOR_DSP_ABNORMAL</td><td>0x42</td><td>DSP异常</td></tr><tr><td>MINOR_ANR_RECORD_FAIED</td><td>0x43</td><td>ANR录像失败</td></tr></table></body></html>  

<html><body><table><tr><td>MINOR_SPARE_WORK_DEVICE_EXCEPT</td><td>0x44</td><td>热备设备工作机异常</td></tr><tr><td>MINOR_START_IPC_MAS_FAILED</td><td>0x45</td><td>开启IPCMAS失败</td></tr><tr><td>MINOR_IPCM_CRASH</td><td>0x46</td><td>IPCM异常重启</td></tr><tr><td>MINOR_POE_POWER_EXCEPTION</td><td>0x47</td><td>POE供电异常</td></tr><tr><td>MINOR_UPLOAD_DATA_CS_EXCEPTION</td><td>0x48</td><td>云存储数据上传失败</td></tr><tr><td>MINOR_SYNC_IPC_PASSWD</td><td>0x53</td><td>同步IPC密码异常</td></tr><tr><td>MINOR_EZVIZ_OFFLINE</td><td>0x54</td><td>萤石下线异常</td></tr><tr><td>MINOR_ACCESSORIES_PLATE</td><td>0x57</td><td>配件板异常</td></tr></table></body></html>  

表 6.4 操作日志次类型  


<html><body><table><tr><td>主类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MAJOR_OPERATION</td><td>0x3</td><td>操作</td></tr><tr><td>次类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MINOR_START_DVR</td><td>0x41</td><td>开机</td></tr><tr><td>MINOR_STOP_DVR</td><td>0x42</td><td>关机</td></tr><tr><td>MINOR_STOP_ABNORMAL</td><td>0x43</td><td>异常关机</td></tr><tr><td>MINOR_REBOOT_DVR</td><td>0x44</td><td>本地重启设备</td></tr><tr><td>MINOR_LOCAL_LOGIN</td><td>0x50</td><td>本地登陆</td></tr><tr><td>MINOR_LOCAL_LOGOUT</td><td>0x51</td><td>本地注销登陆</td></tr><tr><td>MINOR_LOCAL_CFG_PARM</td><td>0x52</td><td>本地配置参数</td></tr><tr><td>MINOR_LOCAL_PLAYBYFILE</td><td>0x53</td><td>本地按文件回放或下载</td></tr><tr><td>MINOR_LOCAL_PLAYBYTIME</td><td>0x54</td><td>本地按时间回放或下载</td></tr><tr><td>MINOR_LOCAL_START_REC</td><td>0x55</td><td>本地开始录像</td></tr><tr><td>MINOR_LOCAL_STOP_REC</td><td>0x56</td><td>本地停止录像</td></tr><tr><td>MINOR_LOCAL_PTZCTRL</td><td>0x57</td><td>本地云台控制</td></tr><tr><td>MINOR_LOCAL_PREVIEW</td><td>0x58</td><td>本地预览(保留不使用)</td></tr><tr><td>MINOR_LOCAL_MODIFY_TIME</td><td>0x59</td><td>本地修改时间(保留不使用)</td></tr><tr><td>MINOR_LOCAL_UPGRADE</td><td>0x5a</td><td>本地升级</td></tr><tr><td>MINOR_LOCAL_RECFILE_OUTPUT</td><td>0x5b</td><td>本地备份录象文件</td></tr><tr><td>MINOR_LOCAL_FORMAT_HDD</td><td>0x5c</td><td>本地初始化硬盘</td></tr><tr><td>MINOR_LOCAL_CFGFILE_OUTPUT</td><td>0x5d</td><td>导出本地配置文件</td></tr><tr><td>MINOR_LOCAL_CFGFILE_INPUT</td><td>0x5e</td><td>导入本地配置文件</td></tr><tr><td>MINOR_LOCAL_COPYFILE</td><td>Ox5f</td><td>本地备份文件</td></tr><tr><td>MINOR_LOCAL_LOCKFILE</td><td>0x60</td><td>本地锁定录像文件</td></tr><tr><td>MINOR_LOCAL_UNLOCKFILE</td><td>0x61</td><td>本地解锁录像文件</td></tr></table></body></html>  

<html><body><table><tr><td>MINOR_LOCAL_DVR_ALARM</td><td>0x62</td><td>本地手动清除和触发报警</td></tr><tr><td>MINOR_IPC_ADD</td><td>0x63</td><td>本地添加IPC</td></tr><tr><td>MINOR_IPC_DEL</td><td>0x64</td><td>本地删除IPC</td></tr><tr><td>MINOR_IPC_SET</td><td>0x65</td><td>本地设置IPC</td></tr><tr><td>MINOR_LOCAL_START_BACKUP</td><td>0x66</td><td>本地开始备份</td></tr><tr><td>MINOR_LOCAL_STOP_BACKUP</td><td>0x67</td><td>本地停止备份</td></tr><tr><td>MINOR_LOCAL_COPYFILE_START_TIME</td><td>0x68</td><td>本地备份开始时间</td></tr><tr><td>MINOR_LOCAL_COPYFILE_END_TIME</td><td>0x69</td><td>本地备份结束时间</td></tr><tr><td>MINOR_LOCAL_ADD_NAS</td><td>0x6a</td><td>本地添加网络硬盘</td></tr><tr><td>MINOR_LOCAL_DEL_NAS</td><td>0x6b</td><td>本地删除 NAS 盘</td></tr><tr><td>MINOR_LOCAL_SET_NAS</td><td>39x0</td><td>本地设置 NAS 盘</td></tr><tr><td>MINOR_REMOTE_LOGIN</td><td>0x70</td><td>远程登录</td></tr><tr><td>MINOR_REMOTE_LOGOUT</td><td>0x71</td><td>远程注销登陆</td></tr><tr><td>MINOR_REMOTE_START_REC</td><td>0x72</td><td>远程开始录像</td></tr><tr><td>MINOR_REMOTE_STOP_REC</td><td>0x73</td><td>远程停止录像</td></tr><tr><td>MINOR_START_TRANS_CHAN</td><td>0x74</td><td>开始透明传输</td></tr><tr><td>MINOR_STOP_TRANS_CHAN</td><td>0x75</td><td>停止透明传输</td></tr><tr><td>MINOR_REMOTE_GET_PARM</td><td>0x76</td><td>远程获取参数</td></tr><tr><td>MINOR_REMOTE_CFG_PARM</td><td>0x77</td><td>远程配置参数</td></tr><tr><td>MINOR_REMOTE_GET_STATUS</td><td>0x78</td><td>远程获取状态</td></tr><tr><td>MINOR_REMOTE_ARM</td><td>0x79</td><td>远程布防</td></tr><tr><td>MINOR_REMOTE_DISARM</td><td>0x7a</td><td>远程撤防</td></tr><tr><td>MINOR_REMOTE_REBOOT</td><td>0x7b</td><td>远程重启</td></tr><tr><td>MINOR_START_VT</td><td>0x7c</td><td>开始语音对讲</td></tr><tr><td>MINOR_STOP_VT</td><td>pLx0</td><td>停止语音对讲</td></tr><tr><td>MINOR_REMOTE_UPGRADE</td><td>0x7e</td><td>远程升级</td></tr><tr><td>MINOR_REMOTE_PLAYBYFILE</td><td>JX0</td><td>远程按文件回放</td></tr><tr><td>MINOR_REMOTE_PLAYBYTIME</td><td>0x80</td><td>远程按时间回放</td></tr><tr><td>MINOR_REMOTE_PTZCTRL</td><td>0x81</td><td>远程云台控制</td></tr><tr><td>MINOR_REMOTE_FORMAT_HDD</td><td>0x82</td><td>远程格式化硬盘</td></tr><tr><td>MINOR_REMOTE_STOP</td><td>0x83</td><td>远程关机</td></tr><tr><td>MINOR_REMOTE_LOCKFILE</td><td>0x84</td><td>远程锁定文件</td></tr><tr><td>MINOR_REMOTE_UNLOCKFILE</td><td>0x85</td><td>远程解锁文件</td></tr><tr><td>MINOR_REMOTE_CFGFILE_OUTPUT</td><td>0x86</td><td>远程导出配置文件</td></tr><tr><td>MINOR_REMOTE_CFGFILE_INTPUT</td><td>0x87</td><td>远程导入配置文件</td></tr></table></body></html>  

<html><body><table><tr><td>MINOR_REMOTE_RECFILE_OUTPUT</td><td>0x88</td><td>远程导出录象文件</td></tr><tr><td>MINOR_REMOTE_DVR_ALARM</td><td>0x89</td><td>远程手动清除和触发报警</td></tr><tr><td>MINOR_REMOTE_IPC_ADD</td><td>0x8a</td><td>远程添加IPC</td></tr><tr><td>MINOR_REMOTE_IPC_DEL</td><td>0x8b</td><td>远程删除IPC</td></tr><tr><td>MINOR_REMOTE_IPC_SET</td><td>0x8c</td><td>远程设置IPC</td></tr><tr><td>MINOR_REBOOT_VCA_LIB</td><td>0x8d</td><td>重启智能库</td></tr><tr><td>MINOR_REMOTE_ADD_NAS</td><td>0x8e</td><td>远程添加 NAS 盘</td></tr><tr><td>MINOR_REMOTE_DEL_NAS</td><td>Ox8f</td><td>远程删除 NAS 盘</td></tr><tr><td>MINOR_REMOTE_SET_NAS</td><td>0x90</td><td>远程设置 NAS 盘</td></tr><tr><td>MINOR_LOCAL_START_REC_CDRW</td><td>0x91</td><td>本地开始刻录</td></tr><tr><td>MINOR_LOCAL_STOP_REC_CDRW</td><td>0x92</td><td>本地停止刻录</td></tr><tr><td>MINOR_REMOTE_START_REC_CDRW</td><td>0x93</td><td>远程开始刻录</td></tr><tr><td>MINOR_REMOTE_STOP_REC_CDRW</td><td>0x94</td><td>远程停止刻录</td></tr><tr><td>MINOR_LOCAL_PIC_OUTPUT</td><td>0x95</td><td>本地备份图片文件</td></tr><tr><td>MINOR_REMOTE_SET_NAS</td><td>0x96</td><td>远程备份图片文件</td></tr><tr><td>MINOR_LOCAL_INQUEST_RESUME</td><td>0x97</td><td>本地恢复审讯事件</td></tr><tr><td>MINOR_REMOTE_INQUEST_RESUME</td><td>0x98</td><td>远程恢复审讯事件</td></tr><tr><td>MINOR_LOCAL_ADD_FILE</td><td>0x99</td><td>本地导入文件</td></tr><tr><td>MINOR_REMOTE_DELETE_HDISK</td><td>0x9a</td><td>远程删除异常不存在的硬盘</td></tr><tr><td>MINOR_REMOTE_LOAD_HDISK</td><td>0x9b</td><td>远程加载硬盘</td></tr><tr><td>MINOR_REMOTE_UNLOAD_HDISK</td><td>0x9c</td><td>远程卸载硬盘</td></tr><tr><td>MINOR_LOCAL_OPERATE_LOCK</td><td>p6x0</td><td>本地操作锁定</td></tr><tr><td>MINOR_LOCAL_OPERATE_UNLOCK</td><td>0x9e</td><td>本地操作解除锁定</td></tr><tr><td>MINOR_REMOTE_BYPASS</td><td>Opxo</td><td>远程旁路</td></tr><tr><td>MINOR_REMOTE_UNBYPASS</td><td>0xd1</td><td>远程旁路恢复</td></tr><tr><td>MINOR_REMOTE_SET_ALARMIN_CFG</td><td>0xd2</td><td>远程设置报警输入参数</td></tr><tr><td>MINOR_REMOTE_GET_ALARMIN_CFG</td><td>EpxO</td><td>远程获取报警输入参数</td></tr><tr><td>MINOR_REMOTE_SET_ALARMOUT_CFG</td><td>0xd4</td><td>远程设置报警输出参数</td></tr><tr><td>MINOR_REMOTE_GET_ALARMOUT_CFG</td><td>0xd5</td><td>远程获取报警输出参数</td></tr><tr><td>MINOR_REMOTE_ALARMOUT_OPEN_MAN</td><td>9px0</td><td>远程手动开启报警输出</td></tr><tr><td>MINOR_REMOTE_ALARMOUT_CLOSE_MAN</td><td>Lpxo</td><td>远程手动关闭报警输出</td></tr><tr><td>MINOR_REMOTE_ALARM_ENABLE_CFG</td><td>Oxd8</td><td>远程设置报警主机的 RS485 串口使能状态</td></tr><tr><td>MINOR_DBDATA_OUTPUT</td><td>6px0</td><td>导出数据库记录</td></tr><tr><td>MINOR_DBDATA_INPUT</td><td>epxo</td><td>导入数据库记录</td></tr><tr><td>MINOR_MU_SWITCH</td><td>Oxdb</td><td>级联切换</td></tr></table></body></html>  

<html><body><table><tr><td>MINOR_MU_PTZ</td><td>opxo</td><td>级联 PTZ 控制</td></tr><tr><td>MINOR_LOCAL_CONF_REB_RAID</td><td>0x101</td><td>本地配置自动重建</td></tr><tr><td>MINOR_LOCAL_CONF_SPARE</td><td>0x102</td><td>本地配置热备</td></tr><tr><td>MINOR_LOCAL_ADD_RAID</td><td>0x103</td><td>本地创建阵列</td></tr><tr><td>MINOR_LOCAL_DEL_RAID</td><td>0x104</td><td>本地删除阵列</td></tr><tr><td>MINOR_LOCAL_MIG_RAID</td><td>0x105</td><td>本地迁移阵列</td></tr><tr><td>MINOR_LOCAL_REB_RAID</td><td>0x106</td><td>本地手动重建阵列</td></tr><tr><td>MINOR_LOCAL_QUICK_CONF_RAID</td><td>0x107</td><td>本地一键配置</td></tr><tr><td>MINOR_LOCAL_ADD_VD</td><td>0x108</td><td>本地创建虚拟磁盘</td></tr><tr><td>MINOR_LOCAL_DEL_VD</td><td>0x109</td><td>本地删除虚拟磁盘</td></tr><tr><td>MINOR_LOCAL_RP_VD</td><td>0x10a</td><td>本地修复虚拟磁盘</td></tr><tr><td>MINOR_LOCAL_FORMAT_EXPANDVD</td><td>0x10b</td><td>本地扩展虚拟磁盘扩容</td></tr><tr><td>MINOR_LOCAL_RAID_UPGRADE</td><td>0x10c</td><td>本地 raid 卡升级</td></tr><tr><td>MINOR_LOCAL_STOP_RAID</td><td>0x10d</td><td>本地暂停 RAID 操作(即安全拔盘)</td></tr><tr><td>MINOR_REMOTE_CONF_REB_RAID</td><td>0x111</td><td>远程配置自动重建</td></tr><tr><td>MINOR_REMOTE_CONF_SPARE</td><td>0x112</td><td>远程配置热备</td></tr><tr><td>MINOR_REMOTE_ADD_RAID</td><td>0x113</td><td>远程创建阵列</td></tr><tr><td>MINOR_REMOTE_DEL_RAID</td><td>0x114</td><td>远程删除阵列</td></tr><tr><td>MINOR_REMOTE_MIG_RAID</td><td>0x115</td><td>远程迁移阵列</td></tr><tr><td>MINOR_REMOTE_REB_RAID</td><td>0x116</td><td>远程手动重建阵列</td></tr><tr><td>MINOR_REMOTE_QUICK_CONF_RAID</td><td>0x117</td><td>远程一键配置</td></tr><tr><td>MINOR_REMOTE_ADD_VD</td><td>0x118</td><td>远程创建虚拟磁盘</td></tr><tr><td>MINOR_REMOTE_DEL_VD</td><td>0x119</td><td>远程删除虚拟磁盘</td></tr><tr><td>MINOR_REMOTE_RP_VD</td><td>0x11a</td><td>远程修复虚拟磁盘</td></tr><tr><td>MINOR_REMOTE_FORMAT_EXPANDVD</td><td>0x11b</td><td>远程虚拟磁盘扩容</td></tr><tr><td>MINOR_REMOTE_RAID_UPGRADE</td><td>0x11c</td><td>远程raid 卡升级</td></tr><tr><td>MINOR_REMOTE_STOP_RAID</td><td>0x11d</td><td>远程暂停 RAID 操作(即安全拔盘)</td></tr><tr><td>MINOR_LOCAL_START_PIC_REC</td><td>0x121</td><td>本地开始抓图</td></tr><tr><td>MINOR_LOCAL_STOP_PIC_REC</td><td>0x122</td><td>本地停止抓图</td></tr><tr><td>MINOR_LOCAL_SET_SNMP</td><td>0x125</td><td>本地配置SNMP</td></tr><tr><td>MINOR_LOCAL_TAG_OPT</td><td>0x126</td><td>本地标签操作</td></tr><tr><td>MINOR_REMOTE_START_PIC_REC</td><td>0x131</td><td>远程开始抓图</td></tr><tr><td>MINOR_REMOTE_STOP_PIC_REC</td><td>0x132</td><td>远程停止抓图</td></tr><tr><td>MINOR_REMOTE_SET_SNMP</td><td>0x135</td><td>远程配置SNMP</td></tr><tr><td>MINOR_REMOTE_TAG_OPT</td><td>0x136</td><td>远程标签操作</td></tr></table></body></html>  

<html><body><table><tr><td>MINOR_REMOTE_TAG_OPT</td><td>0x136</td><td>远程标签操作</td></tr><tr><td>MINOR_LOCAL_VOUT_SWITCH</td><td>0x140</td><td>本地输出口切换操作</td></tr><tr><td>MINOR_STREAM_CABAC</td><td>0x141</td><td>码流压缩性能选项配置操作</td></tr><tr><td>MINOR_LOCAL_SPARE_OPT</td><td>0x142</td><td>本地 N+1热备相关操作</td></tr><tr><td>MINOR_REMOTE_SPARE_OPT</td><td>0x143</td><td>远程N+1热备相关操作</td></tr><tr><td>MINOR_LOCAL_IPCCFGFILE_OUTPUT</td><td>0x144</td><td>本地导出 ipc 配置文件</td></tr><tr><td>MINOR_LOCAL_IPCCFGFILE_INPUT</td><td>0x145</td><td>本地导入ipc 配置文件</td></tr><tr><td>MINOR_LOCAL_IPC_UPGRADE</td><td>0x146</td><td>本地升级IPC</td></tr><tr><td>MINOR_REMOTE_IPCCFGFILE_OUTPUT</td><td>0x147</td><td>远程导出 ipc 配置文件</td></tr><tr><td>MINOR_REMOTE_IPCCFGFILE_INPUT</td><td>0x148</td><td>远程导入ipc 配置文件</td></tr><tr><td>MINOR_REMOTE_IPC_UPGRADE</td><td>0x149</td><td>远程升级IPC</td></tr><tr><td>MINOR_LOCAL_LOAD_HDISK</td><td>0x300</td><td>本地加载硬盘</td></tr><tr><td>MINOR_LOCAL_DELETE_HDISK</td><td>0x301</td><td>本地删除异常不存在的硬盘</td></tr><tr><td>MINOR_REMOTE_CREATE_STORAGE_POOL</td><td>0x211c</td><td>远程添加存储池</td></tr><tr><td>MINOR_REMOTE_DEL_STORAGE_POOL</td><td>0x211d</td><td>远程删除存储池</td></tr><tr><td>MINOR_REMOTE_DEL_PIC</td><td>0x2120</td><td>远程删除图片数据</td></tr><tr><td>MINOR_REMOTE_DEL_RECORD</td><td>0x2121</td><td>远程删除录像数据</td></tr><tr><td>MINOR_REMOTE_CLOUD_ENABLE</td><td>0x2123</td><td>远程设置云存储启用</td></tr><tr><td>MINOR_REMOTE_CLOUD_DISABLE</td><td>0x2124</td><td>远程设置云存储禁用</td></tr><tr><td>MINOR_REMOTE_CLOUD_MODIFY_PARAM</td><td>0x2125</td><td>远程修改云存储池参数</td></tr><tr><td>MINOR_REMOTE_CLOUD_MODIFY_VOLUME</td><td>0x2126</td><td>远程修改云存储池容量</td></tr></table></body></html>  

表 6.5 附加日志次类型  


<html><body><table><tr><td>主类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MAJOR_INFORMATION</td><td>0x4</td><td>附加信息</td></tr><tr><td>次类型的宏定义</td><td>宏定义值</td><td>含义</td></tr><tr><td>MINOR_HDD_INFO</td><td>0xa1</td><td>硬盘信息</td></tr><tr><td>MINOR_SMART_INFO</td><td>0xa2</td><td>S.M.A.R.T信息</td></tr><tr><td>MINOR_REC_START</td><td>0xa3</td><td>开始录像</td></tr><tr><td>MINOR_REC_STOP</td><td>0xa4</td><td>停止录像</td></tr><tr><td>MINOR_REC_OVERDUE</td><td>0xa5</td><td>过期录像删除</td></tr><tr><td>MINOR_LINK_START</td><td>0xa6</td><td>连接前端设备</td></tr><tr><td>MINOR_LINK_STOP</td><td>0xa7</td><td>断开前端设备</td></tr><tr><td>MINOR_NET_DISK_INFO</td><td>0xa8</td><td>网络硬盘信息</td></tr><tr><td>MINOR_RAID_INFO</td><td>0xa9</td><td>raid 相关信息</td></tr></table></body></html>  

<html><body><table><tr><td>MINOR_RUN_STATUS_INFO</td><td>Oxaa</td><td>系统运行状态信息</td></tr><tr><td>MINOR_PIC_REC_START</td><td>0xb3</td><td>开始抓图</td></tr><tr><td>MINOR_PIC_REC_STOP</td><td>0xb4</td><td>停止抓图</td></tr><tr><td>MINOR_PIC_REC_OVERDUE</td><td>0xb5</td><td>过期图片文件删除</td></tr><tr><td>MINOR_CLIENT_LOGIN</td><td>0xb6</td><td>登录服务器成功</td></tr><tr><td>MINOR_CLIENT_RELOGIN</td><td>0xb7</td><td>重新登录服务器</td></tr><tr><td>MINOR_CLIENT_LOGOUT</td><td>0xb8</td><td>退出服务器成功</td></tr><tr><td>MINOR_CLIENT_SYNC_START</td><td>0xb9</td><td>录像同步开始</td></tr><tr><td>MINOR_CLIENT_SYNC_STOP</td><td>eqxo</td><td>录像同步终止</td></tr><tr><td>MINOR_CLIENT_SYNC_SUCC</td><td>Oxbb</td><td>录像同步成功</td></tr><tr><td>MINOR_CLIENT_SYNC_EXCP</td><td>Oxbc</td><td>录像同步异常</td></tr><tr><td>MINOR_GLOBAL_RECORD_ERR_INFO</td><td>Oxbd</td><td>全局错误记录信息</td></tr><tr><td>MINOR_BUFFER_STATE</td><td>Oxbe</td><td>缓冲区状态日志记录</td></tr><tr><td>MINOR_DISK_ERRORINFO_V2</td><td>Oxbf</td><td>硬盘错误详细信息V2</td></tr><tr><td>MINOR_ACCESSORIES_MESSAGE</td><td>0xc6</td><td>配件板信息</td></tr><tr><td>MINOR_EZVIZ_OPERATION</td><td>Oxcc</td><td>萤石运行状态</td></tr></table></body></html>  