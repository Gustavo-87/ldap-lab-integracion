# Actividad Independiente LDAP

## 1. Explicación de LDAP

LDAP (Lightweight Directory Access Protocol) es un protocolo que permite gestionar de forma centralizada usuarios, grupos y recursos en una red. Se organiza de forma jerárquica (como un árbol), lo que permite que múltiples sistemas consulten una única fuente de datos para autenticación y control de acceso.

En este laboratorio, LDAP se utilizó para autenticar usuarios en Linux, evitando el uso de cuentas locales y permitiendo una administración centralizada.

---

## 2. Arquitectura Creada

Para este ejercicio se configuró un servidor OpenLDAP con el dominio:

`dc=empresa,dc=com`

Estructura implementada:

- **Unidad Organizativa (OU) IT:** Contiene usuarios de desarrollo.
- **Unidad Organizativa (OU) HR:** Contiene usuarios de soporte.
- **Unidad Organizativa (OU) Finanzas:** Nuevo departamento creado.

- **Grupo developers (posixGroup):** Para usuarios de IT.
- **Grupo support (posixGroup):** Para usuarios de HR y Finanzas.

- **Usuarios creados:**
  - dev1
  - dev2
  - sup1
  - fin1

---

## 3. Estructura LDAP

```text
dc=empresa,dc=com
├── ou=IT
│   ├── uid=dev1
│   ├── uid=dev2
│   └── cn=developers
├── ou=HR
│   ├── uid=sup1
│   └── cn=support
└── ou=Finanzas
    └── uid=fin1
## 4. Comandos utilizados

sudo apt update
sudo apt install slapd ldap-utils -y
sudo dpkg-reconfigure slapd

##Estructura

ldapadd -x -D cn=admin,dc=empresa,dc=com -W -f estructura.ldif
ldapadd -x -D cn=admin,dc=empresa,dc=com -W -f grupos.ldif
ldapadd -x -D cn=admin,dc=empresa,dc=com -W -f usuarios.ldif

##Modificaciones

ldapmodify -x -D cn=admin,dc=empresa,dc=com -W -f add_dev2.ldif
ldapmodify -x -D cn=admin,dc=empresa,dc=com -W -f add_sup1.ldif

##Integracion con linux

sudo apt install libnss-ldapd libpam-ldapd nslcd nscd ldap-utils -y
sudo systemctl restart nslcd
sudo systemctl restart nscd

##Validacion 

ldapsearch -x -b dc=empresa,dc=com
getent passwd dev1
getent passwd dev2
getent passwd sup1
getent passwd fin1
getent group developers
getent group support
su - dev1
su - dev2
su - sup1
su - fin1

## 5. Estructura (OU, usuarios y grupos)
OU creadas
IT
HR
Finanzas
Grupos creados
developers → gidNumber: 5000
support → gidNumber: 5002
Usuarios creados
dev1 → ou=IT
dev2 → ou=IT
sup1 → ou=HR
fin1 → ou=Finanzas 
