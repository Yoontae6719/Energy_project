# Study for developing deep learning models for energy demand forecast
## UNIST Financial Engineering Lab  

The purpose of this study is to developing DL model for enegy demand forcast.


The project can be accessed over at:
-  Temporal fusion transfomer [https://arxiv.org/abs/1912.09363](https://arxiv.org/abs/1912.09363)


## 📝 Table of Contents

if you want see the detail, click following link.
- [Participant](#Participant)
- [Features](#features)
- [Usage](#usage)
- [Requirements](./requirements.txt) 


## ✍️ Participant <a name = "Participant"></a>
Participating research team:
- [Yongjae Lee](https://www.notion.so/unist-felab/Yongjae-Lee-Ph-D-f43bbcebc05a4697b56b42db61e3e221)
- [Yoontae Hwang](https://www.notion.so/unist-felab/Yoontae-Hwang-9b1c43d6b1924d39a7940764fd0420b7) 
- [Minju Choi](https://www.notion.so/unist-felab/MINJOO-CHOI-b204363e14da45b59db347739f5e84ec)

## 🏁 Features <a name = "Features"></a>

## Folder Structure
  ```
  Energy/
  ├── main.py                  - main script to start training 
  │
  ├── trainer.py               - main script to start training. ( Input variable can be adjusted. )
  │
  ├── scheduler.py             - file that automatically runs multiple experiments
  │
  ├── train_validaion_plot.py  - Jupyter notebook file plotting through selected final model weights
  │
  ├── infer_jupyer.py          - Jupyter notebook file predicting test duration via selected final model weights
  │  
  ├── conf/ - holds configuration for training
  │   ├── conf.py
  │   ├── energy.yaml
  │   └── exp/
  │        └── xxx_tft.yaml    - yaml file for various experiments through parameter setting
  │
  ├── data/ - default directory for storing input data
  │   └── gas_data.xlsx
  │   └── elec_data.xlsx
  │   └── prepro.py            - for preprocessing my data
  │   └── temper.csv           - File with temperature related data
  │
  ├── dataset/                  - folder with preprocessed data
  │   └── utils.py              - utils for modeling (e.g. loss, csv function and metrics.)
  │   └── train_test_data/
  │            └── energy_df_all_sol.csv
  │            └── energy_test.csv
  │            └── energy_test_sol.csv
  │            └── energy_train.csv
  │
  ├── energy_log/
  │   └── defalut/               - trained models are saved here
  │          ├── version_0/
  │          └── version_n/
  │
  ├── energy_log_result_weight/   -Folder with the weights of the best performing models
  │   └── version_n/ 

  │
  └── result/                    - result of modeling
      └── measure_result/        - loss (e.g. MAE, RMSE, MAPE, SMAPE)
      └── prediction_csv/        - forecasting result file 
      └── variable_importance/   
   ```
  

## 🎈 Usage <a name = "usage"></a> 

After cloning this repo you need to install the requirements:
This has been tested with Python `v3.8.1`, Torch `v1.8.1` , pytorch-lightning, `v1.4.1` and pytorch-forecasting `v0.4.2`.

```shell
pip install -r requirements.txt
```

```
python main.py --help

usage: main.py [--help] [--exp_name] [--conf_file_path] [--seed] 

optional arguments:
  -h, --help            show this help message and exit
  --exp_name            Yaml file name. 여기에는 hyper parameter가 들어있습니다.
  --conf_file_path      Yaml file의 경로이며 입력하지 않아도, exp_name를 입력하면 자동으로 입력됩니다.
  --seed                Random seed

'''

Example of how to train the Temporal fusion transfomer:

```shell
python main.py --exp_name energy 
```

