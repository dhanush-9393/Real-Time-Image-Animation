
# First Order Motion Model for Image Animation
### Introduction
Real-time image animation leverages advanced computer vision and machine
learning techniques to animate static images using dynamic driving videos. This
innovative technology enables the transformation of still photos into lively,
moving images, offering exciting possibilities for various applications in
entertainment, social media, and virtual reality. By extracting and transferring
motion patterns from a driving video to a static image, the First Order Motion
Model creates realistic animations, preserving the unique characteristics and
expressions of the original image. This process, which once required extensive
manual effort and expertise, is now achievable in real-time through automated
tools, making it accessible to a broader audience. Furthermore, real-time image
animation utilizes key point detection to identify crucial features on both the static
image and the driving video, such as eyes, nose, mouth, and other landmarks.
These key points are essential for accurately mapping motion patterns from the
video onto the static image.
The benefits of real-time image animation are manifold. It significantly reduces
the time and cost associated with traditional animation methods, making the
process more efficient.The resulting animations are not only realistic but also
interactive, providing a more engaging experience for users.






### Face-swap
It is possible to modify the method to perform face-swap using supervised segmentation masks.
![Screenshot](sup-mat/face-swap.gif)





### Image animation

In order to animate videos run:
```
CUDA_VISIBLE_DEVICES=0 python run.py --config config/dataset_name.yaml --mode animate --checkpoint path/to/checkpoint
```
You will need to specify the path to the checkpoint,
the ```animation``` subfolder will be created in the same folder as the checkpoint.
You can find the generated video there and its loss-less version in the ```png``` subfolder.
By default video from test set will be randomly paired, but you can specify the "source,driving" pairs in the corresponding ```.csv``` files. The path to this file should be specified in corresponding ```.yaml``` file in pairs_list setting.

There are 2 different ways of performing animation:
by using **absolute** keypoint locations or by using **relative** keypoint locations.

1) <i>Animation using absolute coordinates:</i> the animation is performed using the absolute positions of the driving video and appearance of the source image.
In this way there are no specific requirements for the driving video and source appearance that is used.
However this usually leads to poor performance since irrelevant details such as shape is transferred.
Check animate parameters in ```taichi-256.yaml``` to enable this mode.

<img src="sup-mat/absolute-demo.gif" width="512"> 

2) <i>Animation using relative coordinates:</i> from the driving video we first estimate the relative movement of each keypoint,
then we add this movement to the absolute position of keypoints in the source image.
This keypoint along with source image is used for animation. This usually leads to better performance, however this requires
that the object in the first frame of the video and in the source image have the same pose

<img src="sup-mat/relative-demo.gif" width="512"> 


### Datasets

1) **Bair**.
2) **Mgif**. 

3) **Fashion**. 

4) **Taichi**. 

5) **Nemo**.
 
6) **VoxCeleb**.

### Training on your own dataset
1) Resize all the videos to the same size e.g 256x256, the videos can be in '.gif', '.mp4' or folder with images.
We recommend the later, for each video make a separate folder with all the frames in '.png' format. This format is loss-less, and it has better i/o performance.

2) Create a folder ```data/dataset_name``` with 2 subfolders ```train``` and ```test```, put training videos in the ```train``` and testing in the ```test```.

3) Create a config ```config/dataset_name.yaml```, in dataset_params specify the root dir the ```root_dir:  data/dataset_name```. Also adjust the number of epoch in train_params.

### CONCLUSION
The project underscores the versatility and accessibility of cutting-edge machine
learning techniques. By leveraging an intuitive interface, it lowers the barrier for
entry, allowing individuals without a deep technical background to experiment
with and benefit from advanced animation technologies. The project's modular
design ensures that it can be easily extended or adapted to incorporate new models
or features, fostering ongoing innovation and exploration in the realm of image
animation.
In summary, this real-time image animation project not only showcases the
impressive capabilities of the First Order Motion Model but also serves as a
testament to the power of integrating diverse technological components into a
cohesive and user-centric application. It paves the way for new creative
possibilities, inspiring users to reimagine the boundaries of static imagery and
explore new dimensions of animated art and storytelling.













