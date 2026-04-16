# Configuración de LDAP y OpenLDAP en WSL

## 1. Objetivo

Configurar un servidor OpenLDAP en Ubuntu sobre WSL para gestionar usuarios y grupos de forma centralizada y permitir autenticación de usuarios Linux mediante LDAP.

## 2. ¿Qué es LDAP?

LDAP (Lightweight Directory Access Protocol) es un protocolo para gestionar identidades de forma centralizada, como usuarios, grupos, permisos y recursos dentro de una organización.

Su ventaja principal es que evita crear usuarios localmente en cada servidor, permitiendo administrar credenciales desde un único punto.

## 3. Arquitectura implementada

Dominio configurado:

`dc=empresa,dc=com`

Estructura organizacional:

```text
dc=empresa,dc=com
├── ou=IT
│   ├── uid=dev1
│   ├── uid=dev2
│   └── cn=developers
└── ou=HR
    ├── uid=sup1
    └── cn=support
