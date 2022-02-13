# cs505-embedded-template

## Building and running package
The class VM has Java but not Maven, which is used for building the package.  

To install Maven run:  
```
sudo apt install maven -y
```

Then run ./run.sh to build and start the package.

You will see lots of output the first time you build the package, as Maven is pulling down all dependencies.  The process will build a Java Jar located in the target directory (cs505-embedded-template/target/cs505-embedded-template-1.0-SNAPSHOT.jar)

Once built you will see something like this:

```
  Starting Database...
  Database Started...
  Starting Web Server...
  Feb 19, 2021 8:46:11 AM org.glassfish.grizzly.http.server.NetworkListener start
  INFO: Started listener bound to [0.0.0.0:9000]
  Feb 19, 2021 8:46:11 AM org.glassfish.grizzly.http.server.HttpServer start
  INFO: [HttpServer] Started.
  Web Server Started..
```

Curl can be used to check that your API and database is responding:
*Note the use of a required security header
```
curl -H "X-Auth-API-Key: 12463865" http://localhost:9000/api/checkmydatabase
{"status_desc":"accesslog table exists","success":"true"}
```
---

## Creating a container to run your package

A Dockerfile is included in this repo that references the jar you built in the first step.  Run the docker build command to build your container:
```
  sudo docker build -t cs505-embedded .
```

Once a container is built it can be run in the foreground:
```
  sudo docker run -it --rm -p 9000:9000 cs505-embedded
```    
or background:
```
  sudo docker run -d --rm -p 9000:9000 cs505-embedded
```    
    
