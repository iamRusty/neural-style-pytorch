# neural-style: Neural Style in Pytorch!

An implementation of the neural style in PyTorch! This notebook implements [Image Style Transfer Using Convolutional Neural Networks](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf) by Leon Gatys, Alexander Ecker, and Matthias Bethge. 

This implementation is inspired by the implementations of:
* Anish Athalye [Neural Style in Tensorflow](https://github.com/anishathalye/neural-style),
* Justin Johnson [Neural Style in Torch](https://github.com/jcjohnson/neural-style), and
* ProGamerGov [Neural Style in PyTorch](https://github.com/ProGamerGov/neural-style-pt)

The [original caffe pretrained weights of VGG19](https://github.com/jcjohnson/pytorch-vgg) were used for this implementation, instead of the pretrained VGG19's in PyTorch's model zoo.

## Examples
### Catriona Gray + Woman I by Willem de Kooning
![Catriona](https://i.imgur.com/Cx7WEZo.jpg)

### Janelle Monae + Starry Night by Vincent van Gogh
![Janelle Monae](https://i.imgur.com/WWq6I1U.jpg)

### Andrew Y. Ng + Oil Painting of a Girl in Rain
![AndrewYNg](https://i.imgur.com/cO9YdZI.jpg)

### Style Transfer of Golden Bridge
![Golden Bridge](https://i.imgur.com/F4GrkJU.jpg)

### Anish Athalye (author of neural-style-tf) + Starry Night
![anish](https://i.imgur.com/MB90IvW.png)

### [Some Old Man](https://www.google.com/search?q=philippine+idiot&source=lnms&tbm=isch&sa=X&ved=0ahUKEwi0p_PDqK3fAhVIabwKHRWeCPQQ_AUIDigB&biw=2560&bih=1311) + Increasing Style Weights of Starry Night
![Philippine Idiot](https://i.imgur.com/bK8bnCN.jpg)

## Requirements
`NOTE`: For `Google-Colab users` - All data files and dependencies can be installed by running the uppermost cell of the notebook! See `Usage`!

### Data Files
* [Pre-trained VGG19 network weights](https://s3-us-west-2.amazonaws.com/jcjohns-models/vgg16-00b39a1b.pth) - put it in `models/` directory
* [torchvision](https://pytorch.org/) - `torchvision.models` contains the VGG19 model skeleton

### Dependecies
* [PyTorch](https://pytorch.org/)
* [NumPy](https://www.scipy.org/install.html)
* [Jupyter](http://jupyter.org/install)
* [opencv2](https://matplotlib.org/users/installing.html)
* [Copy](https://docs.python.org/3/library/copy.html)

## Usage
If you don't have a GPU, you may want to run the notebook in [Google Colab](https://colab.research.google.com)! Colab is a cloud-GPU service with an interface similar to Jupyter notebook. A separate instruction is included to get started with Colab.

### Local GPU
After installing the dependencies, run `models/download_model.sh` script to download the pretrained VGG19 weights. 
```
sh models/download_models.sh
```

Codes are implemented inside the `neural_style.ipynb` notebook. Jupyter notebook environment is needed to run notebook.
```
jupyter notebook
```

### For Google Colab
The included notebook file is a `Google-Colab-ready` notebook! Uncomment and run the first cell to download the demo pictures, and VGG19 weights. It will also install the dependencies (i.e. PyTorch and torchvision).
```
# Download VGG19 Model
!wget -c https://s3-us-west-2.amazonaws.com/jcjohns-models/vgg19-d01eb7cb.pth
!mkdir models
!cp vgg19-d01eb7cb.pth models/

# Download Images
!wget -c https://github.com/iamRusty/neural-style-pytorch/archive/master.zip
!unzip -q master.zip
!mkdir images
!cp neural-style-pytorch-master/images/1-content.jpg images
!cp neural-style-pytorch-master/images/1-style.jpg images

# Install PyTorch and torchvision
!pip install pytorch
!pip install torchvision
```
## Options
### Image
* `MAX_IMAGE_SIZE`: sets the max dimension of height or weight. Bigger GPU memory is need to run larger `MAX_IMAGE_SIZE`. Default is `512`px.
* `INIT_IMAGE`: Sets the initial image file to either `'random'` or `'content'`. Default is `random` which initializes a noise image. Content copies a resized content image, giving free optimization of content loss!
* `CONTENT_PATH`: path of the content image
* `STYLE_PATH`: path of the style image

### Optimizer
* `OPTIMIZER`: sets the optimizer to either 'adam' or 'lbfgs'. Default optimizer is `Adam` with learning rate of 10. L-BFGS was used in the original (matlab) implementation of the reference paper.
* `ADAM_LR`: learning rate of the adam optimizer. Default is `1e1`
* `CONTENT_WEIGHT`: Multiplier weight of the loss between content representations and the generated image. Default is `5e0`
* `STYLE_WEIGHT`: Multiplier weight of the loss between style representations and the generated image. Default is `1e2`
* `TV_WEIGHT`: Multiplier weight of the [Total Variation Denoising](https://github.com/jcjohnson/neural-style/issues/302). Default is `1e-3`
* `NUM_ITER`: Iterations of the style transfer. Default is `500`
* `SHOW_ITER`: Number of iterations before showing and saving the generated image. Default is `100`

### Model
* `VGG19_PATH` = path of VGG19 Pretrained weights. Default is `'models/vgg19-d01eb7cb.pth'`
* `POOL`: Defines which pooling layer to use. The reference paper suggests using average pooling! Default is `'max'`

## Todo!
* Multiple Style blending
* High-res Style Transfer
* Color-preserving Style Transfer