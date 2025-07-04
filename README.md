# FingerVeinSyn-5M-A-Million-Scale-Synthetic-Finger-Vein-Dataset-and-Benchmark

[![License](https://img.shields.io/badge/license-CC_BY_4.0-blue.svg)](LICENSE)
[![arXiv](https://img.shields.io/badge/arXiv-2506.03635-b31b1b.svg)](https://arxiv.org/abs/2506.03635)

## 📚Overview
This dataset comprises **5 million synthetic finger vein images** generated using the **FVeinSyn** framework, specifically designed to advance research in **finger vein recognition**. The primary objective is to provide a comprehensive resource for the development. This dataset is the **largest publicly available finger vein dataset** to date‌.

### ✨News ！！！ 
- **[2025.06.28] finger_shape_masks and vein_pattern_masks are now available!**
- **[2025.06.09] Annotations are now available!**
- **[2025.05.30] Dataset v1.0 officially released!**
- **[2025.05.30] Datasets will be released progressively!**


### Key Characteristics
- **Total samples**: 5 Million (Size: 300*600)
- **Unique identities**: 50,000 unique identities, per 100 samples
- **Annotations**: Finger Vein patterns (Mask), Finger shapes (Mask), joint cavities (Coordinates), and vein regions of interest (Bounding box)
- **Data format**: PNG and XML
- **Intra-class variations**: *Geometric*(Shift, Rotate, roll, and Scale), *Degradation*(Motion blur, Optical blur, Skin scattering blur and Under/over-exposure)

## ☁️⬇️Download
- [x] Raw synthetic finger vein data can available at [FingerVeinSyn-5M (Kaggle)](https://www.kaggle.com/datasets/evanwang98/fingerveinsyn-5m) [FingerVeinSyn-5M (Part Ⅱ) (Kaggle)](https://www.kaggle.com/datasets/evanwang98/fingerveinsyn-5m-part)
- [x] Annotations can available at [Annotations (Kaggle)](https://www.kaggle.com/datasets/evanwang98/fingerveinsyn-5m-part)   
- [x] Finger Shape Mask can available at [finger_shape_masks (Kaggle)](https://www.kaggle.com/datasets/evanwang98/fingerveinsyn-5m-part)   
- [x] Vein Pattern Mask can available at [vein_pattern_masks (Kaggle)](https://www.kaggle.com/datasets/evanwang98/fingerveinsyn-5m-part) 

## Dataset Structure
```
FingerVeinSyn-5M/
├── raw_images/          # Original finger images (.png)
│   ├── 00001/
│   │   ├── 00001_001_Shift.png
│   │   ├── 00001_002_Shift.png
│   │   ├── ...
│   │   └── 00001_100_Multi.png
│   ├── 00002/
│   │   ├── ...
│   ├── ...
│   └── 50000/
├── roi_images/
├── annotations/         # XML files with landmark coordinates
│   └── (Structure is the same as raw_images)
├── shape_masks/         # Binary masks of finger contours
│   └── (Structure is the same as raw_images)
├── pattern_masks/       # Extracted vein patterns
│   └── (Structure is the same as raw_images)
├── docs/                # Documentation and specifications
├── scripts/             # Sample processing scripts
└── README.md            # This document
```

## Raw Image Data Loading
The raw finger vein images can be Viewed using:

`python Viewer.py --id [ID] --sample [SampleNum] --type [VariationType]` 
```python
python Viewer.py --id 4550 --sample 6 --type Rotate
```
Image naming format: `[ID]_[SampleNum]_[VariationType].png`

## Finger Vein ROI Images Extraction
Combined with `Annotations` to extract ROI, you can perform:
```python
python roiextraction.py --idranges N
```
After execution, the *N*-identities's ROI data will be saved to the `/roi_images` folder as the same storage structure as the original image



## Annotation Data
*Example of annotation file*
```
<?xml version="1.0" encoding="UTF-8"?>
<!-- Finger vein annotation data -->
<annotation>
  <image 
    file="00002_080_Multi.png"  <!-- Source image path -->
    mask="00002_080_Multi.png"  <!-- Corresponding mask file -->
    width="600"                 <!-- Image dimensions -->
    height="300">

    <!-- Image transformation parameters -->
    <IntraVar>
      <rotation><angle>0.00</angle></rotation>  <!-- Rotation in degrees -->
      <shift>
        <x_offset>-9.00</x_offset>  <!-- Pixel offset -->
        <y_offset>-26.00</y_offset>
      </shift>
      <roll>0.00</roll>          <!-- Roll angle -->
      <scale>0.00</scale>        <!-- Scaling factor -->

      <!-- Transformation flags -->
      <IsRoll>True</IsRoll>      <!-- Roll enabled -->
      <IsShift>True</IsShift>    <!-- Shift enabled -->
      <IsRotate>False</IsRotate> <!-- Rotation disabled -->
      <IsScale>False</IsScale>   <!-- Scaling disabled -->
      <IsExposure>True</IsExposure>       <!-- Exposure adjustment -->
      <IsMotionBlur>False</IsMotionBlur>  <!-- Motion blur -->
      <IsOpticalBlur>False</IsOpticalBlur><!-- Optical blur -->
      <IsSkinScatter>False</IsSkinScatter><!-- Skin scattering -->
    </IntraVar>

    <!-- Bounding box coordinates -->
    <bbox>
      <center_x>221.50</center_x>  <!-- Box center -->
      <center_y>124.00</center_y>
      <width>479.00</width>        <!-- Box dimensions -->
      <height>121.00</height>
    </bbox>

    <!-- Anatomical landmark points -->
    <joint_points> <!-- Landmark -->
      <point><x>-6.86</x><y>126.70</y></point>  <!-- Finger root -->
      <point><x>194.57</x><y>122.85</y></point> <!-- Proximal joint cavity -->
      <point><x>370.71</x><y>127.07</y></point> <!-- Distal joint cavity -->
      <point><x>504.19</x><y>126.70</y></point> <!-- Finger tip -->
    </joint_points>
  </image>
</annotation>
```

The annotation can be Viewed using:

`python Viewer.py --id [ID] --sample [SampleNum] --type [VariationType]` 
```python
python annotationViewer.py --id 666 --sample 66 --type Multi
```
Annotation naming format: `[ID]_[SampleNum]_[VariationType].xml`


## Inter-class Variations
The dataset contains systematic variations to simulate real-world conditions:

| Variation Type       | Parameters                          |
|----------------------|-------------------------------------|
| Geometric            | Shift (±15px), Rotate (±15°), Scale (±10%) ,Roll (±15°) |
| Photometric          | Under/Over-Exposure|
| Degradation          | Motion blur, Optical blur, Shin Scatter|

|       |       |       |       |       |       |
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| <img src="FingerVeinSyn5M/raw_images/example/04551_001_Shift.png" width="120"><br><center><font size="6"><em>Shift</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_003_Shift.png" width="120"><br><center><font size="6"><em>Shift</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_005_Shift.png" width="120"><br><center><font size="6"><em>Shift</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_006_Rotate.png" width="120"><br><center><font size="6"><em>Rotate</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_008_Rotate.png" width="120"><br><center><font size="6"><em>Rotate</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_016_Rotate.png" width="120"><br><center><font size="6"><em>Rotate</em></font></center> |
| <img src="FingerVeinSyn5M/raw_images/example/04551_017_Scale.png" width="120"><br><center><font size="6"><em>Scale</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_018_Scale.png" width="120"><br><center><font size="6"><em>Scale</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_019_Scale.png" width="120"><br><center><font size="6"><em>Scale</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_022_Roll.png" width="120"><br><center><font size="6"><em>Roll</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_024_Roll.png" width="120"><br><center><font size="6"><em>Roll</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_030_Roll.png" width="120"><br><center><font size="6"><em>Roll</em></font></center> |
| <img src="FingerVeinSyn5M/raw_images/example/04551_031_OpticalBlur.png" width="120"><br><center><font size="6"><em>OpticalBlur</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_033_OpticalBlur.png" width="120"><br><center><font size="6"><em>OpticalBlur</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_035_OpticalBlur.png" width="120"><br><center><font size="6"><em>OpticalBlur</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_041_Exposure.png" width="120"><br><center><font size="6"><em>Exposure</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_042_Exposure.png" width="120"><br><center><font size="6"><em>Exposure</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_044_Exposure.png" width="120"><br><center><font size="6"><em>Exposure</em></font></center> |
| <img src="FingerVeinSyn5M/raw_images/example/04551_046_SkinScatter.png" width="120"><br><center><font size="6"><em>SkinScatter</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_049_SkinScatter.png" width="120"><br><center><font size="6"><em>SkinScatter</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_050_SkinScatter.png" width="120"><br><center><font size="6"><em>SkinScatter</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_037_MotionBlur.png" width="120"><br><center><font size="6"><em>MotionBlur</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_038_MotionBlur.png" width="120"><br><center><font size="6"><em>MotionBlur</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_039_MotionBlur.png" width="120"><br><center><font size="6"><em>MotionBlur</em></font></center> |
| <img src="FingerVeinSyn5M/raw_images/example/04551_053_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_099_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_078_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_079_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_098_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="FingerVeinSyn5M/raw_images/example/04551_085_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> |

## Mask and BBox Visualizations
|       |       |       |       |       |       |
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| <img src="mask_and_bbox visualization/04551_001_Shift.png" width="120"><br><center><font size="6"><em>Shift</em></font></center> | <img src="mask_and_bbox visualization/04551_003_Shift.png" width="120"><br><center><font size="6"><em>Shift</em></font></center> | <img src="mask_and_bbox visualization/04551_005_Shift.png" width="120"><br><center><font size="6"><em>Shift</em></font></center> | <img src="mask_and_bbox visualization/04551_006_Rotate.png" width="120"><br><center><font size="6"><em>Rotate</em></font></center> | <img src="mask_and_bbox visualization/04551_008_Rotate.png" width="120"><br><center><font size="6"><em>Rotate</em></font></center> | <img src="mask_and_bbox visualization/04551_016_Rotate.png" width="120"><br><center><font size="6"><em>Rotate</em></font></center> |
| <img src="mask_and_bbox visualization/04551_017_Scale.png" width="120"><br><center><font size="6"><em>Scale</em></font></center> | <img src="mask_and_bbox visualization/04551_018_Scale.png" width="120"><br><center><font size="6"><em>Scale</em></font></center> | <img src="mask_and_bbox visualization/04551_019_Scale.png" width="120"><br><center><font size="6"><em>Scale</em></font></center> | <img src="mask_and_bbox visualization/04551_022_Roll.png" width="120"><br><center><font size="6"><em>Roll</em></font></center> | <img src="mask_and_bbox visualization/04551_024_Roll.png" width="120"><br><center><font size="6"><em>Roll</em></font></center> | <img src="mask_and_bbox visualization/04551_030_Roll.png" width="120"><br><center><font size="6"><em>Roll</em></font></center> |
| <img src="mask_and_bbox visualization/04551_031_OpticalBlur.png" width="120"><br><center><font size="6"><em>OpticalBlur</em></font></center> | <img src="mask_and_bbox visualization/04551_033_OpticalBlur.png" width="120"><br><center><font size="6"><em>OpticalBlur</em></font></center> | <img src="mask_and_bbox visualization/04551_035_OpticalBlur.png" width="120"><br><center><font size="6"><em>OpticalBlur</em></font></center> | <img src="mask_and_bbox visualization/04551_041_Exposure.png" width="120"><br><center><font size="6"><em>Exposure</em></font></center> | <img src="mask_and_bbox visualization/04551_042_Exposure.png" width="120"><br><center><font size="6"><em>Exposure</em></font></center> | <img src="mask_and_bbox visualization/04551_044_Exposure.png" width="120"><br><center><font size="6"><em>Exposure</em></font></center> |
| <img src="mask_and_bbox visualization/04551_046_SkinScatter.png" width="120"><br><center><font size="6"><em>SkinScatter</em></font></center> | <img src="mask_and_bbox visualization/04551_049_SkinScatter.png" width="120"><br><center><font size="6"><em>SkinScatter</em></font></center> | <img src="mask_and_bbox visualization/04551_050_SkinScatter.png" width="120"><br><center><font size="6"><em>SkinScatter</em></font></center> | <img src="mask_and_bbox visualization/04551_037_MotionBlur.png" width="120"><br><center><font size="6"><em>MotionBlur</em></font></center> | <img src="mask_and_bbox visualization/04551_038_MotionBlur.png" width="120"><br><center><font size="6"><em>MotionBlur</em></font></center> | <img src="mask_and_bbox visualization/04551_039_MotionBlur.png" width="120"><br><center><font size="6"><em>MotionBlur</em></font></center> |
| <img src="mask_and_bbox visualization/04551_053_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="mask_and_bbox visualization/04551_099_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="mask_and_bbox visualization/04551_078_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="mask_and_bbox visualization/04551_079_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="mask_and_bbox visualization/04551_098_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> | <img src="mask_and_bbox visualization/04551_085_Multi.png" width="120"><br><center><font size="6"><em>Multi</em></font></center> |


## Citation
If you use this dataset in your research, please cite:
```
@misc{wang2025fingerveinsyn5mmillionscaledatasetbenchmark,
      title={FingerVeinSyn-5M: A Million-Scale Dataset and Benchmark for Finger Vein Recognition}, 
      author={Yinfan Wang and Jie Gui and Baosheng Yu and Qi Li and Zhenan Sun and Juho Kannala and Guoying Zhao},
      year={2025},
      url={https://arxiv.org/abs/2506.03635}, 
}
```

## Contact
For questions or reporting issues:
- *Yinfan Wang*, *Jie Gui*
- Email: 230239767@seu.edu.cn
