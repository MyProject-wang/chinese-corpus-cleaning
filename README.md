```markdown
# 大规模中文语料清洗与质量评估

## 项目简介
针对中文预训练语言模型的数据需求，提供自动化语料清洗与质量评估工具。支持自动编码检测、非自然语言过滤、脱敏、多维度质量评分，输出高质量语料库。

## 核心功能
- **多编码支持**：自动检测 utf-8、gbk、gb18030、latin-1 编码，解决中文乱码问题
- **自然语言过滤**：基于中文字符占比（≥10%）、文本长度（5-5000）、特殊符号比例过滤非自然语言行（纯数字、乱码、结构化数据等）
- **精确去重**：MD5 哈希去重
- **脱敏**：手机号、邮箱自动替换
- **质量评分**：完整性、流畅性、安全性、敏感词（总分 0-3 分），自动划分高质量（≥2.0）与低质量语料
- **输出分离**：高质量语料保存为 JSON，低质量语料保存为 CSV，并生成质量分布直方图

## 技术栈
- Python 3.11
- pandas、re、hashlib、matplotlib

## 快速开始

### 1. 克隆仓库
```bash
git clone https://github.com/wdp-data/chinese-corpus-cleaner.git
cd chinese-corpus-cleaner
```

### 2. 安装依赖
```bash
pip install -r requirements.txt
```

### 3. 使用内置样例数据运行
项目已提供 100 条混合样例（正常文本 + 垃圾文本），位于 `sample_data/sample_corpus.txt`，可直接运行测试。

打开 `大模型中文预训练语料清洗工具.ipynb`，确保以下路径设置：
```python
data_dir = "./sample_data"   # 使用内置样例
# data_dir = "./你的完整语料目录"  # 切换真实数据时取消注释
```
然后按顺序执行所有 Cell。

### 4. 运行结果示例
- 控制台输出：去重率、平均质量分、高质量比例
- 生成文件：
  - `output/high_quality.json`：高质量语料（总分 ≥ 2.0）
  - `output/low_quality.csv`：低质量语料（总分 < 2.0）
- 可视化：质量分布直方图

## 目录结构
```
.
├── sample_data/
│   └── sample_corpus.txt          # 样例语料（100行）
├── 大模型中文预训练语料清洗工具.ipynb   # 主程序
├── requirements.txt
└── README.md
```

## 注意事项
- 清洗前建议先解压压缩包（如 `.zip` 文件），本工具不会自动解压。
- 自然语言过滤条件（最小长度、中文字符占比等）可根据实际语料调整，详见代码中的 `_is_natural_language` 函数。
- 如需处理完整数据集，请将文本文件放入一个目录，并修改 `data_dir` 指向该目录。
```
