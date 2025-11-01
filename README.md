# 🌍 看看你那里的天空

*LOOK AT THE SKY WHERE YOU ARE — 一个基于 IPFS 的全球去中心化天空档案计划*

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![IPFS](https://img.shields.io/badge/IPFS-Enabled-blue.svg)](https://ipfs.io)
[![4EVERLAND](https://img.shields.io/badge/Storage-4EVERLAND-green.svg)](https://4everland.org)

</div>

---

## 📖 项目简介

> **"每一片天空,都是一个世界的时间戳；每一次上传,都是一次存在的证明。"**

本项目邀请世界各地的人们上传**此刻头顶的天空**，并填写**姓名、所在地、此时的想法/心情**。所有图片与元信息通过 **4EVERLAND** 自动存储并 **Pin 到 IPFS**，生成唯一 **CID（内容寻址标识符）**。

天空是人类唯一共同抬头时共享的视觉场域，它不属于任何国家、公司或数据库。本项目将天空转化为一种**去中心化、不可删除、可永久引用的公共档案**。

它不是社交网络，不追求点赞或算法曝光；它是一种分布式记录方式：**"我在某时某地真实存在过。"**

### ✨ 核心特性

- ✅ **去中心化存储** - 不依赖中心化云存储
- ✅ **内容寻址** - 每张图片都有不可伪造的 CID
- ✅ **永久访问** - 任意 IPFS 网关可长期访问
- ✅ **开放数据** - 数据可被他人复刻、验证、重混
- ✅ **去平台化记忆** - 真正属于互联网的公共档案

---

## 🔗 在线体验

**网站入口：** https://skyproject_static-xux1ub50-yangliu044.4everland.app/

---

## 🛰 为什么使用 IPFS + 4EVERLAND？

| 传统存储 | 去中心化存储 |
|----------|--------------|
| URL 指向服务器位置 | CID 指向内容本身 |
| 平台可删除、屏蔽、闭源 | 内容分布到节点网络，不依赖单一主机 |
| 需信任平台 | 只需信任哈希 |
| 数据迁移即链接失效 | IPFS 可跨网关永久访问 |

### 访问示例

任何上传的图片都可以通过多个 IPFS 网关访问：

```
https://ipfs.4everland.io/ipfs/<CID>
https://ipfs.io/ipfs/<CID>
https://dweb.link/ipfs/<CID>
```

---

## 🏗 系统架构

```
前端（静态 HTML/JS）
        ↓
后端（Vercel Serverless API）
        ↓
存储（4EVERLAND S3 Bucket）
        ↓
IPFS 网络（自动 Pin）
        ↓
结果：生成 CID，可通过任意网关访问
```

详细架构图见：`/assets/architecture.svg`

---

## 🛠 技术栈

| 层级 | 使用技术 |
|------|----------|
| **前端** | Vanilla JS + HTML/CSS |
| **后端** | Vercel Serverless Functions (Node.js) |
| **存储** | 4EVERLAND S3 endpoint + 自动 IPFS Pin |
| **上传 SDK** | `@aws-sdk/client-s3` |
| **表单解析** | `busboy` |

---

## 📡 API 文档

### `POST /api/upload`

上传天空图片与元信息，返回 CID。

**请求参数：**

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `file` | File | ✅ | 天空图片文件 |
| `name` | String | ❌ | 上传者姓名 |
| `location` | String | ❌ | 所在地点 |
| `thoughts` | String | ❌ | 此刻的想法/心情 |

**返回示例：**

```json
{
  "ok": true,
  "cid": "bafybeid4jk2jxyw...",
  "gateway": "https://ipfs.4everland.io/ipfs/bafybeid4jk2jxyw...",
  "name": "Alice",
  "location": "Tokyo, Japan",
  "thoughts": "It looks like rain today."
}
```

---

## 🧬 元信息结构

每个上传的天空图片都包含以下元数据：

| 字段 | 类型 | 示例 |
|------|------|------|
| `name` | String | `"Alice"` |
| `location` | String | `"Tokyo, Japan"` |
| `thoughts` | String | `"云层很低，像温柔的屋顶。"` |
| `uploaded_at` | ISO 8601 | `"2025-01-06T10:22:11Z"` |

---

## 📦 本地部署

### 前端部署

前端是纯静态页面，可以托管到任意静态服务：

- **4EVERLAND** ✅ 推荐
- **GitHub Pages**
- **Vercel**
- **Netlify**
- **IPFS 网关**

只需上传 `index.html` 及相关静态资源即可。

### 后端部署（Vercel）

1. **克隆仓库**
   ```bash
   git clone https://github.com/your-username/sky-archive.git
   cd sky-archive
   ```

2. **安装依赖**
   ```bash
   npm install
   ```

3. **配置环境变量**

   在 Vercel 项目设置中添加以下环境变量：
   
   ```
   S3_ENDPOINT=your-4everland-endpoint
   S3_ACCESS_KEY_ID=your-access-key
   S3_SECRET_ACCESS_KEY=your-secret-key
   S3_BUCKET_NAME=your-bucket-name
   S3_REGION=your-region
   ```

4. **部署到 Vercel**
   ```bash
   vercel --prod
   ```

---

## 🔧 配置 4EVERLAND

1. 注册 [4EVERLAND](https://4everland.org) 账号
2. 创建 S3 Bucket 并启用 IPFS Pin
3. 获取 Access Key 和 Secret Key
4. 将凭据配置到后端环境变量

---

## 🤝 贡献指南

欢迎任何形式的贡献！

1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的改动 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启一个 Pull Request

---

## 📝 许可证

本项目采用 **MIT License** 授权 - 查看 [LICENSE](LICENSE) 文件了解详情。

您可以自由：
- ✅ 使用
- ✅ 修改
- ✅ 分发
- ✅ 商业使用

---

## 👤 作者

**Yang Liu（杨柳）**

- GitHub: [@your-username](https://github.com/your-username)
- Email: your-email@example.com

---

## 🙏 致谢

- **IPFS** - 去中心化存储协议
- **4EVERLAND** - IPFS 基础设施提供商
- **Vercel** - Serverless 部署平台

---

## 📌 引用与署名

若用于展览、出版或学术引用，请保留署名与项目链接：

```
Yang Liu. (2025). Look at the Sky Where You Are. 
GitHub repository: https://github.com/your-username/sky-archive
```

---

<div align="center">

**愿你所在之处也有一片好看的天空。**

*Look up, upload, and let the sky store itself.*

🌤️ ☁️ 🌥️ ⛅ 🌦️ 🌧️ ⛈️ 🌩️ 🌨️

</div>
