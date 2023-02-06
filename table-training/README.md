# PubTables-1M

This repository contains code and links to data for the papers:
- ["PubTables-1M: Towards comprehensive table extraction from unstructured documents"](https://openaccess.thecvf.com/content/CVPR2022/html/Smock_PubTables-1M_Towards_Comprehensive_Table_Extraction_From_Unstructured_Documents_CVPR_2022_paper.html)
- ["GriTS: Grid table similarity metric for table structure recognition"](https://arxiv.org/pdf/2203.12555.pdf)


## Prerequisites
1. [Git LFS](https://git-lfs.com/) - for installation of model weights
2. [Anaconda](https://docs.anaconda.com/anaconda/install/) - for setting up environment

Add conda to path or open the project using the Anaconda prompt.
But Anaconda is a heavy utility, you can choose miniconda.

[Install miniconda](https://docs.conda.io/en/main/), then add conda to path or open the project using the miniconda prompt


## Model Weights
We provide the pre-trained models for table detection and table structure recognition trained for 20 epochs on PubTables-1M.

<b>Table Detection:</b>
<table>
  <thead>
    <tr style="text-align: right;">
      <th>Model</th>
      <th>Schedule</th>
      <th>AP50</th>
      <th>AP75</th>
      <th>AP</th>
      <th>AR</th>
      <th>File</th>
      <th>Size</th>
    </tr>
  </thead>
  <tbody>
    <tr style="text-align: right;">
      <td>DETR R18</td>
      <td>20 Epochs</td>
      <td>0.995</td>
      <td>0.989</td>
      <td>0.970</td>
      <td>0.985</td>
      <td><a href="https://pubtables1m.blob.core.windows.net/model/pubtables1m_detection_detr_r18.pth">Weights</a></td>
      <td>110 MB</td>
    </tr>
  </tbody>
</table>

<b>Table Structure Recognition:</b>
<table>
  <thead>
    <tr style="text-align: right;">
      <th>Model</th>
      <th>Schedule</th>
      <th>AP50</th>
      <th>AP75</th>
      <th>AP</th>
      <th>AR</th>
      <th>GriTS<sub>Top</sub></th>
      <th>GriTS<sub>Con</sub></th>
      <th>GriTS<sub>Loc</sub></th>
      <th>Acc<sub>Con</sub></th>
      <th>File</th>
      <th>Size</th>
    </tr>
  </thead>
  <tbody>
    <tr style="text-align: right;">
      <td>DETR R18</td>
      <td>20 Epochs</td>
      <td>0.970</td>
      <td>0.941</td>
      <td>0.902</td>
      <td>0.935</td>
      <td>0.9849</td>
      <td>0.9850</td>
      <td>0.9786</td>
      <td>0.8243</td>
      <td><a href="https://pubtables1m.blob.core.windows.net/model/pubtables1m_structure_detr_r18.pth">Weights</a></td>
      <td>110 MB</td>
    </tr>
  </tbody>
</table>

## Training and Evaluation Data
[PubTables-1M](https://msropendata.com/datasets/505fcbe3-1383-42b1-913a-f651b8b712d3) is available for download from [Microsoft Research Open Data](https://msropendata.com/).

But due to size of the original dataset we have included a condensed version of the dataset in the 'data' directory.

## Code Installation
Create a conda environment from the yml file and activate it as follows
```
cd table-training
conda env create -f environment.yml
conda activate table-training
```

## Model Training
The code trains models for 2 different sets of table extraction tasks:

1. Table Detection
2. Table Structure Recognition + Functional Analysis

To train, you need to ```cd``` to the ```src``` directory and specify: 
1. the path to the dataset, 
2. the task (detection or structure), and
3. the path to the config file, which contains the hyperparameters for the architecture and training.

To train the structure recognition model:
```
python main.py --data_type structure --config_file structure_config.json --data_root_dir ../../data
```

## Fine-tuning and Other Model Training Scenarios

If you want to restart training by fine-tuning a saved checkpoint, such as ```model_20.pth```, use the flag ```--model_load_path /path/to/model_20.pth``` and the flag ```--load_weights_only``` to indicate that the previous optimizer state is not needed for resuming training.


```
python main.py --data_type structure --config_file structure_config.json --data_root_dir ../../data ----model_load_path /path/to/model --load_weights_only
```