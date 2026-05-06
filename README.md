# Snf7-puncta-counter

This tool was created to count *S. cerevisiae* cells and to identify Snf7 puncta by automated analysis in fluorescent microscopy images. The tool was used in this publication _____.

## Running the tool:

### System requirements:
This script was made to function in a jupyter notebook. The code was tested on mac and windows, using anaconda to open jupyter notebook and python. Anaconda is available for free online.

### Creating the environment and running the script:
- Download the environment file "Snf7_env.yml" and the code file "Snf7_puncta_counter.ipynb"
- To create the environment in anaconda navigator:
    - Open the tab "environments", click on the "import" icon and select the .yml file
    - The environment should get added to anaconda
    - Activate the environment by selecting it in the "environment" tab
    - Active environment has a green play button next to it and also can be  seen/changed in the "home" tab
    
- To create the environment using the terminal
    - Open terminal at the same folder where you placed the .yml file
    - Type "conda env create --name <name> --file=Snf7_env.yml"
    - To activate the environment, type "conda activate <name>"
    - When the environment is active, you can use the terminal to install new packages directly into it.
    - To deactivate the environment, type "conda deactivate"

- Potential issues when starting Jupyter notebook in the environment
    - You might get this message upon trying to open jupyter notebook: "The file /opt/anaconda3/envs/<name>/bin/jupyter_mac.command does not exist."
    - If that happens, you can find a "jupyter_mac.command" file in "/opt/anaconda3/bin" and you can then copy this file into the bin folder inside the folder of your environment ("/opt/anaconda3/envs/<name>/bin/").

### Practical information:

__How to acquire the images:__
- This program works best with z-stacks of yeast cells
    - It is written for z-stacks where all wavelengths were first acquired for one z-position
    - For optimal cell counting, use 10 steps with a spacing of 1 µm. You can then only use a subset of steps for the puncta counting.
- Acquire:
    - Images of the fluorescently labelled protein of interest
    - Images of a fluorescently labelled ER marker protein
    - Brightfield images

__How to set up the folder:__
- Set up a __master folder__ where all experiment folders to be analysed are put. Input the path to this folder as the "path" variable. This does not require change, as long as the same master folder is used.
    - Inside this folder, set up a folder for your __experiment__.
        - In this folder, the __results folder__ will appear as the program runs.
        - Inside the experiment folder, set up a folder for each __condition or strain__ of the experiment and split the images up accordingly.
            - This will be used to split up the images and get mean values for each condition.
            
__How to run the code:__
- Run all of the cells to read all functions
- The last cell might take a bit, since it's importing all of the modules (wait until an interactive user input window appears)
- Fill in the user input and press "Run interact" button

__This code will:__
- Import all images from the selected folder
- Create a max-z projection of the channel of the clustering protein
- Select the area of the cells present in the image and count the cells
- Detect protein clusters within the cell area and count them
    - Based on brightness, size and circularity of the clusters
    - All parameters are now designed to work best for the Snf7 puncta
- Plot different parameters in preliminary plots and export cell and cluster masks as tiff files for you to examine closer (for example in Fiji)

__The results folder:__
- Will be generated automatically in the __experiment__ folder.
- Will contain a subfolder for each condition, where the tiff files of the __cell mask__ and __puncta mask__ will be generated.
- Will contain the __preliminary graphs__ comparing the different conditions in different parameters
    - "...cells_with_puncta" = Bar graph of the percentage of cells that contain puncta
    - "...intensities" = Bar graph of the puncta intensity per pixel
    - "...violin" = Violin plot showcasing the distribution of number of clusters inside a cell
    - "...puncta" = Bar graph of number of puncta per number of cells
- Will contain an __excel sheet__ with all the results
    - Comparison tab = Will contain all the mean values for each category
    - puncta_in_cells tab = Will contain all the numbers of clusters for each cell in each category
    - parameters tab = Will contain all the parameters that were selected by the user, so you can always check how this set of values was obtained.
