# Información

Registro imagenes de docker para un ambiente local (onPremise)

# Pasos para la configuración

## 1. Habilitar la IP como unidad certificadora
1. Editar el archivo openssl.conf: 
```sh
nano /etc/ssl/openssl.cnf
```

2. Agregar la IP del servidor como unidad certificadora (PA) en la sección "[v3_ca]":  
```sh
subjectAltName=IP: [IP del servidor]
```

## 2. Crear el certificado.
1. Crear la carpeta certs y acceder
```sh
mkdir certs
cd certs
```

2. crear el certificado con nombre domain dentro de la carpeta certs
```sh
openssl req -newkey rsa:4096 -nodes -sha256 -keyout domain.key -x509 -days 365 -out domain.crt
```

3. Importante: asignar la IP de la computadora en el campo "Common Name"

## 3. Validarnos como unidad certificadora para el motor de Docker

1. Agregar el equipo cliente como válido para la unidad certificadora.
```sh
mkdir -p /etc/docker/certs.d/[IP de la computadora:5000]
cp /certificates/domain.crt /etc/docker/certs.d/[IP de la computadora:5000]/ca.crt
```

2. Reinicar el servicio de docker
```sh
service docker reload
```

## 4. Configurar el almacenamiento de volumenes

1. Crear carpeta para almacenar las imagenes
```sh
mkdir volume
```

2. Crear la carpeta para almacenar los usuarios y claves cifrados.
```sh
mkdir auth
```


# Pasos para la ejecución y pruebas.
