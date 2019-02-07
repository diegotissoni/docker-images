# almundo/java
Java base image for self contained web apps with multiple env configurations.

## Supported tags and respective ```Dockerfile``` links
 * ```11-1.0.1``` [11-1.0.1/Dockerfile](https://github.com/almundocom/docker-images/tree/master/almundo/java/11-1.0.1)
 * ```10-1.0.1``` [10-1.0.1/Dockerfile](https://github.com/almundocom/docker-images/tree/master/almundo/java/10-1.0.1)
 * ```9-1.0.1``` [9-1.0.1/Dockerfile](https://github.com/almundocom/docker-images/tree/master/almundo/java/9-1.0.1)
 * ```8-1.1.1```, ```latest```  [8-1.1.1/Dockerfile](https://github.com/almundocom/docker-images/tree/master/almundo/java/8-1.1.1)
 * ```8-1.0.1-lw``` [8-1.0.0-lw/Dockerfile](https://github.com/almundocom/docker-images/tree/master/almundo/java/8-1.0.1-lw)


### Features
 - Lightweight base image for self contained java web apps (in *-lw versions)
 - Multi environment support
 - NewRelic support
 - Tunning JVM by environment
 - Enable JMX by environment
 - Enable debugging by environment


## Project structure
```
.
+-- pom.xml
+-- src
|   +-- ...
+-- conf
|   +-- common
|   |   +-- fooCommon.properties
|   +-- development
|   |   +-- logback.xml
|   |   +-- deploy-propeties.json
|   +-- staging
|   |   +-- logback.xml
|   |   +-- deploy-propeties.json
|   +-- production
|   |   +-- logback.xml
|   |   +-- deploy-propeties.json
|   +-- newrelic
|   |   +-- newrelic.yml
```

&nbsp;
### Put the deploy-properties.json file in each env directory

```json

{
	"jvmArguments":"-Xms1024m -Xmx1024m",
	"debugEnabled": false,
	"jmxEnabled": true,
	"newRelicEnabled": true,
	"mainClass": "com.foo.App"
}

```
&nbsp;
### Used ports
 - 8080 for webApp
 - 9010 for debugging or jmx connections

&nbsp;
# Use the base image

```docker
FROM almundo/java:8-1.0.0

# Uncomment if you use newrelic
#COPY target/newrelic/newrelic.jar application/newrelic/newrelic.jar

COPY conf application/
COPY target/fooApp-fooVersion.jar application/fooApp-fooVersion.jar

```
&nbsp;
```dockerfile
docker build -t fooApp:fooVersion .
```

&nbsp;
# Run a container

 ```bash
 $ docker run -e ENV=development -e HOST_IP=fooIp -v /application --name fooApp -P  fooApp
 ```

&nbsp;
### Changing a reloadable configuration using [freplace image](https://hub.docker.com/r/almundo/freplace/)

```bash
$ docker run --volumes-from fooApp almundo/freplace application/development https://foo.com/logback.xml
```
