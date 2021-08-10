# pet_breed_recognition_yolo

## 1. Data Description

In this project, we used the Oxford-IIIT [Pet Dataset](https://www.robots.ox.ac.uk/~vgg/data/pets/) for training.
This dataset includes 7,349 [images](https://www.robots.ox.ac.uk/~vgg/data/pets/data/images.tar.gz) and corresponding [annotations](https://www.robots.ox.ac.uk/~vgg/data/pets/data/annotations.tar.gz) of 37 cat or dog breeds. Each individual breed is associated with roughly 200 images.

Both cat and dog breeds are covered in one target variable. Breeds included are as follows:
```
{"Abyssinian", "Bengal", "Birman", "Bombay", "British_Shorthair", 
"Egyptian_Mau", "Maine_Coon", "Persian", "Ragdoll", "Russian_Blue", 
"Siamese", "Sphynx", "american_bulldog", "american_pit_bull_terrier", 
"basset_hound", "beagle", "boxer", "chihuahua", "english_cocker_spaniel", "english_setter", "german_shorthaired", "great_pyrenees", "havanese", 
"japanese_chin", "keeshond", "leonberger", "miniature_pinscher", "newfoundland", 
"pomeranian", "pug", "saint_bernard", "samoyed", "scottish_terrier", "shiba_inu",
"staffordshire_bull_terrier", "wheaten_terrier", "yorkshire_terrier"};
```

## 2. Setup
* **Step 1**: Clone the Yolo project with the following commands
```
git clone https://github.com/pjreddie/darknet
cd darknet
make
```
* **Step 2**: Download the pretrained [weights file](https://github.com/ideaRunner/yolo-pet/releases/download/0.0.1/yolov2-tiny-pet_40000.weights)

* **Step 3**: Generate Labels


## 3. Training

## To test or use the trained YOLO for pet breed detection

place holder, will come back later :)
