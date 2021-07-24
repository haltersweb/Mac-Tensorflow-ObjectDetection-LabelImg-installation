# Install TensorFlow 2, Object Detection, and LabelImg on Mac OS

This is how I set up my Mac to do ML object detection.

There are certain steps that are different between PC and Mac.  When I tried to follow instructions by folks who were using PCs for setting up TensorFlow 2 (TF2), Object Detection, etc. I would end up with errors.

I hope this will help those of you who who are on Mac OS and are struggling to set up your learning environment.

* I am using a 2017 Macbook Pro with Big Sur OS.
* I have [Python](https://www.python.org/) 3.8.10 installed (at time of writing).
* I am using two package managers for this: [PIP](https://pypi.org/project/pip/) and [Homebrew](https://brew.sh/).
* I am not using Conda.

## Assumptions

* You are familiar with Terminal
* You already have [Python 3.8](https://www.python.org/) installed (as of this writing, TF is not compatible with 3.9)
* You will be using a Python Virtual Environment
* You are familiar with the [Jupyter Notebook IDE](https://jupyter.org/)
* You have the latest versions of [PIP](https://pypi.org/project/pip/) and [Homebrew](https://brew.sh/)
* You have the latest version of [Xcode](https://apps.apple.com/us/app/xcode/id497799835?mt=12)

Coursera has an excellent [instruction video](https://www.coursera.org/lecture/python-project/how-to-install-jupyter-on-a-mac-optional-RCR8s) by the University of Michigan on installing Homebrew, Python3, spinning up a Python Virtual Environment, and installing Jupyter Notebook.

## Step 0. Setting up different Python versions with pyenv (in case you don't have python installed yet)

__pyenv__ is used to install different major and minor releases of Python.

(Instructions: https://youtu.be/-5vd5GEpF-w)
(GitHub for pyenv: https://github.com/pyenv/pyenv)

### Install pyenv with Homebrew:

1. Update Homebrew.  Brew update usually takes a while.  Go get some coffee while you wait.
```
brew update
```

2. Install pyenv
```
brew install pyenv
```

### Configure terminal so that it always loads pyenv whenever we start a new terminal instance

1. Find out what file changes you need to make for your particular MacOS by typing:
```
pyenv init
```
2. Make any stipulated changes using command-line text editor such as Vim or Nano

For example, I am on BigSur OS.  `pyenv init` instructed me to add 3 lines to `.profile` and to `.zprofile` and then to append `eval "$(pyenv init -)"` into `zshrc` (the zsh config file). Earlier OS may use bin instead of zsh.

(BTW, later if you don't want pyenv to manage its Python versions, comment out the eval line in the .zshrc file. That way python --version = 2.7 (system version) and python3 = whatever version you may have installed without pyenv)

### Install a python version

1. To see a full list of every Python version you can install by typing:
```
pyenv install --list

```
Besides regular Python versions you can even install anaconda versions and others.

2. Install version(s). For example let's install 3.8.9 and 3.9.4:
```
pyenv install 3.9.4
pyenv install 3.8.9
```

3. View the list of installed versions
```
pyenv versions
```

4. Choose your default version by modifying the `~/.pyenv/version` text file (for example 3.8.9)
```
echo 3.8.9 > ~/.pyenv/version
```

## Step 1. Set up your Python virtual environment with venv

These instructions assume you already have Python 3.8 installed.  (If you don't have Python 3.8 installed here is a video that tells you how to [install particular Python versions using pyenv](https://www.youtube.com/watch?v=-5vd5GEpF-w).)

1. In terminal, __create__ a directory to hold your Python virtual environment(s) and then navigate to it.  We'll call ours "projects".
```
mkdir projects
cd projects
```

2. Create a __virtual environment__ (this will also create a new directory).  We'll call it "funEnv".  You will also be sipulating the Python version to use (you can check it with `--version`).  I will be using Python 3.8.10. (as of this writing, TF is not compatible with 3.9)
```
/your/python/file/path/python -m venv funEnv
```
NOTE: if 3.8.10 is the default version on your system, you could just use the aliases `python` or `python3.8` instead of the python file path

3. __Activate__ your virtual python environment.  We'll call ours "funEnv"
```
source funEnv/bin/activate
```
When you see the name of the environment in parentheses at the front of the prompt you know it is active.  For example:
```
(funEnv) [haltersweb]projects$
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
(funEnv) [haltersweb]projects$
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

4. Clone the [Tensorflow Model Garden](https://github.com/tensorflow/models.git). This installs a models directory in the virtual environment root directory.
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
pipenv run pip install pyqt5==5.12.1 lxml
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
