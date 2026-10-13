# PICO-Humanoid 工具链指南

## SolidWorks

- **安装包资源**
    - 百度网盘： https://pan.baidu.com/s/1GSeGaLDas8ZxkCIwwjWVZg?pwd=pico
    - 提取码：pico

- **MCP资源**
    - 项目地址：https://github.com/hjbaard/SolidWorks-MCP
    - 接入文档：[SW-MCP](MCP-guide.md#solidworks-mcp "打开 MCP-guide.md")

## 嘉立创EDA

- **下载安装**
    - 下载地址：https://lceda.cn/page/download?src=index
    - 注意下载“专业版”及相应激活文件

        <img src="assets/jlceda.png" alt="jlceda" height="250">

- **MCP资源**
    - `jlceda-mcp` 为 `嘉立创EDA v4.1.60` 以上版本自带 
    - 接入文档：[JLC-MCP](MCP-guide.md#jlceda-mcp "打开 MCP-guide.md")

## CubeMX + VSCode插件

- **CubeMX安装** 
    - 官网地址：https://www.st.com.cn/zh/development-tools/stm32cubemx.html#get-software
    - 百度网盘：https://pan.baidu.com/s/12-O0fjpwXrd2t90N0UnCkQ?pwd=pico
    - 尚未找到广受好评的 `cubemx-mcp` 资源
        - 以下 MCP 仅能针对导出的 `.ioc` 文件作修改，无法实时操作 CubeMX GUI
        - 项目地址：https://github.com/Wafleem/stm32cubemx_mcp
        - MCP 接入文档：[CUBEMX-MCP](MCP-guide.md#stm32cubemx-mcp)

    > **注意：**
    > - CubeMX 生成代码时建议采用 `CMake` 框架而非Keil系的 `MDK-ARM`
    > - Keil-v5 安装包资源（备用）：
    https://pan.baidu.com/s/1LWUbThkNRGVo9Hb1mBBR_g?pwd=pico

- **VSCode-STM32 插件**
    - 参考教程：https://b23.tv/NYdF9eq

## 常用网站

- [立创商城](https://www.szlcsc.com/?c=Q4&msclkid=0645c5f663481271bd0faf3b9b607182 "访问外部链接")：查找电子元件，查看数据手册，采购器件
- [嘉立创客户中心](https://www.jlc-cnc.com/integrated/)：PCB 打样、3D 打印等