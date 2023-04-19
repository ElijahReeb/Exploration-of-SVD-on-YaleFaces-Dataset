# UW-EE399-Assignment-2
This holds the code and backing for the second assignment of the EE399 class. It uses the 'yalefaces' dataset in order to demonstrate singular value decomposition (SVD).

Project Author: Elijah Reeb, elireeb@uw.edu

.. contents:: Table of Contents

Homework 2
---------------------
Introduction
^^^^^^^^^^^^
This assignment involved the use of the 'yalefaces' data set. This dataset holds 2414 images of faces with various lighting. Each face was cropped and centered into a 32x32 grid and converted to a 1024 vector. This creates a matrix of 1024x2414 which will be indexed and manipulated in order to demonstrate how Single Value Decomposition (SVD) can be used in order to categorize these faces. This assignment will show how using the techniques of linear algebra one can determine "eigenfaces" which hold information that can be used to classify the mathematical characteristics shared by the faces in the dataset.

Theoretical Backgroud
^^^^^^^^^^^^
After loading in the faces into a matrix, a quick dot product allows for one to observe the correlation between each pair of faces. This was done with the code below and produced the graph under it. 

.. code-block:: text

        nfaces = 100
        Xm=X[:, 0:nfaces]
        C=np.matmul(Xm.T,Xm)

.. image:: ![image](https://user-images.githubusercontent.com/130190276/232985736-5ef9b74c-c460-4b69-98e1-9a9fc94d6423.png)

This code produces a correlation matrix that allows us to see which two faces are closest mathematically as two (unitary) vectors are closest to the same when their dot product approaches 1. If observe the specific values we can plot the two faces that are closest and those furthest away. These turned out to be a face and itself (two closest faces were the same face) and the same for the furthest faces. These images are plotted below (only one shown to prevent redundancy). 

.. image:: ![image](https://user-images.githubusercontent.com/130190276/232986635-40beaccd-d23e-48fb-a533-3070eed385e6.png)

Looking at certain specific faces we can determine ones that are even closer together. When a subset of faces are compared it produces the following matrix. Notice the large correlation in the center. 

.. image:: ![image](https://user-images.githubusercontent.com/130190276/232986883-1fd44f06-b268-4bcd-9758-db951b665604.png)

This use of linear algebra between the matricies shows a mathematically simple way to determine relation between images. But this can be expanded further as discussed below.

Algorithm Implementation and Development
^^^^^^^^^^^^
The principles of face correlation described above can be translated with more linear algebra with the properties of matricies of the eigenvalues and eigenvectors. After the matrix of faces is multiplied by its transpose to create a diagonal matrix the eigenvectors become apparant and can be used to see relationships between the faces. This is done with the simple lines below to create this matrix and find its eigenvalues and eigenvectors. 

.. code-block:: text

        Y=np.matmul(X,X.T)
        vals,vects = np.linalg.eig(Y)

After plotting the highest eigen vectors of these newly calculated arrays we can find the so called "eigenfaces" which hold certain measures that are common in all faces. The first 6 "eigenfaces" are plotted below. 

![image](https://user-images.githubusercontent.com/130190276/232988008-b4cafae6-e503-42c7-8fb3-f5bfcd231dfc.png)

Furthering this, we can use the Single Value Decomposition (SVD) method in order to calculate something similar. Numpy's linalg package gives the simple svd command which allows a similar calculation to find the principle component directions of the face matrix. They are plotted below. 

.. code-block:: text

        u,s,v=np.linalg.svd(X)

..image:: ![image](https://user-images.githubusercontent.com/130190276/232988571-96514cca-5f52-43d7-8373-d4c7245062de.png)

Comparing these two sets of plots we can see similar characteristics emerge in the faces with face 3 appearing almost identical in the two methods. Due to slight different math behind these two calculations there is slight difference but that will be explained in the next section. 

Computational Results
^^^^^^^^^^^^
When the first eigenvector and the first SVD mode are compared the norm of their differences is about 1.4. This shows that there is not much difference between the two images (as the same image has a norm difference of 0 with itself). Comparing the images, they appear near opposites meaning the absolute value is important to consider here. 

.. code-block:: text
        dif = v1 - u1
        norm = np.linalg.norm(dif)

Next the percentage of variance captured by each of the first 6 SVD modes were calculated and printed below.
[0.16614047 0.07605299 0.03116886 0.02665768 0.0155555  0.01497437]
As seen, the first mode covers a large percent of the variance with a large dropoff where very little variance is covered by the 5th and 6th modes. Note that observing modes 7 onward this trend of very small variance continues. 

Summary and Conclusions
^^^^^^^^^^^^
We can see that this method is not perfect in determining the variation between faces. It does however provide a mathematical system that a new face can be projected onto in order to determine how the feature spaces compare. This is a good test dataset, but the quality makes it difficult to see all of the different features of faces, however this provides a good starting point to observe the results of matrix manipulation to determine correlation. 
To sum it up, the use of linear algebra through eigenvectors and dot products allows a simple mathematical way to compare images and determine relative correlation. These methods however are very reliant on front-end work such as cropping and centering the faces. If images do not have comparable features in comparable places then these mathematical technqiues will fail. We observed how with just a few SVD modes or eigenvectors a relatively large amount of the variance in the data can be captured. This method has promise to help become a building block for later algorithms. 
