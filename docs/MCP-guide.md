## SolidWorks-MCP

> 项目地址：https://github.com/hjbaard/SolidWorks-MCP

### Step-1 安装uv

- 按 `win+x` ，打开“终端”
- 执行命令安装：
    ```powershell
    winget install --id astral-sh.uv -e
    ```
- 完成后重新打开一个终端，验证：
    ```powershell
    uv --version
    uvx --version
    ```
    正常输出版本号即安装成功。

### Step-2 安装并打开 SolidWorks

- 百度网盘资源： https://pan.baidu.com/s/1GSeGaLDas8ZxkCIwwjWVZg?pwd=pico
提取码：pico

- 打开 SolidWorks，确保基本功能正常可用

### Step-3 接入 SolidWorks-MCP

- 在终端内运行 MCP 自检：
    ```powershell
    uvx solidworks-mcp --selftest
    ```
    期间将可以看到 SolidWorks 内自动执行一系列操作，部分操作可能有弹窗，需手工点击确定。
    > **注意：** 
    > 1. 不要使用带管理员权限的终端（除非SW也是管理员权限打开）
    > 2. 自检时SolidWorks 必须已经处于打开状态 
    > 3. 自检中如果提示测试项没有全部通过（例如“14 of 15 checks passed.”），但整个过程没有程序报错，则可以继续后续步骤。

- 进入 Codex 桌面版，依次点击 `编辑-设置-插件`

- 在 `添加-添加MCP服务器` 中，填入或选择以下参数：

    | 项目 | 内容 |
    |---|---|
    | 名称 | `solidworks` |
    | 连接类型 | `STDIO` |
    | 启动命令 | `uvx` |
    | 参数 | `solidworks-mcp` |

    其他字段留空，随后点击保存。

- 重启 Codex，并输入提示词：
    ```text
    使用 SolidWorks MCP 读取当前 SolidWorks 版本和文档信息，暂不修改模型。
    ```
    如果模型能正常输出回答，那么说明 MCP 注册成功。

## JLCeda-MCP

- 安装嘉立创EDA（专业版） V4.1.60以上版本
- 进入 Codex 桌面版，依次点击 `编辑-设置-插件`
- 在 `添加-添加MCP服务器` 中，填入或选择以下参数：

| 字段 | 内容 |
|---|---|
| 名称 | `jlceda` |
| 类型 | `STDIO` |
| 启动命令 | `lceda-pro.exe` 的实际完整路径 |
| 参数第 1 项 | `--mcp` |
| 参数第 2 项 | `stdio` |
| 环境变量、环境变量传递、工作目录 | 留空 |

- 重启 Codex，并输入提示词：
    ```text
    使用嘉立创MCP读取当前嘉立创EDA版本和文档信息，暂不修改文件。
    ```
    如果模型能正常输出回答，那么说明 MCP 注册成功。

## STM32CubeMX-MCP

> 项目地址：https://github.com/Wafleem/stm32cubemx_mcp

> 注：该 MCP 的局限在于不能实时操纵 CubeMX GUI 界面，只能读写静态 `.ioc` 文件，建议与桌面自动化 MCP 搭配使用。

### Step-1 获取项目

- 打开 powershell 终端，执行：
    ```powershell
    uv python install 3.12
    uvx --python 3.12 --from git+https://github.com/Wafleem/stm32cubemx_mcp.git stm32cubemx-mcp
    ```

- 完成后，程序会保持运行而非自动结束，这是正常的；按 Ctrl+C 退出即可。

### Step-2 接入 MCP

- 进入 Codex 桌面版，依次点击 `编辑-设置-插件`

- 在 `添加-添加MCP服务器` 中，填入或选择以下参数：

    | 字段 | 内容 |
    |---|---|
    | 名称 | `stm32cubemx` |
    | 连接类型 | `STDIO` |
    | 启动命令 | `uvx` |
    | 参数第 1 项 | `--python` |
    | 参数第 2 项 | `3.12` |
    | 参数第 3 项 | `--from` |
    | 参数第 4 项 | `git+https://github.com/Wafleem/stm32cubemx_mcp.git` |
    | 参数第 5 项 | `stm32cubemx-mcp` |
    | 环境变量 | `CUBEMX_MCP_CUBEMX_PATH` = `STM32CubeMX.exe` 所在的路径 |

    随后点击保存。

- 重启 Codex，并输入提示词：
    ```text
    使用 cubemx MCP 读取当前 CubeMX 基本信息。
    ```
    如果模型能正常输出回答，那么说明 MCP 注册成功。

## Windows-MCP 接入与使用指南

> 项目地址：https://github.com/CursorTouch/Windows-MCP

> 注：该 MCP 可以读取 Windows 窗口与界面状态，并执行鼠标、键盘和窗口操作。可与 STM32CubeMX-MCP 搭配使用；CubeMX 界面的控件识别效果需实际验证。

### Step-1 获取项目

- 如果尚未安装 uv，请先按照本文 SolidWorks-MCP 的 Step-1 安装。
- 打开 PowerShell 终端，执行：
    ```powershell
    uv python install 3.13
    uvx --python 3.13 windows-mcp serve
    ```

- 首次运行会下载依赖，可能需要几分钟。程序启动后保持运行、等待 MCP 消息是正常的；按 Ctrl+C 退出即可。若首次连接因安装依赖超时，依赖安装完成后重新连接。

### Step-2 接入 MCP

- 进入 Codex 桌面版，依次点击 `编辑-设置-插件`
- 在 `添加-添加MCP服务器` 中，填入或选择以下参数：

    | 字段 | 内容 |
    |---|---|
    | 名称 | `windows-mcp` |
    | 连接类型 | `STDIO` |
    | 启动命令 | `uvx` |
    | 参数第 1 项 | `--python` |
    | 参数第 2 项 | `3.13` |
    | 参数第 3 项 | `windows-mcp` |
    | 参数第 4 项 | `serve` |
    | 环境变量、环境变量传递、工作目录 | 留空 |

    随后点击保存。

- 如果提示找不到 `uvx`，在 PowerShell 中执行：
    ```powershell
    (Get-Command uvx).Source
    ```
    将输出的 `uvx.exe` 完整路径填入“启动命令”，不用额外添加引号。

### Step-3 验证连接

- 完全退出并重新打开 Codex，同时打开 CubeMX，将其置于前台。
- 输入提示词：
    ```text
    使用 Windows-MCP 读取当前桌面窗口和 CubeMX 界面状态，仅查看，不点击、不输入、不修改文件。
    ```
    如果模型成功调用工具并返回实际窗口或界面信息，说明 MCP 连接成功。仅输出一般性的文字说明不能作为连接成功的依据。

### Step-4 非英文 Windows 环境禁用 App 工具

- 项目 README 建议非英文 Windows 环境禁用 `App-Tool`。当前源码中该工具的实际注册名称是 `App`，用于启动应用、切换窗口和调整窗口大小。
- 编辑上述 MCP 配置，在“环境变量”中增加：

    | 名称 | 值 |
    |---|---|
    | `WINDOWS_MCP_EXCLUDE_TOOLS` | `App` |

    值区分大小写，填写 `App`，不要填写 `App-Tool`，不用额外添加引号。

- 也可以不设置环境变量，改为在原参数表末尾追加两项：

    | 字段 | 内容 |
    |---|---|
    | 参数第 5 项 | `--exclude-tools` |
    | 参数第 6 项 | `App` |

    对应完整命令为：
    ```powershell
    uvx --python 3.13 windows-mcp serve --exclude-tools App
    ```
    两种方式任选一种即可。如果另外设置了 `--tools` 或 `WINDOWS_MCP_TOOLS` 工具白名单，应从白名单中移除 `App`；白名单优先于排除列表。

- 保存后重新连接 MCP，必要时完全退出并重启 Codex。让模型列出 Windows-MCP 当前暴露的工具，确认其中没有 `App`。
- 禁用后，可手动打开 CubeMX 并置于前台，再读取界面。此设置只移除 App 工具，截图、界面读取、鼠标和键盘工具不会因此被移除；这些功能在 CubeMX 中的效果仍需实际验证。

> **注意：** 项目要求 Python 3.13 及以上版本。上述排除设置依据当前项目源码；若安装版本不支持，可先执行 `uvx --python 3.13 windows-mcp serve --help`，确认是否包含 `--exclude-tools`。

> 配置参考：[项目 README](https://github.com/CursorTouch/Windows-MCP)、[工具排除选项源码](https://github.com/CursorTouch/Windows-MCP/blob/main/src/windows_mcp/__main__.py)、[App 工具注册源码](https://github.com/CursorTouch/Windows-MCP/blob/main/src/windows_mcp/tools/app.py)。
