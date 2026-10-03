# AG (guider) test data

Real AG data for drp_qa's `tests/guiders`, from engineering visits of Run 30 (2026-08-31), read with
drp_qa's `pfs.drp.qa.guiders.queries` and trimmed to a few guide stars per camera.
`makeGuiderFixtures.py` makes them and says what each holds.

| File | Contents |
| --- | --- |
| `agcData-focusSweep.parquet` | `readAgcData`, visits 148266, 148270–148277: a focus sweep |
| `agcData-raster.parquet` | `readAgcData`, visits 148284–148292: a raster scan and a flux uniformity exposure |
| `agcData-allSky.parquet` | `readAgcData`, visit 148258: a 900 s all-sky exposure |
| `agcStars.parquet` | `readAGCStars` for visits 148258 and 148291, the stars in the files above |
