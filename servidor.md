# Configuración del servidor DHCP

- Lo primero que debemos hacer es encender la máquina y descargarnos el paquete **isc-dhcp-server**.

          ![Isc-dhcp-server](img/iscserver.jpg)

- Una vez hecho, apagamos la máquina y cambiamosel adaptador de red a red interna, con el nombre de red1.

![Red servidor](img/redservidor.jpg)

- Entramos en el archivo de configuración de las interfaces de red con el comando **sudo nano /etc/network/interfaces**, cambiamos al red a estática y le añadimos una ip.

![Estática server](img/Imagen13.jpg)

- Hacemos **systemctl restart networking** y luego **ip a** para comprobar que se ha asignado correctamente.

![Ip a server](img/Imagen14.jpg)

## Después de configurar RELAY

- Para comprobar que hay conectividad entre el servidor DHCP y el cliente hacemos ping al cliente.

![Ping servidor](img/pingservidor.jpg)

Podemos ver que sí hay conectividad.

- Una vez haya conectividad configuramos el archivo **/etc/default/isc-dhcp-server**, para
configurar la tarjeta que va a escuchar las peticiones del cliente.

![peticion](img/interfazdhcp.jpg)

- Entramos en el archivo **/etc/dhcp/dhcpd.conf** y le asignamos un rango de ips al cliente, para cuando el cliente le vaya a pedir una ip al servidor DHCP esté dentro de este rango.

![rango](img/Imagen23.jpg)

- Reiniciamos el servicio con **systemctl restart isc-dhcp-server**

- Ahora debemos volver a la máquina de cliente y en su archivo de configuración de interfaces ponemos la red en dhcp. Hecho esto, el cliente debe hacer **dhclient -r** para borrar la ip y **dhcliente -v** para pedirle ip al servidor.

![dhclient](img/Imagen27.jpg)

- Usamos ahora en el servidor DHCP **tail -v /var/lib/dhcp/dhcpd.leases** para ver el proceso de como le concede la ip.

![rango](img/Imagen28.jpg)
