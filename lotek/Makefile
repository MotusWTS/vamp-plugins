## NB: on linux, do a make clean whenever there are significant changes to the class structure
## of any plugin.
##
##  Skeleton Makefile for Vamp plugin builds using command-line tools.
##
##  Rename this to Makefile, and edit as appropriate.
##  This Makefile WILL NOT WORK until you have edited it as described
##  below -- the Makefile as supplied does nothing useful at all!
##
##  Various sets of options are provided, commented out -- just uncomment
##  (remove the '#' characters for) the set that most closely resembles
##  your own situation, and adjust to taste.  Then run "make".
##
##  (For Windows builds using MS Visual Studio, start instead with the
##  VampExamplePlugins project found in the build directory of the SDK.)


# Edit this to the base name of your plugin library
#
PLUGIN_LIBRARY_NAME = lotek-plugins

# Where the plugin library should be installed:

PLUGIN_INSTALL_DIR = ~/.vamp

# Edit this to list one .o file for each .cpp file in your plugin project
#
PLUGIN_CODE_OBJECTS = SNRZFindPulse.o SlidingSpectrum.o FindPulseFD.o FindPulseFDBatch.o FreqEstimator.o FindPulseTD.o FindPulseTDBatch.o

# Edit this to the location of the Vamp plugin SDK, relative to your
# project directory
#
VAMP_SDK_INCLUDE_DIR = /usr/include/
VAMP_SDK_LIB_DIR = /usr/lib/x86_64-linux-gnu

CXXFLAGS_PRODUCTION = -std=c++0x -I$(VAMP_SDK_INCLUDE_DIR) -Wall -fPIC -O3 -ffast-math  -ftree-vectorize
CXXFLAGS_DEBUG = -std=c++0x -I$(VAMP_SDK_INCLUDE_DIR) -Wall -fPIC -g3

##CXXFLAGS = $(CXXFLAGS_DEBUG)
CXXFLAGS = $(CXXFLAGS_PRODUCTION)
PLUGIN_EXT = .so
PLUGIN = $(PLUGIN_LIBRARY_NAME)$(PLUGIN_EXT)
LDFLAGS = -shared -Wl,-soname=$(PLUGIN) -lvamp-sdk -L/usr/local/lib -lfftw3f -Wl,--version-script=vamp-plugin.map


$(PLUGIN): $(PLUGIN_CODE_OBJECTS) lotek-plugins.o
	   $(CXX) -o $@ $^ $(LDFLAGS)

lotek-plugins.o: $(PLUGIN_CODE_OBJECTS) lotek-plugins.cpp

SNRZFindPulse.o: SpectralPulseFinder.h SNRZFindPulse.h FixedPulseDetector.h MovingSum.h SlidingSpectrum.h PeakFinder.h

FindPulseTDSNRZ.o: FindPulseTDSNRZ.h FixedPulseDetector.h KahanMovingAverager.h SlidingSpectrum.h PeakFinder.h FreqEstimator.h

FreqEstimator.o: FreqEstimator.h

FindPulseFD.o: FindPulseFD.h PulseFinder.h

FindPulseFDBatch.o: FindPulseFDBatch.h PulseFinder.h

FindPulseTD.o: FindPulseFD.h PulseFinder.h

FindPulseTDBatch.o: FindPulseTDBatch.h PulseFinder.h

FindPulse.o: FindPulse.h MovingAverager.h

FindPulseBatch.o: FindPulseBatch.h MovingAverager.h

AveragePower.o: AveragePower.h MovingAverager.h

NewFindPulse.o: NewFindPulse.h RingBufferWithMax.h DynamicQuantile.h PeakFinder.h MovingAverager.h FreqEstimator.h EdgeDetector.h PulseDetector.h KahanSum.h

FreqEstimator.o: FreqEstimator.h

SlidingSpectrum.o: SlidingSpectrum.cpp SlidingSpectrum.h

FindNarrowBandPulsePlugin.o: FindNarrowBandPulsePlugin.h PeakFinder.h NarrowBandSpectralPulseFinder.h NarrowBandSlidingSpectrum.h

testFreqEstimator.o: FreqEstimator.h testFreqEstimator.cpp

testFreqEstimator: testFreqEstimator.o FreqEstimator.o
	$(CXX) -o $@ $^ -L/usr/local/lib -lfftw3f

testKahanSum: KahanSum.h testKahanSum.cpp
	g++ -$(CXXFLAGS) -o testKahanSum testKahanSum.cpp

testPeakFinder: PeakFinder.h testPeakFinder.cpp RingBuffWithMax.h
	g++ $(CXXFLAGS) -o testPeakFinder testPeakFinder.cpp

testDynamicQuantile: DynamicQuantile.h testDynamicQuantile.cpp
	g++ $(CXXFLAGS) -o testDynamicQuantile testDynamicQuantile.cpp

testEdgeDetector: EdgeDetector.h testEdgeDetector.cpp
	g++ $(CXXFLAGS) -o testEdgeDetector testEdgeDetector.cpp

testVariablePulseDetector: VariablePulseDetector.h testVariablePulseDetector.cpp
	g++ $(CXXFLAGS) -o testVariablePulseDetector testVariablePulseDetector.cpp

testFixedPulseDetector: FixedPulseDetector.h testFixedPulseDetector.cpp
	g++ $(CXXFLAGS) -o testFixedPulseDetector testFixedPulseDetector.cpp

testAccordion: Accordion.h testAccordion.cpp
	g++ $(CXXFLAGS) -o testAccordion testAccordion.cpp

testKahanMovingAverager: KahanMovingAverager.h testKahanMovingAverager.cpp
	g++ $(CXXFLAGS) -o testKahanMovingAverager testKahanMovingAverager.cpp

testMovingSum: MovingSum.h testMovingSum.cpp
	g++ $(CXXFLAGS) -o testMovingSum testMovingSum.cpp

testSlidingSpectrum: SlidingSpectrum.h testSlidingSpectrum.o SlidingSpectrum.o
	g++ $(CXXFLAGS) -o testSlidingSpectrum SlidingSpectrum.o testSlidingSpectrum.cpp -lfftw3f

testNarrowBandSlidingSpectrum: NarrowBandSlidingSpectrum.h testNarrowBandSlidingSpectrum.o
	g++ $(CXXFLAGS) -o testNarrowBandSlidingSpectrum testNarrowBandSlidingSpectrum.cpp

testSpectralPulseFinder: SpectralPulseFinder.h testSpectralPulseFinder.cpp SlidingSpectrum.o
	g++ $(CXXFLAGS) -o testSpectralPulseFinder testSpectralPulseFinder.cpp SlidingSpectrum.o -lfftw3f

testNarrowBandSpectralPulseFinder: NarrowBandSpectralPulseFinder.h testNarrowBandSpectralPulseFinder.cpp NarrowBandSlidingSpectrum.h
	g++ $(CXXFLAGS) -o testNarrowBandSpectralPulseFinder testNarrowBandSpectralPulseFinder.cpp

clean:
	rm -f *.o                               \
	testAccordion				\
	testDynamicQuantile			\
	testEdgeDetector			\
	testFixedPulseDetector			\
	testKahanMovingAverager			\
	testKahanSum                            \
	testNarrowBandSpectralPulseFinder	\
	testPeakFinder				\
	testSpectralPulseFinder			\
	testVariablePulseDetector


install: $(PLUGIN)
	if [ "$(CXXFLAGS)" != "$(CXXFLAGS_DEBUG)" ]; then strip $(PLUGIN); fi
	cp -f $(PLUGIN) $(PLUGIN_INSTALL_DIR)
