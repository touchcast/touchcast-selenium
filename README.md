# touchcast-selenium

A Docker project to run your own Selenium Grid and watch the tests fly via VNC.

Ensure you have all the Docker tools already installed.

### Manual build process:

`cd hub`  
`docker build --no-cache -t selenium/hub .`

`cd ..`  
`cd chrome`  
`docker build --no-cache -t selenium/chrome .`

`cd ..`  
`cd firefox`  
`docker build --no-cache -t selenium/firefox .`

`cd ..`  
`docker-compose up -d`

Now you should have 3 containers running, verify this by going:

`docker ps`

### Automatic build process:

Use the alternative `docker-compose.yml.prebuilt` by renaming it to `docker-compose.yml`  

Then run:

`docker-compose up -d`  

Now you should have 3 containers running, verify this by going:

`docker ps`  

### Yay, you have it running:

Selenium Grid Console is now available at:

`<docker ip address>:4444/grid/console`

To view what's going on, use VNC - Macs have "Screen Viewer" built-in, just type this into your favourite browser:

`vnc://<docker ip address>:5900` - to connect to the Firefox container  
`vnc://<docker ip address>:5901` - to connect to the Chrome container

If for some reason VNC service dies, connect to container and restart service:

`docker exec -it <container name> bash`

And then run:

`x11vnc -forever -usepw -shared -rfbport 5900 -display ":99.0" &`  
`exit`

Both Firefox and Chrome containers use VNC on port 5900, it's only you connecting via Docker on 5901 on the Chrome container, so don't go changing the VNC port on the container itself or the port mapping will fail!

Now you can use your Selenium Grid for testing.
