# PlasTrans: Identify the conjugative and mobilizable plasmid fragments in plasmidome using sequence signatures 

* [Introduction](#introduction)
* [Version](#version)
* [Requirements](#requirements)
* [Installation](#installation)
* [Usage](#usage)
* [Output](#output)
* [Citation](#citation)
* [Contact](#contact)
    

## Introduction

PlasTrans is designed to distinguish the transmissible plasmid-derived sequences from the non-transmissible plasmid-derived sequences in the plasmid metageomic data. It take a "fasta" file that contains the plasmid sequences as input and outputs a tabular file with transferability annotation for each sequence. 

## Version
+ PlasTrans 1.0 (Tested on Ubuntu 16.04)

## Requirements
------------

+ [Python 2.7.12](https://www.python.org/)
+ [numpy 1.13.1](http://www.numpy.org/)
+ [h5py 2.6.0](http://www.h5py.org/)
+ [TensorFlow 1.4.1](https://www.tensorflow.org/)
+ [Keras 2.0.8](https://keras.io/)
+ [MATLAB Component Runtime (MCR) R2018a](https://www.mathworks.com/products/compiler/matlab-runtime.html) or [MATLAB R2018a](https://www.mathworks.com/products/matlab.html)

  **Note:**
(1) PlasTrans should be run under Linux operating system.
(2) For compatibility, we recommend installing the tools with the similar version as described above.
(3) If GPU is available in your machine, we recommend installing a GPU version of the TensorFlow to speed up the program.
(4) PlasTrans can be run with either an executable file or a MATLAB script. If you run PlasTrans through the executable file, you need to install the MCR (for free) while MATLAB is not necessary. If you run PlasTrans through the MATLAB script, MATLAB is required.



## Installation
### 1 Prerequisites
  
  First, please install **numpy, h5py, TensorFlow** and **Keras** according to their manuals. All of these are python packages, which can be installed with ``pip``. If “pip” is not already installed in your machine, use the command “sudo apt-get install python-pip python-dev” to install “pip”. Here are example commands of installing the above python packages using “pip”.
    
    pip install numpy
    pip install h5py
    pip install tensorflow==1.4.1  #CPU version
    pip install tensorflow-gpu==1.4.1  #GPU version
    pip install keras==2.0.8
    
  If you are going to install a GPU version of the TensorFlow, specified NVIDIA software should be installed. See https://www.tensorflow.org/install/install_linux to know whether your machine can install TensorFlow with GPU support.  
  
  When running PlasTrans through the executable file, MCR should be installed. See https://www.mathworks.com/help/compiler/install-the-matlab-runtime.html to install MCR. On the target computer, please append the following to your LD_LIBRARY_PATH environment variable according to the tips of MCR:
  
    <MCR_installation_folder>/v94/runtime/glnxa64
    <MCR_installation_folder>/v94/bin/glnxa64
    <MCR_installation_folder>/v94/sys/os/glnxa64
    <MCR_installation_folder>/v94/extern/bin/glnxa64
    
  When running PlasTrans through the MATLAB script, please see https://www.mathworks.com/support/ to install the MATLAB.  
  
  **Note:**
  If you find it difficult to install these packages, you may download the Virtual Machine from http://cqb.pku.edu.cn/ZhuLab/PPR_Meta/VM_Bioinfo.vdi.7z, in which we have installed all dependent software. In this way, you only need to copy the PlasTrans folder to the Virture Machine. The manual of PPR-Meta (our previous work) contains a step by step guide about how to install the Virtual Machine (link: http://cqb.pku.edu.cn/ZhuLab/PPR_Meta/Manual.pdf). You can also refer to a brief video guide http://cqb.pku.edu.cn/ZhuLab/PPR_Meta/Video_Guide.mp4 for the Virtual Machine installation.
  
### 2 Install PlasTrans using git
  
  Clone PlasTrans package
  
    git clone https://github.com/zhenchengfang/PlasTrans.git
    
  Change directory to PlasTrans:
  
    cd PlasTrans
    
  The executable file and all scripts are under the folder

## Usage

### 1. Run PlasTrans using executable file (in command line)

  Please simply execute the command:
  
    ./PlasTrans <input_file_folder>/input_file.fna <output_file_folder>/output_file.csv
    
  The input file must be in fasta format containing the sequences to be identified. For example, users can use the file "example.fna" in the folder to test PPR-Meta by simply executing the command:
  
    ./PlasTrans example.fna result.csv
    
### 2. Run PlasTrans using MATLAB script (in MATLAB GUI)

  Please execute the following command directly in MATLAB command window:
  
    PlasTrans('<input_file_folder>/input_file.fna','<output_file_folder>/output_file.csv')
    
  For example, if you want to identify the sequences in "example.fna", please execute:
  
    PlasTrans('example.fna','result.csv')
    
  Please remember to set the working path of MATLAB to PlasTrans folder before running the programe.
  
### 3. Run PlasTrans with specified threshold (-t option)

  Given a specified threshold t (0<t<0.5), a sequence with a score falling into the interval of |score-0.5|<t will be labelled as uncertain, and the remaining predictions will be more reliable. For example, if you want to get reliable predictions in the file "example.fna", you can take 0.2 as the threshold. Please run PPR_Meta using -t option:
  
    ./PlasTrans example.fna result.csv -t 0.2 (by executable file)
    or
    PlasTrans('example.fna','result.csv','-t','0.2') (by MATLAB script)

### 4. Run PlasTrans over a large file (-b option)

  If the RAM of your machine is small, or your file is very large, you can you -b option to let the program read the file in block to reduce the memory requirements and speed up the program. For example, if you want to let the program to predict 1000 sequences at a time, please execute:
  
    ./PlasTrans example.fna result.csv -b 1000 (by executable file)
    or
    PlasTrans('example.fna','result.csv','-b','1000') (by MATLAB script)
    
The default value of -b is 10000.

  
## Output

The output of PPR-Meta consists of six columns:

Header | Length | Score |Transmissibility |
------ | ------ | ----- | --------------- |


**Note:**
(1) The current version of PPR-Meta uses “comma-separated values (CSV)” as the format of the output file. Please use “.csv” as the extension of the output file. PPR-Meta will automatically add the “.csv” extension to the file name if the output file does not take “.csv” as its extension”.
(2) The program allows run mutiple tasks in parallel. However, running mutiple same tasks (with the same input file under the same '-t' and '-b' setting will throw error. 


# Citation
+ Identify the conjugative and mobilizable plasmid fragments in plasmidome using sequence signatures 


# Contact
Any question, please do not hesitate to contact me: fangzc@pku.edu.cn
