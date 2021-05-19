#Websocket 行情推送
本篇所列出的所有wss接口的baseurl为: wss://wss:ws.bitrue.com/kline-api/ws

###数据压缩
客户端发送消息订阅websocket不需要压缩。
客户端接收到的websocket消息是经过gzip 压缩的，客户端需要进行解压。

###心跳
每3分钟，服务端会发送ping帧，客户端应当在10分钟内回复pong帧，
否则服务端会主动断开链接。允许客户端发送不成对的pong帧(即客户端可以以高于10分钟每次的频率发送pong帧保持链接)。

###更新频率
更新速度都是实时更新

###心跳消息
服务端发送给客户端的心跳
``` json
{
  "ping":1621418174969
}
```
客户端发送给服务端的心跳
``` json
{
  "pong":1621418174969
}
```

###请求数据
请求数据的event 为req 。成功请求到数据后会收到数据结构集
例如请求交易对adausdt的成交信息

``` json
{"event":"req","params":{"cb_id":"adausdt","channel":"market_adausdt_trade_ticker","top":20}}
```
收到的响应数据为
``` json
{"event_rep":"rep","cb_id":"adausdt","status":"ok","top":20,"ds":"2021-05-19 17:53:00","ts":1621417980160,"channel":"market_adausdt_trade_ticker","data":[{"id":28187162,"price":1.743900,"amount":472.07373000000000000000000000000000,"side":"BUY","vol":270.70,"ts":1621412844000,"ds":"2021-05-19 16:27:24"},{"id":28187161,"price":1.742800,"amount":4.93212400000000000000000000000000,"side":"SELL","vol":2.83,"ts":1621412843000,"ds":"2021-05-19 16:27:23"},{"id":28187160,"price":1.742600,"amount":18.55869000000000000000000000000000,"side":"BUY","vol":10.65,"ts":1621412843000,"ds":"2021-05-19 16:27:23"},{"id":28187159,"price":1.743200,"amount":28.71050400000000000000000000000000,"side":"BUY","vol":16.47,"ts":1621412842000,"ds":"2021-05-19 16:27:22"},{"id":28187158,"price":1.744500,"amount":28.01667000000000000000000000000000,"side":"SELL","vol":16.06,"ts":1621412842000,"ds":"2021-05-19 16:27:22"},{"id":28187157,"price":1.744200,"amount":57.48883200000000000000000000000000,"side":"SELL","vol":32.96,"ts":1621412841000,"ds":"2021-05-19 16:27:21"},{"id":28187156,"price":1.742900,"amount":1.67318400000000000000000000000000,"side":"BUY","vol":0.96,"ts":1621412841000,"ds":"2021-05-19 16:27:21"},{"id":28187155,"price":1.743000,"amount":186.18726000000000000000000000000000,"side":"SELL","vol":106.82,"ts":1621412840000,"ds":"2021-05-19 16:27:20"},{"id":28187154,"price":1.743200,"amount":120.61200800000000000000000000000000,"side":"BUY","vol":69.19,"ts":1621412840000,"ds":"2021-05-19 16:27:20"},{"id":28187153,"price":1.743900,"amount":0.45341400000000000000000000000000,"side":"SELL","vol":0.26,"ts":1621412839000,"ds":"2021-05-19 16:27:19"},{"id":28187152,"price":1.743400,"amount":16.87611200000000000000000000000000,"side":"SELL","vol":9.68,"ts":1621412839000,"ds":"2021-05-19 16:27:19"},{"id":28187151,"price":1.743300,"amount":1.48180500000000000000000000000000,"side":"SELL","vol":0.85,"ts":1621412839000,"ds":"2021-05-19 16:27:19"},{"id":28187150,"price":1.743000,"amount":903.65835000000000000000000000000000,"side":"BUY","vol":518.45,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187149,"price":1.743600,"amount":15.81445200000000000000000000000000,"side":"BUY","vol":9.07,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187148,"price":1.743600,"amount":76.63122000000000000000000000000000,"side":"BUY","vol":43.95,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187147,"price":1.743600,"amount":58.98598800000000000000000000000000,"side":"BUY","vol":33.83,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187146,"price":1.743700,"amount":21.81368700000000000000000000000000,"side":"BUY","vol":12.51,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187145,"price":1.743600,"amount":524.94565200000000000000000000000000,"side":"BUY","vol":301.07,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187144,"price":1.743700,"amount":6.08551300000000000000000000000000,"side":"BUY","vol":3.49,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187143,"price":1.743700,"amount":9.31135800000000000000000000000000,"side":"BUY","vol":5.34,"ts":1621412838000,"ds":"2021-05-19 16:27:18"}]}

```
###订阅数据
订阅数据的event 为sub 。 成功订阅后
例如订阅adausdt 币对的成交信息

``` json
{"event":"sub","params":{"cb_id":"adausdt","channel":"market_adausdt_trade_ticker","top":20}}
```
订阅成功后会收到订阅成功的响应信息

``` json
{
  "channel":"market_adausdt_trade_ticker",
  "cb_id":"adausdt",
  "event_rep":"subed",
  "status":"ok",
  "ts":1621418172662
}
```
之后会收到用户具体的订阅的响应数据

``` json
{
  "channel":"market_adausdt_trade_ticker",
  "cb_id":"adausdt",
  "event_rep":"subed",
  "status":"ok",
  "ts":1621418172662
}
```


###取消订阅数据
 取消订阅数据的event 为unsub 。例子：
 取消成交信息的订阅
 

#K线

k线的channel 格式为：market_%s_kline_%S
其中占位符 %s 是币对名称，例如 adausdt ，%S 是k线支持的精度例如 1min。
目前支持的币对可以通过接口 https://www.bitrue.com/kline-api/coin/symbolForShow 获取。
目前支持的精度如下：
1min
5min
15min
30min
1h
2h
4h
6h
8h
12h
1d
1w


举例：adausdt 的1min 精度的k线的channel 就是 market_adausdt_kline_1min。

### 请求历史k线
历史k线默认返回的是1440根k线的信息，更早的历史k线目前不支持查询。

``` json
{"event":"req","params":{"channel":"market_adausdt_kline_1min","cb_id":"adausdt"}}

```
响应数据
示例响应数据中省略了部分数据
``` json
{
  "data":[
    {
      "close":2.0968, #收盘价
      "amount":28899.212766, #成交金额
      "high":2.0996, #最高价
      "id":1621326480, k线的时间 秒
      "low":2.096, # 最低价
      "open":2.0989, #开始的价格
      "vol":13775.04 #成交数量
    },
    {
      "close":2.0991,
      "amount":15431.118281,
      "high":2.1006,
      "id":1621326540,
      "low":2.0957,
      "open":2.0967,
      "vol":7358.66
    }
 ],
  "ts":1621418992094,
  "event_rep":"rep",
  "cb_id":"adausdt",
  "status":"ok",
  "channel":"market_adausdt_kline_1min"
}
```

### 订阅k线

``` json
{"event":"sub","params":{"channel":"market_adausdt_kline_1min","cb_id":"adausdt"}}

```
 响应数据
 订阅成功
 ``` json
{
  "channel":"market_adausdt_kline_1min",
  "cb_id":"adausdt",
  "event_rep":"subed",
  "status":"ok",
  "ts":1621419881168
}
 
 ```
 k线数据消息
  ``` json
{
  "channel":"market_adausdt_kline_1min",
  "ts":1621413503504,
  "tick":{
    "amount":49855.950209,
    "close":1.7439,
    "vol":28616.74,
    "high":1.7445,
    "low":1.7406,
    "open":1.7423,
    "id":1621412820
  }
}

  ```

### 取消订阅k线

  ``` json
{
  "event":"unsub",
  "params":{
    "channel":"market_adausdt_kline_1min",
    "cb_id":"adausdt"
  }
}
```
  
#成交
###请求成交信息

``` json
{"event":"req","params":{"cb_id":"adausdt","channel":"market_adausdt_trade_ticker","top":20}}
```
收到的响应数据为
``` json
{"event_rep":"rep","cb_id":"adausdt","status":"ok","top":20,"ds":"2021-05-19 17:53:00","ts":1621417980160,"channel":"market_adausdt_trade_ticker","data":[{"id":28187162,"price":1.743900,"amount":472.07373000000000000000000000000000,"side":"BUY","vol":270.70,"ts":1621412844000,"ds":"2021-05-19 16:27:24"},{"id":28187161,"price":1.742800,"amount":4.93212400000000000000000000000000,"side":"SELL","vol":2.83,"ts":1621412843000,"ds":"2021-05-19 16:27:23"},{"id":28187160,"price":1.742600,"amount":18.55869000000000000000000000000000,"side":"BUY","vol":10.65,"ts":1621412843000,"ds":"2021-05-19 16:27:23"},{"id":28187159,"price":1.743200,"amount":28.71050400000000000000000000000000,"side":"BUY","vol":16.47,"ts":1621412842000,"ds":"2021-05-19 16:27:22"},{"id":28187158,"price":1.744500,"amount":28.01667000000000000000000000000000,"side":"SELL","vol":16.06,"ts":1621412842000,"ds":"2021-05-19 16:27:22"},{"id":28187157,"price":1.744200,"amount":57.48883200000000000000000000000000,"side":"SELL","vol":32.96,"ts":1621412841000,"ds":"2021-05-19 16:27:21"},{"id":28187156,"price":1.742900,"amount":1.67318400000000000000000000000000,"side":"BUY","vol":0.96,"ts":1621412841000,"ds":"2021-05-19 16:27:21"},{"id":28187155,"price":1.743000,"amount":186.18726000000000000000000000000000,"side":"SELL","vol":106.82,"ts":1621412840000,"ds":"2021-05-19 16:27:20"},{"id":28187154,"price":1.743200,"amount":120.61200800000000000000000000000000,"side":"BUY","vol":69.19,"ts":1621412840000,"ds":"2021-05-19 16:27:20"},{"id":28187153,"price":1.743900,"amount":0.45341400000000000000000000000000,"side":"SELL","vol":0.26,"ts":1621412839000,"ds":"2021-05-19 16:27:19"},{"id":28187152,"price":1.743400,"amount":16.87611200000000000000000000000000,"side":"SELL","vol":9.68,"ts":1621412839000,"ds":"2021-05-19 16:27:19"},{"id":28187151,"price":1.743300,"amount":1.48180500000000000000000000000000,"side":"SELL","vol":0.85,"ts":1621412839000,"ds":"2021-05-19 16:27:19"},{"id":28187150,"price":1.743000,"amount":903.65835000000000000000000000000000,"side":"BUY","vol":518.45,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187149,"price":1.743600,"amount":15.81445200000000000000000000000000,"side":"BUY","vol":9.07,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187148,"price":1.743600,"amount":76.63122000000000000000000000000000,"side":"BUY","vol":43.95,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187147,"price":1.743600,"amount":58.98598800000000000000000000000000,"side":"BUY","vol":33.83,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187146,"price":1.743700,"amount":21.81368700000000000000000000000000,"side":"BUY","vol":12.51,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187145,"price":1.743600,"amount":524.94565200000000000000000000000000,"side":"BUY","vol":301.07,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187144,"price":1.743700,"amount":6.08551300000000000000000000000000,"side":"BUY","vol":3.49,"ts":1621412838000,"ds":"2021-05-19 16:27:18"},{"id":28187143,"price":1.743700,"amount":9.31135800000000000000000000000000,"side":"BUY","vol":5.34,"ts":1621412838000,"ds":"2021-05-19 16:27:18"}]}

```
收到的数据消息
``` json
{
  "event_rep":"rep",
  "cb_id":"adausdt",
  "status":"ok",
  "top":20,
  "ds":"2021-05-19 19:32:23",
  "ts":1621423943916,
  "channel":"market_adausdt_trade_ticker", 
  "data":[
    {
      "id":28187162,  #成交id 
      "price":1.7439, #价格
      "amount":472.07373, #成交金额
      "side":"BUY",  #方向
      "vol":270.7, #数量
      "ts":1621412844000, #成交的时间戳
      "ds":"2021-05-19 16:27:24" #成交的utc+8时间
    },
    {
      "id":28187161,
      "price":1.7428,
      "amount":4.932124,
      "side":"SELL",
      "vol":2.83,
      "ts":1621412843000,
      "ds":"2021-05-19 16:27:23"
    }
  ]
}
```

###订阅成交信息
``` json
{
  "event":"sub",
  "params":{
    "cb_id":"adabtc",
    "channel":"market_adabtc_trade_ticker"
  }
}
```

订阅成功后会收到订阅成功的响应信息

``` json
{
  "channel":"market_adausdt_trade_ticker",
  "cb_id":"adausdt",
  "event_rep":"subed",
  "status":"ok",
  "ts":1621418172662
}
```
之后会收到用户具体的订阅的响应数据

``` json
{
  "channel":"market_ltcbtc_trade_ticker",
  "tick":{
    "data":[
      {
        "id":20482764,
        "price":0.006277,
        "amount":0.00520991,
        "side":"BUY",
        "vol":0.83,
        "ts":1621426164263,
        "ds":"2021-05-19 20:09:24"
      },
      {
        "id":20482763,
        "price":0.006278,
        "amount":0.00018834,
        "side":"SELL",
        "vol":0.03,
        "ts":1621426160884,
        "ds":"2021-05-19 20:09:20"
      }
    ]
  },
  "ts":1621426164471
}
``` 

###取消订阅成交信息
``` json
{"event":"unsub","params":{"cb_id":"adausdt","channel":"market_adausdt_trade_ticker","top":20}}
```


#按Symbol的完整Ticker

###订阅ticker
``` json
{"event":"sub","params":{"channel":"market_xlmeth_ticker","cb_id":"xlmeth"}}

```

订阅成功的响应

``` json
{
  "channel":"market_xlmeth_ticker",
  "cb_id":"xlmeth",
  "event_rep":"subed",
  "status":"ok",
  "ts":1621422413684
}
```
数据响应
``` json
{
  "tick":{
    "amount":0,  #成交金额
    "rose":0,  #24小时的涨跌幅
    "close":0.000309,  #收盘价格
    "vol":0,  #成交量
    "high":0.000309, #最高价
    "low":0.000309, #最低价 
    "open":0.000309 #开盘价
  },
  "channel":"market_xlmeth_ticker", #channelName 
  "ts":1621422413684  #时间戳
}
```


###取消订阅ticker

``` json
{
  "event":"unsub",
  "params":{
    "channel":"market_xlmeth_ticker",
    "cb_id":"xlmeth"
  }
}
```

#有限档深度信息
默认提供的深度信息是40档的深度信息。
深度悉尼下有三个精度。

###订阅深度信息

``` json
{"event":"sub","params":{"cb_id":"adausdt","channel":"market_adausdt_depth_step0"}}

```
首先收到响应

``` json
{
  "channel":"market_adausdt_depth_step0", #订阅的channel
  "cb_id":"adausdt",  #订阅的币对名称
  "event_rep":"subed", #订阅成功
  "status":"ok",  #订阅成功标示
  "ts":1621419669423  #时间戳
}
```

之后收到数据消息
``` json
{
  "channel":"market_adausdt_depth_step0",
  "ts":1621426497365,
  "tick":{
    "buys":[
      [
        "0.15579",
        110
      ],
      [
        "0.12579",
        100
      ],
      [
        "0.05260",
        924402.01
      ]
    ],
    "asks":[
    ]
  }
}
```


###取消订阅深度信息
``` json
{"event":"unsub","params":{"cb_id":"adausdt","channel":"market_adausdt_depth_step0"}}

```

###请求深度信息

``` json
{"event":"req","params":{"cb_id":"adausdt","channel":"market_adausdt_depth_step0"}}

```

响应
``` json
{
  "ts":1621419599417,
  "tick":{
    "buys":[  #买单
    ],
    "asks":[  #卖单
      [
        "40199.75",  #价格
        0.1  #数量
      ]
    ]
  }
}
```

##获取支持的币对信息
**请求URL：**
- `https://www.bitrue.com/kline-api/coin/symbolForShow`

**请求方式：**
- GET

**参数：**
无

**返回示例**

```json
{"btc":[{"name":"BTR/BTC","key":"btrbtc","scale":{"price":9,"volume":1},"depth":[9,8,7]},{"name":"BTR/BTC","key":"btrbtc","scale":{"price":9,"volume":1},"depth":[9,8,7]}],"usdt":[],"xrp":[],"eth":[]}
```


