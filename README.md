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

## Experiment
The default augmentations used were `Resize`, `Flip`, and `Normalize`.  
EfficientDet, Swin Transformer, Libra R-CNN, and YOLO were used in the experiment.  
In the end, `Cascade R-CNN` and `Faster R-CNN` models were used.

| Model       | Backbone | Depth | Augmentation                                      | Public mAp |
|-------------|----------|-------|---------------------------------------------------|-----------|
| FasterRCNN  | ResNeXt  | 101   | Mixup                                             | 0.9133    |
| FasterRCNN  | ResNeSt  | 200   | Mixup                                             | 0.9341    |
| FasterRCNN  | ResNeSt  | 101   | Mixup, Cutout                                     | 0.95      |
| CascadeRCNN | ResNeSt  | 200   | Mixup, Cutout, AutoAugment, PhotoMetricDistortion | 0.969     |
| CascadeRCNN | ResNeSt  | 200   | Mixup, Cutout, AutoAugment, PhotoMetricDistortion | 0.982     |
| ...         | ...      | ...   | ...                                               | ...      |

#### Ensemble
`Weighted-Boxes-Fusion` on the results of 8 models. 


## Result
Public mAp `0.9964`  Private mAP `0.99403`  
You can find detailed information about the experimental results through the PowerPoint presentation.

## Development Environment
```
OS: Window11
CPU: Intel i9-11900K
RAM: 128GB
GPU: NVIDIA GeFocrce RTX3090
```

## Host
- 주최 : 비솔(VISOL)  
- 주관 : 데이콘(DACON)
- 기간 : 2023.05.08 ~ 2023.06.19 09:59  
[Competition Link](https://dacon.io/competitions/official/236107/overview/description)
