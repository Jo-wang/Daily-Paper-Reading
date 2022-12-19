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
- Instance-wise prompt query
- Objective
- 
### Experiments

### Notes
