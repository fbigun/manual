# mKCP Transport

[![English][1]][2] [![Chinese][3]][4] [![German][5]][6] [![Russian][7]][8]

[1]: ../../resources/english.svg
[2]: https://www.v2ray.com/en/configuration/transport/mkcp.html
[3]: ../../resources/chinese.svg
[4]: https://www.v2ray.com/chapter_02/transport/mkcp.html
[5]: ../../resources/german.svg
[6]: https://www.v2ray.com/de/configuration/transport/mkcp.html
[7]: ../../resources/russian.svg
[8]: https://www.v2ray.com/ru/configuration/transport/mkcp.html

mKCP is a reliable stream transport. It is an UDP based protocol.

Configuration:

```javascript
{
  "mtu": 1350,
  "tti": 20,
  "uplinkCapacity": 5,
  "downlinkCapacity": 20,
  "congestion": false,
  "readBufferSize": 1,
  "writeBufferSize": 1,
  "header": {
    "type": "none"
  }
}
```

Where:

* `mtu`: Maximum transmission unit. It indicates the maxium number bytes that an UDP packet can carry. Recommended value is between `576` and `1460`. Default value `1350`.
* `tti`: Transmission time interval, in milli-second. mKCP sends data in this interval. Recommended value is between `10` and `100`. Default value `50`.
* `uplinkCapacity`: Uplink bandwidth, in MB/s. The maximum bandwidth for the V2Ray instance to upload data to a remote one. Default value is `5`.
  * Please note it is byte (in MB/s), not bit.
  * One may use value `0` for a small bandwidth.
* `downlinkCapacity`: Downlink bandwidth, in MB/s. The maximum bandwidth for the V2Ray instance to download data. Default value is `20`.
  * Please note it is byte (in MB/s), not bit.
  * One may use value `0` for a small bandwidth.
* `congestion`: Whether or not to enable congestion control. Default value is `false`.
  * When congestion control is enabled, V2Ray will detect network quality. It will send less packets when packet loss is severe, or more data when network is not fully filled.
* `readBufferSize`: Read buffer size for a single connection, in MB. Default value is `2`.
* `writeBufferSize`: Write buffer size for a single connection, in MB. Default value is `2`.
* `header`: Packet header for obfuscation.
  * `type`: Type of obfuscation. Choices are:
    * `"none"`: Default value. No obfuscation is added.
    * `"srtp"`: Obfuscated as SRTP traffic. It may be recognized as video calls such as Facetime.
    * `"utp"`: Obfuscated as uTP traffic. It may be recognized as Bittorrent traffic.
    * `"wechat-video"`: Obfuscated to WeChat traffic.
    * `"dtls"` (V2Ray 3.24+): Obfuscated as DTLS 1.2 packets.

## Tips {#tips}

* `uplinkCapacity` and `downlinkCapacity` determine the speed of mKCP. On client side, `uplinkCapacity` specifies the speed for client sending data to server. On sever side, `downlinkCapacity` specifies the speed of server receiving data. The minimum of this pair is effective in an actual connection.
