# M.Sc-Disserrtation-Code

## General Linear Model
The code used to run the GLM analysis is the "glm_final.py" file. The file may be run via the command line and may perform two separate GLM analysis. Firslty, it can perform a subject level "first-level" analysis. In addition to this it may also perform a group-level "second-level analysis". The code also has the capability of spatially normalising the first-level results to MNI space which is required to perform the second level analysis. 

### Example uses: first-level analysis
In this example, a first level analysis is performed on subject "20". The required arguments are the path to the preprocessed .nii.gz fMRI file, the path to the T1-weighted structural file, and the path to the events.tsv file outputted by PyschoPy during the experiment. In addition, the argument -vv specifies the voxel size of the pulse sequence used.
```
python3 glm_final first-level -pf $path_to_fmri_file$ -ps $path_to_T1w_image$ -pe $path_to_events.tsv$ -vv 1.8 -sub 20
```
### Example uses: first-level analysis with smoothing
In this example, we perform the same first level analysis but we also smoothen the data with a FWHM of 4mm.
```
python3 glm_final first-level -pf $path_to_fmri_file$ -ps $path_to_T1w_image$ -pe $path_to_events.tsv$ -vv 1.8 -sub 20 -sm -fw 4
```
Note that the first level analysis outputs the statistical t-maps required for the second-level analysis.

### Example used: normalisation to MNI space
In order to perform a second level analysis, the t-maps need to be spatially normalised to a common space e.g. MNI. To spatially normalise with this code, the path of the statistical maps, the transformation file outputted by for example fMRIprep (.h5 file), and the reference T1-weighted image normalised to MNI space of the volunteer. The algorithm will normalise using trilinear interpolation.
```
python3 glm_final normalise --s_maps $path_to_t-maps$ --transform $path_to_h5_file$ --reference_img $path_t1w_to_mni_img$
```
### Example used: second-level analysis
To perform a second-level analysis, the paths to the spatially normalised t-maps need to be passed through and the voxel volume of the image as required arguments. In the below example, the t-maps of three volunteers are passed. In addition, a second-level smoothing operation with a FWHM of 4mm is also performed using the -slsm command in the following example:
```
python3 glm_final second-level --s_maps $path_to_norm_t-map1$ $path_to_norm_t-map2$ $path_to_t-norm_map3$ -vv 1.8 -slsm 4
```

