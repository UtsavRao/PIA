# PIA：Personalized Image Animator

[**PIA: Your Personalized Image Animator via Plug-and-Play Modules in Text-to-Image Models**](https://arxiv.org/abs/2312.13964)








PIA is a personalized image animation method which can generate videos with **high motion controllability** and **strong text and image alignment**.

<img src="__assets__/image_animation/teaser/teaser.gif">

## What's New
 [ Demo & API](https://replicate.com/cjwbw/pia)!

 Third-party [Colab](https://github.com/camenduru/PIA-colab)!

PIA can animate a 1024x1024 image with just 16GB of GPU memory with `scaled_dot_product_attention`!





## Setup
### Prepare Environment

Use the following command to install Pytorch==2.0.0 and other dependencies:

```
conda env create -f environment-pt2.yaml
conda activate pia
```

If you want to use lower version of Pytorch (e.g. 1.13.1), you can use the following command:

```
conda env create -f environment.yaml
conda activate pia
```

We strongly recommand you to use Pytorch==2.0.0 which supports `scaled_dot_product_attention` for memory-efficient image animation.

### Download checkpoints
<li>Download the Stable Diffusion v1-5</li>

```
git lfs install
git clone https://huggingface.co/runwayml/stable-diffusion-v1-5 models/StableDiffusion/
```

<li>Download Personalized Models</li>

```
bash download_bashscripts/1-RealisticVision.sh
bash download_bashscripts/2-RcnzCartoon.sh
bash download_bashscripts/3-MajicMix.sh
```

<li>Download PIA</li>

```
bash download_bashscripts/0-PIA.sh
```


You can also download *pia.ckpt* through link on [Google Drive](https://drive.google.com/file/d/1RL3Fp0Q6pMD8PbGPULYUnvjqyRQXGHwN/view?usp=drive_link)
or [HuggingFace](https://huggingface.co/Leoxing/PIA).

Put checkpoints as follows:
```
└── models
    ├── DreamBooth_LoRA
    │   ├── ...
    ├── PIA
    │   ├── pia.ckpt
    └── StableDiffusion
        ├── vae
        ├── unet
        └── ...
```

## Usage
### Image Animation
Image to Video result can be obtained by:
```
python inference.py --config=example/config/lighthouse.yaml
python inference.py --config=example/config/harry.yaml
python inference.py --config=example/config/majic_girl.yaml
```
Run the command above, you will get:
<table class="center">
    <tr>
      <td><p style="text-align: center">Input Image</p></td>
      <td><p style="text-align: center">lightning, lighthouse</p></td>
      <td><p style="text-align: center">sun rising, lighthouse</p></td>
      <td><p style="text-align: center">fireworks, lighthouse</p></td>
    </tr>
    <tr>
      <td><img src="__assets__/image_animation/real/lighthouse.jpg"></td>
      <td><img src="__assets__/image_animation/real/1.gif"></td>
      <td><img src="__assets__/image_animation/real/2.gif"></td>
      <td><img src="__assets__/image_animation/real/3.gif"></td>
    </tr>
    <tr>
      <td><p style="text-align: center">Input Image</p></td>
      <td><p style="text-align: center">1boy smiling</p></td>
      <td><p style="text-align: center">1boy playing the magic fire</p></td>
      <td><p style="text-align: center">1boy is waving hands</p></td>
    </tr>
    <tr>
      <td><img src="__assets__/image_animation/rcnz/harry.png"></td>
      <td><img src="__assets__/image_animation/rcnz/1.gif"></td>
      <td><img src="__assets__/image_animation/rcnz/2.gif"></td>
      <td><img src="__assets__/image_animation/rcnz/3.gif"></td>
    </tr>
    <tr>
      <td><p style="text-align: center">Input Image</p></td>
      <td><p style="text-align: center">1girl is smiling</p></td>
      <td><p style="text-align: center">1girl is crying</p></td>
      <td><p style="text-align: center">1girl, snowing </p></td>
    </tr>
    <tr>
      <td><img src="__assets__/image_animation/majic/majic_girl.jpg"></td>
      <td><img src="__assets__/image_animation/majic/1.gif"></td>
      <td><img src="__assets__/image_animation/majic/2.gif"></td>
      <td><img src="__assets__/image_animation/majic/3.gif"></td>
    </tr>

</table>

<!-- More results:

<table class="center">
    <tr>
      <td><p style="text-align: center">Input Image</p></td>
    </tr>
    <tr>
    </tr>
</table> -->

### Motion Magnitude
You can control the motion magnitude through the parameter **magnitude**:
```sh
python inference.py --config=example/config/xxx.yaml --magnitude=0 # Small Motion
python inference.py --config=example/config/xxx.yaml --magnitude=1 # Moderate Motion
python inference.py --config=example/config/xxx.yaml --magnitude=2 # Large Motion
```
Examples:

```sh
python inference.py --config=example/config/labrador.yaml
python inference.py --config=example/config/bear.yaml
python inference.py --config=example/config/genshin.yaml
```

<table class="center">
    <tr>
      <td><p style="text-align: center">Input Image<br>& Prompt</p></td>
      <td><p style="text-align: center">Small Motion</p></td>
      <td><p style="text-align: center">Moderate Motion</p></td>
      <td><p style="text-align: center">Large Motion</p></td>
    </tr>
    <tr>
    <td><img src="__assets__/image_animation/magnitude/labrador.png" style="width: 220px">a golden labrador is running</td>
     <td><img src="__assets__/image_animation/magnitude/1.gif"></td>
      <td><img src="__assets__/image_animation/magnitude/2.gif"></td>
      <td><img src="__assets__/image_animation/magnitude/3.gif"></td>
    </tr>
    <tr>
    <td><img src="__assets__/image_animation/magnitude/bear/bear.jpg" style="width: 220px">1bear is walking, ...</td>
     <td><img src="__assets__/image_animation/magnitude/bear/1.gif"></td>
      <td><img src="__assets__/image_animation/magnitude/bear/2.gif"></td>
      <td><img src="__assets__/image_animation/magnitude/bear/3.gif"></td>
    </tr>
    <tr>
    <td><img src="__assets__/image_animation/magnitude/genshin/genshin.jpg" style="width: 220px">cherry blossom, ...</td>
     <td><img src="__assets__/image_animation/magnitude/genshin/1.gif"></td>
      <td><img src="__assets__/image_animation/magnitude/genshin/2.gif"></td>
      <td><img src="__assets__/image_animation/magnitude/genshin/3.gif"></td>
    </tr>
</table>

### Style Transfer
To achieve style transfer, you can run the command(*Please don't forget set the base model in xxx.yaml*):

Examples:

```sh
python inference.py --config example/config/concert.yaml --style_transfer
python inference.py --config example/config/ania.yaml --style_transfer
```
<table class="center">
    <tr>
      <td><p style="text-align: center">Input Image<br> & Base Model</p></td>
      <td><p style="text-align: center">1man is smiling</p></td>
      <td><p style="text-align: center">1man is crying</p></td>
      <td><p style="text-align: center">1man is singing</p></td>
    </tr>
    <tr>
      <td style="text-align: center"><img src="__assets__/image_animation/style_transfer/concert.png" style="width:220px">Realistic Vision</td>
      <td><img src="__assets__/image_animation/style_transfer/1.gif"></td>
      <td><img src="__assets__/image_animation/style_transfer/2.gif"></td>
      <td><img src="__assets__/image_animation/style_transfer/3.gif"></td>
    </tr>
    <tr>
      <td style="text-align: center"><img src="__assets__/image_animation/style_transfer/concert.png" style="width:220px">RCNZ Cartoon 3d</td>
      <td><img src="__assets__/image_animation/style_transfer/4.gif"></td>
      <td><img src="__assets__/image_animation/style_transfer/5.gif"></td>
      <td><img src="__assets__/image_animation/style_transfer/6.gif"></td>
    </tr>
    <tr>
      <td><p style="text-align: center"></p></td>
      <td><p style="text-align: center">1girl smiling</p></td>
      <td><p style="text-align: center">1girl open mouth</p></td>
      <td><p style="text-align: center">1girl is crying, pout</p></td>
    </tr>
    <tr>
      <td style="text-align: center"><img src="__assets__/image_animation/style_transfer/anya/anya.jpg" style="width:220px">RCNZ Cartoon 3d</td>
      <td><img src="__assets__/image_animation/style_transfer/anya/1.gif"></td>
      <td><img src="__assets__/image_animation/style_transfer/anya/2.gif"></td>
      <td><img src="__assets__/image_animation/style_transfer/anya/3.gif"></td>
    </tr>
</table>

### Loop Video

You can generate loop by using the parameter --loop

```sh
python inference.py --config=example/config/xxx.yaml --loop
```

Examples:
```sh
python inference.py --config=example/config/lighthouse.yaml --loop
python inference.py --config=example/config/labrador.yaml --loop
```

<table>
  <tr>
    <td><p style="text-align: center">Input Image</p></td>
    <td><p style="text-align: center">lightning, lighthouse</p></td>
    <td><p style="text-align: center">sun rising, lighthouse</p></td>
    <td><p style="text-align: center">fireworks, lighthouse</p></td>
  </tr>
  <tr>
    <td style="text-align: center"><img src="__assets__/image_animation/loop/lighthouse/lighthouse.jpg" style="width:auto"></td>
    <td><img src="__assets__/image_animation/loop/lighthouse/1.gif"></td>
    <td><img src="__assets__/image_animation/loop/lighthouse/2.gif"></td>
    <td><img src="__assets__/image_animation/loop/lighthouse/3.gif"></td>
  </tr>
  <tr>
    <td><p style="text-align: center">Input Image</p></td>
    <td><p style="text-align: center">labrador jumping</p></td>
    <td><p style="text-align: center">labrador walking</p></td>
    <td><p style="text-align: center">labrador running</p></td>
  </tr>
  <tr>
    <td style="text-align: center"><img src="__assets__/image_animation/loop/labrador/labrador.png" style="width:auto"></td>
    <td><img src="__assets__/image_animation/loop/labrador/1.gif"></td>
    <td><img src="__assets__/image_animation/loop/labrador/2.gif"></td>
    <td><img src="__assets__/image_animation/loop/labrador/3.gif"></td>
  </tr>
</table>

## AnimateBench
We have open-sourced AnimateBench on [HuggingFace](https://huggingface.co/datasets/ymzhang319/AnimateBench) which includes images, prompts and configs to evaluate PIA and other image animation methods.



## Acknowledgements
The code is built upon [AnimateDiff](https://github.com/guoyww/AnimateDiff), [Tune-a-Video](https://github.com/showlab/Tune-A-Video) and [PySceneDetect](https://github.com/Breakthrough/PySceneDetect)
