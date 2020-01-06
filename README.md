# Crack Segmentation

For cloning the repository, please use the recursive flag to also clone the submodules:
```
git clone https://github.com/khanhha/crack_segmentation.git --recursive
```

## Model
The trained model can be obtained by:
```
cd models
wget https://cloud.uni-weimar.de/s/m5KpTHomWjnyGQb/download -O model_weights_cracknausnet.pt
```

## Inference
In order to run inference on one image, please use the provided bash script
```
bash run_inference.sh
```
or apply, where each argument should be self-exanatory:
```
python inference.py \
-model_path ./models/model_weights_cracknausnet.pt \
-image_path ./uav75/test_img/DSC00595.jpg \
-out_path ./results/DSC00595.jpg \
-device cuda:0
```

## Evaluation
Before running the evaluation you have to make sure that the submodule ```evaluation``` was properly cloned. To run the evaluation use:
```
bash run_evaluation.sh
```
or run directly from command line:
```
python evaluation/semseg_evaluator.py \
--pred_path ./uav_results \
--true_path ./uav75/test_lab \
--show_pr_curve
```
The evaluation offers a clear interface: ```--pred_path``` refers to a folder containing probability maps/heatmaps (range [0;1]) as images. The argument ```--true_path``` refers to the ground truth stored as images. To display the precision-recall-curve set the flag ```--show_pr_curve```.

## Datasets
Apart from the UAV75 dataset, other datasets were used for training. Please refer to:
- CrackTree260: https://sites.google.com/site/qinzoucn/
- CRKWH100: https://sites.google.com/site/qinzoucn/
- Stone311: https://sites.google.com/site/qinzoucn/
- CrackForest: https://github.com/cuilimeng/CrackForest-dataset
- CRACK500: https://github.com/fyangneil/pavement-crack-detection
- DeepCrack: https://github.com/yhlleo/DeepCrack

## Submodules
- TernausNet: hosts the used architecture
- UAV75: hosts the used dataset
- Evaluation: hosts the evaluation script
- Patcher
- Filter (to come...)


## Drawbacks
- Overproportionally large encoder (VGG16)
- Generalizability to other concrete surfaces (with possibly different planking patterns) not assessed
- Still sensitive to planking patterns
- Applicable only to smaller crack (i.e. cracks lesser than 8?->check pixels wide)
- Presumably limited applicability of the TernausNet for problems with 3+ classes



## Reference
For reference and citation please use (will be shortly put into final format):

Benz, C., Debus, P., Ha, H.-K. & Rodehorst, V. (2019): Crack Segmentation on UAS-based Imagery using Transfer Learning. *Image and Vision Computing New Zealand*, *IVCNZ*, Dunedin.

See: [http://ivcnz2019.otago.ac.nz/](http://ivcnz2019.otago.ac.nz/)
