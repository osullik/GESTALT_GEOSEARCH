# GESTALT: Geospatially Enhanced Search with Terrain Augmented Location Targeting

This git repository is for the work **GESTALT: Geospatially Enhanced Search with Terrain Augmented Location Targeting** presented at the 2nd ACM SIGSPATIAL International Workshop on Searching and Mining Large Collections of Geospatial Data in November 2023, [available online](https://dl.acm.org/doi/pdf/10.1145/3615890.3628535). 

## Application

A preliminary beta of the UI is available at [gestalt.umiacs.umd.edu/](https://gestalt.umiacs.umd.edu/)

## Presentation 
The workshop presentation is available in the [presentations directory](https://github.com/osullik/GESTALT_GEOSEARCH/tree/main/presentations), along with a recording of the talk. 

## Research Abstract:
Geographic information systems (GIS) provide users with a means to efficiently search over spatial data given certain key pieces of information, like the coordinates or exact name of a location of interest. Current GIS capabilities do not enable users to search for locations using imperfect or incomplete information easily. In these cases, GIS tools help narrow down a region of interest, but users must conduct a manual last-mile search to find the exact location of interest within that region. This typically involves the user visually inspecting many remote sensing or street-view images to identify distinct landmarks or terrain features that match the partial information provided. This step of the search process is a bottleneck. Taking inspiration from the way humans recall and search for information, we present the Geospatially Enhanced Search with Terrain Augmented Location Targeting (GESTALT), an end-to-end pipeline for extracting geospatial data, transforming it into coherent spatial relations, storing those relations, and searching over them. We contribute a new Swan Valley Wineries dataset and a proof of concept architecture that includes multiple methods for querying spatial configurations of objects, handling uncertainty in the information known about a location or object, and accounting for the fuzzy boundaries between locations.

## Replicating the Experiments

### Get GESTALT and configure the environment 

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

### Data
Copies of the experiment data are located in the GESTALT_GEOSEARCH [data directory](https://github.com/osullik/GESTALT_GEOSEARCH/tree/main/data) (i.e. not the Main GESTALT Repo) and contains three datasets

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

Note that Swan Valley has additional files in the Input Directory to reflect the ingestion of hand labeled data. 

You will need to copy these into the [GESTALT/data](https://github.com/osullik/GESTALT/tree/main/data) directory when you clone it down from github, overwriting any files that are currently there (may be different versions of the data)

#### [Optional] Recollecting the data. 
These commands should be run in the main GESTALT repo you cloned above, and assume a start point of ~/GESTALT

You are able to recollect the data yourself, given the mutable nature of OSM and Flickr it will lead to changes in the results from what we report here. 

To get the files from FLICKR you need API Keys. API access can be requested [here](https://www.flickr.com/services/api/misc.api_keys.html). You then need to add them to your local environment variables with commands

    export flickr_key=<your_api_key_here>
    export flickr_secret=<your_secret_key_here>

To use the end-to-end scripts, navigate to the scripts folder from the root directory **IMPORTANT: The scripts use relative directory addressing and all assume that they are being executed from within the ~/GESTALT/scripts directory**: 

    cd scripts

### Swan Valley Wineries:

    sh 99a_ingestSwanValley.sh	

### DC:

    sh 99b_IngestDC.sh

### HAMBURG:

    sh 99e_IngestHamburg.sh

Note that after you have run the shell scripts for the first time you may want to comment out the lines that invoke the querying of FLICKR - the results will be stored after a single run. 

## Code (Replication)


Change into the scripts directory: 

      cd scripts

run the experiment scripts

      zsh 99_experiments.sh
      zsh 99c_DC_experiments.sh
      zsh 99d_SV_experiments.sh

Analyze the output:



## Recompiling the paper from TeX:

### Setting up compilation environment for MacOS: 

1. Download [Homebrew](brew.sh): 

        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

2. Install TexLive: 

        brew install texlive

3. Install Inkscape

        brew install --cask inkscape

4. (If it isn't on your machine by default) GNU Make

        brew install make

### Setting up compilation environment For Windows: 

1. Run Powershell as administrator: 

2. Install [Chocolatey](https://chocolatey.org/): 

        Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

3. Install GNU Make: 

        choco install Make

4. Install Perl (for LatexMk)

        choco install strawberryperl

5. Install Ruby (for Editing Scripts)

        choco install ruby

6. Install TexLive Utilites: 

        choco install texlive

7. Install MiKTeX: 

        choco install miktex

8. Install LatexMK with MikTex Package Manager (through GUI)

9. Install InkScape

        choco install inkscape

## Paper
The published PDF, LaTeX source and key auxiliary files are located in the [papers directory](https://github.com/osullik/GESTALT_GEOSEARCH/tree/main/paper). 

To compile from scratch, change from the project root into the project directory: 

    cd papers

To compile the PDF, simply run the following from the root of the project directory:

    make gestalt.pdf

You'll notice a lot of random intermediary files get made. To get rid of them and leave your PDF use:

    make publish

Sometimes everything goes wrong and we need to start again, when that happens use: 

    make clean

The [scripts](https://github.com/osullik/GESTALT_GEOSEARCH/tree/main/paper/scripts) directory contains a collection of scripts taken from [Jordan Boyd-Graber](https://github.com/Pinafore/publications/tree/master/scripts) that are useful for editing and checking. Github tends to mess with the permissions on these, so you'll likely need to CHMOD them back to be executable again. The *make main.pdf* command uses some of these scripts, so it is a good idea to do that occasionally


## Citation

If you use this work, please include the following citation: 

      @inproceedings{Osullivan2023,
      title={GESTALT: Geospatially Enhanced Search with Terrain Augmented Location Targeting},
      author={O'Sullivan, Kent and Schneider, Nicole R and Rasheed, Aleeza and Samet, Hanan},
      booktitle={Proceedings of the 2nd ACM SIGSPATIAL International Workshop on Searching and Mining Large Collections of Geospatial Data},
      pages={1--8},
      year={2023}
}

## Contact

If you have any questions or feedback please reach out to 

  Kent - osullik [at] umd [dot] edu

  Nicole - nsch [at] umd [dot] edu