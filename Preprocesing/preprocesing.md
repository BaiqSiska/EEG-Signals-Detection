**Signal Preprocesing**
===
The signal preprocessing stage is the initial stage undertaken to obtain new data used in the classification process. EEG signals have a duration of 30 minutes truncated to two seconds. The signal used for research is a signal has the characteristics of muscle signals and ictal. The EEG signal is cut off for two seconds because the muscle signals have a very short duration. Therefore, in this case, the signal is cut off for only two seconds. Muscle artifact signals often occur in Fp1, Fp2, F4 and F8 channels. The process of cutting the EEG signal as follows.
1) prepare your app EEG signals.
2) Please choose one object who will investigate.
3) Please change a montage to Cz.
4) Furthermore, Please export your data to CSV or text.
5) Please, signals were cut out based on doctor's notes.
6) Hereafter make sure your note is correct. Base on your note, you can be made a script for cutting signals automatic where I did that with a Python program.
