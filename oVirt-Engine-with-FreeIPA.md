Base Environment: CentOS 7

The guide assumes that you're running oVirt Engine with PostgreSQL as per the oVirt Engine with PostgreSQL in 
a container guide or the standard oVirt Engine installation that requires you to have PostgreSQL installed and
appropriately configured. 

### Steps
1. Make sure that the Docker service is running:

   `$ sudo service docker start`

or

   `$ sudo systemctl start docker.service`

2. Clone the repo to build the image. 
   
   `$ git clone https://github.com/freeipa/freeipa-container.git`
   
3. Build the Docker image.
   
   i. Change directory into where you've cloned the above repo:
      
      `$ cd freeipa-container/`
   
   FreeIPA provides the option of building images based on the following distributions:
   - CentOS
   - Fedora 
   - Red Hat Enterprise Linux
   
   By default, it will build for Fedora. To avoid this, copy the Dockerfile named `Dockerfile.centos-7` to `Dockerfile`
   as follows:
   
      `$ cp Dockerfile.centos-7 Dockerfile`
   
   This should make the build use CentOS 7. Do the same for RHEL if that's what you'd like. [1]
   
   ii. Build the image as follows:
   
      `sudo docker build -t freeipa-server`

4. Run the container image

   `sudo docker run --privileged --name ovirt-freeipa-server -ti -h ipa.ovirt.test -p 1443:443 -e PASSWORD=Secret123 freeipa/freeipa-server`

5. Make directory.

mkdir /var/lib/ipa-data


[1]: Here the README for FreeIPA containers says that the option to build an image based on something other that what is offered by the default target can be specified using the -f option. Didn't work for me. Reference [here.](https://github.com/freeipa/freeipa-container)
