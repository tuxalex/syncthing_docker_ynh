syncthing_docker_ynh
Installation information

This package installs Syncthing in a container with docker and use redirection in nginx to add the app in yunohost SSO. The install script install docker if yunohost have installed on the host. Docker-py has been used as a docker client to interact with docker thus this package can be used on a host with yunohost installed (not tested yet) or on a yunohost docker container. The first installation can take time, because docker download the base image and construct the ajenti image, so be patient. In yunohost this app will be installed with the name "syncthing_docker" Syncthing doesn't support multi-user so this app is multi-instance, each user must have an install of this app to access to it. The first instance installed will be called "syncthing_docker", after "__NUMBEROFINSTANCE" will be added to "syncthing_docker" (Example: the secondary instance will be called "btsync_docker__2") The package creates for each install a container with a name composed of "syncthing" and the username concatened like syncthing_USERNAME.
Credit

This work is based on Scith work : https://github.com/scith/redirect_ynh
TODO

    Multi-instance
    Upgrade script
    Backup script
    Restore script
    supervisor
    loop in build_container.py to auto add all port
    script to auto generate ynh package (auto add and )

