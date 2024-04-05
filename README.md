# Peft-starcoder-1b-Lora-P100

WE will fintune the starcoder-1b model which is trained on 80+ programming language.

As these models have a lot of trainable params (**1B** for this model) to tune them we require a lot of computation resources and powerful GPU so to solve this we use **PEFT** (Parameter Efficient Fine Tuning) and **LoRa** config (Low Rank Adaption) which reduces the no of trainable params by a lot so we can no tune this in our own collab notebook.
Below is just a brief depiction on how to make your own copilot which can auto complete your code.

To find out more about lora and peft refer to this paper
(https://huggingface.co/docs/peft/conceptual_guides/lora)

You can acces the notebook from here: (https://colab.research.google.com/drive/1GS4p4bFGhwq3JpHU2GhCyRFSfmujIG9n)


## Model description

The model Peft-starcoder-lora-P100 is a fine tuned version of the starcodebase-1b.It is trained on the following dataset 'smangrul/hf-stack-v1'
The model is basically a small replica of the github co-pilot it can autocomplete your python code(Machine Learning Related)


## Training and evaluation data

As mentioned above the model is trained on the dataset 'smangrul/hf-stack-v1'. The dataset contains 24k rows out of which 4k was used for evaluation.The remaining rows were shuffled
and used to train the model.The dataset contains three columns out of which the column on which model is tuned is called content. It contains code of different machine learning projects from which the model learns and tries to auto complete the code.

## Training procedure

The training procedure for the model involved utilizing the base mode "starcodebase-1b" and fine-tuning it on the dataset "smangrul/hf-stack-v1". Due to limited computational resources, techniques such as PEFT (Parameter Efficient Fine Tuning) and LORA (Low Rank Adaptation) were employed. PEFT and LORA are methods designed to optimize the training process by efficiently utilizing parameters and adapting to low-rank structures in the data, respectively. Following the setup of hyperparameters and LORA configuration, the model underwent training on a GPU P100. This comprehensive approach ensured an effective training process despite resource constraints, ultimately enhancing the model's performance and capabilities.

### Training hyperparameters

The following hyperparameters were used during training: 
  
  # Training arguments
 - SEQ_LENGTH = 2048 
 - MAX_STEPS = 100
 - BATCH_SIZE = 4
 - GR_ACC_STEPS = 1 
 - LR = 5e-4
 - LR_SCHEDULER_TYPE = "cosine"
 - WEIGHT_DECAY = 0.01
 - NUM_WARMUP_STEPS = 30
 - EVAL_FREQ = 100
 - SAVE_FREQ = 100
 - LOG_FREQ = 25
 - OUTPUT_DIR = "peft-starcoder-lora-P100"
  
  # Set bf16 to true in A100
 - BF16 = False
 - FP16 = False
  
 - FIM_RATE=0.5
 - FIM_SPM_RATE=0.5
  
  # LORA
 - LORA_R = 4
 - LORA_ALPHA = 8
 - LORA_DROPOUT = 0.1
 - LORA_TARGET_MODULES = "c_proj,c_attn,q_attn,c_fc,c_proj"

### Training results

| Training Loss | Epoch | Step | Validation Loss |
|:-------------:|:-----:|:----:|:---------------:|
| 1.0395        | 1.0   | 100  | 0.9165          |


### Framework versions

- PEFT 0.10.0
- Transformers 4.38.2
- Pytorch 2.1.2
- Datasets 2.1.0
- Tokenizers 0.15.2
