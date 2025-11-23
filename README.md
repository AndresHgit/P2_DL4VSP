# P2_DL4VSP

## Installation 

```text
# 
conda create --name MEGA -y python=3.7
source activate MEGA

conda install ipython pip

pip install ninja yacs cython matplotlib tqdm opencv-python scipy

# pytorch 1.2.0 is required and torchvision 0.4.0 guarantees compatibility 
conda install pytorch=1.2.0 torchvision=0.4.0 cudatoolkit=10.0 -c pytorch

export INSTALL_DIR=$PWD

# install pycocotools
cd $INSTALL_DIR
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
python setup.py build_ext install

# install cityscapesScripts
cd $INSTALL_DIR
git clone https://github.com/mcordts/cityscapesScripts.git
cd cityscapesScripts/
python setup.py build_ext install

# install PyTorch Detection
cd $INSTALL_DIR
git clone https://github.com/Scalsol/mega.pytorch.git
cd mega.pytorch

python setup.py build develop

pip install 'pillow<7.0.0'

unset INSTALL_DIR

# With that, all the necessary directories are installed, though some files need to be updated, while remaining inside /mega.pitorch folder

curl -o mega_core/layers/nms.py https://raw.githubusercontent.com/AndresHgit/P2_DL4VSP/main/nms.py
curl -o demo/predictor.py https://raw.githubusercontent.com/AndresHgit/P2_DL4VSP/main/predictor.py
curl -o mega_core/layers/roi_align.py https://raw.githubusercontent.com/AndresHgit/P2_DL4VSP/main/roi_align.py
curl -o mega_core/layers/roi_pool.py https://raw.githubusercontent.com/AndresHgit/P2_DL4VSP/main/roi_pool.py
curl -o configs/vid_R_101_C4_1x.yaml https://raw.githubusercontent.com/AndresHgit/P2_DL4VSP/main/vid_R_101_C4_1x.yaml.py
curl -o configs/MEGA/vid_R_101_C4_MEGA_1x.yaml https://raw.githubusercontent.com/AndresHgit/P2_DL4VSP/main/vid_R_101_C4_MEGA_1x.yaml.py

```

## Running the code
Before showing the specific instruction to run the code, both the input video/image_folder and the checkpoint files (see https://github.com/Scalsol/mega.pytorch Main Results) must be included in the folder mega.pytorch created during installation, and the code must be run from that folder as well.

### Image folders 
If the input video is stored as a group of independent images, the command line would be: 

```
python demo/demo.py ${METHOD} ${CONFIG_FILE} ${CHECKPOINT_FILE} [--visualize-path ${IMAGE-FOLDER}] [--suffix ${IMAGE_SUFFIX}][--output-folder ${FOLDER}] [--output-video]
```

### Video 
If the video is stored in a normal video format, the command line would be: 

```
python demo/demo.py ${METHOD} ${CONFIG_FILE} ${CHECKPOINT_FILE} --video [--visualize-path ${VIDEO-NAME}] [--output-folder ${FOLDER}] [--output-video]
```

