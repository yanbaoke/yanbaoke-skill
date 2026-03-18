# 研报客 Research Report Download Skill

[![Version](https://img.shields.io/badge/version-2.0.4-blue)](https://github.com)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

从研报客平台（pc.yanbaoke.cn）搜索和下载研究报告的 Claude Code Skill。平台覆盖 5000+ 家机构、五百万+ 份行业深度研究报告。

## 功能特性

- **搜索研报** - 无需 API Key，免费搜索百万级研究报告
- **下载报告** - 获取完整 PDF 研究报告（需要 API Key）
- **多维度筛选** - 支持按机构、报告类型、股票、日期范围、页数等条件筛选
- **双语支持** - 中文界面和文档，便于国内用户使用

## 安装

### 前置要求

- Node.js 18+
- Claude Code with OpenClaw

### 安装步骤

详见 [instruct.md](instruct.md) 获取完整安装指南。

```bash
# 创建目录
mkdir -p ~/.openclaw/skills/yanbaoke/scripts

# 下载 Skill 定义
curl -fSL https://app.quzili.cn/skills/yanbaoke/SKILL.md -o ~/.openclaw/skills/yanbaoke/SKILL.md

# 下载脚本
curl -fSL https://app.quzili.cn/skills/yanbaoke/scripts/search.mjs -o ~/.openclaw/skills/yanbaoke/scripts/search.mjs
curl -fSL https://app.quzili.cn/skills/yanbaoke/scripts/download.mjs -o ~/.openclaw/skills/yanbaoke/scripts/download.mjs
```

### 配置 API Key（可选）

如需下载报告，请前往 [https://pc.yanbaoke.cn/openclaw](https://pc.yanbaoke.cn/openclaw) 获取 API Key：

```bash
echo 'export YANBAOKE_API_KEY="sk-your-api-key"' >> ~/.bashrc
source ~/.bashrc
```

## 使用方法

### 搜索报告

```bash
# 基础搜索
node ~/.openclaw/skills/yanbaoke/scripts/search.mjs "人工智能"

# 指定数量
node ~/.openclaw/skills/yanbaoke/scripts/search.mjs "新能源汽车" -n 20

# 全文搜索
node ~/.openclaw/skills/yanbaoke/scripts/search.mjs "深度分析" --type content

# 机构筛选
node ~/.openclaw/skills/yanbaoke/scripts/search.mjs "半导体" --org "中信证券,华泰证券"

# 日期范围筛选
node ~/.openclaw/skills/yanbaoke/scripts/search.mjs "光伏" --start-date "2024-01-01" --end-date "2024-12-31"

# 页数筛选
node ~/.openclaw/skills/yanbaoke/scripts/search.mjs "深度分析" --min-pages 30 --max-pages 100
```

### 下载报告

```bash
# 使用环境变量中的 API Key
node ~/.openclaw/skills/yanbaoke/scripts/download.mjs <uuid>

# 直接传入 API Key
node ~/.openclaw/skills/yanbaoke/scripts/download.mjs <uuid> "sk-your-api-key"
```

## 项目结构

```
yanbaoke-skill/
├── SKILL.md          # Skill 定义和文档
├── README.md         # 项目说明
├── instruct.md       # 安装指南
├── _meta.json        # Skill 元数据
└── scripts/
    ├── search.mjs    # 搜索脚本
    └── download.mjs  # 下载脚本
```

## API 参考

### 搜索 API

```
GET https://api.yanbaoke.cn/skills/search_report
```

### 下载 API

```
GET https://api.yanbaoke.cn/skills/report_download/{uuid}
Authorization: Bearer YOUR_API_KEY
```

## 定价

| 用户类型 | 首次下载 | 再次下载 |
|---------|---------|---------|
| 用户 | 10 个豆 | 免费 |

每份报告仅收费一次，已购买报告可重复下载。

## 相关链接

- [研报客平台](https://pc.yanbaoke.cn)
- [API Key 获取](https://pc.yanbaoke.cn/openclaw)
- [详细文档](SKILL.md)

## 许可证

MIT License
