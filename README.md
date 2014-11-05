##NOTES##
- Change the permission of the HOST path so JENKINS_HOME so the docker-jenkins can write to the host volume.
```
chmod 777 /host/path
```

- Created the Dockerfile in case we wanted to change up the way Jenkins is configured