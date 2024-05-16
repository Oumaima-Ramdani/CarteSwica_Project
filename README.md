# Swica Card Data Extraction

This project aims to automate the process of extracting data from insurance cards, a task known for its tediousness and susceptibility to errors when performed manually. Leveraging a blend of image processing and text recognition methodologies, this script systematically extracts pertinent information from each section of an insurance card, encompassing details such as the insured individual's name, AVS number, expiration date, and more. Subsequently, these extracted data points are meticulously organized and stored within a structured JSON file, facilitating seamless access and utilization for future endeavors.

## Key Features

- Automatic detection and extraction of relevant zones on an insurance card.
- Recognition and extraction of textual information from each zone.
- Generation of a structured JSON file containing the extracted data for each insurance card.

## Project Background

This project originates from the need to modernize and streamline the insurance claims processing workflow in an emerging insurance company. Faced with a growing volume of claims and limited resources, the company sought
a solution to automate data extraction from insurance claim forms submitted by clients.

By automating this process, the company aims to reduce processing times, minimize data entry errors, and free up time for its employees to focus on higher-value tasks. This project, therefore, aims to address this 
specific need by developing a reliable and efficient data extraction system from insurance claim forms.

# Which Programming Language to use ?

The choice of programming language is crucial for successfully completing this project. Python has been selected due to its versatility, simplicity, and extensive range of libraries specialized in image processing and data extraction.

Python offers a multitude of well-established libraries such as OpenCV for image processing, as well as tools like pandas for data manipulation. Its clear syntax and ease of learning make it an ideal choice for this type of project.

Python is widely used in the field of image processing due to its specialized libraries such as OpenCV, which provide advanced features for image manipulation, object detection, shape recognition, etc.

Additionally, Python is also a popular choice for data extraction because of its ability to efficiently process and analyze large datasets. Libraries like pandas facilitate the manipulation and analysis of structured data, which is essential for extracting information from documents such as insurance cards.

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


# Image Preprocessing and Data Extraction Workflow : 
#  Instructions for the user:
To complete the project, please follow the following instructions:

### 1. Installing Libraries :
```bash
!pip install rembg
!pip install pillow
!pip install pytesseract
!pip install easyocr
```

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

### 3. Download and extract the necessary resources : 
Run the following command to download the necessary files: "!wget https://pyimagesearch-code-downloads.s3-us-west-2.amazonaws.com/easy-ocr-tutorial/easy-ocr-tutorial.zip
!unzip -qq easy-ocr-tutorial.zip
%cd easy-ocr-tutorial" 

The script will extract the files into a folder named easy-ocr-tutorial.

### 4. Setting Up Input and Output Folders : 

1. Create a folder named "input" on your desktop.
2. Place all the insurance card images you want to process in a folder named "input" inside the easy-ocr-tutorial directory.
4. Create a folder named "output" on your desktop.
5. Replace the `input_folder` and `output_folder` paths in the script with the paths to your input and output folders.
6. Run the script in your Python environment.

### 5. Configuring  Output and Input Folder Paths :

1. Create a folder named "output_final" on your desktop.
2. Replace the output folder path (output_folder) in the script with the path to your "output_final" folder.
3. Similarly, replace the input folder path (input_folder) in the script with the path to your "output" folder.
4. Run the script in your Python environment.


### 6. Setting Up Carte Swica Folder : 

1. Create a folder named "carte_swica" on your desktop.
2. Replace the output folder path (`output_folder`) in the script with the path to your "carte_swica" folder.
3. Run the script in your Python environment.
 
### 7. Configuring Carte Swica final Folder Path : 

1. Create a folder named "Cartes_swica_final" on your desktop.
2. Replace the output folder path (output_folder) in the script with the path to your "Cartes_swica_final" folder.
3. Run the script in your Python environment.

### 8. Instructions for Using the JSON Configuration File :

![2022-07-18-topstory-teaserbild](https://github.com/Oumaima-Ramdani/CarteSwica_Project/assets/167336780/f13e4c62-9413-4267-be43-4915e24826a9)


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


