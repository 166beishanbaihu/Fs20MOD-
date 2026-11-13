# Fs20modConverterV3 1.2.1.0

FS19 → FS20（移动版）mod 转换器。UI 使用 HTML + CSS + JS，由本地 http 服务（127.0.0.1）加载进 WebView；转换引擎为原生 Kotlin 管线。

## 文件
- `Fs20modConverterV3_1.2.1.0.apk`：已签名安装包（v3 签名方案，minSdk 31）
- `Fs20modConverterV3_工程源码.zip`：完整工程源码（不含 build 目录与签名密钥）

## 转换规则
- modDesc `descVersion` 40–59 判定为 FS19
- storeItems 的 `xmlFilename` 定位车辆 XML（.xml 后缀大小写不敏感）
- 车辆 `<image>` 封面解析预览，`<brand>` 按 ID 在品牌包 `brands/brand_<id>.png` 中查找（不区分大小写），内置 118 个品牌图标
- 车辆 XML 重命名为 520.xml 起，并同步 modDesc / I3D 引用
- modDesc 标题改为 `FS20_` 前缀
- I3D：`<Files>` 中 `.dds` 引用改 `.png`，以 `$` 开头的行跳过；CustomShader version 4 → 5
- DDS 贴图转 PNG，删除原 dds

## 签名
签名密钥不随源码公开。keystore 单独保存在作者本机 `keys/fs20-release.jks`。
