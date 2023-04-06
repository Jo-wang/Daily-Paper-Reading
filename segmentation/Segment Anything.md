## [Segment Anything](https://scontent-syd2-1.xx.fbcdn.net/v/t39.2365-6/10000000_900554171201033_1602411987825904100_n.pdf?_nc_cat=100&ccb=1-7&_nc_sid=3c67a6&_nc_ohc=Ald4OYhL6hgAX9ic6m_&_nc_ht=scontent-syd2-1.xx&oh=00_AfDNPDvMMYKShmkjzkfic38J-wrULgV3jaInSWB5uZD8Rg&oe=643306A7)

**From Meta AI Research**

<img width=700 alt="1680744562276" src="https://user-images.githubusercontent.com/46414159/230249896-8abccbb5-3e12-4b20-9371-4f379e6d9a91.png">


### Introduction and background
- What we expect of a one-for-all segmentation model? 
- **A: support flexible prompts; ambiguity-aware**
- Architecture?
- **A: Similar to CLIP, an image encoder, a prompt encoder and a mask decoder**
- How to collect huge amount of data?
- **A: build a data engine, co-develop model with model-in-the-loop dataset annotations.**
  - 1. assisted-manual: assists annotators in annotating masks, similar to a classic interactive segmentation setup
  - 2. semi-automatic: automatically generate masks for a subset of objects by prompting it with likely object locations and annotators focus on annotating the remaining objects, helping increase mask diversity
  - 3. fully automatic: prompt SAM with a regular grid of foreground points, yielding on average ∼100 high-quality masks per image
- xxx

### Method

### Experiments
- dataset: SA-1B, includes more than 1B masks from 11M licensed and privacy-preserving images
### Notes
