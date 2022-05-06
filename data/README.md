# Titanic Dataset with dvc version control

### Initialize and setup dvc for data folder

* Download dataset from [here](https://www.kaggle.com/competitions/titanic/data)

* Create a remote storage in Google drive(You can use local or cloud remote storage.)

* Since we have data in both raw and processed folder we will track both of those folder using ```dvc```.

* We will have two version of processed dataset and one single version of raw data during this example.

Steps : (run these steps from titanic folder in terminal path)

```
git init 

dvc init

git add .dvc/

git commit -m "Initialize DVC"

dvc add data/raw

git add 'data\.gitignore' 'data\raw.dvc'

dvc add data/processed/

git add 'data\.gitignore' 'data\processed.dvc'

git commit -m " Added raw and processed data folder tracking "

```

According to the above steps the folder structure would look like

titanic/raw 
* .gitkeep
* gender_submission.csv
* test.csv
* train.csv

titanic/processed
* .gitkeep


### Remote data storage setup

For this example, a google drive folder named titanic is created. </br> 
Anyone with this [link](https://drive.google.com/drive/folders/1bsoNT0rQycXZr0p39AlFtq2rrvfSWgdK) can access the drive. </br>
We will use this folder as remote location for our folder to track data.For remotely adding this folder to our dvc tracked dataset we will first take the last part of the folder link which is this case is : 
```
1bsoNT0rQycXZr0p39AlFtq2rrvfSWgdK
```  

Now we will follow the following commands

```

dvc remote add -d storage gdrive:/1bsoNT0rQycXZr0p39AlFtq2rrvfSWgdK 
# Will create config file containing remote storage address inside .dvc folder inside 

git commit .dvc/config -m "Configured remnote storage" 

dvc push
# Sometime remote location address inside .dvc/config might be incorrect. Change accordingly

```
Currently we have no processed data what so ever. We will create two python scripts which will create two version of processed data. Lets see how we can track them.

```