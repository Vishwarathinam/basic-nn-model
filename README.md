# Developing a Neural Network Regression Model

## AIM

To develop a neural network regression model for the given dataset.

## THEORY

Neural network regression is a supervised learning method, and therefore requires a tagged dataset, which includes a label column. Because a regression model predicts a numerical value, the label column must be a numerical data type. You can train the model by providing the model and the tagged dataset as an input to Train Model.

In this experiment we need to develop a Neural Network Regression Model so first we need to create a dataset (i.e : an excel file with some inputs as well as corresponding outputs).Then upload the sheet to drive then using corresponding code open the sheet and then import the required python libraries for porcessing.

Use df.head to get the first 5 values from the dataset or sheet.Then assign x and y values for input and coressponding outputs.Then split the dataset into testing and training,fit the training set and for the model use the "relu" activation function for the hidden layers of the neural network (here two hidden layers of 4 and 6 neurons are taken to process).To check the loss mean square error is uesd.Then the testing set is taken and fitted, at last the model is checked for accuracy via preiction.

## Neural Network Model

![neural-network-model](https://user-images.githubusercontent.com/95266350/187114481-389a6719-af9d-4d1f-b66b-571b1e6b6a68.png)

## DESIGN STEPS

### STEP 1:

Loading the dataset

### STEP 2:

Split the dataset into training and testing

### STEP 3:

Create MinMaxScalar objects ,fit the model and transform the data.

### STEP 4:

Build the Neural Network Model and compile the model.

### STEP 5:

Train the model with the training data.

### STEP 6:

Plot the performance plot

### STEP 7:

Evaluate the model with the testing data.

## PROGRAM
~~~
 Developed by : vishwa rathinam.S
 Reg.no : 212221240063
 Program to develop a neural network regression model
 
### To Read CSV file from Google Drive :

from google.colab import auth
import gspread
from google.auth import default
import pandas as pd

### Authenticate User:

auth.authenticate_user()
creds, _ = default()
gc = gspread.authorize(creds)

### Open the Google Sheet and convert into DataFrame :

worksheet = gc.open('data').sheet1
rows = worksheet.get_all_values()
df = pd.DataFrame(rows[1:], columns = rows[0])
df = df.astype({'Input':'int','Output':'int'})

### Import the packages :

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

df.head()

X = df[['Input']].values
y = df[['Output']].values
X

### Split Training and testing set :

X_train,X_test,y_train,y_test = train_test_split(X,y,test_size = 0.33,random_state = 42)

### Pre-processing the data :

Scaler = MinMaxScaler()
Scaler.fit(X_train)
Scaler.fit(X_test)

X_train1 = Scaler.transform(X_train)
X_test1 = Scaler.transform(X_test)

X_train1

### Model :

ai_brain = Sequential([
    Dense(4,activation = 'relu'),
    Dense(6,activation = 'relu'),
    Dense(1)
])

ai_brain.compile(
    optimizer = 'rmsprop',
    loss = 'mse'
)

ai_brain.fit(X_train1,y_train,epochs = 4000)

### Loss plot :

loss_df = pd.DataFrame(ai_brain.history.history)

loss_df.plot()

### Testing with the test data and predicting the output :

ai_brain.evaluate(X_test1,y_test)

X_n1 = [[89]]

X_n1_1 = Scaler.transform(X_n1)

ai_brain.predict(X_n1_1)

~~~

## Dataset Information

![out1](https://user-images.githubusercontent.com/95266350/187114538-370bed6f-3e6a-4227-bd2c-1bd051b93842.png)

## OUTPUT

### Initiation of program
![out2](https://user-images.githubusercontent.com/95266350/187114802-19c38500-5117-4d3e-b3cb-73e52d98e1d9.png)

![out3](https://user-images.githubusercontent.com/95266350/187114830-c3f80608-25db-461c-95ee-d0ef8102d3f6.png)

![out4](https://user-images.githubusercontent.com/95266350/187114859-917ced87-0ed2-4729-8333-3a28d94881fc.png)

### Training Loss Vs Iteration Plot
![out5](https://user-images.githubusercontent.com/95266350/187114904-67e6a85d-a4e0-4894-819e-8c147d2c3258.png)

![out6](https://user-images.githubusercontent.com/95266350/187114987-6de0aaf8-d177-43d4-8600-51239ad77d72.png)

### Test Data Root Mean Squared Error
![out7](https://user-images.githubusercontent.com/95266350/187115012-c29cc70c-74cd-47d8-91b1-7a210f161c4c.png)

### New Sample Data Prediction
![out8](https://user-images.githubusercontent.com/95266350/187115058-2aa96e05-e26a-423d-bf40-c0107c86c9da.png)

## RESULT
Thus a neural network model for regression using the given dataset is written and executed successfully.
