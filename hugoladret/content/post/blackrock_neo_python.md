+++
author = "Hugo Ladret"
title = "Extracting data from Blackrock files in Python #ephys #code"
date = "2023-04-17"
description = """ 'People are so into digital recording now they forgot how easy analog recording can be.' > Dave Grohl
"""
tags = [

]
+++

<!--more-->
# The problem
Recently, I've had the pleasure to get some data from to the very talented [Paolo Papale](https://scholar.google.ca/citations?user=5kBTdH0AAAAJ&hl=fr&oi=ao) working in [Pieter Roelfsema's lab](https://nin.nl/research-groups/roelfsema/). Both of them kindly sent me some electrophysiological data from their Utah array recordings. Their massively parallel recordings (about [1000 recording sites in visual cortices](https://www.researchgate.net/publication/359161666_1024-channel_electrophysiological_recordings_in_macaque_V1_and_V4_during_resting_state)) are acquired and digitized through a Blackock Neurotech board that outputs the data in a proprietary [.nev format](https://blackrockneurotech.com/research/wp-content/ifu/LB-0023-7.00_NEV_File_Format.pdf).

Rather than bother them for access to properitary tools or in-house solutions, I wanted to play around with the data on my own

# The solution
A very simple solution relies on the brillant [Python NEO package](https://github.com/NeuralEnsemble/python-neo). It becomes trivially simple to load data with their BlackRock I/O interface :
```python
import numpy as np
import os
from neo.rawio import BlackrockRawIO
import time

recording_path = './path_to_recording/path_to_subfolder'
now = time.time()

print('> Loading array : %s/instance1_B001.nev . . .' % (recording_path))
reader = BlackrockRawIO(filename= '%s/instance1_B001.nev' % (recording_path))
reader.parse_header()

print('Getting analog signals . . .')
signals = reader.get_analogsignal_chunk(block_index=0, seg_index=0, i_start=None, i_stop=None, channel_indexes=None)
signals = signals[:,0:128] #  here an instance has 144 channels, but the last 16 are not signals

print('Writing to disk . . . ')
if os.path.isfile('./raw_array_1.bin') : os.remove('./raw_array_1.bin') # better safe than sorry
with open ('./raw_array_1.bin' % instance,'wb') as FileToWrite:
    signals.tofile(FileToWrite)

print('Total time : %s' % (time.time() - now))
```
which gives a .bin file that can easily be loaded for further processing, for example using Kilosort for spike sorting.

Simple as that ! For a .nev file of half a gigabyte, it takes less than a minute on a modern setup to convert everything to a bin file.
