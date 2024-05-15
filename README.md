# Deep Learning with TensorFlow
Convolutional neural network (CNN) that predicts a dog's facial emotion.

### Project Overview Motivation
The motivation of this project is to explore the application of Convolutional Neural Network (CNN) modeling with Keras and TensorFlow using a single NVIDIA GPU. After the passing of my wife's American Bulldog, Perogi, my wife inspired me to leverage this project to classify images of of Perogi's life with particular interest in efficiently sorting out his happiest moments.

### Image Dataset
The project intended to begin with the simple but manually intensive approach of building a personally design Tensorflow CNN model trained on 100 manually labeled images of Perogi. However, I came across a labeled "Dog Emotions Prediction" dataset on Kaggle (https://www.kaggle.com/datasets/devzohaib/dog-emotions-prediction), which came with images stored within four labeled sub-directories "angry", "happy", "relaxed", and "sad".

### Data Set Exploration and Preparation
On initial image visualization and data exploration, it became apparent that the "Dog Emotions Prediction" images were inconsistently labeled, likely due to varied and biased opinions of what a "happy", "angry", "relaxed", or "sad" dog looks like. There were well over 2,000 images of animals other than dogs, such as cartoons, lions, cats, monkeys, cows, horses, rabbits, etc. Consequently, I elected to manually re-label images based on consistent and objective emotional features, with an additional fifth class - frown. For ease of coding to associate directory label titles with one-hot encoding, I adjusted the label names to have exactly five characters each, for a final dataset total of 9,325 images:

- alert - the appearance of vigilance and attention toward something (wide eyes, stiff ears, rigid body)
- angry - the appearance of growling, with an aggressive display of teeth
- frown - the appearance of dejection, pain, or abuse
- happy - the display of the tongue, with a near human-like appearance of a smile
- relax - lying down or having the appearance of resting or doing nothing in particular

6,575 images were removed for three reasons:
- images other than a real dog
- the dog's face was not visible
- it did not reasonably fall within one of the five classes.

This effort was an extremely slow and time-consuming process done, however, it underlined the criticality of data quality and maintenance to design a useful classification model.

The dataset was split into 
 training and 
 validation, and randomly shuffled to maximize each dataset combination of classes. The images are instantiated at an RGB three-dimensional size (128x128x3).

### Model Development
I applied transfer learning and model fine-tuning to maximize my compute resources for optimal model performance. To establish a model performance standard and to validate my model development approach, I built and tested a few basic CNN models. The best non-transfer learning and non-fine-tuned CNN model my machine could handle achieved a maximum validation accuracy of ~40% with up to five hidden convolutional hidden layers, before exhausting local machine memory.

For the transfer learning CNN model, I selected the EfficientNetV2S model for its heuristic development as a small model (
 times smaller than other models trained on the ImageNet dataset) with improved training speed and parameter efficiency (EfficientNetV2: Smaller Models and Faster Training paper). I iterate over various combinations of fully connected dense layers added on top of EfficientNetV2S, while constraining the model training with categorical cross-entropy learning rate reduction and early stopping callback features.

Fine-tuning development was centered around finding the optimal EfficientNetV2S layer to unfreeze after the best transfer learning performance was achieved.

### Model Evaluation
A combination of metric plotting (training and validation accuracy, categorical cross-entropy, and F1 Score), confusion matrix visualization (for class F1 Scoring), as well as a metrics record table were used to evaluate model testing and performance.

### Practical Evaluation
The real test, after a satisfactory model evaluation, was to observe how the model classified images of Perogi, and in particular the introduction image.

### Project Flow and Plan
1. Problem Statement and Objectives
2. Modeling Metrics
3. Load Required Modules
4. Set-Up the Python Environment
5. Load and Preview the Data
6. CNN Transfer Learning Model Design
	- CNN Model Parameters
	- CNN Callback Features
	- CNN Transfer Learning Model set-up
	- Train the CNN Transfer Learning Model
	- CNN Transfer Learning Model Performance Analysis
7. CNN Fine-Tuning Model Design
	- CNN Fine-Tuning Model Set-Up
	- Train and Fine-Tune the CNN Transfer Model
	- Fine-tuned CNN transfer learning model performance analysis
	- Display Predicted Emotions From Validation Set
8. Final CNN Model Confusion Matrix
9. Final CNN Model Evaluation on Unseen Images of Perogi
10. Project Summary and Metrics History Review

-------------------------------------------------------------------------------
For Tensorflow with GPU, run this notebook via WSL:
PS C:\Users\dougr> wsl
(base) drandrade@Doug-PC:/mnt/c/Users/dougr$ jupyter-notebook
-------------------------------------------------------------------------------
## Steps for committing Jupyter Notebook .ipynb files to the GitHub repository:
### Initial Set-up:
1. Create a repo on GitHub
2. Install Git (if not already done) - https://git-scm.com/downloads
3. Clone repo by copying repo link - click on the "<> Code" button and copy the HTTPS URL
4. In Powershell, navigate to the directory you want to clone the repo
	`PS C:\Users\dougr> cd ~\Data_Science_Projects\Python`
6. Clone the directory:
	`PS C:\Users\dougr\Data_Science_Projects\NPS> git clone https://github.com/dougrandrade/NPS_DS_Repo.git`
7. Save your Jupyter Notebook to the directory where the repo is cloned:
	`C:\Users\dougr> cd ~\Data_Science_Projects\Python\Dog_Emotions_CNN_Repo`

Committing and Pushing Changes to the GitHub repo:
1. Open Powershell
2. Navigate to the repo directory: 
	`PS C:\Users\dougr> cd ~\Data_Science_Projects\Python\Dog_Emotions_CNN_Repo`
3. Add changes to the staging area:
	`PS C:\Users\dougr\Data_Science_Projects\Python\Dog_Emotions_CNN_Repo> git add .`
4. Commit changes:
	`PS C:\Users\dougr\Data_Science_ProjectsPython\Dog_Emotions_CNN_Repo> git commit -m "Add Jupyter Notebook"`
5. Push the changes to the repo on GitHub:
	`PS C:\Users\dougr\Data_Science_Projects\Python\Dog_Emotions_CNN_Repo> git push`
