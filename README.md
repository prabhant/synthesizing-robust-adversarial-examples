# Synthesizing robust adversarial examples
My entry for ICLR 2018 Reproducibility Challenge for paper Synthesizing robust adversarial examples https://openreview.net/pdf?id=BJDH5M-AW

# Review:
## Reproducibility Report
The current report has been generated as a part of ICLR reproducibility challenge http://www.cs.mcgill.ca/~jpineau/ICLR2018-ReproducibilityChallenge.html

Author: Prabhant Singh, University of Tartu, prabhant.singh@ut.ee

## Abstract:
The paper’s main goal was to provide an algorithm to generate adversarial examples that are robust across any chosen distribution of transformations. The author demonstrated this algorithm in 2 and 3 dimensions in the paper. The author was successfully able to demonstrate that adversarial examples are a practical concern for real-world systems. During the reproducibility of the paper, we have implemented authors algorithm on 2D scenario and was able to verify authors claim. We have also checked for transferability with the image of 3D adversarial example generated in this paper in the real-world environment. This report also checks the robustness of adversarial examples on black box scenario which is out of the scope of the selected paper.

## Experimental methodology:
After reproducing the Expectation Over Transformation(EOT) algorithm we have generated adversarial examples on the pre-trained inceptionV3 model trained on imagenet dataset. The adversarial examples were robust under the predefined distribution. One interesting observation here is that whenever we rotated the image out of the distribution there was confidence reduction in case of prediction and the target class which was predefined while creating the adversarial example was in the top 10 probabilities. The probability of Fooling class was decreased when we rotated it away from the distribution and vice versa. As the papers state that there are no guarantees of adversarial examples being robust outside the chosen distribution but the adversarial example was still able to reduce the confidence of the prediction.

## Transferability:
We checked 4 images of adversarial examples while checking transferability 1 of the adversarial examples we generated and 3 of adversarial Turtle mentioned in the paper[1] on 6 different architectures pre-trained on the imagenet dataset (Resnet50, InceptionV3, InceptionResnetV2, Xception, VGG16, VGG19). As our adversarial examples were generated using tensorflow pre-trained inception model here we are using the pre-trained model on keras for some variation[2].
The results of the experiments are listed below:

Generated adversarial image using EOT

**True class: Tabby cat**

1. InceptionV3:
Prediction: Flatworm, Confidence : 100%
2. InceptionResnet:
Prediction: Comicbook, Confidence : 100%
3. Xception:
Prediction: Necklace, Confidence : 92.5%
4. Resnet50:
Prediction: Tabby cat, Confidence: 35%
5. VGG 19:
Prediction: Tabby cat, Confidence: 47.9%
6. VGG16
Prediction: Tabby cat, Confidence: 34.8%

Original image of 3D adversarial turtle mentioned in the paper
**True class: Turtle**

1. InceptionV3:
Prediction: Pencil sharpner, Confidence : 67.7%
2. InceptionResnet:
Prediction: Comic book, Confidence : 100%
3. Xception:
Prediction: Table lamp, Confidence : 84.8%
4. Resnet50:
Prediction: Bucket , Confidence: 20%
5. VGG 19:
Prediction: Mask, Confidence: 10.9%
6. VGG16
Prediction: Turtle, Confidence: 3.6%

Other images of Adversarial turtle generated similar results.

## Observations:
Both images of adversarial turtle and cat were detected incorrectly by inception related architectures with a high confidence.
Both images were classified as “Comic book” with 100 percent confidence by InceptionResnetV2.
The adversarial examples were able to reduce the confidence by a high margin, about 50-60 percent in case of Tabbycat. Only VGG16 was able to classify the turtle correctly but by a very low confidence of 3.6%
Similar results were found when we rotated, cropped and Zoomed out of the image.[3]
In case of adversarial turtle the photo was clicked out of the distribution with respect to camera distance and background, still the image was misclassified.

## Conclusion:
The author successfully generated robust adversarial examples which are robust under the given distribution in case of targeted misclassification. The adversarial examples were also robust in case of Untargeted misclassification under any distribution if classified against Inception related models.The adversarial examples reduced confidence by a wide margin in case of non-inception architectures. The Image of 3D adversarial turtle can be considered robust under any distribution as it has been misclassified against all the architectures and only classified correctly by VGG16 but with a very insignificant percentage.

**Sources:**
* [1] The Image of adversarial turtle was clicked at the recent NIPS conference by a number of viewpoints out of the given distribution.

* [2] Pre-trained keras models: https://keras.io/applications/

* [3] The source code and experiments info can be found in this Github repo: https://github.com/prabhant/synthesizing-robust-adversarial-examples





