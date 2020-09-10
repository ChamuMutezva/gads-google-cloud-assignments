#  Getting Started with Cloud Storage and Cloud SQL
## Deploy a web server VM instance

Open Cloud shell and type in the following command
```
gcloud beta compute --project=qwiklabs-gcp-labs instances create onetwotesting --zone=us-central1-a --machine-type=e2-medium --subnet=default --network-tier=PREMIUM --metadata=startup-script=apt-get\ update$'\n'apt-get\ install\ apache2\ php\ php-mysql\ -y$'\n'service\ apache2\ restart --maintenance-policy=MIGRATE --service-account=565080145140-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --tags=http-server --image=debian-9-stretch-v20200902 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=bloghost --reservation-affinity=any
gcloud compute --project=qwiklabs-gcp-03-b04c8ad971dd firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server
```

The command will create a vm instance called `onetwotesting` in the zone `us=central1-a` with the specified machine types and boot disk. A startup script is also included in the command - this will be executed when the vm instance starts

### Creating a Cloud Storage bucket using the gsutil command line
All Cloud Storage bucket names must be globally unique. Cloud Storage buckets can be associated with either a region or a multi-region location: US, EU, or ASIA.

1. Activate Cloud Shell if not open and click `Start Cloud Shell`
2. For convenience, enter your chosen location into an `environment variable` called *LOCATION*. EG 
`export LOCATION=US`
3. In Cloud Shell, the `DEVSHELL_PROJECT_ID` environment variable contains your project ID. Enter this command to make a bucket named after your project ID:   `gsutil mb -l $LOCATION gs://$DEVSHELL_PROJECT_ID`
4. You can retrieve a banner image from a publicly accessible Cloud Storage location: eg
    `gsutil cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png`
5.  Copy the banner image to your newly created Cloud Storage bucket:
    `gsutil cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png`
6. Modify the Access Control List of the object you just created so that it is readable by everyone:
    `gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png`

    

