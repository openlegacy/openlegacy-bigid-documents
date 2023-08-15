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

## List of Supported Environment Variables:

OL HUB Params:

| Name | Type | Default Value | Description | Required |
| ------------- |:-------------:| :-------------:| :-------------:| :-------------:|
| OL_HUB_API_KEY     | String     | | OpenLegacy Hub API Key | true|
| OL_HUB_PROJECT_NAME     | String    | |OpenLegacyHub Project Name| true|
| OL_CORE_LICENSE_KEY     | String     | |OpenLegacyHub License String | true|
| OL_SOURCE_PROVIDER     | String     | HUB|  In case of OPZ use OL_PROJECT_ZIP  | false|
| OL_HUB_URL     | String    |  https://api.ol-hub.com| Public URL of the deployed Hub Instance| false|
| OL_PROJECT_ZIP_PATH     | String    |  | <PATH_TO_OPZ_FILE> inside the container| true ONLY when using OPZ|

---
Global FTP Params

| Name | Type | Default Value | Description | Required |
| ------------- |:-------------:| :-------------:| :-------------:| :-------------:|
| OVERRIDE     | Boolean  | | Use to override connections params with the ones below  | false|
| GLOBAL_USER     | String     | | FTP user| false
| GLOBAL_PASSWORD     | String     | |FTP Password| false|
| SSL_ENABLE     | Boolean     | false | Enable Secure FTP| false|
| SSL_PROTOCOL     | String    | TLS | Set the TLS protocol| false|
| SSL_IMPLICIT     | Boolean    | false | Enable Implicit FTP| false|
| JOB_CARD     | String     | OL5TEST1  JOB  A123,'CICS COBOL',CLASS=A,MSGCLASS=H,NOTIFY=&SYSUID | The JCL Job Card to submit| false|
| VAR0     | String     | ''| | false|
| FILE_NAME     | String     |OUT1| | false|
| HLQ     | String     | BATCON| | false|
| CUSTID     | String     |CN8HD631 | | false|
| VERSION     | String     | V0000001 | | false|
| INC     | String     | &HLQ..&VERSION..INCLUDES || false|
| FILE_PARAM     | String     | &HLQ..&VERSION..INCLUDES | | false|

---
Functional Params

| Name | Type | Default Value | Description | Required |
| ------------- |:-------------:| :-------------:| :-------------:| :-------------:|
| DEBUG_LEVEL     | String    | info | Sets the OpenLegacy Connector Log Level| false|
| RANDOM_ID     | Boolean  | false | Use UUID for each record in the BigID scanner  | false|
| RECORD_ID_START_POS     | Int     | 0 | Default Records ID start position(in cases we don't use UUID)| false
| RECORD_ID_LENGTH     | Int     | 16 |Default Records ID length(in cases we don't use UUID)| false|
| WITH_METADATA     | Boolean     | true | Return additional records metadata in the BigID Structured Scan (VSAM connector)| false|
| METADATA_ONLY     | Boolean    | false | Return ONLY records metadata  in the BigID Structured Scan (VSAM connector)| false|
| RECORD_READ_OFFSET     | Int    | 0 | First Record position in the VSAM file (used in the unstructured generic API)| false|
| RECORD_READ_LIMIT     | Int    | 50000 | The number of records to scan in the VSAM file (used in the unstructured generic API)| false|


      
