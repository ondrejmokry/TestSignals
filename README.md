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

The set of signals was used before for evaluation in several publications:

- MOKRÝ, O.; MAGRON, P.; OBERLIN, T.; FÉVOTTE, C. Algorithms for audio inpainting based on probabilistic nonnegative matrix factorization. *SIGNAL PROCESSING*, 2022, no. 206, p. 1-10. ISSN: 1872-7557. [[ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0165168422004443)] [[arXiv preprint](https://arxiv.org/abs/2206.13768)] [[codes](https://github.com/ondrejmokry/InpaintingNMF)]
    
- MOKRÝ, O.; RAJMIC, P. Audio Inpainting: Revisited and Reweighted. *IEEE/ACM TRANSACTIONS ON AUDIO, SPEECH AND LANGUAGE PROCESSING*, 2020, no. 28, p. 2906-2918. ISSN: 2329-9290. [[IEEE Xplore](https://ieeexplore.ieee.org/document/9222235)] [[arXiv preprint](https://arxiv.org/abs/2001.02480)] [[codes](https://github.com/ondrejmokry/InpaintingRevisited)]

- MOKRÝ, O.; RAJMIC, P.; ZÁVIŠKA, P. Flexible framework for audio reconstruction. In *Proceedings of the International Conference on Digital Audio Effects (DAFx)*. Vienna: DAFx, 2020. p. 117-124. ISSN: 2413-6689. [[full text in proceedings](https://www.dafx.de/paper-archive/2020/proceedings/papers/DAFx2020_paper_34.pdf)] [[arXiv preprint](https://arxiv.org/abs/2004.11162)] [[codes](https://github.com/ondrejmokry/AudioReconstructionFramework)]

- MOKRÝ, O.; RAJMIC, P. *Reweighted l1 minimization for audio inpainting*. SPARS Workshop, Toulouse, France: 2019. [[full text at ResearchGate](https://www.researchgate.net/publication/344840708_Reweighted_l1_minimization_for_audio_inpainting)]

Please note that even though the mentioned publications include testing using the same clean signals, the gap positions might be slightly different due to minor evolution of the algorithm used to distribute the gaps.
Furthermore, a recorting of a wind ensemble was part of the experiments, but it was omitted in the present dataset in order to keep its single-instrument nature.
