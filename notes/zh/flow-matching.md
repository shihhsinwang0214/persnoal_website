# Flow Matching：直觀入門

Flow Matching 是一種生成模型方法，其核心是學習一個 **vector field（向量場）**，將簡單分佈（如 Gaussian）連續地轉換為複雜的資料分佈。

---

## 1. 動機

在生成模型中，我們希望從目標分佈 $p_0(x)$（例如影像、分子）取樣。

常見策略是：

- 從簡單分佈 $p_1(x)$（如 Gaussian）開始
- 逐步轉換到 $p_0(x)$

Flow Matching 提供了一個**連續時間（continuous-time）**的觀點來描述這個過程。

---

## 2. 核心概念

我們定義一條分佈路徑：

$$
p_t(x), \quad t \in [0,1]
$$

其中：
- $p_1(x)$ 是簡單分佈（noise）
- $p_0(x)$ 是資料分佈

並學習一個向量場：

$$
v_t(x)
$$

使其滿足 **continuity equation（連續方程）**：

$$
\partial_t p_t(x) + \nabla \cdot (p_t(x) v_t(x)) = 0
$$

👉 這表示粒子沿著 $v_t$ 流動時，分佈會正確演化。

---

## 3. Flow Matching 的訓練

Flow Matching 不直接解 PDE，而是透過 regression 訓練。

我們取樣：
- $x_0 \sim p_0$
- $x_1 \sim p_1$
- 建立 interpolation 得到 $x_t$

然後定義目標速度場 $u_t(x)$，並最小化：

$$
\mathcal{L} = \mathbb{E} \| v_t(x_t) - u_t(x_t) \|^2
$$

👉 這個方法簡單且穩定，不需要估計 score。

---

## 4. 與 Diffusion Models 的關係

Diffusion models 同樣定義一條分佈路徑 $p_t(x)$，但：

- 它們學習的是 **score function**：
  $$
  \nabla_x \log p_t(x)
  $$

- 並透過隨機微分方程（SDE）建模

---

### 核心差異

| | Flow Matching | Diffusion Models |
|:---|:---|:---|
| 學習對象 | Velocity field $v_t(x)$ | Score $\nabla \log p_t(x)$ |
| 動態 | 決定性（ODE） | 隨機性（SDE） |
| 訓練方式 | Regression | Score matching |

---

## 5. 統一觀點

兩者其實都在描述「機率的運輸（transport）」：

- Diffusion：隨機運輸  
- Flow Matching：決定性運輸  

在某些條件下，Diffusion model 可以轉為：

👉 **Probability Flow ODE**

這說明：

> Flow Matching 與 Diffusion 本質上是同一個動態系統的不同表示方式。

---

## 6. 為什麼選擇 Flow Matching？

- 訓練目標更簡單
- 不需要 score estimation
- 推論速度通常更快（ODE）
- 可自由設計 path

---

## 7. 重點整理

Flow Matching 將生成模型重新詮釋為：

> 學習一個向量場，將機率質量從 noise transport 到 data。

這提供了一個更乾淨、具物理意義的生成建模框架。
