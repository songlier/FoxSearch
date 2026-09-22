<p align="center">
  <picture>
    <img alt="FoxSearch" src="https://github.com/user-attachments/assets/3436a599-e2ab-4f3d-a014-793a868dfe56" width=40%>
  </picture>
</p>

<p align="center">一款本地部署的 AI 文件搜索工具，支持图片、视频的语义与 OCR 文字检索</p>

<br>

## 功能  

- 中文语义搜索图片和视频
- OCR 文字搜索与文件名搜索
- 文字搜图片
- 以图搜图片
- 文字搜视频
- 以图搜视频
- 图文相似度计算

<br>


<p align="center">
  <picture>
    <img alt="FoxSearch" src="https://github.com/user-attachments/assets/46b0f1d4-a893-411c-a496-b9d6a3fa607e" width=100%>
  </picture>
</p>

<br>

## 特色  

- 视频相似片段定位
- 图片、视频和 OCR 索引
- 增量扫描与失败记录重试
- 无效索引检测与清理
- 数据库路径批量编辑
- 图片和视频文件预览
- OCR 识别结果展示、搜索词高亮和全文复制
- 超大图片缩略图加载，降低浏览器卡顿
- 大规模结果虚拟列表和有限缓存
- 浅色模式、深色模式和响应式布局

### AI 搜索与 OCR

FoxSearch 使用中文 CLIP 模型理解图片和视频中的视觉内容，可以通过自然语言搜索场景、对象、角色和风格。

OCR 功能可以识别图片中的文字，并支持通过文字片段、文件名和路径进行检索。

### 响应式网页界面

网页界面兼容电脑宽屏和手机竖屏：

- 宽屏模式适合大量结果浏览。
- 窄屏模式适合手机触控操作。
- 支持响应式搜索栏、标签页和结果布局。
- 支持自定义每行显示数量。
- 支持手机触控、滚轮缩放和图片拖动。
- 支持浅色与深色模式。

### 文件预览

图片和视频均支持独立预览：

- 图片缩放、拖动和平移。
- 双击放大或恢复原始预览状态。
- 视频从检索命中的时间点开始播放。
- 支持打开文件和定位到资源管理器。
- 支持复制链接、复制原图和复制视频文件。
- OCR 结果可以在预览窗口中查看完整内容。
- 支持调整 OCR 字号、自动换行和复制全文。

### 数据库编辑与迁移

FoxSearch 支持批量修改图片、视频和 OCR 索引中的文件路径。

当素材从一台电脑迁移到另一台电脑，或磁盘盘符发生变化时，可以直接替换索引中的旧路径，继续使用已有的视觉特征和 OCR 识别结果，减少重新扫描和重新识别的时间。

### 高级版本支持

- 文件浏览和多用户管理功能
- 多个素材根目录。
- 目录树和文件夹浏览。
- 图片与视频混合浏览。
- 面包屑路径导航。
- 不同用户独立的素材路径和忽略规则。
- 用户密码和浏览器登录记忆。
- 不同浏览器同时登录不同用户。
- 普通用户只能访问自己的文件。
- 管理员访问和管理所有用户的素材。
- 【高级版本】请通过邮件联系或赞赏码备注接收邮箱

## 硬件要求

FoxSearch 支持 CPU 与 NVIDIA 10 系列、20 系列、30 系列和 40 系列显卡的 GPU 加速。

## 安装与启动

Windows：解压后运行
```
.\start.bat
```

默认访问地址：
```
http://127.0.0.1:8082
```

## 配置
通过设置 `.env` 文件进行配置
管理员配置为必填项：

```
ASSETS_PATH=D:/Pictures,E:/Media
IGNORE_STRINGS=thumb,avatar,__MACOSX,icons,cache
PASSWORD=1234

HOST=127.0.0.1
PORT=8082
INDEX_DIR=./data
```

- `ASSETS_PATH`：需要搜索的素材目录，多个路径使用英文逗号分隔。
- `IGNORE_STRINGS`：需要忽略的路径或文件名关键词。
- `PASSWORD`：管理员数字密码。
- `PORT`：网页服务端口。
- `DEVICE`：使用 `auto`、`cuda` 或 `cpu`。

如需启用 OCR，可配置：

```
ENABLE_OCR=true
OCR_THREADS=4
PADDLEOCR_EXE=./models/PaddleOCR-json/PaddleOCR-json.exe
PADDLEOCR_MODELS=./models/PaddleOCR-json/models
```

## 远程访问

FoxSearch 可以通过 SakuraFrp 等内网穿透工具映射到公网，实现手机或其他设备远程访问。

在 `.env` 中设置端口：

```
HOST=127.0.0.1
PORT=8082
```

在 SakuraFrp 中创建 TCP 隧道：

```
隧道类型：TCP
本地 IP：127.0.0.1
本地端口：8082
```

启动 FoxSearch 和 SakuraFrp 后，使用 SakuraFrp 分配的公网地址访问：

```
http://公网地址:远程端口
```

如果 SakuraFrp 客户端和 FoxSearch 不在同一台电脑上，需要将 FoxSearch 的 `HOST` 设置为：

```
HOST=0.0.0.0
```

然后将隧道本地 IP 设置为 FoxSearch 所在电脑的局域网 IP。

远程访问前请务必：

- 设置 SakuraFrp 通道密码
- 设置管理员和普通用户密码。
- 限制防火墙开放范围。
- 不要将未配置密码的服务直接暴露到公网。
- 仅在可信网络中使用管理员账号。

更多 SakuraFrp 配置可参考：

https://doc.natfrp.com/app/http.html

## 数据文件

默认数据保存在 `data` 目录：

```
data/
  image_index.npz
  video_index.pkl
  ocr_index.jsonl
  cache.json
```

- `image_index.npz`：图片视觉特征索引。
- `video_index.pkl`：视频片段特征索引。
- `ocr_index.jsonl`：OCR 识别文字索引。
- `cache.json`：失败记录和可重新计算的缓存。

## 致谢

https://github.com/chn-lee-yumi/MaterialSearch

https://github.com/yeqizhang/PaddleOCR-json

https://github.com/hiroi-sora/Umi-OCR

## 支持

感谢每一位使用、反馈和支持 FoxSearch 的用户

欢迎提 Issue ，请点免费 Star
