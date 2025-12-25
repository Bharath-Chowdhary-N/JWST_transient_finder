## How to create PSF for F200W and also perform sanity check on its Pixel scale
```
from matplotlib import pyplot as plt
import stpsf

nircam = stpsf.NIRCam()
nircam.filter = 'F200W'
psf200 = nircam.calc_psf(nlambda=5, oversample=1)

# Check the pixel scale in the PSF
print("PSF pixel scale info:")
print(f"PIXELSCL: {psf200[0].header['PIXELSCL']} arcsec/pixel")
print(f"Oversample: {psf200[0].header.get('OVERSAMP', 'Not found')}")
print(f"Detector: {psf200[0].header.get('DETECTOR', 'Not found')}")

plt.figure(figsize=(16, 6))
plt.subplot(1,2,1)
stpsf.display_psf(psf200, colorbar_orientation='horizontal')
axis2 = plt.subplot(1,2,2)
stpsf.display_ee(psf200, ax=axis2) 

psf200.writeto('nircam_{}.fits'.format(nircam.filter), overwrite=True)
plt.savefig('plot_nircam_{}.pdf'.format(nircam.filter))
```
