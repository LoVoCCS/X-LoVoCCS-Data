These set of response and background files were generated using
a ~340 ks observation of Tycho. The ARF was generated using
the "extended" source option for the 5 arcminute radius circle centered
on Cas A with the optical axis roughly centered on the SNR. These
response files are for ONE of the two NuSTAR telescopes.

The RMF and ARF files were generated using nuproducts, while the
background PHA file was simulated using the nuskybgd simulation toolkit.

extended_5arcminRad.arf =
	"Extended" object with an extraction radius of 5 arcminute
	bgd_5arcmin.pha - background from a 5 arcminute radius extraction region.
	nustar.rmf - detector response file for sources near the optical axis.

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

Now, do a simulation without background. The correct responses are shown below for
the queries. This will give you some idea of what the *source* statistics will be for
a given duration of an observation.

XSPEC12> fakeit none
For fake spectrum #1 response file is needed: nustar.rmf
   ...and ancillary file: 5arcminA.arf
 Use counting statistics in creating fake data? (y): y
 Input optional fake file prefix: nobgd
 Fake data file name (nobgdtest2.fak.fak): nobgd.fak
 Exposure time, correction norm, bkg exposure time (1.00000, 1.00000, 1.00000): 

Now we want to do a fakeit with background. First we load the provided background file:

XSPEC12> da nobgd.fak
XSPEC12> backgrnd bgd_5arcminA.pha

NOTE!! The spectrum that you currently have loaded will not be correctly background
subtracted since we didn't simulate any background. To generate a source+background
we use fakeit again (without the "none" this time). Again, we've filled in the correct responses. Note that we here we've simulated a 100 ks exposure. The user can adjust this
to the desired observation duration.


XSPEC12> fakeit 
 Use counting statistics in creating fake data? (y): y
 Input optional fake file prefix: withbgd.fak
 Fake data file name (withbgd.faknobgd.fak.fak): withbgd.fak
 Exposure time, correction norm, bkg exposure time (1.00000, -1.00000, 293674.): 100e3, 1, 100e3

