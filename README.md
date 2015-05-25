# Dockfix
Docker fixture helpers

This package helps writing unit tests in Go that depends on services available in docker images. It will create a docker container based on a base image, and cache the id of the created container so running a test suite is kept fast.

The container id is stored in files name <base-image>.container in the working directory where this library is used.

It handles DOCKER_HOST and DOCKER_CERT_PATH environment variables as set up by boot2docker, so it works on OSX.

## Usage


```
    var postgresContainer *docker.Container

    func Setup(){
        var err error
        postgresContainer, err = dockfix.StartContainer("test-postgres", "postgres")
        if err != nil {
            log.Fatal("Failed to start postgres: ", err)
        }
        dockerURL, err := dockfix.PortURL(postgresContainer, "5432/tcp")
        //dockerURL now has a URL pointing to the standard port for postgres
    }

    func Teardown(){
        dockfix.StopContainer(postgresContainer)
    }

```


