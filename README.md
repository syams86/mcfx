mcfx - multichannel cross plattform audio plug-in suite
==============

- mcfx is a suite of multichannel vst plug-ins or standalone applications (standalone currently meter and convolver only)

- channel count is configurable with compile time flag

- cross plattform VST for MacOSX, Windows and Linux

- uses the JUCE framework (www.juce.com, GPLv3), libsoxr (LGPL, http://soxr.sourceforge.net)

- ready to use binaries for MacOSX (> 10.5, 32/64 bit) and Windows (32/64 bit) can be found at http://www.matthiaskronlachner.com/?p=1910

- these plug-ins have been developed to be used with the ambiX Ambisonic plug-ins: http://www.matthiaskronlachner.com/?p=2015

license
--------------

mcfx is free software and licensed under the GNU General Public License version 3 (GPLv3).

prerequisites for building
--------------

- cmake, working build environment
- libsoxr for the convolver (http://soxr.sourceforge.net)

Install LINUX Libraries (Debian, Ubuntu):
*$ sudo apt-get install libasound-dev libfreetype6-dev libgl1-mesa-dev libx11-dev libxext-dev libxinerama-dev libxcursor-dev freeglut3-dev libxmu-dev libxi-dev*

howto build yourself:
--------------

- use cmake gui or cmake/ccmake from terminal:

- *NUM_CHANNELS* adjusts the number of input/output channels

**TERMINAL:**

- create a folder in the *mcfx* folder eg. *BUILD*

*mcfx/BUILD> $ ccmake ..*

- adjust NUM_CHANNELS 

then
*mcfx/BUILD> $ make*

- find the binaries in the *mcfx/BUILD/_bin* folder and copy to system VST folder

**VST installation folders:**


- MacOSX: /Library/Audio/Plug-Ins/VST or ~/Library/Audio/Plug-Ins/VST
- Windows: eg. C:\Programm Files\Steinberg\VstPlugins
- Linux: /usr/lib/lxvst or /usr/local/lib/lxvst

plug-ins explained:
==============

mcfx_convolver
--------------
multichannel convolution matrix
loads configuration files (compatible to jconvolver .conf files)
have a look at 'CONVOLVER_CONFIG_HOWTO.txt' for details about the configuration files
searches for configuration file in following folders:
		* Windows 7,8: C:\Users\username\AppData\Roaming\mcfx\convolver_presets\
		* MacOS: ~/Library/mcfx/convolver_presets/
		* Linux: ~/mcfx/convolver_presets/


mcfx_delay
--------------
delay each channel about the same time (maximum delay time in seconds is a compile time flag (default 0.5s): MAX_DELAYTIME_S)


mcfx_filter
--------------
filter each channel with the same low/high cut, peak filter and high/low shelf filter settings, frequency analyzer that displays a sum of all channels

low and high pass: 2nd order butterworth filter or 2x 2nd order butterworth cascaded (resulting in linkwitz riley characteristic) for use as x-over network
plus 2x parametric filter +- 18dB
plus low and high shelf filters +- 18dB


mcfx_gain_delay
--------------
set different delay time and gain setting for each channel (good for multispeaker calibration), includes a signal generator for testing individual channels
the GUI allows to paste a list of float gain and delay values from the clipboard with semicolon, comma, newline, tab or space separated.
maximum delay time in seconds is a compile time flag (MAX_DELAYTIME_S)

mcfx_meter
--------------

multichannel level meter with RMS, peak and peak hold


changelog:
==============
- 0.5.4 (2017-05-20) - mcfx_convolver and mcfx_filter: fixed threadsafety to avoid startup crash if other plugins use fftw

- 0.5.3 (2017-05-02) - mcfx_delay and mcfx_gain_delay fixed glitch in delayline

- 0.5.2 (2017-03-20) - various bugfixes; mcfx_convolver: performance optimizations, adjustable maximum partition size

- 0.5.1 (2016-04-25) - mcfx_convolver: fixed bug in loading packed (dense) matrix; mcfx_gain_delay gui fix

- 0.5.0 (2016-04-08) - add signal generator to mcfx_gain_delay; convolver: support for packed wav file to load a dense FIR matrix from only one .wav file -> have a look at CONVOLVER_CONFIG_HOWTO.txt; filter: smooth iir filter to avoid clicks when parameters change

- 0.4.2 (2016-02-19) - fixed one more convolver bug

- 0.4.1 (2016-02-17) - fixed convolver bug which resulted in mixed up partitions

- 0.4.0 (2015-11-04) - gui for mcfx_delay, gui for mcfx_filter (with fft analyzer), added phase, solo and mute buttons to mcfx_gain_delay

- 0.3.3 (2015-07-19) - performance improvements for mcfx_convolver
_
- 0.3.2 (2014-12-28) - audiomulch compatibility, gui for mcfx_gain_delay with paste from clipboard functionality, mcfx_meter added scale offset

- 0.3.1 (2014-06-16) - fixed vst id for bidule compatibility

- 0.3 (2014-03-15) - added mcfx_convolver

- 0.2 (2014-02-25) - removed some license incompatible code, juce update

- 0.1 (2014-01-10) - first release 

______________________________
(C) 2013-2017 Matthias Kronlachner
m.kronlachner@gmail.com
