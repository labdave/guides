# Data transfer to Google Cloud Platform (GCP)

The guide provides details to transfer seqeuncing data files from `linux` server to [GCP].

## Requirements
* [Python 3]
* [Google Cloud SDK]
* [GCP] authentication - Please provide an email address for the personnel who will push the data to the bucket. The 
  system admin will grant access for the respective individual using the provided email address.

### Install Google Cloud SDK on linux server
Follow the following steps to install the [Google Cloud SDK].

```bash
# install SDK to desired location
$ curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-335.0.0-linux-x86_64.tar.gz

# extract the contents
$ tar -xzvf curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-335.0.0-linux-x86_64.tar.gz

# run the installation script
$ ./google-cloud-sdk/install.sh

# initialize the SDK and select appropriate options
$ ./google-cloud-sdk/bin/gcloud init --console-only
```

### Files to transfer
List of files to transfer
* FASTQ file (including the underemined read files)
* Demultiplex report
* MD5SUM check file - a two column text file with first column contianing the file name and second column containing 
  the MD5SUM check
  
# Requirements to have in-hand before transferring the files
Please make sure of the followings before transferring the data files:
* You have permission to push the data file to the bucket.
* You have correct bucket name to push the data to.
* You must transfer the data file to the correct flowcell bucket.

# Transfer one file
Please use the command line below to transfer a single file to the bucket

```bash
# syntax
$ gsutil cp <file_name> <bucket_name>

# examples
$ gsutil cp sample1.R1.fastq.gz gs://davelab_duke_core/HWAXDSXY/
$ gsutil cp demux.csv gs://davelab_duke_core/HWAXDSXY/
$ gsutil cp ms5sum_check.md5 gs://davelab_duke_core/HWAXDSXY/
```

# Transfer multiple files
A `bash` script helps to transfer more than one file systematically. Please use the following steps to transfer the 
multiple files.

1. Create a file containing all the files to transfer
2. Use the `bash` script template shown below to make your script

```bash
#!/bin/bash

for file in `cat files`;
do
  # change the bucket and flowcell name
  gsutil cp ${file} gs://davelab_duke_core/HWAXDSXY/
 done;
 
 exit;
```

After you transfer all the data files, please transfer an empty file with extension `.done` (e.g. `HWAXDSXY.done`).



[Python 3]:https://www.python.org/download/releases/3.0/
[GCP]:https://cloud.google.com/
[Google Cloud SDK]:https://cloud.google.com/sdk/docs/quickstart