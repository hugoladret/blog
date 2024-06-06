+++
author = "Hugo Ladret"
title = "[ephys] [code] Extracting data from Blackrock files in Python"
date = "2023-04-17"
description = """ 'People are so into digital recording now they forgot how easy analog recording can be.' > Dave Grohl
"""
tags = [

]
+++

<!--more-->
# The problem
Recently, received data from the talented [Paolo Papale](https://scholar.google.ca/citations?user=5kBTdH0AAAAJ&hl=fr&oi=ao), working in [Pieter Roelfsema's lab](https://nin.nl/research-groups/roelfsema/). Electrophysiological data from Utah array recordings with massive parallel recordings (about [1000 recording sites in visual cortices](https://www.researchgate.net/publication/359161666_1024-channel_electrophysiological_recordings_in_macaque_V1_and_V4_during_resting_state)), digitized via Blackrock Neurotech board, output in proprietary [.nev format](https://blackrockneurotech.com/research/wp-content/ifu/LB-0023-7.00_NEV_File_Format.pdf).

Rather than request proprietary tools, better to process data independently.

# The solution
Simple solution, using the brilliant [Python NEO package](https://github.com/NeuralEnsemble/python-neo). Loading data with BlackRock I/O interface becomes trivial:
```
python
import numpy as np
import os
from neo.rawio import BlackrockRawIO
import time

recording_path = './path_to_recording/path_to_subfolder'
now = time.time()

print('> Loading array: %s/instance1_B001.nev . . .' % (recording_path))
reader = BlackrockRawIO(filename='%s/instance1_B001.nev' % (recording_path))
reader.parse_header()

print('Getting analog signals . . .')
signals = reader.get_analogsignal_chunk(block_index=0, seg_index=0, i_start=None, i_stop=None, channel_indexes=None)
signals = signals[:, 0:128]  # Here, instance has 144 channels, but last 16 are not signals

print('Writing to disk . . .')
if os.path.isfile('./raw_array_1.bin'): os.remove('./raw_array_1.bin')  # Better safe than sorry
with open('./raw_array_1.bin', 'wb') as FileToWrite:
    signals.tofile(FileToWrite)

print('Total time: %s' % (time.time() - now))
```

Produces a .bin file, easily loaded for further processing, e.g., using Kilosort for spike sorting.\
Simple, efficient. For a 500mb .nev file, conversion takes less than a minute.