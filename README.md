# CrossPoint PaperDIY 工作分支

本仓库承接 PaperDIY 固件的持续构建与移植工作。

- 当前分支：`paperdiy-bringup-20261019`。
- [本分支构建和下载产物](https://github.com/blacktea1891/crosspoint-reader/actions/runs/39205119150)。
- [固定的真实固件源码](https://github.com/prateek/crosspoint-reader/tree/268216cdc3f5e7c5a016f476f57fa26d75047ebb)。
- [CrossPoint 分支](https://github.com/blacktea1891/crosspoint-reader/tree/paperdiy-bringup-20261019)。
- [CrossMux 分支](https://github.com/blacktea1891/crosspoint-reader/tree/crossmux-paperdiy-20261019)。

这是独立的构建工作分支：工作流显式拉取对应固件源码及 SDK，并在 Linux 构建；
根目录其余继承文件不是该项目的已整合源码。工作流见 `.github/workflows/build-sticky.yml`。
更新并推送此分支会触发后续构建。默认 `develop` 保持不变。

复现：递归克隆上述固定版本，按工作流安装固定工具链依赖后执行 `pio run -e paperdiy`。匹配 SDK 和模拟器版本均已固定在工作流中。

CrossPoint 已在用户 PaperDIY 完成启动、SD、阅读、按键和菜单实测；休眠电流仍未测量。

Actions 产物保留 30 天，请下载留存。`firmware.factory.bin` 是合并安装镜像，
`firmware.bin` 是应用镜像，不能混用偏移。SHA256SUMS 随固件提供。
本工作流没有刷机步骤；任何新候选都应先核验芯片、机型、分区和哈希，
保留已验证的原机完整 Flash 备份，再经明确批准后刷机。

工作流只依赖本仓库与指定的开发者上游，不依赖旧 CJK 仓库。
