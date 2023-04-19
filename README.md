# UW-EE399-Assignment-2
This holds the code and backing for the second assignment of the EE399 class. It uses the 'yalefaces' dataset in order to demonstrate singular value decomposition (SVD).

Project Author: Elijah Reeb, elireeb@uw.edu

.. contents:: Table of Contents

Homework 2
---------------------
Introduction
^^^^^^^^^^^^
This assignment involved the use of the 'yalefaces' data set. This dataset holds 2414 images of faces with various lighting. Each face was cropped and centered into a 32x32 grid and converted to a 1024 vector. This creates a matrix of 1024x2414 which will be indexed and manipulated in order to demonstrate how Single Value Decomposition (SVD) can be used in order to categorize these faces. This assignment will show how using the techniques of linear algebra one can determine "eigenfaces" which hold information that can be used to 



Theoretical Backgroud
^^^^^^^^^^^^

.. code-block:: text

        fit = np.polyfit(x,y,19)
        model = np.poly1d(fit)


Computational Results
^^^^^^^^^^^^

.. image:: https://user-images.githubusercontent.com/130190276/231073437-a90b1201-3d3c-4d46-8e42-5a324d96edb1.png

Summary and Conclusions
^^^^^^^^^^^^
