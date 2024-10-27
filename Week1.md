# Environment Setup

## 1. 配置虚拟环境
### 需要python <= 3.7, TensorFlow 1.x (1.15)
% in anoconda prompt
conda create -n deeplab_env python=3.7
conda activate deeplab_env
pip install tensorflow==1.15
conda install git
%conda deactivate
%verify env
conda info --envs


## 2.clone repo
git clone https://github.com/tensorflow/models.git

## 3. Install dependencies
参考: https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/installation.md
conda install pillow matplotlib jupyter
pip install numpy
pip install mkl-service
pip install tf_slim

备注？：Numpy必须由pip安装，否则运行测试 'bash local_test.sh'时会有如下问题 'Importing the numpy c-extensions failed',参考 https://stackoverflow.com/questions/58868528/importing-the-numpy-c-extensions-failed。


## 4.Add Libraries to PYTHONPATH (Do this for every new terminal)
参考：https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/installation.md#add-libraries-to-pythonpath
From tensorflow/models/research/:
$env:PYTHONPATH = ""
$env:PYTHONPATH = "$(Get-Location);$(Get-Location)\slim"
##verify path:
echo $env:PYTHONPATH

## 7.测试安装:
参考：https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/installation.md#testing-the-installation

测试1:
From tensorflow/models/research/
python deeplab/model_test.py

结果：
 [       OK ] DeeplabModelTest.testForwardpassDeepLabv3plus
[ RUN      ] DeeplabModelTest.testWrongDeepLabVariant
[       OK ] DeeplabModelTest.testWrongDeepLabVariant
[ RUN      ] DeeplabModelTest.test_session
[  SKIPPED ] DeeplabModelTest.test_session

Test2（未完成）:
# From tensorflow/models/research/deeplab (Windows用Git Bash)
bash local_test.sh








# Dataset preparation:
## 1.dataset used: gtFine_trainvaltest and leftImg8bit_trainvaltest
https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/cityscapes.md#running-deeplab-on-cityscapes-semantic-segmentation-dataset

## 2.
git clone https://github.com/mcordts/cityscapesScripts.git #clone repository of cityscapesscripts
setup and re-structure repo according to deeplab/datasets/cityscapes/convert_cityscapes.sh:
python -m pip install ".[gui]"

modified structure:
+ datasets
  - build_cityscapes_data.py
  - convert_cityscapes.sh
  + cityscapes
    + cityscapesscripts
    + gtFine
    + leftImg8bit

run the script provided by Cityscapes
`preparation/createTrainIdLabelImgs.py` to generate the training groundtruth. #required to run convert_cityscapes.sh


