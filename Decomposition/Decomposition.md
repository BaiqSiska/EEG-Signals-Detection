Decomposition
===
EEG signals that have been cut will be processed again into some sub-bands of signals which are often called the signal decomposition process. The EEG signals decomposition process, in this case, uses the Wavelet Transform (WT) method, especially the Discrete Wavelet Transform. EEG signal decomposition was done before doing the feature extraction process. This process will decompose the signal into low and high sub-signals. The high signal will be eliminated and the low signal will be decomposed again into two slices, it is a level decomposition process.
Below is the illustration of the decomposition signal on 7th level.

![Screenshot from 2020-05-08 09-57-35](https://user-images.githubusercontent.com/10173320/81365498-79f8aa80-9112-11ea-9d08-ed0fb65d2ed5.png)

Descrete Wavele Transform (DWT)
---
Wave is a function of time or space that moves (oscillating). Wavelets are small waves that have energy focused on time, providing tools for transient, non-stationary analysis, phenomena that vary with time. The below picture is some wavelet has normally used. 
![wavelet1](https://user-images.githubusercontent.com/10173320/81378487-9526e280-9131-11ea-9a53-79cf67b427ae.png)

Wavelet transform is a tool used to cut data or functions into different frequency components and study each component according to the scale resolution. Wavelet transform has classified into two types, Continuous Wavelet Transform (CWT) and Discrete Wavelet Transform (DWT). Now, I use DWT for decomposition EEG signals. DWT has used as a method for breaking down EEG signals into several different frequency bands. DWT decomposes the signal by estimating the details of the first level coefficient, then estimating the details of the signal coefficient for signal decomposition at the estimated next level coefficient.

Theories of decomposition signals step as follows:
* EEG signals have been cut off.
* EEG signal has filtered into two parts a high frequency (H) and low (L).
* Hereafter, it was determined the approximate coefficient (A1) and detail (D1) values using the downsampling method.
* Therefore, it has got a first-level decomposition.
* Please, do above step get the next level decomposition.

DWT script as follows:

---
```
import pandas as pd
import numpy as np
```
Below script is used to unite all the signal pieces.
```
import glob
a=glob.glob(r'E:\MAGISTER\DATA\ANALISIS\POTONG DATA\A\A*.txt')
b=glob.glob(r'E:\MAGISTER\DATA\ANALISIS\POTONG DATA\I\I*.txt')
a.sort()
b.sort()
allFiles=a+b
list_=[]
for file_ in allFiles:
    df = pd.read_csv(file_,index_col=None, header=None)
    list_.append(df)
df1 = pd.DataFrame()
for i in range (0,len(allFiles)) :
    df1=pd.concat([df1, list_[i]], axis=1)
L = ['A','I']
K = [len(a),len(b)]
kolom=[]
for i in range (len(K)):
    L2 = range(1, (K[i]+1))
    kolom= kolom+[x+ str(y) for x,y in list(product(L[i],L2))]
df1.columns=kolom
df1=df1.dropna()
df1.tail()
```
Below script is used to decomposition signals into 7th level.
```
import time
import matplotlib.pyplot as plt
import pywt
import pywt.data
start = time.time()
mode = pywt.Modes.smooth
w = pywt.Wavelet('db4')
x= range(2160)
y=range(9)
ca=dict()
cd=dict()
rec_a=dict()
rec_d=dict()

for i in range(0,2160):
    a = df1.iloc[:,i]
    ca[i] = []
    cd[i] = []
    for j in y:
        (a, d) = pywt.dwt(a, w, mode)
        ca[i].append(a)
        cd[i].append(d)

    rec_a[i] = []
    rec_d[i] = []

    for j, coeff in enumerate(ca[i]):
        coeff_list = [coeff, None] + [None] * j
        rec_a[i].append(pd.DataFrame(pywt.waverec(coeff_list, w)))

    for j, coeff in enumerate(cd[i]):
        coeff_list = [None, coeff] + [None] * j
        rec_d[i].append(pd.DataFrame(pywt.waverec(coeff_list, w)))
        
df3 = pd.DataFrame()
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][0]], axis=1)
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][1]], axis=1) 
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][2]], axis=1)
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][3]], axis=1) 
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][4]], axis=1) #INGAT rec_a dan rec_i perlu diganti
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][5]], axis=1) 
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][6]], axis=1)
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][7]], axis=1)
for i in range (2160):
        df3=pd.concat([df3,rec_d[i][8]], axis=1)
for i in range (2160):
        df3=pd.concat([df3,rec_a[i][8]], axis=1) 
end = time.time()

a=glob.glob(r'E:\MAGISTER\DATA\ANALISIS\POTONG DATA\A\A*.txt')
b=glob.glob(r'E:\MAGISTER\DATA\ANALISIS\POTONG DATA\I\I*.txt')
a.sort()
b.sort()
from itertools import product
#L = ['D1 A','D1 I','D2 A','D2 I','D3 A','D3 I','D4 A','D4 I','D5 A','D5 I','D6 A','D6 I','A6 A','A6 I']
#k = [len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b)]
L = ['D1 A','D1 I','D2 A','D2 I','D3 A','D3 I','D4 A','D4 I','D5 A','D5 I','D6 A','D6 I','D7 A','D7 I','D8 A','D8 I','D9 A','D9 I','A9 A','A9 I']
k = [len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b),len(a),len(b)]
kolom = []
for i in range (len(L)):
    L2 = range(1, k[i]+1)
    kolom = kolom+[L[i]+ str(y) for y in L2]
df3.columns=kolom
df3
kolom = []
for i in range (len(L)):
    L2 = range(1, k[i]+1)
    kolom = kolom+[L[i]+ str(y) for y in L2]
df3.columns=kolom
df3=df3.dropna()
df3.tail(20)
```
