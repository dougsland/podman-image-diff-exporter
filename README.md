# podman-image-diff-exporter

The podman-image-diff-exporter utility facilitates a comparison between the current state of a container image and its original version by mounting both the container and the image onto the filesystem. This process enables a detailed examination of the disparities between the two. Ultimately, the tool produces a compressed (.tar.gz) file containing the identified differences, providing a comprehensive snapshot of the changes made to the container image over time.

Consider this scenario: your vehicle is currently operating on version 1 of a containerized image, and you're contemplating an upgrade to version 2. It's crucial to ensure that any files created or modified within the container environment are seamlessly preserved during this upgrade process. The objective is to guarantee a smooth transition to the updated container image while safeguarding the integrity of customizations and modifications made within the system.

Example:
```
./podman-image-diff-exporter --image-name fedora --verbose --container-name fedora
```
