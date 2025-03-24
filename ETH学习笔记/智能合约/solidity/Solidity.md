
# Solidity 笔记

## 视频资源
- [32小时最全课程：区块链，智能合约 & 全栈 Web3 开发](https://www.bilibili.com/video/BV1Ca411n7ta?spm_id_from=333.788.videopod.episodes&vd_source=9e7f96609fdf67741d9bbf68913badca&p=14)

---

## Remix
- [Remix IDE](https://remix.ethereum.org/)

### 视频资源
- [10分钟学会使用Remix创建、编译、部署、调试智能合约](https://www.bilibili.com/video/BV1WT411a7N7/?spm_id_from=333.337.search-card.all.click&vd_source=9e7f96609fdf67741d9bbf68913badca)

### **Solidity智能合约学习笔记**

---

### **文件类型**
- `.ts` - TypeScript（前端或工具代码）
- `.sol` - Solidity（智能合约代码）

---

### **快捷键**
- `Cmd + S`（Mac） / `Ctrl + S`（Windows） - 编译 Solidity 代码（依赖编译器或工具，如 Remix IDE 或 Hardhat）。

---

## **Solidity 编写标准**

### **1. 定义许可证声明和版权**
许可证声明（`SPDX License Identifier`）用于声明代码的开源协议。  
每个合约文件的开头需要明确指定许可证类型，方便合规和复用。

```solidity
// SPDX-License-Identifier: GPL-3.0
```

#### 常见许可证：
- `MIT`：宽松的开源协议，允许重复使用和修改。
- `GPL-3.0`：约束力更强的开源协议，要求衍生项目同样保持开源。
- `UNLICENSED`：不对外开放的私有项目。

---

### **2. 声明 Solidity 编译器版本**

Solidity 合约部分需要声明编译器的版本号范围，以确保合约在指定的版本中正常工作。

#### **指定范围版本号**
- 表示允许的编译器版本范围。  
```solidity
pragma solidity >=0.4.22 <0.9.0;
```

#### **固定版本号**
- 限制合约只能使用某个特定版本编译。
```solidity
pragma solidity 0.8.7;
```

#### **软版本号范围**
- 使用 `^` 符号，表示向上兼容，例如：
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7; // 允许使用任何 >=0.8.7 且 <0.9.0 的版本
```

---

## **合约基本结构**

每个 Solidity 文件都可以包含多个合约。合约可以理解为类似“类”的定义，包含变量、函数和事件。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7; // 声明版本号

contract MyContract {
    // 合约内容（如状态变量、函数、事件等）
}
```

---

## **Solidity 数据类型**

Solidity 是强类型语言，支持多种基本和复杂数据类型。以下是常见的基础数据类型：

### **1. 布尔类型 (`bool`)**
- 用于表示 `true` 或 `false` 的条件值。

```solidity
bool public myBool = true; // 默认值为 false

function toggle() public {
    myBool = !myBool; // 取反运算
}
```

---

### **2. 整数类型**
#### **2.1 无符号整数（`uint`）**
- `uint`：无符号整数类型，不能是负数。  
- 可以指定宽度（如 `uint8`、`uint256`）。
- 默认为 `uint256`。

```solidity
uint8 public smallNumber = 255; // 最大值是 255
uint public normalNumber = 1000; // 默认是 uint256
```

#### **2.2 有符号整数（`int`）**
- `int`：有符号整数类型（可为正或负）。
- 同样可以指定宽度（如 `int8`、`int256`）。

```solidity
int public signedNumber = -10; // 默认是 int256
```

---

### **3. 地址类型（`address`）**
- 表示以太坊账户或智能合约的地址，长度固定为 20 字节。
- 通常用于跟踪账户、合约地址或管理权限。

```solidity
address public owner;

constructor() {
    owner = msg.sender; // msg.sender 是调用者的地址
}

function updateAddress(address _newOwner) public {
    owner = _newOwner;
}
```

---

### **4. 定长二进制数组（`bytes`/`bytes32`）**
- `bytes` 表示动态字节序列，主要用于存储原始数据。
- `bytes32` 是固定长度的字节数组，常用于哈希值或加密数据。

```solidity
bytes32 public hashValue;

function setHash(bytes32 _hash) public {
    hashValue = _hash;
}
```

---

## **复杂数据结构**

Solidity 除了基础类型，还支持一些复杂的数据类型，如 `mapping`、`array`、`struct`。

---

### **1. 映射类型（`mapping`）**
`mapping` 是 Solidity 中的核心数据结构，类似于键值对字典。

#### **用法**
```solidity
mapping(address => uint) public balances;

function setBalance(address _addr, uint _value) public {
    balances[_addr] = _value;
}

function getBalance(address _addr) public view returns (uint) {
    return balances[_addr];
}
```

---

### **2. 数组类型（`array`）**
#### **动态数组**
动态数组可以根据需要改变大小。

```solidity
uint[] public numbers;

function addNumber(uint _num) public {
    numbers.push(_num); // 动态添加
}

function getNumbers() public view returns (uint[] memory) {
    return numbers;
}
```

#### **固定大小数组**
固定大小数组有指定的长度，不能动态扩展。

```solidity
uint[5] public fixedArray = [1, 2, 3, 4, 5];
```

---

### **3. 结构体类型（`struct`）**
- `struct` 是自定义的复杂数据类型。

```solidity
struct Person {
    string name;
    uint age;
}

Person[] public people;

function addPerson(string memory _name, uint _age) public {
    people.push(Person(_name, _age));
}
```

---

## **函数详解**

### **1. 函数修饰符**

函数可以有以下修饰符：
- **`public`**: 公开函数，任何人都能调用。
- **`private`**: 私有函数，仅限合约内部使用。
- **`internal`**: 合约内部和继承合约中使用。
- **`external`**: 仅外部账户或合约调用，合约内部调用无效。

```solidity
contract FunctionExample {
    uint private counter;

    function increment() public {
        counter += 1;
    }

    function getCounter() public view returns (uint) {
        return counter; // 只读函数
    }

    function resetCounter() private {
        counter = 0;
    }
}
```

---

### **2. Payable 函数**
- 用于接收以太币的函数需带有 `payable` 关键字。

```solidity
contract PayableExample {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    // 接收以太币
    function deposit() public payable {}

    // 提取合约余额
    function withdraw(uint _amount) public {
        require(msg.sender == owner, "Not the owner");
        payable(owner).transfer(_amount);
    }

    // 查询余额
    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```

---

## **事件机制**
- `event` 是 Solidity 中用来记录区块链事件的功能，便于外部 DApp 追踪日志。

```solidity
event Transfer(address indexed from, address indexed to, uint value);

function transfer(address _to, uint _amount) public {
    emit Transfer(msg.sender, _to, _amount); // 记录事件
}
```

---

## **继承与权限控制**

### **1. 合约继承**
- Solidity 支持单继承和多继承。

```solidity
contract Parent {
    string public parentData = "Parent Contract";
}

contract Child is Parent {
    function getData() public view returns (string memory) {
        return parentData; // 继承父合约属性
    }
}
```

### **2. 权限控制 with `modifier`**
- 自定义修饰符 `modifier` 用于函数权限及逻辑控制。

```solidity
contract Owned {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner");
        _;
    }

    function changeOwner(address _newOwner) public onlyOwner {
        owner = _newOwner;
    }
}
```

--- 

以上内容涵盖了 Solidity 的基础语法和特性，配合实际智能合约需求（如代币、投票、拍卖等场景）可以快速掌握开发技巧。