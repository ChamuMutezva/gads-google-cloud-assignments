# Getting Started with Compute Engine
## Create a virtual machine using the gcloud command line

1. In GCP console, on the top right toolbar, click the **Open Cloud Shell** button.

2. Click Continue.

3. Display a list of all the zones in the region to which Qwiklabs assigned you, enter this partial command `gcloud compute zones list | grep` followed by the region eg. `gcloud compute zones list | grep us-central1`

4. Choose a zone and a region from that list. For example region *us-central1* and zone *us-central1-a* 

5. Set your default zone to the one you just chose, enter this partial command `gcloud config set compute/zone` followed by the zone you chose.
eg. `gcloud config set compute/zone us-central1-b`

6. To create a VM instance called **my-vm-2** in that zone, execute this command:

```
gcloud compute instances create "my-vm-2" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20190213" \
--subnet "default"
```

7. close the Cloud Shell, execute the **exit** command

