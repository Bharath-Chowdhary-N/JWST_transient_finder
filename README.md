## How to create PSF for F200W
```
from matplotlib import pyplot as plt
import stpsf

nircam = stpsf.NIRCam()
nircam.filter = 'F200W'
psf200 = nircam.calc_psf(nlambda=5, oversample=1)


plt.figure(figsize=(16, 6))  # width=16 inches, height=6 inches
plt.subplot(1,2,1)
stpsf.display_psf(psf200, colorbar_orientation='horizontal')
axis2 = plt.subplot(1,2,2)
stpsf.display_ee(psf200, ax=axis2) 
psf200.writeto('nircam_{}.fits'.format(nircam.filter), overwrite=True)
plt.savefig('plot_nircam_{}.pdf'.format(nircam.filter))
```
