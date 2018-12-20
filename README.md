# Adaptive Temporal Encoding Network for Video Instance-level Human Parsing
By Qixian Zhou, Xiaodan Liang, Ke Gong, Liang Lin (ACM MM18)
[![Video demo](demo.gif)](http://www.sysu-hcp.net/wp-content/uploads/2018/10/video_human_parsing_demo.mp4)
[complete video demo](http://www.sysu-hcp.net/wp-content/uploads/2018/10/video_human_parsing_demo.mp4)

## Requirements
Python3, TensorFlow 1.3+, Keras 2.0.8+

## Dataset
The model is trained and evaluated on our proposed [VIP dataset](http://sysu-hcp.net/lip/video_parsing.php) for video instance-level human parsing. Please check it for more dataset details. VIP dataset contains 404 video sequences, including 304 sequences for training set, 50 sequences for validation set and 50 sequences for test set. For every 25 consecutive frames in each video, one frame is annotated densely with pixel-wise semantic part categories and instance-level identification. We release the source videos, frames and the fine annotations for training and validation set. You can evaluate the performance of your model on validation set with our released evaluation code. Also, you can upload the results on test set to our [evaluation server](http://www.sysu-hcp.net/lip/vparsing_lb.php?type=0) to get your model score and ranking on leaderboard.

## Models
Models are released on [OneDrive](https://1drv.ms/u/s!ArFSFaZzVErwgR-Ed4Eywn67HtGr) and [baidu drive](https://pan.baidu.com/s/1tZfm3Prvzn47cZi5RZ-lNw):

* Parsing-RCNN(frame-level) weights(parsing_rcnn.h5).

* ATEN(p=2,l=3) weights(aten_p2l3.h5).

## Installation
1. Clone this repository
2. Keras with convGRU2D installation.
```Bash
cd keras_convGRU
python setup.py install
```
3. Compile flow_warp ops(optional). The flow_warp.so have been generated(Ubuntu14.04, gcc4.8.4, python3.6, tf1.4). To compile flow_warp ops, you can excute the code as follows:
```Bash
cd ops
make
```
4. Dataset setup. Download the [VIP dataset](http://sysu-hcp.net/lip/video_parsing.php)(both VIP_Fine and VIP_Sequence) and decompress them. The directory structure of VIP should be as follows:

VIP  
----Images  
--------videos1  
--------...  
--------videos404  
----adjacent_frames  
--------videos1  
--------...  
--------videos404    
----front_frame_list  
----Category_ids  
----Human_ids   
----Instance_ids  
----lists  
........  

5. Model setup. Download released weights and place in models floder.

## Training
```Bash
# ATEN training on VIP
python scripts/vip/train_aten.py

# Parsing-RCNN(frame-level) training on VIP
python scripts/vip/train_parsingrcnn.py
```

## Inference
```Bash
# ATEN inference on VIP
python scripts/vip/test_aten.py

# Parsing-RCNN(frame-level) inference on VIP
python scripts/vip/test_parsingrcnn.py
```
the results are stored in ./vis

## Evaluate
1. modify the path in evaluate/\*.py
2. run the code to evaluate your results generated by visualize.py
```Bash
# for human parsing
python evaluate/test_parsing.py

# for instance segmentation
python evaluate/test_ap.py

# for instance-level human parsing
python evaluate/test_inst_part_ap.py
```

## Reference
```
@inproceedings{zhou2018,
    Author = {Qixian Zhou, Xiaodan Liang, Ke Gong, Liang Lin},
    Title = {Adaptive Temporal Encoding Network for Video Instance-level Human Parsing},
    Booktitle = {Proc. of ACM International Conference on Multimedia (ACM MM)},
    Year = {2018}
} 
```

## Acknowledgements
This code is based on other source code on github:
1. matterport/Mask_RCNN(https://github.com/matterport/Mask_RCNN), an implementation of Mask R-CNN on Python 3, Keras, and TensorFlow. 
2. KingMV/ConvGRU(https://github.com/KingMV/ConvGRU), an implementation of ConvGRU2D on Keras.
