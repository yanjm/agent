# agent(网关）
[![Build Status](https://travis-ci.org/gonet2/agent.svg?branch=master)](https://travis-ci.org/gonet2/agent)

## 设计理念
设备只连接到网关，网关无状态，长连接。        

## agent功用           
1. 数据包加解密(DH+RC4)         
2. 透传原始数据到后端(bidirectional stream)
3. 对协议(API)做测量，可视化(metrics visualization)
4. 不断开tcp连接选服(game在线切换)
5. 统一的连接入口(方便DNS round robin)
6. 处理接入的各种协议，TCP/UDP

## 协议号划分
数据包会根据协议编号（0-65535) **透传** 到对应的服务， 例如(示范）:      

      1-1000: 登陆相关协议，网关协同auth服务处理。
      1001-10000: 游戏逻辑段
      
具体的划分根据业务需求进行。

## 封包
 
        +----------------------------------------------------------------+     
        | SIZE(2) | TIMESTAMP(4) | PROTO(2) | PAYLOAD(SIZE-6)            |     
        +----------------------------------------------------------------+     
        
> SIZE: 后续数据包总长度         
> TIMESTAMP: 数据包序号           
> PROTO: 协议号           
> PAYLOAD: 负载           
