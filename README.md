# Real-time multi-object tracking and segmentation using Yolov8

## Speed Estimation (Velocity Estimation)

```bash
$ python speed.py --yolo-weights yolov8n.pt     # bboxes only
                                 yolov8n-seg.pt  # bboxes + segmentation masks
```


<div align="center">
  <p>
  <img src="trackers/strongsort/results/track_all_seg_1280_025conf.gif" width="400"/>
  </p>
  <br>
  <div>
  <a href="https://github.com/mikel-brostrom/Yolov5_DeepSort_Pytorch/actions"><img src="https://github.com/mikel-brostrom/Yolov5_DeepSort_Pytorch/workflows/CI%20CPU%20testing/badge.svg" alt="CI CPU testing"></a>
  <br>  
  <a href="https://colab.research.google.com/drive/18nIqkBr68TkK8dHdarxTco6svHUJGggY?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a>
<a href="https://doi.org/10.5281/zenodo.7629840"><img src="https://zenodo.org/badge/DOI/10.5281/zenodo.7629840.svg" alt="DOI"></a>
  </div>
</div>


## Introduction

This repository contains a highly configurable two-stage-tracker that adjusts to different deployment scenarios. It can jointly perform multiple object tracking and instance segmentation (MOTS). The detections generated by [YOLOv8](https://github.com/ultralytics/ultralytics), a family of object detection architectures and models pretrained on the [COCO](https://arxiv.org/abs/1405.0312) dataset, are passed to the tracker of your choice. Supported ones at the moment are: [BoTSORT](https://arxiv.org/abs/2206.14651) [OSNet](https://github.com/KaiyangZhou/deep-person-reid)[](https://arxiv.org/abs/1905.00953), [StrongSORT](https://github.com/dyhBUPT/StrongSORT)[](https://arxiv.org/abs/2202.13514) [OSNet](https://github.com/KaiyangZhou/deep-person-reid)[](https://arxiv.org/abs/1905.00953), [OCSORT](https://github.com/noahcao/OC_SORT)[](https://arxiv.org/abs/2203.14360) and [ByteTrack](https://github.com/ifzhang/ByteTrack)[](https://arxiv.org/abs/2110.06864). They can track any object that your Yolov8 model was trained to detect.

## Why using this tracking toolbox?

Everything is designed with simplicity and flexibility in mind. We don't hyperfocus on results on a single dataset, we prioritize real-world results. If you don't get good tracking results on your custom dataset with the out-of-the-box tracker configurations, use the `evolve.py` script for tracker hyperparameter tuning.

## Installation

```
git clone --recurse-submodules https://github.com/ryuhat/yolov8_tracking.git  # clone recursively
cd yolov8_tracking
pip install -r requirements.txt  # install dependencies
```

<details>
<summary>Tutorials</summary>

* [Yolov5 training (link to external repository)](https://github.com/ultralytics/yolov5/wiki/Train-Custom-Data)&nbsp;
* [Deep appearance descriptor training (link to external repository)](https://kaiyangzhou.github.io/deep-person-reid/user_guide.html)&nbsp;
* [ReID model export to ONNX, OpenVINO, TensorRT and TorchScript](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/ReID-multi-framework-model-export)&nbsp;
* [Evaluation on custom tracking dataset](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/How-to-evaluate-on-custom-tracking-dataset)&nbsp;
* Inference acceleration with Nebullvm
  * [Yolov5](https://colab.research.google.com/drive/1J6dl90-zOjNNtcwhw7Yuuxqg5oWp_YJa?usp=sharing)&nbsp;
  * [ReID](https://colab.research.google.com/drive/1APUZ1ijCiQFBR9xD0gUvFUOC8yOJIvHm?usp=sharing)&nbsp;
  
  </details>
  
<details>
<summary>Experiments</summary>

In inverse chronological order:

* [Evaluation of the params evolved for first half of MOT17 on the complete MOT17](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/Evaluation-of-the-params-evolved-for-first-half-of-MOT17-on-the-complete-MOT17)

* [Segmentation model vs object detetion model on MOT metrics](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/Segmentation-model-vs-object-detetion-model-on-MOT-metrics)
  
* [Effect of masking objects before feature extraction](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/Masked-detection-crops-vs-regular-detection-crops-for-ReID-feature-extraction)
  
* [conf-thres vs HOTA, MOTA and IDF1](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/conf-thres-vs-MOT-metrics)

* [Effect of KF updates ahead for tracks with no associations on MOT17](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/Effect-of-KF-updates-ahead-for-tracks-with-no-associations,-on-MOT17)

* [Effect of full images vs 1280 input to StrongSORT on MOT17](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/Effect-of-passing-full-image-input-vs-1280-re-scaled-to-StrongSORT-on-MOT17)

* [Effect of different OSNet architectures on MOT16](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/OSNet-architecture-performances-on-MOT16)

* [Yolov5 StrongSORT vs BoTSORT vs OCSORT](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/StrongSORT-vs-BoTSORT-vs-OCSORT)
    * Yolov5 [BoTSORT](https://arxiv.org/abs/2206.14651) branch: https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/tree/botsort

* [Yolov5 StrongSORT OSNet vs other trackers MOT17](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/MOT-17-evaluation-(private-detector))&nbsp;

* [StrongSORT MOT16 ablation study](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/Yolov5DeepSORTwithOSNet-vs-Yolov5StrongSORTwithOSNet-ablation-study-on-MOT16)&nbsp;

* [Yolov5 StrongSORT OSNet vs other trackers MOT16 (deprecated)](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/wiki/MOT-16-evaluation)&nbsp;

  </details>
  
<details>
<summary>Custom object detection architecture</summary>

The trackers provided in this repo can be used with other object detectors than Yolov8. Make sure that the output of your detector has the following format:

```bash
(x1,y1, x2, y2, obj, cls0, cls1, ..., clsn)
```

pass this directly to the tracker here:

https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/blob/a4bc0c38c33023fab9e5481861d9520eb81e28bc/track.py#L189

</details>

## Tracking

```bash
$ python track.py --yolo-weights yolov8n.pt     # bboxes only
                                 yolov8n-seg.pt  # bboxes + segmentation masks
```

<details>
<summary>Tracking methods</summary>

```bash
$ python track.py --tracking-method strongsort
                                    ocsort
                                    bytetrack
                                    botsort
```
  
</details>

<details>
<summary>Tracking sources</summary>

Tracking can be run on most video formats

```bash
$ python track.py --source 0  # webcam
                           img.jpg  # image
                           vid.mp4  # video
                           path/  # directory
                           path/*.jpg  # glob
                           'https://youtu.be/Zgi9g1ksQHc'  # YouTube
                           'rtsp://example.com/media.mp4'  # RTSP, RTMP, HTTP stream
```

</details>

<details>
<summary>Select Yolov8 model</summary>

There is a clear trade-off between model inference speed and overall performance. In order to make it possible to fulfill your inference speed/accuracy needs you can select a Yolov5 family model for automatic download. These model can be further optimized for you needs by the [export.py](https://github.com/ultralytics/yolov5/blob/master/export.py) script

```bash


$ python track.py --source 0 --yolo-weights yolov8n.pt --img 640
                                            yolov8s.tflite
                                            yolov8m.pt
                                            yolov8l.onnx 
                                            yolov8x.pt --img 1280
                                            ...
```
  
</details>

<details>
<summary>Select ReID model</summary>

Some tracking methods combine appearance description and motion in the process of tracking. For those which use appearance, you can choose a ReID model based on your needs from this [ReID model zoo](https://kaiyangzhou.github.io/deep-person-reid/MODEL_ZOO). These model can be further optimized for you needs by the [reid_export.py](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/blob/master/reid_export.py) script

```bash


$ python track.py --source 0 --reid-weights osnet_x0_25_market1501.pt
                                            mobilenetv2_x1_4_msmt17.engine
                                            resnet50_msmt17.onnx
                                            osnet_x1_0_msmt17.pt
                                            ...
```

</details>
  
<details>
<summary>Filter tracked classes</summary>

By default the tracker tracks all MS COCO classes.

If you want to track a subset of the classes that you model predicts, add their corresponding index after the classes flag,

```bash
python track.py --source 0 --yolo-weights yolov8s.pt --classes 16 17  # COCO yolov8 model. Track cats and dogs, only
```

[Here](https://tech.amikelive.com/node-718/what-object-categories-labels-are-in-coco-dataset/) is a list of all the possible objects that a Yolov8 model trained on MS COCO can detect. Notice that the indexing for the classes in this repo starts at zero

</details>

<details>
<summary>Updates with predicted-ahead bbox in StrongSORT</summary>
  
If your use-case contains many occlussions and the motion trajectiories are not too complex, you will most certainly benefit from updating the Kalman Filter by its own predicted state. Select the number of predictions that suits your needs here:

https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/blob/b1da64717ef50e1f60df2f1d51e1ff91d3b31ed4/trackers/strong_sort/configs/strong_sort.yaml#L7

Save the trajectories to you video by:

```bash
python track.py --source ... --save-trajectories --save-vid
```

<div align="center">
<p>
<img src="trackers/strong_sort/results/preds_example.gif" width="400"/> 
</p>
</div>

</details>

<details>
<summary>MOT compliant results</summary>
  
Can be saved to your experiment folder `runs/track/<yolo_model>_<deep_sort_model>/` by 

```bash
python track.py --source ... --save-txt
```

</details>

<details>
<summary>Tracker hyperparameter tuning</summary>

We use a fast and elitist multiobjective genetic algorithm for tracker hyperparameter tuning. By default the objectives are: HOTA, MOTA, IDF1. Run it by

```bash
$ python evolve.py --tracking-method strongsort --benchmark MOT17 --n-trials 100  # tune strongsort for MOT17
                   --tracking-method ocsort     --benchmark <your-custom-dataset> --objective HOTA # tune ocsort for maximizing HOTA on your custom tracking dataset
```

The set of hyperparameters leading to the best HOTA result are written to the tracker's config file.

</details>

<!-- ## Contact 

For Yolov8 tracking bugs and feature requests please visit [GitHub Issues](https://github.com/mikel-brostrom/Yolov5_StrongSORT_OSNet/issues). 
For business inquiries or professional support requests please send an email to: yolov5.deepsort.pytorch@gmail.com -->
