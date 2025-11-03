---
title: "在无代理服务器上远程使用 VSCode + Codex"
date: 2025-11-01T11:07:15+08:00
draft: false
tags: ["remote", "proxy", "codex", "vscode"]
---

这里记录一下如何通过 SSH 做端口转发，让 VSCode + Codex 插件直接连接远程服务器上的 Codex 服务。整体流程参考了 [cccignore 的这篇博文](https://cccignore.github.io/2025/06/21/%E8%BF%9C%E7%A8%8B%20SSH%20%E4%BD%BF%E7%94%A8%20Codex%EF%BC%9A%E8%BD%AC%E5%8F%91%E6%9C%AC%E5%9C%B0%20Clash%20%E4%BB%A3%E7%90%86%E5%88%B0%E6%9C%8D%E5%8A%A1%E5%99%A8/)，但是我最后还调整了 VSCode 的 `settings.json` 来固定端口。

## 场景说明

- **远程服务器**：位于内网或无外网代理环境，只能通过 SSH 访问；在服务器上启动 Codex 服务并监听本机端口。
- **本地电脑**：可以访问外网，也运行 Clash 等代理工具；使用 VSCode Remote-SSH 连接远程服务器。
- **目标**：VSCode 插件访问 `127.0.0.1:7890`（本地 Clash），并把请求转发到远程服务器上运行的 Codex。

整个过程不需要额外的中转机，而是单纯依赖 SSH 反向端口转发。


## 第一步：在本地建立反向转发

重点是把本地 Clash 的端口（默认 7890）与远程服务器的端口（7890）分别反向映射：

1. **转发本地代理到服务器**  
   在本地终端执行：

   ```bash
   ssh -p <your-server-port> \
       -R 7890:127.0.0.1:7890 \
       -o ServerAliveInterval=60 \
       your-user-name@your-server-ip
   ```

   含义：让服务器的 `127.0.0.1:7890` 指向本地 `127.0.0.1:7890`（即 Clash 代理）。

## 第二步：在远程服务器上设置代理环境变量
   在远程服务器终端执行：

   ```bash
        \\ bash
        echo 'export http_proxy="http://127.0.0.1:7890"' >> ~/.bashrc
        echo 'export https_proxy="http://127.0.0.1:7890"' >> ~/.bashrc
        echo 'export no_proxy="localhost,127.0.0.1,.local"' >> ~/.bashrc
        source ~/.bashrc

        \\ zsh
        echo 'export http_proxy="http://127.0.0.1:7890"' >> ~/.zshrc
        echo 'export https_proxy="http://127.0.0.1:7890"' >> ~/.zshrc
        echo 'export no_proxy="localhost,127.0.0.1,.local"' >> ~/.zshrc
        source ~/.zshrc
   ```

## 第三步：测试代理是否生效
   在远程服务器终端执行：

   ```bash
    curl -I https://www.google.com
    curl -I https://chat.openai.com
   ```
若输出包含 `HTTP/1.1 200 Connection established` 或 `HTTP/2 200`，说明代理成功。

## 第四步：VSCode Remote-SSH 设置
在本地VScode中`Ctrl+Shift+P`打开命令面板，输入 `Open SSH Configuration File`，在弹出的列表里选择当前用户的 `~/.ssh/config`（Windows 可见 `C:\Users\<用户名>\.ssh\config`），修改如下
   ```json
    Host Your-server-name
    HostName Your-server-ip
    User Username
    RemoteForward 7890 127.0.0.1:7890
    ServerAliveInterval 60
   ```


为了让 VSCode 在连接服务器时自动做 RemoteForward，并固定端口，需要在本地 VSCode 的 `settings.json` 添加：

```json
{
    "remote.SSH.remoteForwardPorts": [7890],
    "remote.SSH.serverPickPortsFromRange": {
        "start": 7890,
        "end": 7890
    },
    "remote.SSH.logLevel": "debug",
    "remote.SSH.configFile": "~/.ssh/config"
}
```

- `remoteForwardPorts` 会在连接远程时自动加上 `ssh -R 7897:localhost:7890`；
- `serverPickPortsFromRange` 保证远程端使用固定端口（避免 VSCode 随机占用其他端口）；
- `configFile` 指向上面的 SSH 配置，省得每次写长命令。



至此，即便服务器完全没有外网代理，也能顺利使用 VSCode + Codex 进行远程开发。如果你也遇到类似需求，希望这份记录能提供一些思路。祝开发顺利！ 🚀
