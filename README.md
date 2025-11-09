![Overall workflow](flow_chart.png)

**Basic requirements**
- Python3
- Other requirements can be found at requirement.txt and installation can be done via:
```
pip install -r requirements.txt
```

**Image dataset requirements**
- For both training and testing, geometry image (256, 256) and field image (256, 256) need to be stitched into one image with size (256, 512).
- If images with size (512, 512) are used, replace the corresponding python codes with codes in "HIGH_RESO". 
- Make sure the solid black background is in good proportion in order to match pixes. 
- Make sure they are named in order. e.g. 1.png, 2.png,...

**Before training or testing**
- Hyperparameters are indicated in "config.py".
- Specify the directory path which contains data set in config.py. e.g. PATH="./MISES/"
- Split your data set into training set and test set under dataset directory:
```

cd MISES
mkdir train ### training set dir
mkdir test ### test set dir
## move you data into these two folders (You can also not use two commands below and customize)##
cp split.sh ./MISES
bash split.sh
```
- Make sure images in training set and test set are named in order separately. e.g. 1.png, 2.png,...

**Training**
- Specify epochs in "config.py". e.g. EPOCHS = 150
- Start training by typing
```
python train.py
```
- The training checkpoints will be stored
- Checking the training status using Tensorboard:
```
tensorboard --logdir logs/fit
```

**Testing/prediction**
```
mkdir training_checkpoints
mkdir predict
cp DOWNLOAD_PATH/ckpt/MISES/* training_checkpoints
```
- Specify the number of data in test set in test.py. e.g. num_data = 5, so in test set, there will be 5 images: 1.png,...,5.png
- Run prediction on test set by typing:
```
python test.py
```
- The predcition will be in folder "./predict", stitched image from left to right is geometry, ground truth and prediction
- To change the checkpoint used for predictions, open "./training_checkpoints/checkpoint" to specify the checkpoint
