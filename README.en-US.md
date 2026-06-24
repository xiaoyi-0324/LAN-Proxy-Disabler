# LAN Proxy Disabler

**Choose the version that works for your language:**
- [简体中文](README.md)
- [English](README.en-US.md)

## English Version

A one‑click batch script to **disable the system‑wide LAN proxy** on Windows.  
Ideal for quickly reverting to a direct network connection after VPN/proxy tools exit improperly, or when switching network environments.

---

### Features

- ✅ Shows the current user account running the script
- ✅ Queries the current proxy enable status (`ProxyEnable` registry value)
- ✅ **Disables** the LAN proxy for the current user (sets `ProxyEnable` to `0`)
- ✅ Flushes DNS cache to avoid stale name resolution
- ✅ Displays a success popup dialog (PowerShell first, fallback to VBScript)
- ✅ Pauses at the end so you can review the output

---

### Usage

1. Download `lan-proxy-simple.bat`.
2. **Right‑click** the file and select **“Run as administrator”** (recommended to ensure DNS flush works).
   - If you run without admin rights, the DNS flush step may fail silently, but the proxy disable still works.
3. The script executes each step sequentially and finally shows a popup confirming completion.
4. Press any key to close the command window.

---

### How It Works

The script modifies the following registry key:
- Sets `ProxyEnable` (REG_DWORD) from `1` (enabled) to `0` (disabled).
- **Note**: Only affects the current user (HKCU); does not change other users or system‑wide (HKLM) settings.
- The proxy server address (`ProxyServer`) is **not** deleted or modified – only the enable switch is turned off.

The `ipconfig /flushdns` command clears the local DNS cache, ensuring subsequent name resolution does not use stale proxy‑related entries.

---

### Important Notes

- **Permissions**: Modifying HKCU does not require admin rights, but flushing DNS does. Without admin, the flush command is silently redirected (error hidden), which does not affect the proxy disable.
- **Popup Security**: The popup is triggered via PowerShell or VBScript; some security software may intercept or warn – this is normal.
- **Scope**: Only affects applications that follow the system proxy settings (e.g., Internet Explorer, Edge, Chrome). Some applications (e.g., Firefox) use their own proxy configuration and are not affected.
- **Re‑enabling**: To turn the proxy back on, manually set `ProxyEnable` to `1` or re‑run your proxy tool.

---

### Troubleshooting

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| Popup does not appear | PowerShell/VBScript disabled or blocked by security software | Check if the popup was blocked; verify `ProxyEnable` became `0` in the registry manually |
| DNS flush fails | Not running as administrator | Re‑run the script as administrator |
| Proxy still active | Application cached old proxy settings | Restart the browser/application; or check if it uses a separate proxy (e.g., Firefox) |
| Script window closes instantly | Missing `pause` or file corruption | Ensure the script ends with `pause`; or run it manually from a command prompt to see output |

---

### License

This script is the result of Vibe Coding and can be freely used, modified, and distributed.
The author is not responsible for any system issues caused by using this script, so please assess the risks yourself.

---

### Special Statement
This README is generated with one click by AI after reading the script content.
If there are any mistakes, feel free to point them out.

---

### Follow my Twitter account

https://x.com/intent/follow?screen_name=xiaoyi_0324
