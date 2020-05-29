# Project of Data Visualization (COM-480)
# Torchlurk
Developping a front-end focused library aiming at making visualization of pytorch CNN easier, more accessible and more intuitive.

| Student's name | SCIPER |
| -------------- | ------ |
| Yann Mentha    | 252256 |
| Gianni Guisto  | 251795 |
| Julien Berger  | 247179 |

[Milestone 1](#milestone-1-friday-3rd-april-5pm) • [Milestone 2](#milestone-2-friday-1st-may-5pm) • [Milestone 3](#milestone-3-thursday-28th-may-5pm)

_____
## Milestone 1 (Friday 3rd April, 5pm)

**10% of the final grade**

### Abstract

In the past recent years, Convolutional Neural Networks (CNN) have shown impressive capabilities in image recognition tasks even outperforming humans. Despite undeniable success in all field of science, one can wonder why do these processing paradigms perform so well. Indeed, complexity increases along with the number of layers and internal computation lack of transparency for the user.

This project aims to develop a visualization tool to ease the interpretation of trained CNN and give insights to the user about what the network is actually learning. The name `Torch-` refers to the use of the PyTorch framework and `-lurk` to our willingness to unveil the intrinsic abstraction levels that are _'hidden'_ in these CNNs.

### Motivation
PyTorch is one of the most used deep learing framework and it just keeps getting more and more popular. Nevertheless, we feel like it lacks practical visual tool associated to it to get insights about network structure. We believe that is a great opportunity to develop such a tool as part of this course as it combines _utility_ to _visualization_.

### Approach
#### Backend
The `backend` insures that the data is properly formated so that it can be used interactively in the frontend. Analysis involving images computation are carried out using Python and the PyTorch framework. For now, we use networks such as _VGG16_ pretrained on the ImageNet dataset. We also make use of existing PyTorch CNN visualization libraries that enable to display _gradient_ and _filters_ (see [here](https://github.com/utkuozbulak/pytorch-cnn-visualizations)). Best responding images and filters are saved into _JSON_ file format.


#### Frontend
The goal of the `frontend` is to provide a user-friendly and intuitive interface to navigate through the network and analyse its internal states. It will enable the user to navigate through layers and examine it. An example of application we wish to offer (non-exhaustive list which may change according to the progress of the project): 
* visualize the structure of the network
* display most significant images activating a given neuron
* from a feature map, we want to project back the feature map thanks to deconvolution in order to isolate the pixel(s) responsible for the given activation

Network dynamical visualization are done using JavaScript and the library `D3.js`. To grasp the idea of our project, you are invited to open the HTML file `test.html` with the command (when no instance of chrome is already running):

```
google-chrome --allow-file-access-from-files main.html
```

### Road to Milestones 2-3
We provide here a working beta version to show the direction we are taking in this project. By milestone 2, we will in particular:
* display network architecture
* include more network architectures
* improve the HTML visually and make it intuitive
* use deconvolution to project back the output to the input

### References
* M. D. Zeiler and R. Fergus, _Visualizing and Understanding Convolutional Networks_. In _arXiv:1311.2901_, 2013. Available: https://arxiv.org/abs/1311.2901
* J. Yosinski _et al_., _Understanding neural networks through deep visualization_. In _arXiv:1506.06579_, 2015. Available: https://arxiv.org/abs/1506.06579
* Yosinski Jason, _Deep visualization toolbox_, (2017), GitHub repository: https://github.com/yosinski/deep-visualization-toolbox
* Yosinski Jason, _Understanding Neural Networks Through Deep Visualization_, (2020), Access: http://yosinski.com/deepvis
* Ozbulak, Utku, _PyTorch CNN visualizations_, (2020), GitHub repository: https://github.com/utkuozbulak/pytorch-cnn-visualizations


_____
## Milestone 2 (Friday 1st May, 5pm)

**10% of the final grade**

You will find the project description in the `milestone2` folder. 

The functional project prototype with the minimal HTML backbone can be found by running the following command: 

```
google-chrome --allow-file-access-from-files main.html
```

_____
## Milestone 3 (Thursday 28th May, 5pm)

**80% of the final grade**

Instead of copying all the code for the library and the website, we redirect you to Torchlurk's main directories. Indeed, it was easier to split the content into distinct repositories as follow:
* [website repo](https://torchlurk.github.io/)
* [backend and documentation](https://github.com/torchlurk/torchlurk) 
* [website repo](https://github.com/torchlurk/torchlurk.github.io)
* [library](https://github.com/torchlurk/torchlurk/tree/master/torchlurk)


The *website* is available at: [torchlurk.github.io](https://torchlurk.github.io/). The *process book* can be found [here](https://github.com/torchlurk/torchlurk.github.io/blob/master/process_book.pdf). There is as well a [tool presentation](https://www.youtube.com/watch?v=iRjrnuwGJ9M&t=11s) as well as a [website tour](https://www.youtube.com/watch?v=27HSh75LnhQ). Finally, you can check the library [on pip](https://pypi.org/project/torchlurk/0.1.2/)


_____
## Structure of the project
### Directories
`documentation` : where to put relevant articles/sources for the project<br>
`lib`: useful git repositories for the project<br>
`results`: directory where we store generated images for multiple runs<br>
`src`: for the source code (frontend) i.e. main.html, main.css and main.js<br>
`saved_model`: directory where we keep the json structure of each layers/filters for a given NN<br>
`data`: data directory<br>
-- `tinyimagenet`: subset of imageNet (10 img per class, 1000 classes) <br>
-- `exsmallimagenet`: subset of tinyimagenet (variables img and classes) <br>
`src`: source code <br>
-- `Torchlurk.ipynb`: backend code <br>
-- `main.css,main.html,main.js`:frontend interface

# Explanation of the structure of the results folder
For each filter the top4_avg (top 4 of the images of the tinyimagenet dataset that lead to the highest average output) and top4_max are stored in the json (they just reference the image in the tinyimagenet/exsmallimagenet folder.
## avg_grads
The gradients of the top4_avg of each filter with respect to that filter.

## max_grads
Equivalent of avg_grads for top4_avg with respect to top4_max

## cropped
for each image in the top4_max (the image of the tinyimagenet that managed to enhance the highest scalar score for the given filter), there is a region in the original image that lead to that pixel with highest scalar value. the cropped folder keep this cropped version of the top4_max images.

## cropped_grad
this same cropping is applied to the gradients of top4_max

## max_activ
the artificial image obtained by gradient descent which gives the highest average output score for a given filter.

To summary we have:
- 1: top4_avg
- 2: top4_max
- 3: avg_grads (deconvolution of top4_avg)
- 4: max_grads (deconvolution of top4_max)
- 5: cropped (cropped version of top4_max, slice of the original image resulting in the value which allowed the image to belong to top4_max
- 6: cropped_grad (same cropping applied to max_grads)
- 7: max_activ



