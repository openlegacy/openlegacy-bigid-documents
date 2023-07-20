# Openlegacy BigID API
This repository will include the documentation for the Openlegacy BigID API integration 

For more information regarding the docker image, please check: https://hub.docker.com/r/openlegacy/nocode-bigid

## How to start?
Follow the guide we have created under OpenLegacy-BigID Dataset and CLI

When you want to test the image using docker-compose fill in the required properties in the docker-compose.yml and run `docker-compose up -d` this will start the API.

## How to install helm chart

`helm install <NAME> ./helm-chart/nocode-bigid --vlues <values.file> --namespace <k8s namespace>`

Values file should contain these variables:
```
envData:
  OL_HUB_API_KEY: <key>
  OL_HUB_PROJECT_NAME: <name>
  OL_CORE_LICENSE_KEY: <key>
```
for nginx ingress endpoint:

```
ingress:
  className: nginx
  enabled: true
  hosts:
  - host: < url to the service >
    paths:
    - path: /
      pathType: Prefix
```
## How to install helm chart with opz file
put .opz file to the `./helm-chart/nocode-bigid/files` folder
```
envData:
  OL_HUB_PROJECT_NAME: <name>
  OL_CORE_LICENSE_KEY: <key>
  OL_SOURCE_PROVIDER: OL_PROJECT_ZIP
  OL_PROJECT_ZIP_PATH: /data/<file.opz>
```
for nginx ingress endpoint:

```
ingress:
  className: nginx
  enabled: true
  hosts:
  - host: < url to the service >
    paths:
    - path: /
      pathType: Prefix
```
