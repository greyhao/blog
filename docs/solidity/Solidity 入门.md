## Solidity 入门



### 工具

编写、编译、部署使用浏览器 [IDE](http://remix.ethereum.org/)，适合新手，在浏览器中快速部署测试智能合约。



### 第一个程序

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;
contract HelloWeb3 {
    string public _string = "hello web3!";
}
```

文件结构

* 第一行是注释，表明代码所用的软件许可，不写协议的情况下进行编译虽然程序可以运行但是会有警告
* 第二行是声明使用的 solidity 版本，此处意思是源文件将不允许低于 0.8.4 版本的编译器编译
* 第三、四行是合约部分
  * 第三行：创建名字为 HelloWeb3 的合约
  * 第四行：声明了一个 string 变量 _string，并赋值 “hello web3!”



### 编译

在编辑页面使用 command + s 快捷键或者在编译页面进行编译

### 部署

打开部署页面，直接点击 Deploy 按钮进行部署。

部署成功可以在底部看到名为 HelloWeb3 的合约，及定义的 _string，点击可以看到输出。

![image-20220719183930263](https://tva1.sinaimg.cn/large/e6c9d24ely1h4cf85fu5ej20ja0yoac0.jpg)



### 语法

#### 变量类型

* 数值类型（Value Type），这类变量赋值时直接传递数值

  * 布尔类型

    * 取值：true、false
    * 可以进行逻辑运算

  * 整型

    * int、uint、uint256 等
    * 可以进行比较运算和算数运算

  * 地址类型（address）

    * 存储一个 20 字节的值（以太坊地址的大小）
    * 有成员变量
    * 普通地址
    * 可以进行转账 ETH 的地址：payable(address)
      * 拥有 balance 属性 和 transfer() 方法，可以查询余额及转账

  * 定长字节数组（bytes）

    * byte、bytes8、bytes32 
    * 定长 bytes 可以存数据，消耗 gas 比较少

  * 枚举（enum）

    * 用户定义的数据类型，从 uint 0 开始表示
    * 主要用于为 uint 分配名称，提供程序易读性和维护

  * 函数类型（Function Type）

    说法格式：

    ```solidity
    function funName(<parameter types>) {internal|external|public|private} [pure|view|payable] [returns (<return typs>)] {
    	// function body
    }
    ```

    * `function` 声明函数的关键字
    * `(<parameter types>)`  函数的参数
    * `{internal|external|public|private}` 函数的可见性说明符 
      * public 内部外部均可见，并且自动给 stoage 变量生成 getter 函数
      * private 只能从合约内部访问，继承的合约也不能用
      * external 只能从合约外部访问（但是可以通过 this.f() 来调用）
      * internal  默认值，只能从合约外部访问，继承的合约可以用
    * `[pure|view|payable] ` 决定函数权限/功能的关键字 -- **合约的状态变量存储在链上**
      * payable  出现该关键字时，可以给合约转入 ETH，**通过在合约的构建方法添加 payable，实现部署合约时往合约转账**
      * pure 不能读取也不能写入存储在链上的状态变量 -- **不消耗 gas**
      * view 能读取但是不能写入状态变量 -- **不消耗 gas**
      * 无 pure 并且无 view时，函数既可以读取也可以写入状态变量
    * `[returns <return typs>]` 函数返回的变量类型和名称
      * returns 加在函数名后面，用于声明返回的变量类型及变量名
      * retur 用于函数主体中，返回指定的变量

    

* 引用类型（Reference Type），占空间大，赋值传递的是地址，**使用时声明存储位置**

  * 数组（array）

    * 固定长度数组  声明时指定数组的长度格式：T[k] k 为长度， `uint[8] array1; // 长度为 8`

    * 可变长度数组  声明时不指定长度，格式：T[] ，`uint[] array2;`

    * 数组属性

      * length：内存数组的长度在创建后是固定的
      * push()：可变长度数组和 bytes 可用，在数组最后添加一个 0 元素
      * push(x)：可变长数组和 bytes 可用，在数组最后添加一个 x 元素
      * pop：可变长度数组和 bytes 可用，移除最后一个元素

    * 创建规则：

      * memory 可变长数组，可以用 new 来创建，但是必须声明长度，并且长度不可变 

      ```solidity
      // memory 可变长度 Array
      uint[] memory array3 = new uint[](5);
      bytes memory array4 = new bytes(9);
      ```

      	* 数组字面常数是写作表达式形式的数组，不会立即赋值 `[uint(1), 2, 3] // 声明第一个元素的类型 `
      	* dynamic arrya 需要一个一个元素的赋值

      ```solidity
      uint[] momory x = new uint[](3);
      x[0] = 1;
      x[1] = 2;
      x[2] = 3;
      ```

      

  * 结构体（struct）

    * 通过结构体定义新类型

    ```solidity
    // 结构体
    struct Student {
    	uint256 id;
    	uint256 score;
    }
    
    // 初始化结构体
    Student student;
    
    // 给结构体赋值
    // 方法1: 在函数中创建一个 storage 的 struct 引用
    function initStudent1() external {
    	Student storage _student = student;
    	_student.id = 11;
    	_student.score = 100;
    }
    
    // 方法2: 直接饮用状态变量的 struct
    function initStudent2() external {
    	student.id = 1;
    	student.scrore = 80;
    }
    
    
    ```

    

  * 映射类型（mapping），Solidity 的哈希表

    * 语法格式：`mapping(_KeyType => _valueType)` ，声明时会指定 key、value 的类型

    ```solidity
    mapping(uint => address) public idToAddress; // id 映射到地址
    mapping(address => address) public swapPair; // 币对的映射，地址到地址
    ```

    * 映射的规则

      * `_KeyType` 只能选择默认类型，不能用自定义的结构体。`_Value` 可用使用自定义类型
      * 映射的存储位置必须时 storage，因此可以用于合约的状态变量，函数中的 storage 变量，不能用于 public 函数的参数或返回结果中
      * 如果映射声明为 public，那么会自动创建一个 getter 函数，可以通过 Key 来查询对应的 Value
      * 给映射新增的键值对语法为 `_Var[_key] = _Value // _Var 是映射对象`

      ```solidity
      function writeMap(uint _Key, address _Value) public {
      	idToAddress[_Key] = _Value;
      }
      ```



基本数据类型变量的初始值为 false/0，应用数据类型的初始值为成员默认值。

```solidity
类型 	 初始值
bool // false
string // ""
int	// 0
uint // 0
enum // 枚举中的第一个元素
address // 0x0000000000000000000000000000000000000000 (或 address(0))
function internal // internal 的空白方程
function external // external 的空白方程

uint[3] public _staticArray; // [0, 0, 0]
uint[] public _dynamicArray; // []
mapping(uint => address) public _mapping; // 所有元素都为其默认值的mapping
// 所有成员设为其默认值的结构体 0, 0
struct Student{
	uint256 id;
	uint256 score; 
}
Student public student;


// delete
bool public _bool = true;
function d() external {
	delete _bool; // _bool 的值变为默认值 false
}
```

**使用 delete 操作符，将变量设置为默认初始值**





```solidity
// 变量类型示例代码
// ----- 布尔类型 ----- 
bool public _bool = true;


// ----- 整型 ----- 
int public _int = 1; // 整数，包括负数
uint public _unit = 1; // 正整数
uint256 public _unit256 = 202313; // 256 位正整数


// ----- address 类型 ----- 
address public _address = 0x1efB0993128aC88C86E8E90AbA95914037d70b16;
address payable public _address1 = payable(_address);
// 获取余额
uint256 public balance = _address1.balance;


// ----- 定长数组 ----- 
// MiniSolidity 以字节方式存储进变量 _bytes32，十六进制:0x6772657900000000000000000000000000000000000000000000000000000000
bytes32 public _bytes32 = "grey";
// 存储 _bytes32 的第一个字节 值为：0x67
bytes1 public _byte = _bytes32[0];


// ----- 枚举 ----- 
// 将 unit 0、1、2 表示为 Buy、Hold、Sell
enum ActionSet {Buy, Hold, Sell};
// 创建 enum 变量 action
ActionSet action = ActionSet.Buy;
// enum 和 uint 转换
function enumToUint() external view returns(uint) {
	return uint(action);
}


// ----- 函数 ----- 
uint256 public number = 5;


// ----- pure、view ------
// 读取，处理后改变 number 的值
function add() external {
	number = number + 1;
}

// 只能传入一个参数(number)处理后返回新的参数
function addPure(uint256 _number) external pure returns(uint256 new_number) {
	new_number = _number + 1;
}

// 读取 number 的值，处理后返回新的变量
function addView() external view returns(uint256 new_number) {
	new_number = number + 1;
}


// ----- external、internal ------
// 内部方法，合约内访问
function minus() internal {
	number = number + 1;
}

// 合约外访问
function minusCall() external {
	minus();
}


// ----- payable ------
// 给合约里转入 1 个 ETH
// this 当前合约地址
function minusPayable() external payable returns(uint256 balance) {
	minus();
	balance = address(this).balance;
}


// ----- return ------
// 返回多个变量
function returnMultiple() public pure returns(uint256, bool, uint256[3] memory) {
	return(1, true, [uint256(1), 2, 5])
}

// 命名式返回
function returnNamed() public pure returns(uint256 _number, bool _bool, uint256[3] memory _array) {
	_number = 2;
	_bool = false;
	_array = [uint256(3), 2, 1];
}

// 命名式返回，支持 return
function returnNamed2() public pure returns(uint256 _number, bool _bool, uint256[3] memory _array){
	return (1, true, [uint256(1), 2, 5]);
}

// calldata
function fCalldata(uint[] calldata _x) public pure returns(uint[] calldata) {
	// 参数为 calldata 数组，不能被修改
	// _x[0] = 0; // 该语句会报错
	return(_x);
}
```



#### 运算符

#####逻辑运算 

`!、&&、||、==、!=`

**&& 和 || 遵循短路规则，存在 f(x) || g(x) ，若 f(x) 为 true，则 g(x) 不会被计算**



##### 比较运算符

`<=、<、==、!=、>=、 =` 

返回值为布尔值



##### 算数运算符

`+、-、*、/、%、**(幂)`



#### 数据存储位置

solidity 数据存储位置不同需要的 gas 也不同，有以下三类：

* storage：合约里的状态变量的默认存储位置，存储在链上，消耗 gas 多
* memory：函数里的参数和临时变量一般用这个，存储在内存中过，不上链，消耗 gas 少
* calldata：和 memory 类似，存储在内存中不上链。不同点：calldata 变量不能修改，一般用于函数的参数，消耗 gas 少

#####赋值时的规则

* storage （合约的状态变量）赋值给本地 storage 时，会创建引用，改变新变量会影响原变量

  ```solidity
  uint[] x = [1, 2, 3]; // 状态变量：数组 x
  
  function fStorage() public {
  	// 声明一个 storage 变量 xStorage，指向 x，修改 xStorage 会影响 x 的值
  	uint[] storage xStorage = x;
  	xStorage[0] = 100;
  }
  ```

  

* storage 赋值给 memory，会创建独立的复本，修改其中一个不会影响另一个

  ```solidity
  uint[] x = [1, 2, 3];
  
  function fMemory() public view {
  	// 修改 xMemory 不会影响 x
  	uint[] memory xMemory = x;
  	xMemory[0] = 100;
  }
  ```



* memory 赋值给 memory，会创建引用，改变新变量会影响原变量
* 其他情况，变量赋值给 storage，会创建独立的复本，修改其中一个不会影响另一个



#### 变量的作用域

* 状态变量（state variable）

  * 存储在链上，gas 消耗高
  * 合约内函数均可访问
  * 声明在合约内、函数外

  ```solidity
  contract Variables {
  	uint public x = 1;
  	uint public y;
  	string public z;
  	
  	function foo() external {
  		// 可以在函数中更改状态变量的值
  		x = 5;
  		y = 2;
  		z = "0xhh";
  	}
  }
  ```

  

* 局部变量（local variable）

  * 仅在函数执行过程中有效的变量，函数退出后变量无效
  * 存储在内存中，不上链，gas 低
  * 声明在函数内

  ```solidity
  function bar() external pure returns(uint) {
  	uint xx = 1;
  	uint yy = 3;
  	uint zz = xx + yy;
  	return(zz);
  }
  ```

  

* 全局变量（global variable）

  * 为预留关键字
  * 是全局范围工作的变量
  * 在函数内可以不声明直接使用

  ```solidity
  function global() external view returns(address, uint, bytes memory) {
  	address sender = msg.sender;
  	uint blockNum = block.number;
  	bytes memory data = msg.data;
  	return(sender, blockNum, data);
  }
  ```

​	 

####常用全局变量

* block hash(uint blockNumber): (bytes32)  给定区块的哈希值，只适用于 256 最近区块，不包含当前区块
* block.coinbase: (address payable) 当前区块的矿工地址
* block.gaslimit: (uint) 当前区块的 gaslimit
* block.number: (uint) 当前区块的 number
* block.timestamp: (uint) 当前区块的时间戳，为 unix 纪元以来的秒
* gasleft(): (uint) 剩余 gas
* msg.data: (bytes calldata) 完整 call data
* msg.sender: (address payable) 消息发送者（当前 caller）
* msg.sig: (bytes4) calldata 的前四个字节
* msg.value: (uint) 当前交易发送的 wei 值
* now: (uint) 当前块的时间戳

[完整列表](https://learnblockchain.cn/docs/solidity/units-and-global-variables.html])



#### 解构式赋值

Solidity 使用解构式赋值的规则，支持读取函数的全部或部分返回值。

* 读取所有返回值：声明变量，并将要赋值的变量用 `,` 隔开，按顺序排列
* 读取部分返回值：声明要读取的返回值对应的变量，不读取的留空。

```solidity
// ----- 解构式赋值 ------
// 读取所有返回值
uint256 _number;
bool _bool;
uint256[3] memory _array;
(_number, _bool, _array) = returnNamed();

// 读取部分返回值 只读取 _bool 的值
(, _bool _bool2, ) = returnNamed();
```



#### 关键字 constant、immutable

状态变量声明在这两个关键字之后，不能在合约后更改数值；并且可以节省 gas。

**只有数值变量可以声明 constant 和 immutable；string 和 bytes 只能声明为 constant。**

* constant 
  * 必须在声明的时候初始化，之后不能改变，尝试改变会导致编译失败
* immutable
  * 可以在声明时或构造函数中初始化
  * 可以赋值为全局变量
  * 自定义函数给变量赋值

```solidity
// constant
uint256 constant CONSTANT_NUM = 10;

// immutable
uint256 public immutable IMMUTABLE_NUM = 1000;
address public immutable IMMUTABLE_ADDRESS;
uint256 public immutable IMMUTABLE_TEST;

// 使用构造函数初始化 immutable 变量
constructor() {
 	// 赋值为全局变量
	IMMUTABLE_ADDRESS = address(this);
	// 使用 test() 函数赋值
	IMMUTABLE_TEST = test();
}

function test() public pure returns(uint256) {
	uint256 what = 9;
	return(what);
}
```



#### 控制流（语句）

1. if...else

   ```solidity
   function ifElseTest(uint256 _number) public pure returns(bool) {
   	if(_number == 0) {
   		return(true);
   	} else {
   		return(false);
   	}
   }
   ```

   

2. for

   ```solidity
   function forTest() public pure returns(uint256) {
   	uint sum = 0;
   	for(uint i = 0; i < 10; i++) {
   		sum += i;
   	}
   	return(sum);
   }
   ```

   

3. while

   ```solidity
   function whileTest() public pure returns(uint256) {
   	uint sum = 0;
   	uint i = 0;
   	while(i < 10) {
   		sum += i;
   		i++;
   	}
   	return(sum);
   }
   ```

   

4. do-while

   ```solidity
   function doWhiteTest() public pure returns(uint256) {
   	uint sum = 0;
   	uint i = 0;
   	do {
   		sum += i;
   		i++;
   	}while(i < 10);
   	return(sum);
   }
   ```

   

5. 三元运算符

   ```solidity
   function tenaryTest(uint256 x, uint256 y) public pure returns(uint256) {
   	return x >= y ? x : y;
   }
   ```



6. 支持关键字：continue （立即进入下一个循环），break （跳出当前循环）



#### 构造函数、修饰器

构造函数（constructor）是一种特殊的函数

特点：

* 每个合约定义一个

* 部署合约的时候自动运行一次
* 可以用来初始化合约的一些参数，比如初始化合约的 owner 地址

```solidity
address owner;

constructor() public {
	owner = msg.sender; // 部署合约时，将 owner 设置为部署者的地址
}
```



修饰器（modifier）是 solidity 特有的语法

使用场景：运行函数前的检查，例如地址，变量，余额等；可以用来控制智能合约权限

```solidity
// 定义一个叫做 onlyOwner 的 modifier
modifier onlyOwner {
	require(msg.sender == owner); // 检查调用者是否为 owner 地址
	_; // 如果是的话，继续运行函数主体；否则报错并 revert 交易
}

// 带有 onlyOwner 修饰符的函数只能被 owner 地址调用
function changeOwner(address _newOwner) external onlyOwner {
	owner = _newOwner;
}
```



#### 事件

Solidity 中的事件（event）是 EVM 上日志的抽象

特点：

* 响应： 应用程序可以通过 RPC 接口订阅和监听这些事件，并在前端做响应
* 经济：事件是 EVM 上比较经济的存储数据的方式，消耗 gas 相对较少，存储新的变量会比较费 gas



事件声明格式：event 事件名(变量类型 变量名)

```solidity
// ERC20 代币合约中的 Transfer 事件
// 记录 from、to、value 三个变量；indexed 表示重要，可以进行筛选，每个事件最多 3 个带 indexed 的变量
event Transfer(address indexed from, address indexed to, uint256 value);
```



在函数中释放事件

```solidity
// _transfer 函数，执行转账逻辑
function _transfer(address from, address to, uint256 amount) external {
	_balance[from] = 1000000; // 给转账地址一些初始代币
	
	_balance[from] -= amount; // from 地址减去转账数量
	_balance[to] += amount; // to 地址加上转账数量
	
	// 释放事件
	emit Transfer(from, to, amount);
}
```



#### 继承

solidity 中的继承（inheritance），包括单继承、多重继承以及修饰器和构造函数的继承。

规则

* virtual：父合约中的函数，如果希望子合约重写，需要加上 virtual 关键字

* override：子合约重写了父合约的函数，需要加上 override 关键字

* 可以多继承
* 继承关键字： is



##### 合约、函数继承

```solidity
// 合约 A
constract A {
	evet Log(string msg);
	
	function hip() public virtual {
		emit Log("A");
	}
	
	function a() public virtual {
		emit Log("A");
	}
}

// 合约 B
constract B is A {
	// 重写父合约的方法
	function hip() public virtual override {
		emit Log("B");
	}
}

// 合约 C
// 多继承
constract CC is A, B {
	// 重写父合约的方法
	function hip() public virtual override(A, B) {
		emit Log("CC");
	}
}
```



#####修饰器的继承

使用同函数类似



##### 构造函数的继承

子合约需要提供基类构造函数所需的所有参数，有以下两种实现方式：

```solidity
// 基类 A
contract A {
	uint public a;
	
	constructor(uint _a) {
		a = _a;
	}
}

// 方式 1 继承时声明基类构造函数的参数
contract B is A(1) {

}

// 方式 2 在子合约的构造函数中声明构造函数的参数
contract C is A {
	constructor(uint _c) A(_c * _c) {
	
	}
}

```



#### 调用基类合约的函数

子合约有两种方式调用基类合约的函数

* 直接调用，格式：基类合约.函数名()
* 使用 super 关键字，访问最近的基类合约，继承关系按声明从左到右排序，左边为最近

```solidity
// 以下例子以合约 CC 为背景

// 直接调用
function callBase() public {
	B.hip();
}

// 使用 super 关键字
function callBaseSuper() public {
	// 调用的是 A.hip() 方法 
	super.hip();
}

```



#### 抽象合约（abstract）



#### 接口（interface）





第 14 讲

[本笔记教程 Git 地址](https://github.com/AmazingAng/WTFSolidity)

[教程官网](https://wtf.academy/docs/intro)

[Solidity 官方文档](https://solidity-cn.readthedocs.io/zh/develop/introduction-to-smart-contracts.html)

