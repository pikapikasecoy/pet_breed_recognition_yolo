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
* **Step 2**: Download the pretrained weights file [yolov2-tiny-pet_40000.weights](https://github.com/ideaRunner/yolo-pet/releases/download/0.0.1/yolov2-tiny-pet_40000.weights)

* **Step 3**: Generate Label Files
[pet_label.py](https://github.com/pikapikasecoy/pet_breed_recognition_yolo/blob/763be5413623438680ac9dd3f87a59f9b178d077/pet_label.py) was created to create annotations and generate labels. Since our dataset provides images with annotations, so in this step, we will only use generate function to generate label files directly with following command.
```
python pet_label.py generate
```
Then there will be a Train_list.txt file and Val_List.txt file in the root directory and labels in ```labels``` directory. And we have to keep ```labels``` and ```Images``` In the same directory.

* **Step 4**: Configuration

- Create a configuration file ```pet.data``` in the ```darknet/cfg``` directory, with the following content:
```
classes= 37
train  = Train_List.txt
valid  = Val_List.txt
names = data/pet.names
backup = pet_backup
```
- Create the breeds file ```pet.names``` in the ```darknet/data``` directory, with the 37 breeds as follows:
    
```
Abyssinian
Bengal
Birman
Bombay
British_Shorthair
Egyptian_Mau
Maine_Coon
Persian
Ragdoll
Russian_Blue
Siamese
Sphynx
american_bulldog
american_pit_bull_terrier
basset_hound
beagle
boxer
chihuahua
english_cocker_spaniel
english_setter
german_shorthaired
great_pyrenees
havanese
japanese_chin
keeshond
leonberger
miniature_pinscher
newfoundland
pomeranian
pug
saint_bernard
samoyed
scottish_terrier
shiba_inu
staffordshire_bull_terrier
wheaten_terrier
yorkshire_terrier
```
- Create a yolov2.cfg file for configuration parameters. After playing around a little bit, [yolov2-tiny-pet_40000.cfg](https://github.com/pikapikasecoy/pet_breed_recognition_yolo/blob/763be5413623438680ac9dd3f87a59f9b178d077/yolov2-tiny-pet_40000.cfg) is our final configuration file.

- Make a directory for training backup with the following command and the name should be the same as defined in ```pet.data```
```
mkdir darknet/pet_backups
```

## 3. Training
Use the following commands to train yolo
```
cd darknet 
./darknet detector train cfg/pet.data cfg/yolov2-tiny-pet_40000.cfg  yolov2-tiny-pet_40000.weights 
```

## To test or use the trained YOLO for pet breed detection

place holder, will come back later :)
