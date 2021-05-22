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
