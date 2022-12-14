# Setup
    ROOTDIR=/work/hassans/createCalib/calib-b1r1b3r3
    setup pfs_pipe2d w.2022.49
    setup -jr /work/hassans/software/drp_pfs_data

# Copy over recent calib with biases, darks etc
    cp -r /work/drp/CALIB-20220630 $ROOTDIR/CALIB
    CALIBDIR=$ROOTDIR/CALIB

# Generate b1 bootstrap

## Delete previous b1 detectormap and ingest sim
    sqlite3 $CALIBDIR/calibRegistry.sqlite3 'DELETE FROM detectorMap WHERE arm = "b" AND spectrograph = 1'
    \rm $CALIBDIR/DETECTORMAP/*b1.fits
    ingestPfsCalibs.py /work/drp --calib $CALIBDIR $DRP_PFS_DATA_DIR/detectorMap/detectorMap-sim-b1.fits --mode=copy --validity 100000 -c clobber=True

## bootstrap
    nohup bootstrapDetectorMap.py /work/drp --calib=$CALIBDIR --rerun=hassans/b1r1b3r3-detectorMap --flatId visit=45739 arm=b spectrograph=1 --arcId visit=45744 arm=b spectrograph=1 -c spatialOffset=0 spectralOffset=0 matchRadius=2 readLineList.exclusionRadius=1 > /work/hassans/logs/bootstrap-b1.log 2>&1 &

Stats:
    bootstrap INFO: Found 189 lines in 10 traces
    bootstrap INFO: Matched 110 lines
    bootstrap INFO: Median difference from detectorMap: 11.360055,-4.912796 pixels
    bootstrap INFO: Fit 48/66 points, rms: x=0.036863 y=0.076283 total=0.045361 pixels
    bootstrap INFO: Updating detectorMap...
    bootstrap INFO: Median difference from detectorMap: -1.959077,-7.007115 pixels
    bootstrap INFO: Fit 32/44 points, rms: x=0.099307 y=0.078170 total=0.064172 pixels
    bootstrap INFO: Updating detectorMap...

## Delete previous detectormap and ingest bootstrap
    sqlite3 $CALIBDIR/calibRegistry.sqlite3 'DELETE FROM detectorMap WHERE arm = "b" AND spectrograph = 1'
    rm -i $CALIBDIR/DETECTORMAP/*b1.fits
    ingestPfsCalibs.py /work/drp --calib $CALIBDIR /work/drp/rerun/hassans/b1r1b3r3-detectorMap/DETECTORMAP/pfsDetectorMap-045744-b1.fits --mode=copy --validity 100000 -c clobber=True


# Generate r1 bootstrap
## ingest sim
    sqlite3 $CALIBDIR/calibRegistry.sqlite3 'DELETE FROM detectorMap WHERE arm = "r" AND spectrograph = 1'
    \rm $CALIBDIR/DETECTORMAP/*r1.fits
    ingestPfsCalibs.py /work/drp --calib $CALIBDIR $DRP_PFS_DATA_DIR/detectorMap/detectorMap-sim-r1.fits --mode=copy --validity 100000 -c clobber=True

## bootstrap
    bootstrapDetectorMap.py /work/drp --calib=$CALIBDIR --rerun=hassans/r1-detectorMap --flatId visit=45742 arm=r spectrograph=1 --arcId visit=45744 arm=r spectrograph=1 -c spectralOffset=8 matchRadius=2 readLineList.exclusionRadius=1

Stats
    bootstrap.readLineList INFO: Filtered line lists, keeping species {'NeI'}.
    bootstrap INFO: Found 479 lines in 10 traces
    bootstrap INFO: Matched 365 lines
    bootstrap INFO: Median difference from detectorMap: -3.849263,-13.152738 pixels
    bootstrap INFO: Fit 171/217 points, rms: x=0.056161 y=0.109914 total=0.089740 pixels
    bootstrap INFO: Updating detectorMap...
    bootstrap INFO: Median difference from detectorMap: -4.674041,-11.844797 pixels
    bootstrap INFO: Fit 106/148 points, rms: x=0.097037 y=0.055410 total=0.050315 pixels

## ingest bootstrap
    sqlite3 $CALIBDIR/calibRegistry.sqlite3 'DELETE FROM detectorMap WHERE arm = "r" AND spectrograph = 1'
    \rm $CALIBDIR/DETECTORMAP/*r1.fits
    ingestPfsCalibs.py /work/drp --calib $CALIBDIR /work/drp/rerun/hassans/r1-detectorMap/DETECTORMAP/pfsDetectorMap-045744-r1.fits --mode=copy --validity 100000 -c clobber=True

# Generate b3 bootstrap
## ingest sim
    sqlite3 $CALIBDIR/calibRegistry.sqlite3 'DELETE FROM detectorMap WHERE arm = "b" AND spectrograph = 3'
    \rm $CALIBDIR/DETECTORMAP/*b3.fits
    ingestPfsCalibs.py /work/drp --calib $CALIBDIR $DRP_PFS_DATA_DIR/detectorMap/detectorMap-sim-b3.fits --mode=copy --validity 100000 -c clobber=True

## bootstrap
    bootstrapDetectorMap.py /work/drp --calib=$CALIBDIR --rerun=hassans/b3-detectorMap --flatId visit=81980 arm=b spectrograph=3 --arcId visit=81976 arm=b spectrograph=3 -c spectralOffset=8 matchRadius=2 readLineList.exclusionRadius=1

Stats
    bootstrap.readLineList INFO: Filtered line lists, keeping species {'HgII', 'CdI', 'HgI'}.
    WARNING: The fit may be unsuccessful; check fit_info['message'] for more information. [astropy.modeling.fitting]
    astropy WARN: The fit may be unsuccessful; check fit_info['message'] for more information.
    bootstrap INFO: Found 6225 lines in 600 traces
    bootstrap INFO: Matched 5414 lines
    bootstrap INFO: Median difference from detectorMap: 19.650212,-3.171097 pixels
    bootstrap INFO: Fit 2260/2645 points, rms: x=0.072107 y=0.109168 total=0.067631 pixels
    bootstrap INFO: Updating detectorMap...
    bootstrap INFO: Median difference from detectorMap: 16.960000,5.495879 pixels
    bootstrap INFO: Fit 2179/2769 points, rms: x=0.128155 y=0.272685 total=0.137044 pixels
    bootstrap INFO: Updating detectorMap...

## ingest bootstrap
    sqlite3 $CALIBDIR/calibRegistry.sqlite3 'DELETE FROM detectorMap WHERE arm = "b" AND spectrograph = 3'
    \rm $CALIBDIR/DETECTORMAP/*b3.fits
    ingestPfsCalibs.py /work/drp --calib $CALIBDIR /work/drp/rerun/hassans/b3-detectorMap/DETECTORMAP/pfsDetectorMap-081976-b3.fits --mode=copy --validity 100000 -c clobber=True


# Generate r3 bootstrap
## ingest sim
    sqlite3 $CALIBDIR/calibRegistry.sqlite3 'DELETE FROM detectorMap WHERE arm = "r" AND spectrograph = 3'
    \rm $CALIBDIR/DETECTORMAP/*r3.fits
    ingestPfsCalibs.py /work/drp --calib $CALIBDIR $DRP_PFS_DATA_DIR/detectorMap/detectorMap-sim-r3.fits --mode=copy --validity 100000 -c clobber=True

## bootstrap
    bootstrapDetectorMap.py /work/drp --calib=$CALIBDIR --rerun=hassans/r3-detectorMap --flatId visit=81879 arm=r spectrograph=3 --arcId visit=81808 arm=r spectrograph=3 -c spatialOffset=20 spectralOffset=40 matchRadius=2 readLineList.exclusionRadius=1
Stats
    bootstrap.readLineList INFO: Filtered line lists, keeping species {'ArI'}.
    bootstrap INFO: Found 229 lines in 10 traces
    bootstrap INFO: Matched 157 lines
    bootstrap INFO: Median difference from detectorMap: -0.850864,-6.565199 pixels
    bootstrap INFO: Fit 46/92 points, rms: x=0.082030 y=0.075462 total=0.039469 pixels
    bootstrap INFO: Updating detectorMap...
    bootstrap INFO: Median difference from detectorMap: -2.445870,4.506994 pixels
    bootstrap INFO: Fit 42/65 points, rms: x=0.174390 y=0.183400 total=0.046074 pixels
## ingest bootstrap
    sqlite3 $CALIBDIR/calibRegistry.sqlite3 'DELETE FROM detectorMap WHERE arm = "r" AND spectrograph = 3'
    \rm $CALIBDIR/DETECTORMAP/*r3.fits
    ingestPfsCalibs.py /work/drp --calib $CALIBDIR /work/drp/rerun/hassans/r3-detectorMap/DETECTORMAP/pfsDetectorMap-*r3.fits --mode=copy --validity 100000 -c clobber=True
