# Documentation

## ELO Score Excel File Format Guide
The excel file used for capturing data should have a format with multiple sheets where each sheet is used for a specific cage. Each sheet contains rows where each row is an experiment and bloks of rows are reffered to as sessions.
The headings on each sheet should be in the first/top row and be written in full __lowercase__. With the following headers:
* `runner` - This header designates the name of the person supervising each interactive experiment. each session is conventionally supervised by one in person. 
* `date` -  This header records the date at which each experiment was performed. Conventionally a session is completed on a single day. The date should be recorded in the following format: __DD MM YYYY__. Note, excel will automatically convert most date like texts to a date object.
* `match` - This coloumn records the IDs of the individuals participating in the experiment. The data in this column should be recorded with the following ofrmat: __<indiviudal ID 1>vs<indiviudal ID 2>__. Note, no spaces are used.
* `winner` - This indicates the winner of each experiment. This should be the ID of an idnividual participating in the experiemnt. Note, if no ID is shown here the experiemnt will be discarded in the ELO calcualtion. 
* `loser` - This indicates the loser of each experiment. This should be the ID of an idnividual participating in the experiemnt. Note, if no ID is shown here the experiemnt will be discarded in the ELO calcualtion. 
* `ties` - ???
* `notes` - This is an optional column, but is encouraged. Taking notes during experimentation may give further insights when all experiments are analyzed. 

An example template of what the input excel file should look like can be found [here](https://github.com/padillacoreanolab/social_competiton_elo_rating/blob/main/jupyter_notebooks/data/pilot_3_tube_test.xlsx). 

## Methods to calculate ELO scores:
#### 1. [Jupyter Notebook](https://github.com/ChristopherMarais/social_competiton_elo_rating/blob/main/revised/tube_test_processing_GCM.ipynb)
#### 2. [Python file with params.yaml](https://github.com/ChristopherMarais/social_competiton_elo_rating/blob/main/revised/tube_test_processing.py)
#### 3. [Huggingface Spaces Webapp](https://huggingface.co/spaces/ChristopherMarais/ELO_scores)

\* Method 1 and 2 both rely on functions from this repository. Make sure to clone this repository to use those approaches. Additionally, method 1 and 2 also require a specific suite of python packages. The `environement.yml` file can be used to create a conda envienment that includes the required packages with the following code:

```
conda env create -f environment.yml
```

### 1. [Jupyter Notebook](https://github.com/ChristopherMarais/social_competiton_elo_rating/blob/main/revised/tube_test_processing_GCM.ipynb)
The jupyter notebook has a cell here a number of parameters have to be filled out before running it. Thereafter it generates the output in an output folder. The parameters are described within the notebook iteself. 

### 2. [Python file with params.yaml](https://github.com/ChristopherMarais/social_competiton_elo_rating/blob/main/revised/tube_test_processing.py)

The Python script `tube_test_processing.py` is exactly the same as the notebook, but is run from the terminal. The terminal command has one parameter indicating the full path to the `params.yaml` file that the python script relieson. The script can be run from the terminal with the folowing code:

```
python tube_test_processing.py -p ./params.yaml
```
The `params.yaml` file contains the same arguments to the parameters in the notebook. These parameters should be filled out in the file before running the python script. 

#### Inputs:
The Jupyter notebook and python script both rely on the following parameters:
* 
