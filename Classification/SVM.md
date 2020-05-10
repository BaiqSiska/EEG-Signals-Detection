Support Vector Machine
===

Support Vector Machine (SVM) is one of the binary classification methods that is most often used to solve classification problems, especially in binary cases but requires a long time in analysis. SVM is a learning machine method that works on the principle of Structural Risk Minimization (SRM) to find the best hyperplane that separates two classes in the input space. SVM is a method applied to classify linear and nonlinear cases. SVM algorithm acts using nonlinear mapping to transform training data from a new dimension to a higher dimension. SVM has got new dimensions then looking for an optimal hyperplane to separate class labels with each other. SVM has got high dimensions then looking for an optimal hyperplane to separate class labels with each other.

Some of kernel function has normally used as follows:
  * Kernel Linear
  * Kernel RBF
  * Kernel Poly

                                             SVM with Kernel Linear
```
import pandas as pd
import numpy as np
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split, GridSearchCV, cross_val_score,StratifiedKFold
from sklearn.feature_selection import SelectFromModel
from sklearn.metrics import confusion_matrix, accuracy_score, log_loss, roc_auc_score

data=pd.read_csv(r'E:\MAGISTER\DATA\ANALISIS\POTONG DATA\EEG_dataset.csv', index_col=None)
y1=data['label']
x1=data.iloc[:,0:37]
y = np.squeeze(np.asarray(y1))
import time
from sklearn import svm
start= time.time()
svm=svm.SVC(class_weight=None,C=0.001,kernel='linear',random_state=100) 
#Setup arrays to store training and test accuracies
n=10 #number of fold
from sklearn.model_selection import StratifiedKFold
kf=StratifiedKFold(n_splits=n, random_state=None)
cm=[]
total=[]
ac=[]
se=[]
sp=[]
auc=[]

for train_index, test_index in kf.split(X,y):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    svm.fit(X_train, y_train)
    y_pred = svm.predict(X_test)
    cm.append((confusion_matrix(y_test, y_pred)).astype(float))
for j in range (n):
    total.append(sum(sum(cm[j])))
    ac.append((cm[j][0,0]+cm[j][1,1])/total[j])
    se.append(cm[j][0,0]/(cm[j][0,0]+cm[j][0,1]))
    sp.append(cm[j][1,1]/(cm[j][1,0]+cm[j][1,1]))
    auc.append(((cm[j][0,0]/(cm[j][0,0]+cm[j][0,1]))+(cm[j][1,1]/(cm[j][1,0]+cm[j][1,1])))/2)
akurasi=np.mean(ac)
spesifisiti=np.mean(se)
sensitiviti=np.mean(sp)
AUC=np.mean(auc)
df=pd.DataFrame()
test=dict()
for j in range (4):
    test[j]=[]
for i in range (n):
    test[0].append(ac[i])
    test[1].append(se[i])
    test[2].append(sp[i])
    test[3].append(auc[i])
for i in range (4):
    df_k2=pd.concat([df_k2,pd.DataFrame(test[i])],axis=1)
df.columns=['Akurasi','Spesifisitas','Sensitivitas','Area Under the Curve']
end = time.time()
print ("Waktu Proses Klasifikasi SVM dengan Kernel Linear", end - start,"Second")
df

```
the results are as follows:

---
![linar](https://user-images.githubusercontent.com/10173320/81488392-59575e80-9292-11ea-8554-ff049e8b466f.png)
---


                                             SVM with Kernel RBF
```
import pandas as pd
import numpy as np
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split, GridSearchCV, cross_val_score,StratifiedKFold
from sklearn.feature_selection import SelectFromModel
from sklearn.metrics import confusion_matrix, accuracy_score, log_loss, roc_auc_score

data=pd.read_csv(r'E:\MAGISTER\DATA\ANALISIS\POTONG DATA\EEG_dataset.csv', index_col=None)
y1=data['label']
x1=data.iloc[:,0:37]
y = np.squeeze(np.asarray(y1))
import time
from sklearn import svm
start= time.time()
svm=svm.SVC(class_weight=None,C=10,gamma=0.001,kernel='rbf',random_state=100) 
#Setup arrays to store training and test accuracies
n=10 #number of fold
from sklearn.model_selection import StratifiedKFold
kf=StratifiedKFold(n_splits=n, random_state=None)
cm=[]
total=[]
ac=[]
se=[]
sp=[]
auc=[]

for train_index, test_index in kf.split(X,y):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    svm.fit(X_train, y_train)
    y_pred = svm.predict(X_test)
    cm.append((confusion_matrix(y_test, y_pred)).astype(float))
for j in range (n):
    total.append(sum(sum(cm[j])))
    ac.append((cm[j][0,0]+cm[j][1,1])/total[j])
    se.append(cm[j][0,0]/(cm[j][0,0]+cm[j][0,1]))
    sp.append(cm[j][1,1]/(cm[j][1,0]+cm[j][1,1]))
    auc.append(((cm[j][0,0]/(cm[j][0,0]+cm[j][0,1]))+(cm[j][1,1]/(cm[j][1,0]+cm[j][1,1])))/2)
akurasi=np.mean(ac)
spesifisiti=np.mean(se)
sensitiviti=np.mean(sp)
AUC=np.mean(auc)
df=pd.DataFrame()
test=dict()
for j in range (4):
    test[j]=[]
for i in range (n):
    test[0].append(ac[i])
    test[1].append(se[i])
    test[2].append(sp[i])
    test[3].append(auc[i])
for i in range (4):
    df_k2=pd.concat([df_k2,pd.DataFrame(test[i])],axis=1)
df.columns=['Akurasi','Spesifisitas','Sensitivitas','Area Under the Curve']
end = time.time()
print ("Waktu Proses Klasifikasi SVM dengan Kernel RBF", end - start,"Second")
df

```
the results are as follows:

---
![rbf](https://user-images.githubusercontent.com/10173320/81488435-e8647680-9292-11ea-8e9e-97762d89f818.png)
---

                                               SVM with Kernel Poly
```
import pandas as pd
import numpy as np
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split, GridSearchCV, cross_val_score,StratifiedKFold
from sklearn.feature_selection import SelectFromModel
from sklearn.metrics import confusion_matrix, accuracy_score, log_loss, roc_auc_score

data=pd.read_csv(r'E:\MAGISTER\DATA\ANALISIS\POTONG DATA\EEG_dataset.csv', index_col=None)
y1=data['label']
x1=data.iloc[:,0:37]
y = np.squeeze(np.asarray(y1))
import time
from sklearn import svm
start= time.time()
svm=svm.SVC(class_weight=None,C=0.025,gamma=0.001,kernel='poly',random_state=100) 
#Setup arrays to store training and test accuracies
n=10 #number of fold
from sklearn.model_selection import StratifiedKFold
kf=StratifiedKFold(n_splits=n, random_state=None)
cm=[]
total=[]
ac=[]
se=[]
sp=[]
auc=[]

for train_index, test_index in kf.split(X,y):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    svm.fit(X_train, y_train)
    y_pred = svm.predict(X_test)
    cm.append((confusion_matrix(y_test, y_pred)).astype(float))
for j in range (n):
    total.append(sum(sum(cm[j])))
    ac.append((cm[j][0,0]+cm[j][1,1])/total[j])
    se.append(cm[j][0,0]/(cm[j][0,0]+cm[j][0,1]))
    sp.append(cm[j][1,1]/(cm[j][1,0]+cm[j][1,1]))
    auc.append(((cm[j][0,0]/(cm[j][0,0]+cm[j][0,1]))+(cm[j][1,1]/(cm[j][1,0]+cm[j][1,1])))/2)
akurasi=np.mean(ac)
spesifisiti=np.mean(se)
sensitiviti=np.mean(sp)
AUC=np.mean(auc)
df=pd.DataFrame()
test=dict()
for j in range (4):
    test[j]=[]
for i in range (n):
    test[0].append(ac[i])
    test[1].append(se[i])
    test[2].append(sp[i])
    test[3].append(auc[i])
for i in range (4):
    df_k2=pd.concat([df_k2,pd.DataFrame(test[i])],axis=1)
df.columns=['Akurasi','Spesifisitas','Sensitivitas','Area Under the Curve']
end = time.time()
print ("Waktu Proses Klasifikasi SVM dengan Kernel Polynomial", end - start,"Second")
df

```
the results are as follows:

---
![poly](https://user-images.githubusercontent.com/10173320/81488465-5741cf80-9293-11ea-89ca-e7d86a9acfb0.png)
---
