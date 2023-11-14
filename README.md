# podman-image-diff-exporter

The podman-image-diff-exporter utility facilitates a comparison between the current state of a container image and its original version by mounting both the container and the image onto the filesystem. This process enables a detailed examination of the disparities between the two. Ultimately, the tool produces a compressed (.tar.gz) file containing the identified differences, providing a comprehensive snapshot of the changes made to the container image over time.

Example:
```
./podman-image-diff-exporter --image-name fedora --verbose --container-name fedora
```
