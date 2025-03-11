
获取API KEY

https://developer.metamask.io/

#### 获取最新区块号

```js
const { ethers } = require("ethers");

// 连接到以太坊主网
const provider = new ethers.JsonRpcProvider("https://mainnet.infura.io/v3/your-infura-api-key");

async function main() {
    // 获取最新区块号
    const blockNumber = await provider.getBlockNumber();
    console.log(`Latest block number: ${blockNumber}`);
}

main();

```

#### 获取钱包余额

```js
const { ethers } = require("ethers");

// 使用 Infura 的提供器
const provider = new ethers.JsonRpcProvider("https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID");

// 查询钱包余额
async function getWalletBalance(address) {
    const balance = await provider.getBalance(address);
    console.log(`Balance of ${address}: ${ethers.formatEther(balance)} ETH`);
}

const walletAddress = "Your walletAddress"; // 示例地址
getWalletBalance(walletAddress);

```

官方文档
https://docs.metamask.io/services/reference/ethereum/

#### 使用测试网络发起交易

```js
// 导入 ethers.js
const { ethers } = require("ethers");

// 配置 Infura 的 Sepolia 连接信息
const INFURA_API_KEY = "INFURA_API_KEY";  // 替换为你的 Infura API Key
const provider = new ethers.JsonRpcProvider(`https://sepolia.infura.io/v3/${INFURA_API_KEY}`);

// 私钥 (不要在生产环境中暴露真实的私钥!)
const privateKey = "Your Private Key"; // 替换为你的钱包私钥
const wallet = new ethers.Wallet(privateKey, provider); // 使用私钥和提供者连接钱包

// 接收方地址和转账金额
const recipient = "Accept Address"; // 替换为目标接收地址
const amountInEth = "0.01"; // 要发送的金额 (Sepolia ETH)

async function sendTransaction() {
    try {
        // 构造并发送一笔交易
        const tx = await wallet.sendTransaction({
            to: recipient,
            value: ethers.parseEther(amountInEth), // 将 ETH 转换为 Wei
        });

        console.log(`Transaction sent! Hash: ${tx.hash}`);

        // 等待交易确认
        const receipt = await tx.wait();
        console.log("Transaction confirmed:", receipt);

    } catch (error) {
        console.error("Error sending transaction:", error);
    }
}

// 调用函数
sendTransaction();


```

结果返回

```
Transaction sent! Hash: xxxxxxxx
Transaction confirmed: TransactionReceipt {
  provider: JsonRpcProvider {},
  to: 'xxxxx',
  from: 'xxxxxx',
  contractAddress: null,
  hash: 'xxxxxxxx',
  index: 170,
  blockHash: 'xxxxx',
  blockNumber: 7879017,
  logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
  gasUsed: 21000n,
  blobGasUsed: null,
  cumulativeGasUsed: 15194128n,
  gasPrice: 12331105n,
  blobGasPrice: null,
  type: 2,
  status: 1,
  root: undefined
}

```


#### web3.js 和 ethers.js
**`web3.js`** 和 **`ethers.js`** 是与以太坊网络交互的两个常见 JavaScript 库，它们各有优点和适用场景。两者的主要功能类似，但在设计、易用性、模块化、安全性等方面存在一些重要区别。

 **适用场景**

| 场景                          | web3.js                                                                            | ethers.js                                                                          |
| ----------------------------- | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **小型轻量的前端 DApp**       | 不推荐，功能臃肿，体积较大。                                                       | 推荐，体积小（大约 88kB），加载速度快。                                           |
| **复杂的后端应用程序**        | 比较适合，历史悠久，功能全面。（但仍需对接其他模块完成细化工作）                     | 更推荐，模块化设计使得分层解耦较容易，工具链完整且稳定。                           |
| **离线钱包或签名功能**        | 支持较初级的离线签名功能，但不够完善。                                              | 推荐，内置支持离线交易构造、签名，还有更强的密钥管理工具和硬件钱包集成支持。       |
| **老项目迭代/维护**           | 如果早期项目基于 web3.js 开发，直接扩展可以降低学习成本。                          | 如果重写或升级为目标，可选择更轻量的 ethers.js，与现代开发理念更贴合。             |
| **多链扩展（EVM 兼容链）**    | 支持但集成起来较繁琐。                                                             | 更推荐，对多链支持较好，API 结构更加灵活易扩展。                                   |

---


| 指标               | **web3.js**                                | **ethers.js**                              |
| ------------------ | ------------------------------------------ | ------------------------------------------ |
| **体积**          | 较大                                      | 较小                                      |
| **模块化设计**    | 无模块化，代码臃肿                        | 模块化，按需加载                          |
| **API 设计**      | API 较老，存在兼容性问题                  | 现代化 API，设计简洁易用                   |
| **私钥管理**      | 无内置密钥工具                            | 提供完整的密钥管理工具                     |
| **多链支持**      | 支持多链但有一定开发成本                  | 支持更灵活的多链环境优化                   |
| **适用场景**      | 历史项目或者初级开发                      | 现代 DApp 和复杂系统开发更适合             |

**总体建议：**
- **web3.js**：适合维护老项目，或者在熟悉其原有生态情况下轻松开发。
- **ethers.js**：更推荐用于现代项目，它更轻量、更安全、模块化，且开发体验更好。

