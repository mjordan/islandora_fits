# Islandora FITS
Config module to make Islandora aware of FITS microservice

## Installation
#### Install this module
Install and enable this module in the usual way


#### Install FITS Webservice
FITS xmls are generated from an easily installed web service.  
Get the latest fits.zip and fits.war from https://projects.iq.harvard.edu/fits/downloads
(on my box I had to install a missing zip library with ‘sudo apt-get install php7.1-zip’)

Install following their instructions.
Copy the .war file to your webapps directory  and test.
Edit the catalina.properties file on the Drupal server by adding the following two lines to the bottom of the file-

fits.home=/<path-to-fits>/fits
shared.loader=/<path-to-fits>/fits/lib/*.jar

Restart Tomcat and test with 

`curl -k -F datafile="@/path/to/myfile.jpg" http://example.com:8080/fits/examine`
(note: the ‘@’ is required.)

#### Installing Microservice 
Get code from https://github.com/roblib/CrayFits and install.  This code can live anywhere, including an external server, 
but most installations will have it at /var/www/html.

The App runs by entering php bin/console server:start *:8050 in the App root folder.
The server is stopped with php bin/console server:stop.  On a production machine you'd probably want to configure an additonal port in Apache.


Note: The location of the fits webserver is stored in the .env file in the root dir of the Symfony app.  This will have to be reconfigured if the Fits server is anywhere other than localhost:8080/fits

#### Adding FITs requests to the queue
Copy the file `assets/ca.islandora.alpaca.connector.ocr.blueprint.xml` to `/opt/karak/deploy` on your server.  There is no need to restart.

#### Adding Checksum to Display
A pseudo field with the computed checksum can be added to Repository Item display.  Naviage to `admin/structure/types/manage/islandora_object/display` to enable or disable display of `File Checksum`.  
