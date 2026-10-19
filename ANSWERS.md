## 1. Dockerfile instruction order

I start with the Python base image and set the working directory.
I copy requirements.txt and install the dependencies before copying app.py.
This allows Docker to reuse the dependency layer when only my application code changes.
If I moved COPY app.py before RUN pip install, changing app.py would invalidate the cache for the installation step and make rebuilds slower.

## 2. Container data and persistence

Files stored only in a container's writable layer are lost when the container is removed.
Stopping a container does not remove those files.
A named Docker volume can keep data independently of the container, and a bind mount can store files on the host.
Important application state should be stored in persistent storage, such as a database with a volume or an external database, with backups.

## 3. Image tags and reproducibility

The latest tag can point to a different image over time.
This means that building the same project later could use a different base image.
I used python:3.12.12-slim-bookworm as my base image and tagged my application image as selin-web:1.0.
Version tags make the intended version clearer, but they can also be updated; pinning an image digest provides a stronger guarantee of using the same image.

## AI assistance

I used ChatGPT to help prepare the Flask application, Dockerfile, and documentation, and to explain the commands step by step.
I built and ran the image on my Mac and checked the three endpoints.
