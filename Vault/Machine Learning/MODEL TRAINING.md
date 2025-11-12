
## 1.1 Import Data and Required Packages
##### Importing Pandas, Numpy, Matplotlib, Seaborn and Warings Library.

```python
# Basic Import
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt 
import seaborn as sns
# Modelling
from sklearn.metrics import mean_squared_error, r2_score
from sklearn.neighbors import KNeighborsRegressor
from sklearn.tree import DecisionTreeRegressor
from sklearn.ensemble import RandomForestRegressor,AdaBoostRegressor
from sklearn.svm import SVR
from sklearn.linear_model import LinearRegression, Ridge,Lasso
from sklearn.metrics import r2_score, mean_absolute_error, mean_squared_error
from sklearn.model_selection import RandomizedSearchCV
from catboost import CatBoostRegressor
from xgboost import XGBRegressor
import warnings
```

#### Import the CSV Data as Pandas DataFrame

```python
df = pd.read_csv('data/stud.csv')
```

#### Show Top 5 Records

```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gender</th>
      <th>race_ethnicity</th>
      <th>parental_level_of_education</th>
      <th>lunch</th>
      <th>test_preparation_course</th>
      <th>math_score</th>
      <th>reading_score</th>
      <th>writing_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>female</td>
      <td>group B</td>
      <td>bachelor's degree</td>
      <td>standard</td>
      <td>none</td>
      <td>72</td>
      <td>72</td>
      <td>74</td>
    </tr>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>group C</td>
      <td>some college</td>
      <td>standard</td>
      <td>completed</td>
      <td>69</td>
      <td>90</td>
      <td>88</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>group B</td>
      <td>master's degree</td>
      <td>standard</td>
      <td>none</td>
      <td>90</td>
      <td>95</td>
      <td>93</td>
    </tr>
    <tr>
      <th>3</th>
      <td>male</td>
      <td>group A</td>
      <td>associate's degree</td>
      <td>free/reduced</td>
      <td>none</td>
      <td>47</td>
      <td>57</td>
      <td>44</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>group C</td>
      <td>some college</td>
      <td>standard</td>
      <td>none</td>
      <td>76</td>
      <td>78</td>
      <td>75</td>
    </tr>
  </tbody>
</table>
</div>



#### Preparing X and Y variables

```python
X = df.drop(columns=['math_score'],axis=1)
```

```python
X.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gender</th>
      <th>race_ethnicity</th>
      <th>parental_level_of_education</th>
      <th>lunch</th>
      <th>test_preparation_course</th>
      <th>reading_score</th>
      <th>writing_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>female</td>
      <td>group B</td>
      <td>bachelor's degree</td>
      <td>standard</td>
      <td>none</td>
      <td>72</td>
      <td>74</td>
    </tr>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>group C</td>
      <td>some college</td>
      <td>standard</td>
      <td>completed</td>
      <td>90</td>
      <td>88</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>group B</td>
      <td>master's degree</td>
      <td>standard</td>
      <td>none</td>
      <td>95</td>
      <td>93</td>
    </tr>
    <tr>
      <th>3</th>
      <td>male</td>
      <td>group A</td>
      <td>associate's degree</td>
      <td>free/reduced</td>
      <td>none</td>
      <td>57</td>
      <td>44</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>group C</td>
      <td>some college</td>
      <td>standard</td>
      <td>none</td>
      <td>78</td>
      <td>75</td>
    </tr>
  </tbody>
</table>
</div>



```python
print("Categories in 'gender' variable:     ",end=" " )
print(df['gender'].unique())

print("Categories in 'race_ethnicity' variable:  ",end=" ")
print(df['race_ethnicity'].unique())

print("Categories in'parental level of education' variable:",end=" " )
print(df['parental_level_of_education'].unique())

print("Categories in 'lunch' variable:     ",end=" " )
print(df['lunch'].unique())

print("Categories in 'test preparation course' variable:     ",end=" " )
print(df['test_preparation_course'].unique())
```

    Categories in 'gender' variable:      ['female' 'male']
    Categories in 'race_ethnicity' variable:   ['group B' 'group C' 'group A' 'group D' 'group E']
    Categories in'parental level of education' variable: ["bachelor's degree" 'some college' "master's degree" "associate's degree"
     'high school' 'some high school']
    Categories in 'lunch' variable:      ['standard' 'free/reduced']
    Categories in 'test preparation course' variable:      ['none' 'completed']


```python
y = df['math_score']
```

```python
y
```




    0      72
    1      69
    2      90
    3      47
    4      76
           ..
    995    88
    996    62
    997    59
    998    68
    999    77
    Name: math_score, Length: 1000, dtype: int64



```python
# Create Column Transformer with 3 types of transformers
num_features = X.select_dtypes(exclude="object").columns
cat_features = X.select_dtypes(include="object").columns

from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.compose import ColumnTransformer

numeric_transformer = StandardScaler()
oh_transformer = OneHotEncoder()

preprocessor = ColumnTransformer(
    [
        ("OneHotEncoder", oh_transformer, cat_features),
         ("StandardScaler", numeric_transformer, num_features),        
    ]
)
```

```python
X = preprocessor.fit_transform(X)
```

```python
X.shape
```




    (1000, 19)



```python
# separate dataset into train and test
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.2,random_state=42)
X_train.shape, X_test.shape
```




    ((800, 19), (200, 19))



#### Create an Evaluate Function to give all metrics after model Training

```python
def evaluate_model(true, predicted):
    mae = mean_absolute_error(true, predicted)
    mse = mean_squared_error(true, predicted)
    rmse = np.sqrt(mean_squared_error(true, predicted))
    r2_square = r2_score(true, predicted)
    return mae, rmse, r2_square
```

```python
models = {
    "Linear Regression": LinearRegression(),
    "Lasso": Lasso(),
    "Ridge": Ridge(),
    "K-Neighbors Regressor": KNeighborsRegressor(),
    "Decision Tree": DecisionTreeRegressor(),
    "Random Forest Regressor": RandomForestRegressor(),
    "XGBRegressor": XGBRegressor(), 
    "CatBoosting Regressor": CatBoostRegressor(verbose=False),
    "AdaBoost Regressor": AdaBoostRegressor()
}
model_list = []
r2_list =[]

for i in range(len(list(models))):
    model = list(models.values())[i]
    model.fit(X_train, y_train) # Train model

    # Make predictions
    y_train_pred = model.predict(X_train)
    y_test_pred = model.predict(X_test)
    
    # Evaluate Train and Test dataset
    model_train_mae , model_train_rmse, model_train_r2 = evaluate_model(y_train, y_train_pred)

    model_test_mae , model_test_rmse, model_test_r2 = evaluate_model(y_test, y_test_pred)

    
    print(list(models.keys())[i])
    model_list.append(list(models.keys())[i])
    
    print('Model performance for Training set')
    print("- Root Mean Squared Error: {:.4f}".format(model_train_rmse))
    print("- Mean Absolute Error: {:.4f}".format(model_train_mae))
    print("- R2 Score: {:.4f}".format(model_train_r2))

    print('----------------------------------')
    
    print('Model performance for Test set')
    print("- Root Mean Squared Error: {:.4f}".format(model_test_rmse))
    print("- Mean Absolute Error: {:.4f}".format(model_test_mae))
    print("- R2 Score: {:.4f}".format(model_test_r2))
    r2_list.append(model_test_r2)
    
    print('='*35)
    print('\n')
```

    Linear Regression
    Model performance for Training set
    - Root Mean Squared Error: 5.3243
    - Mean Absolute Error: 4.2671
    - R2 Score: 0.8743
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 5.3960
    - Mean Absolute Error: 4.2158
    - R2 Score: 0.8803
    ===================================
    
    
    Lasso
    Model performance for Training set
    - Root Mean Squared Error: 6.5938
    - Mean Absolute Error: 5.2063
    - R2 Score: 0.8071
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 6.5197
    - Mean Absolute Error: 5.1579
    - R2 Score: 0.8253
    ===================================
    
    
    Ridge
    Model performance for Training set
    - Root Mean Squared Error: 5.3233
    - Mean Absolute Error: 4.2650
    - R2 Score: 0.8743
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 5.3904
    - Mean Absolute Error: 4.2111
    - R2 Score: 0.8806
    ===================================
    
    
    K-Neighbors Regressor
    Model performance for Training set
    - Root Mean Squared Error: 5.7077
    - Mean Absolute Error: 4.5167
    - R2 Score: 0.8555
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 7.2530
    - Mean Absolute Error: 5.6210
    - R2 Score: 0.7838
    ===================================
    
    
    Decision Tree
    Model performance for Training set
    - Root Mean Squared Error: 0.2795
    - Mean Absolute Error: 0.0187
    - R2 Score: 0.9997
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 7.6371
    - Mean Absolute Error: 6.0250
    - R2 Score: 0.7603
    ===================================
    
    
    Random Forest Regressor
    Model performance for Training set
    - Root Mean Squared Error: 2.2851
    - Mean Absolute Error: 1.8253
    - R2 Score: 0.9768
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 6.0959
    - Mean Absolute Error: 4.7194
    - R2 Score: 0.8473
    ===================================
    
    
    XGBRegressor
    Model performance for Training set
    - Root Mean Squared Error: 0.9087
    - Mean Absolute Error: 0.6148
    - R2 Score: 0.9963
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 6.5889
    - Mean Absolute Error: 5.0844
    - R2 Score: 0.8216
    ===================================
    
    
    CatBoosting Regressor
    Model performance for Training set
    - Root Mean Squared Error: 3.0427
    - Mean Absolute Error: 2.4054
    - R2 Score: 0.9589
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 6.0086
    - Mean Absolute Error: 4.6125
    - R2 Score: 0.8516
    ===================================
    
    
    AdaBoost Regressor
    Model performance for Training set
    - Root Mean Squared Error: 5.7843
    - Mean Absolute Error: 4.7564
    - R2 Score: 0.8516
    ----------------------------------
    Model performance for Test set
    - Root Mean Squared Error: 6.0447
    - Mean Absolute Error: 4.6813
    - R2 Score: 0.8498
    ===================================
    
    


### Results

```python
pd.DataFrame(list(zip(model_list, r2_list)), columns=['Model Name', 'R2_Score']).sort_values(by=["R2_Score"],ascending=False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Model Name</th>
      <th>R2_Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Ridge</td>
      <td>0.880593</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Linear Regression</td>
      <td>0.880345</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CatBoosting Regressor</td>
      <td>0.851632</td>
    </tr>
    <tr>
      <th>8</th>
      <td>AdaBoost Regressor</td>
      <td>0.849847</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Random Forest Regressor</td>
      <td>0.847291</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Lasso</td>
      <td>0.825320</td>
    </tr>
    <tr>
      <th>6</th>
      <td>XGBRegressor</td>
      <td>0.821589</td>
    </tr>
    <tr>
      <th>3</th>
      <td>K-Neighbors Regressor</td>
      <td>0.783813</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Decision Tree</td>
      <td>0.760313</td>
    </tr>
  </tbody>
</table>
</div>



## Linear Regression

```python
lin_model = LinearRegression(fit_intercept=True)
lin_model = lin_model.fit(X_train, y_train)
y_pred = lin_model.predict(X_test)
score = r2_score(y_test, y_pred)*100
print(" Accuracy of the model is %.2f" %score)
```

     Accuracy of the model is 88.03


## Plot y_pred and y_test

```python
plt.scatter(y_test,y_pred);
plt.xlabel('Actual');
plt.ylabel('Predicted');
```


    
![png](output_25_0.png)
    


```python
sns.regplot(x=y_test,y=y_pred,ci=None,color ='red');
```


    
![png](output_26_0.png)
    


#### Difference between Actual and Predicted Values

```python
pred_df=pd.DataFrame({'Actual Value':y_test,'Predicted Value':y_pred,'Difference':y_test-y_pred})
pred_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Actual Value</th>
      <th>Predicted Value</th>
      <th>Difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>521</th>
      <td>91</td>
      <td>76.507812</td>
      <td>14.492188</td>
    </tr>
    <tr>
      <th>737</th>
      <td>53</td>
      <td>58.953125</td>
      <td>-5.953125</td>
    </tr>
    <tr>
      <th>740</th>
      <td>80</td>
      <td>76.960938</td>
      <td>3.039062</td>
    </tr>
    <tr>
      <th>660</th>
      <td>74</td>
      <td>76.757812</td>
      <td>-2.757812</td>
    </tr>
    <tr>
      <th>411</th>
      <td>84</td>
      <td>87.539062</td>
      <td>-3.539062</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>408</th>
      <td>52</td>
      <td>43.546875</td>
      <td>8.453125</td>
    </tr>
    <tr>
      <th>332</th>
      <td>62</td>
      <td>62.031250</td>
      <td>-0.031250</td>
    </tr>
    <tr>
      <th>208</th>
      <td>74</td>
      <td>67.976562</td>
      <td>6.023438</td>
    </tr>
    <tr>
      <th>613</th>
      <td>65</td>
      <td>67.132812</td>
      <td>-2.132812</td>
    </tr>
    <tr>
      <th>78</th>
      <td>61</td>
      <td>62.492188</td>
      <td>-1.492188</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 3 columns</p>
</div>



```python

```
