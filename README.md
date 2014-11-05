##NOTES##
- Change the permission of the HOST path to persist generated files created by jenkins, basically allow JENKINS_HOME environment variable to write to the host volume.
```
$ chmod 777 /host/path
```
so we can do the following,
```
(fig.yml)
   ...
   volumes:
    - /host/path:/var/jenkins_home
   ...
```

- Created the Dockerfile in case we wanted to change the way Jenkins is configured.