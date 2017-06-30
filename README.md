# docker_contao
Dockerfiles for Contao-Installations coming along with sample configuration files for the docker composer.

If not mentioned otherwise, the images require a mysql database somewhere reachbale via network. In the docker-compose.yml files I use the standard mysql:latest image of the docker library.

After starting the image, the installation of contao has to be completed via the standard installation tool. 
In the 4.4-manager variant, the manager has to be called on the address http://[image:80]/contao-manager.phar.php as mentioned in the installation manual of the contao menager.

Currently available are the following version / tags:

3.5.27: simple installation of the latest 3.5-version of contao

4.4.0-manual: manual installation version 

4.4-composer: composer variant of the 4.4 contao release

4.4-manager: manager installation variant of the 4.4. contao release


