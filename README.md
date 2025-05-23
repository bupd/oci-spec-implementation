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
