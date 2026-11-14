# Fs20modConverterV3 1.2.7.0

FS19 → FS20（移动版）mod 转换器。UI 使用 HTML + CSS + JS，由本地 http 服务（127.0.0.1）加载进 WebView；转换引擎为原生 Kotlin 管线。

## 文件
- `Fs20modConverterV3_1.2.7.0.apk`：已签名安装包（v3 签名方案，minSdk 31）
- `Fs20modConverterV3_工程源码.zip`：完整工程源码（不含 build 目录与签名密钥）

## 转换规则
- modDesc `descVersion` 40–59 判定为 FS19
- storeItems 的 `xmlFilename` 定位车辆 XML（.xml 后缀大小写不敏感）
- 车辆 `<image>` 封面解析预览，`<brand>` 按 ID 在品牌包 `brands/brand_<id>.png` 中查找（不区分大小写），内置 118 个品牌图标
- 车辆 XML 重命名为 520.xml 起，并同步 modDesc / I3D 引用
- modDesc 标题改为 `FS20_` 前缀
- I3D：`<Files>` 中 `.dds` 引用改 `.png`，以 `$` 开头的行跳过；CustomShader version 4 → 5
- DDS 贴图转 PNG，删除原 dds（车辆重命名 / 标题前缀 / I3D 同步默认开启，无开关）

## 签名
签名密钥不随源码公开。keystore 单独保存在作者本机 `keys/fs20-release.jks`。

## 界面说明
- 仅「转换」「设置」两页，工具页在做完真机验证前隐藏
- Android 15 通过 windowOptOutEdgeToEdgeEnforcement 退出强制全屏，另用 inset 容器兜底，内容不压状态栏

## 日志与崩溃
- 运行轨迹实时写入 `filesDir/run_log.txt`，界面「设置 → 运行日志」可查看与导出
- 未捕获异常生成 `crash_log.txt`，同时写入系统下载目录 `Fs20crash_<时间戳>.txt`，内容含完整堆栈与崩溃前 200 条轨迹
- 记录范围：进程启动、HTTP 服务、WebView 页面加载、JS console、SAF 选择、modDesc 解析、每辆车、每个转换步骤、打包与导出
