# 图像标注工具 - wd14_tagger

基于 SmilingWolf 的 wd14-tagger 的本地化实现，用于为图片生成描述性标签（tags）。

## ✨ 功能特性

- 一键式批处理脚本快速执行
- 支持批量处理整个文件夹内的图片
- 生成包含英文标签的文本文件
- 针对国内用户的阿里云镜像加速选项
- 可配置阈值/批量大小/文件格式等参数

## 📂 项目结构
    ├── models/ # 模型存放目录（需自行下载）
    ├── setup.bat # 环境配置脚本（标准版）
    ├── setup_阿里云加速.bat # 环境配置脚本（阿里云加速版）
    ├── run_tagger.bat # 标注执行脚本
    └── tagger.py # 核心标注脚本


## 🛠️ 安装与配置

### 安装依赖环境：

- 标准安装（推荐国外用户）：  
  `setup.bat`
- 阿里云镜像安装（推荐国内用户）：  
  `setup_阿里云加速.bat`

### 下载模型文件：

1. 访问 SmilingWolf 的 Hugging Face 页面
2. 下载 ONNX 格式模型（推荐 wd-v1-4-vit-tagger-v2）
3. 解压后放入 models 文件夹

## 🚀 使用说明

1. 双击运行 `run_tagger.bat`
2. 按提示输入要标注的图片目录路径
3. 程序将自动执行标注过程
4. 完成后，图片同级目录会生成同名文本文件（如 image.jpg.txt）

## ⚙️ 自定义参数

在 `run_tagger.bat` 中可直接修改的参数：

| 参数 | 默认值 | 说明 |
|------|--------|------|
| modelDir | .\models\ | 模型存储路径 |
| batchSize | 1 | 批量处理大小（显存不足时设为1） |
| threshold | 0.27 | 标签置信度阈值（0.01~0.99） |
| captionExtension | .txt | 标签文件扩展名 |
| replaceUnderscores | true | 是否将下划线转为空格 |
| maxDataLoaderWorkers | 4 | 数据加载线程数 |

## 📌 注意事项

### 模型下载：

- 必须从 SmilingWolf 的 Hugging Face 下载 ONNX 格式模型
- 解压后需保持原始文件名 `model.onnx` 和 `selected_tags.csv`

### 文件处理：

- 支持 JPG/PNG/WEBP 格式
- 可递归处理子目录
- 原图片不会被修改

### 性能建议：

- GPU显存小于6GB时建议`batchSize=1`
- 大图集处理需时较长（处理进度显示在控制台）

### 输出格式：

- 默认生成逗号分隔的英文标签
- 示例输出：`1girl, solo, looking at viewer, smile`

## 💡 示例命令

直接命令行执行（需先激活虚拟环境）：

```bash
python tagger.py "D:\my_images" \
  --model_dir ".\models\" \
  --batch_size 4 \
  --thresh 0.3 \
  --caption_extension ".caption"