# GESTALT
This repository holds the paper, data and instructions for how to replicate the results presented at the [2ND ACM SIGSPATIAL INTERNATIONAL WORKSHOP ON SEARCHING AND MINING LARGE COLLECTIONS OF GEOSPATIAL DATA](https://geosearch-workshop.github.io/geosearch2023/#Program)

If you use this work, please include the following citation: 

    @inproceedings{Osullivan2023,
      author          = {O'Sullivan, Kent and Schneider, Nicole R and Rasheed, Aleeza and Samet, Hanan},
      booktitle       = {GeoSearch'23: Proceedings of the 2nd ACM SIGSPATIAL International Workshop on Searching and Mining Large Collections of Geospatial Data},
      editor          = {Hao, Li and Cavallaro, Gabriele and Heras, Dora Blanco and Lunga, Dalton and Werner, Martin and Z\"{u}fle, Andreas},
      title           = {GESTALT: Geospatially Augmented Search with Terrain Augmented Location Targeting},
      year            = {2023}    
      }

## Paper
The published PDF, LaTeX source and key auxiliary files are located in the [papers directory](https://github.com/osullik/GESTALT_GEOSEARCH/tree/main/paper). 

To compile from scratch, change from the project root into the project directory: 

    cd papers

Compilation has been tested on MacOS, Windows and Linux using: [latexMk](https://mg.readthedocs.io/latexmk.html), [inkscape](https://inkscape.org/) and [GNU make](https://www.gnu.org/software/make/). 
To initiate compilation, use: 

Run the following command: 

    make gestalt.pdf

Which will produce a file called gestalt.pdf. More detailed instructions on how to set up the compilation environment are located [here](https://github.com/osullik/project_template)

## Data
The data is located in the [data directory](https://github.com/osullik/GESTALT_GEOSEARCH/tree/main/data) and contains three datasets

  - Swan Valley (used for hand-labelling)
  - Washington DC (used for stress-testing)
  - Hamburg (used in the demonstration)

Each dataset has the following structure (with ... denoting the rest of the file path): 

```
  |
  |---Input
  |
  |---Output
      |---concept_mapping
          |---ConceptMaps....
          |---RelativeLocations...
      |---dataCollection
          |---locations...
          |---objects...
      |---ownershipAssignment
          |---...predicted_locations
          |---locations
          |---objects
```

Note that Swan Valley has additional files in the Input Directory to reflect the ingestion of hand labelled data. 

## Code (Replication)
The code is hosted on the main [GESTALT Repository](https://github.com/osullik/GESTALT). To replicate the experiments, assuming you have already cloned this repository into a directory called `GEOSEARCH23' and are in that directory. 

      git clone https://github.com/osullik/GESTALT.git

Replace the GESTALT data file with the GEOSEARCH data: 

      cp GESTALT_GEOSEARCH/data GESTALT/data

Change into the GESTALT directory

      cd GESTALT

Create and activate the virtual environment 

      python -m venv gestalt_env
      source gestalt_env/bin.activate
      pip install -r requirements.txt

Change into the scripts directory: 

      cd scripts

run the experiment scripts

      zsh 99_experiments.sh
      zsh 99c_DC_experiments.sh
      zsh 99d_SV_experiments.sh

TODO: Add in details for generating experiment results
