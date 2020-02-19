<h1 align="center">如何加入比特币跨链生态：商户篇</h1>
<h4 align="center">Version 1.0 </h4>

[English]() | [中文](./README_CN.md)

## 引言

通过联盟链提供的基础设施，可以实现比特币到其他链的转移，下面会以比特币与以太坊为例子，介绍如何开展自己的比特币跨链业务。

Alice、Bob和Carl是合作伙伴，他们热爱比特币与去中心化技术，希望在比特币上开展更加复杂的业务，但是碍于比特币链的诸多不便，难以实现。于是他们决定利用联盟链的跨链生态，将比特币转移到以太坊上，然后通过以太坊的合约开发自己的业务。

## 跨链的准备工作

1. Alice、Bob和Carl分别准备了自己的**比特币私钥**，并用这些私钥构成了一个P2WSH或者P2SH形式的2/3**多签地址**，多签的作用主要是锁住比特币。

2. 然后，他们需要按照模板开发一个特殊的ERC20代币**合约**（以下称为EBTC），部署在以太坊上，用来接收跨链的比特币。每个人都是用自己的私钥对合约和Redeem脚本进行签名，然后向中继链进行注册，这可以使用[工具](https://github.com/ontio/cross-chain/blob/master/btc/cross-chain_transaction_construction_tool_user_manual.md)实现。

3. 接下来，下载多签的[**签名工具**](https://github.com/ontio/cross-chain/blob/master/btc/redeem_tool_guide.md)，它可以监听联盟链，当有比特币从以太坊合约返回的时候，各自使用自己的私钥对解锁交易签名，这样比特币就回到了客户自己的手里。

4. 最后，每人都创建一个联盟链跨链生态的**钱包**，用来向联盟链提交自己的签名。

## 开启跨链业务

### 第一步，部署以太坊合约

​	将准备好的EBTC合约部署到以太坊上，准备接收比特币。当然也可以使用其他链的合约，比如本体等。

### 第二步，启动签名工具

​	按照[说明](https://github.com/zouxyan/cross-chain/blob/master/btc/redeem_tool_guide.md)，把自己的私钥加密后导入工具，启动工具监听联盟链并提交自己的签名。

### 第三步，发送跨链交易

​	按照特定的格式[构造交易](https://github.com/ontio/cross-chain/blob/master/btc/cross-chain_transaction_construction_tool_user_manual.md)，发送比特币到多签地址，活跃在跨链生态中的Relayer就会把这些跨链交易转发到联盟链，最终比特币会准确地发送到EBTC指定的账户中了。

​	Alice在交易中写入了EBTC合约的地址、自己以太坊的地址和以太坊的chain id，并发送了1BTC到多签地址，在这笔交易拥有6个确认之后，Alice发现自己多了1个EBTC，而发送到多签地址的1BTC则被锁住。

​	Alice想把自己的1EBTC转回比特币链，于是直接调用EBTC合约的接口，填入要转回的金额、比特币地址、比特币chain id等信息，一段时间后，发现签名工具对一笔交易进行了签名，这笔交易就是多签用来释放Alice比特币的，同时另外两人的签名工具也会签名，最终这笔交易会被Relayer成功广播到比特币网络中，这时候Alice会看到这笔交易，但是她发现转回来的比特币不足1BTC，因为这笔多签交易的手续费需要Alice支付，这是跨链生态所要求的，不过手续费并不多，Alice表示完全能接受。

​	经过测试，三人开始基于EBTC开发自己的比特币业务合约，他们终于能在以太坊智能合约上实现自己天马行空的想法了，这多亏了跨链生态！