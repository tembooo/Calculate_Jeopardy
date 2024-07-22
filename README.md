# Calculate_Jeopardy
This project involves analyzing a Jeopardy dataset by writing functions to: Filter topics of interest to create a personalized dataset. Compute the average difficulty of selected questions for targeted practice. Utilize the filtered dataset for training to become the next Jeopardy champion.<br/>
## Step1:Prerequisites
In order to complete this project, you should have completed the Pandas lessons in the Analyze Data with Python Skill Path.
## Step2:Load the data into a DataFrame
We’ve provided a csv file containing data about the game show Jeopardy! in a file named `jeopardy.csv`. Load the data into a DataFrame and investigate its contents. Try to print out specific columns.
Note that in order to make this project as “real-world” as possible, we haven’t modified the data at all — we’re giving it to you exactly how we found it. As a result, this data isn’t as “clean” as the datasets you normally find on Codecademy. More specifically, there’s something odd about the column names. After you figure out the problem with the column names, you may want to rename them to make your life easier the rest of the project.<br/>
In order to display the full contents of a column, we’ve added this line of code to the top of your file:
```python
pd.set_option('display.max_colwidth', none)
```
The column names all have a leading space. For example, the column that contains the answers is `" Answer"`. Notice the space at the front of the column name.
```python
#Step2
import pandas as pd
pd.set_option('display.max_colwidth', None)

# Loading the data and investigating it
jeopardy_data = pd.read_csv("jeopardy.csv")
print(jeopardy_data.columns)

# Renaming misformatted columns
jeopardy_data = jeopardy_data.rename(columns = {" Air Date": "Air Date", " Round" : "Round", " Category": "Category", " Value": "Value", " Question":"Question", " Answer": "Answer"})
print(jeopardy_data.columns)
print(jeopardy_data["Question"])
```
## Step3: Write a function that filters the dataset for questions that contains all of the words in a list of words.
For example, when the list `["King", "England"]` was passed to our function, the function returned a DataFrame of 152 rows. Every row had the strings "King" and "England" somewhere in its " Question".
```python
#Step3
#Filtering a dataset by a list of words
def filter_data(data, words):
  #Lowercases all words in the list of words as well as the questions. Returns true if all of the words in the list appear in the question.
  filter = lambda x: all(word in x for word in words)
  #Applies the lambda function to the Question column and returns the rows where the function returned True
  return data.loc[data["Question"].apply(filter)]

#Testing the filter function
filtered = filter_data(jeopardy_data, ["King", "England"])
print(filtered["Question"])
```
## Step4: Test your original function with a few different sets of words to try to find some ways your function breaks.
For example, think about capitalization. We probably want to find questions that contain the word `"King"` or `"king"`.<br/>
You may also want to check to make sure you don’t find rows that contain substrings of your given words.</br>
For example, our function found a question that didn’t contain the word "king", however it did contain the word "viking" — it found the "king" inside "viking". Note that this also comes with some drawbacks — you would no longer find questions that contained words like "England's".
```python
#Step4
#Filtering a dataset by a list of words
def filter_data(data, words):
  #Lowercases all words in the list of words as well as the questions. Returns true if all of the words in the list appear in the question.
  filter = lambda x: all(word.lower() in x.lower() for word in words)
  #Applies the lambda function to the Question column and returns the rows where the function returned True
  return data.loc[data["Question"].apply(filter)]
#Testing the filter function
filtered = filter_data(jeopardy_data, ["King", "England"])
print(filtered["Question"])
```






