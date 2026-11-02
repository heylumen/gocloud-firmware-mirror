# 高恪固件镜像（GOCLOUD）

> 高恪（GOCLOUD）**路由器、无线 AP、x86 软路由**的固件归档镜像。
>
> **归档源**：**54 个型号 / 1,545 个固件 + 132 个清单/文档 = 1,677 文件 / 21.22 GB**（统计日期 2026-11-02）。
> **发布副本**：单文件 **19.78 GB**；旧整包 zip **21.20 GB**；两者并存，合计约 **40.99 GB**。
>
> **固件版权归高恪（GOCLOUD）及各自权利人所有**；最新版本请以厂商官方为准。
> 官网：<http://www.gocloud.cn/>

## 一、快速开始

1. **确认型号**：在 [MODEL_INDEX.md](MODEL_INDEX.md) 按型号查「最新版本 / 全部版本」，或看机身标签。
   - K2P → `S3A`；K2 → `S1A_8M`；贴牌型号见 `MODEL_INDEX` 的“找不到型号？”。
2. **选择下载方式**：
   - **单文件**：在 [SINGLE_FILE_INDEX.md](SINGLE_FILE_INDEX.md) 找到型号，进入对应的 `single-<型号>` Release，直接下载单个固件；
   - **整包**：到 Releases 的 `stable` / `beta` / `base` / `ap` / `wifi-ap` 分类下载 zip。
3. **校验文件**：用 [MODEL_INDEX.csv](MODEL_INDEX.csv) 的 `md5` / `sha256` 比对（见 §五）。
4. **刷机**：确认硬件版本、备份后，按 §四选择底包/升级包或 ISO/IMG。

### 示例：S3A（K2P）5.2.2.22550

| 目标 | 入口 | 文件 |
|---|---|---|
| 单文件 | `single-s3a` Release | `S3A__5.2.2.22550__stable__GOCLOUD-S3A-5.2.2.22550.bin.web` |
| 整包 | `stable` Release | `stable__5.2.2__5.2.2.22550.zip` |

> 单文件 asset 名是 ASCII；Release 的 `label` 保留中文原路径。
> 单文件 Release：<https://github.com/heylumen/gocloud-firmware-mirror/releases/tag/single-s3a>

## 二、单文件 vs 整包

| 场景 | 推荐 | 原因 |
|---|---|---|
| 只下一个固件 | **单文件** | 不用下整包、不用解压；手机/弱网更省流量 |
| 分享某个具体固件 | **单文件** | 可直接分享 asset 直链 |
| 一次收齐某型号/某版本 | **整包 zip** | 一次点击，少请求 |
| 历史版本收藏 | **整包 zip** | 旧链接稳定，文件完整 |
| 首次访问、不知道选哪个 | **先看索引** | `MODEL_INDEX` 查版本，`SINGLE_FILE_INDEX` 查单文件入口 |

单文件与旧 zip **并存**；旧 zip 链接不变。

## 三、支持型号

> 归档中**实际有文件的 54 个型号**；完整列表与版本见 [MODEL_INDEX.md](MODEL_INDEX.md)。

- **RN1200（MTK）**：`S1A` / `S1A_8M` / `S1B` / `S2A` / `S2A_WL` / `S3A`
- **RN8000 / x86**：`SX1000` / `SX1100` / `SX1200` / `SX2000`；`RN8000` / `RN9800T`
- **RE / RH / NX / R**：`RE50G` / `RE80G` / `RE100G` / `RE150G` / `RE300G` / `RE304G` / `RE306G` / `RE307G` / `RE500G` / `RE1000G` / `RE8500`；`RH30GP` / `RH80GP`；`NX300` / `NX300T`；`R10` ~ `R40`
- **无线 AP**：`AH-C1` / `AH-C2` / `AH-C3` / `AH-W1` / `AH-W2` / `AH-W3` / `AH-W3V2`；`GC-AK` 全系；`GC-AX1800CG` / `GC-AX1800MG`
- **AP 板卡**：`S1A_AP` / `S3A_AP`

> 部分文件带 `TG-NET-` / `UTT-` / `TE-NET-` / `WWWS-` / `GC-` 等贴牌前缀，属于同一固件的不同品牌分发。
> 厂商还有其他型号，但**本镜像未收录**；不要按厂商产品线推断这里一定有文件，以 `MODEL_INDEX` 为准。

## 四、文件格式与刷机

| 后缀 | 用途 |
|---|---|
| `.bin.web` | MTK 机型升级包（网页后台上传） |
| `.bin.online` | 部分 RE 机型升级包 |
| `.iso` / `.img` / `.GHO` | x86 机型安装镜像 / 写盘镜像 |
| `.rar` / `.zip` | 底包、二合一安装包等 |
| `.ini` | 厂商发布清单 |

刷机顺序：

1. **确认型号与硬件版本**（A1/A2、8M/128M 等），先备份 ART/factory 或原厂配置；
2. **MTK 机型**（S1A / S2A / S3A 等）用 `.bin.web` 网页升级；跨大版本或从第三方固件切换时，先刷 `base` 底包，再刷目标版本；
3. **Breed 刷机**需要裸镜像，不能直接拿网页升级包 `.bin.web` 混用；
4. **x86 机型**（SX 系列）用 `.iso` / `.img` 装机；
5. 刷完核对版本与校验值，确认回退路径。

> 刷机有风险，可能变砖、失去保修；请自行确认设备型号与固件匹配。

## 五、校验与完整性

- [MODEL_INDEX.csv](MODEL_INDEX.csv)：每个固件一行，含 `size` / `md5` / `sha256`；
- 下载后请核对 `sha256` 或 `md5`；不一致不要刷。

Windows 校验示例：

```powershell
Get-FileHash .\GOCLOUD-S3A-5.2.2.22550.bin.web -Algorithm SHA256
# 或
certutil -hashfile GOCLOUD-S3A-5.2.2.22550.bin.web SHA256
```

把输出与 `MODEL_INDEX.csv` 的 `sha256` 比对；不一致不要刷。

## 六、仓库结构

```text
README.md                 本文件
MODEL_INDEX.md / .csv     54 型号 / 1,545 固件索引（含 MD5/SHA256）
SINGLE_FILE_INDEX.md      54 个 single-<型号> Release 入口
```

## 七、Release 与 tag

| tag | 内容 |
|---|---|
| `stable` | 稳定版整包 zip |
| `beta` | 公测版整包 zip |
| `base` | 底包 / 安装镜像 |
| `ap` | AP 板卡整包 |
| `wifi-ap` | 无线 AP 整包 |
| `single-<型号>` | 该型号全部固件的单文件（54 个） |

当前共 **61 个 Release**（7 个整包/清单 + 54 个单文件）；普通用户只需看固件整包与单文件。单文件入口见 [SINGLE_FILE_INDEX.md](SINGLE_FILE_INDEX.md)。

## 八、更新说明

- 固件来源：高恪官方发布渠道；本镜像仅做归档，最新版本以厂商官方为准。
- 版本与文件清单见 [MODEL_INDEX.md](MODEL_INDEX.md)；镜像不保证与官方实时同步。

## 九、常见问题

**Q1：单文件和 zip 选哪个？**  
只下一个/手机弱网选单文件；一次收齐/历史收藏选 zip。两者内容一致。

**Q2：K2P 底包和升级包怎么区分？**  
`base` Release 是底包/安装镜像；`stable`/`beta` 是升级包。跨大版本或从第三方固件切换先刷底包。

**Q3：`.bin.web` 能直接给 Breed 用吗？**  
不能。`.bin.web` 是网页后台升级包；Breed 需要裸镜像，两者不要混用。

**Q4：找不到型号/版本？**  
先在 [MODEL_INDEX.md](MODEL_INDEX.md) 查；贴牌型号按 `TG-NET-RE8500 → RE8500`、`WWWS-SX2000 → SX2000` 归一；仍找不到请提 Issue。

**Q5：校验失败怎么办？**  
重新下载；仍不一致不要刷，附上型号、版本、`sha256` 提 Issue。

**Q6：为什么有 61 个 Release？**  
7 个是整包/清单，54 个是每型号一个 `single-<型号>`；普通下载按索引进入即可。

## 十、官方链接

| 渠道 | 地址 |
|---|---|
| 官网 | <http://www.gocloud.cn/> |
| 讨论区 | <http://www.gocloud.cn/bbs/> |
| 云端 | <http://agent.gocloud.cn/> |
| 帮助文档 | <http://docs.gocloud.cn/> |

## 十一、免责声明与使用条款

- 本项目**仅作个人备份与学习研究**之用；固件与文档版权归高恪及各自权利人所有。
- 只收录厂商公开固件与文档，**不含授权文件、收费固件、修改版固件**。
- 不提供任何形式的担保，不对因使用本镜像造成的后果负责；刷机前请备份并确认回退路径。
- 如权利人认为不妥，请联系删除；转载/商用请先获得权利人授权。

## 十二、反馈

- 问题/缺版本：<https://github.com/heylumen/gocloud-firmware-mirror/issues>
- 请附：型号、硬件版本、目标版本、文件名、`sha256`（如有）、截图/报错。
- 不提供收费代刷/破解；只讨论官方原版固件与归档问题。

*最新版本与文件清单以 [MODEL_INDEX.md](MODEL_INDEX.md) 为准；统计日期 2026-11-02。*
