# Raspicam
Raspberry Pi camera interface prototype to the Alcator C-Mod datasystem

This is the software that was used to initialize the webcam, store, modify and upload data
to the MDSplus dataservers at the MIT PSFC. The workflow depended on the proper installation
of MDSplus on a linux distribution (raspianOS mainly), which allowed for the typical linux
installation to be used.  The process worked as follows:

0) At beginning of day, raspicam.sh started the camera daemon/python scripts
1) init.py was run in the background polling for a camera-specific initialization call by
MDSplus
2) using raw-encoded data, the acq.py script was started with the shot number
3) The acquisition parameters were hardcoded into the acq.py script, which set the camera
to wait for a specific GPIO pin to go low
4) It acquired for a set period of time at set parameters, and stored the data as .h264
(This provided the greatest data throughput due to memory limitations)
5) The data was converted to YUV420 and the brightness was extracted (anal.py)
6) The datafile was moved locally for the MDSplus server
7) The MDSplus user pulled the data via scp from their raspberry pi workspace, and stored
the data in the SPECTRSCOPY tree (hardcoded per camera in raspicam_store.py) 

A more detailed explanation of the entire system can be found at my website: http://ianfaust.com/2017/07/07/Raspicam/
