These set of response and background files were generated using
a ~134 ks observation of G21.5-0.9. The ARF was generated using
the "extended" source option for the 1 arcminute radius circle centered
on the source with the optical axis roughly centered on the SNR. These
response files are for ONE of the two NuSTAR telescopes.


The RMF and ARF files were generated using nuproducts, while the
background PHA file was simulated using the nuskybgd simulation toolkit.

File nomenclature:

extended_1arcminRad.arf =
	"Extended" object with an extraction radius of 1 arcminute
bgd_1arcmin.pha = background from a 1 arcminute radius extraction region.
nustar.rmf = detector response file for sources near the optical axis.

To simulate an exposure, set up your model first, e.g.:

mo apec
3.0
1.
0.
1.

Adjust you flux to the desired level, e.g.:

We want 2-10 keV flux of 1e-10 ergs/cm^2/sec

flux 2 10
->Model Flux   0.11642 photons (6.6779e-10 ergs/cm^2/s) range (2.0000 - 10.000 keV)

newpar 4 0.15

flux 2 10
-> Model Flux  0.017462 photons (1.0017e-10 ergs/cm^2/s) range (2.0000 - 10.000 keV)

XSPEC12>fakeit bgd_1arcmin.pha 
For fake spectrum #1 response file is needed: nustar.rmf 
   ...and ancillary file: 1arcmin_extended.arf 
 Use counting statistics in creating fake data? (y): 
 Input optional fake file prefix: 
 Fake data file name (nustar.fak): 
 Exposure time, correction norm, bkg exposure time (133782., 1.00000, 133782.): 100000

Note that the exposure time that fakeit suggests comes from the background.