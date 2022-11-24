# CS 337 Course Project.
Python>=3.6 is required to run the code.

# Directions to install:
Run the following from the base directory:

0. (This step is optional, if you dont want to update your libraries):
Make a virtual environment for pip to work in

1. Clone the Synchronized-BatchNorm-PyTorch repository for
```
cd Face_Enhancement/models/networks/
git clone https://github.com/vacancy/Synchronized-BatchNorm-PyTorch
cp -rf Synchronized-BatchNorm-PyTorch/sync_batchnorm .
cd ../../../
```
and
```
cd Global/detection_models
git clone https://github.com/vacancy/Synchronized-BatchNorm-PyTorch
cp -rf Synchronized-BatchNorm-PyTorch/sync_batchnorm .
cd ../../
```

2. Download the pretrained model for detecting face landmarks:
```
cd Face_Detection/
wget http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2
bzip2 -d shape_predictor_68_face_landmarks.dat.bz2
cd ../
```

3. Download pretrained models in correct folders:
```
cd Face_Enhancement/
wget https://github.com/microsoft/Bringing-Old-Photos-Back-to-Life/releases/download/v1.0/face_checkpoints.zip
unzip face_checkpoints.zip
cd ../
cd Global/
wget https://github.com/microsoft/Bringing-Old-Photos-Back-to-Life/releases/download/v1.0/global_checkpoints.zip
unzip global_checkpoints.zip
cd ../
```

4. Install dependencies:
if you did step 0:
```
pip install -r requirements.txt
```
else:
```
cat requirements.txt | sed -e '/^\s*#.*$/d' -e '/^\s*$/d' | xargs -n 1 python -m pip install
```

# How to run the code:
For images without scratches:
```
python run.py --input_folder [test_image_folder_path] \
              --output_folder [output_path] \
              --GPU -1
```
For scratched images:
```
python run.py --input_folder [test_image_folder_path] \
              --output_folder [output_path] \
              --GPU -1 \
              --with_scratch
```
For high-resolution images with scratches:
```
python run.py --input_folder [test_image_folder_path] \
              --output_folder [output_path] \
              --GPU -1 \
              --with_scratch \
              --HR
```

# Only for scratch detection:
```
cd Global/
python detection.py --test_path [test_image_folder_path] \
                    --output_dir [output_path] \
                    --input_size full_size
```

# Global restoration (if you have mask):
```
cd Global/
python test.py --Scratch_and_Quality_restore \
               --test_input [test_image_folder_path] \
               --test_mask [corresponding mask] \
               --outputs_dir [output_path]
python test.py --Quality_restore \
               --test_input [test_image_folder_path] \
               --outputs_dir [output_path]
```

# OurImages
To reproduce the results we obtained from our experimentation, please use the images provided in _OurImages_.
Specifically, given below is an example command to get scratch free images for all photos present in the folder:
```
mkdir MyOutput
python run.py --input_folder ./OurImages \
              --output_folder ./MyOutput \
              --GPU -1 \
              --with_scratch \
              --HR
```
