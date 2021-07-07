syntheticFlux_withInterp_ps_HSCPS1GaiaSDSS.fits
-----------------------------------------------

This FITS BinTable includes the synthetic photometry
of 56456 stellar model templates with four instruments.
Available filters are:

    HSC g, r, r2, i, i2, z, y,
    Gaia Bp, Rp, G,
    PS1 g, r, i, z, y,
    SDSS u, g, r, i, z.

The stellar model templates are based on the AMBRE templates
(de Laverny et al. 2012, A&A, 544, 126).
The original resolutions of the four stellar parameters
(effective temperature [Teff K], surface gravity [Log(g/cm/s^2)],
metallicity [M/H], and alpha-elements abundance [alpha/Fe])
were regrided into small ones
and the templates were interpolated
using a radial basis function (`scipy.interpolate.Rbf`).
This table gives the four stellar parameters
and the corresponding synthetic photometry set in Janskies.
Photon-counting detectors were assumed
in the computation of the synthetic photometries.

This table was computed by T. Yamashita,
but is due to be generated on the user side.
A computing script and necessary materials will be provided in future.
