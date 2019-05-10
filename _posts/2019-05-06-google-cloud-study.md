---
layout: post
title: Google cloud study
date: 2019-05-06 22:31 +0000
---

### Basic
```bash
# list the active account name with this command:
gcloud auth list

# you can list the project ID with this command:
gcloud config list project
```

### Install TensorFlow
```bash
# Run the following command to install TensorFlow:
pip install --user --upgrade tensorflow

# Verify the installation:
python -c "import tensorflow as tf; print('TensorFlow version {} is installed.'.format(tf.VERSION))"

```

### Grap example
```bash
git clone https://github.com/GoogleCloudPlatform/cloudml-samples.git

cd cloudml-samples/census/estimator
```

### training data

```bash
# Run the following command to download the data to a local file directory and set variables that point to the downloaded data files:

mkdir data
gsutil -m cp gs://cloud-samples-data/ml-engine/census/data/* data/

#Now set the TRAIN_DATA and EVAL_DATA variables to your local file paths by running the following commands:

export TRAIN_DATA=$(pwd)/data/adult.data.csv
export EVAL_DATA=$(pwd)/data/adult.test.csv

#To open the adult.data.csv file, run the following command:

head data/adult.data.csv
```

### dependencies

Although TensorFlow is installed on Cloud Shell, you must run the sample's `requirements.txt` file to ensure you are using the same version of TensorFlow required by the sample:

```bash
pip install --user -r ../requirements.txt
```


### Run a local training job

Specify an output directory and set a MODEL_DIR variable by running the following command:
```bash
export MODEL_DIR=output
```
Run this training job locally by running the following command:
```bash
gcloud ml-engine local train \
    --module-name trainer.task \
    --package-path trainer/ \
    --job-dir $MODEL_DIR \
    -- \
    --train-files $TRAIN_DATA \
    --eval-files $EVAL_DATA \
    --train-steps 1000 \
    --eval-steps 100
```

### TensorBoard
Launch TensorBoard:
```bash
tensorboard --logdir=$MODEL_DIR --port=8080
```


### Running model prediction locally

```bash
ls output/export/census/

# output like 1557186901


gcloud ml-engine local predict \
--model-dir output/export/census/<timestamp> \
--json-instances ../test.json

gcloud ai-platform local predict \
--model-dir output/export/census/<timestamp> \
--json-instances ../test.json

# example of
gcloud ml-engine local predict \
--model-dir output/export/census/1557186901 \
--json-instances ../test.json


# CLASS_IDS  CLASSES  LOGISTIC                LOGITS                PROBABILITIES
# [0]        [u'0']   [0.043588194996118546]  [-3.088402271270752]  [0.9564118385314941, 0.043588194996118546]
```


### Google Cloud Storage

The Cloud ML Engine services need to access Google Cloud Storage (GCS) to read and write data during model training and batch prediction.

```bash
# First, set the following variables:

PROJECT_ID=$(gcloud config list project --format "value(core.project)")
BUCKET_NAME=${PROJECT_ID}-mlengine
echo $BUCKET_NAME
REGION=us-central1

# Create the new bucket:

gsutil mb -l $REGION gs://$BUCKET_NAME
```


---