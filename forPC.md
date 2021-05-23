# Install TensorFlow 2, Object Detection, and LabelImg on PC

I initially created this GitHub repository to document how I set up my environment my Mac.  But my daughter has a PC and wanted to play with TensorFlow as well.  This is how I set up my daughter's PC to do ML object detection.

* My daughter has a Windows 10 machine.
* I will be using Python Virtual Environments.
* I am using two package managers for this: [PIP](https://pypi.org/project/pip/) and [Homebrew](https://brew.sh/).
* I am not using Conda.

## Assumptions

* You are familiar with shell applications such as Command Prompt or Git CMD (what I'm using). (__NOTE:__ If using Git Bash some of the commands will differ and line up more with Mac/Linux commands)
* You are familiar with the [Jupyter Notebook IDE](https://jupyter.org/)
* You have the latest versions of [PIP](https://pypi.org/project/pip/) and [Homebrew](https://brew.sh/)
* You have the latest version of [Xcode](https://apps.apple.com/us/app/xcode/id497799835?mt=12)

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
(__NOTE:__ if you are using Git Bash the command will match the Mac instructions, namely: `source funEnv/Scripts/activate`)

When you see the name of the environment in parentheses at the front of the prompt you know it is active.  For example:
```
(funEnv) [sally_sue]python_projects$
```

4. Navigate to your virtual environment
```
cd funEnv
```

5. IMPORTANT: make sure to __update PIP and Homebrew__ before using them.  Brew update usually takes a while.  Go get some coffee while you wait.
```
pip install --upgrade pip
brew update
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
2. Navigate to the virtual environment folder.
3. You will use `pip install notebook`.  This is the up-to-date Jupyter Notebook.  DO NOT USE `pip install jupyter`.
```
pip install notebook
```

### Starting Jupyter Notebook

1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. Type `jupyter notebook` at the terminal prompt.
```
jupyter notebook
```

4. Copy the url from terminal and paste it into your browser. This runs an instance of Jupyter Notebook on localhost.

FYI: To __end the Jupyter session__ use `CTRL-C` and confirm.

## Step 3. Installing TensorFlow 2 with pip (on virtual environment)

For reference: https://www.tensorflow.org/install/pip and https://www.pyimagesearch.com/2019/12/09/how-to-install-tensorflow-2-0-on-macos/

1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. Update pip
```
pip install --upgrade pip
```

4. Install TensorFlow 2
```
pip install --upgrade tensorflow
```

5. Confirm the install was successful
```
python -c "import tensorflow as tf;print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```
something like this should be returned: `tf.Tensor(-1402.6809, shape=(), dtype=float32)`

### install necessary packages

No need to install __numpy__ and __keras__ since they are installed when installing TF2

1. Make sure the latest __Xcode__ is installed (thru the App Store)
2. Install image processing libraries
```
pip install opencv-contrib-python
pip install scikit-image
pip install pillow
pip install imutils
```

3. Install ML and support libraries
```
pip install scikit-learn
pip install matplotlib
pip install progressbar2
pip install beautifulsoup4
pip install pandas
```

## Step 4. Installing Object Detection API with pip and brew

For reference: https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2.md and https://www.tensorflow.org/hub/build_from_source#install_protoc


1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. Make sure Homebrew is also up to date
```
brew update
```

4. Clone the TF2 models repository. This installs a models directory in the virtual environment root directory.
```
git clone https://github.com/tensorflow/models.git
```

5. Navigate to the models research directory
```
cd models/research
```

6. Install protobuf with Homebrew
```
brew install protobuf
```

7. Compile protos using protoc
```
protoc object_detection/protos/*.proto --python_out=.
```

8. Copy setup file from object detection packages into current directory
```
cp object_detection/packages/tf2/setup.py .
```

9. Install all dependencies neede for our object detection library (ignore warnings)
```
python -m pip install --use-feature=2020-resolver .
```

10. Confirm installation was successful
```
python object_detection/builders/model_builder_tf2_test.py
```
It should result in something like:
```
Ran 21 tests in 27.946s
OK (skipped=1)
```

## Step 5. Installing LabelImg

Use LabelImg __to prepare images__ you want to use for training data.  Watch [Nicholas Renotte's "Real Time Face Mask Detection" video](https://youtu.be/IOI0o3Cxv9Q) to see how he uses LabelImg to prep his training data.

I installed LabelImg from [tzutalin's version of LabelImg on GitHub](https://github.com/tzutalin/labelImg) since [Douglas Meneghetti](https://douglasrizzo.com.br/tf-obj-tutorial/) mentioned it's better than the version you can install with pip.

I am following the Mac instructions from [tzutalin's LabelImg GitHub page](https://github.com/tzutalin/labelImg#user-content-macos) for "Python 3 Virtualenv"

### download LabelImg from GitHub

1. Ensure the virtual environment is active
2. Navigate to the virtual environment folder
3. Clone Tzutalin's LabelImg version
```
git clone https://github.com/tzutalin/labelImg.git
```

### build the application with pipenv

1. Navigate to the LabelImg directory
```
cd labelImg
```

2. Install pipenv for better dependency management
```
pip install pipenv
```

3. Build labelImg
```
pipenv run pip install pyqt5 lxml
pipenv run make qt5py3
```

### run labelImg

1. Start the LabelImg application
```
pipenv run python labelImg.py
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
