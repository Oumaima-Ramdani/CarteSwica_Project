# Swica Card Data Extraction

This project aims to automate the process of extracting data from insurance cards, a task known for its tediousness and susceptibility to errors when performed manually. Leveraging a blend of image processing and text recognition methodologies, this script systematically extracts pertinent information from each section of an insurance card, encompassing details such as the insured individual's name, AVS number, expiration date, and more. Subsequently, these extracted data points are meticulously organized and stored within a structured JSON file, facilitating seamless access and utilization for future endeavors.

## Key Features

- Automatic detection and extraction of relevant zones on an insurance card.
- Recognition and extraction of textual information from each zone.
- Generation of a structured JSON file containing the extracted data for each insurance card.


# Which Programming Language to use ?

Python was chosen for its versatility, simplicity, and extensive libraries specialized in image processing and data extraction. Tools like OpenCV and pandas offer advanced features for image processing and data manipulation. Python's clear syntax makes it ideal for this project, where image processing and data extraction are crucial.

# which working environment to choose?

After selecting Python as the programming language, the next step was to choose the right environment for development. This led to the decision to utilize Anaconda, a powerful Python distribution that streamlines package management and provides essential tools for data science projects.

Anaconda includes Jupyter Notebook, an interactive web application for creating and sharing documents containing live code, equations, visualizations, and explanatory text. Using Jupyter Notebook within Anaconda provides a convenient and efficient environment for developing and documenting data science projects.

### Installing Anaconda on Mac:

To do so, feel free to download it from the following link:

[Download Anaconda for Mac](https://repo.anaconda.com/archive/Anaconda3-2022.10-MacOSX-arm64.pkg)

### Installing Anaconda on Windows

To install Anaconda on Windows, follow these simple steps:
1. Download the Anaconda installer from the official Anaconda website.
2. Run the downloaded installer (.exe) file.
3. Follow the on-screen instructions, selecting your installation preferences.
4. Once the installation is complete, you can start using Anaconda by launching the Anaconda Navigator application from the Windows Start menu.

### Installing Anaconda on Linux

To install Anaconda on Linux, follow these straightforward steps:
1. Download the Anaconda installer for Linux from the official Anaconda website.
2. Open a terminal and navigate to the directory where the installer was downloaded.
3. Make the installer executable by running the command: `chmod +x Anaconda3-<version>-Linux-x86_64.sh` (Replace `<version>` with the appropriate version number.) 
4. Run the installer script with the command: `./Anaconda3-<version>-Linux-x86_64.sh`
5. Once the installation is finished, you can start using Anaconda by opening a new terminal or typing `anaconda-navigator` in the terminal.


# How to Use Anaconda ?

To use Anaconda, follow these simple steps:
1. Open it.
2. Run the installer and follow the on-screen instructions.
3. Once the installation is complete, you can start Anaconda Navigator from the start menu of your operating system.
4. In Anaconda Navigator, you can launch Jupyter Notebook to work on your project.

   <img width="1709" alt="Capture d’écran 2024-05-15 à 22 56 30" src="https://github.com/Oumaima-Ramdani/CarteSwica_Project/assets/167336780/e950e476-fd69-48b4-9cbd-bec8eaf0a3ba">


# Image Preprocessing and Data Extraction Workflow 
#  Instructions for the user:
To complete the project, please follow the following instructions:

### 1. Installing Libraries :

```bash
!pip install rembg
!pip install pillow
!pip install pytesseract
!pip install easyocr
```
These commands install the necessary Python libraries for image background removal (rembg), image manipulation (Pillow), text recognition (pytesseract), and optical character recognition (OCR) with ease (easyocr).

### 2. Importing Libraries : 

```bash
import os
from rembg import remove
from PIL import Image
import cv2
import numpy as np
import matplotlib.pyplot as plt
from skimage import io
from skimage.measure import label, regionprops
import pytesseract
from pytesseract import Output
from easyocr import Reader
```
This code imports essential Python libraries for various tasks including image processing, computer vision, data visualization, and text recognition. It includes modules for background removal (rembg), image manipulation (Pillow and OpenCV), data analysis (numpy and skimage), data visualization (matplotlib), and text recognition (pytesseract).

### 3. Download and extract the necessary resources : 
Run the following command to download the necessary files:

```bash
!wget https://pyimagesearch-code-downloads.s3-us-west-2.amazonaws.com/easy-ocr-tutorial/easy-ocr-tutorial.zip
!unzip -qq easy-ocr-tutorial.zip
%cd easy-ocr-tutorial
```
The script will extract the files into a folder named easy-ocr-tutorial.

### 4. Setting Up Input and Output Folders : 

1. Create a folder named "input" on your desktop.
2. Place all the insurance card images you want to process in a folder named "input" inside the easy-ocr-tutorial directory.
3. Replace the `input_folder` path in the script with the path to your input folder.
4. Replace all the `output_folder` path in the all the script with the paths where you want the files to be created. (`output`, `output_final`, `carte_swica` and `Cartes_swica_final`)
5. Run the script in your Python environment.

### 5. Instructions for Using the JSON Configuration File :

The following image illustrates the categorization of distinct zones for the extraction of their respective data:

![2022-07-18-topstory-teaserbild](https://github.com/Oumaima-Ramdani/CarteSwica_Project/assets/167336780/e24fb783-8079-429d-91cb-6202f9eff096)

For that:
- Create a folder named "JsonConfig" on your desktop.
- Place the JSON configuration file named "modeleSwica.json" inside the "JsonConfig" folder. This file contains a text file "text.json" containing the coordinates of each zone :
  
```python
{
    "Document Type": [225, 25, 940, 140],
    "Username": [40, 432, 480, 486],
    "Card Number": [30, 495, 495, 540],
    "Date of Birth & Gender": [35, 560, 291, 605],
    "Customer Service": [710, 255, 1025, 306],
    "Telemedicine Health 24": [710, 298, 1025, 343],
    "Policyholder Number": [650, 338, 1025, 385],
    "Date Expiration": [815, 560, 1035, 610],
    "Useless Zone 1": [285, 215, 755, 385],
    "Useless Zone 2": [100, 140, 550, 195],
    "test_coordinates": [695, 490, 1040, 550],
    "OFSP_number_coordinates": [515, 495, 645, 540]
}
```

- Open the Python script.
- Locate the lines where the folder paths are defined and replace them with the paths to your "Cartes_swica_final" and "JsonConfig" folders.
- Once the paths have been configured, execute the script.

The script will extract information from the insurance cards located in the "Cartes_swica_final" folder using the zones defined in the "modeleSwica.json" file. It will then display and save the results in a JSON file named "extraction_results.json".

- Once the paths have been configured, execute the script.

The script will extract information from the insurance cards located in the "Cartes_swica_final" folder using the zones defined in the "modeleSwica.json" file. It will then display and save the results in a JSON file named "extraction_results.json".
