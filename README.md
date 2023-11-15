# podman-image-diff-exporter

The podman-image-diff-exporter utility facilitates a comparison between the current state of a container image and its original version by mounting both the container and the image onto the filesystem. This process enables a detailed examination of the disparities between the two. Ultimately, the tool produces a compressed (.tar.gz) file containing the identified differences, providing a comprehensive snapshot of the changes made to the container image over time.

Consider this scenario: your vehicle is currently operating on version 1 of a containerized image, and you're contemplating an upgrade to version 2. It's crucial to ensure that any files created or modified within the container environment are seamlessly preserved during this upgrade process. The objective is to guarantee a smooth transition to the updated container image while safeguarding the integrity of customizations and modifications made within the system.

Example, generating the .tar.gz:
```
# ./podman-image-diff-exporter --image-name fedora --container-name myfedora

Summary
====================
Tuesday, November 14, 2023 17:31:25 EST

New:
	 /etc/auto-rhivos /etc/cow-team

Changed:
	 /etc/libaudit.conf

Removed:
	 /etc/localtime

Generated 2023-11-14-173125-exported-container-fedora-image-myfedora.tar.gz
```

## Output tarball
```
# tar zxvf 2023-11-14-173125-exported-container-fedora-image-myfedora.tar.gz
./tmp.XMTiZFD8q3/
./tmp.XMTiZFD8q3/etc/
./tmp.XMTiZFD8q3/etc/auto-rhivos
./tmp.XMTiZFD8q3/etc/cow-team
./tmp.XMTiZFD8q3/etc/libaudit.conf
./tmp.XMTiZFD8q3/metadata.json
./tmp.XMTiZFD8q3/summary
./tmp.XMTiZFD8q3/import_files_to_container
```

## About the tarball

File                      | Description
------------------------- | -------------
metadata.json             | Metadata file
import_files_to_container | Tool to import files from .tar.gz to container
summary                   | Summary of the tool
/etc/auto-rhivos          | New file detected
/etc/cow-team             | New file detected
/etc/libaudit.conf        | File changed detected

## Metadata format and fields**

Example of metadata json:
```
{
"./tmp.XMTiZFD8q3/etc/auto-rhivos": { "size": 0, "sha256sum": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855", "destdir": "/etc", "permission": 644 },
"./tmp.XMTiZFD8q3/etc/cow-team": { "size": 0, "sha256sum": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855", "destdir": "/etc", "permission": 644 },
"./tmp.XMTiZFD8q3/etc/libaudit.conf": { "size": 201, "sha256sum": "8887c253c82da4a2a81520ace9f2dce1cd0626320d49800e106a5b5719b68817", "destdir": "/etc", "permission": 640 }
}
```

## Description of the metadata json

Each entry begins with the path of the file, copied from the original container, and is followed by fields that provide descriptions of the file.

Fields     | Description
--------   | ----------------
size       | Size of the file
sha256sum  | sha256sum digest
destdir    | The destiny dir for the file
permission | octal permission
