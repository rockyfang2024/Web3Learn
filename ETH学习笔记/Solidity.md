## Solidity

视频资源
-[（32 小时最全课程）区块链，智能合约 & 全栈 Web3 开发](https://www.bilibili.com/video/BV1Ca411n7ta?spm_id_from=333.788.videopod.episodes&vd_source=9e7f96609fdf67741d9bbf68913badca&p=14)


##### Remix

[Remix](https://remix.ethereum.org/)

视频资源
- [10分钟学会使用Remix创建、编译、部署、调试智能合约](https://www.bilibili.com/video/BV1WT411a7N7/?spm_id_from=333.337.search-card.all.click&vd_source=9e7f96609fdf67741d9bbf68913badca)

文件类型
- .ts  TypeScript
- .sol Solidity

快捷键
- cmd + S 编译代码
##### 定义license和分享规则

```
// SPDX-License-Identifier: GPL-3.0
```

##### 约定版本号

约定版本号 大于0.4.22且小于0.9.0

```
pragma solidity >=0.4.22 <0.9.0;
```
或者
```
pragma solidity 0.8.7;
```
或者
```
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.7; // 任何比0.8.7更新的版本都可以
```
##### 定义合约

```
contract name {}
```

##### 基础数据类型

[官方文档](https://docs.soliditylang.org/en/v0.8.14/types.html)

基础数据类型
- bool
- uint
    - unit8 // 8个bit
    - unit256 // 256个bit
- int
- address
- bytes


