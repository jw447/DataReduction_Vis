# DataReduction_Vis

Submission to DRBSD22: Analyzing the Impact of Lossy Data Reduction on Volume Rendering of Cosmology Data

### Compression configurations for ForeSight

In compression experiments, we specify the configurations, especially the absolute error bound, for each compressor and each field into a JSON file. Those JSON files are listed under **foresight_input**. For example, *nyx_img_compression_sz_abs_baryon_density.json*  indicates the configuration JSON file for *SZ* to compress *Baryon_density*.

```bash
./CBench -i nyx_img_compression_sz_abs_baryon_density.json
```

### Volume rendering for Nyx scientific application

The scripts to generate volume rendering visualization using ParaView are listed under **visualization_scripts**.

```bash
PYTHON ... img_baryon_density_ReOr.py
```

### ImgDiff calculation

The script to calculate the absolute difference between testing images and reference images can be found in **iqa_metrics**. The testing images are contained in **Test** and reference images are contained in **Reference**. The imgDiff images will be output to **imgDiff** folder.

```bash
cd iqa_metrics
mkdir -p imgDiff
python getImgDiff.py
```

### Image quality assessment (IQA) metrics computation

In order to computet he IQA metrics used in this work (listed below), the scripts 

| SSIM | MS-SSIM | FSIM | DSS | SR-SIM | HaarPSI | VSI | MDSI | MS-GMSD | DISTS | PieAPP | LPIPS | **L2PIPS** | **DeepQA** |
|:----:|:-------:|:----:|:---:|:------:|:-------:|:---:|:----:|:-------:|:-----:|:------:|:-----:|:----------:|:----------:|
