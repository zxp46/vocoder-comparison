### Vocoder Review

This is a simple review of five popular vocoder models: **MelGAN**, **HifiGAN**, **WaveGlow**, **WaveFlow**, Neural Harmonic Vocoder (**NHV**). Groudtruth audios and WaveNet are taken are baseline.

#### Audio quality on LJSpeech (Single woman speaker):

##### My result

All models except WaveFlow have exellent performance, while there's some echo from WaveFlow. It may be caused by imperfect implementation, as comparing the pretrained model (unofficial) with official audios samples, quality of the same sentence varies.

##### Comparing with data offered in papers

| MelGAN                                      | HifiGAN                                                  |
| ------------------------------------------- | -------------------------------------------------------- |
| 3.61 (GT 4.52, WaveGlow 4.11, WaveNet 4.05) | 4.23 (GT 4.45, MelGAN 3.79, WaveGlow 3.81, WaveNet 4.02) |

| WaveGlow                      | WaveFlow                                   |
| ----------------------------- | ------------------------------------------ |
| 3.96 ( GT 4.27, WaveNet 3.85) | 4.38 (GT 4.56, WaveGow 4.34, WaveNet 4.43) |

Results are consistent in all papers: HifiGAN > WaveNet > WaveFlow > WaveGlow > MelGAN

#### Audio quaulity on VCTK (Multigender multi speaker, a dirty data set)

##### My result

MelGAN and HifiGAN have the best performance, followed by WaveFlow and WaveGlow. GAN models outperform flow models on a dirty data set.

No data are offered by the original papers.

#### Training Speed

##### My result

$MelGAN \approx NHV \approx Wavenet > WaveGlow > WaveFlow > HifiGAN$

Training speed is mostly proportional to the model size.

No data are offered by the original papers.

#### Synthesis Speed

##### My result

MelGAN > HifiGAN > NHV > WaveGlow > WaveFlow > Wavenet

$3:4:6:37:43:100000$

GAN models are the fastest, as they only need generator while synthesizing (about 5 M parameters). NHV is also fast due to its special structure. Flow models are slower, as they need to reverse the whole model while synthesizing. WaveGlow is a little faster, as the synthesizing process can be done in parallel. WaveFlow is in series, however it duplicated the 1*1 convolution layer to make it faster. Wavenet is the slowest, as it's generated frame by frame.

##### Comparing with data offered in papers

| MelGAN                              | HifiGAN                                           |
| ----------------------------------- | ------------------------------------------------- |
| 2500 (WaveGlow 223, WaveNet 0.0787) | 16863 (MelGAN 14238, WaveGlow 3.81, WaveNet 0.07) |

| WaveGlow      | WaveFlow                              |
| ------------- | ------------------------------------- |
| Not specified | 21.32 (WaveGow 34.69， WaveNet 0.002) |

Consistent with my results, except that HifiGAN claims to be faster than MelGAN. This could be caused by implementation (The code I use for MelGAN has the spectrum preprocessed, while HifiGAN doesn't).

#### Sample audios

Available on SoundCloud

wavenet+lj

https://soundcloud.com/zmf876ofoicg/sets/wavenet-ljspeech?si=5aef9df223d140d7b28f55067c17c9cb

Hifigan + lj

https://soundcloud.com/zmf876ofoicg/sets/ljspeech-with-hifigan?si=e5002c4682c44471a9117547b564d0b0

MelGAN + lj

https://soundcloud.com/zmf876ofoicg/sets/ljspeech-with-melgan?si=516812e51da34e3c81303a3e67959864

WaveFlow + lj

https://soundcloud.com/zmf876ofoicg/sets/ljspeech-waveflow?si=516812e51da34e3c81303a3e67959864

GroudTruth + lj

https://soundcloud.com/zmf876ofoicg/sets/ljspeech-groundtruth?si=516812e51da34e3c81303a3e67959864

WaveGlow + lj

https://soundcloud.com/zmf876ofoicg/sets/waveglow-lj?si=516812e51da34e3c81303a3e67959864

VCTK + GT

https://soundcloud.com/zmf876ofoicg/sets/vctk-groudtruth?si=516812e51da34e3c81303a3e67959864

VCTK + MelGAN

https://soundcloud.com/zmf876ofoicg/sets/vctk-melgan?si=516812e51da34e3c81303a3e67959864

VCTK + HifiGAN

https://soundcloud.com/zmf876ofoicg/sets/vctk-hifigan?si=516812e51da34e3c81303a3e67959864

VCTK + WaveGlow

https://soundcloud.com/zmf876ofoicg/sets/vctkwaveglow?si=516812e51da34e3c81303a3e67959864

VCTK + WaveFlow

https://soundcloud.com/zmf876ofoicg/sets/vctk-waveflow?si=516812e51da34e3c81303a3e67959864

#### Code sources

MelGAN (unofficial implementation): https://github.com/kan-bayashi/ParallelWaveGAN

HifiGAN: https://github.com/jik876/hifi-gan

WaveGlow: https://github.com/NVIDIA/waveglow

WaveFlow (unofficial implementation): https://github.com/L0SG/WaveFlow

WaveNet: https://github.com/r9y9/wavenet_vocoder

NHV: Unpublished code from Zhijun Liu (original author)

Thanks a lot to the authors!