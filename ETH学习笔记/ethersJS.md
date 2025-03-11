# MetaMask 开发指南

## 获取 API Key
访问 [MetaMask Developer](https://developer.metamask.io/) 获取 API Key。

---

## 获取最新区块号
```javascript
const { ethers } = require("ethers");

// 连接到以太坊主网
const provider = new ethers.JsonRpcProvider("https://mainnet.infura.io/v3/your-infura-api-key");

async function main() {
    const blockNumber = await provider.getBlockNumber();
    console.log(`Latest block number: ${blockNumber}`);
}

main();
```

---

## 获取钱包余额
```javascript
const { ethers } = require("ethers");

const provider = new ethers.JsonRpcProvider("https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID");

async function getWalletBalance(address) {
    const balance = await provider.getBalance(address);
    console.log(`Balance of ${address}: ${ethers.formatEther(balance)} ETH`);
}

const walletAddress = "Your walletAddress"; // 示例地址
getWalletBalance(walletAddress);
```

---

## 使用测试网络发起交易
```javascript
const { ethers } = require("ethers");

// 配置 Infura 的 Sepolia 连接信息
const INFURA_API_KEY = "INFURA_API_KEY"; // 替换为你的 Infura API Key
const provider = new ethers.JsonRpcProvider(`https://sepolia.infura.io/v3/${INFURA_API_KEY}`);

const privateKey = "Your Private Key"; // 替换为你的钱包私钥
const wallet = new ethers.Wallet(privateKey, provider);

const recipient = "Accept Address"; // 替换为目标接收地址
const amountInEth = "0.01"; // 要发送的金额 (Sepolia ETH)

async function sendTransaction() {
    try {
        const tx = await wallet.sendTransaction({
            to: recipient,
            value: ethers.parseEther(amountInEth), // 将 ETH 转换为 Wei
        });

        console.log(`Transaction sent! Hash: ${tx.hash}`);
        const receipt = await tx.wait();
        console.log("Transaction confirmed:", receipt);

    } catch (error) {
        console.error("Error sending transaction:", error);
    }
}

sendTransaction();
```

---

### 结果示例
```
Transaction sent! Hash: xxxxxxxx
Transaction confirmed: TransactionReceipt {...}
```

---

## web3.js vs ethers.js

| 场景                          | web3.js                              | ethers.js                              |
| ----------------------------- | ------------------------------------ | -------------------------------------- |
| **小型轻量的前端 DApp**       | 不推荐，功能臃肿                     | 推荐，体积小，加载速度快               |
| **复杂的后端应用程序**        | 适合，功能全面                      | 推荐，模块化设计，分层解耦容易         |
| **离线钱包或签名功能**        | 支持但不完善                        | 推荐，内置支持离线交易构造与签名       |
| **老项目迭代/维护**           | 适合直接扩展                        | 推荐重写为 ethers.js                  |
| **多链扩展（EVM 兼容链）**    | 支持但繁琐                        | 更推荐，API 结构灵活易扩展             |

---

| 指标               | **web3.js**         | **ethers.js**       |
| ------------------ | ------------------- | ------------------- |
| **体积**          | 较大                 | 较小                 |
| **模块化设计**    | 无                   | 模块化               |
| **API 设计**      | 较老                 | 现代化，设计简洁     |
| **私钥管理**      | 无内置密钥工具      | 提供完整的密钥管理工具 |
| **多链支持**      | 支持但成本高        | 支持灵活的多链环境优化 |
| **适用场景**      | 维护老项目           | 现代 DApp 和复杂系统开发 |

---

### 总体建议
- **web3.js**：适合维护老项目或在熟悉的原有生态上开发。
- **ethers.js**：更推荐用于现代项目，轻量、安全、模块化，开发体验更佳。
