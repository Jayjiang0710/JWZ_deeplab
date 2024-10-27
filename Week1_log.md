
# Environment Setup

## 1. Check Version
### Requirements
- Python versions 3.8 - 3.11 to support TensorFlow 2. 
- Refer to the [TensorFlow installation guide](https://www.tensorflow.org/install).

#### Commands:
```bash
python --version  # Should be Python 3.11.9
pip --version     # Should be greater than 19.0
```

#### Note:
As of 2024/10/20, there are unresolved compatibility issues; install Python 3.6 to support TensorFlow 1.15.

## 2. Configure Virtual Environment
```bash
python -m venv deeplab_env
.\deeplab_env\Scripts\activate
```

## 3. Install TensorFlow
```bash
pip install tensorflow
```

## 4. Clone Repository
```bash
git clone https://github.com/tensorflow/models.git
```

## 5. Install Dependencies
Refer to the [installation guide](https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/installation.md) for TensorFlow models.

```bash
pip install numpy pillow matplotlib jupyter #packages listed here due to lack of documented dependencies
```

## 6. Add Libraries to PYTHONPATH
Refer to the [Deeplab installation guide](https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/installation.md#add-libraries-to-pythonpath).
```bash
# For Windows
$env:PYTHONPATH += ";$PWD;$PWD\slim"
```

## 7. Test Installation
Refer to the [testing guide](https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/installation.md#testing-the-installation).

```bash
# From tensorflow/models/research/
python deeplab/model_test.py
```

### Known Issue with TensorFlow 2.x
```plaintext
Traceback (most recent call last):
  File "F:\MB_Intern\models\research\deeplab\model_test.py", line 21, in <module>
    from deeplab import common
  File "F:\MB_Intern\models\research\deeplab\common.py", line 24, in <module>
    flags = tf.app.flags
            ^^^^^^
AttributeError: module 'tensorflow' has no attribute 'app'
```
Solution: (https://itsourcecode.com/attributeerror/attributeerror-module-tensorflow-has-no-attribute-app-solved/?source=post_page-----0dab78b4467a--------------------------------&utm_content=cmp-true) or [the official guide(same approach)](https://www.tensorflow.org/guide/migrate/upgrade)

# Dataset Preparation

## 1. Dataset Used
- `gtFine_trainvaltest` and `leftImg8bit_trainvaltest` from [Cityscapes dataset](https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/cityscapes.md#running-deeplab-on-cityscapes-semantic-segmentation-dataset).

## 2. Clone and Set Up Cityscapes Scripts
```bash
git clone https://github.com/mcordts/cityscapesScripts.git
```

### Modified Structure
```plaintext
+ datasets
  - build_cityscapes_data.py
  - convert_cityscapes.sh
  + cityscapes
    + cityscapesscripts
    + gtFine
    + leftImg8bit
```

### Run Script
Execute the script `preparation/createTrainIdLabelImgs.py` to generate the training ground truth as required by `convert_cityscapes.sh`.
