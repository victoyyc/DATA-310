# Project 4
### Victoria Yuanyuan Chang


## 1. Problem Statement
The current project aims at identifying dog breeds from images. The problem I wish to solve is the identification and recording of stray dogs. If one finds a stray dog in need of rescue or adoption, they can take a picture of the dog and the model can identify the breed of dog. Such model, with more refinement, also has the potential to identify lost pets if caught in security cameras. Moreover, dogs are just cute and they deserve the attention of data science people. The complexity of this project lays on the variety of the dog breeds. To fully incorporate all dog breeds the model needs to be able to classify images into hundreds of categories. What’s more, the input images can have various backgrounds that interrupts the identification, and different dog breeds can have very subtle differences in terms of appearance. In conclusion, the central research question is how to build a model that identifies dog breed with an image of the dog.

## 2. Description of Data
The training and testing data is a segment of a dataset from Kaggle (https://www.kaggle.com/c/dog-breed-identification/data). The original data includes one .csv file that maps the images to its breed name and 10222.jpg images of various dogs. The .csv file consists of one column that records image filename and another that records its breed. The images are everyday photos of all kinds of dogs in different backgrounds (some include other objects/animals/humans) rather than staged stock images. These images fits better than stock images the scenario in which the model can be potentially applied. Sample images are shown to the right. The size of the images vary, but they are mostly under 50KB. In consideration of this preliminary model's limited capacity, I segmented the original data by selecting only the 10 most common breeds (out of the 120 breeds it contains). This segment of data contrains 1141 images and 10 categories. 

Sample Images:

![image](https://user-images.githubusercontent.com/57189964/117375171-7cfcb700-ae9c-11eb-94af-4a8e5a4304e1.png)
![image](https://user-images.githubusercontent.com/57189964/117375185-825a0180-ae9c-11eb-8351-69f971567181.png)
![image](https://user-images.githubusercontent.com/57189964/117375271-a0bffd00-ae9c-11eb-93c5-b17eb5b93eb0.png)
![image](https://user-images.githubusercontent.com/57189964/117375259-9c93df80-ae9c-11eb-8049-2549b2ba15a3.png)
![image](https://user-images.githubusercontent.com/57189964/117375373-d95fd680-ae9c-11eb-91f4-590294e8a1d1.png)

Sample .csv file (label names):
|id	|breed|
|---|----|
|000bec180eb18c7604dcecc8fe0dba07|	boston_bull
|001513dfcb2ffafc82cccf4d8bbaba97| dingo
|001cdf01b096e06d78e9e5112d419397|	pekinese
|00214f311d5d2247d5dfe4fe24b2303d|	bluetick
|0021f9ceb3235effd7fcde7f7538ed62|	golden_retriever
|002211c81b498ef88e1b40b9abf84e1d|	bedlington_terrier
|00290d3e1fdd27226ba27a8ce248ce85|	bedlington_terrier
|002a283a315af96eaea0e28e7163b21b|	borzoi
|003df8b8a8b05244b1d920bb6cf451f9|	basenji

The top 10 most common breeds are shown below. These are the labels used for the current model.
```
Index(['afghan_hound', 'basenji', 'bernese_mountain_dog', 'entlebucher',
       'great_pyrenees', 'maltese_dog', 'pomeranian', 'samoyed',
       'scottish_deerhound', 'shih-tzu']
```
The 10 selected breeds, as shown above, are actually commonly seen pet breeds, therefore, I think the model would have some practical value if it can predict these categories accurately.

## 3. Specification for the applied machine learning method
Since the aim of this project is to label images, I believe the method that presented the most promise in providing a solution is CNN. I first encoded the labeling into indicator variables using df.get_dummies(the resulting dataframe is shown below). 

![image](https://user-images.githubusercontent.com/57189964/117377291-eed6ff80-aea0-11eb-95ed-fcbea16ed6ad.png)


I then turned the images into pixel arrays and did data augmentation using ImageDataGenerator from tensorflow.
```
train_datagen = ImageDataGenerator(
    rotation_range=30,
    width_shift_range=0.2,
    height_shift_range=0.2,
    rescale=1./255,
    shear_range=0.2,
    zoom_range=0.2,
    horizontal_flip=True,
    fill_mode='nearest')

test_datagen=ImageDataGenerator(rescale=1./255)
```

Finally, after splitting the training and testing data using tts, I built the CNN model using keras. 

Model summary:
![image](https://user-images.githubusercontent.com/57189964/117377477-5bea9500-aea1-11eb-851d-195a52e178e8.png)

Model architecture, layers, functional arguments and specifications for compiling and fitting are shown as the code below:
```
model=Sequential()

model.add(ZeroPadding2D((1,1),input_shape=(299,299,3)))
model.add(Conv2D(32,kernel_size=(3,3),activation='relu'))
model.add(ZeroPadding2D(padding=(1,1)))
model.add(Conv2D(32,kernel_size=(3,3),activation='relu'))
model.add(MaxPooling2D(pool_size=(2,2),strides=(2,2)))

model.add(Flatten())
model.add(Dense(64,activation='relu'))
model.add(Dropout(0.2))

model.add(Dense(10,activation='softmax'))

model.compile(loss=categorical_crossentropy,optimizer='adam',metrics=['accuracy'])
model.summary()

epochs=30
history=model.fit_generator(training_set,
                        steps_per_epoch = 16,
                        validation_data = testing_set,
                        validation_steps = 4,
                        epochs = epochs,
                        verbose = 1)
```

## 4. Assessment of Model Performance
The performance and accuracy of the model is shown in the graph below (epoch=30).
![image](https://user-images.githubusercontent.com/57189964/117377980-7a9d5b80-aea2-11eb-8399-e9feac8b22b6.png)
Although CNN and image classfication is a well-studied field, few literature is available in this particular narrow topic I am interested in. However, as the original data is obtained from a Kaggle programming competition, I find that the highest rated submisson achived an accuracy of 0.98 using pretrained keras models (that are too complicated for me to understand or draw lessons from). Comparing to this top-rated model, my model still needs much improvement.
