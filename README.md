<div align="center">

# DeepMath

<div>
🗄️ A Large-Scale, Challenging, Verifiable, and Decontaminated Mathematical Dataset for Advancing Reasoning
</div>
</div>

<div>
<br>

<div align="center">

[![Data](https://img.shields.io/badge/Data-4d5eff?style=for-the-badge&logo=huggingface&logoColor=ffffff&labelColor)](https://huggingface.co/datasets/Skywork/Skywork-OR1-RL-Data)
[![Github](https://img.shields.io/badge/Code-000000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/zwhe99/DeepMath)
[![GitHub Stars](https://img.shields.io/github/stars/zwhe99/DeepMath?style=for-the-badge&logo=github&logoColor=white&label=Stars&color=000000)](https://github.com/zwhe99/DeepMath)
[![arXiv](https://img.shields.io/badge/arXiv-1234.56789-b31b1b.svg?style=for-the-badge)](https://arxiv.org/abs/xxxx.xxxxx)
</div>
</div>

## 🔥 News

- **April 14, 2025**: We release **`DeepMath-103K`**, a large-scale dataset featuring challenging, verifiable, and decontaminated math problems tailored for RL and SFT. We open source:
  - 🤗 Training data: [`DeepMath-103K`](https://huggingface.co/datasets/zwhe99/DeepMath-103K)
  - 💻 Code: [`DeepMath`](https://github.com/zwhe99/DeepMath)
  - 📝 Paper detailing data curation: [`arXiv:xxxx.xxxxx`](https://www.google.com/search?q=[https://arxiv.org/abs/xxxx.xxxxx](https://arxiv.org/abs/xxxx.xxxxx))
  - *(Coming Soon)*: Model weights trained on DeepMath-103K.



## 📖 Overview

**`DeepMath-103K`** is meticulously curated to push the boundaries of mathematical reasoning in language models. Key features include:

**1. Challenging Problems**: DeepMath-103K has a strong focus on difficult mathematical problems (primarily Levels 5-9), significantly raising the complexity bar compared to many existing open datasets.

<div align="center"> <img src="./assets/github-difficulty.png" width="90%"/>

<sub>Difficulty distribution comparison.</sub> </div>

**2. Broad Topical Diversity**: The dataset spans a wide spectrum of mathematical subjects, including Algebra, Calculus, Number Theory, Geometry, Probability, and Discrete Mathematics.

<div align="center"> <img src="./assets/github-domain.png" width="50%"/>

<sub>Hierarchical breakdown of mathematical topics covered in DeepMath-103K.</sub></div>

**4. Rigorous Decontamination**: Built from diverse sources, the dataset underwent meticulous decontamination against common benchmarks using semantic matching. This minimizes test set leakage and promotes fair model evaluation.

<div align="center"> <img src="./assets/github-contamination-case.png" width="80%"/>

<sub>Detected contamination examples. Subtle conceptual overlaps can also be identified.</sub> </div>

**5. Rich Data Format**: Each sample in `DeepMath-103K` is structured with rich information to support various research applications:

<div align="center"> <img src="./assets/github-data-sample.png" width="90%"/>

<sub>An example data sample from DeepMath-103K.</sub> </div>

- **Question**: The mathematical problem statement.
- **Final Answer**: A reliably verifiable final answer, enabling robust rule-based reward functions for RL.
- **Difficulty**: A numerical score for difficulty-aware training or analysis.
- **Topic**: Hierarchical classification for topic-specific applications.
- **R1 Solutions**: Three distinct reasoning paths from DeepSeek-R1, valuable for supervised fine-tuning (SFT) or knowledge distillation.

## 📊Main Results

We are currently cooking the `DeepMath-Zero-7B` model using the `DeepMath-103K` dataset, starting from `Qwen2.5-7B-Base` via the zero RL method. Training is still in progress.


|          Model           | MATH 500 |  AMC23   | Miverva Math | Olympiad Bench |  AIME24  |  AIME25  |
| :----------------------: | :------: | :------: | :----------: | :------------: | :------: | :------: |
|     Qwen2.5-7B-Base      |   54.8   |   35.3   |     16.2     |      27.8      |   7.7    |   5.4    |
|  Open-Reasoner-Zero-7B   |   81.8   |   58.9   |     38.4     |      47.9      |   15.6   |   14.4   |
| Qwen-2.5-7B-SimpleRL-Zoo |   77.0   |   55.8   |     41.2     |      41.0      |   15.6   |   8.7    |
|     DeepMath-Zero-7B     | **85.5** | **64.7** |   **45.3**   |    **xx.x**    | **20.4** | **17.5** |



## 🎯Quick Start

#### Environment Preparation

```shell
git clone --recurse-submodules https://github.com/zwhe99/DeepMath.git && cd DeepMath

conda create -y -n deepmath python=3.12.2 && conda activate deepmath
pip3 install ray[default]
pip3 install torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 --index-url https://download.pytorch.org/whl/cu124
pip3 install flash-attn==2.7.4.post1 --no-build-isolation
pip3 install omegaconf==2.4.0.dev3 hydra-core==1.4.0.dev1 antlr4-python3-runtime==4.11.0 vllm==0.7.3
pip3 install math-verify[antlr4_11_0]==0.7.0 fire deepspeed tensorboardX prettytable datasets transformers==4.49.0
pip3 install -e verl
```



#### Evaluation
