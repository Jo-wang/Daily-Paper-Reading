## [Surrogate Gap Minimization Improves Sharpness-Aware Training](https://arxiv.org/pdf/2203.08065.pdf)

ICLR2022

Ranking: 4
### Introduction and background
- About SAM (Sharpness-Aware Minimization):
  - SAM is a generalization method to find out the **flat minima** rather than the sharp minima is better when doing optimization.   
![image](https://user-images.githubusercontent.com/46414159/209905032-bfd84ce0-89a9-4942-b50f-0044e01f65b4.png)
  - Main process
    - 1. 基於參數 w 對 batch data S 計算 gradient G 
    - 2. 求解 G 的 dual norm，依照 dual vector 方向更新參數，得到 w+ε
    - 3. 基於參數 w+ε 對 S 計算 gradient G’ 
    - 4. 用 G’ 更新原本的的參數 w 
    - (官方code中實際上做法就是對梯度除以所有梯度的平方和開根號)
- xxx
- xxx

### Method

### Experiments

### Notes
