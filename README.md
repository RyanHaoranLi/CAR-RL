# Consistent Adversarial Robust Reinforcement Learning

This repository contains a reference implementation for Consistent Adversarial Robust Proximal Policy Optimization (CAR-PPO).  See our paper ["Towards Optimal Adversarial Robust Reinforcement Learning with Infinity Measurement Error"]() for more details. 

The reference implementation for Consistent Adversarial Robust Deep Q Networks (CAR-DQN) can be found at [RyanHaoranLi/CAR-DQN](https://github.com/RyanHaoranLi/CAR-DQN). See our paper ["Towards Optimal Adversarial Robust Q-learning with Bellman Infinity-error"](https://arxiv.org/abs/2402.02165) for more details. This paper has been accepted by [**ICML 2024**](https://proceedings.mlr.press/v235/li24cl.html) as an [**oral**](https://icml.cc/virtual/2024/oral/35463) presentation.

Our code is based on the [SA_PPO](https://github.com/huanzhang12/SA_PPO) codebase.


## Setup

First, clone this repository and install necessary Python packages:

```bash
git submodule update --init
pip install -r requirements.txt
cd src
```

Python 3.7+ is required. Note that you need to install MuJoCo 1.5 first to use the Gym environments. See [here](https://github.com/openai/mujoco-py/blob/9ea9bb000d6b8551b99f9aa440862e0c7f7b4191/README.md#requirements) for instructions.

## Training CAR-PPO Agents

To train an agent, use `run.py` in the `src` folder and specify a configuration file path.  All training hyperparameters are specified in a JSON configuration file.

Hopper CAR-PPO training (solved using SGLD):

```bash
python run.py --config-path config_hopper_car_ppo_sgld.json
```

Hopper CAR-PPO training (solved using PGD):

```bash
python run.py --config-path config_hopper_car_ppo_pgd.json
```

Change `hopper` to `walker`, `halfcheetah` or `ant` to run other environments.

Training results will be saved to a directory specified by the `out_dir` parameter in the JSON file. To allow multiple runs, each experiment is 
assigned a unique experiment ID, which is saved as a folder under `out_dir`.

## Evaluations

The natural performance of agents can be evaluated using `test.py`.  For example, evaluate the CAR-PPO (PGD) Hopper agent:

```bash
python test.py --config-path config_hopper_car_ppo_pgd.json --exp-id YOUR_EXP_ID --deterministic
```

To evaluate agents under random, critic, RS, and MAD attacks, see [SA-PPO/Agent Evaluation Under Attacks](https://github.com/huanzhang12/SA_PPO?tab=readme-ov-file#agent-evaluation-under-attacks) for instructions.

To evaluate agents under the SA-RL attack, see [ATLA](https://github.com/huanzhang12/ATLA_robust_RL) for instructions.

To evaluate agents under the PA-AD attack, see [PA-AD](https://github.com/umd-huang-lab/paad_adv_rl/tree/master/code_mujoco) for instructions.
