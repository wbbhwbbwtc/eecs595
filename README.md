# eecs595

To reproduce our results, please follow these steps:

## Requirements

`pip install -r requirements.txt`

## Usage
### Data and pretrained roberta-large preparation.
- Download drop data.
  
  `wget -O drop_dataset.zip https://s3-us-west-2.amazonaws.com/allennlp/datasets/drop/drop_dataset.zip`
  
  `unzip drop_dataset.zip`

- Download roberta model.
 
  `cd drop_dataset && mkdir roberta.large && cd roberta.large `
  
  `wget -O pytorch_model.bin https://s3.amazonaws.com/models.huggingface.co/bert/roberta-large-pytorch_model.bin`

- Download roberta config file.
  
  `wget -O config.json https://s3.amazonaws.com/models.huggingface.co/bert/roberta-large-config.json`
  - Modify `config.json` from `"output_hidden_states": false` to `"output_hidden_states": true`.
  
  
- Download roberta vocab files.
  
  `wget -O vocab.json https://s3.amazonaws.com/models.huggingface.co/bert/roberta-large-vocab.json`
  
  `wget -O merges.txt https://s3.amazonaws.com/models.huggingface.co/bert/roberta-large-merges.txt`  
  
### Train 


    `sh train.sh 345 5e-4 1.5e-5 5e-5 0.01`
    

### Eval
- Save the model as model.pt.
        
        `sh eval.sh drop_dataset/drop_dataset_dev.json prediction.json`
    
    
    `python drop_eval.py --gold_path drop_dataset/drop_dataset_dev.json --prediction_path prediction.json`
