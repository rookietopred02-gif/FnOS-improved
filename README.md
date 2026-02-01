# FnOS Explorer

一个用于管理和浏览路径遍历漏洞目标的 Web 应用程序。

## 功能特性

- 📥 **批量导入** - 支持从 CSV 文件批量导入目标资产
- 🔍 **多线程扫描** - 可配置的并发扫描（默认 32 线程）
- 🌍 **地理位置** - 显示目标的国家、地区和城市信息
- 📁 **文件浏览** - 浏览漏洞目标的文件系统
- 👁️ **文件预览** - 支持图片、文本、日志等文件的在线预览
- 📦 **批量下载** - 支持打包下载整个目录
- 🔗 **WebDAV 快捷跳转** - 快速访问 WebDAV 目录
- 🔄 **实时统计** - 自动更新扫描统计数据
- 🔎 **高级搜索** - 支持按状态、IP、城市等条件筛选

## 安装

### 环境要求

- Python 3.7+
- pip

### 安装步骤

1. 克隆或下载项目

2. 创建虚拟环境（推荐）
```bash
python -m venv .venv
```

3. 激活虚拟环境
```bash
# Windows
.venv\Scripts\activate

# Linux/Mac
source .venv/bin/activate
```

4. 安装依赖
```bash
pip install -r requirements.txt
```

## 使用方法

### 启动应用

```bash
python app.py
```

应用将在 `http://localhost:5000` 启动

### 导入目标

1. **单文件导入**
   - 在首页选择 CSV 文件
   - 点击"单文件扫描"

2. **批量导入**
   - 将 CSV 文件放入 `csv_imports` 目录
   - 点击"一键导入所有 CSV"
   - 点击"开始检查可用性"进行扫描

### CSV 格式

CSV 文件需包含以下列（支持逗号或 Tab 分隔）：

```csv
host,ip,port,protocol,country,region,city
https://183.23.162.198:9000,183.23.162.198,9000,https,CN,广东省,Dongguan
dragonsun.top:5666,112.17.144.152,5666,http,CN,浙江省,Hangzhou
```

**必需字段：**
- `ip` - IP 地址
- `port` - 端口号

**可选字段：**
- `host` - 主机名或域名
- `protocol` - 协议（http/https，默认 http）
- `country` - 国家代码（如 CN, US）
- `region` - 省份/州
- `city` - 城市

### 扫描配置

点击"开始检查可用性"按钮可配置：
- **并发线程数**：1-100（默认 32）
- 线程数越多扫描越快，但会占用更多资源

### 文件浏览

1. 点击"浏览文件"进入文件浏览器
2. 点击"WebDAV"快速跳转到 WebDAV 目录
3. 使用面包屑导航或快捷跳转按钮切换目录
4. 文件操作：
   - **新窗口** - 在新标签页打开
   - **预览** - 在弹窗中预览
   - **下载** - 下载到本地（文件名格式：`{ID}_{原文件名}`）

## 项目结构

```
.
├── app.py              # Flask 应用主文件
├── database.py         # 数据库操作
├── scanner.py          # 扫描逻辑
├── file_ops.py         # 文件操作
├── templates/          # HTML 模板
│   ├── base.html
│   ├── index.html
│   └── explorer.html
├── csv_imports/        # CSV 导入目录
├── requirements.txt    # Python 依赖
└── vuln_targets.db     # SQLite 数据库（自动创建）
```

## 技术栈

- **后端**: Flask, SQLite
- **前端**: Bootstrap 5, JavaScript
- **扫描**: 多线程并发
- **文件解析**: BeautifulSoup4, Pandas

## 注意事项

⚠️ **安全警告**
- 本工具仅用于授权的安全测试
- 请勿用于非法用途
- 使用前请确保已获得目标系统的授权

## 许可证

本项目仅供学习和研究使用。
