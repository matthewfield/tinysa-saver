This is a PyQt6 fork of Erik Kaashoek's tinysa-saver for TinySA. It is pretty much impossible to get PyQt5 to install alongside any of the newer versions of Python, so I gave up and ported to PyQt6 instead. This works with Python 3.11


TinySASaver
============
A multiplatform tool to save scans from the TinySA, sweep frequency spans in segments to gain more than
290 data points, and generally display and analyze the resulting data.

Copyright 2019 Rune B. Broberg, 2020 Erik Kaashoek, 2023 Matthew Field

## Introduction
This software connects to a TinySA and extracts the data for display on a computer, and for saving to Touchstone files.

Current features:
- Reading data from a TinySA
- Splitting a frequency range into multiple segments to increase resolution (tried up to >10k points)
- Averaging data for better results particularly at higher frequencies
- Displaying data on multiple chart types, such as Smith, LogMag, Phase and VSWR-charts, for both S11 and S21
- Displaying markers, and the impedance, VSWR, Q, equivalent capacitance/inductance etc. at these locations
- Displaying customizable frequency bands as reference, for example amateur radio bands
- Exporting and importing 1-port and 2-port Touchstone files
- TDR function (measurement of cable length) - including impedance display
- Filter analysis functions for low-pass, high-pass, band-pass and band-stop filters
- Display of both an active and a reference trace
- Live updates of data from the TinySA, including for multi-segment sweeps
- In-application calibration, including compensation for non-ideal calibration standards
- Customizable display options, including "dark mode"
- Exporting images of plotted values

0.1.4:
![Screenshot of version 0.1.4](https://i.imgur.com/ZoFsV2V.png)

## Running the application

Python 3.11 with modules PyQT6, numpy, scipy and pyserial.

#### Installation and Use with pip

1. Clone repo and cd into the directory

        git clone https://github.com/matthewfield/tinysa-saver
        cd tinysa-saver

3. Run the pip installation

        pip3 install .

4. Once completed run with the following command

        TinySASaver
	
	
#### Installation and Use with virtualenv
Virtualenv - a tool for creating isolated 
virtual python environments

The benefits of using virtualenv - absolutely isolated environment, 
you can delete it - nothing will happen to the main system

1. Install ( if not exist ) 
```
python -m pip install --user virtualenv
python -m virtualenv --help
```

2. Creating Python3 virtual environment 
```
virtualenv tinysa
```

3. Install requirements
```
tinysa/bin/pip3 install -r requirements.txt
```

4. Run the code
```
tinysa/bin/python3 tinysa-saver.py
```

	
	

### Linux
#### Ubuntu 18.04 & 19.04
##### Installation and Use with pip
1. Install python3.11 and pip

        sudo apt install python3.7 python3-pip

3. Clone repo and cd into the directory 
		
        git clone https://github.com/matthewfield/tinysa-saver
        cd tinysa-saver

4. Run the pip installation

        python3.11 -m pip install .
    
    (You may need to install the additional packages python3-distutils, python3-setuptools and python3-wheel for this command to work on some distributions.)
    
5. Once completed run with the following command

        python3.11 tinysa-saver.py
    
    
### Mac OS:
#### Homebrew
1. Install Homebrew
		From : https://brew.sh/

	     /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

2. Python :

        brew install python

3. TinySASaver Installation

        git clone https://github.com/matthewfield/tinysa-saver
        cd tinysa-saver
        
4. Install local pip packages

        python3 -m pip install .
        TinySASaver

## Using the software

Connect your TinySA to a serial port, and enter this serial port in the serial port box.  If the TinySA is
connected before the application starts, it should be automatically detected. Otherwise, click "Rescan". Click
"Connect to TinySA" to connect.

The app can collect multiple segments to get more accurate measurements. Enter the number of segments to be done in the
"Segments" box. Each segment is 101 data points, and takes about 1.5 seconds to complete.

Frequencies are entered in Hz, or suffixed with k or M.  Scientific notation (6.5e6 for 6.5MHz) also works.

Markers can be manually entered, or controlled using the mouse. For mouse control, select the active marker using the
radio buttons, or hold "shift" while clicking to drag the nearest marker. The marker readout boxes show the actual
frequency where values are measured.  Marker readouts can be hidden using the "hide data" button when not needed.

Display settings are available under "Display setup". These allow changing the chart colours, the application font size
and which graphs are displayed.  The settings are saved between program starts.

### Calibration
_Before using TinySA-Saver, please ensure that the device itself is in a reasonable calibration state._ A calibration
of both ports across the entire frequency span, saved to save slot 0, is sufficient.  If the TinySA is completely
uncalibrated, its readings may be outside the range accepted by the application.

In-application calibration is available, either assuming ideal standards, or with relevant standard correction. To
manually calibrate, sweep each standard in turn, and press the relevant button in the calibration window. For assisted
calibration, press the "Calibration assistant" button.  If desired, enter a note in the provided field describing the
conditions under which the calibration was performed.

Calibration results may be saved and loaded using the provided buttons at the bottom of the window.  Notes are saved
and loaded along with the calibration data.

![Screenshot of Calibration Window](https://i.imgur.com/p94cxOX.png)

Users of known characterized calibration standard sets can enter the data for these, and save the sets.

After pressing _Apply_, the calibration is immediately applied to the latest sweep data.

_Currently, load capacitance is unsupported_

### TDR
To get accurate TDR measurements, calibrate the device, and attach the cable to be measured at the calibration plane -
ie. at the same position where the calibration load would be attached.  Open the "Time Domain Reflectometry" window, and
select the correct cable type, or manually enter a propagation factor.

### Frequency bands
Open the "Display setup" window to configure the display of frequency bands. By clicking "show bands", predefined
frequency bands will be shown on the frequency-based charts.  Click manage bands to change which bands are shown, and
the frequency limits of each.  Bands default and reset to European amateur radio band frequencies.

## License
This software is licensed under version 3 of the GNU General Public License. It comes with NO WARRANTY.

You can use it, commercially as well. You may make changes to the code, but I (and the license) ask that you give these
changes back to the community.

See https://github.com/erikkaashoek/tinysa-saver for other documentation
