# filebeat-boshrelease
BOSH release for filebeat log shipper.

filebeat is a logshipper from elastic (elastic.co).

## Creating a development bosh release
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

## Creating a final release

1.  create bosh final release (requires s3 credentials in `config/final.yml`)
```
export VERSION=x.y.z
bosh create-release --final --version=$VERSION --name=filebeat --tarball=releases/filebeat/filebeat-$VERSION.tgz
```

1. commit and push changes
```
git add releases .final_builds/
git commit -m"BOSH release $VERSION"
git tag v$VERSION
git push origin master
git push --tags
```

1. Create a release from the new tag and upload the tarball `releases/filebeat/filebeat-$VERSION.tgz`.

It is helpful to include a `releases` snippet showing how to include this release into a deployment. To generate the sha of the tarball blob:
```
shasum releases/filebeat/filebeat-$VERSION.tgz
```
