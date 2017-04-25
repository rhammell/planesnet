# PlanesNet

PlaneNet is a labeled dataset consiting of subset images extracted from [Open California](https://www.planet.com/products/open-california/) satellite imagery. The dataset includes 10500 20x20 RGB images labeled with either a "plane" or "no-plane" classification. Reference image IDs and lon/lat coordinates are also available for each image.  
 
## Classes

The "planes" class includes 3500 images. Images in this class are centered on on the body of a single airplane, with both wings and the tail visible. Example images from this class are shown below, and a mosaic of all images in this class can be seen [here]. 

![planes](http://i.imgur.com/SkimtmU.png)

The "no-planes" class includes 7000 images. Half of these images are a random sampling of different landcover features - water, vegetion, bare earth, buildings, etc. - 

PlanesNet is labeled training data consisting of images  

Labeld training data for detection of airplaines in Planet satellite imagery

The dataset is divided into five training batches and one test batch, each with 10000 images. The test batch contains exactly 1000 randomly-selected images from each class. The training batches contain the remaining images in random order, but some training batches may contain more images from one class than another. Between them, the training batches contain exactly 5000 images from each class. 

## Dataset Layout

The PlanesNet dataset can be loaded into Python as a dictionary object (see below) containing the following elements: 

- **data:** a 10500x1200 numpy array of uint8s. Each row of the array stores a single 20x20 color image. The first 400 entries contain the red channel values, the next 400 the green, and the final 400 the blue. The image is stored in row-major order, so that the first 20 entries of the array are the red channel values of the first row of the image.

- **labels:** a list of 10500 numbers, either 1. or 0, representing the "planes" class and "no-plane" class, respectively. The number at index *i* indicates the label of the *i*th image in the array **data**.

- **scene_ids:** a list of 10500 strings image was extracted from. Individual images

- **locations:** a list of 10500 tuples containing the longitude and latitude coordinages of the 

## Common Operations

### Loading the Data   

Wne loadoing the data do thsi and that and this ist eh best thing eve

```python
import gzip
import cPickle
```
### Saving Images

Each individual example image 

```python
from PIL import Image

index = 50 # Row to be saved
row_image = planesnet['data'][index]

im = Image.fromarray(row_image.reshape((3, 400)).T.reshape((20,20,3)))
im.save('20x20.png')
```
