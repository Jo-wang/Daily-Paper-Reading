## [Learning To Prompt for Continual Learning](https://openaccess.thecvf.com/content/CVPR2022/html/Wang_Learning_To_Prompt_for_Continual_Learning_CVPR_2022_paper.html)
CVPR2022

Ranking: 4 

### Introduction and background
![Screen Shot 2022-12-19 at 12 39 53](https://user-images.githubusercontent.com/46414159/208337120-ab62da0a-827c-494d-9272-bb8dfaf98744.png)

- model overfit on the currently available data, and
- suffers from performance deterioration on previous data due to catastrophic forgetting 
- Rehearsal buffer suffer from substantial performance deterioration with smaller buffer size, and
- ineffective when a rehearsal buffer is not allowed 
- Things need to be focused:
  - more intelligent and succinct episodic memory system?
  - automatically select relevant knowledge component for arbitrary sample **without knowing its task identity**?
- Solution: Proposes Learning to Prompt for Continual Learning (L2P)

### Method
#### Types of continual learning
A sequence of tasks D, where $D_{t}$ is $t^{th}$ task.   
- class-incremental learning: each task have different classes
- task-incremental learning: task identity is known at test time; each task have different classes
- domain-incremental learning: maintains the same set of classes for every task and only changes the distribution of x by task.
- task-agnostic setting: task data in D changes smoothly, and the task identity t is unknown

This paper: class-incremental and domain-incremental => task-agnostic

![image](https://user-images.githubusercontent.com/46414159/208336162-a5e0720d-2532-4bbf-a73d-5a627562529a.png)
#### L2P
- From prompt to prompt pool
  - Use prompt pool to store encoded knowledge: $P={P_{1}, P_{2}, ..., P_{M}}$, M is total num of prompts.
  - $x_{p} = [P_{s1}; ..., P_{sN}; x_{e}]$, the input embedding is a concat of subset of prompt pool and the feature $x_{e}$
- Instance-wise prompt query: ${(k_{1},P_{1}), (k_{2},P_{2}),...,(k_{M},P_{M})}$; let the input instance itself decide which prompts to choose through query-key matching. So the author propose a query function q that encode the input x to the same dimension as the key.
  - use the whole pre-train model as a frozen feature extractor to get the query features: $q(x)=f(x)[0,:]$ 
  - define a function $\gamma$ to score the match between the query and prompt key. 
  - ![Screen Shot 2022-12-19 at 15 55 42](https://user-images.githubusercontent.com/46414159/208357494-44e17827-7941-4cb3-8a2c-d95de68d3f5d.png)
decouples the query mechanism learning and prompt learning processes
- extension of task boundary: maintain a prompt frequency table $H_{t}=[h_{1},h_{2},...,h_{M}]$, each entry represent normalized freq of prompt $P_{i}$ being selected up until task t-1. To encourage query mechanism to select diverse prompt,![Screen Shot 2022-12-19 at 16 20 48](https://user-images.githubusercontent.com/46414159/208360716-2ea2b5d7-226a-43da-b488-016f11e59cac.png)
$g_{\phi}$ is final classifier, ![Screen Shot 2022-12-19 at 16 21 39](https://user-images.githubusercontent.com/46414159/208360824-3a6140b4-848f-4298-b8aa-f937b1457b7e.png) the output hidden vectors corresponding to the N ·L p prompt locations are averaged before the classiﬁcation head.
$L$ is CE and the sec term is surrogate loss.

### Experiments
- Dataset: Split CIFAR-100
  - 5 datasets for class-incremental 
  - CORe50 for domain incremental 
  - Gaussian scheduled CIFAR-100 for task agnostic setting
 
 - Performance
 ![Screen Shot 2022-12-19 at 16 29 36](https://user-images.githubusercontent.com/46414159/208362228-a7741a7e-e882-493c-8c64-52bf4152c1f7.png)
 ![Screen Shot 2022-12-19 at 16 31 28](https://user-images.githubusercontent.com/46414159/208362339-08447a63-060a-4d14-9e6d-008d46e1b75b.png)

### Notes
