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
- This paper found **both sharp and ﬂat minima can have a low perturbed loss**, implying that SAM does not always prefer ﬂat minima.

<img width="1000" alt="Screen Shot 2022-12-29 at 17 35 32" src="https://user-images.githubusercontent.com/46414159/209918805-d4dac5ba-042a-4aa2-83ac-cde67cfff0cc.png">

- Jointly minimizes the perturbed loss $f_{p}$ and the surrogate gap h: 
  - a low perturbed loss $f_{p}$ indicates a low training loss within the neighborhood (SAM), 
  - and a small surrogate gap h avoids solutions in sharp valleys and hence narrows the generalization gap between training and test performances. 
  - When both criteria are satisﬁed, we ﬁnd a generalizable model with good performances.

### Method
<img width="1000" alt="Screen Shot 2022-12-29 at 18 19 24" src="https://user-images.githubusercontent.com/46414159/209923690-42e01659-edbd-4e30-9415-4e58446b8973.png">

#### Surrogate Gap

<img width="1000" alt="Screen Shot 2022-12-29 at 18 25 10" src="https://user-images.githubusercontent.com/46414159/209924297-f287e85f-efb9-42fa-94b8-b5183614f4ee.png">

#### Surrogate Gap Guided Sharpness-Aware Minimzation (GSAM)
Minimize both perturbed loss $f_{p}$ and the surrogate gap h: $min_{w}(f_{p}(w), (\lambda) h(w))$ (gradient descent for the surrogate gap could potentially increase the loss $f_{p}$)
- Weighted perturbed loss and surrogate loss is not good as GSAM
<img width="780" alt="Screen Shot 2022-12-29 at 22 00 13" src="https://user-images.githubusercontent.com/46414159/209948235-7b48970c-7a4c-4737-a84e-2cc6197f61de.png">
- A Toy Example
<img width="790" alt="Screen Shot 2022-12-29 at 22 00 50" src="https://user-images.githubusercontent.com/46414159/209948282-8510b0c7-d39f-4974-b013-865295fc9548.png">


### Experiments

<img width="700" alt="Screen Shot 2022-12-29 at 22 07 01" src="https://user-images.githubusercontent.com/46414159/209948947-eff12969-e443-4d0d-a26e-afb6624fdda7.png">

<img width="700" alt="Screen Shot 2022-12-29 at 22 07 46" src="https://user-images.githubusercontent.com/46414159/209949049-f2883cbf-fb96-4a83-b3d2-192064723a81.png">

<img width="700" alt="Screen Shot 2022-12-29 at 22 09 45" src="https://user-images.githubusercontent.com/46414159/209949265-10b7e30d-68f1-48ae-8fc3-de6cafefba7a.png">

### Notes
