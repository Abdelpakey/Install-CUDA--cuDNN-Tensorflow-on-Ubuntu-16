# Install-CUDA--cuDNN-Tensorflow-on-Ubuntu-16 (https://www.youtube.com/watch?v=vxjbL5iN1XY)
Requirements

Install Anaconda 
https://www.anaconda.com/download/

If you got a blank (black/white) spyder window after installation then do:

  source activate (yourenv)
  conda install -c anaconda pyopengl  (https://anaconda.org/anaconda/pyopengl)
  
An NVIDIA GPU with a compute capability of 3.0 or higher.
I'll be using a TITAN XP GPU
Ubuntu comes with python 2.7 already installed but I will be using anaconda
Overview

    Step 1: Update your GPU driver (should be higher than version 390)
    Step 2: Install the CUDA Toolkit version 9.0 (with all the patches)
    Step 3: Install CUDNN 7.0.5
    Step 4: Install Tensorflow GPU with pip
    Step 5: Test it!
    
# Step 1: Update your GPU driver
Open a terminal and run the following 3 commands

    sudo add-apt-repository ppa:graphics-drivers/ppa
    sudo apt update
    sudo apt install nvidia-390
Reboot your compute to verify the installation, open a terminal and run the following command

    nvidia-smi
The output should show the GPU name and the driver

# Step 2: Install the CUDA Toolkit (9.0)

go to https://developer.nvidia.com/cuda-90-download-archive 

download the toolkit for linux, x86_64, ubuntu, 16.04, deb l

once the download is complete, open a terminal in the directory the base installer is and run the follow commands

    sudo dpkg -i cuda-repo-ubuntu1704-9-0-local_9.0.176-1_amd64.deb
    sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub
    sudo apt-get update
    sudo apt-get install cuda
    download patch 1 and install (you should get a prompt to install once its done downloading)
    download patch 2 and install (you should get a prompt to install once its done downloading)
    open your .bashrc file with nano
    sudo nano ~/.bashrc

go to the last line and add the following lines (this will set your PATH variable)

    export PATH=/usr/local/cuda-9.0/bin${PATH:+:$PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

# Step 3: Install CUDNN 7.0.5

    go to https://developer.nvidia.com/cudnn
    Select CUDNN 7.0.5 for CUDA 9.0
    download the cuDNN v7.0.5 Library for Linux (tar file)
    open a terminal in the directory the tar file is located
    unzip the tar file using the command
    tar -xzvf cudnn-9.0-linux-x64-v7.tgz
    run the following commands to move the appropriate files to the CUDA folder
    sudo cp cuda/include/cudnn.h /usr/local/cuda/include
    sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
    sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*

# Step 4: pip install tensorflow-gpu

  I will be using a conda environment for installing tensorflow

    create a conda environment by using the following command
    conda create -n tf python=3.6 pip
    activate your environment using
    source activate tf
  run the following command to install tensorflow

    pip install tensorflow-gpu==15
  Step 5: Test it!
  start a python interpreter in the terminal by typing
    python
    run the following lines
    >>> import tensorflow as tf
    >>> hello = tf.constant('hello tensorflow')
    >>> with tf.Session() as sesh:
    >>>     sesh.run(hello)
    the output should be
    >>> 'hello tensorflow'
