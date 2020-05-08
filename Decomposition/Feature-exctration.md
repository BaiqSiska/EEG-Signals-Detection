Feature Exctraction
===
Feature extraction is a method produced features used as independent variables. It was to solving classification problems of EEG signals. Some features used in this case as follows:
* Mean
* Maximum
* Minimum
* Entropy
* Deviance

---
Mean script as follows:
```
import statistics
import pandas as pd
import numpy as np

Mean = []
# a same as d
a = data.as_matrix()

for column in range(0,21600):
    b=data.iloc[:,column].isnull().sum()
    Mean.append(np.mean(a[:,column]))

Mean = pd.DataFrame(ratarata, columns=['Mean '])
Mean.tail()
```
Maximum Script as follows:
```
Maksimum = []

# a same as d
a = data.as_matrix()

for column in range(0,21600):#diganti sesuai jumlah kolom
    Maksimum.append(max(a[:,column]))

Maksimum = pd.DataFrame(Maksimum, columns=['Maksimum'])
Maksimum.tail()
```
Minimum Script as follows:
```
Minimum = []

# a same as d
a = data.as_matrix()

for column in range(0,21600):
    Minimum.append(min(a[:,column]))

Minimum = pd.DataFrame(Minimum, columns=['Minimum'])
Minimum.tail()
```
 Entropy
 ```
entropy=[]
b=dict()
result=dict()
entr=dict()
for i in range (0,1500):
    result[i] = df3.iloc[:,i]
    entropy.append(sum([(xi ** 2)*np.log10(xi**2) for xi in result[i]]))
entropy=pd.DataFrame([entropy])
entropy=np.transpose(entropy)
entropy.columns=['entropy']
entropy.to_csv('Entrp.csv')
entropy.head()
 ```
Deviance
 ```
Deviance = []

# a same as d
a = data.as_matrix()
b=dict()
for column in range(0,15120):
    b=data.iloc[:,column].isnull().sum()
    Deviance.append(np.std(a[0:a.shape[0]-b,column]))

Deviance = pd.DataFrame(StandarDeviasi, columns=['Deviance'])
Deviance.tail()
```
