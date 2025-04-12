## RTP时间戳时钟频率详解

- RTP时间戳作用：标记媒体数据的采集时刻，用户接收端同步播放
- 时钟频率定义：每秒的时间戳增量单位数(单位：hz)
- 音频流：通常使用采样率作为时钟频率

## AMR-WB的时钟频率
编码类型	采样率	RTP时钟频率	规范依据

AMR-WB	16,000	16,000	RFC 4867

RFC 4867 关键条款：
    "The RTP timestamp is in units of the sampling frequency, so 16,000 Hz for AMR-WB."

## 时间戳增量计算

场景：发送端每20ms生成一个AMR-WB帧(即50帧/秒)

- 单帧时间戳增量
```
时间戳增量 = 时钟频率 * 时间间隔
          = 16000 HZ * 0.02s
          = 320
```
- RTP包时间戳示例
```
包1： timestamp = 0x12345678 //0ms
包2： timestamp = 0x12345678 + 320 = 0x123457d8 //20ms
包2： timestamp = 0x123457d8 + 320 = 0x12345938 //40ms
```
