WebSocket Route
====================================
This bundle creates a simple route that consumes and produces messages via WebSockets

### Requirements:
 * JBoss Fuse 6.2.0
 * Maven 3.0 or Greater (http://maven.apache.org/)
 * Java 8
 * Internet browser supporting WebSockets

Building
-----------------------
To build the project.

     mvn clean install

This will build the bundle including the manifest information.

Deploying to JBoss Fuse
-----------------------

To start up Fuse browse to your fuse install directory. Then run

     /bin/fuse

This will bring up the fuse console. Once in the console you will be able to install your bundle. Usually we would install multiple bundles using a feature file, but in this case since we only have one bundle to install we can just install it using the file by the following command. Another option is to set up your local m2 repository in fuse in the fuse/etc/org.ops4j.pax.url.mvn.cfg file. Then you can use the mvn syntax below.

     karaf@root> osgi:install -s file:/home/yourUser/.m2/repository/com.redhat.consulting.fusequickstarts.karaf.websocket/websocket_route/websocket_route-1.0.0.jar
        OR
     karaf@root> osgi:install -s mvn:com.redhat.consulting.fusequickstarts.karaf.websocket/websocket_route/1.0.0

 The -s here indicates to also start the bundle.  Alternatively you can omit the -s and after the install run

     karaf@root> osgi:start <bundleId>

Results
-----------------------
After running the above commands and installing the `osgi_consumer` bundle you should see your services started:

    [ 286] [Active     ] [            ] [       ] [   50] camel-websocket (2.15.1.redhat-621084)
    [ 287] [Active     ] [Created     ] [       ] [   80] Fuse Quickstart :: Karaf :: Blueprint :: Websocket :: Route (6.2.1)


Testing
---------------------

Start the web based chat application by launching a web browser and navigating to [http://localhost:9090](http://localhost:9090).

Enter a username and click **Join** to start the chat session. Enter some text and click **Send** to produce a message that will be consumed by Fuse and sent to all parties currently connected to the chat.

Open a second browser window to simulate multiple users. 

The Fuse log will display a result similar to the following output:

    2016-02-11 21:50:54,268 | INFO  | qtp774858011-119 | websocketChat                    | 198 - org.apache.camel.camel-core - 2.15.1.redhat-621084 | >> Message received : joe:has joined!
    2016-02-11 21:51:33,598 | INFO  | qtp774858011-119 | websocketChat                    | 198 - org.apache.camel.camel-core - 2.15.1.redhat-621084 | >> Message received : mary:has joined!
    2016-02-11 21:51:42,434 | INFO  | qtp774858011-120 | websocketChat                    | 198 - org.apache.camel.camel-core - 2.15.1.redhat-621084 | >> Message received : joe:hi mary
    2016-02-11 21:51:52,406 | INFO  | qtp774858011-117 | websocketChat                    | 198 - org.apache.camel.camel-core - 2.15.1.redhat-621084 | >> Message received : mary:hi joe, how are you?
    2016-02-11 21:52:01,837 | INFO  | qtp774858011-118 | websocketChat                    | 198 - org.apache.camel.camel-core - 2.15.1.redhat-621084 | >> Message received : joe:doing fine, thanks for asking
