# Install TensorFlow 2, Object Detection, and LabelImg on PC

I initially created this GitHub repository to document how I set up my environment my Mac.  But my daughter has a PC and wanted to play with TensorFlow as well.  This is how I set up my daughter's PC to do ML object detection.

I am following [Nicholas Renotte's Tensorflow Object Detection YouTube tutorial](https://youtu.be/dZh_ps8gKgs) for much of these instructions.

* My daughter has a 64-bit Windows 10 machine.
* I will be using Python Virtual Environments.
* I am using [Git](https://git-scm.com/downloads) version controller
* I am using two package managers for this: [PIP](https://pypi.org/project/pip/) and [Homebrew](https://brew.sh/).
* I am not using Conda.

### Assumptions

* You are familiar with shell applications such as Command Prompt or Git CMD (what I'm using). (__NOTE:__ If using Git Bash some of the commands will differ and line up more with Mac/Linux commands)
* You are familiar with the [Jupyter Notebook IDE](https://jupyter.org/)
* You have the latest versions of [PIP](https://pypi.org/project/pip/) and [Homebrew](https://brew.sh/)

### Dependencies

__Follow [Nicholas Renotte's Tensorflow Object Detection YouTube tutorial](https://youtu.be/dZh_ps8gKgs?t=351)__ for a step-by-step to install these dependencies.

#### MS Visual C++ Build Tools

* [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/vs/community)

#### Leverage your GPU with CUDA and CUDNN

Source: [CUDA Installation Guide for Microsoft Windows](https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html)

If you have an NVIDIA GPU, then you might be able to use CUDA and CUDNN to leverage your GPU when training.  This will speed up your training immensely.

1. First check your Windows Device Manager against the [CUDA list of CUDA-capable GPUs](https://developer.nvidia.com/cuda-gpus).  (Open your device manager via command line with `devmgmt.msc`.)
2. Choose the right CUDA and CUDNN to use based on TensorFlow version at https://www.tensorflow.org/install/source_windows#gpu.

For example, if you are using TensorFlow 2.3.0 you would use:

* [CUDA 10.1](https://developer.nvidia.com/cuda-10.1-download-archive-base)
* [CUDNN 7.6.5](https://developer.nvidia.com/rdp/cudnn-archive)

#### Protocol buffers

Google's protocol buffers are a language- and platform-neutral method for serializing structured data.  Tensorflow uses this format.  Protoc is the tool to be used with protocol buffers. Learn more on [Google's protocol buffers page](https://developers.google.com/protocol-buffers)

* [Protobuf](https://github.com/protocolbuffers/protobuf/releases)

Remember to follow [Nicholas Renotte's Tensorflow Object Detection YouTube tutorial](https://youtu.be/dZh_ps8gKgs?t=351) for __step-by-step instructions of these dependencies__ since there are a lot of intricacies in these installations.

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
5. Install [Jupyter Notebook](https://jupyter.org/install.html#installation-with-pip-1)
```
python -m pip install notebook
```

### Starting Jupyter Notebook

Type `jupyter notebook` at the command line prompt.
```
jupyter notebook
```

If it doesn't launch automatically, copy the url from your shell and paste it into your browser. This runs an instance of Jupyter Notebook on localhost.

FYI: To __end the Jupyter session__ click the "Quit" button at the top right of the IDE interface.

## Step 3. Installing TensorFlow 2 with pip (on virtual environment)

For reference: https://www.tensorflow.org/install

1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. IMPORTANT: make sure to __update PIP__ before using it.
```
python -m pip install --upgrade pip
```

4. Make sure all dependencies are installed (see the section on dependencies at the top of this document)

### Enable Win32 long paths

Different Windows OS have different methods.  For Windows 10 I did this through the Regedit settings [using the Windows Club directions](https://www.thewindowsclub.com/how-to-enable-or-disable-win32-long-paths-in-windows-11-10)

1. Type `RegEdit` in the start menu
2. Paste `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem` into the address bar and click "Enter".
<img width="572" alt="image" src="https://user-images.githubusercontent.com/1916488/126911645-6130cb8f-1d79-49dc-b6a9-8cd71d46f30f.png">

4. Double click on `LongPathsEnabled` in the FileSystem folder.
<img width="505" alt="image" src="https://user-images.githubusercontent.com/1916488/126911660-d8741836-5b35-4b86-95ae-576ad3ad245e.png">

5. Change Value Data to `1` (default is 0) and click "OK"

### Install TensorFlow 2
```
python -m pip install --upgrade tensorflow
```

### Confirm the install was successful
```
python -c "import tensorflow as tf;print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

something like this should be returned: `tf.Tensor(-1402.6809, shape=(), dtype=float32)`

### install necessary packages

View the current list of packages installed within the virtual environment:
```
pip list
```
Use pip to install any of the packages below that weren't listed 
* numpy
* keras
* opencv-contrib-python
* scikit-image
* pillow
* imutils
* scikit-learn
* matplotlib
* progressbar2
* beautifulsoup4
* pandas
```
python -m pip install <package name>
```

## Step 4. Installing Tensorflow Object Detection

Refer to the [Object Detection API with TensorFlow 2 installation instructions](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2.md)

1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. Clone the [Tensorflow Model Garden](https://github.com/tensorflow/models).  This installs a models directory in the virtual environment root directory.
```
git clone https://github.com/tensorflow/models.git
```

4. Navigate to models > research
```
cd models\research
```

5. Compile protos using protoc
```
protoc object_detection/protos/*.proto --python_out=.
```
6. Copy setup file from object detection packages into current directory
```
copy object_detection\packages\tf2\setup.py .
```
7. Install all dependencies needed for our object detection library (ignore warnings)
```
python -m pip install --use-feature=2020-resolver .
```

8. Confirm installation was successful (ignore CUDA and GPU warnings if you are not leveraging your GPU)
```
python object_detection/builders/model_builder_tf2_test.py
```

It should result in something like:
```
Ran 21 tests in 27.946s
OK (skipped=1)
```

If, instead you get a `ModuleNotFoundError`, install the module using `pip install` (see last part of Step 3)

## Step 5. Installing LabelImg

Use LabelImg __to prepare images__ you want to use for training data.  Watch [Nicholas Renotte's "Real Time Face Mask Detection" video](https://youtu.be/IOI0o3Cxv9Q) to see how he uses LabelImg to prep his training data.

I installed LabelImg from [tzutalin's version of LabelImg on GitHub](https://github.com/tzutalin/labelImg) since [Douglas Meneghetti](https://douglasrizzo.com.br/tf-obj-tutorial/) mentioned it's better than the version you can install with pip.

I am following the Mac instructions from [tzutalin's LabelImg GitHub page](https://github.com/tzutalin/labelImg#windows) for "Windows"

### download LabelImg from GitHub

1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. Clone Tzutalin's LabelImg version
```
git clone https://github.com/tzutalin/labelImg.git
```

### upgrade pip (if you haven't already)
```
python -m pip install --upgrade pip
```

### install dependencies

1. Navigate to the LabelImg directory
```
cd labelImg
```

2. Install [PyQt5](https://www.riverbankcomputing.com/software/pyqt/download5)
```
pip install PyQt5
```

3. Install [lxml](https://lxml.de/installation.html)
```
pip install lxml
```

### build the labelImg application
```
pyrcc5 -o libs/resources.py resources.qrc
```

### run labelImg
```
python labelImg.py
```

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
