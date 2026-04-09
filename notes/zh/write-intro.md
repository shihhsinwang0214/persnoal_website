# Writing a Compelling Research Introduction

一個好的 introduction 不只是 summary，而是一個 **argument**。你的目標是讓讀者相信：這個問題是重要的、現有方法是不足的，而你的方法是自然且必要的下一步。

---

## Step 1: 建立「Macro」重要性
**Goal：** 讓讀者理解這個領域與問題的重要性（先抓住 attention）。

- **The Hook：** 從高層應用切入（例如 drug discovery, protein folding, generative modeling）。
- **The Bridge：** 將應用連結到具體的數學或計算問題。

### Example: The Macro Hook

| **Type** | **Example Text** |
|:---|:---|
| ❌ **Weak** | Deep learning has been very popular for modeling molecules in recent years. |
| ✅ **Strong** | While deep learning has transformed drug discovery, its utility is gated by the ability to predict molecular binding affinity with high precision under 3D geometric constraints. |

👉 重點：不要只是說「很熱門」，要說「**為什麼重要 + 卡在哪裡**」。

---

## Step 2: 「Failure Mode」（限制與缺口）
**Goal：** 精準指出現有 SOTA 方法的不足，建立你的 research gap。

- **Identify the Bottleneck：** 是 computational complexity（如 $O(N^2)$）？lack of theoretical guarantees？還是 loss of equivariance？
- **Failure Case：** 描述一個具體失敗場景，而不是抽象批評。

> **Action for the Writer：** 放一張 **Figure 1（Hero Graphic）**
>
> **Figure 1 Concept: The Contrast Plot**
> - **Left (Failure)：** Standard model 失敗（例如無法區分 isomers / 無法維持 symmetry）  
>   → *"Standard Methods: Geometric Drift"*
> - **Right (Solution)：** 你的方法成功  
>   → *"Ours: Symmetry-Preserving Representation"*

👉 重點：  
讓讀者「看到問題」，而不是只是「被告知問題」。

---

## Step 3: 「Principled」Proposal
**Goal：** 將你的方法呈現為對 Step 2 問題的「必然解答」，而不是隨意設計。

- **The Formula：**  
  “We propose **[Name]** via **[Technique]** to address **[Limitation]**.”
- **Highlight the Insight：** 強調 *why*，而不是只講 *what*。

### Example: The Proposal

| **Feature** | ❌ **Bad (Descriptive Only)** | ✅ **Good (Principled / Insightful)** |
|:---|:---|:---|
| **Logic** | We added a new layer to the transformer to make it faster. | We reformulate the attention mechanism as a **low-rank kernel approximation**, reducing complexity from $O(N^2)$ to $O(N)$. |
| **Phrasing** | Our model is called "Fast-ML" and it works well. | Our key insight is that by treating the problem as a **constrained optimization on a manifold**, we naturally satisfy the physical laws of the system. |

👉 重點：  
從「engineering tweak」升級為「mathematical inevitability」。

---

## Step 4: Quantifiable Achievement（結果與證據）
**Goal：** 用數據證明你的方法有效，並給出有衝擊力的結論。

- **The Evidence：** 使用 "Hero Numbers"（例如 100× speedup, SOTA on QM9）
- **The “So What?”：** 說明這些結果代表什麼意義

### Result Summary Table

| **Metric** | **Baseline (SOTA)** | **Our Method** | **Improvement** |
|:---|:---|:---|:---|
| **Accuracy (MAE)** | 0.152 | **0.084** | **45% Reduction** |
| **Inference Time** | 240 ms | **12 ms** | **20× Speedup** |
| **Memory Usage** | 8.2 GB | **1.1 GB** | **Scalable to Large Graphs** |

👉 重點：  
不要只說「better」，要量化「好多少」。

---

## Pro-Tips（寫作細節優化）

- **Zero Inference：**  
  不要讓讀者猜。慢就說多慢，錯就說錯在哪。

- **Checklist Test：**  
  問自己：  
  *“如果只看 introduction + Figure 1，能不能理解整篇 paper？”*

- **Signposting：**  
  用關鍵句引導讀者，例如：  
  - *"Crucially..."*  
  - *"Unlike previous approaches..."*  
  - *"Our primary contribution is twofold:"*

👉 重點：  
好的 introduction = 清楚 + 有說服力 + 有節奏感。