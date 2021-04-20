# Información

Registro imagenes de docker para un ambiente local (onPremise)

# Pasos para la configuración

## 1. Habilitar la IP como unidad certificadora
1. Editar el archivo openssl.conf: nano /etc/ssl/openssl.cnf
2. Agregar la IP del servidor como unidad certificadora (PA) en la sección "[v3_ca]":  subjectAltName=IP: [IP del servidor]


## 2. Crear el certificado.
1. crear el certificado : openssl req \
  -newkey rsa:4096 -nodes -sha256 -keyout domain.key \
  -x509 -days 365 -out domain.crt


