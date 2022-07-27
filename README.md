# OpenLDAP

To learn this tutorial, you can read the step-by-step tutorial from [my post](https://oscarchou.com/posts/howto/setup-local-ldap-server-with-tls-enabled/). (5 mins)

## Run up LDAP service

```
docker-compose up
```

## Run up LDAP service with custom TLS certificates

```
docker-compose -f docker-compose-tls.yml up
```

## Login admin panel

Open `http://localhost:8090` with the webbrowser.  

The login credential is

```
Login DN: cn=admin,dc=example,dc=org
Password: admin_pass
```

## Test with ldap client tool 

```
docker exec openldap_ldap_server_1 ldapsearch -x -H ldap://localhost:389 -b dc=example,dc=org -D "cn=admin,dc=example,dc=org" -w admin_pass
```
## Test with ldap client tool with custom TLS certificate

```
env LDAPTLS_CACERT=/path/to/cert ldapsearch -x -H ldaps://localhost:636 -b dc=example,dc=org -D "cn=admin,dc=example,dc=org" -w admin_pass
```

References:
1. [Github osixia/openldap](https://github.com/osixia/docker-openldap)
2. [Build an OpenLDAP Docker Image That’s Populated With Users](https://betterprogramming.pub/ldap-docker-image-with-populated-users-3a5b4d090aa4)
3. [ldapwiki](https://ldapwiki.com/wiki/Distinguished%20Names)
