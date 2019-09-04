# [Bi-Directional ConvLSTM U-Net with Densely Connected Convolutions ](https://arxiv.org/pdf/1909.00166.pdf)


Deep auto-encoder-decoder network for medical image segmentation with state of the art results on skin lesion segmentation, lung segmentation, and retinal blood vessel segmentation. This method applies bidirectional convolutional LSTM layers in U-net structure to non-linearly encode both semantic and high-resolution information with non-linearly technique. Furthermore, it applies densely connected convolution layers to include collective knowledge in representation and boost convergence rate with batch normalization layers. If this code helps with your research please consider citing the following paper:
</br>
> [R. Azad](https://scholar.google.com/citations?hl=en&user=Qb5ildMAAAAJ&view_op=list_works&sortby=pubdate), [M. Asadi](https://scholar.google.com/citations?hl=en&user=8UqpIK8AAAAJ&view_op=list_works&sortby=pubdate), [Mahmood Fathy](https://scholar.google.com/citations?hl=en&user=CUHdgPcAAAAJ&view_op=list_works&sortby=pubdate) and [Sergio Escalera](https://scholar.google.com/citations?hl=en&user=oI6AIkMAAAAJ&view_op=list_works&sortby=pubdate) "Bi-Directional ConvLSTM U-Net with Densely Connected Convolutions ", ICCV, 2019, download [link](https://arxiv.org/pdf/1909.00166.pdf).

## Updates
- Augest 28, 2019: First release (Complete implemenation for [SKin Lesion Segmentation on ISIC 218](https://challenge2018.isic-archive.com/), [Retina Blood Vessel Segmentation](http://www.isi.uu.nl/Research/Databases/DRIVE/) and [Lung segmentation]()dataset added.)
- Augest 27, 2019: Paper Accepted in the ICCV workshop 2019 (Oral presentation).

## Prerequisties and Run
This code has been implemented in python language using Keras libarary with tensorflow backend and tested in ubuntu OS, though should be compatible with related environment. following Environement and Library needed to run the code:

- Python 3
- Keras - tensorflow backend


## Run Demo
For training deep model for each task, go to the related folder and follow the bellow steps:

#### Skin Lesion Segmentation
1- Download the ISIC 2018 train dataset from [this](https://challenge.kitware.com/#phase/5abcb19a56357d0139260e53) link and extract both training dataset and ground truth folders inside the `dataset_isic18`. </br>
2- Run `Prepare_ISIC2018.py` for data preperation and dividing data to train,validation and test sets. </br>
3- Run `train_isic18.py` for training BCDU-Net model using trainng and validation sets. The model will be train for 100 epochs and it will save the best weights for the valiation set. You can also train U-net model for this dataset by changing model to unet, however, the performance will be low comparing to BCDU-Net. </br>
4- For performance calculation and producing segmentation result, run `evaluate.py`. It will represent performance measures and will saves related figures and results in `output` folder.</br>

#### Retina Blood Vessel Segmentation
1- Download Drive dataset from [this](http://www.isi.uu.nl/Research/Databases/DRIVE/) link and extract both training  and test  folders in a folder name DRIVE (make a new folder with name DRIVE) </br>
2- Run `prepare_datasets_DRIVE.py` for reading whole data. This code will read all the train and test samples and will saves them as a hdf5 file in the `DRIVE_datasets_training_testing` folder. </br>
3- The next step is to extract random patches from the training set to train the model, to do so, Run `save_patch.py`, it will extract random patches with size 64*64 and will save them as numpy file. This code will use `help_functions.py`, `spre_processing.py` and `extract_patches.py` functions for data normalization and patch extraction.  
4- For model training, run `train_retina.py`, it will load the training data and will use 20% of training samples as a validation set. The model will be train for 50 epochs and it will save the best weights for the valiation set.</br>
4- For performance calculation and producing segmentation result, run `evaluate.py`. It will represent performance measures and will saves related figures and results in `test` folder.</br>
Note: For image pre-processing and patch extraction we used [this](https://github.com/orobix/retina-unet) github's code.</br>




## Quick Overview
![Diagram of the proposed method](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/bcdunet.png)

### Structure of the Bidirection Convolutional LSTM that used in our network
![Diagram of the proposed method](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/convlstm.png)

## Results
For evaluating the performance of the proposed method, Two challenging task in medical image segmentaion has been considered. In bellow, results of the proposed approach illustrated.
</br>
#### Task 1: Retinal Blood Vessel Segmentation


#### Performance Comparision on Retina Blood Vessel Segmentation
In order to compare the proposed method with state of the art appraoches on retinal blood vessel segmentation, we considered Drive dataset.  

Methods | Year |F1-scores | Sensivity| Specificaty| Accuracy | AUC
------------ | -------------|----|-----------------|----|---- |---- 
Chen etc. all [Hybrid Features](https://link.springer.com/article/10.1007/s00138-014-0638-x)        |2014	  |	-       |0.7252	  |0.9798	  |0.9474	  |0.9648
Azzopardi  etc. all [Trainable COSFIRE filters ](https://www.sciencedirect.com/science/article/abs/pii/S1361841514001364)   |2015	  |	-       |0.7655	  |0.9704	  |0.9442	  |0.9614
Roychowdhury and etc. all [Three Stage Filtering](https://ieeexplore.ieee.org/document/6848752)|2016 	|	-       |0.7250	  |**0.9830**	  |0.9520	  |0.9620
Liskowsk  etc. all[Deep Model](https://ieeexplore.ieee.org/document/7440871)	  |2016	  |	-       |0.7763	  |0.9768	  |0.9495	  |0.9720
Qiaoliang  etc. all [Cross-Modality Learning Approach](https://ieeexplore.ieee.org/document/7161344)|2016	  |	-       |0.7569	  |0.9816	  |0.9527	  |0.9738
Ronneberger and etc. all [U-net](https://arxiv.org/abs/1505.04597)	     	    |2015   | 0.8142	|0.7537	  |0.9820	  |0.9531   |0.9755
Alom  etc. all [Recurrent Residual U-net](https://arxiv.org/abs/1802.06955)	|2018	  | 0.8149  |0.7726	  |0.9820	  |0.9553	  |0.9779
Oktay  etc. all [Attention U-net](https://arxiv.org/abs/1804.03999)	|2018	  | 0.8155	|0.7751	  |0.9816	  |0.9556	  |0.9782
Alom  etc. all [R2U-Net](https://arxiv.org/ftp/arxiv/papers/1802/1802.06955.pdf)	        |2018	  | 0.8171	|0.7792	  |0.9813	  |0.9556	  |0.9784
Azad etc. all [Proposed BCDU-Net](https://github.com/rezazad68/LSTM-U-net/edit/master/README.md)	  |2019 	| **0.8222**	|**0.8012**	  |0.9784	  |**0.9559**	  |**0.9788**


#### Retinal blood vessel segmentation result on test data

![Retinal Blood Vessel Segmentation result 1](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/Figure_1.png)
![Retinal Blood Vessel Segmentation result 2](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/Figure_2.png)
![Retinal Blood Vessel Segmentation result 3](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/Figure_3.png)


## Skin Lesion Segmentation

#### Performance Evalution on the Skin Lesion Segmentation task

Methods | Year |F1-scores | Sensivity| Specificaty| Accuracy | PC | JS 
------------ | -------------|----|-----------------|----|---- |---- |---- 
Ronneberger and etc. all [U-net](https://arxiv.org/abs/1505.04597)	     	    |2015   | 0.647	|0.708	  |0.964	  |0.890  |0.779 |0.549
Alom  etc. all [Recurrent Residual U-net](https://arxiv.org/abs/1802.06955)	|2018	  | 0.679 |0.792 |0.928 |0.880	  |0.741	  |0.581
Oktay  etc. all [Attention U-net](https://arxiv.org/abs/1804.03999)	|2018	  | 0.665	|0.717	  |0.967	  |0.897	  |0.787 | 0.566 
Alom  etc. all [R2U-Net](https://arxiv.org/ftp/arxiv/papers/1802/1802.06955.pdf)	        |2018	  | 0.691	|0.726	  |0.971	  |0.904	  |0.822 | 0.592
Azad etc. all [Proposed BCDU-Net](https://github.com/rezazad68/LSTM-U-net/edit/master/README.md)	  |2019 	| **0.847**	|**0.783**	  |**0.980**	  |**0.936**	  |**0.922**| **0.936**





#### Skin Lesion Segmentation results

![Skin Lesion Segmentation result 1](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/1%20(1).png)
![Skin Lesion Segmentation result 1](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/1%20(2).png)
![Skin Lesion Segmentation result 1](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/1%20(3).png)
![Skin Lesion Segmentation result 1](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/1%20(4).png)


## Lung Segmentation

#### Performance Evalution on the Lung Segmentation task

Methods | Year |F1-scores | Sensivity| Specificaty| Accuracy | PC | JS 
------------ | -------------|----|-----------------|----|---- |---- |---- 
Ronneberger and etc. all [U-net](https://arxiv.org/abs/1505.04597)	     	    |2015   | 0.647	|0.708	  |0.964	  |0.890  |0.779 |0.549
Alom  etc. all [Recurrent Residual U-net](https://arxiv.org/abs/1802.06955)	|2018	  | 0.679 |0.792 |0.928 |0.880	  |0.741	  |0.581
Oktay  etc. all [Attention U-net](https://arxiv.org/abs/1804.03999)	|2018	  | 0.665	|0.717	  |0.967	  |0.897	  |0.787 | 0.566 
Alom  etc. all [R2U-Net](https://arxiv.org/ftp/arxiv/papers/1802/1802.06955.pdf)	        |2018	  | 0.691	|0.726	  |0.971	  |0.904	  |0.822 | 0.592
Azad etc. all [Proposed BCDU-Net](https://github.com/rezazad68/LSTM-U-net/edit/master/README.md)	  |2019 	| **0.847**	|**0.783**	  |**0.980**	  |**0.936**	  |**0.922**| **0.936**





#### Lung Segmentation results
![Lung Segmentation result 1](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/es3.png)
![Lung Segmentation result 2](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/es5.png)
![Lung Segmentation result 3](https://github.com/rezazad68/LSTM-U-net/blob/master/output_images/est2.png)




### Model weights
You can download the learned weights for each task in the following table. 

Task | Dataset |Learned weights
------------ | -------------|----
Retina Blood Vessel Segmentation | [Drive](http://www.isi.uu.nl/Research/Databases/DRIVE/) |[BCDU_net_D3](https://drive.google.com/open?id=1_hpfspGGJcWyFcGLXkFUa4k1NdUyOSOb)
Skin Lesion Segmentation | [ISIC2018](https://challenge.kitware.com/#phase/5abcb19a56357d0139260e53) |[BCDU_net_D3](https://drive.google.com/open?id=1EPRC-YmMk0AjHbdjoVy53jlSuweSbAHX)
Lung Segmentation | [ISIC2018](https://challenge.kitware.com/#phase/5abcb19a56357d0139260e53) | [BCDU_net_D3](https://drive.google.com/open?id=1pHOntUOdqd0MSz4cHUOHi2Ssn3KBH-fU)



### Query
Implementation done by Reza Azad. For any query please contact us for more information.

```python
rezazad68@gmail.com

```
