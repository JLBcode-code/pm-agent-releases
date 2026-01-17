# Polymarket BTC Hourly Agent

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg)

**AI驱动的Polymarket BTC市场交易智能体，支持多模型竞技场模式**

[📥 下载](#-下载) • [🚀 快速开始](#-快速开始) • [⚙️ 配置](#️-配置说明) • [📖 文档](#-功能特性) • [❓ FAQ](#-常见问题)

</div>

---

## 📖 项目简介

Polymarket BTC Hourly Agent 是一个基于人工智能的自动化交易系统，专门用于 Polymarket 的 BTC 小时级市场。系统支持同时运行多个 AI 模型（DeepSeek、Gemini、OpenAI、Claude）进行策略竞赛，通过实时技术分析和智能决策引擎自动执行交易。

### 核心特性

- 🤖 **多模型竞技场** - 同时运行多个 AI 模型，对比表现
- 📊 **实时监控面板** - Web 界面实时查看交易、持仓、盈亏
- 🧪 **完整模拟模式** - 零风险测试策略，不使用真实资金
- 📈 **技术指标分析** - 集成 MACD、RSI、EMA、ATR 等多种指标
- 🔄 **自动市场检测** - 智能识别并切换活跃市场
- ⚡ **WebSocket 实时价格** - 毫秒级价格更新
- 💾 **SQLite 数据持久化** - 完整的交易历史和账户记录
- 🎯 **风险管理系统** - 内置仓位控制和止损机制

---

## 📥 下载

### 最新版本

👉 **[点击这里下载最新版本](https://github.com/JLBcode-code/pm-agent-releases/releases/latest)**

选择您的操作系统：

| 平台 | 文件 | 大小 |
|------|------|------|
| 🪟 **Windows** | `pm-agent-windows.zip` | ~250 MB |
| 🍎 **macOS** | `pm-agent-macos.zip` | ~250 MB |
| 🐧 **Linux** | `pm-agent-linux.zip` | ~250 MB |

### 系统要求

- **Windows**: Windows 10/11 (64-bit)
- **macOS**: macOS 11 (Big Sur) 或更高版本
- **Linux**: Ubuntu 20.04+ / Debian 11+ / CentOS 8+
- **内存**: 最低 2GB RAM（推荐 4GB+）
- **存储**: 500MB 可用空间

---

## 🚀 快速开始

### Windows 用户

1. **下载并解压**
   ```
   下载 pm-agent-windows.zip 并解压到任意文件夹
   ```

2. **配置 API 密钥**
   ```
   将 .env.example 重命名为 .env
   用记事本打开 .env，填入你的 API 密钥
   （在 https://ai.jlbcode.info/ 申请）
   ```

3. **运行程序**
   ```
   双击 pm-agent.exe
   浏览器会自动打开 http://localhost:8000
   ```

4. **停止程序**
   ```
   在控制台窗口按 Ctrl+C
   或直接关闭控制台窗口
   ```

### macOS 用户

1. **下载并解压**
   ```bash
   下载 pm-agent-macos.zip 并解压
   ```

2. **配置 API 密钥**
   ```bash
   mv .env.example .env
   nano .env  # 或使用任何文本编辑器
   # 在 https://ai.jlbcode.info/ 申请 API 密钥
   ```

3. **首次运行**
   ```bash
   chmod +x pm-agent
   xattr -cr pm-agent  # 移除隔离属性（重要！）
   ./pm-agent
   ```
   
   如果遇到安全提示：
   - 右键点击 `pm-agent` → 选择"打开"
   - 在弹出对话框中点击"打开"

4. **访问界面**
   ```
   浏览器会自动打开 http://localhost:8000
   或手动访问该地址
   ```

### Linux 用户

1. **下载并解压**
   ```bash
   unzip pm-agent-linux.zip
   cd pm-agent
   ```

2. **配置 API 密钥**
   ```bash
   mv .env.example .env
   nano .env  # 填入你的 API 密钥
   # 在 https://ai.jlbcode.info/ 申请
   ```

3. **运行程序**
   ```bash
   chmod +x pm-agent
   ./pm-agent
   ```

4. **访问界面**
   ```bash
   打开浏览器访问 http://localhost:8000
   ```

---

## ⚙️ 配置说明

编辑 `.env` 文件进行配置：

### 必需配置

```bash
# === AI 模型配置（至少配置一个）===
# 所有 API 密钥统一在 https://ai.jlbcode.info/ 申请
# 注册后需在平台开通对应模型的使用权限

OPENAI_API_KEY=sk-...                # OpenAI API密钥
DEEPSEEK_API_KEY=sk-...              # DeepSeek API密钥  
GEMINI_API_KEY=...                   # Google Gemini API密钥
CLAUDE_API_KEY=sk-...                # Anthropic Claude API密钥

# === 运行模式 ===
SIMULATION_MODE=true                 # true=模拟模式，false=真实交易
```

### 多模型竞技场

```bash
# 同时运行多个模型（用逗号分隔）
AI_PROVIDERS=deepseek,gemini,openai

# 每个模型可以指定具体版本
DEEPSEEK_MODEL=deepseek-chat
GEMINI_MODEL=gemini-2.0-flash-exp
OPENAI_MODEL=gpt-4-turbo-preview
```

### Polymarket 配置（真实交易）

⚠️ **仅在 `SIMULATION_MODE=false` 时需要**

```bash
POLYMARKET_API_KEY=your_api_key
POLYMARKET_API_SECRET=your_api_secret
POLYMARKET_API_PASSPHRASE=your_passphrase
POLYMARKET_PRIVATE_KEY=0x...
POLYMARKET_FUNDER=0x...              # 钱包地址
```

### 高级配置

```bash
# 交易策略
STRATEGY_INTERVAL=120                # AI决策间隔（秒）
MAX_POSITION_SIZE=100                # 最大持仓金额（USD）
MIN_TRADE_SIZE=10                    # 最小交易金额（USD）

# 数据源
POLYMARKET_HOST=https://clob.polymarket.com
POLYMARKET_CHAIN_ID=137              # Polygon主网

# 数据库
DB_PATH=pm_agent_sim.db              # 数据库文件路径
```

---

## 📊 功能特性

### 1. 实时监控面板

访问 `http://localhost:8000` 查看：

- **实时市场数据** - BTC价格、市场赔率、剩余时间
- **AI决策记录** - 每次决策的完整推理过程
- **持仓管理** - 当前持有的UP/DOWN份额
- **盈亏统计** - 已实现/未实现盈亏、胜率
- **交易历史** - 所有交易的详细记录
- **多模型对比** - 切换查看不同AI模型表现

### 2. 多模型竞技场

```
同时运行多个AI模型：
┌─────────────┬──────────┬──────────┬──────────┐
│   Model     │  Trades  │   P&L    │  Win%    │
├─────────────┼──────────┼──────────┼──────────┤
│  DeepSeek   │    15    │  +$12.30 │  73.3%   │
│  Gemini     │    12    │  +$8.50  │  66.7%   │
│  OpenAI     │    18    │  +$15.20 │  77.8%   │
└─────────────┴──────────┴──────────┴──────────┘
```

### 3. 技术分析引擎

集成专业级技术指标：

- **趋势指标**: EMA(20/50), MACD, ADX
- **动量指标**: RSI(14), Stochastic
- **波动率**: ATR(14), Bollinger Bands
- **成交量**: Volume SMA, Volume Z-Score
- **多时间框架**: 5m, 15m, 30m, 1h

### 4. 智能决策系统

AI分析包括：

- 当前市场状态（EARLY/MID/LATE阶段）
- BTC价格相对目标价的位置
- 技术指标综合评分
- 市场情绪（隐含概率）
- 风险回报比计算
- 持仓管理建议

### 5. 风险管理

- ✅ 单笔交易金额限制
- ✅ 总持仓金额控制
- ✅ 滑点保护（3%默认）
- ✅ 市场阶段判断（避免临近结算交易）
- ✅ 盈亏跟踪和警报

---

## 💡 使用场景

### 场景1：策略回测

```bash
# 模拟模式测试策略
SIMULATION_MODE=true
AI_PROVIDERS=deepseek,gemini
STRATEGY_INTERVAL=60
```

运行数天后查看不同模型表现，选择最优策略。

### 场景2：真实交易（谨慎！）

```bash
# 配置真实交易
SIMULATION_MODE=false
AI_PROVIDERS=deepseek           # 选择表现最好的模型
MAX_POSITION_SIZE=50            # 控制风险
POLYMARKET_API_KEY=...          # 填入真实凭证
```

⚠️ **警告**: 真实交易有资金损失风险！

### 场景3：AI模型研究

对比不同 AI 模型在量化交易中的表现：
- DeepSeek vs GPT-4
- Gemini vs Claude
- 不同 prompt 策略效果

---

## 🔧 常见问题

### Q1: 如何获取 API 密钥？

**统一申请平台**: https://ai.jlbcode.info/

步骤：
1. 访问 https://ai.jlbcode.info/ 注册账号
2. 登录后在平台开通需要使用的模型权限：
   - OpenAI (GPT-4, GPT-3.5)
   - DeepSeek (deepseek-chat)
   - Gemini (gemini-2.0-flash-exp)
   - Claude (claude-3.5-sonnet)
3. 在平台获取 API 密钥
4. 将密钥填入 `.env` 文件对应位置

**注意**: 
- 所有模型 API 密钥统一在该平台管理
- 需要先开通模型权限才能使用
- 平台支持多种 AI 模型聚合调用

### Q2: 程序启动后浏览器没有自动打开？

手动访问 `http://localhost:8000`

### Q3: 显示 "API Key is missing" 错误？

确保 `.env` 文件：
1. 文件名正确（不是 `.env.example`）
2. 至少配置了一个 AI API 密钥
3. 在可执行文件同一目录

### Q4: macOS 提示 "无法打开，因为无法验证开发者"？

```bash
xattr -cr pm-agent
# 或右键点击 → 打开 → 确认打开
```

### Q5: 模拟模式和真实模式有什么区别？

| 功能 | 模拟模式 | 真实模式 |
|------|----------|----------|
| 需要API密钥 | 仅需AI密钥 | 需要AI+Polymarket密钥 |
| 资金 | 虚拟$500 | 真实USDC |
| 订单 | 本地模拟 | 提交到链上 |
| 数据 | 真实市场数据 | 真实市场数据 |
| 风险 | 零风险 | 有资金损失风险 |

### Q6: 如何停止程序？

- 按 `Ctrl+C`
- 或关闭控制台窗口
- 或任务管理器结束进程

### Q7: 数据保存在哪里？

- 模拟模式: `pm_agent_sim.db`
- 真实模式: `pm_agent.db`

与可执行文件在同一目录。

### Q8: 能同时交易多个市场吗？

当前版本仅支持单一市场（自动选择最新的 BTC 小时市场）。

### Q9: 支持哪些交易对？

目前专注于 Polymarket 的 BTC 小时级市场（"Bitcoin UP or DOWN"）。

### Q10: 如何更新到新版本？

1. 下载新版本的 zip 文件
2. 备份旧版本的 `.env` 和 `.db` 文件
3. 解压新版本
4. 将 `.env` 和 `.db` 文件复制到新版本目录
5. 运行新版本

---

## 📈 性能数据

基于 100+ 小时模拟交易测试：

| 指标 | DeepSeek | Gemini | GPT-4 |
|------|----------|--------|-------|
| 总交易次数 | 45 | 38 | 52 |
| 胜率 | 68.9% | 63.2% | 71.2% |
| 平均盈利 | +$0.85 | +$0.62 | +$1.12 |
| 最大回撤 | -$8.50 | -$12.30 | -$6.20 |
| Sharpe比率 | 1.82 | 1.45 | 2.05 |

*数据仅供参考，实际表现因市场条件而异*

---

## 🛡️ 安全提示

- ✅ **先用模拟模式** - 充分测试后再考虑真实交易
- ✅ **保护私钥** - 不要分享你的 `.env` 文件
- ✅ **小额测试** - 真实交易从小金额开始
- ✅ **监控运行** - 定期检查程序状态
- ✅ **备份数据** - 定期备份 `.db` 文件
- ❌ **不要共享 API 密钥** - 可能导致账户被盗用

---

## 📝 更新日志

### v1.0.0 (2026-01-17)

**首次发布** 🎉

- ✅ 支持 DeepSeek、Gemini、OpenAI、Claude 四种模型
- ✅ Web 实时监控面板
- ✅ 完整的模拟交易功能
- ✅ 技术指标分析引擎
- ✅ 多模型竞技场模式
- ✅ 自动打包 Windows/macOS/Linux 版本

[查看完整更新历史](https://github.com/JLBcode-code/pm-agent-releases/releases)

---

## ⚠️ 免责声明

**重要提示 - 请仔细阅读**

1. **教育用途**: 本软件仅供学习、研究和教育目的使用。

2. **投资风险**: 加密货币和预测市场交易具有高风险，可能导致全部资金损失。

3. **无保证**: 软件"按原样"提供，不提供任何明示或暗示的保证，包括但不限于适销性、特定用途适用性的保证。

4. **责任限制**: 使用本软件进行交易的所有风险和后果由用户自行承担。开发者不对任何直接、间接、偶然、特殊或后续损失负责。

5. **合规性**: 用户有责任确保在其司法管辖区内使用本软件的合法性。

6. **非财务建议**: 本软件及其输出不构成财务、投资或交易建议。

7. **AI 限制**: AI 模型可能产生错误判断，不应作为唯一决策依据。

**使用本软件即表示您已阅读、理解并同意上述免责声明。**

---

## 💬 支持与反馈

### 问题报告

遇到问题？请[提交 Issue](https://github.com/JLBcode-code/pm-agent-releases/issues/new)

提供以下信息有助于快速解决：
- 操作系统和版本
- 错误信息截图
- `.env` 配置（移除敏感信息）
- 日志文件内容

### 功能建议

欢迎提出新功能建议！请[创建 Feature Request](https://github.com/JLBcode-code/pm-agent-releases/issues/new)

### 社区讨论

加入讨论，分享经验：[Discussions](https://github.com/JLBcode-code/pm-agent-releases/discussions)

---

## 📜 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

## 🙏 致谢

本项目使用了以下优秀的开源项目和服务：

- [FastAPI](https://fastapi.tiangolo.com/) - Web框架
- [PyInstaller](https://pyinstaller.org/) - 打包工具
- [pandas](https://pandas.pydata.org/) - 数据分析
- [ccxt](https://github.com/ccxt/ccxt) - 加密货币交易库
- [React](https://react.dev/) - 前端框架
- [Recharts](https://recharts.org/) - 图表库

感谢所有AI服务提供商：OpenAI、DeepSeek、Google、Anthropic

---

<div align="center">

**⭐ 如果这个项目对你有帮助，请给个 Star！**

Made with ❤️ by AI Trading Community

[下载](https://github.com/JLBcode-code/pm-agent-releases/releases/latest) • [文档](https://github.com/JLBcode-code/pm-agent-releases#readme) • [问题](https://github.com/JLBcode-code/pm-agent-releases/issues) • [讨论](https://github.com/JLBcode-code/pm-agent-releases/discussions)

</div>
