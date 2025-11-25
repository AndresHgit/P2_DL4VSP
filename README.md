# P2_DL4VSP

## Installation 
To install the required dependencies for running the BASE and MEGA methods described in the CVPR 2020 paper “Memory Enhanced Global-Local Aggregation for Video Object Detection”, the following process must be carried out in a Linux terminal.

```text
# For this installation is necessary to use a conda environment. If not available, this instructions will not work
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
curl -o configs/vid_R_101_C4_1x.yaml https://raw.githubusercontent.com/AndresHgit/P2_DL4VSP/main/vid_R_101_C4_1x.yaml
curl -o configs/MEGA/vid_R_101_C4_MEGA_1x.yaml https://raw.githubusercontent.com/AndresHgit/P2_DL4VSP/main/vid_R_101_C4_MEGA_1x.yaml

```

## Running the code
Before showing the specific instruction to run the code, both the input video or image_folder and the checkpoint files (see https://github.com/Scalsol/mega.pytorch Main Results) must be included in the folder mega.pytorch created during installation, and the code must be run from that folder as well.

### Image folders 
If the input video is stored as the group of each independent frame, the command line would be: 

```
python demo/demo.py ${METHOD} ${CONFIG_FILE} ${CHECKPOINT_FILE} [--visualize-path ${IMAGE-FOLDER}] [--suffix ${IMAGE_SUFFIX}][--output-folder ${FOLDER}] [--output-video]
```

In this case, the frames in the folder need to be numbered with the following format, in order: 00000, 00001, 00002...

### Video 
If the video is stored in a normal video format, the command line would be: 

```
python demo/demo.py ${METHOD} ${CONFIG_FILE} ${CHECKPOINT_FILE} --video [--visualize-path ${VIDEO-NAME}] [--output-folder ${FOLDER}] [--output-video]
```

## Aditional notes
This installation is designed to work for base and MEGA methods, any other change is not guaranteed to work, as this is not an original implementation.
For the original implementation and more details about its functionalities and how this code works, see https://github.com/Scalsol.

