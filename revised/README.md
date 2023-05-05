# Documentation

## ELO Score Excel File Format Guide
The excel file used for capturing data should have a format with multiple sheets where each sheet is used for a specific cage. Each sheet contains rows where each row is an experiment and blocks of rows are referred to as sessions.
The headings on each sheet should be in the first/top row and be written in full __lowercase__. With the following headers:
* `runner` - This header designates the name of the person supervising each interactive experiment. each session is conventionally supervised by one in person. 
* `date` -  This header records the date at which each experiment was performed. Conventionally a session is completed on a single day. The date should be recorded in the following format: __DD MM YYYY__. Note, excel will automatically convert most date-like texts to a date object.
* `match` - This column records the IDs of the individuals participating in the experiment. The data in this column should be recorded with the following format: __<individual ID 1>vs<individual ID 2>__. Note, no spaces are used.
* `winner` - This indicates the winner of each experiment. This should be the ID of an individual participating in the experiment. Note, if no ID is shown here the experiment will be discarded in the ELO calculation. 
* `loser` - This indicates the loser of each experiment. This should be the ID of an individual participating in the experiment. Note, if no ID is shown here the experiment will be discarded in the ELO calculation. 
* `ties` - ???
* `notes` - This is an optional column but is encouraged. Taking notes during experimentation may give further insights when all experiments are analyzed. 

An example template of what the input excel file should look like can be found [here](https://github.com/padillacoreanolab/social_competiton_elo_rating/blob/main/jupyter_notebooks/data/pilot_3_tube_test.xlsx). 

## Methods to calculate ELO scores:
#### 1. [Jupyter Notebook](https://github.com/ChristopherMarais/social_competiton_elo_rating/blob/main/revised/tube_test_processing_GCM.ipynb)
#### 2. [Python file with params.yaml](https://github.com/ChristopherMarais/social_competiton_elo_rating/blob/main/revised/tube_test_processing.py)
#### 3. [Huggingface Spaces Webapp](https://huggingface.co/spaces/ChristopherMarais/ELO_scores)

\* Method 1 and 2 both rely on functions from this repository. Make sure to clone this repository to use those approaches. Additionally, method 1 and 2 also require a specific suite of python packages. The `environement.yml` file can be used to create a conda environment that includes the required packages with the following code:

```
conda env create -f environment.yml
```

### 1. [Jupyter Notebook](https://github.com/ChristopherMarais/social_competiton_elo_rating/blob/main/revised/tube_test_processing_GCM.ipynb)
The jupyter notebook has a cell here a number of parameters have to be filled out before running it. Thereafter it generates the output in an output folder. The parameters are described within the notebook itself. 

### 2. [Python file with params.yaml](https://github.com/ChristopherMarais/social_competiton_elo_rating/blob/main/revised/tube_test_processing.py)

The Python script `tube_test_processing.py` is exactly the same as the notebook but is run from the terminal. The terminal command has one parameter indicating the full path to the `params.yaml` file that the python script relies on. The script can be run from the terminal with the following code:

```
python tube_test_processing.py -p ./params.yaml
```
The `params.yaml` file contains the same arguments to the parameters in the notebook. These parameters should be filled out in the file before running the python script. 

#### Inputs:
The (1) Jupyter notebook and (2) python script both rely on the following parameters:
* `raw_data_file_path` (str) - This is the full path to the excel data capturing file. The default is None. 
* `inputted_sheet_names_list` (list) - This is a list of all the sheet names that should be included in the ELO calculations. The default is all the sheets are included.
* `session_divider_column` (str) - This designates the column that is used to divide the data up into sessions. The assumption is made that the values in the session_divider_column do not change throughout a session. The default is "date" but, "runner" is also a good option.
* `header_row_dict` (dict) - This is a dictionary to indicate which rows are the rows with the headers in for each sheet. The dictionary takes sheet names as keys and header row numbers as values. It is recommended to leave this dictionary empty and rather change the excel spreadsheet so that each sheet's headers are on the first row. The default is 0 for each sheet.
* `id_to_cage` (dict) - This input is used ot change the origin cage for an individual. The dictionary takes individual IDs as keys and origin cage names as values. The default is that each individual is assigned the cage wherein it was last experimented on.
* `cage_to_strain` (dict) - This is to assign the strain of each individual and add that information in the output table. This can be left blank. This takes a dictionary with individual IDs as keys and strain as values. 
* `subfolder_name` (str) - This is the folder name that will be generated within the output folder. It is recommended to name this folder a general name that describes the entire excel file. 
* `all_sheet_scores_name` (str) - This is the name of the CSV file where all the ELO scores are saved in. This cannot be left blank. 
* `final_elo_score_name` (str) - This is the name of the CSV file wherein all the final ELO scores for each individual are saved. This cannot be left blank. 
* `aggregate_all_pairwise_name` (str) - This is the name of the CSV file containing information on which individuals were dominant in every pairwise comparative experiment that was performed. This cannot be left blank. 
* `save_plots` (bool) - This designates whether the plots should be saved or not. This takes either True or False with the default being True.

\*Note: The format of the values in the notebook and in the params.yaml file differ slightly in syntax. Please use the templates available in this repository as a guide.

#### Outputs:
\*Note: Outputs are sent to an output folder into a user named subfolder.
* `Plots` - For both the Notebook and Python script methods high resolution PNG and SVG images are downloaded alongside an interactive HTML version of each plot.  Note, the HTML interactive plots also have the functionality to export high resolution PNG plots of what is cropped or selected in interactive mode. Therefore the number of files generated are __selected_sheet_names x 3 (PNG, SVG, and HTML)__.
* `CSV Files` - 3 CSV files are generated for each run. These files can be named accordingly by the user and descriptions for their contents can be seen in the Inputs section. 

### 3. [Huggingface Spaces Webapp](https://huggingface.co/spaces/ChristopherMarais/ELO_scores)

The huggingface Spaces webapp is made using Gradio and is hosted for free on huggingfacehub. 
#### Inputs:
The inputs are similar to the ones described for the Notebook and Python script methods. The only notable differences are:
- The inputs are auto filled with their default values, but can be edited in the Inputs tab before clicking the `Calculate ELO scores button`. 
- The `id_to_cage` and `cage_to_strain`variables are combined. into one table where information can be filled out. 

#### Outputs:
- The output tab in the webapp only shows a small sample of each table and shows only one of the generated plots. To get the full CSV files and all the plots they need to be downloaded. 
- The SVG and PNG versions of the plots are not downloaded, only the interactive HTML versions are available. Keep in mind that the PNG versions can be generated from the HTML version when using the export to PNG camera button after opening the HTML interactive plots in the browser.
