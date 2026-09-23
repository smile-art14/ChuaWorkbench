# Chua Workbench

面向 Chua 电路研究的 Windows 桌面分析工具，集成储备池计算、参数优化、非线性动力学分析与结果导出。

[下载最新版 v1.0.20](https://github.com/smile-art14/ChuaWorkbench/releases/tag/v1.0.20)

## 主要功能

- 读取 Chua 电路三路电压 TXT 数据，训练与管理储备池模型
- 绘制时间序列、V1–V2 相图及三路电压频谱
- 基于三维 Poincaré 状态和 DBSCAN 辅助判定基本周期
- 参数延拓扫描与分叉图实时增量绘制
- 差分进化超参数优化
- 使用 Benettin 双轨迹重标定法计算最大李雅普诺夫指数
- 使用 SINDy / STLSQ 稀疏回归辨识动力学方程
- 统一评估 NRMSE、周期一致率、关联维数 D2 和 SINDy 结构误差
- 从倍周期级联估计 Feigenbaum 常数

## 下载

| 版本 | 适用设备 | 下载 | 大小 |
|---|---|---|---:|
| CUDA | NVIDIA GPU，适合批量优化加速 | [下载安装器](https://github.com/smile-art14/ChuaWorkbench/releases/download/v1.0.20/ChuaWorkbench-v1.0.20-Windows-x64-CUDA-Setup.exe) | 约 1.12 GB |
| DirectML | 支持 DirectX 12 的 Intel、AMD 或 NVIDIA GPU，兼容范围更广 | [下载安装器](https://github.com/smile-art14/ChuaWorkbench/releases/download/v1.0.20/ChuaWorkbench-v1.0.20-Windows-x64-DIRECTML-Setup.exe) | 约 243 MB |

两个版本的界面和功能相同，仅计算后端不同。NVIDIA 用户优先选择 CUDA；其他 Windows GPU 可选择 DirectML。

> DirectML 的优势是兼容性。本项目包含较多串行储备池时间步，因此它在部分集成显卡上可能比 CPU 更慢。DirectML 安装包中，`auto` 默认使用 CPU；需要测试 GPU 时，请在“模型与优化”页选择 `gpu` 或 `directml`。

## 系统要求

- 64 位 Windows
- CUDA 版：兼容的 NVIDIA GPU 与显卡驱动
- DirectML 版：支持 DirectX 12 的 GPU 与较新的显卡驱动
- 建议保留足够磁盘空间用于安装包、程序文件和计算结果

安装包已包含 Python 及运行依赖，无需另行安装 Python、NumPy、SciPy 或 Matplotlib。

## 安装与使用

1. 下载适合显卡的 `Setup.exe`。
2. 双击安装器并按提示完成安装；可选择创建桌面快捷方式。
3. 从开始菜单或桌面启动 **Chua Workbench**。
4. 在“数据”页使用随软件提供的示例数据，或选择自己的 TXT 文件。
5. 按需进入模型与优化、单参数综合分析、分叉图、稀疏回归或误差评估页面。

程序默认安装到当前用户的 `%LOCALAPPDATA%\Programs\ChuaWorkbench`，无需管理员权限。

## 用户数据

首次启动时，程序会在以下位置准备示例数据、默认参数和结果目录：

```text
文档\ChuaWorkbench
├─ data\raw\100k    示例 TXT 数据
└─ results           图像、数值和评估结果
```

升级或卸载程序不会主动删除该目录。迁移数据时，备份整个 `文档\ChuaWorkbench` 文件夹即可。

内置示例文件与参数映射：

| 文件 | R |
|---|---:|
| `1480.txt` | 1.480 |
| `1467.txt` | 1.467 |
| `1455.txt` | 1.455 |
| `1443.txt` | 1.443 |

选择其他 TXT 文件时，程序会尝试从文件名识别 R 值，并在界面中显示文件与参数的映射。

## 文件校验

下载后可在 PowerShell 中执行：

```powershell
Get-FileHash .\ChuaWorkbench-v1.0.20-Windows-x64-CUDA-Setup.exe -Algorithm SHA256
Get-FileHash .\ChuaWorkbench-v1.0.20-Windows-x64-DIRECTML-Setup.exe -Algorithm SHA256
```

| 安装器 | SHA-256 |
|---|---|
| CUDA | `AF65B2C60F97BC54B717B5E8424E4E6AD2D3DE84FF88E380406C34AD3A2BD3DD` |
| DirectML | `E97B2F41356D370F2E910FB50FB2BF299DF6EE70941EA2F2470FFDF86A878064` |

## 常见问题

**Windows SmartScreen 提示未知发布者**

当前安装器尚未使用商业代码签名证书签名，因此首次运行时可能出现提示。请核对下载地址和上方 SHA-256 后再决定是否运行。

**程序无法启动或 GPU 后端不可用**

先更新显卡驱动。DirectML 用户也可在“模型与优化”页选择 `cpu` 验证基础功能，以排除 GPU 运行时兼容问题。

**计算结果在哪里？**

默认保存在 `文档\ChuaWorkbench\results`。

## 版本

当前发布版：**v1.0.20**  
完整安装包与更新记录见 [Releases](https://github.com/smile-art14/ChuaWorkbench/releases)。
