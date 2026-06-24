# LAN-Proxy-Disabler
Suitable for situations where you need to quickly turn off a proxy and go back to a direct network connection, like when leftover proxy settings remain after quitting a VPN tool or switching company networks.
# 局域网代理禁用工具

一键禁用 Windows 系统全局 LAN 代理设置的批处理脚本。  
适用于快速关闭代理、恢复直连网络，例如 VPN/代理工具退出后遗留配置，或切换网络环境时使用。

---

### 功能

- ✅ 显示当前运行脚本的用户账户
- ✅ 查询当前代理启用状态（`ProxyEnable` 注册表值）
- ✅ **一键禁用** 当前用户的 LAN 代理（将 `ProxyEnable` 设为 `0`）
- ✅ 刷新 DNS 缓存，避免域名解析残留
- ✅ 弹出成功提示对话框（优先 PowerShell，回退 VBScript）
- ✅ 执行完毕后暂停窗口，方便查看结果

---

### 使用方法

1. 下载 `lan-proxy-simple.bat` 文件。
2. **右键** 单击文件，选择 **“以管理员身份运行”**（推荐，确保 DNS 刷新成功）。
   - 若不使用管理员权限，DNS 刷新步骤可能失败，但不影响代理禁用功能。
3. 脚本会依次执行各步骤，最后弹出提示框告知操作完成。
4. 按任意键关闭命令行窗口。

---

### 原理说明

脚本修改以下注册表项：
- 将 `ProxyEnable` 的 `REG_DWORD` 值由 `1`（启用）改为 `0`（禁用）。
- **注意**：仅修改当前用户（HKCU）配置，不影响其他用户或系统级（HKLM）设置。
- 脚本**不会**删除或修改代理服务器地址（`ProxyServer`），只关闭启用开关。

`ipconfig /flushdns` 用于清除本地 DNS 缓存，确保后续域名解析不再使用旧的代理配置。

---

### 注意事项

- **权限要求**：修改 HKCU 不需要管理员权限，但刷新 DNS 需要。如无管理员权限，`ipconfig /flushdns` 会静默失败（错误被重定向），不影响代理禁用功能。
- **弹窗安全警告**：弹窗通过 PowerShell 或 VBScript 实现，某些安全软件可能会拦截或提示，属于正常行为。
- **适用范围**：仅影响遵循系统代理设置的应用程序（如 Internet Explorer、Edge、Chrome 等）。部分软件（如 Firefox）使用独立代理配置，不受此脚本影响。
- **恢复代理**：如需重新启用代理，可手动将 `ProxyEnable` 设为 `1`，或重新运行代理工具。

---

### 故障排除

| 问题 | 可能原因 | 解决方法 |
|------|----------|----------|
| 弹窗未出现 | PowerShell/VBScript 被禁用或被安全软件拦截 | 检查弹窗是否被阻止，或手动查看注册表确认 `ProxyEnable` 已变为 `0` |
| DNS 刷新失败 | 未以管理员身份运行 | 以管理员身份重新运行脚本 |
| 代理仍然生效 | 应用程序缓存了旧代理设置 | 重启浏览器或应用程序；或检查是否使用了独立代理配置（如 Firefox） |
| 脚本一闪而过 | 未使用 `pause` 或文件损坏 | 确保脚本末尾有 `pause` 命令，或手动在命令行中执行查看输出 |

---

### 许可证

本脚本为Vibe Coding的结果，可随意使用、修改和分发。
作者不对使用此脚本造成的任何系统问题负责，请自行评估风险。

---
### 特别声明

本Readme由AI读取脚本内容后一键生成，若有错误，欢迎指出

---
### 关注我的X账户

https://x.com/intent/follow?screen_name=xiaoyi_0324
