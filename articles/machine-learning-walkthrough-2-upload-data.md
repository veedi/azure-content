<properties title="Step 2: Upload existing data into an Azure Machine Learning experiment" pageTitle="Step 2: Upload data into a Machine Learning experiment | Azure" description="Step 2: Upload existing public data into Azure Machine Learning Studio" metaKeywords="" services="machine-learning" solutions="big-data" documentationCenter="" authors="garye" videoId="" scriptId="" manager="paulettm" editor="cgronlun" />

<tags ms.service="machine-learning" ms.workload="tbd" ms.tgt_pltfrm="na" ms.devlang="na" ms.topic="article" ms.date="01/06/2015" ms.author="garye" />

This is the second step of the walkthrough, [Developing a Predictive Solution with Azure ML][develop]:

[develop]: ../machine-learning-walkthrough-develop-predictive-solution/


1.	[Create an ML workspace][create-workspace]
2.	**Upload existing data**
3.	[Create a new experiment][create-new]
4.	[Train and evaluate the models][train-models]
5.	[Publish the web service][publish]
6.	[Access the web service][access-ws]

[create-workspace]: ../machine-learning-walkthrough-1-create-ml-workspace/
[upload-data]: ../machine-learning-walkthrough-2-upload-data/
[create-new]: ../machine-learning-walkthrough-3-create-new-experiment/
[train-models]: ../machine-learning-walkthrough-4-train-and-evaluate-models/
[publish]: ../machine-learning-walkthrough-5-publish-web-service/
[access-ws]: ../machine-learning-walkthrough-6-access-web-service/

----------

#Step 2: Upload existing data into an Azure Machine Learning experiment  

To develop a predictive model for credit risk, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UCI Machine Learning repository. You can find it here:  
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>

We'll use the file named **german.data**. Download this file to your local hard drive.  

This dataset contains rows of 20 variables for 1000 past applicants for credit. These 20 variables represent the dataset's feature vector which provides identifying characteristics for each credit applicant. An additional column in each row represents the applicant's credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.   

The UCI website provides a description of the attributes of the feature vector, which include financial information, credit history, employment status, and personal information. For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.  

We'll use this data to train a predictive analytics model. When we're done, our model should be able to accept information for new individuals and predict whether they are a low or high credit risk.  

Here's one interesting twist. The description of the dataset explains that misclassifying a person as a low credit risk when they are actually a high credit risk is 5 times more costly to the financial institution than misclassifying a low credit risk as high. One simple way to take this into account in our experiment is by duplicating (5 times) those entries that represent someone with a high credit risk. Then, if the model misclassifies a high credit risk as low, it will do that misclassification 5 times, once for each duplicate. This will increase the cost of this error in the training results.  

##Convert the dataset format
The original dataset uses a blank-separated format. ML Studio works better with a comma-separated (CSV) file, so we'll convert the dataset by replacing spaces with commas.  

We can do this using the following Windows PowerShell command:   

	cat german.data | %{$_ -replace " ",","} | sc german.csv  

We can also do this using the Unix sed command:  

	sed 's/ /,/g' german.data > german.csv  

##Upload the dataset to ML Studio

Once the data has been converted to CSV format, we need to upload it into ML Studio.  

1.	Sign in to ML Studio ([https://studio.azureml.net](https://studio.azureml.net)) using the Microsoft account you specified as the owner of the workspace, and click the **Studio** tab at the top.
2.	Click **+NEW** at the bottom of the window.
3.	Select **DATASET**.
4.	Select **FROM LOCAL FILE**.
5.	In the **Upload a new dataset dialog**, click **Browse** and find the **german.csv** file you created.
6.	Enter a name for the dataset. For this example, we'll call it "UCI German Credit Card Data".
7.	For data type, select "Generic CSV File With no header (.nh.csv)".
8.	Add a description if you’d like.
9.	Click **OK**.  

![Upload the dataset][1]  

 
This uploads the data into a Dataset module that we can use in an experiment.

**Next: [Create a new experiment][create-new]**

[1]: ./media/machine-learning-walkthrough-2-upload-data/upload1.png
