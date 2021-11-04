# Docker-compose-final

## Explicación del docker-compose
### El docker compose es un archivo que al ejecutarlo nos crea los docker, les asigna un volumen entre otros elementos.

## docker-compose estructura:
### version: "3.3" --> versión que vamos a usar para crear los dockers
### services: --> aquí se dan origen a los docker(servicios)
 ### asir_bind9_2: --> nombre del primer docker
   ### image: internetsystemsconsortium/bind9:9.16 --> imagen del primer docker
   ### networks: --> esta parte le asiganmos la red propia creada con anterioridad
      ### br02: --> nombre de la red
        ### ipv4_address: 10.1.0.254 --> aqui le asignamos un ipfija de la red a nuestro docker DNS
   ### ports: --> puertos que le asignamos
     ### - 53:53 
   ### volumes: --> volume empleado, elcual fue creado con anterioridad.
     ### - confdnsubuntu:/etc/bind 
 ### asir_cliente_2: --> segundo docker
   ### image: iagofernandezblanco/cliente-ubuntu:netools --> imagen del docker, la cual es una imagen modificada por mi.
   ### networks: 
     ### - br02
   ### stdin_open: true  # docker run -i --> estos dos comandos nos permiten ejecutar los docker unto con una shell para poder trabajar sobre ella
   ### tty: true         # docker run -t
   ### dns: --> asignacion del servidor DNS mediante la IP fija
     ### - 10.1.0.254
### volumes: --> volumen empleado
 ### confdnsubuntu:
   ### external: true --> esto indica que el volume o elemento declarado, el cual debe ser uno ya existente, no se originará al lanzar el docker-compose
### networks:
  ### br02: 
    ### external: true  
# ----------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Una vez acabado el docker compose, debes situarte desde una terminal en la carpeta donde hayas guardado el docker compose y una vez situado en esta, ejecutamos el comando docker-compose up.

## COMANDO NECESARIO PARA CREAR UNA RED PROPIA
### docker network create --subnet 10.1.0.0/24 --gateway 10.1.0.1 br02

## docker compose up
## docker compose down
