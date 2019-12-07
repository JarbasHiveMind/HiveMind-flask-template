# Mycroft WebUI
A very simple WebUI for interacting with your Mycroft instance.

## Configuration
This project needs the following configuration:

### Environment variables
`MYCROFT_HOST`: Set to the IP address or hostname of your Mycroft instance. Please ensure port 8181 is ONLY accessible to this container.
`ADMIN_USERNAME`: The username for the authentication dialog
`ADMIN_PASSWORD`: The password for the authentication dialog

If you wish, you could instead provide your own .htpasswd file. See Files below.

### Files
No files are necessary, but this container exposes a /config directory which supports the following files:
`nginx.crt`: SSL certificate
`nginx.key`: SSL key
`.htpasswd`: [Authentication file](https://docs.nginx.com/nginx/admin-guide/security-controls/configuring-http-basic-authentication/#creating-a-password-file)

If nginx.crt and nginx.key exist, the container will automatically start using SSL.

If .htpasswd exists, it will be used instead of the ADMIN_USERNAME and ADMIN_PASSWORD environment variables.

## Build image
Git pull this repository.

```bash
git clone https://github.com/TheLastProject/mycroft-webui.git
```

Build the docker image in the directory that you have checked out.

```bash
docker build -t mycroft-webui .
```

## Run

```bash
docker run -d \
-e MYCROFT_HOST=127.0.0.1 \
-v /your/config/directory/location:/config \
-p 8080:8080 \
-p 8443:8443 \
--name mycroft-webui mycroft-webui
```
