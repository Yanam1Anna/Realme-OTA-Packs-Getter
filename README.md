# 真我(Realme)系列手机 全量包 下载器 
![License](https://img.shields.io/github/license/R0rt1z2/realme-ota)
![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/R0rt1z2/realme-ota?include_prereleases)
![GitHub Issues](https://img.shields.io/github/issues-raw/R0rt1z2/realme-ota?color=red)

---

## 配置要求
* Python 3.9 (或更高).

---

## 安装
### Windows
需要 [Windows Terminal](https://github.com/microsoft/terminal) 或 [PowerShell](https://github.com/PowerShell/PowerShell).
```powershell
# (需要以管理员身份运行)
Invoke-WebRequest https://raw.githubusercontent.com/R0rt1z2/realme-ota/master/Install.ps1 | Invoke-Expression
```

### Linux
```bash
sudo apt install python3-pip
pip3 install --upgrade git+https://github.com/R0rt1z2/realme-ota
```

---

## 使用方法
```bash
usage: realme-ota [-h] [-v {0,1,2,3,4,5} | -s] [-r {0,1,2,3}] [-g GUID]
               [-i IMEI [IMEI ...]] [-b] [--old-method] [-d DUMP] [-o ONLY]
               product_model ota_version {1,2,3,4} [nv_identifier]

positional arguments:
  product_model         Product Model (ro.product.name).
  ota_version           OTA Version (ro.build.version.ota).
  {1,2,3,4}             RealmeUI Version (ro.build.version.realmeui).
  nv_identifier         NV (carrier) identifier (ro.build.oplus_nv_id) (if
                        none, provide 0 or omit).

options:
  -h, --help            show this help message and exit
  -v {0,1,2,3,4,5}, --verbosity {0,1,2,3,4,5}
                        Set the verbosity level. Range: 0 (no logging) to 5
                        (debug). Default: 4 (info).
  -s, --silent          Enable silent output (purge logging). Shortcut for
                        '-v0'.

request options:
  -r {0,1,2,3}, --region {0,1,2,3}
                        Use custom region for the request (GL = 0, CN = 1, IN
                        = 2, EU = 3).
  -g GUID, --guid GUID  The guid of the third line in the file
                        /data/system/openid_config.xml (only required to
                        extract 'CBT' in China).
  -i IMEI [IMEI ...], --imei IMEI [IMEI ...]
                        Specify one or two IMEIs for the request.
  -b, --beta            Try to get a test version (IMEI probably required).
  --old-method          Use old method for the request (only applies if
                        rui_version >= 2).

output options:
  -d DUMP, --dump DUMP  Save request response into a file.
  -o ONLY, --only ONLY  Only show the desired value from the response.
```

---

## 使用示例
```python
realme-ota -r 1 RMX3300 RMX3300_11.F.00_0000_000000000000 5 10010111
```



| 代码                   | 含义                                                         |
| ---------------------- | ------------------------------------------------------------ |
| realme-ota             | 调用ROM包链接提取脚本                                        |
| -r 数字                | -r：区域；数字：（国际版 = 0, 中国 = 1, 印度 = 2, 欧洲 = 3） |
| RMX3300                | 设备型号（在“关于本机”-“版本信息”中，“版本号”前面的字符串，不包含下划线及其后方内容） |
| RMX3300_11.            | 硬件版本号（设备型号_11）                                        |
| F.00_0000_000000000000 | 字母表示版本类型，类型有以下几种：<br>A=出厂版本   C=跨代版本   F=末代更新版本<br>后方数字为ROM的版本号（后方数字全为0即为获取最新，其他请自行测试） |
| 5                      | realme ui的版本                                              |
| 10010111               | 区域的NV_ID（BIN），详情参与下方NV_ID表格，具体情况请自行测试 |

---

### NV_ID表:（引用源：[[Global/EU] Collection of firmware files for Realme GT2 Pro](https://xdaforums.com/t/global-eu-collection-of-firmware-files.4478153/)）

|              国家/地区               |     区域缩写     | NV_ID (HEX) | NV_ID (BIN) | ROM 类型 | 注释  |
| :----------------------------------: | :--------------: | :---------: | :---------: | :------: | :---: |
|               中国台湾               |        TW        |     1A      |  00011010   |  export  |       |
|                 印度                 |        IN        |     1B      |  00011011   |  export  |       |
|              印度尼西亚              |        ID        |     33      |  00110011   |  export  |       |
|                俄罗斯                |        RU        |     37      |  00110111   |  export  |       |
|               马来西亚               |        MY        |     38      |  00111000   |  export  |       |
|                 泰国                 |        TH        |     39      |  00111001   |  export  |       |
|                菲律宾                |        PH        |     3E      |  00111110   |  export  |       |
|              沙特阿拉伯              |        SA        |     83      |  10000011   |  export  |       |
|               拉丁美洲               |      LATAM       |     9A      |  10011010   |  export  |       |
|                 巴西                 |        BR        |     9E      |  10011110   |  export  |       |
|              中东和非洲              |       MEA        |     A6      |  10100110   |  export  |       |
| 欧洲（欧盟，欧洲经济区，英国和瑞士） |       EUEX       |     44      |  01000100   |   GDPR   |       |
|                 英国                 |        GB        |     8A      |  10001010   |   GDPR   |   1   |
|                土耳其                |        TR        |     51      |  01010001   |   GDPR   |       |
|                 西欧                 | EU-NONEEA-Double |     8D      |  10001101   |   GDPR   |       |
|                 中国                 |      ALLNET      |     97      |  10010111   | domestic |       |

#### 注释:

1. 仅在版本 C.08 到 C.16 中（含）中找到；与 EUEX 相同，但有可能区分某些分区。

---

## 其他说明
* 如果您的请求返回`flow limit`或状态代码`500`，请尝试等待几分钟然后再次请求。
* 您可以使用`ALL_PROXY`环境变量通过代理发送请求（如果在您所在的国家/地区找不到更新，则很有用）。在 Windows 上，您可以运行`set ALL_PROXY=ADDRESS:PORT`，而在 Linux 和 MacOS 上，您可以执行`export ALL_PROXY=ADDRESS:PORT`。
* 自 Android 11 (Realme UI2) 以来，Realme 开始使用组件，这意味着您将无法获得完整的 OTA 链接。
* 该`--beta`选项可能无法正常工作，尚未经过全面测试！

## 协议
* 此工具根据 GNU (v3) 通用公共许可证授权。 请参阅 `LICENSE` 了解更多信息。
