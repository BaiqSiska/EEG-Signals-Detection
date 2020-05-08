Decomposition
===
EEG signals that have been cut will be processed again into some sub-bands of signals which are often called the signal decomposition process. The EEG signals decomposition process, in this case, uses the Wavelet Transform (WT) method, especially the Discrete Wavelet Transform. EEG signal decomposition was done before doing the feature extraction process. This process will decompose the signal into low and high sub-signals. The high signal will be eliminated and the low signal will be decomposed again into two slices, it is a level decomposition process.
Below is the illustration of the decomposition signal in 7th level.

![Screenshot from 2020-05-08 09-57-35](https://user-images.githubusercontent.com/10173320/81365498-79f8aa80-9112-11ea-9d08-ed0fb65d2ed5.png)

Descrete Wavele Transform (DWT)
---

```
import pandas as pd
import numpy as np
```
menyatukan semua potongan sinyal
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
proses dekomoposisi sinyal dengan DWT level 6
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
