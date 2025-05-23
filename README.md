# oci-spec-implementation
Create Containers from Scratch &amp; Implement OCI Spec

## Prerequisites
- ORAS
- Crane
- an oci-compliant registry (e.g, Harbor)

## Steps
first push the kumar.txt file with oras
`❯ oras push localhost:5000/kumar/oras:latest kumar.txt`

then use crane to export the container to filesystem to understand how it is done
use
`crane export -h`
to get available options

use the below cmd to generate the model
```
$ modctl modelfile generate .
```
use the below command to build the model
```
$ modctl build -t localhost:5000/models:v1.0 -f Modelfile .
```
use the below cmd to push the model
```
❯ modctl push localhost:5000/models:v1.0 --insecure --plain-http
```

after this we need to pull the model we uploaded
so that we can learn its oci-layout
```
❯ crane pull localhost:5000/models/lesslayer:v2 --insecure --format=oci kumar-oci
```

we can see that the model have been changed into oci format we can edit recalculate the hashes and repush this model

```json
{
   "schemaVersion": 2,
   "mediaType": "application/vnd.oci.image.index.v1+json",
   "manifests": [
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 1331,
         "digest": "sha256:667c2d3c0389685459e14680c7a15dffa38aad59d6b8adeabaa9b6507ee55c12",
         "artifactType": "application/vnd.cnai.model.config.v1+json"
      }
   ]
}
```

then we need to calculate the hashes of each file in the oci-layout directory
```
find . -type f -exec sha256sum {} \;
```


