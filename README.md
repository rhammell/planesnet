# PlanesNet

PlanesNet is a labeled dataset consiting of image chips extracted from [Planet](https://www.planet.com/) satellite imagery. The purpose of PlanesNet is to serve as labeled training data to train machine learning algorithms to detect the locations of airplanes in Planet's medium resolution remote sensing imagery. 

The dataset includes 14700 20x20 RGB images labeled with either a "plane" or "no-plane" classification. Image chips were derived from PlanetScope full-frame visual scene products, which are orthorectified to a 3 meter pixel size. 

PlanesNet will be continusouly updated as new Planet imagery is collected becomes available to grow the dataset. Current PlanesNet images were collected prior to May 10, 2017. 
 
## Class Labels   

The "plane" class includes 4900 images. Images in this class are near-centered on the body of a single airplane, with the majority of the plane's wings, tail, and nose also visible. Examples of different aircraft sizes, orientations, and atmospheric collection conditions are included. Example images from this class are shown below. 

![planes](http://i.imgur.com/SkimtmU.png)

The "no-plane" class includes 9800 images. Half of these are a random sampling of different landcover features - water, vegetion, bare earth, buildings, etc. - that do not include any portion of an airplane. The other half are "confusers" that contain a portion of an airplane, but not enough to meet the full definition of the "plane" class. Example images from this class are shown below.

![no-planes](http://i.imgur.com/9mxE7Ca.png)
![planes](http://i.imgur.com/81eOBRz.png)

## Dataset Layout
Provided is a zipped directory *planesnet.7z* that contains the entire dataset as .png image chips. Each individual image filename follows a specific format: *label* __ *scene id* __ *longitude* _ *latitude*.png

- **label:** Valued 1 or 0, representing the "plane" class and "no-plane" class, respectively. 

- **scene id:** The unique identifier of the PlanetScope visual scene the image chip was extracted from. The scene id can be used with the [Planet API](https://www.planet.com/docs/reference/data-api/) to discover and download the entire scene.

- **longitude_latitude:** The longitude and latitude coordinates of the image center point, with values separated by a single underscore. 

The dataset is also distributed as a compressed "pickled" file *planesnet.pklz*. This file can be loaded into a Python dictionary object by using the gzip and pickle modules.
```python
# Python 3
import gzip
import pickle
    
f = gzip.open('planesnet.pklz','rb')
planesnet = pickle.load(f, encoding='latin1')
f.close()
```
The loaded dictionary object will contain the following elements: 

- **data:** a 14700x1200 numpy array of datatype uint8. Each row of the array stores a single 20x20 RGB image. The first 400 entries contain the red channel values, the next 400 the green, and the final 400 the blue. The image is stored in row-major order, so that the first 20 entries of the array are the red channel values of the first row of the image.
- **labels:** a list of 14700 numbers, valued 1 or 0, representing the "planes" class and "no-plane" class, respectively.
- **scene_ids:** a list of 14700 strings containing the unique identifier of the PlanetScope visual scene the image was extracted from. The scene id can be used with the [Planet API](https://www.planet.com/docs/reference/data-api/) to discover and download the scene.
- **locations:** a list of 14700 two-element tuples containing the longitude and latitude coordinates of the image center point.

The list values at index *i* in **labels**, **scene_ids**, and **locations** each correspond to the *i*-th image in the **data** array.

## License
Satellite imagery used to build PlanesNet is made available through Planet's [Open California](https://www.planet.com/products/open-california/) dataset, which is [openly licensed](https://creativecommons.org/licenses/by-sa/4.0/). As such, PlanesNet is also available under the same CC-BY-SA license.
