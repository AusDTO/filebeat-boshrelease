# filebeat-boshrelease
BOSH release for filebeat log shipper.

filebeat is a logshipper from elastic (elastic.co).

### Creating a development bosh release
```
bosh create release --force
bosh upload release
```

### Deploying to *bosh-lite*.
a sample cloud-config and deployment manifest is provided in the `templates` directory.

```
bosh update cloud-config templates/bosh-lite-cloud-config.yml
bosh deployment templates/bosh-lite-deployment.yml
bosh deploy
```
