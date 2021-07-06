# License Plate Detection via Information Maximization (TITS-LPST)

This is the official website for "License Plate Detection via Information Maximization (submitted to T-ITS 2020)", which is a newly built real-world dataset for license plate detection and scene text detection.
- 9.7k+ images and 110k+ instances
- Scenes: **traffic** and **drone**, Tasks: **license plate detection** and **scene text (excluding license plate) detection**
- **Variations in tilt degrees**: Horizontal tilt degree (15 ~ 45 degrees) and vertical tilt degree (15 ~ 45 degrees).
- **Variations in distance**: The distance from the license plate to the camera location is relatively diverse.
- **Variations in blur**: Blurry image due to motion blur and hand jitter while capturing images.
- If you are interested in license plate detection, please refer to [our paper] or [our github project](https://github.com/brightyoun/TITS-LPST).


#### Younkwan Lee, Jihyo Jeon, Yeongmin Ko, Moongu Jeon, Witold Pedrycz

## Table of Contents
0. [Abstract](#0)
1. [Introduction](#1)  
2. [License Plate Detection Benchmarks](#2)  
   2.1 [TJU-DHD-traffic](#2.1)  
   2.2 [TJU-DHD-campus](#2.2)   
4. [Benchmark](#4)  
   4.1 [TJU-DHD-traffic](#4.1)  
   4.2 [TJU-DHD-campus](#4.2)   
   4.3 [TJU-DHD-pedestrian](#4.3) 
5. [Citation](#5)  
6. [Evaluation on the test set](#6) 
7. [Contact](#7) 

## Abstract <a name="0"></a>
License plate (LP) detection in the wild remains challenging due to the diversity of environmental conditions.  Nevertheless,  prior solutions have focused on controlled environments,  such as when  LP  images frequently emerge as from an approximately frontal viewpoint and without scene text which might be mistaken for an LP. However, even for state-of-the-art object detectors, their detection performance is not satisfactory for real-world environments, suffering from various types of degradation. To solve these problems, we propose a novel end-to-end framework for robust LP detection, designed for such challenging settings. Our contribution is threefold:  (1) A novel information-theoretic learning that takes advantage of a shared encoder, an LP detector and a scene text detector (excluding LP) simultaneously; (2) Localization refinement for generalizing the bounding box regression network to complement ambiguous detection results; (3) a large-scale, comprehensive dataset, LPST-110K, representing real-world unconstrained scenes including scene text annotations. Computational tests show that the proposed model outperforms other state-of-the-art methods on a variety of challenging datasets.License plate (LP) detection in the wild remains challenging due to the diversity of environmental conditions.  Nevertheless,  prior solutions have focused on controlled environments,  such as when  LP  images frequently emerge as from an approximately frontal viewpoint and without scene text which might be mistaken for an LP. However, even for state-of-the-art object detectors, their detection performance is not satisfactory for real-world environments, suffering from various types of degradation. To solve these problems, we propose a novel end-to-end framework for robust LP detection, designed for such challenging settings. Our contribution is threefold:  (1) A novel information-theoretic learning that takes advantage of a shared encoder, an LP detector and a scene text detector (excluding LP) simultaneously; (2) Localization refinement for generalizing the bounding box regression network to complement ambiguous detection results; (3) a large-scale, comprehensive dataset, LPST-110K, representing real-world unconstrained scenes including scene text annotations. Computational tests show that the proposed model outperforms other state-of-the-art methods on a variety of challenging datasets.


## 1. Introduction <a name="1"></a>

Object detection research has attracted great interest in recent years, with models being applied widely in many traffic-related applications. A variety of methods have demonstrated high accuracy in detecting license plates (LP) under controlled settings. While existing detectors successfully applied to the LP detection problem, many key challenges still remain in \textit{unconstrained wild scenarios}. For example, real-world LP detection causes the following problems: modifications of prior settings to adapt to wild, incorrect detection results, ambiguity in classifying objects associated with scene text, low-quality visual data, uneven lighting, motion blur, and others. However, such scenarios are becoming increasingly common and gaining significant popularity in a variety of applications, including civil security, crowd analytics, law enforcement, and street view images. Despite being the most common scenario, LP benchmarks still do not consider real-world cases, and therefore many problems are not adequately addressed. As a result, state-of-the-art detectors struggle with these images. we propose an end-to-end framework which is composed of a single shared feature encoder and two parallel detection branches. The single shared encoder learns a global feature across all detection tasks (LP and non-LP respectively). More specifically, due to non-LP objects (scene text but not LP), our framework is divided into 1) LP detection network and 2) non-LP detection network. Different from traditional LP detection models, we explicitly prevent learning of non-LP objects. To this end, we bring a novel information-theoretic loss to minimize mutual information between the embedding feature and non-LP distribution that interferes with LP detection. We collect a new large-scale dataset, LPST-110K, containing images captured from unconstrained scenes. To the best of our knowledge, LPST-110K is the first dataset to address LP and scene text simultaneously for LP detection. By evaluating state-of-the-art detection models on LPST-110K, we demonstrate the accuracy improvement of our proposed model compared with other approaches.

## 2. License Plate Detection Benchmarks <a name="2"></a>

| name       | \#images               | \#instances               | \#LP instances/Image  | \#ST instances/Image     | \#Variations in tilt degrees. | \#Variations in distance. |  \#Variations in blur. |
| :--------- | :--------------------: | :-----------------------: | :-------------------: | :----------------------: | :---------------------------: | :---------------------------: | :---------------------------: |
| AOLP       |         2,049          |          2,049            |        1              |         1                | ✓ | ✗ | ✓ |
| SSIG       |         2,000          |          8,683            |        4.34           |         4.34             | ✗ | ✓ | ✗ |
| PKU        |         3,977          |          4,389            |        1.10           |         1.10             | ✗ | ✗ | ✗ |
| UFPR       |         4,500          |          4,500            |        1              |         1                | ✗ | ✓ | ✓ |
| CD-HARD    |         102            |          102              |        1              |         1                | ✓ | ✓ | ✗ |
| CCPD       |         250K           |          250K             |        1              |         1                | ✓ | ✓ | ✓ |
| **LPST-110K**  |         9,795        |          110K             |        **5.21**         |         **11**       | ✓ | ✓ | ✓ |
 
#### 2.1 LPST-110K <a name="2.1"></a>
* training & validation set:
    * images:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/ERPTtJ9Qf3hHnKn9JQc9_y0B5uaq6qXjnF4U--2wiSTjRw?e=aarX3v)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1eLxfl19LVLy9k-DrqTOYvg)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_traffic_trainval_images.zip)
    * annotations:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EY0m5aX84EJFnquyCE8KSp8BiZKTlNHySbdJ0QG-nE2XTQ?e=Abpvgz)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1xFhMwQgpqk1QILwXS_dR2g)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_traffic_trainval_annos.zip)
* test set:
    * images:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EbkVOGVzsoRIhR6u73iAv44BN3n9geqp3R-eTJeZCJen-w?e=az00He)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1b1iR8eujY28qm-pH8rHV-A)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_traffic_test_images.zip)
    * imageinfo:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EfuzQvR7qrhAi8oDMy5PheUBvxSL539oua1kD6g130DChg?e=yOhBGM)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1Np079urN0uQmybBM4RriZA)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_traffic_test_imageinfo.zip)
* evaluation tools:
  [cocoapi](https://github.com/cocodataset/cocoapi)

#### 2.2 TJU-DHD-campus <a name="2.2"></a>
(The training imageset is too large, thus is ziped as a 4-part archive.
One should download all of them and open the `.zip.001` using your favorite zip file extractor.)
* training & validation set:
    * training images-1:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EQOf_tTaDz9AtGBA7xXZdMYBmGgEN3wI6pYxdj_sqU9RaA?e=IAa4z4)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1aar9GAbityEBMMEnXEwbOA)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_campus_train_images.zip.001)
    * training images-2:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EYdb15b5s3hOm_2EWc_uLn8BtpzXnpZJLVRIH6HdbXfbVw?e=hHJNon)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1xWDiok5DTVT8HEMK09DPiA)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_campus_train_images.zip.002)
    * training images-3:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EatVjZJ4uJZGm3OOvdbjheMB6dIOlDumkbhVSMqNZFjSDQ?e=5a9C63)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1gUQs6XdUU7fczaydtLPBSg)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_campus_train_images.zip.003)
    * training images-4:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/ERJGIKSOjrVGodjyAtYWOBIBz7Yn3EGGjmtMRDpG9eFlHQ?e=x8MASb)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1PncIpCpS_En9Ka0aD6-_lA)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_campus_train_images.zip.004)
    * validation images:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EUHmv-SilRtPlKVuV7TTYlUB24CVeAi9HPto9ZJ6m61kpA?e=aREmy0)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1WgbIEXIbGHjh6jBjh_l37A)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_campus_val_images.zip)
    * annotations:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EfJ_SbAK2itJk8kyLBF9ER8BqO0faVumeWn8rPYMkGpqNw?e=Ckc2jn)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1JKnGky_Qzk3QluURgFxCBQ)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_campus_trainval_annos.zip)
* test set:
    * images:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EZZe-4Atw8tEkPdTToNXEboBtdORbKqz2j6asah_hgUgAA?e=ABQibv)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1I33BMKvU9WP_nC64wM1hHw)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_campus_test_images.zip)
    * imageinfo:
      [OneDrive](https://tjueducn-my.sharepoint.com/:u:/g/personal/hqsun_tju_edu_cn/EQJpKUI5UUxBuM6ZQGLCLNwBEfGX0tgBR_JyZhAyRp4YYw?e=f6Zrxz)
      / [BaiduNetDisk (code: biit)](https://pan.baidu.com/s/1LmJRobdmYoqWv1NAqwKcsg)
      / [backup](http://vi.tju.edu.cn/public/dhd_dataset/dhd_campus_test_imageinfo.zip)
* evaluation tools:
  [cocoapi](https://github.com/cocodataset/cocoapi)


## 4. Benchmark <a name="4"></a>

#### 4.1 TJU-DHD-traffic <a name="4.1"></a>

* Results on validation

  | method       | backbone | input size |  AP   | AP@0.5 | AP@0.75 | AP_s  | AP_m  | AP_l  |
  | :----------- | :------: | :--------: | :---: | :----: | :-----: | :---: | :---: | :---: |
  | RetinaNet    | ResNet50 |  1333x800  | 53.5  |  80.9  |  60.0   | 24.0  | 50.5  | 68.0  |
  | FCOS         | ResNet50 |  1333x800  | 53.8  |  80.0  |  60.1   | 24.6  | 50.6  | 68.8  |
  | FPN          | ResNet50 |  1333x800  | 55.4  |  83.4  |  63.0   | 30.4  | 52.2  | 68.2  |
  | Cascade RCNN | ResNet50 |  1333x800  | 57.9  |  82.7  |  66.6   | 32.6  | 54.4  | 71.4  |

#### 4.2 TJU-DHD-campus <a name="4.2"></a>

* Results on validation

  | method       | backbone | input size |  AP   | AP@0.5 | AP@0.75 | AP_t  | AP_s  | AP_l  | AP_l  |
  | :----------- | :------: | :--------: | :---: | :----: | :-----: | :---: | :---: | :---: | :---: |
  | RetinaNet    | ResNet50 |  1333x800  | 48.4  |  79.3  |  52.4   |  4.7  | 27.3  | 56.2  | 73.8  |
  | FCOS         | ResNet50 |  1333x800  | 49.3  |  73.8  |  53.8   |  5.6  | 29.6  | 55.9  | 74.3  |
  | FPN          | ResNet50 |  1333x800  | 52.4  |  77.5  |  58.4   |  8.5  | 37.4  | 58.6  | 74.9  |
  | Cascade RCNN | ResNet50 |  1333x800  | 55.1  |  77.6  |  60.9   | 10.8  | 40.1  | 61.2  | 78.8  |

#### 4.3 TJU-DHD-pedestrian <a name="4.3"></a>

* Miss rate with same-scene evaluation

  | method |  R/RS/HO/R+HO/A (TJU-Ped-campus)  | R/RS/HO/R+HO/A (TJU-Ped-traffic)  |
  | :----- | :---------------------------: | :---------------------------: |
  | FPN    | 27.92/73.14/67.52/35.67/38.08 | 22.30/35.19/60.30/26.71/37.78 |

* Miss rate with cross-scene evaluation

  | method | R/R+HO (TJU-Ped-campus -> traffic) | R/R+HO (TJU-Ped-traffic -> campus) |
  | :----- | :-----------------------------------------: | :---------------------------------------------: |
  | FPN    |              30.62 / 33.89               |               42.08 / 50.55               |

## 5. Citation <a name="5"></a>

If this project help your research, please consider to cite our github page.

## 6. Evaluation on the test set <a name="6"></a>

Ablation studies can be conducted on the validation set.
If you would like to evaluate your model on the test set, you can send us (connor#tju.edu.cn, replace `#` with `@`) your detection results in the `json` format.

## 7. Contact <a name="7"></a>

If you have any questions or want to add your results, please feel free to [contact us](brightyoun@gist.ac.kr).
