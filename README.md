# azure_ml


# azure-machine-learning
azure dp 100 divided into 4 sections
1.seeting azure ml workspace
2.run experiments anmd train models
3.optimize and run models
4.deployement


========
 azure ml workspace**:
1.creste an azure workspace
2.manage data objects in workplace
3.manage experiment compute contexts


  run experiments and train models:
--> create model by azureML designer
--> run training scripts in azure ml workpace
--> generate metrics from experiment run
->automate model training sceipts

optimize models:
1. use automated ml  to create optimal models
2. use hyperdrive to tune hyperameters
3.manage models

  deployement:
1.create production compute targets
2. deploy model as service
3. create pipeline for batch interfacing
4.publish a designer pipeline asa web service


  workspace is central resporstry:
1.compute instance
2.compur clusters

  linked services:
1.data stores
2.compute targets


 creating a azure workspace 
 --> all azure machine learning services stores information in cosmoDB

 datastore:  connection information of all data storages account
  -> contains all database connectioins information in azure
 usinh "sas" we can connect datastore




  compute instance:

data storage created while creating resource gruop mounted to "compute instance"

compute instance: used for traininga and developing purpose
compute clusters: used for pipeline
compute targets :used for model deployement VM,LOCAL MACHINE

--> use compute instance while  developing model using note books
-->use compue clusters for auto ml is used
-->testing for deployement use compute targets
--> final deplyment use 'interfernce clusters"


create compute instance or compute clusters:

--> use compute option to crrate both of compute 


run experiments and train models:

how to create a pipeine:
--> click deigner option
--> we have option to selct coulumns in dataset - select
--> split data  test= 0.7,  train=0.3
-->stratification column - dependent column
-->two class LOGIIESTIC REGRESSION
-->RANDOM SEED =123



interfernce pipeline:
--> it is present in jobs option (three dots)

--> webserve input and webservice output added in the flow
--> target column sholid be removed in selected columns module
--> webservie input given to apply transformation

getting data from outside:
--> select import data component and give data url in respective url
-->we have to run the pipeline to get the data, 
--> for editing the data, "use edit metadata" component

if you want export data from one component to datastore use "export data"-

--> add columns are used to addd two tables
-->to add rows "Add rows" is used add two 

NORMALIZATION:

--> conversetion of large scale data into small values for data distrubution, varaiable sshould be in 0 or 1
-->it is appile din numerical col5. apply normalizationumns   
--> methods for NORMALIZATION
         1.zscore
         2.minmax
         3.logistic
 normalize using azure ML:
 --> USE normalize component FOR normalize

--> misisng module is cleaning the data
-->split data module is used for data partioning

logistic REGRESSION:

--> it is used for classification for binary classification, SUPERVIDSED learning
-->  y=b+b1x
--> propability=e^y/e^y+1
--> q=1-p

data preparation:

1. convert metadata string foramat into numerical format
2. missinf data handling
3. split the data
4. normalize the data (first train data normalize)
5.apply normalization transformation to test data

configure the alogoritham:

train the model with normalize  training data

score the model using normalixze transformation test data

evaluate the model

-----------------

for normalization we use two functions
1.normalization for train inf data
2. apply for transformation for test, requires two inputs, one from normalization and another split data2

------------------------------------------------------------
1.import data
2. edit meta data
3.split the data
4.apply normalization on training dataset
5. tale transformation normalize the test data
6. take algoritham based on requirement
7.train the model component with algoritham and train data
8.score model with test data and trained model
9. evaluate the model using score models


"clip model"   is used foe removing outliers

confusion matrix:

                  predicted_positives      predicted_negitives

actual positives   true positive           false negitives


actual negitives   flase positive           true negitive


DECEISION TREE:

-->USEWD FOR CONTIONOUS AND CETEGORICAL
-->root node - >decisison node-> terminal node

ensemble learning:
->bagging
->boosting

bagging ans boosting in decisiion tree:
bagging:
-->various models are built production
-->all models give to give final prediction
--> majaroty model output is final result
"random forest model is example foe ensemble learning"

BOOSTING:
--> TRAIN THE ALGO WITH SEQUNCE
--> LEARN FROM PREVIOUS TREEby focussing on incoreect observations
-->build new model with higher weignt for incoreect  observations  from previous SEQUNCE

simple linear REGRESSION:
-->continous varaiable output
--> relation between one or more independent varaiable with dependent values

ordinary least Squares:
--> this method means least squares

mean abosulate eerror:

--> average of sqaures of abosulte error

root mean sqaured eeror:

--> root of mean squared error

--> stratified split is only for "classification"


Gradicient DECENT:

-->calculus ,rate of change limits

--> dy/dx=2x   positive slope, negitive slope



PANDAS:

data=pd.read_csv("data",header=None,names=columns)
data=data.iloc[1:4]   -- only rows
data=data.iloc[1:4,1:5]  --> both rows and columns
x=data[:,:-1]
y=data[:,-1:]
data=data[["a","b"]]  --> assign required columns
data=data.drop(['a','b'],axis=1)  --> removing the columns  axis=1 means columns, 0 ,means rows
data=data.join(data1)
data=data.concat(dat,dat1,ignore_indes=True)  for restiing index
data.isnull()  -->get true or flase 
data.isnull().sum()  -> get how many elementsa are null in each column
data.dropna(axis=0)  -> drop row where values are missing
data.dropna(axis=1)  -> drop columns whic are missing
data.dtypes

data["a"]=data["a"].astype("category") --> changing float type to categorical

data.describe(), data.describe(include='all',percentailes=[0.01,0.05,0.1,0.9,0.99])  --> to get all percentailes
data[['income']].clip(lower=999,upper=50000)   used for set values between this limits "constants values"
data[[income']].clip()
dta=data.selct_dtypes(include='numerber').columns  

# converting columns using clap functions

data_n=data.select_dtypes(include='numbers').columns    ->get columns whic are numerical
-->for column in data_n:
      lower=data[['column']].quantile(0.01) # 1%
      upper=data[['column']].quantile(0.99) # 99%
      data['column']=data['column'].clap(lower,upper)


##normalization is done in sckit learan linrary

-->from sckitlearn.preprocessing import minMaxScaler
   scaler=minMaxScaler()
   scaler.fit_transform(columns)


# label encoding

data=data.slect_dtype(include="category").columns

--->data["a"]=data["a"].astype("category")
==>data["a"]=data["a"].cat.codes --> changing 0 or 1 one hot encoding

# who to convert string to category
-->data=data.select_dtypes(include="object").columns

for column in columns:
   data['columnn']=data['column'].cat.codes

# one hot coding

--> data=pd.get_dummies(data)

## splt the test and train dataset
==>
import sklearn.model_selection import  train_test_split

x_train,x_test,y_train,y_test=train_test_split(x,y,train_size=0.7,random_state=123,stratify=y)

#logistic regressiom

==>from sklearn.linear_model import LogisticRegression

-->  lr=LogisticRegression()

#train

-> lr.fit(x_train,y_train)  # 

#test

a=lr.predict(x_test)

#propability

==>dat_pro=lr.predict_proba(x_test)


$metrics

=> from sklearn.metrics import confusion_matrix

cm=confusion_matrix(y_test,y_predict)





