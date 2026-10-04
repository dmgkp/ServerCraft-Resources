# ServerCraft Resources

ServerCraft（我的世界开服工具 · Android）的**外部资源仓库**：存放体积过大、不适合打进 APK 的运行时资源，通过 **Releases** 分发，应用在需要时按需下载。

## 为什么单独建仓库

`debian-rootfs.bin`（Java 版服务器所需的完整 Debian 环境根文件系统）解压后约 **940MB**，压缩后仍有 **313MB**。把它打进 APK 会让安装包体积暴涨、也让每次更新都要重复下载这几百兆。因此：

- APK 里**不再内置**该文件；
- 资源放在本仓库的 **Release** 里；
- 应用在「Java 版」首次进入时，让用户二选一：**从本地导入** 或 **从网络下载**；
- 下载/导入完成后**自动删除**下载的压缩包，避免占用设备空间。

## 资源列表

| 文件 | 说明 | 压缩大小 | 解压后 | SHA-256 |
|---|---|---|---|---|
| `debian-rootfs.bin` | Debian 根文件系统（gzip 压缩的 tar，含 JDK 运行环境） | 327,888,432 B (≈313 MiB) | ≈940 MiB | `417cf7563a9c3de839dc63feacde2e4c3de9e9e4fe2dd5f66ea89718f19dc3db` |

> 文件是 **gzip 压缩的 tar**（`file` 类型：`gzip compressed data`，内层为 `ustar` tar）。解压到应用私有目录后即为完整的 rootfs（含 `/bin -> usr/bin` 等符号链接）。

## 下载方式

优先使用受支持的 **GitHub 加速代理**（国内可直连、更快），代理不可用时回退 GitHub 直连：

```
# 代理示例（应用内默认优先走代理）
https://ghfast.top/https://github.com/dmgkp/ServerCraft-Resources/releases/latest/download/debian-rootfs.bin
https://gh-proxy.com/https://github.com/dmgkp/ServerCraft-Resources/releases/latest/download/debian-rootfs.bin
https://ghproxy.link/https://github.com/dmgkp/ServerCraft-Resources/releases/latest/download/debian-rootfs.bin

# 直连
https://github.com/dmgkp/ServerCraft-Resources/releases/latest/download/debian-rootfs.bin
```

下载后请校验 SHA-256 与上表一致再使用。

## 校验

```bash
sha256sum debian-rootfs.bin
# 期望: 417cf7563a9c3de839dc63feacde2e4c3de9e9e4fe2dd5f66ea89718f19dc3db
```

## 许可

- 本仓库自身内容（文档、脚本、元数据）以 **GNU AGPL-3.0** 授权，全文见 [LICENSE](LICENSE)。
- `debian-rootfs.bin` 内包含 Debian GNU/Linux 系统及大量第三方软件包，其版权与许可归各自权利人所有（多数为 GPL/LGPL/BSD/MIT 等开源许可）。分发与使用请遵守相应许可证条款。
- 本仓库与 Mojang Studios / Microsoft 无任何隶属、赞助或背书关系。
