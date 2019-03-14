# Tmask

This software called Tmask (multiTemporal mask) is used for automated clouds, cloud shadows, and snow masking for Landsat 4-8 images based on time series analysis. Please contact Zhe Zhu (zhe@uconn.edu) at Department of Natural Resources and the Environment, University of Connecticut if you have any questions. 

Please cite the following paper: Zhu, Z. and Woodcock, C. E., Automated cloud, cloud shadow, and snow detection based on multitemporal Landsat data: an algorithm designed specifically for monitoring land cover change, Remote Sensing of Environment (accepted), doi:10.1016/j.rse.2014.06.012 (This paper explains the 1.0 version of Tmask in great details).

Please note that this algorithm is very time consuming. For example, to provide cloud, cloud shadow, and snow masks for all sample images (33 Landsat images), it may take approximately 20 CPU hours! Running on the high performance computing server is suggested.

After running Fmask, there will be an image called XXXTmask that can be opened by ENVI. The image values are presenting the following classes:

0 => clear land pixel

1 => clear water pixel

2 => cloud shadow

3 => snow

4 => cloud

255 => no observation

# 1.0 Version
This algorithm provide better results than Fmask and is based on the Fmask results and time series analysis.

Before using this Tmask algorithm, there are many works need to be done. First, you need to convert the three Landsat bands (Band 2, 4, and 5 - Landsat 7 numbering) into TOA reflectance. Second, you need to run Fmask algorithm for each Landsat images. Third, you need to stack the three TOA bands and Fmask band together into the same biq image file (ENVI format) in the ordering of TOA Band 2, 4, 5, and Fmask result. Fourth, put each stack file and original metadata into the same folder (each folder contain one Landsat images). Finally, resample all the stacked images into the same dimension and same upper-left corner (make images comparable) as the first image. Then you are able to run Tmask for as many images as you want.

There are some sample stacked data prepared for Tmask algorithm located at: http://ftp-earth.bu.edu/public/zhuzhe/Tmask/data/

Matlab code
Need Matlab environment and toolboxes and can be run on any 64bits machine (PC, Mac, Linux) with 4G+ memory. 

You can download the Matlab code [here]: (https://www.dropbox.com/sh/4qjcihruku5bou6/AAAEdsQUdzirVFmyEqpkZLRsa?dl=0)

Linux Executable
Stand alone Linux executable Fmask software which do not need to install Matlab or R and runs on Linux 64 bits machine with 4G+ memory. Please use the following steps:

1. Download Tmask 1.0 version Linux package "Tmask_pkg.zip" Use any Brosweer and go to the following [ftp sites]: (http://ftp-earth.bu.edu/public/zhuzhe/Tmask/Tmask_Linux_1.0v/)

2. Unzip the software using "unzip Tmask_pkg.zip"

3. There will be a new file called MCRInstaller.zip at the same folder and unzip this file.

4. Install MCRInstaller by typing "./install" in the same folder

5. There will be wizard that help you install and there will be two environment variables called "LD_LIBRARY_PATH" and "XAPPLRESDIR" showed up in the wizard. Copy the two variables.

For example, This is what I got:

"On the target computer, append the following to your LD_LIBRARY_PATH environment variable:

/home/amd64

Next, set the XAPPLRESDIR environment variable to the following value:

/home/app-defaults"

6. Edit your .cshrc (.tcsh is the same, for .bash replace it with export LD_LIBRARY_PATH="...") file and add this

"setenv LD_LIBRARY_PATH /home/amd64"

"setenv XAPPLRESDIR /home/app-defaults"

7. Save the shell or bash script and source it;

8. Copy the "Tmask" software to any location you want (for example "/Tools/Tmask");

9. cd into the folder where all the folders of Landsat data are stored and run Tmask by entering "/Tools/Tmask stk_n" in the terminals. Wait a few seconds you will be able to see both robust fit percent and Tmasking.

There are 7 important tuning variables that you can play with:

1) "stk_n" is the stack image file name (such as "TOAstack").

2) "n_start" is the number of the first image you want to have Tmask processed (default value of 1).

3) "n_end" is the number of the last image you want to have Tmask processed (default value of the total number of folders with name start as L)

4) "T_times" is the threshold used for detecting cloud, cloud shadow, and snow (default value of 400).

5) "bufcd" is buffered number of pixels for cloud (default value of 3).

6) "bufsd" is buffered number of pixels for cloud shadow (default value of 3).

7) "bufsn" is buffered number of pixels for snow (default value of 0).

You can use "/Tools/Tmask stk_n n_start n_end T_times bufcd bufsd bufsn", for example "/Tools/Tmask TOAstack 1 33 400 3 3 0" in the terminals. Or if you want to use default values, you can use "/Tools/Tmask stk_n n_start n_end T_times", or "/Tools/Tmask stk_n n_start n_end", or "/Tools/Tmask stk_n".

Windows Executable
Stand alone Linux executable Tmask software which do not need to install Matlab or R and runs on Linux 64 bits machine with 4G+ memory. Please use the following steps:

1. Download Tmask 1.0 version Windows package "Tmask_pkg.exe" Use any Brosweer and go to the following [ftp sites]: (http://ftp-earth.bu.edu/public/zhuzhe/Tmask/Tmask_Windows_1.0v/)

2. Double click "Tmask_pkg.exe" and install it with wizard.

3. There will be a new file called "Tmask.exe" at the same folder and this is your Tmask software

4. Copy the "Tmask.exe" software to any location you want (for example "c:\Tools");

5. In the Command Prompt Window (enter cmd in the start menu), cd into the folder where all the folders of Landsat data are stored and run Tmask by entering "c:\Tools\Tmask stk_n". Wait a few seconds you will be able to see both robust fit percent and Tmasking.

There are 7 important tuning variables that you can play with:

1) "stk_n" is the stack image file name (such as "TOAstack").

2) "n_start" is the number of the first image you want to have Tmask processed (default value of 1).

3) "n_end" is the number of the last image you want to have Tmask processed (default value of the total number of folders with name start as L)

4) "T_times" is the threshold used for detecting cloud, cloud shadow, and snow (default value of 400).

5) "bufcd" is buffered number of pixels for cloud (default value of 3).

6) "bufsd" is buffered number of pixels for cloud shadow (default value of 3).

7) "bufsn" is buffered number of pixels for snow (default value of 0).

You can use "/Tools/Tmask stk_n n_start n_end T_times bufcd bufsd bufsn", for example "c:\Tools\Tmask TOAstack 1 33 400 3 3 0" in the terminals. Or if you want to use default values, you can use "c:\Tools\Tmask stk_n n_start n_end T_times", or "c:\Tools\Tmask stk_n n_start n_end", or "c:\Tools\Tmask stk_n".
