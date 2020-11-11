# Ultimate Vocal Remover GUI v4.0.0
<img src="https://raw.githubusercontent.com/Anjok07/ultimatevocalremovergui/beta/img/UVRBETA.jpg" />

[![Release](https://img.shields.io/github/release/anjok07/ultimatevocalremovergui.svg)](https://github.com/anjok07/ultimatevocalremovergui/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/anjok07/ultimatevocalremovergui/total.svg)](https://github.com/anjok07/ultimatevocalremovergui/releases)

## About

This application is a GUI version of the vocal remover AI created and posted by GitHub user [tsurumeso](https://github.com/tsurumeso). You can find tsurumeso's original command line version [here](https://github.com/tsurumeso/vocal-remover). 

- **Special Thanks**
    - [tsurumeso](https://github.com/tsurumeso) - The engineer who authored the AI code. Thank you for the hard work and dedication you put into the AI application this GUI is built around!
    - [DilanBoskan](https://github.com/DilanBoskan) - The main GUI code contributor. Thank you for helping bring this GUI to life! Your hard work and continued support is greatly appreciated.

## Installation

The application was made with Tkinter for cross-platform compatibility, so it should work with Windows, Mac, and Linux systems. However, this application has only been tested on Windows 10 & Linux Ubuntu.

### Install Required Applications & Packages

1. Download & install Python 3.7 [here](https://www.python.org/ftp/python/3.7.0/python-3.7.0-amd64.exe) (Windows link)
    - **Note:** Ensure the *"Add Python 3.7 to PATH"* box is checked
2. Once Python has installed, download **Ultimate Vocal Remover GUI Version 4.0.0** here (link pending)
3. Place the UVR-V4GUI folder contained within the *.zip* file where ever you wish. 
    - Your documents folder or home directory is recommended for easy access.
4. From the UVR-V4GUI directory, open the Windows Command Prompt and run the following installs -

```
pip install --no-cache-dir -r requirements.txt
pip install torch==1.6.0+cu101 torchvision==0.7.0+cu101 -f https://download.pytorch.org/whl/torch_stable.html
```

### Running the Vocal Remover GUI & Models

- Open the file labeled *'VocalRemover.py'*.
   - It's recommended that you create a shortcut for the file labeled *'VocalRemover.py'* to your desktop for easy access.
     - **Note:** If you are unable to open the *'VocalRemover.py'* file, please go to the [**troubleshooting**](https://github.com/Anjok07/ultimatevocalremovergui/tree/beta#troubleshooting) section below.

## Option Guide

### Choose AI Engine:

- This option allows you to toggle between tsurumeso's v2 & v4 AI engines. 
  - **Note:** Each engine comes with it's own set of models.
  - **Note:** The TTA option and the ability to set the N_FFT value is limited to the v4 engine only.
  
### Model Selections:

The v2 & v4 AI engines use different sets of models. When selected, the models available for v2 or v4 will automatically populate within the model selection dropdowns. 

- **Choose Main Model** - Here is where you choose the main model to perform a deep vocal removal.
  - Each of the models provided were trained on different parameters, though they can convert tracks of all genres. 
  - Each model differs in the way they processes given tracks.  
     - The [*'Model Test Mode'*](https://github.com/Anjok07/ultimatevocalremovergui/tree/beta#checkboxes) option makes it easier for the user to test different models on given tracks.
- **Choose Stacked Model** - These models are meant to clean up vocal artifacts from instrumental outputs. 
  - The stacked models provided are only meant to process instrumental outputs created by a main model. 
  - Selecting the [*'Stack Passes'*](https://github.com/Anjok07/ultimatevocalremovergui/tree/beta#checkboxes) option will enable you to select a stacked model to run with a main model. 
    - If you wish to only run a stacked model on a track, make sure the [*'Stack Conversion Only'*](https://github.com/Anjok07/ultimatevocalremovergui/tree/beta#checkboxes) option is checked.
  - The wide range of main model/stacked model combinations gives the user more flexibility in discovering what model blend works best for the track(s) they are proessing.
    - To reiterate, the [*'Model Test Mode'*](https://github.com/Anjok07/ultimatevocalremovergui/tree/beta#checkboxes) option streamlines the process of testing different main model/stacked model combinations on a given track. More information on this option can be found in the next section.

### Checkboxes
- **GPU Conversion** - Selecting this option ensures the GPU is used to process conversions. 
  - **Note:** This option will not work if you don't have a Cuda compatible GPU.
    - Nividia GPU's are most compatible with Cuda.
  - **Note:** CPU conversions are much slower compared to those processed through the GPU. 
- **Post-process** - This option can potentially identify leftover instrumental artifacts within the vocal outputs. This option may improve the separation on *some* songs. 
  - **Note:** Having this option selected can potentially have an adverse effect on the conversion process, depending on the track. Because of this, it's only recommended as a last resort.
- **TTA** - This option performs Test-Time-Augmentation to improve the separation quality. 
  - **Note:** Having this selected will increase the time it takes to complete a conversion.
  - **Note:** This option is ***not*** compatible with the *v2* AI engine.
- **Output Image** - Selecting this option will include the spectrograms in *.jpg* format for the instrumental & vocal audio outputs.
- **Stack Passes** - This option activates the stacked model conversion process and allows the user to set the number of times a track runs through a stacked model.
  - **Note:** The best range is 3-7 passes. 8 or more passes can result in degraded sound quality for the track.
- **Stack Conversion Only** - Selecting this option allows the user to bypass the main model and run a track through a stacked model only.
- **Save All Stacked Outputs** - Having this option selected will auto-generate a new directory with the track name to your *'Save to'* path. The new directory will contain all of the outputs generated by each stack pass. The amount of audio outputs will depend on the number of stack passes chosen.  
  - **Note:** Each output filename will be appended with the number of passes it has had.
    - **Example:** If 5 stack passes are chosen, the application will provide you with all 5 pairs of audio outputs generated after each pass, if this option is enabled.
  - This option can be very useful in determining the optimal number of passes needed to clean a track.
- **Model Test Mode** - This option is meant to make it easier for users to test the results of different models, and model combinations, without having to manually create new folders and/or change the filenames. 
  - When this option is selected, the application will auto-generate a new folder with the name of the selected model(s) in the *'Save to'* path you have chosen.
    - The output files will be saved to the auto-generated directory.
    - The filenames for the instrumental & vocal outputs will have the selected model(s) name(s) appended to them. 

### Parameter Values

All models released here will have the values they were trained with appended to the end of their filenames like so, **'MGM-HIGHEND_sr44100_hl512_w512_nf2048.pth'**. The *'_sr44100_hl512_w512_nf2048'* portion automatically sets the *SR*, *HOP LENGNTH*, *WINDOW SIZE*, & *N_FFT* values within the application. If there are no values appended to the end of a selected model filename, the *SR*, *HOP LENGNTH*, *WINDOW SIZE*, & *N_FFT* fields will be editable and auto-populate with default values. 

- **Default Values:**
  - **SR** - 44100
  - **HOP LENGTH** - 1024
  - **WINDOW SIZE** - 512
  - **N_FFT** - 2048

### Other Buttons:

- **Add New Model** - This button will automatically open the models folder. 
  - **Note:** If you are adding a new model, make sure to add it accordingly based on the AI engine it was trained on.
    - **Example:** If you wish to add a model trained on the v4 engine, add it to the correct folder located in the 'models/v4/' directory.
  - **Note:** The application will automatically detect any models added the correct directories without needing a restart.
- **Restart Button** - If the application hangs for any reason, you can hit the circular arrow button immediately to the right of the *'Start Conversion'* button.

## Models Included

**PLEASE NOTE:** Do not change the name of the models provided! The required parameters are specified and appended to the end of the filenames.

Here's a list of the models included within the package -

- **v2 AI Engine**
    - **Main Models**
        - *(list pending)*
    - **Stacked Models**
        - *(list pending)*
        
- **v4 AI Engine**
    - **Main Models**
        - *(list pending)*
    - **Stacked Models**
        - *(list pending)*

A special thank you to aufr33 for helping me expand the dataset used to train these models and for the helpful training tips.

## Other GUI Notes

- The application will automatically remember your *'save to'* path upon closing and reopening until it's changed.
  - **Note:** The last directory accessed within the application will also be remembered.
- Multiple conversions are supported.
- The ability to drag & drop audio files to convert has also been added.
- Conversion times will greatly depend on your hardware. 
  - **Note:** This application will *not* be friendly to older or budget hardware. Please proceed with caution! Pay attention to your PC and make sure it doesn't overheat. ***We are not responsible for any hardware damage.***

## Troubleshooting

If the *'VocalRemover.py'* file won't open *under any circumstances* and all other resources have been exhausted, please do the following - 

1. Open the cmd prompt from the UVR-V4GUI directory
2. Run the following command - 
```
python VocalRemover.py
```
3. Copy and paste the error output in the cmd prompt to the issues center on the GitHub repository.

## License

The **Ultimate Vocal Remover GUI** code is [MIT-licensed](LICENSE). 

## Contributing

- For anyone interested in the ongoing development of **Ultimate Vocal Remover GUI** please send us a pull request and we will review it. This project is 100% open-source and free for anyone to use and/or modify as they wish. 
- Please note that we do not maintain or directly support any of tsurumesos AI application code. We only maintain the development and support for the **Ultimate Vocal Remover GUI**. 

## References
- [1] Takahashi et al., "Multi-scale Multi-band DenseNets for Audio Source Separation", https://arxiv.org/pdf/1706.09588.pdf
