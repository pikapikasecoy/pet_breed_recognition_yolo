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
* **Step 2**: Download Pretrained Convolutional Weights of Yolo-v3.
```
wget https://pjreddie.com/media/files/darknet53.conv.74
```

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
The we used the following commands to train yolo
```
cd darknet 
./darknet detector train cfg/pet.data cfg/yolov3-pet.cfg  darknet53.conv.74 
```

# Test or Use Trained YOLO 

We can simply apply YOLO to detect pet breed given any jpg image using the [trained weight file](https://github.com/ideaRunner/yolo-pet/releases/download/0.0.1/yolov2-tiny-pet_40000.weights) (60.9MB) provided by [ideaRunner](https://github.com/ideaRunner). Alternatively, we can also test the performance of the weight file trained by ourselves as shown in the previous stages, if it's the case, please jump directly to the ***Test*** step.

* **Clone YOLO Project**: clone [YOLO](https://pjreddie.com/darknet/yolo/) project if you haven't done so, and cd into the darknet folder.
```
git clone https://github.com/pjreddie/darknet
cd darknet
make
```

* **Download Weight Files**: Download [trained weight file](https://github.com/ideaRunner/yolo-pet/releases/download/0.0.1/yolov2-tiny-pet_40000.weights) mentioned above

* **Add Pet Breed Detection Config Files**: move or copy ```pet.data``` and ```yolov2-tiny-pet_40000.cfg``` under the root directory of this repo to ```darknet/cfg```, and ```pet.names``` to ```darknet/data```

* **Replace source code**: replace ```yolo.c``` in ```darknet/example``` with ```yolo.c``` under the home directory of this repo. By doing this, we create a new array of labels string containing all pet breed names, and pass it to the function ```draw_detections(im, dets, l.side*l.side*l.n, thresh, pet_names, alphabet, 37)```, which enables YOLO to annotate any detected area with the corresponing pet breed.

* **Compile**: compile and link this project by running the following commands
```
make clean
make -j8
```

* **Add Test Image**: for testing purpose, move or copy the image ```img_README/Abyssinian_1.jpg``` under the root directory of this repo to ```/darknet/data```.

![alt text](https://github.com/pikapikasecoy/pet_breed_recognition_yolo/blob/main/img_README/Abyssinian_1.jpg)

* **Test**: To test YOLO, run the following command which specifies the configuration files and weights, as well as the image you'd like to detect. Please replace the weight file if you've trained your own one.
```
./darknet detector test cfg/pet.data cfg/yolov2-tiny-pet_40000.cfg yolov2-tiny-pet_40000.weights  data/Abyssinian_1.jpg
```
An image named predictions.png will be added to the darknet root directory.
![alt text](https://github.com/pikapikasecoy/pet_breed_recognition_yolo/blob/main/img_README/predictions.jpg)

* **Testing on Multiple Images**: Instead of supplying an image on the command line, you can leave it blank to try multiple images in a row. Instead you will see a prompt when the config and weights are done loading:
```
./darknet detector test cfg/pet.data cfg/yolov2-tiny-pet_40000.cfg yolov2-tiny-pet_40000.weights  
```
![alt text](https://github.com/pikapikasecoy/pet_breed_recognition_yolo/blob/main/img_README/multiple_img_demo.png)

Enter an image path like data/Abyssinian_1.jpg to have it predict boxes for that image. Once it is done it will prompt you for more paths to try different images. Use Ctrl-C to exit the program once you are done.
