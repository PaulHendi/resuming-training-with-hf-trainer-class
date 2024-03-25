# Resuming training

The notebook demonstrates a way to save model checkpoints during training using the Trainer class from Hugging Face <img src="./images/HF.png" width="15" height="15">
. It not only saves checkpoints locally but also to cloud storage services, with examples for Amazon S3 and Google Cloud Storage (GCS).

Note that using Sagemaker it is considered best practice to execute a training with Trainer from within a Deep Learning Container as shown [here](https://huggingface.co/docs/sagemaker/index#deep-learning-containers), and by using the <img src="./images/HF.png" width="15" height="15"> Estimator it is easy to do [checkpointing to S3](https://huggingface.co/docs/sagemaker/train#training-output-management). 

We assume here that the training is done locally regardless of any cloud provider, therefore the method describe in the notebook is based on the [TrainerCallback](https://huggingface.co/docs/transformers/v4.29.1/en/main_classes/callback#transformers.TrainerCallback).

> We can also [push the model checkpoint to the Hugging face hub](https://huggingface.co/docs/transformers/main_classes/trainer#transformers.TrainingArguments.push_to_hub) everytime there is a new save, but here we focus on saving checkpoints to cloud storages like S3 or GCS buckets.



## Requirements

To run the python script, you need:

- Python 3.8 or later
- <img src="./images/HF.png" width="15" height="15"> Transformers library (and more depending on your training)
- Boto3 for Amazon S3 (if using S3 for storage)
- Google Cloud Storage Python client (if using GCS for storage)

Note that there is a requirements.txt file which you can use to install the libraries : 
```bash
pip instal -r requirements.txt
```

Since we are saving checkpoints to buckets, we need to create buckets but we also need credentials in order to use the S3 and GCS sdk. To create a bucket from the console, you can follow this [link](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) for AWS or this [one](https://cloud.google.com/storage/docs/creating-buckets) for GCP.

### S3 local configuration
You will need to install [aws cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) and then authenticate following this [guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-authentication.html)

### GCS local configuration
You will need to install [gcloud](https://cloud.google.com/sdk/docs/install) and authenticate in the terminal with ```gcloud auth application-default login``` before using the sdk


## Usage

You can follow along the notebook to have a simple example.
