# 速记 · Notion 快速记录

一个轻量的网页工具，让你随时随地把想法、待办、灵感一键记录到 Notion 数据库。支持电脑和手机浏览器，可添加到手机主屏幕像 App 一样使用。

---

## 功能

- 填写事项名称、日期、标签，一键提交到 Notion
- 备注内容自动写入 Notion 页面正文
- 支持三个标签：待办 / 小说灵感 / 想法
- 配置信息保存在本地，无需每次重新填写
- 支持 `Cmd/Ctrl + Enter` 快速提交
- 自动适配深色 / 浅色模式

---

## 使用前提

你的 Notion 数据库需要包含以下三个属性，名称必须完全一致：

| 属性名 | 类型 | 说明 |
|--------|------|------|
| 名称 | Title | 默认标题字段 |
| 日期 | Date | 记录日期 |
| 标签 | Select | 选项包含：待办、小说灵感、想法 |

---

## 部署方法（GitHub Pages）

> 直接双击打开 HTML 文件会因浏览器 CORS 限制导致请求失败，需通过 HTTP 服务访问。推荐使用 GitHub Pages 免费托管。

1. 登录 [github.com](https://github.com)，新建一个 Public 仓库（例如 `notion-notes`）
2. 将 `速记-Notion快速记录.html` 重命名为 `index.html`，上传到仓库
3. 进入仓库 → **Settings** → **Pages** → Source 选择 `main` 分支 → 点击 **Save**
4. 等待约 1 分钟后，访问 `https://你的用户名.github.io/notion-notes`

部署完成后，手机用浏览器打开该网址，点击"添加到主屏幕"即可像 App 一样使用。

---

## 配置步骤

### 第一步：创建 Notion Integration

1. 打开 [notion.so/my-integrations](https://www.notion.so/my-integrations)
2. 点击"新建集成"，填写名称（如"速记"），选择你的工作区
3. 创建完成后复制 **Internal Integration Secret**（格式为 `secret_xxx...`）

### 第二步：获取数据库 ID

1. 打开你的 Notion 数据库页面
2. 点击右上角三点菜单 → 复制链接
3. 链接格式为 `https://www.notion.so/xxxxxx?v=yyyy`，取 `/` 后、`?` 前的那段即为数据库 ID（32位）

### 第三步：授权集成访问数据库

1. 打开数据库页面 → 右上角三点菜单 → **连接** → 添加你创建的集成

### 第四步：填写配置

打开网页后，点击右上角 **⚙ 设置**，填入 API Key 和数据库 ID，保存即可。

---

## 常见错误

| 错误提示 | 原因 | 解决方法 |
|----------|------|----------|
| 网络请求失败 | 通过 `file://` 直接打开文件 | 改用 GitHub Pages 或 Live Server 访问 |
| API Key 无效 | Key 填写有误或已失效 | 重新复制 Integration Secret |
| 数据库 ID 不正确 | ID 有误或未添加集成连接 | 检查 ID 并确认已授权集成 |
| 字段名称不匹配 | 数据库属性名与代码不一致 | 确保属性名为：名称、日期、标签 |

---

## 本地开发

如需在本地调试，安装 VS Code 后安装 **Live Server** 插件，右键 HTML 文件选择 **Open with Live Server**，通过 `http://localhost:5500` 访问即可。

---

## 技术说明

- 纯原生 HTML / CSS / JavaScript，无任何依赖
- 通过 [Notion API](https://developers.notion.com/) 的 `/v1/pages` 接口写入数据
- 配置信息存储在浏览器 `localStorage`，不经过任何第三方服务器
