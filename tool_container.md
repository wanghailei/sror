# Container

MRSK uses the dynamic reverse-proxy Traefik to hold requests, while the new app container is started and the old one is stopped — working seamlessly across multiple hosts, using SSHKit to execute commands. Originally built for Rails apps, MRSK will work with any type of web app that can be containerized with Docker.
