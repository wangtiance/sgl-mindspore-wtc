[English](README.md)

# SGL-MindSpore

本仓库为[SGLang](https://github.com/sgl-project/sglang)提供MindSpore模型支持。要使用MindSpore模型，您需要安装SGLang和本仓库。

## 支持矩阵

| 模型 | Ascend 910B/C | Ascend 310P |
|  ----  | ----  | ----  |
| Qwen-3 Dense | &#x2705; | &#x2705; |
| Qwen-3 MoE | &#x2705; | &#x2705; |
| DeepSeek V3 | &#x2705; |  |

## 安装

这是一个分步指南，帮助您在 SGLang 中运行 MindSpore 模型。

### 1. 安装 CANN

请安装 8.3.RC1 社区版：[https://www.hiascend.com/developer/download/community/result?module=cann&cann=8.3.RC1]
包括toolkit, kernels和nnal。请根据您的NPU选择合适的软件包。

### 2. 安装基于Ascend平台的SGLang

```
git clone https://github.com/sgl-project/sglang.git
cd sglang
cp python/pyproject_other.toml python/pyproject.toml
pip install -e "python[all_npu]"
```

### 3. 安装 sgl-kernel-npu

此步骤需要 GCC 版本 >= 9。您可以使用 `gcc -v` 检查 GCC 版本。如果版本低于 9，请安装更新的版本。

```
git clone https://github.com/sgl-project/sgl-kernel-npu.git
cd sgl-kernel-npu
bash build.sh -a kernels
pip install output/*.whl
```

### 4. 安装 MindSpore 模型存储库
```
git clone https://github.com/mindspore-lab/sgl-mindspore.git
cd sgl-mindspore
pip install -e .
```

## 使用示范

运行前请设置以下环境变量：
```
export ASCEND_RT_VISIBLE_DEVICES=0  # NPU 设备 ID
export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python  # 避免 protobuf 版本不匹配
```

### 离线推理演示：

```
python examples/offline_infer.py --model-path /path/to/your/model
```

要启用数据或张量并行，请修改以上脚本中的 `dp_size` 和 `tp_size`。

### 服务器推理演示：

```
python examples/server_infer.py --model-path /path/to/your/model
```

## 许可证

Apache License 2.0
