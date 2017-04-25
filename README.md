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

The PlanesNet dataset can be loaded into Python as a dictionary object (see below) containing the following keys: 

- **data:** this is a tes ton  this nadn do ign it
- **labels:** tes tets te st te set e ts tes t set se t
- **scene_ids:** athe s test se tse tse tse tse tse tse tse tes ts et
- **locations:** asdflk asdfl; jasdflkjsf ;lsakjf sa;ldkfj as;ldfkj 

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
