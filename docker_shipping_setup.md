
# Moving local container to the server

## Step 1: Save Container as Image

### Identify the Container ID

First, list all running containers to find the ID of the one you want to save:

```bash
docker ps
```

### Commit the Container to an Image

Use the `docker commit` command to save the container as a new image:

```bash
docker commit CONTAINER_ID IMAGE_NAME
```

Replace `CONTAINER_ID` with your actual container ID and `IMAGE_NAME` with your desired image name.

## Step 2: Save Image to Tar File

Save the image to a tar file for transfer:

```bash
docker save -o image.tar IMAGE_NAME
```

## Step 3: Transfer Tar File to Server


### Transfer the Tar File

Use your `USERNAME` and `PASSWORD` with scp to transfer the tar file to the server (`SERVER_IP`):

```bash
scp image.tar USERNAME@SERVER_IP:/home/USERNAME/
```

Replace `USERNAME` and `SERVER_IP` with your actual server credentials.

## Step 4: Load and Run the Image on the Server

### Connect to the Server

Log in to your server using SSH:

```bash
ssh USERNAME@SERVER_IP
```

**Note:** Keep in mind the ports that you want to map with the VM. For example, if you need to access the `8888` port on the container or the VM, you need to map that port to your localhost when connecting to the server. This can be done as follows:

```bash
ssh -L 8888:localhost:8888 USERNAME@SERVER_IP
```

### Load the Image

Use the docker load command to load the image from the tar file:

```bash
docker load -i /home/USERNAME/image.tar
```

### Run the Image

Once loaded, you can run the image using the docker run command:

```bash
docker run IMAGE_NAME
```
