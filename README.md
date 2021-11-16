# KE-R-CNN

Official implementation of **KE-R-CNN** for part-level attribute parsing.

## Installation
- pytorch 1.8.1
- python 3.7.0
- [mmdetection 2.17.0](https://mmdetection.readthedocs.io/en/latest/get_started.html#installation)
- [fashionpeida-API](https://github.com/KMnP/fashionpedia-api)
- einops

## Dataset
You need to download the datasets and annotations follwing this repo's formate

- [FashionPedia](https://github.com/cvdfoundation/fashionpedia)
- [knowledge_matrix](https://drive.google.com/file/d/1m1ycDqK6wvdvlLwz7jyyAuIGjyhdggBe/view?usp=sharing)

Make sure to put the files as the following structure:

```
  ├─data
  │  ├─fashionpedia
  │  │  ├─train
  │  │  ├─test
  │  │  │─instances_attribute_train2020.json
  │  │  │─instances_attribute_val2020.json
  |  |  |─train_attr_knowledge_matrix.npy
  |
  ├─work_dirs
  |  ├─KE-RCNN_r50_1x
  |  |  ├─latest.pth
  ```

## Results and Models

|  Backbone    |  LR  | AP_iou/AP_iou+f1 | AP_mask_iou/AP_mask_iou+f1 | DOWNLOAD |
|--------------|:----:|:----------------:|:--------------------------:|:--------:|
|  R-50        |  1x  | 41.9/39.1        | 37.5/36.2                  |[model](https://drive.google.com/file/d/1-m83sJcu9fsRNE4pNTBLmkOB8cKhPyCK/view?usp=sharing)|
|  R-101       |  1x  | 43.8/39.9        | 38.2/36.0                  |[model](https://drive.google.com/file/d/1Zqa7ziBKUe3-t419dsLq6ihtYUfFLHhr/view?usp=sharing)|
|  Cascade-R-50|  1x  | 44.0/41.0        | 37.5/36.5                  |[model](https://drive.google.com/file/d/1ze5lPXf83PlVEWN6WfdLsOaxDdJkvZHr/view?usp=sharing)|
|  Swim-tiny   |  1x  | 45.0/41.5        | 40.6/38.6                  |[model](https://drive.google.com/file/d/1Y_yVRp7G6E07Mty8TIEWJe7a4dQXl44E/view?usp=sharing)|

## Evaluation
```
# inference
CUDA_VISIBLE_DEVICES=0,1,2,3,4,5,6,7 ./tools/dist_test.sh configs/KE-RCNN/KE-RCNN_r50_1x.py work_dirs/KE-RCNN_r50_1x/latest.pth 8 --format-only --eval-options "jsonfile_prefix=./KE-RCNN_r50_1x_val_result"

# eval, noted that should change the json path produce by previous step.
python eval/fashion_eval.py
```

## Training

Coming soon...