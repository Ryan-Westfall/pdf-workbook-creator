# pdf-workbook-creator

Automates the creation of a "workbook" outputting a pdf.

The generated workbook contains a table of contents and pages populated with images.

The user is expected to supply the data and images for the workbook to be generated.


# Production:

## To run the image:
You must have an **Input** directory on *your* machine that contains:
* A correctly formatted ***config.yml*** file.
* A correctly formatted ***pdf.json*** file.
* An ***images*** directory filled with images wanted in the workbook.

Preferably also include an output directory for the docker container to mount to

---

Run the production image with:
```
docker run -v $(pwd)/<input path>/:/app/input -v $(pwd)/<output path>/:/app/output -e "production=true" --user "$(id -u):$(id -g)" --rm ryanwestfall/pdf-workbook-creator:latest
```

# Development:

#### When running in development:
* The container will continously run until manually exited
* An express app will run on localhost:3000
* Hot realoading will be enabled on the express app and the outputted pdf file

### You must build the development image yourself to use the developemet tools
Build development image with:
```
docker build -t pdf-workbook-creator-dev -f Dockerfile.dev .
```
Run the development image with:
```
docker run -v $(pwd):/app/ -v /app/node_modules/ --user "$(id -u):$(id -g)" --rm -e "dev=true" -p 8000:8000 -p 3000:3000 pdf-workbook-creator-dev
```

