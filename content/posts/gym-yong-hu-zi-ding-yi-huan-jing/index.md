---
title: "Gym 用户自定义环境实践"
date: 2022-11-23 10:26:05
draft: false
---

最近在做强化学习相关实验时，需要为 OpenAI Gym 构建一个专用的环境。把整个流程整理如下，方便之后复用，也希望能帮到同样折腾 Gym 的你。

## 1. 官方示例与初始化

- 阅读官方文档：<https://www.gymlibrary.dev/content/environment_creation/>
- 推荐克隆官方示例：

```bash
git clone https://github.com/Farama-Foundation/gym-examples
cd gym-examples
python -m venv .env
source .env/bin/activate
pip install -e .
```

示例仓库提供了常见的环境骨架，便于参考其注册方式、空间定义与调试流程。

## 2. 按需创建工程结构

如果需要完全自定义，可以建立如下目录：

```
my-gym/
├── setup.py
└── my_gym/
    ├── __init__.py
    ├── envs/
    │   ├── __init__.py
    │   └── myenv.py
    └── wrappers/
        ├── __init__.py
        └── relative_position.py
```

- `myenv.py`：环境核心逻辑，定义动作空间、状态空间、step/reset/render 等方法；
- `wrappers/`：可选，存放环境包装器；
- `setup.py`：使项目能被 `pip install -e .` 安装并在其他工程中引用。

## 3. 关键代码片段

```python
import gym
from gym import spaces
import numpy as np

class MyEnv(gym.Env):
    metadata = {"render.modes": ["human"]}

    def __init__(self, config=None):
        super().__init__()
        self.config = config or {}
        self.action_space = spaces.Discrete(5)
        self.observation_space = spaces.Box(
            low=-1.0, high=1.0, shape=(3,), dtype=np.float32
        )
        self.state = None

    def reset(self, *, seed=None, options=None):
        super().reset(seed=seed)
        self.state = np.zeros(3, dtype=np.float32)
        info = {"episode": 0}
        return self.state, info

    def step(self, action):
        # 根据动作更新状态，这里仅作示意
        self.state = np.clip(self.state + (action - 2) * 0.1, -1, 1)
        reward = -np.linalg.norm(self.state)
        terminated = bool(np.linalg.norm(self.state) < 0.1)
        truncated = False
        info = {}
        return self.state, reward, terminated, truncated, info

    def render(self):
        print(f"state: {self.state}")
```

## 4. 环境注册与安装

在 `my_gym/__init__.py` 中注册：

```python
from gym.envs.registration import register

register(
    id="MyEnv-v0",
    entry_point="my_gym.envs:MyEnv",
)
```

随后执行：

```bash
pip install -e .
```

安装完成后即可在其它项目中：

```python
import gym
import my_gym

env = gym.make("MyEnv-v0")
```

## 5. 调试建议

1. 使用 `env.reset()` / `env.step()` 单步验证奖励、终止条件等逻辑。
2. 为环境设置随机种子，确保实验结果可复现。
3. 如需可视化，可以简单打印训练过程指标或接入 `matplotlib`、`pygame` 等工具。

希望这份记录能帮助你快速搭建出自己的强化学习环境。如果有新的经验，欢迎继续补充完善。
