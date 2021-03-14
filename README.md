<meta http-equiv="refresh" content="0; url=https://codeberg.org/monilophyta/imageio-flif" />

# imageio-FLIF

imageio plugin with FLIF wrapper for Python

Code repository here: [https://codeberg.org/monilophyta/imageio-flif](https://codeberg.org/monilophyta/imageio-flif)


## Purpose

The purpose of this project is to provide a simple python wrapper for the [FLIF](https://github.com/FLIF-hub/FLIF) image compression.
It implements a simple [plugin](https://imageio.readthedocs.io/en/stable/plugins.html) for the [imageio](https://imageio.github.io) library that enables reading and writing FLIF image files.

[FLIF](https://github.com/FLIF-hub/FLIF) supports lossy and lossless compression for 8bit and 16bit gray scale and RGB(A) images.
The lossless compression mode outperforms PNG, lossless WebP, lossless BPG and lossless JPEG 2000 in terms of compression ratio.

Like GIF, FLIF files support animations by storing mutliple frames within one `.flif` file.

### This plugin supports

|                  | image shape | depth | reading | writing |
|------------------|:-----------:|:-----:|:-------:|:-------:|
|       Gray scale |    [WxH]    | 8bit  | ✅ | ✅ |
|       Gray scale |    [WxH]    | 16bit | ✅ | ✅ |
|              RGB |   [WxHx3]   | 8bit  | ✅ | ✅ |
|              RGB |   [WxHx3]   | 16bit | ✅ | ❌ |
|             RGBA |   [WxHx4]   | 8bit  | ✅ | ✅ |
|             RGBA |   [WxHx4]   | 16bit | ✅ | ❌ |
| Palette color <br>(quantized) images |    [WxH]    | 8bit  | ✅ | ✅ |

<br>

## Build Instructions

### Install the dependencies

#### FLIF dependencies

`imageio-FLIF` imports the [FLIF](https://github.com/FLIF-hub/FLIF) library as a sub-module. Please have a look [here](https://github.com/FLIF-hub/FLIF#install-the-dependencies) for [FLIF](https://github.com/FLIF-hub/FLIF) library dependencies.

#### `imageio-FLIF` dependencies

 - numpy: `sudo apt-get install python3-numpy` (on debian/ubuntu)
 - imageio: `sudo apt-get install python3-imageio` (on debian/ubuntu)

### Checkout + Compile

```bash
git clone https://codeberg.org/monilophyta/imageio-flif.git imageio_flif
cd imageio_flif
git submodule init
git submodule update
make
```

## Usage

### Import Reader/Writer

```python
# import imageio framework for image reading/writing
import imageio

# imported FLIF plugin registers itself at the imageio framework
import imageio_flif
```

### Decoding

#### Simple method for single images

```python
# returns a uint8 or uint16 numpy array of shape [WxH(x3/4)]
img = imageio.imread( "path_to/image.flif" )
```

#### Decoding aninmations

```python
# return a list with each item a equal shaped array with dtype uint8 or uint16
img_list = imageio.mimread( "path_to/image.flif" ) 
```

### Encoding

#### Simple method for single images

```python
# img must be an uint8 or uint16 numpy array with shape [WxH(x3/4)]
imageio.imwrite( "path_to/image.flif", img ) 
```

#### Encoding aninmations

```python
# img must be a list of equal shaped [WxH(x3/4)] numpy arrays, all of them with dtype uint8 or uint16 [WxH(x3/4)]
imageio.mimwrite( "path_to/image.flif", img_list, duration=N ) 
```


