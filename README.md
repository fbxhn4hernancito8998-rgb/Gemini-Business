# Gemini Business 自动注册工具

邮箱注册功能来自： DuckMail https://linux.do/u/syferie/summary
注册成功后的登录地址：https://business.gemini.google/
邮件登录地址：https://ducktempmail.netlify.app/

## 功能特性

- **浏览器自动化**: 基于 DrissionPage 的 Chromium 自动化
- **代理管理**: 集成 Clash 代理，自动检测可用节点
- **临时邮箱**: 通过 DuckMail API 自动生成临时邮箱
- **自动验证**: 自动获取并填入邮箱验证码

## 项目结构

```
├── auto_register_browser.py   # 主自动化脚本
├── clash_manager.py           # Clash 代理管理器
├── mail_client.py             # 临时邮箱客户端
├── local.yaml.example         # Clash 配置模板
├── requirements.txt           # Python 依赖
├── Run.bat                    # 快速启动脚本
└── 一键配置环境.bat            # 环境配置脚本
```

## 快速开始

### 环境要求
- Python 3.10+
- Chrome/Chromium 浏览器

### 安装步骤

1. **克隆仓库**
   ```bash
   git clone https://github.com/Zooo-1/Gemini-Business.git
   cd Gemini-Business
   ```
2. **运行环境配置脚本**
   ```
   双击 一键配置环境.bat
   ```

3. **配置 Clash**
   - 将 `local.yaml.example` 重命名为 `local.yaml`
   - 填入你自己的 Clash 订阅配置（节点信息）

4. **下载 Clash 核心**
   - 下载 [Mihomo (Clash Meta)](https://github.com/MetaCubeX/mihomo/releases) v1.19+ 版本
   - 推荐版本：`mihomo-windows-amd64.exe`
   - 重命名为 `clash.exe` 放入项目根目录

5. **运行程序**
   ```
   双击 Run.bat
   ```

## 工作流程

```
1. 启动 Clash → 寻找可用代理节点
2. 注册临时邮箱 (DuckMail API)
3. 启动浏览器 → 访问 Gemini Business
4. 输入邮箱 → 点击继续
5. 等待验证码邮件
6. 输入验证码 → 提交
7. 保存账号到 result.csv
8. 循环执行
```

## 自动生成的文件

| 文件 | 说明 | 生成时机 |
|------|------|----------|
| `config_runtime.yaml` | Clash 运行时配置 | 程序启动时自动生成 |
| `log.txt` | 运行日志 | 程序运行时自动生成 |
| `result.csv` | 注册成功的账号 | 注册成功时自动生成 |

## 配置说明

### 代理设置

修改 `auto_register_browser.py` 中的代理地址：
```python
PROXY_ADDR = "127.0.0.1:17890"
```
注意如果你的电脑中有使用17890的端口，请自行更改相关配置

### 邮箱 API

如需使用其他临时邮箱服务，修改 `mail_client.py`：
```python
BASE_URL = "https://api.duckmail.sbs"
```

## 输出格式

注册成功的账号保存到 `result.csv`：

| ID | Account | Password | Date |
|----|---------|----------|------|
| 1 | temp_xxx@domain.com | Pwdxxx | 2024-01-10 |

## 依赖项

- DrissionPage >= 4.1.0
- requests >= 2.31.0
- PyYAML >= 6.0

## 待完善功能

| 功能 | 状态 | 说明 |
|------|------|------|
| 纯 API 注册 | ❌ 未实现 | Google 使用 reCAPTCHA Enterprise，纯 API 无法绕过 

## 已知问题

| 问题 | 说明 |
|------|------|
| IP 封锁 | 部分代理节点被 Google 封禁，程序会自动切换节点 |
| 按钮匹配不正确 | 有大概率触发点击验证和重发验证码两个按钮，但是不影响功能 |
| 页面加载慢 | 网络不稳定时页面加载较慢，可能导致超时 |
| 存在僵尸进程clash.exe| 在后台会占用资源，可自己手动进任务管理器结束 |

## 免责声明

**重要提示：请在使用本工具前仔细阅读以下声明**

1. **学习研究用途**：本项目仅供学习、研究和技术交流使用，旨在探索浏览器自动化技术。

2. **使用者责任**：使用本工具所产生的一切后果由使用者自行承担，包括但不限于账号封禁、法律责任等。

3. **合规使用**：使用者应遵守所在国家/地区的法律法规，以及 Google 服务条款。作者不对任何违规使用行为负责。

4. **无担保声明**：本项目按"现状"提供，不提供任何明示或暗示的担保，包括但不限于适销性、特定用途适用性的担保。

5. **禁止商业用途**：禁止将本工具用于商业目的或大规模滥用。

6. **第三方服务**：本项目依赖第三方服务（DuckMail API、Clash 等），其可用性和稳定性不在作者控制范围内。

7. **随时停止维护**：作者保留随时停止维护本项目的权利，恕不另行通知。

**继续使用本工具即表示您已阅读、理解并同意以上所有条款。**

## 许可证

MIT




