<h1>Dog Breed Classifier Project</h1>

**Table of Contents**
- [Project Overview](#project-overview)
- [Project Instructions](#project-instructions)
- [Project Approaches](#project-approaches)
	- [Model 1: Build CNN Model from Scratch](#model-1-build-cnn-model-from-scratch)
	- [Model 2: Transfer Learning with VGG-16](#model-2-transfer-learning-with-vgg-16)
	- [Model 3: InceptionV3](#model-3-inceptionv3)
- [Results](#results)
- [Publication](#publication)

# Project Overview
This project uses Convolutional Neural Networks (CNNs)! In this project, we will to build a pipeline to process real-world, user-supplied images. Given an image of a dog, the algorithm will identify an estimate of the canine’s breed. If supplied an image of a human, the code will identify the resembling dog breed.

Sample dog output            |  Sample human output   
:-------------------------:|:-------------------------:
![sample_dog_output](images/sample_dog_output.png)|  ![sample_human_output](images/sample_human_output.png)

# Project Instructions

1. Clone the repository and navigate to the downloaded folder.
```	
git clone https://github.com/udacity/dog-project.git
cd dog-project
```

2. Download the [dog dataset](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip).  Unzip the folder and place it in the repo, at location `path/to/dog-project/dogImages`. 

3. Download the [human dataset](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/lfw.zip).  Unzip the folder and place it in the repo, at location `path/to/dog-project/lfw`.  If you are using a Windows machine, you are encouraged to use [7zip](http://www.7-zip.org/) to extract the folder. 

4. Donwload the [VGG-16 bottleneck features](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/DogVGG16Data.npz) for the dog dataset.  Place it in the repo, at location `path/to/dog-project/bottleneck_features`.

5. (Optional) __If you plan to install TensorFlow with GPU support on your local machine__, follow [the guide](https://www.tensorflow.org/install/) to install the necessary NVIDIA software on your system.  If you are using an EC2 GPU instance, you can skip this step.

6. (Optional) **If you are running the project on your local machine (and not using AWS)**, create (and activate) a new environment.

	- __Linux__ (to install with __GPU support__, change `requirements/dog-linux.yml` to `requirements/dog-linux-gpu.yml`): 
	```
	conda env create -f requirements/dog-linux.yml
	source activate dog-project
	```  
	- __Mac__ (to install with __GPU support__, change `requirements/dog-mac.yml` to `requirements/dog-mac-gpu.yml`): 
	```
	conda env create -f requirements/dog-mac.yml
	source activate dog-project
	```  
	**NOTE:** Some Mac users may need to install a different version of OpenCV
	```
	conda install --channel https://conda.anaconda.org/menpo opencv3
	```
	- __Windows__ (to install with __GPU support__, change `requirements/dog-windows.yml` to `requirements/dog-windows-gpu.yml`):  
	```
	conda env create -f requirements/dog-windows.yml
	activate dog-project
	```

7. (Optional) **If you are running the project on your local machine (and not using AWS)** and Step 6 throws errors, try this __alternative__ step to create your environment.

	- __Linux__ or __Mac__ (to install with __GPU support__, change `requirements/requirements.txt` to `requirements/requirements-gpu.txt`): 
	```
	conda create --name dog-project python=3.5
	source activate dog-project
	pip install -r requirements/requirements.txt
	```
	**NOTE:** Some Mac users may need to install a different version of OpenCV
	```
	conda install --channel https://conda.anaconda.org/menpo opencv3
	```
	- __Windows__ (to install with __GPU support__, change `requirements/requirements.txt` to `requirements/requirements-gpu.txt`):  
	```
	conda create --name dog-project python=3.5
	activate dog-project
	pip install -r requirements/requirements.txt
	```
	
8. (Optional) **If you are using AWS**, install Tensorflow.
```
sudo python3 -m pip install -r requirements/requirements-gpu.txt
```
	
9. Switch [Keras backend](https://keras.io/backend/) to TensorFlow.
	- __Linux__ or __Mac__: 
		```
		KERAS_BACKEND=tensorflow python -c "from keras import backend"
		```
	- __Windows__: 
		```
		set KERAS_BACKEND=tensorflow
		python -c "from keras import backend"
		```

10. (Optional) **If you are running the project on your local machine (and not using AWS)**, create an [IPython kernel](http://ipython.readthedocs.io/en/stable/install/kernel_install.html) for the `dog-project` environment. 
```
python -m ipykernel install --user --name dog-project --display-name "dog-project"
```

11. Open the notebook.
```
jupyter notebook dog_app.ipynb
```

12. (Optional) **If you are running the project on your local machine (and not using AWS)**, before running code, change the kernel to match the dog-project environment by using the drop-down menu (**Kernel > Change kernel > dog-project**). Then, follow the instructions in the notebook.

__NOTE:__ While some code has already been implemented to get you started, you will need to implement additional functionality to successfully answer all of the questions included in the notebook. __Unless requested, do not modify code that has already been included.__

# Project Approaches
In this project, we test and evaluate 3 CNN models to choose the best one before deploying in production. 

### Model 1: Build CNN Model from Scratch
For this model, we completely use our collected data from 133 dog breeds to train and predict.
![first_model](images/localCNN_architecture.png)

### Model 2: Transfer Learning with VGG-16
To leverage the power of transfer learning, we use a pre-trained VGG-16 model and add more layers to make it map with our prediction purpose. Adding layers are as below:
![second_model](images/VGG16_architecture.png)

### Model 3: InceptionV3
Finally, we try with another pre-trained model to check if the performance can be improved.
![third_model](images/inceptionv3_architecture.png)
# Results

We use accuracy metric to evaluate model performance. To calculate metrics, I will use the model to predict the dog breed of all images in the **test set**, and then find the percentage of images the model correctly predicted. Because this is a multi-class problem with up to 133 classes, accuracy metric is a good choice.

| Metrics               | Test Accuracy  | 
|---------------------- |-----------------| 
| CNN model from scratch| 3.9474 %         |       
| VGG-16                | 70.0957%        | 
| InceptionV3           | 78.3493%        | 

# Publication
A blog post for this project is published [here](https://medium.com/@lminhkhoa/can-a-machine-learn-how-to-classify-dog-breeds-2f5f3b1e19b3).
