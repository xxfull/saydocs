# 費用

### 開平倉交易費

#### 公式與捨入

* **名義價值**

$$
N = Q \cdot P_{\text{fill}}
$$

* **開倉費**：

$$
F_{\text{open}} = \mathrm{round}(N \cdot r,\ 8)
$$

* **平倉費**：

$$
F_{\text{close}} = \mathrm{round}(Q \cdot P_{\text{exec}} \cdot r,\ 8)
$$

***

### 滑點

* **作用**：在**標記價**上，按**買貴 / 賣便宜**的方向**調整執行價**。

***

### 罰金預留

$$
R_p = M \times p
$$

* **M**：該逐倉**目前**的 `margin`；
* **p**：該標的或全域生效的**罰金率**。

若 M 小於等於 0，或 p 小於等於 0，則：

$$
R_p = 0
$$

**用於計算權益與強平觸發**時，盯市**權益**為：

$$
E = M + \mathrm{PnL} - R_p
$$

**維持要求**仍使用：

$$
\text{maintenance} = Q \cdot P_m \cdot m
$$

當且僅當權益**嚴格小於**維持要求時，系統才**可**強平。**邊界相等不強平**。

**預估強平價時**，同樣先計算**可用保證金**：

$$
M_{\text{eff}} = M - R_p
$$

#### 實際扣罰**上限**

* 記**盯市權益**為

$$
\text{eq} = M + \mathrm{PnL}
$$

* 先算原始罰金

$$
\text{penalty}_\text{raw} = \mathrm{round}(M \times p,\ 8)
$$

* **實扣**

$$
\text{penalty} = \min(\text{penalty}_\text{raw},\ \text{eq})
$$

* **餘量**

$$
\text{remainder} = \text{eq} - \text{penalty}
$$

也就是說，若全倉浮虧已使盯市權益很小，實扣罰金不會超過當時仍可分配的正權益。這可避免理論罰金大於剩餘權益時的過扣衝突。
