# pygeogreen
python library for identify green areas 
import rasterio
import numpy

image_file = "imagen_NDVI.tif"

# Load red and NIR bands - note all PlanetScope 4-band images have band order BGRN
with rasterio.open(image_file) as src:
    band_red = src.read(3)

with rasterio.open(image_file) as src:
    band_nir = src.read(4)
    # Calculate NDVI
ndvi = (band_nir.astype(float) - band_red.astype(float)) / (band_nir + band_red)
# Set spatial characteristics of the output object to mirror the input
kwargs = src.meta
kwargs.update(dtype=rasterio.float32,count = 1)
# Create the file
with rasterio.open('ndvi.tif', 'w', **kwargs) as dst:
        dst.write_band(1, ndvi.astype(rasterio.float32))
#apply a color map
import matplotlib.pyplot as plt
plt.imsave("ndvi_cmap.png", ndvi, cmap=plt.cm.summer)
