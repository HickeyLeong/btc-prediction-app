# 🚀 BTC Price Prediction App

一个基于 Binance BTC 合约价格的猜涨跌 Web 应用，类似 Binance Events。

## ✨ 功能特性

- 💰 初始余额 100 USDT
- 🎯 支持 5/10/30 分钟倒计时
- 📈 最小下单 5 USDT
- 🏆 赢额 80% 收益
- 📊 实时 BTC 价格（来自 Binance 期货 API）
- 📱 响应式设计（Desktop/Mobile）
- 🏅 排行榜系统
- 📝 完整的投注历史记录

## 🛠️ 技术栈

**后端：**
- Node.js + Express
- Axios（调用 Binance API）
- CORS 中间件

**前端：**
- Vue 3（Composition API）
- Vite
- Axios

## 📦 安装与运行

### 1. 克隆仓库
```bash
git clone https://github.com/HickeyLeong/btc-prediction-app.git
cd btc-prediction-app
```

### 2. 安装后端依赖
```bash
npm install
```

### 3. 安装前端依赖
```bash
cd client
npm install
cd ..
```

### 4. 配置环境变量
```bash
cp .env.example .env
```

编辑 `.env` 文件（可选配置 Binance API Key）：
```
PORT=5000
NODE_ENV=development
INITIAL_BALANCE=100
MIN_BET=5
WIN_RATE=0.8
```

### 5. 启动应用

**方式一：同时运行前后端**

终端 1 - 启动后端服务器（端口 5000）：
```bash
npm run dev
```

终端 2 - 启动前端开发服务器（端口 5173）：
```bash
npm run client
```

访问：http://localhost:5173

**方式二：只运行后端（生产构建）**

首先构建前端：
```bash
cd client
npm run build
cd ..
```

然后启动服务器：
```bash
npm start
```

访问：http://localhost:5000

## 📖 使用说明

### 1. 进入应用
- 输入任意用户 ID（如：user123）
- 点击 "Start" 按钮初始化账户

### 2. 下单步骤
- 选择下单金额（5-100 USDT）
- 选择时间期限（5/10/30 分钟）
- 点击 **📈 UP** 或 **📉 DOWN**
- 等待倒计时结束自动结算

### 3. 结算规则
- **赢**：获得 80% 的收益（投注额 + 80% 收益）
- **输**：失去投注额
- 自动结算，无需手动操作

### 4. 查看数据
- **Active Bets**：当前未结算的投注
- **Bet History**：历史投注记录（最近 10 条）
- **Leaderboard**：排行榜前 10 名

## 🔌 API 端点

| 方法 | 端点 | 说明 |
|------|------|------|
| GET | `/api/user/:userId` | 获取用户信息 |
| GET | `/api/price` | 获取当前 BTC 价格 |
| POST | `/api/bet` | 下单投注 |
| GET | `/api/bets/:userId` | 获取用户投注历史 |
| GET | `/api/bet/:betId` | 获取单个投注详情 |
| GET | `/api/leaderboard` | 获取排行榜 |
| GET | `/api/health` | 健康检查 |

## 📊 数据流程

```
用户下单
   ↓
验证 → 扣款 → 创建投注记录
   ↓
等待指定时间
   ↓
获取结算价格 → 比较涨跌
   ↓
结算 → 更新余额 → 记录结果
```

## 🚀 部署指南

### Heroku 部署

1. 创建 Heroku 应用
2. 连接 GitHub 仓库
3. 设置环境变量
4. 点击 Deploy

### Docker 部署

创建 `Dockerfile`：
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 5000

CMD ["npm", "start"]
```

构建并运行：
```bash
docker build -t btc-prediction-app .
docker run -p 5000:5000 btc-prediction-app
```

## 🔒 安全建议

- ⚠️ 生产环境使用数据库（MongoDB/PostgreSQL）而不是内存存储
- ⚠️ 添加用户认证（JWT/OAuth）
- ⚠️ 实现速率限制
- ⚠️ 使用 HTTPS
- ⚠️ 验证所有输入参数
- ⚠️ 添加交易日志审计

## 🐛 常见问题

### Q: 为什么价格没有更新？
A: 检查网络连接，确保能访问 Binance API。价格每 5 秒更新一次。

### Q: 投注后多久结算？
A: 根据您选择的时间期限自动结算（5/10/30 分钟）。

### Q: 如何重置账户？
A: 使用新的用户 ID 即可创建新账户。

### Q: 能否修改收益率？
A: 修改 `.env` 文件中的 `WIN_RATE` 参数（如 0.8 = 80%）。

## 📝 许可证

MIT License

## 👨‍💻 作者

HickeyLeong

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

**免责声明**：本应用仅作学习用途，不构成任何投资建议。使用本应用自担风险。
