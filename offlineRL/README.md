
# 离线强化学习（Offline Reinforcement Learning）学习笔记

## 🧠 简介

离线强化学习（Offline RL 或 Batch RL）致力于在 **不能与环境交互** 的前提下，仅依赖一个静态数据集进行策略学习。主要挑战是 **分布偏移（distributional shift）**，即学习策略与收集数据的行为策略不同，导致策略性能退化。

---

## 🔥 重要算法与论文

### 1. **BCQ (Batch-Constrained deep Q-learning)**
- **论文**: Fujimoto et al., ICML 2019
- **核心思想**：限制策略选择只在数据集中常见的动作附近，避免策略产生 out-of-distribution 行为。
- 方法结构：VAE + perturbation model + Q-filter
- 🔗 [论文链接](https://arxiv.org/abs/1812.02900)

---

### 2. **BEAR (Bootstrapping Error Accumulation Reduction)**
- **论文**: Kumar et al., NeurIPS 2019
- 使用 Kernel MMD 限制新策略不要偏离行为策略，从而减少估值误差积累。
- 🔗 [论文链接](https://arxiv.org/abs/1906.00949)

---

### 3. **CQL (Conservative Q-Learning)**
- **论文**: Kumar et al., NeurIPS 2020
- 保守地估计 Q 值，主动惩罚数据外动作的 Q 值，使策略更加稳健。
- 🔗 [论文链接](https://arxiv.org/abs/2006.04779)

---

### 4. **AWAC (Advantage-Weighted Actor-Critic)**
- **论文**: Nair et al., arXiv 2020
- 使用 advantage 对 BC 进行加权，使策略更合理地更新。
- 🔗 [论文链接](https://arxiv.org/abs/2006.09359)

---

### 5. **DT (Decision Transformer)**
- **论文**: Chen et al., NeurIPS 2021
- 基于 Transformer 的序列建模方法，输入 return + (state, action) 序列。
- 开创了将 Offline RL 建模为序列建模的方向。
- 🔗 [论文链接](https://arxiv.org/abs/2106.01345)

---

### 6. **TD3+BC**
- **论文**: Fujimoto & Gu, NeurIPS 2021
- 在 TD3 的 actor 更新中加入 behavior cloning loss，更稳定地进行策略学习。
- 🔗 [论文链接](https://arxiv.org/abs/2106.06860)

---

### 7. **IQL (Implicit Q-Learning)**
- **论文**: Kostrikov et al., ICLR 2022
- 无需明确提纯策略，直接从 Q 函数提取 actor。训练稳定、效果好。
- 🔗 [论文链接](https://arxiv.org/abs/2110.06169)

---

## 📦 常用数据集

### D4RL (Datasets for Deep Data-Driven RL)
提供 MuJoCo、AntMaze、Minigrid、Atari 等离线数据集。

- 🔗 [GitHub: D4RL](https://github.com/rail-berkeley/d4rl)

---

## 📚 学习清单与推荐路线

### 🧩 Step 1: 理解离线 RL 问题
- ✅ 阅读综述：[Offline Reinforcement Learning: Tutorial, Review, and Perspectives](https://arxiv.org/abs/2005.01643)
- ✅ 理解离线 RL 相比在线 RL 的主要区别：distribution shift, extrapolation error

### 🧪 Step 2: 入门经典方法
- ✅ 阅读 BCQ, BEAR, CQL 三篇经典论文
- ✅ 实现 BCQ 或 CQL（推荐从 [d3rlpy](https://github.com/takuseno/d3rlpy) 或 [CleanRL](https://github.com/vwxyzjn/cleanrl) 开始）

### 🤖 Step 3: Transformer 方法
- ✅ 阅读 Decision Transformer 论文
- ✅ 学习 HuggingFace 的 [Decision Transformer 实现](https://huggingface.co/blog/decision-transformer)

### 📊 Step 4: 应用与实践
- ✅ 下载并使用 D4RL 数据集，复现实验
- ✅ 探索医疗/推荐系统等 Offline RL 应用场景

---

## 🧭 方法结构总结

```
离线RL主流方法分类：
┌────────────────────────────┐
│   Value-based 方法        │
│   - BCQ, BEAR, CQL        │
├────────────────────────────┤
│   Actor-Critic 方法        │
│   - AWAC, IQL, TD3+BC      │
├────────────────────────────┤
│   Sequence modeling 方法    │
│   - Decision Transformer    │
└────────────────────────────┘
```

---

## 📘 参考资源

- Berkeley CS285 课程：[Deep RL](http://rail.eecs.berkeley.edu/deeprlcourse/)
- NeurIPS/ICLR 会议论文集
- GitHub: [d3rlpy](https://github.com/takuseno/d3rlpy), [CleanRL](https://github.com/vwxyzjn/cleanrl)
