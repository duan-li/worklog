---
layout: page
title: GCP
---

## Regions and Zones [^rz]

[^rz]: [Regions and Zones](https://cloud.google.com/compute/docs/regions-zones/)

Region | Zones | Location
------------ | ------------- | ------------
asia-east1 | a, b, c | Changhua County, Taiwan
asia-east2 | a, b, c | Hong Kong
asia-northeast1 | a, b, c | Tokyo, Japan
asia-northeast2 | a, b, c | Osaka, Japan
asia-south1 | a, b, c | Mumbai, India
asia-southeast1 | a, b, c | Jurong West, Singapore
australia-southeast1 | a, b, c | Sydney, Australia
europe-north1 | a, b, c | Hamina, Finland
europe-west1 | b, c, d | St. Ghislain, Belgium
europe-west2 | a, b, c | London, England, UK
europe-west3 | a, b, c | Frankfurt, Germany
europe-west4 | a, b, c | Eemshaven, Netherlands
europe-west6 | a, b, c | Zürich, Switzerland
northamerica-northeast1 | a, b, c | Montréal, Québec, Canada
southamerica-east1 | a, b, c | Osasco (São Paulo), Brazil
us-central1 | a, b, c, f | Council Bluffs, Iowa, USA
us-east1 | b, c, d | Moncks Corner, South Carolina, USA
us-east4 | a, b, c | Ashburn, Northern Virginia, USA
us-west1 | a, b, c | The Dalles, Oregon, USA
us-west2 | a, b, c | Los Angeles, California, USA

## VM instances

### Help
```bash
gcloud compute instances create --help
```

### Create 
```bash
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone us-central1-c
```

### SSH access
```bash
gcloud compute ssh gcelab2 --zone us-central1-c

```
---