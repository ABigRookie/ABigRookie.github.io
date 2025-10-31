---
title: "Gym用户自定义环境"
date: 2022-11-23 10:26:05
draft: false
---
Gym官方教程：[https://www.gymlibrary.dev/content/environment_creation/]('https://www.gymlibrary.dev/content/environment_creation/')
## 创建自定义环境工程
- 方法一：git clone gym-examples
    - 从github上克隆Gym官方示例到本地进行自定义环境编写  
``` bash
# git clone from gym-examples
git clone https://github.com/Farama-Foundation/gym-examples
cd gym-examples
python -m venv .env
source .env/bin/activate
pip install -e .
```
- 方法二：自建环境工程文件
    - 自建环境工程文件，文件目录应如下（只列出必要文件）
```bash
my-gym/
    setup.py
    my_gym/
        __init__.py
        envs/   
            __init__.py
            myenv.py
        wrappers/
            __init__.py
            relative_position.py（不必须）
```
## 设计环境
自定义环境通常只需关注myenv的编写，myenv.py文件的整体框架如下：
```python
import gym
import numpy as np
from typing import Optional
import torch
from gym import spaces
import math

class MyEnv(gym.Env):
    def __init__(self, args1, args2, ...):
        super().__init__()

        self.args1 = args1
        self.args2 = args2
        ...

        # define action space
        # gym doc:
        # https://www.gymlibrary.dev/api/spaces/
        self.action_space = spaces.Discrete(ACTION_SPACE)

        # define observation space
        self.observation_space = spaces.Discrete(OBSERVATION_SPACE)

    # not necessary
    def _get_obs(self):
        return obs
    
    # not necessary
    def _get_info(self):
        return info
    
    
    def step(self, action):
        # input the action and step to next state
        # return the next_obs, reward, done and info
        return obs, reward, done, {}

    def reset(self, seed=None, options=None):
        # set ramdom seed if need
        super().reset(seed=seed)
        # reset the start observation and some parameters
        self.state = START_STATE
        self.paras1= PARAS1
        ...
        # return the start observation and info
        return observation, info

    def render(self, mode='human', close=False):
        # render the environments
        # can simply print some infomation of your training process
        print(f'Step:{self.count}')
        print(f'State:{self.state}')
```

## 修改配置文件
### 注册环境
- 为了保证Gym能够检测到用户自定义的环境，需要在/my-gym/my_gym/\__init__.py中对环境进行注册
```python
from gym.envs.registration import register

register(
    # the id of your env, which can be used to during environment creation
    id="MyEnv",
    # the entry point is the path of your env
    entry_point="my_gym.envs:myenv",
    # other parameters can be found at 
    # https://www.gymlibrary.dev/content/environment_creation/
)
```
- 同时在/my-gym/my_gym/envs/\__init__.py下需要如下设置
```python
from my_gym.envs.myenv import MyEnv
```
### 创建包
- 最后一步将环境工程文件构建为一个python包，需要配置/my-gym/setup.py，简单示例如下
```python
from setuptools import setup

setup(
    name="my_gym",
    version="0.0.1",
    install_requires=["gym==0.26.0", "pygame==2.1.0"],
)
```
### 安装包
- 在需要安装自定义环境的python环境下，通过pip安装自定义环境
```bash
pip install -e USER_DEFINE_ENV_PATH
```
### 加载环境
```python
import my_gym
import gym
env = gym.make('MyEnv')
```
到此，一个简单的用户自定义环境就配置完成啦🎉🎉🎉
