# Betting dapp

A simple decentralized application in which the user can bet an amount of ether of choice on numbers 1-10.

Remix + Web3 + Vue.js创建的一个简单Dapp：
玩家可以在输入框中下注，然后在1-10之间选择一个数字，如果选中，则以一定比率获得奖励。
其组件基本可划分为：
- 需要知道合约的所有者并拥有访问权限（为简单起见，我们将不再修改所有者）
- 合约的所有者可以销毁合约并提取余额
- 玩家用户可以在 1 - 10 之间下注
- 在合约创建时，所有者能够设置最低下注金额和庄家上风（为简单起见，创建后不可更改）
    - 如果庄家上风为 0，我们的乘数是 10；如果庄家上风是 10%，则乘数是 9。奖励金额为乘数×下注金额。

## 界面上：
- 显示测试网络
- 显示测试账号及余额
- 输入框供玩家用户输入自己的赌资
- 1-10 十个数供用户选择，选对获得奖励，并输出结果。
    - 选中输出Congragulations, you have won + 计算得到的奖励金额
    - 选错输出Sorry you lost, please try again

智能合约存放于contract文件夹下。

## 合约讲解：
- 创建合约 Ownable，构造函数 Ownable（）将在创建时被调用，并将状态变量 'owner' 设置为创建者的地址。
- 将此功能传递到 Mortal 合约中（Mortal 继承自 Ownabe ）。 它有一个函数，允许合约所有者（访问控制）销毁合约并将剩余资金发回给他。
- 创建 Casino 合约，minBet 和 houseEdge分别为合约创建时设置的最小赌资和庄家上分。通过将参数传递给构造函数 Casino() 实现。
- bet（）函数用于下注一个数字。此函数将生成一个1-10的随机数（取当前区块编号%10+1），然后计算并发送赢得的奖励。
- checkContractBalance()函数检查合约的余额。

