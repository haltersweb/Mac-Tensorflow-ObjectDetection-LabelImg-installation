# Install TensorFlow 2, Object Detection, and LabelImg on PC

I initially created this GitHub repository to document how I set up my environment my Mac.  But my daughter has a PC and wanted to play with TensorFlow as well.  This is how I set up my daughter's PC to do ML object detection.

I am following [Nicholas Renotte's Tensorflow Object Detection YouTube tutorial](https://youtu.be/dZh_ps8gKgs) for much of these instructions.

* My daughter has a 64-bit Windows 10 machine.
* I will be using Python Virtual Environments.
* I am using two package managers for this: [PIP](https://pypi.org/project/pip/) and [Homebrew](https://brew.sh/).
* I am not using Conda.

### Assumptions

* You are familiar with shell applications such as Command Prompt or Git CMD (what I'm using). (__NOTE:__ If using Git Bash some of the commands will differ and line up more with Mac/Linux commands)
* You are familiar with the [Jupyter Notebook IDE](https://jupyter.org/)
* You have the latest versions of [PIP](https://pypi.org/project/pip/) and [Homebrew](https://brew.sh/)

### Dependencies

Follow [Nicholas Renotte's Tensorflow Object Detection YouTube tutorial](https://youtu.be/dZh_ps8gKgs?t=351) for a step-by-step to install these dependencies.

* [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/vs/community)

If you have an NVIDIA GPU, then using CUDA and CUDNN to leverage your NVIDIA GPU when training will speed up your training immensely. Make sure you are using the correct versions of CUDA and CUDNN:

* [CUDA 10.1](https://developer.nvidia.com/cuda-10.1-download-archive-base)
* [CUDNN 7.6.5](https://developer.nvidia.com/rdp/cudnn-archive)

Google's protocol buffers are a language- and platform-neutral method for serializing structured data.  Tensorflow uses this format.  Protoc is the tool to be used with protocol buffers. Learn more on [Google's protocol buffers page](https://developers.google.com/protocol-buffers)

* [Protobuf](https://github.com/protocolbuffers/protobuf/releases)

Remember to follow [Nicholas Renotte's Tensorflow Object Detection YouTube tutorial](https://youtu.be/dZh_ps8gKgs?t=351) for a step-by-step instructions since there are a lot of intricacies in these installations.

## Step 0. Install Python (set up your system for multiple Python versions and virtual environments)

TensorFlow doesn't yet work with Python 3.9.  And it's best practice anyway to have different versions of Python on your machine and then pick one to build a virtual environment from.

Python programmer has an excellent [instruction video](https://youtu.be/28eLP22SMTA) on installing multiple python versions using virtual environments.

1. In a shell, __create__ a directory for various python versions.
```
mkdir python_versions
```

2. Within `python_versions` create a folder to hold the particular python release you will be installing.  She currently has Python 3.9.5 installed in a folder called `3.9.5`.  I will be creating a folder for [Python 3.8.10](https://www.python.org/downloads/release/python-3810/) for use with TensorFlow.
```
cd python_versions
mkdir 3.8.10
```

3. Download the correct Windows Installer file (I'm using the [64-bit installer](https://www.python.org/ftp/python/3.8.10/python-3.8.10-amd64.exe)).  Then launch the installer.
4. Do __NOT__ check the "Add Python 3.8 to PATH" option.  We will not need it when running virtual environments.
5. Choose the __Customize Installation__ option rather than "Install Now".
6. Use the default Optional Features.
7. Add the "Precompile standard library" option to the selected Advanced Options. 
8. Customize your install location by selecting your version directory to install your Python version into. For example: `C:\Users\sally_sue\python_versions\3.8.10`

## Step 1. Set up your Python virtual environment with venv

These instructions assume you now have Python 3.8 installed.  As a reminder, Python programmer has an excellent [instruction video](https://youtu.be/28eLP22SMTA) on installing multiple python versions using virtual environments.

1. In terminal, __create__ a directory to hold your Python virtual environment(s) and then navigate to it.  We'll call ours "python_projects".
```
mkdir python_projects
cd python_projects
```

2. Create a __virtual environment__ (this will also create a new directory).  We'll call it "funEnv".  You will also be sipulating the Python version to use (you can check it with `--version`).  I will be using Python 3.8.10. (as of this writing, TF is not compatible with 3.9)
```
C:\Users\Sally_Sue\python_versions\3.8.10\python -m venv funEnv
```

3. __Activate__ your virtual python environment.  We'll call ours "funEnv"
```
funEnv\Scripts\activate
```
(__NOTE:__ if you are using Git Bash the activation command will match the Mac instructions instead, namely: `source funEnv/Scripts/activate`)

When you see the name of the environment in parentheses at the front of the prompt you know it is active.  For example:
```
(funEnv) [sally_sue]python_projects$
```

4. Navigate to your virtual environment
```
cd funEnv
```

5. IMPORTANT: make sure to __update PIP__ before using it.
```
python -m pip install --upgrade pip
```

FYI: To __deactivate__ your virtual Python environment just type:
```
deactivate
```

### IMPORTANT: Is your venv (Python virtual environment) inactive?

Are you having trouble with pip and python or defaulting to older versions of them? Are you unable to start Jupyter Notebook or run TensorFlow?

That's usually a sign that your venv (Python virtual environment) is inactive.

Even opening a new terminal window will default to a deactivated venv state.  You need to activate venv on each terminal window if you are working in venv.  You will know it's active if the first thing you see in the terminal prompt is the name of the venv directory in parentheses:
```
(funEnv) [sally_sue]python_projects$
```

## Step 2. Install Jupyter Notebook IDE

1. Ensure the virtual environment is active.
3. Navigate to the virtual environment folder.
4. Make sure pip is up to date
5. Install Jupyter Notebook
```
python -m pip install jupyter
```

7. Install Python Kernel.
```
pip install ipykernel
```

6. Add your virtual environment to the Python Kernel and give it a name.  I'll call mine `funEnv_j`
```
python -m ipykernel install --user --name=funEnv_j
```

7. When creating a new python file, choose the Python Kernel you created to ensure you are using the correct Python version that matches your virtual environment.
![image](https://user-images.githubusercontent.com/1916488/119246532-5f904400-bb50-11eb-9595-f0e2703ebba9.png)

### Starting Jupyter Notebook

1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. Type `jupyter notebook` at the terminal prompt.
```
jupyter notebook
```

4. If it doesn't launch automatically, copy the url from your shell and paste it into your browser. This runs an instance of Jupyter Notebook on localhost.
5. Remember to choose the Python Kernel you created for your virtual environment when starting a new Python file.

FYI: To __end the Jupyter session__ use `CTRL-C` and confirm.

## Step 3. Installing Tensorflow Object Detection

1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. Clone https://github.com/tensorflow/models repo
```
git clone https://github.com/tensorflow/models.git
```

4. Navigate to models > research
```
cd models\research
```

5. 


## Step 5. Installing TensorFlow 2 with pip (on virtual environment)

## Step 6. Installing Object Detection API with pip and brew

## Step 7. Installing LabelImg

## Putting it all together
If you are new to TensorFlow, or even machine learning in general take a look at the following resources:

* [3Blue1Brown's "Neural Network" YouTube series](https://youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)
* [ML Hello World with TensorFlow](https://developers.google.com/codelabs/tensorflow-1-helloworld#0)
* [Beyond Hello World](https://colab.research.google.com/github/lmoroney/mlday-tokyo/blob/master/Lab2-Computer-Vision.ipynb)
* ML Zero to Hero with TensorFlow: [Part 1](https://youtu.be/KNAWp2S3w94), [Part 2](https://youtu.be/bemDFpNooA8), [Part 3](https://youtu.be/x_VrgWTKkiM), [Part 4](https://youtu.be/u2TjZzNuly8)

If you are ready to delve into object detection with TensorFlow, check out [Nicholas Renotte's YouTube channel](https://www.youtube.com/channel/UCHXa4OpASJEwrHrLeIzw7Yg) for excellent tutorials.

Here are some of my favorites from his channel:
* [Real Time Facemask Detection with TensorFlow](https://youtu.be/IOI0o3Cxv9Q)
* [Real Time Sign Language Detection with Tensorflow](https://youtu.be/pDXdlXlaCco)
* [Tensorflow Object Detection in 5 Hours with Python](https://youtu.be/yqkISICHH-U)
