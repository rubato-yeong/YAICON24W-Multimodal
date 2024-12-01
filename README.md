![header](https://capsule-render.vercel.app/api?type=waving&color=0:7b4397,100:004e92&height=250&section=header&text=YAICON24W-Multimodal&desc=Team%20for%20Growing%20MLLMs&fontAlign=38&fontAlignY=40&fontSize=50&fontColor=f7f5f5&descSize=25&descAlign=21)

<h3 align="center">🥉 YAICON24W 3rd Prize 🥉</h3>

<br>

# 🔍 Project Overview

### Introduction

> **Note** this project is not a full-fledged research project and is only a preliminary exploration. Do not use the results of this project as a reference for any research or development.

This is the repository for **"Can We Add Personalized Knowledge to LVLMs Naively? : A Preliminary Exploration"** in *YAICON 2024 Winter*. This project is a preliminary exploration of adding personalized knowledge to Large Vision-Language Models (LVLMs) naively (i.e., only w/ fine-tuning).

### Preliminary Results

✨ **Key Finding**: LoRA can add knowledge while preserving the original capabilities of the LVLMs.

![output](https://github.com/user-attachments/assets/9b64fadf-c495-4038-8588-610c0e6123da)

![output1](https://github.com/user-attachments/assets/40153389-2f66-4f57-99cb-30226e74ba1e)

📌 **Qualitative Results**: LVLMs indeed demonstrate the ability to learn personalized knowledge without relying on memorization at certain points.

![image](https://github.com/user-attachments/assets/fc797f27-5c84-443e-abc9-685175d273b6)
![image](https://github.com/user-attachments/assets/d30a9017-20e3-4003-b734-91f0d8c3580b)

### Discussion

* Related with [LoRA Learns Less and Forgets Less](https://arxiv.org/abs/2405.09673)
* Limitations: Unefficient training scheme / Only applied to a small-scale dataset

<br>

# 🧪 Tutorial

### Installation

1. Install Necessary Packages

```bash
conda create -n llava python=3.10 -y
conda activate llava
pip install --upgrade pip  # enable PEP 660 support
pip install -e .
```

2. Install Additional Packages for Training

```bash
pip install -e ".[train]"
pip install flash-attn --no-build-isolation
```

### Training

1. Prepare Training Dataset (json file + image folder)

```json
[
  {
    "id": "000000033471",
    "image": "000000033471.jpg",
    "conversations": [
      {
        "from": "human",
        "value": "<image>\nWhat are the colors of the bus in the image?"
      },
      {
        "from": "gpt",
        "value": "The bus in the image is white and red."
      },
    ]
  }
  ...
]
```

2. Train LLaVA (Set `--data_path` and `--image_folder`)

```bash
bash scripts/v1.5/finetune_task.sh
bash scripts/v1.5/finetune_task_lora.sh
```

### Evaluation

1. Prepare Evaluation Dataset (jsonl file + image folder)

```json
{"question_id": 0, "image": "kar40.jpg", "text": "Could you provide details about the person in this picture?", "category": "default"}
{"question_id": 1, "image": "kar40.jpg", "text": "Who is the person shown in this image?", "category": "default"}
...
```

2. Evaluate LLaVA (Set `--model-path`, `--question-file`, `--image-folder`, and `--answers-file`)

> Tip: For faster evaluation, set `--max_new_tokens` to a smaller value. (llava/eval/model_vqa_loader.py)

```bash
bash scripts/v1.5/eval/***.sh
```

<br>

# 🐣 Contribution

### Team Members

* **Dabin Lee**: Leader, Presentation, Data Collection
* **Jinyeong Kim**: Model Implementation, Visualization, Presentation
* **Jungsik Yoon**: Background Research, Data Collection
* **Chanyong Yoon**: Data Collection
* **Sangmin Lee**: Data Preprocessing, Model Implementation

### Acknowledgement

We sincerely thank the organizers of [YAICON 2024 Winter](https://github.com/yonsei-YAI) for providing us with the opportunity to present our preliminary exploration. We also extend our gratitude for the excellent [LLaVA](https://github.com/haotian-liu/LLaVA) codebase.