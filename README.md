# PotholeDetection
An AWS micro-service classifier for classifying potholes and plain road images.


Data: https://www.kaggle.com/virenbr11/pothole-and-plain-rode-images 
Goal: to train an Image Classifier, using the GPUs (p2.xlarge) available through Amazon's AWS.
Preprocessing steps:
1. Create an AWS account and create an instance.
2. Request a GPU of p2.xlarge size or more for your instance.
3. Connect the S3 storage to the AWS instance.
4. Open S3 services and upload the files. Folder tree is very important here.
5. Feature Engineering
    Generating LST files
    Using lst_generator.py, we create 2 separate files with the suffixes train.lst and test.lst. A typical LST file contains a list of information, separated by line breaks. In our case, these lst files are a mapper between the images, a label assigned to them (0 or 1 for binary classification) and their relative path.
6. Start a training job in Sagemaker
    using the pre-existing ImageClassification model.
    my parameters were: num_classes: 2, num_of_training_examples: 200, and memory: 60GB. (the classifier ran out of memory at 40GB)

The remaining steps of creating a complete end-to-end AWS microservice are as follows:
7. Create model Used the default Sagemaker settings to create a model once the training job was over - took 23minutes
8. Create an endpoint Other than the name fields, I kept the default settings for creating an endpoint as well. Takes a small amount of time.
9. Lambda function (provided on request)
10. Create an IAM role for Lambda and deploy. Create a test event with a base64 type of images to test deployment.
11. Create an API Gateway on AWS and finally create a POST function for the link to the 'url' to be invoked externally. I used POSTMAN. Curl can also be used.
