# PlanesNet

PlanesNet is a labeled dataset consiting of image chips extracted from [Planet](https://www.planet.com/) satellite imagery. The purpose of PlanesNet is to serve as labeled training data to train machine learning algorithms to detect the locations of airplanes in Planet's medium resolution remote sensing imagery. 

The dataset includes 14700 20x20 RGB images labeled with either a "plane" or "no-plane" classification. Image chips were derived from PlanetScope full-frame visual scene products, which are orthorectified to a 3 meter pixel size. 

PlanesNet will be continusouly updated as new Planet imagery is collected becomes available to grow the dataset. Current PlanesNet images were collected prior to May 10, 2017. 
 
## Class Labels   

The "planes" class includes 4700 images. Images in this class are near-centered on the body of a single airplane, with the majority of the plane's wings, tail, and nose also visible. Examples of different aircraft sizes, orientations, and atmospheric conditions are included. Example images from this class are shown below. 

![planes](http://i.imgur.com/SkimtmU.png)

The "no-planes" class includes 9800 images. 4700 of these images are a random sampling of different landcover features - water, vegetion, bare earth, buildings, etc. - that do not include any portion of an airplane. The other 4700 images are "confusers" that contain a portion of an airplane, but not enough to meet the full definition of the "planes" class. Example images from this class are shown below.

![no-planes](http://i.imgur.com/9mxE7Ca.png)
![planes](http://i.imgur.com/81eOBRz.png)

## Dataset Layout

The PlanesNet dataset can be loaded into Python as a dictionary object ([see below](https://github.com/rhammell/planesnet/blob/master/README.md#loading-the-data)) containing the following elements: 

- **data:** a 14700x1200 numpy array of datatype uint8. Each row of the array stores a single 20x20 RGB image. The first 400 entries contain the red channel values, the next 400 the green, and the final 400 the blue. The image is stored in row-major order, so that the first 20 entries of the array are the red channel values of the first row of the image.

- **labels:** a list of 14700 numbers, valued 1 or 0, representing the "planes" class and "no-plane" class, respectively.

- **scene_ids:** a list of 14700 strings containing the unique identifier of the PlanetScope visual scene the image was extracted from. The scene id can be used with the [Planet API](https://www.planet.com/docs/reference/data-api/) to discover and download the scene.

- **locations:** a list of 14700 two-element tuples containing the longitude and latitude coordinates of the image center point.

The list values at index *i* in **labels**, **scene_ids**, and **locations** each correspond to the *i*-th image in the **data** array.

## Common Operations

### Loading the Data   

PlanesNet is distributed as a compressed "pickled" object. The dataset can be loaded into a dictionary object by using the gzip and cPickle modules.

```python
# Python 2.7
import gzip
import cPickle

f = gzip.open('planesnet.pklz','rb')
planesnet = cPickle.load(f)
f.close()
```
### Saving Images

Each individual image is stored as a single row within the PlanesNet **data** array. Images can be saved into a .png format by reshaping the 1200 row values into a 20x20x3 dimensional array that can be saved out using the Python Image Libary.  

```python
from PIL import Image

index = 50 # Row to be saved
row = planesnet['data'][index]

im = Image.fromarray(row.reshape((3, 400)).T.reshape((20,20,3)))
im.save('20x20.png')
```

## License

Satellite imagery used to build PlanesNet is made availble through Planet's [Open California](https://www.planet.com/products/open-california/) dataset, which is [openly licenesed](https://creativecommons.org/licenses/by-sa/4.0/). As such, PlanesNet is also available under the same CC-BY-SA license.
