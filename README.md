# CrossMux PaperDIY 工作分支

本仓库承接 PaperDIY 固件的持续构建与移植工作。

- 当前分支：`crossmux-paperdiy-20261019`。
- [本分支构建和下载产物](https://github.com/blacktea1891/crosspoint-reader/actions/runs/39205119411)。
- [固定的真实固件源码](https://github.com/0x1abin/crossmux/tree/a78a39ed04d6755c6885d57521704d2f96f8b955)。
- [CrossPoint 分支](https://github.com/blacktea1891/crosspoint-reader/tree/paperdiy-bringup-20261019)。
- [CrossMux 分支](https://github.com/blacktea1891/crosspoint-reader/tree/crossmux-paperdiy-20261019)。

这是独立的构建工作分支：工作流显式拉取对应固件源码及 SDK，并在 Linux 构建；
根目录其余继承文件不是该项目的已整合源码。工作流见 `.github/workflows/build-sticky.yml`。
更新并推送此分支会触发后续构建。默认 `develop` 保持不变。

本分支根目录的 `firmware.patch`、`sdk.patch`、`provenance.json` 和 `SHA256SUMS` 保存完整移植补丁与版本记录。

复现：递归克隆固定 CrossMux 版本，先对根仓库应用 `firmware.patch`，再在 `freeink-sdk` 应用 `sdk.patch`；安装 `pioarduino==6.2.0`，运行 `python scripts/patch_pioarduino_cache.py --prepare-platform`，最后 `pio run -e paperdiy`。

完整验证记录：10 个固件目标编译通过；1060/1060 主机测试、格式、默认目标 cppcheck 和显示事务测试通过。新仓库重验 PaperDIY 编译及全部主机测试。CrossMux 尚待实机验收。

Actions 产物保留 30 天，请下载留存。`firmware.factory.bin` 是合并安装镜像，
`firmware.bin` 是应用镜像，不能混用偏移。SHA256SUMS 随固件提供。
本工作流没有刷机步骤；任何新候选都应先核验芯片、机型、分区和哈希，
保留已验证的原机完整 Flash 备份，再经明确批准后刷机。

工作流只依赖本仓库与指定的开发者上游，不依赖旧 CJK 仓库。
