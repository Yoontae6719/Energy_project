# Study for developing deep learning models for energy demand forecast
## UNIST Financial Engineering Lab  

The purpose of this study is to developing DL model for enegy demand forcast.


The project can be accessed over at:
-  Temporal fusion transfomer [https://arxiv.org/abs/1912.09363](https://arxiv.org/abs/1912.09363)
-  N-beats [https://arxiv.org/abs/1905.10437](https://arxiv.org/abs/1905.10437)
-  DeepAR wolud be release. [Tentative] 



## 📝 Table of Contents

if you want see the detail, click following link.
- [Authors](#authors)
- [Features](#features)
- [Usage](#usage)
- [Requirements](./requirements.txt) 


## ✍️ Authors <a name = "authors"></a>
Participating research team:
- [Yongjae Lee](https://www.notion.so/unist-felab/Yongjae-Lee-Ph-D-f43bbcebc05a4697b56b42db61e3e221)
- [Yoontae Hwang](https://www.notion.so/unist-felab/Yoontae-Hwang-9b1c43d6b1924d39a7940764fd0420b7) 
- [Minju Choi](https://www.notion.so/unist-felab/MINJOO-CHOI-b204363e14da45b59db347739f5e84ec)

## 🏁 Features <a name = "Features"></a>


## Folder Structure
  ```
  Energy/
  ├── main.py - main script to start training and test
  │
  ├── trainer.py - main script to start training and test
  │
  ├── conf/ - holds configuration for training
  │   ├── conf.py
  │   ├── gas_tft.yaml
  │   └── gas_nbeates.yaml
  │
  ├── data/ - default directory for storing input data
  │   └── gas_data.xlsx
  │   └── prepro.py       - for preprocessing my data
  │   └── prepro_data.csv
  │   └── solution.csv
  │
  ├── dataset/ -  anything about data loading goes here
  │   └── dataset.py      - dataloader for modeling
  │   └── utils.py        - utils for modeling (e.g. loss, csv function and metrics.)
  │
  ├── lighting_logs/
  │   └── defalut/        - trained models are saved here
  │          ├── version_0/
  │          └── version_n/
  ├── plot/
  │   ├── n_beats/ 
  │   └── tft/ 
  │
  ├── trainer/ - trainers
  │   └── trainer.py
  │
  └── result/                - result of modeling
      └── measure
   ```
  

## 🎈 Usage <a name = "usage"></a> 

After cloning this repo you need to install the requirements:
This has been tested with Python `v3.8.1`, Torch `v1.8.1` , pytorch-lightning, `v1.4.1` and pytorch-forecasting `v0.4.2`.

```shell
pip install -r requirements.txt
```

The are various arguments available for training and testing the network.
모델을 트레이닝 하기전에 미리 `--conf_file_path`에서 hyper-parameter를 설정하여야합니다. `--exp_name`에서는 hyper-parameter를 설정하기 위해 다양한 실험을 셋팅할 수 있습니다. 만약, 예측지수를 제외한 변수를 학습하고 싶다면 `--inference`, `--only_use_month`
를 `False`로 지정하면 됩니다. 마지막으로 학습된 결과중 최적의 모델을 선택하여 결과를 test하는 경우 `--inference`를 `--True`로 지정하십시오.
```
python main.py --help

usage: main.py [--help] [--exp_name] [--conf_file_path] [--seed] [--inference] [--read_model_weight] [--only_use_month]

optional arguments:
  -h, --help            show this help message and exit
  --exp_name            Yaml file name. 여기에는 hyper parameter가 들어있습니다.
  --conf_file_path      Yaml file의 경로이며 입력하지 않아도, exp_name를 입력하면 자동으로 입력됩니다.
  --seed                Random seed
  --inference           모델의 test를 진행합니다.
  --read_model_weight   .//lighting_log//defalut// 안의 폴더에 있는 "version_x"를 입력합니다.  
  --only_use_month      예측 지수 변수를 사용여부를 결정합니다. 

[INFO] 
모델 학습(python main.py --exp_name gas_tft)시에 ./lighting_log/defalut에 자동으로 version_x형태로 폴더가 저장됩니다. 이 폴더는 학습된 모델의
파라미터와 weight 정보를 담고 있습니다. 
inference시에 read_model_weight에 이 version_x 폴더를 입력해주시면 자동으로 최종 결과를 plot과 result에 입력합니다.

[INFO]
N-beats 모델 학습시에는 예측변수를 사용하지 못합니다. 이 모델은 시계열 특성을 학습하는 모델로서 covariate 정보는 사용하지 않고 학습하도록 의도적으로
설계되어있습니다.
```

Example of how to train the Temporal fusion transfomer:

```shell
python main.py --exp_name gas_tft 
python main.py --exp_name gas_tft --inference False --only_use_month True
python main.py --exp_name gas_tft --inference False --only_use_month False
```


Example of how to test the Temporal fusion transfomer:

```shell
python main.py --exp_name gas_tft  --inference True --read_model_weight vesrion_0 --only_use_month True
python main.py --exp_name gas_tft  --inference True --read_model_weight vesrion_1 --only_use_month False
```


Example of how to train the N-beats:

```shell
python main.py --exp_name gas_nbeats 
```

Example of how to test the N-beats:

```shell
python main.py --exp_name gas_tft  --inference True --read_model_weight version_2
```




