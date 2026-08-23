# Quantum Route Forge — 最终项目代码

本目录是 DeepBlock 路线优化项目的精简提交版，只包含最终应用运行、核心算法实现和离线验收所需内容。

## 环境要求

- Python 3.12
- Windows PowerShell（以下命令也可按当前终端等价调整）

## 安装与运行

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python app.py --port 8050
```

浏览器访问 `http://127.0.0.1:8050`。

默认 Hardware 模式只执行 dry-run，不会提交真实量子任务。项目根目录已经提供 `.env`，其中的 API Token 初始为空。若需运行 Quafu 真机任务，请打开 `.env`，在 `QUAFU_API_TOKEN=` 后填写使用者自己的访问令牌，并在页面中明确确认真实提交。

```dotenv
QUAFU_API_TOKEN=填写使用者自己的Token
QUAFU_BASE_URL=https://quafu-sqc.baqis.ac.cn/
```

未填写 Token 不影响 Web 应用、经典优化、随机基线、精确基线和理想模拟器运行，只会禁用真实量子硬件提交。请勿把已经填写真实 Token 的 `.env` 转发给其他人。

## 验收测试

```powershell
python -m pytest -q
```

提交包内的测试覆盖最终 Web 入口、DeepBlock 分块/代理 QUBO/评估流程、运行历史，以及经典优化烟雾测试。测试不需要真实硬件令牌或网络访问。

## 目录说明

```text
app.py                         最终 Dash Web 应用入口
src/quantum_route_forge/       路线优化、量子测量与 DeepBlock 核心实现
tests/                         与最终项目直接相关的离线验收测试
requirements.txt               Python 依赖
.env                           Quafu 真机配置（初始 Token 为空）
LICENSE                        开源许可证
```

运行时产生的历史记录会写入 `results/competition_history/`。该目录不是源码，因此未包含在提交包中。
