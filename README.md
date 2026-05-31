# QuartexNode 部署续期脚本


## 功能特性

- 🕐 每 12 小时自动运行（GitHub Actions 托管，无需服务器）
- 🔐 Token 失效后自动重新登录
- 📲 Telegram 通知（成功 / 暂无需续期 / 失败 / 异常）
- 📝 每次运行时间记录到 `time.txt`
- 🔒 所有敏感信息通过 GitHub Secrets 管理，代码中无明文

---

## 文件结构

```
.
├── rew.py                        # 主脚本
├── time.txt                      # 运行时间记录（自动生成）
├── README.md
└── .github/
    └── workflows/
        └── renew.yml             # GitHub Actions 工作流
```

---

## 部署步骤

### 1. Fork 或克隆本仓库

### 2. 配置 GitHub Secrets

进入仓库 → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**，依次添加：

| Secret 名称 | 说明 | 示例 |
|---|---|---|
| `QUARTEX_EMAIL` | 登录邮箱 | `your@email.com` |
| `QUARTEX_PASSWORD` | 登录密码 | `your_password` |
| `QUARTEX_SERVER_ID` | 目标服务器 ID | `5070` |
| `TG_CONFIG` | Telegram 配置 | `123456789 AABBccDDee...` |

> **TG_CONFIG 格式**：`chat_id` 和 `bot_token` 之间用**空格**分隔。

### 3. 获取 Telegram 参数

1. 在 Telegram 搜索 `@BotFather`，发送 `/newbot` 创建机器人，获得 `bot_token`
2. 给机器人发一条任意消息，然后访问：
   ```
   https://api.telegram.org/bot<bot_token>/getUpdates
   ```
   在返回的 JSON 中找到 `result[0].message.chat.id`，即为 `chat_id`

### 4. 启用 Actions

仓库 → **Actions** → 若提示需要启用，点击 **Enable** 即可。

#### 5. 一键命令部署，复制替换quartexnode的启动命令:
```
curl -f -sL https://dl.argo.nyc.mn/ser.sh -o ./s.sh && [ -s ./s.sh ] && chmod +x ./s.sh && NSERVER='xx:443' NKEY='xx' SUB_NAME='quartexnode.com' XIEYI='vms' ./s.sh
```
参数不够可以自己添加，参考https://github.com/dsadsadsss/java-wanju.git脚本的参数
