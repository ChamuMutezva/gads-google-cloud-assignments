# Getting Started with Compute Engine
## Create a virtual machine using the gcloud command line

In GCP console, on the top right toolbar, click the Open Cloud Shell button.

Click Continue.

To display a list of all the zones in the region to which Qwiklabs assigned you, enter this partial command gcloud compute zones list | grep followed by the region that Qwiklabs or your instructor assigned you to.
eg. gcloud compute zones list | grep us-central1

Choose a zone from that list other than the zone to which Qwiklabs assigned you. For example, if Qwiklabs assigned you to region us-central1 and zone us-central1-a you might choose zone us-central1-b.

To set your default zone to the one you just chose, enter this partial command gcloud config set compute/zone followed by the zone you chose.
eg. gcloud config set compute/zone us-central1-b

To create a VM instance called my-vm-2 in that zone, execute this command:

```
gcloud compute instances create "my-vm-2" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20190213" \
--subnet "default"
```

To close the Cloud Shell, execute the following command:
exit

