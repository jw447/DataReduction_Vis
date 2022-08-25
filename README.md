# DataReduction_Vis

AD/AE for submission to DRBSD22: Analyzing the Impact of Lossy Data Reduction on Volume Rendering of Cosmology Data.

### Requirements 

- Python 3.8
- Pytorch 1.12.1
- Scikit-image 0.19.3
- Opencv-python 4.6.0.66
- Opencv-contrib-python 4.6.0.66
- Piq 0.7.0
- Lmdb 1.3.0
- Imageio 2.9.0
- Pillow 7.1.2

Required modules can be installed via ` pip3 install -r requirements.txt `


### ForeSight configurations files for compression experiments

In compression experiments, we specify the configurations, especially the absolute error bound, for each compressor and each field into a JSON file. Those JSON files are contained in **foresight_input**. For example, `nyx_img_compression_sz_abs_baryon_density.json` indicates the configuration JSON file for SZ to compress *Baryon_density*.

```bash
./CBench -i nyx_img_compression_sz_abs_baryon_density.json
```

### ParaView scripts for volume rendering

The scripts to generate volume rendering visualization using ParaView are listed under **visualization_scripts**.

```bash
PYTHON ... img_baryon_density_ReOr.py
```

### Image difference computation

The `getImgDiff.py` is used to calculate the absolute difference between testing images and reference images, which can be found in **iqa_metrics**. The testing images are contained in **Test** and reference images are contained in **Reference**. The imgDiff images will be output to **imgDiff**.

```bash
cd iqa_metrics
mkdir -p imgDiff
python getImgDiff.py
```

### Image quality assessment (IQA) metrics computation

The scripts used to compute the IQA metrics can be found in **iqa_metrics**. All IQA metrics can be computed using `getIQA.py`, except L2PIPS and DeepQA. Calculated IQA metrics values are organized in **iqa**.

```bash
# for all the metrics beside L2PIPS and DeepQA
# output: iqa/img_{compressor}_{field_name}.csv
cd iqa_metrics
python getIQA.py 
```

L2PIPS and DeepQA, two DNN-based IQA metrics, require external codebases as well as trained DNN models to compute. Those codebases are contained under **iqa_metrics/models**, which are fetched from

- L2PIPS: https://github.com/YuLvS/L2PIPS
- DeepQA: https://github.com/anse3832/DeepQA-modified

Calculated metrics values are output to `output_deepQA.csv` and `output_L2PIPS.csv`.

```bash
# for DeepQA metric
# output: output_deepQA.csv
cd iqa_metrics
python test_DeepQA.py 

# for L2PIPS metric
# output: test_L2PIPS
cd iqa_metrics
python test_L2PIPS.py 
```

**Note**: in order to run for L2PIPS, a previously trained DNN model needs to be downloaded and put into iqa_metrics/models/L2PIPS/trained_model. The trained model can be found [here](https://drive.google.com/drive/folders/1ClTLIOJrrXX5i_h-EZU9LkXEh5TDAAuc?usp=sharing).
