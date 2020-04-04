# Semantics-Assisted Video Captioning Model Trained with Scheduled Sampling Strategy
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
![](https://img.shields.io/badge/VideoCaptioning-DeepLearning-orange)
![Github Watchers](https://img.shields.io/github/watchers/WingsBrokenAngel/Semantics-AssistedVideoCaptioning?color=brightgreen)
![GitHub stars](https://img.shields.io/github/stars/WingsBrokenAngel/Semantics-AssistedVideoCaptioning?color=brightgreen)
![GitHub forks](https://img.shields.io/github/forks/WingsBrokenAngel/Semantics-AssistedVideoCaptioning?color=brightgreen&label=Fork)
![License](https://img.shields.io/github/license/WingsBrokenAngel/Semantics-AssistedVideoCaptioning.svg?color=brightgreen&style=flat)
 
## Table of Contents
1. [Description](#description)
2. [Dependencies](#dependencies)
3. [Manual](#manul)
4. [Data](#data)
5. [Results](#results)
    1. [Comparison on Youtube2Text](#cy)
    2. [Comparison on MSR-VTT](#cm)
6. [Citation](#citation)

---
## <a name="description"></a> Description

This repo contains the code of Semantics-Assisted Video Captioning Model, based on the paper 
"[Semantics-Assisted Video Captioning Model Trained with Scheduled Sampling Strategy](https://arxiv.org/abs/1909.00121)". It is under review at *Frontiers in Robotics and AI*.


We propose three ways to improve the video captioning model. First of all, we utilize both spatial 
features and dynamic spatio-temporal features as inputs for semantic detection network in order
to generate meaningful semantic features for videos. Then, we propose a scheduled sampling 
strategy which gradually transfers the training phase from a teacher guiding manner towards
a more self teaching manner. At last, the ordinary logarithm probability loss function
is leveraged by sentence length so that short sentence inclination is alleviated. Our model
achieves state-of-the-art results on the Youtube2Text dataset and is competitive with the 
state-of-the-art models on the MSR-VTT dataset.



The overall structure of our model looks like this ![overall structure](https://github.com/WingsBrokenAngel/Semantics-AssistedVideoCaptioning/blob/master/photos/overall_framework.jpg).
Here is some captions generated by our model.
![captions](https://github.com/WingsBrokenAngel/Semantics-AssistedVideoCaptioning/blob/master/photos/captions.png)

---

If you need a newer and more powerful model, please refer to [Delving-Deeper-into-the-Decoder-for-Video-Captioning](https://github.com/WingsBrokenAngel/delving-deeper-into-the-decoder-for-video-captioning).

---
## <a name="dependencies"></a> Dependencies
* Python3.6
* TensorFlow 1.13
* NumPy
* sklearn
* pycocoevalcap(Python3)

---
## <a name="manual"></a> Manual
1. Make sure you have installed all the required packages.
2. Download [pycocoevalcap](https://github.com/Illuminati91/pycocoevalcap.git) and put it along with `msrvttt`, `msvd`, `tagging` folders.
3. Download files in the [Data section](#data).
4. `cd path_to_directory_of_model; mkdir saves`
5. `run_model.sh` is used for training models and `test_model.sh` is used for testing models.
 Specify the GPU you want to use by modifying `CUDA_VISIBLE_DEVICES` value. Specify the needed 
 data paths by modifying `corpus`, `ecores`, `tag` and `ref` values. The words will be sampled
 by argmax strategy if `argmax` is 1 and they will be sampled by multinomial strategy if `argmax`
 is 0. `name` is the name which you give to the model. `test` refers to the path of the saved model
 which is to be tested. Do not give a parameter to `test` if you want to train a model.
 6. After completing the configuration of the bash file, then `bash run_model.sh` for training, 
 `bash test_model.sh` for testing.

---
## <a name="results"></a> Results

### <a name="cy"></a> Comparison on Youtube2Text

| Model   | B-4      | C        | M        | R        |  Overall |
| :------ | :------: | :------: | :------: | :------: | :------: |
|LSTM-E   | 45.3     |          | 31.0     |          |          |
|h-RNN    | 49.9     | 65.8     | 32.6     |          |          |
|aLSTMs   | 50.8     | 74.8     | 33.3     |          |          |
|SCN      | 51.1     | 77.7     | 33.5     |          |          |
|MTVC     | 54.5     | 92.4     | 36.0     | 72.8     | 0.9198   |
|ECO      | 53.5     | 85.8     | 35.0     |          |          |
|SibNet   | 54.2     | 88.2     | 34.8     | 71.7     | 0.8969   |
|Our Model| **61.8** |**103.0** |**37.8**  |**76.8**  |**1.0000**|

### <a name="cm"></a> Comparison on MSR-VTT

| Model       | B-4      | C        | M        | R        |  Overall |
| :------     | :------: | :------: | :------: | :------: | :------: |
|v2t_navigator| 40.8     | 44.8     | 28.2     | 60.9     | 0.9325   |
|Aalto        | 39.8     | 45.7     | 26.9     | 59.8     | 0.9157   |
|VideoLAB     | 39.1     | 44.1     | 27.7     | 60.6     | 0.9140   |
|MTVC         | 40.8     | 47.1     | 28.8     | 60.2     | 0.9459   |
|CIDEnt-RL    | 40.5     | **51.7** | 28.4     | 61.4     | 0.9678   |
|SibNet       | 40.9     | 47.5     | 27.5     | 60.2     | 0.9374   |
|HACA         | 43.4     | 49.7     | **29.5** | 61.8     | 0.9856   |
|TAMoE        | 42.2     | 48.9     | 29.4     | 62.0     | 0.9749   |
|Our Model    | **43.8** | 51.4     | 28.9     | **62.4** |**0.9935**|

---
## <a name="data"></a> Data

### <a name="dmsvd"></a> MSVD
- [MSVD reference file](https://cloud.tsinghua.edu.cn/f/aafd02d8cf4f44529bbd/?dl=1)
    * MD5 9101af3b24c27e0c63b98ac55511d04c
    * SHA-1 3cd3b556c06e8f944f0f01ae8ac03a262dd0af04
- [MSVD ResNeXt ECO file](https://cloud.tsinghua.edu.cn/f/8f5dfba901a34f0eb474/?dl=1)
    * This is the video-level feature extracted by [ResNeXt101c64](https://github.com/taehoonlee/tensornets) and [Efficient Convolutional Network](https://github.com/mzolfaghari/ECO-efficient-video-understanding).
    * MD5 b4307b302f8d9754e6e7dac284da0625
    * SHA-1 a34ab8c1b3fc2ecfae43d454ddd3f6eddccbeb1a
- [MSVD Semantic tag file](https://cloud.tsinghua.edu.cn/f/d463a2eecc7645f3965d/?dl=1)
    * MD5 df5dd440bf6ad78a3266dfbf9018d01e
    * SHA-1 0fb63a3b381c56baf982bbb4fc46027f26a45b02
- [MSVD Corpus file](https://cloud.tsinghua.edu.cn/f/70b264998e4d40aeb1d6/?dl=1)
    * MD5 0161e1d3207f10f7e13f36a10ae81c4f
    * SHA-1 a57c184f80ab2962ffdee71391fc6692c9a42c4b
- [MSVD tag ground truth for MSVD tag model](https://cloud.tsinghua.edu.cn/f/a8149c864cf741039c0d/?dl=1)
    * MD5 e2d66ae3f2c28f25071c8ed4591ee9bb
    * SHA-1 351ed0f794ac4ff17ff96a7984a259b1843fa2f0
- [MSRVTT tag ground truth for MSVD tag model](https://cloud.tsinghua.edu.cn/f/d5ee9fd74cde47feb7d6/?dl=1)
    * The previous two files are used to train the tagging network.
    * MD5 d899e591940926fdbe97dd756a6b1cd8
    * SHA-1 4a8b7c72c2ba9e525ef5cdce27c61e4eff22bb5e
- [MSVD tag index2word and word2index mappings](https://github.com/zhegan27/SCN_for_video_captioning)
    * We use the same word-index mapping in semantic tag to the code in this link.
- [Video name to numerical index mapping file of MSVD](https://cloud.tsinghua.edu.cn/f/fb7b269de7964d56af82/?dl=1) 
    + data type: dict, each key is a video name and the corresponding value is the video index.
    + MD5 ee3ef82df50694db629297fd60fd7427
    + SHA-1 99240d9e91cb6378fded8a6702301e390ffc17fc 
- Model Checkpoint:
    + [meta](https://cloud.tsinghua.edu.cn/f/7e2a7d9947a94d7d9a07/?dl=1)
        * MD5 5d8a0510b20734cf58df9554fd421c50
        * SHA-256 b3ce468e35cab0b409b6de8379fe4db89a439756ca9a33f16e4724b245c3174b
    + [index](https://cloud.tsinghua.edu.cn/f/86c1f4d1d4154c09991c/?dl=1)
        * MD5 0867cdf66639e9f6fc1f5d1c78b7d05e
        * SHA-256 462ca7467593393e28f211fb2554e34f80c23e2e3d8e1f49668530064cb7abae
    + [data-00000-of-00001](https://cloud.tsinghua.edu.cn/f/7c94ed922e204fc090d3/?dl=1)
        * MD5 1c3a83f1c9a0a38e30d4ab22af77377d
        * SHA-256 caeaf341f86599c4acef0a67d893f040fa0d287dde8cac7db70bb3e24a10b68f

### <a name="dmsrvtt"></a> MSRVTT
- [MSRVTT reference file](https://cloud.tsinghua.edu.cn/f/5c5d25edacae415fa0bf/?dl=1)
    * MD5 2ca68300ab2440ab0f6972ea12a0f323
    * SHA-1 024be7b58fd26c5add388e42210170484f0e86cf
- [MSRVTT ResNeXt ECO file](https://cloud.tsinghua.edu.cn/f/8ecb879d77db41b2b06c/?dl=1)
    * This is the video-level feature extracted by 
    [ResNeXt101c64](https://github.com/taehoonlee/tensornets) and 
    [Efficient Convolutional Network](https://github.com/mzolfaghari/ECO-efficient-video-understanding).
    * MD5 d0f05df7d113e4914ab9981d03c7dc70
    * SHA-1 258e3e92462469dbaf97808f2ca1eb8369f0930b
- [MSRVTT Semantic tag file](https://cloud.tsinghua.edu.cn/f/07158bab9f7a4ba3918b/?dl=1)
    * MD5 e41fd8fe8e198a6578c84db273ca8bd9
    * SHA-1 2129dccd7a67a3d56d803e9f4c032da9b7e81742
- [MSRVTT Corpus file](https://cloud.tsinghua.edu.cn/f/97cb4f640f194731a550/?dl=1)
    * MD5 eba8f53dc1fc1f91bc1d434326964366
    * SHA-1 5a63a2d4215b6894cb6d8c9319c133896ece3ea2
- [MSVD tag ground truth for MSRVTT tag model](https://cloud.tsinghua.edu.cn/f/5d411b6e16f64da58bb5/?dl=1)
    * MD5 c9ce9007ef754338d89e40018d14c923
    * SHA-1 03719c1324f9299a510c8c380352b9f4b7125878
- [MSRVTT tag ground truth for MSRVTT tag model](https://cloud.tsinghua.edu.cn/f/831616470b344dec9de0/?dl=1)
    * The previous two files are used to train the tagging network.
    * MD5 e7d6defa3278bc91ecd7dcbdbda16649
    * SHA-1 2eea2721fcf744d8e42b6ef95c1e2b481534c5aa
- [MSRVTT tag word2index and index2word](https://cloud.tsinghua.edu.cn/f/ea0c962bfca147d6bdbb/?dl=1)
    * This file contains word-to-index mapping and index-to-word mapping.
    * SHA-256 50b00cebb12a38c0c4a546c577c99c12e97c8961b4f2ce9472b77d4ad05e1226
- Model Checkpoint:
    + [meta](https://cloud.tsinghua.edu.cn/f/cd66aab5dacb4f228aa0/?dl=1)
        * MD5 cc4e6775bf0eec75b06e6e6fecfd5eb6
        * SHA-256 f0e1cca6d4186756b6a7f062a0a9824357fe1d37dfb984ad09ceda2a7db01fac
    + [index](https://cloud.tsinghua.edu.cn/f/e9c5d2fc4ab8461595ce/?dl=1)
        * MD5 0da1d37d62ca514c9b31f6c8fced4559
        * SHA-256 ab6f16f94b91d824b8777dda40a67770e0d73b548f556d1f6c169a7862fb3906
    + [data-00000-of-00001](https://cloud.tsinghua.edu.cn/f/0af43c801cfd4be7bb9d/?dl=1)
        * MD5 5f28126cc6a2e38fe7919715cbc4bb7e
        * SHA-256 74ad87644a9380ef8fca0f2beee85e0ba87a9bfe20e05e4e93dfe4d876a7f167
- MSR-VTT Dataset:
	- [train_val_test_annotation.zip](https://cloud.tsinghua.edu.cn/f/19979e0c71e34988b440/?dl=1)
		- SHA-256: ce2d97dd82d03e018c6f9ee69c96eb784397d1c83f734fdb8c17aafa5e27da31
	- [msr-vtt-v1.part1.rar](https://cloud.tsinghua.edu.cn/f/5b52ddbf9ad8400c8825/?dl=1)
		- SHA-256: 3445e0d1bffda3739110dfcf14182b63222731af8a4d7153f0ac09dbec39a0d3
	- [msr-vtt-v1.part2.rar](https://cloud.tsinghua.edu.cn/f/0d20582e783d447ab96e/?dl=1)
		- SHA-256: b550997526272ab68a42f1bd93315aa2bbb521c71f33d0cb922fbbfb86f15aae
	- [msr-vtt-v1.part3.rar](https://cloud.tsinghua.edu.cn/f/28d799c95d3a47a4aed9/?dl=1)
		- SHA-256: debbd0e535e77d9927ffb375299c08990519e22ba7dac542b464b70d440ef515

### <a name="deco"></a>ECO
- [ECO_full_kinetics.caffemodel](https://cloud.tsinghua.edu.cn/f/fbc0d5879d2c4ab8ab81/?dl=1)
    + MD5 31ed18d5eadfd59cb65b7dcdadc310b4
    + SHA-1 b749384d2dac102b8035965566e3030fce465c20

---
## <a name="citation"></a> Citation

    @ARTICLE{2019arXiv190900121C,
           author = {{Chen}, Haoran and {Lin}, Ke and {Maye}, Alexander and {Li}, Jianming and
             {Hu}, Xiaolin},
            title = "{A Semantics-Assisted Video Captioning Model Trained with Scheduled Sampling}",
          journal = {arXiv e-prints},
         keywords = {Computer Science - Computer Vision and Pattern Recognition, Computer Science - Computation and Language},
             year = "2019",
            month = "Aug",
              eid = {arXiv:1909.00121},
            pages = {arXiv:1909.00121},
    archivePrefix = {arXiv},
           eprint = {1909.00121},
     primaryClass = {cs.CV},
           adsurl = {https://ui.adsabs.harvard.edu/abs/2019arXiv190900121C},
          adsnote = {Provided by the SAO/NASA Astrophysics Data System}
    }

