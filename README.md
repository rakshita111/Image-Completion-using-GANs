The existing work on Image Inpainting [PEN-Net](https://github.com/researchmm/PEN-Net-for-Inpainting/blob/master/docs/PEN-Net.gif?raw=true) is improved by adding the [Spatial Pyramid Attentive Pooling](https://arxiv.org/abs/1901.06322) Module at the encoder.

<!-- ------------------------------------------------------------------------------ -->
## Introduction 
The spatial pyramid attentive pooling (SPAP) module used dilated convolution to capture the multi-scale information and further fuse the information from different levels of the pyramid through cascade attention. This is integrated with the PEN-Net in different ways to test for the improvement in the images generated. The SPAP module implemented in coarse-to-fine order is integrated at the multi-scale decoder and with the cross-layer attention transfer (ATN) at the encoder of PEN-Net separately. 

![PEN-Net_SPAP](https://github.com/rakshita111/Image-Completion-using-GANs/blob/main/docs/PEN-Net_SPAP.png?raw=true)



<!-- ------------------------------------------------------------------------------ -->
## Results 

![results](https://github.com/rakshita111/Image-Completion-using-GANs/blob/main/docs/generated_imgs.png)?raw=true)

Here are the results obtained on 256x256 images from DTD dataset where (a) Original image, (b) Masked image, (c) Original model output, (d) Original model with SPAP module at decoder, (e) Original model with SPAP module for attention layers

![table](https://github.com/rakshita111/Image-Completion-using-GANs/blob/main/docs/table.png?raw=true)



<!-- -------------------------------------------------------- -->
## Run 

0. Requirements:
    * Install python3.6
    * Install [pytorch](https://pytorch.org/) (tested on Release 1.1.0)
1. Training:
    * Prepare training images filelist [[our split]](https://drive.google.com/open?id=1_j51UEiZluWz07qTGtJ7Pbfeyp1-aZBg)
    * Modify [celebahq.json](configs/celebahq.json) to set path to data, iterations, and other parameters.
    * Our codes are built upon distributed training with Pytorch.  
    * Run `python train.py -c [config_file] -n [model_name] -m [mask_type] -s [image_size] `. 
    * For example, `python train.py -c configs/celebahq.json -n pennet -m square -s 256 `
2. Resume training:
    * Run `python train.py -n pennet -m square -s 256 `.
3. Testing:
    * Run `python test.py -c [config_file] -n [model_name] -m [mask_type] -s [image_size] `. 
    * For example, `python test.py -c configs/celebahq.json -n pennet -m square -s 256 `
4. Evaluating:
    * Run `python eval.py -r [result_path]`
  
<!-- ----------------------------------------------------- -->
## Reference

The code is majorly borrowed from [PEN-Net](https://github.com/researchmm/PEN-Net-for-Inpainting/blob/master/docs/PEN-Net.gif?raw=true). The images of the architecture is taken from [Learning Pyramid-Context Encoder Network for High-Quality Image Inpainting](https://arxiv.org/pdf/1904.07475.pdf?raw=true), [Learning Spatial Pyramid Attentive Pooling in Image Synthesis and
Image-to-Image Translation](https://arxiv.org/abs/1901.06322) and modified. 
