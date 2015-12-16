# docker-keycloak-import-realm
Keycloak standalone server which will import a realm at startup, if it is not yet imported. An admin user `admin` with password `password` is available.

```
/!\ This build should always be extended and should not run directly in a container as there is no realm to import (Keycloak server will fail!).
```
In order to extend it, create a directory with following files:
* `import-realm.json` : the contents can be exported from a running Keycloak server where the realm was defined, see [Keycloak documentation](https://keycloak.github.io/docs/userguide/keycloak-server/html/export-import.html)
* `Dockerfile` with following contents:
```
FROM dfranssen/keycloak-import-realm
ADD import-realm.json /opt/jboss/keycloak/
```

If you would like to reuse this Dockerfile and rebuild it, the following Docker *build-arg* can be used:
* `KEYCLOAK_ADMIN_USER`: username that will be added as an admin user. Default is **admin**
* `KEYCLOAK_ADMIN_PASWORD`: password that will be used for the admin user. Default is **password**
* `KEYCLOAK_IMPORT_REALM`: custom json file that contains the realm info and that will be added to the build. Default is **import-realm.json** and this file should exist next to the Dockerfile.
