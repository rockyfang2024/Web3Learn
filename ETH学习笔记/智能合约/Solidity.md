
# Solidity 笔记

## 视频资源
- [32小时最全课程：区块链，智能合约 & 全栈 Web3 开发](https://www.bilibili.com/video/BV1Ca411n7ta?spm_id_from=333.788.videopod.episodes&vd_source=9e7f96609fdf67741d9bbf68913badca&p=14)

---

## Remix
- [Remix IDE](https://remix.ethereum.org/)

### 视频资源
- [10分钟学会使用Remix创建、编译、部署、调试智能合约](https://www.bilibili.com/video/BV1WT411a7N7/?spm_id_from=333.337.search-card.all.click&vd_source=9e7f96609fdf67741d9bbf68913badca)

### 文件类型
- `.ts` - TypeScript
- `.sol` - Solidity

### 快捷键
- `cmd + S`  - 编译代码

---

## 定义许可证和分享规则
```solidity
// SPDX-License-Identifier: GPL-3.0
```

## 约定版本号
- 允许版本：大于 `0.4.22` 且小于 `0.9.0`
```solidity
pragma solidity >=0.4.22 <0.9.0;
```
- 固定版本
```solidity
pragma solidity 0.8.7;
```
- 或使用软版本控制
```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.7; // 允许任何比0.8.7更新的版本
```

---

## 定义合约
```solidity
contract MyContract {}
```

---

## 基础数据类型
[官方文档](https://docs.soliditylang.org/en/v0.8.14/types.html)

### 基础数据类型
- `bool`
- `uint`
  - `uint8`  // 8位
  - `uint256` // 256位
- `int`
- `address`
- `bytes`



