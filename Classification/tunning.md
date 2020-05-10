                                                  Kernel Linear
 ```
import time
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split, StratifiedKFold, GridSearchCV
from sklearn import svm
def svc_param_selection(X, y, nfolds):
    Cs = [0.001, 0.01,0.025, 0.1, 0.5, 1, 10, 10,100]
    param_grid = {'C': Cs}
    grid_search = GridSearchCV(svm.SVC(kernel='linear'), param_grid, cv=nfolds)
    grid_search.fit(X, y)
    grid_search.best_params_
    return grid_search.best_params_
 ```
                                                  Kernel RBF
 ```
 def svc_param_selection(X, y, nfolds):
    Cs = [0.001, 0.01,0.025, 0.1, 0.5, 1, 10, 10,100]
    gammas = [0.001, 0.01,0.025, 0.1, 0.5, 1, 10, 10,100]
    param_grid = {'C': Cs, 'gamma' : gammas}
    grid_search = GridSearchCV(svm.SVC(kernel='rbf'), param_grid, cv=nfolds)
    grid_search.fit(X, y)
    grid_search.best_params_
    return grid_search.best_params_
 ```
                                                  Kernel Poly
 ```
 def svc_param_selection(X, y, nfolds):
    Cs = [0.001, 0.01,0.025, 0.1, 0.5, 1, 10, 10, 100]
    Degrees = [0, 1, 2, 3, 4, 5, 6]
    param_grid = {'C': Cs, 'degree' : Degrees }
    grid_search = GridSearchCV(svm.SVC(kernel='poly'), param_grid, cv=nfolds)
    grid_search.fit(X, y)
    grid_search.best_params_
    return grid_search.best_params_
 ```
