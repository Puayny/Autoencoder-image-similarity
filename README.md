The main purpose of this exercise is to understand autoencoders.

<strong>In part 1, I model autoencoder networks for the MNIST and cifar-100 datasets.</strong>

The MNIST dataset was reduced from from 784 dimensions to 64 dimensions, while the cifar-100 dataset was reduced from 3072 dimensions to 512 dimensions.<br><br>
In both cases, the object category can generally still be discerned from the reconstrucuted autoencoded images.<br><br>
I'd hoped to achieve more dimensionality reduction on the cifar-100 dataset, but reconstruction quality is too low with further reduction. Perhaps the cifar images are pretty low resolution to begin with, making any loss of information through autoencoding more significant?<br><br>
I used binary cross entropy as the loss function. The model runs much slower if cosine similarity is used.<br><br>

<strong>In part 2, I use the encoded representation of the images to find similar images.</strong>

I tried using binary cross entropy and cosine similarity to determine similarity of the encoded vectors, as a proxy for image similarity. The results returned by both tend to be visually similar.<br><br>
For the MNIST dataset, where most images are centered, this similarity comparison tends to work well, and digits of the same type are deemed to be similar. However, any significant shifts in the position of the digit will lead to it being deemed to be dissimilar.<br><br>
For the cifar-100 dataset, images with a similar background color / shape are deemed to be similar, rather than images of the same type of object (e.g. with the current similarity metric, flowers are not usually deemed to be similar to other flowers).<br><br>
As a baseline comparison, I used binary cross entropy to determine image similarity based on the original image dimensions (rather than the encoded dimensions). 
Much like the results from the reduced dimensions, images with a similar background color / shape are deemed to be similar.<br><br>
My original hope was that the image features learned by the autoencoder in the encoded layer would have lead to a decent way of determining image similarity.
Unfortunately, since the autoencoder simply tries to reconstruct the original image, it does not necessarily encode features which would have been useful in determining image similarity (in the sense of flowers being deemed to be similar to flowers). Also, the similarity metric places equal focus on all parts of the images, rather than the parts which could be more important (e.g. the subject of the image).
