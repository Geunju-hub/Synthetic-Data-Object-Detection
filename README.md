# 합성데이터 기반 객체 탐지 AI 경진대회

### 합성 데이터를 활용한 자동차 탐지 AI 모델 개발
- 합성데이터란 실제 환경에서 수집되거나 측정되는 것이 아니라 디지털 환경에서 생성되는 데이터셋으로,  최근 방대한 양질의 데이터셋이 필요해짐에 따라 그 중요성이 대두되고 있습니다.

- 합성 데이터는 데이터 라벨링 작업을 위한 2배 이상의 시간 절약과 10배 가까운 비용을 절감하게 하고, 자동화를 바탕으로 정확한 라벨링의 데이터 그리고 정확한 AI 모델 개발을 위한 데이터의 다양화를 가능하게 합니다.
- 학습용 합성데이터를 활용하여 `자동차 탐지를 수행하는 AI 모델`을 개발해야 합니다.


## Project structure
```
VISOL
├─ .gitignore
├─ archive  # implementation pytorch 
├─ data  
│  ├─ raw
│  │  └─ raw data
│  ├─ ensemble
│  │  └─ ensemble data
│  └─ submission
├─ models
│  └─ model file
├─ mmdetection
│  ├─ configs  # hyperparameter & path
│  │  ├─ _base_  
│  │  └─ visol  # model config
│  │      └─ model config file.py
│  └─ mmdet
├─ inference.py # Test Inference
├─ grad_cam.py  # GradCam
├─ ensemble.py  # weighted boxes fusion
└─ README.md
```
## Getting Started
`Python 3.8.10` `mmdetection 2.x`
```
git clone https://github.com/Myungbin/VISOL.git

python -m pip install --upgrade pip
python -m pip install -r requirements.txt

cd mmdetection
python .\tools\train.py .\configs\visol\{config_file.py}
python .\tools\test.py '{config_file_path}' '{model_result_path}' --format-only --out '{result_path}'
```
## Data
[Dataset Link](https://dacon.io/competitions/official/236107/data)  
The project utilizes a custom dataset for training and evaluation.
The dataset consists of labeled images with bounding box annotations for each object of interest.
The dataset is not included in this repository and needs to be prepared separately.


## Experiment
The default augmentations used were `Resize`, `Flip`, and `Normalize`.  
Faster R-CNN, EfficientDet, Swin Transformer, Libra R-CNN, and YOLO were used in the experiment.  
In the end, `Cascade R-CNN` models was used.

| Model         | Backbone | Depth | Augmentation                                      | Public mAp |
|---------------|----------|-------|---------------------------------------------------|------------|
| Cascade R-CNN | SwinT    | -     | Mixup, Cutout                                     | 0.89       |
| Libra R-CNN   | Resnest  | 200   | Mixup, Cutout, AutoAugment, PhotoMetricDistortion | 0.89       |
| Faster R-CNN  | ResNeXt  | 101   | Mixup                                             | 0.91     |
| Faster R-CNN  | ResNeSt  | 200   | Mixup                                             | 0.93     |
| Faster R-CNN  | ResNeSt  | 101   | Mixup, Cutout                                     | 0.95       |
| Cascade R-CNN | ResNeSt  | 200   | Mixup, Cutout, AutoAugment, PhotoMetricDistortion | 0.98      |
| ...           | ...      | ...   | ...                                               | ...        |


#### Ensemble
`Weighted-Boxes-Fusion` on the results of 8 models.

## Result
Public mAp `0.9964`  Private mAP `0.99403`  

To reproduce the results of a public mAP of 0.9964 and a private mAP of 0.99403, follow these steps  
In final folder `969.py`, the **seed** used was `1927851590`, and a **GPU** `NVIDIA RTX 3090` was utilized. 
For the other case with **seed** `378452678`, an **GPU** `NVIDIA A100`  was used.

You can find detailed information about the experimental results through the PowerPoint presentation.

## Development Environment
```
OS: Window11
CPU: Intel i9-11900K
RAM: 128GB
GPU: NVIDIA GeFocrce RTX3090 & RTX4090 & A100 & V100
```

## Host
- 주최 : 비솔(VISOL)  
- 주관 : 데이콘(DACON)
- 기간 : 2023.05.08 ~ 2023.06.19 09:59  
[Competition Link](https://dacon.io/competitions/official/236107/overview/description)
