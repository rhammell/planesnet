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

Explain what the datasets are

## Common Operations

###Loading the Data   

Wne loadoing the data do thsi and that and this ist eh best thing eve

```python
import gzip
import cPickle
```
###Saving Images

Images chan gebe saved out and filler filler filler fille 

```python
import gzip
import cPickle
```
