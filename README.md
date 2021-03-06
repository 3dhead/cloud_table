# CloudTable

<br><br>

![cloud table](https://github.com/ytakzk/cloud_table/raw/master/images/cloud_table_02.png)

<br><br>


ETH DFAB 2018 Mini-project for Frame Möbel by Nicolas & Yuta  

Exercice to design a metal-fdm printed join for a space frame, aimed at a table.  
The exercice was taken as an oportunity to explore a possible way of sharing the work of designing, between a machine (computer system) and a human.  
Given the short timeframe of this exploration, it was choosen from the start to split the design in two parts.  
The main idea is to have as little human input as possible for the global design of the table (general shape and derived space-frame).  
The join in contrast has a strong emphasize on the human intent (no form-finding strategies).  
It is of note that this strict separation is not necessarly the best option, but merely a starting point in this research on human-machine intergration for design tasks, that some others may continue.


## Contents

* **train_auto_encoder**  
Training of an auto encoder based on PointNet.  
* **python**  
Python program to tweak point clouds for table manipulation.  
* **pointcloud2mesh**  
C++ program to create a mesh from a point cloud.   
* **grasshopper**  
Grasshopper scripts as a client to call the programs above.   
* **processing_app**  
Processing applications as a client.  
* **cloudtable_docker**  
Docker environments hosting this project. 


## Environments

![system architecture](https://github.com/ytakzk/cloud_table/raw/master/images/system_architecture.jpg)

The easiest way to set up this environment is to use Docker.

#### For the first time

1. Clone this repository
1. Build a docker image (takes around 5 mins)  
`cd cloud_table/cloudtable_docker && docker build ./ -t cloud_table`
1. Run and log into a docker container (mount all files in this repository with the container)
`docker run -it --name cloud_table -v {ABSOLUTE_PATH_OF_THIS_REPOSITORY}:/cloud_table -p 9997-9999:9997-9999 cloud_table`


#### From the next time

1. Start the docker container  
`docker start -i cloud_table`

## Apps

### tweak_latent_vector / Processing app

![tweak_latent_vector](https://github.com/ytakzk/cloud_table/raw/master/images/tweak_latent_vector.jpg)

In the docker container, run `python3 /cloud_table/python/socket_app.py` then open [tweak_latent_vector](https://github.com/ytakzk/cloud_table/tree/master/processing_app/tweak_latent_vector). Note that you need to restart its socket connection every time before running the Proceeing app.


### semantic_morphing / web app - [DEMO](http://cloudtable.ytakzk.me/semantic_morphing)  

![semantic_morphing](https://github.com/ytakzk/cloud_table/raw/master/images/semantic_morphing.jpg)

In the docker container, run `python3 /cloud_table/python/webapp.py` then browse `http://127.0.0.1:9997/semantic_morphing` with some modern browser


### weather_table / web app - [DEMO](http://cloudtable.ytakzk.me/weather_table)  

![weather_table](https://github.com/ytakzk/cloud_table/raw/master/images/weather_table.jpg)

In the docker container, run `python3 /cloud_table/python/webapp.py` then browse `http://127.0.0.1:9997/weather_table` with some modern browser


## Data Source
* [Point clouds](https://www.dropbox.com/s/fpzchkh1zwvjkn6/04379243.zip)  
1 point-cloud with 2048 points per model from [ShapeNet](https://www.shapenet.org/).


## Workflow

### Training Process
1. Download point clouds from [DropBox](https://www.dropbox.com/s/fpzchkh1zwvjkn6/04379243.zip)  extracted from [ShapeNet](https://www.shapenet.org/)
1. Train the auto encoder

### Manipulation Process

1. Select a base table
1. Tweak its latent vector
1. create a mesh from the point cloud
1. Apply a joint system between connected edges


## Dependences

* Docker
* Rhinoceros 6
* Processing 3


#### Neural Nets

* Python 3.6.5
* PyTorch 0.4.1
* CUDA 9.0 (for training an auto encoder)


#### Mesh Generator

* C++14 (GNU++14)
* libc++
* CGAL 4.13


## References

#### Papers

* [deep cloud The Application of a Data-driven, Generative Model in Design](https://sites.google.com/site/artml2018/showcase/final-project)
* [PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation](https://arxiv.org/abs/1612.00593)
* [Three-Dimensional Alpha Shapes](http://pub.ist.ac.at/~edels/Papers/1994-J-04-3DAlphaShapes.pdf)


#### Codes

* [fxia22/pointnet.pytorch](https://github.com/fxia22/pointnet.pytorch)
* [optas/latent_3d_points](https://github.com/optas/latent_3d_points)


## Fabricated table 

![cloud table](https://github.com/ytakzk/cloud_table/raw/master/images/table_01.jpg)
![cloud table](https://github.com/ytakzk/cloud_table/raw/master/images/table_02.jpg)
![cloud table](https://github.com/ytakzk/cloud_table/raw/master/images/table_03.jpg)


## Misc 

* [Algorithm for generating a triangular mesh from a cloud of points](https://stackoverflow.com/questions/7879160/algorithm-for-generating-a-triangular-mesh-from-a-cloud-of-points)
* [Using CGAL and Xcode](https://3d.bk.tudelft.nl/ken/en/2016/03/16/using-cgal-and-xcode.html)
* [3D Alpha Shapes](https://doc.cgal.org/latest/Alpha_shapes_3/index.html)
* [Everything You Always Wanted to Know About Alpha Shapes But Were Afraid to Ask](http://cgm.cs.mcgill.ca/~godfried/teaching/projects97/belair/alpha.html)
* [VAE with PyTorch](https://github.com/pytorch/examples/blob/master/vae/main.py)
* [Intuitively Understanding Variational Autoencoders](https://towardsdatascience.com/intuitively-understanding-variational-autoencoders-1bfe67eb5daf)
* [What The Heck Are VAE-GANs?](https://towardsdatascience.com/what-the-heck-are-vae-gans-17b86023588a)
* [robust algorithm for surface reconstruction from 3D point cloud?](https://stackoverflow.com/questions/838761/robust-algorithm-for-surface-reconstruction-from-3d-point-cloud)
* [Eigenchairs](https://vimeo.com/57901236)
