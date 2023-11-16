# TestSignals

Repository with signals and masks used for testing and evaluation of audio inpainting methods. The following single-instrument recordings from the [EBU SQUAM database](https://tech.ebu.ch/publications/sqamcd) are available:
1. `a08_violin`
2. `a16_clarinet`
3. `a18_bassoon`
4. `a25_harp`
5. `a35_glockenspiel`
6. `a41_celesta`
7. `a42_accordion`
8. `a58_guitar_sarasate`
9. `a60_piano_schubert`

All the signals are sampled at 44.1 kHz. Then, we consider gap lengths from 10 ms up to 80 ms, and create 10 gaps in each signal at pseudo-random locations.

For the following examples of loading the data, let's choose the violin signal (number 1) and gap length 20 ms.

## Loading data in Matlab

### Using Matlab table

For loading the mask, the first argument is "mask" + length in miliseconds,
the second argument is the signal name.

For the clean signal, the first argument is "clean".

    load("gaps_table.mat")
    clean_signal = gaps_table.("clean"){"a08_violin"};
    mask = gaps_table.("mask20"){"a08_violin"};

### Using struct

For loading the mask, the first argument is signal number (starting from 1 as above),
the second argument is "mask" + length in miliseconds.

For the clean signal, the second argument is "clean".

    load("gaps_struct.mat")
    clean_signal = gaps_struct(1).("clean");
    mask = gaps_struct(1).("mask20");

## Loading data in Python using SciPy

For loading the mask, the first argument is the file name "gaps_struct",
the second argument is "mask" + length in miliseconds,
the third argument is the signal number (starting from 0).
The last argument is always 0 to deal with the data structure.

For the clean signal, the second argument is "clean".

    import scipy.io as sio
    gaps_sio = sio.loadmat("gaps_struct.mat")
    clean_signal = gaps_sio["gaps_struct"]["clean"][0, 0]
    mask = gaps_sio["gaps_struct"]["mask20"][0, 0]

# Previous use

The set of signals was used before for evaluation in several publications.
