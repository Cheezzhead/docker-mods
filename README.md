# API Gateway - Docker mod for swag

This mod adds nginx configuration files that facilitate an API gateway at the api.* subdomain. In doing so, you can lock down the default api endpoint of each service to the outside and direct all external api requests to this subdomain.

## Features
* The gateway is protected with http authentication, which should be compatible with most API services.
* Separate log file for all API requests, with the option of further dividing by API service (by uncommenting the relevant lines in each service's conf file)
* Errors are returned as JSON, with 404 (invalid paths) treated as bad requests (400)

## Limitations
* Only services proxied over subfolder are compatible (although the relevant configuration files could be included on a subdomain level with ease)

## Setup
* In swag docker arguments, set an environment variable `DOCKER_MODS=linuxserver/mods:swag-apigateway`
  * If adding multiple mods, enter them in an array separated by `|`, such as `DOCKER_MODS=linuxserver/mods:swag-apigateway|linuxserver/mods:swag-mod2`
* create an htpasswd file at `/config/etc/.htpasswd`: `docker exec -ti swag htpasswd -c /config/etc/.htpasswd $USER`. You will be prompted for the password
* Remove the `.sample` suffix from any files in `/config/nginx/api-confs` you wish to use
* Reload or restart the swag container

