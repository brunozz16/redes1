# redes1
Práctica - ARP 	
Saber cargar IPs a cada computadora entrando en desktop -> IPconfig 	
Ver las MAC address de cada PC en config -> nombre del puerto (FA0 ej) 	
Ver la MAC de un switch -> Entrar a la pestaña cli y (#)show version
Comando PING ip que se hace desde la terminal de una PC
mostrar tabla arp, pararse en el CLI del switch-> Switch# show arp
Práctica - STP (spanning tree protocol)	 
Para ver si es root bridge el switch (si root ID == bridge ID es root bridge) 	
(#) show spanning-tree [comando 1] 

Cambiar root bridge, para esto se usa el siguiente comando subiendo la prioridad (con números más altos) de cada switch y poniendo la del que queremos que sea root bridge en 4096 
(#config) spanning-tree vlan 1 priority 4096 [comando 2] 	

Activar RSTP: es necesario activarlo para cada switch de la topología y se hace:
(#config) spanning-tree mode rapid-pvst [comando 3]
posteriormente se verifica con el (#) show spanning-tree.
Desactivar RSTP: 
(#config) spanning-tree mode pvst [comando 4]

Guardar la configuración del switch:
(#)copy running-config startup-config [comando 5]

Práctica - VLAN 
Configurar en un switch el protocolo VTP en modo SERVER con dominio y contraseña 	los demás switch van en modo cliente con misma contraseña y dominio 	
(#config) vtp domain “nombredominio” 
(#config) vtp password contraseña 
(#config) vtp mode server #para el que es servidor 
Para los otros switches: 	
(#config) vtp domain “nombredominio” 
(#config) vtp mode client 
(#config) vtp password “contraseña” 
Ahora se deben configurar las VLANs en el switch SERVER 		
Para ello se agregan en el switch en VLAN database con nombre y número, luego se asocia cada puerto (dispositivo) a la que queramos en modo ACCESS. 
Luego hay que poner las conexiones entre switch en modo TRUNK para que por ahí pasen las VLANs. 
Para comprobar el funcionamiento, se deberían ver las VLANs en todos los switches. 	
Finalmente, comprobar que las VLANs funcionan tratando de enviar mensajes entre PCs de misma VLAN y viendo que anda y entre distintas VLAN no anda. 
(#config) vtp mode transparent 
Se lo podes poner a un switch y lo que hace es que no transfiere las vlans a los demás switches pero si estableces las vlans a pata en el switch permite la comunicación entre equipos conectados de las vlans

Práctica - VTP-LACP-PAGP
1_VTP
-configurar IPs de las pcs
-configurar los switches vtp según corresponda
(#config) vtp domain “nombredominio” 
(#config) vtp password contraseña 
(#config) vtp mode server/transparent/client  #para el que es servidor 
-Establecer Vlans

2-LACP 
Prestar atencion al modelo del switch 
Switch(config)#interface range fa0/1-3  //Permite Configurar, a un rango de interfaces
Switch(config-if-range)#channel-protocol lacp  //Se configura, en el rango de puertos, el protocolo lacp. Se debe hacer, en ambos conmutadores
Switch(config-if-range)#channel-group 1 mode (active/passive) //Se configura, en el rango de puertos, el grupo 1, que puede variar entre 1 y 6 y en modo active. Se debe configurar en ambos switches, lo que cambia en el otro que debe ser en modo passive

Switch#showetherchannel summary
Switch#showetherchannel port-channel

3-PGAP  
Prestar atencion al modelo del switch (mismo que el anterior)
Switch(config)#interface range fa0/1-3  //Permite Configurar, a un rango de interfaces
Switch(config-if-range)#channel-protocol pagp //Se configura, en el rango de puertos, el protocolo lacp. Se debe hacer, en ambos conmutadores
Switch(config-if-range)#channel-group 1 mode (auto/desirable) //Se configura, en el rango de puertos, el grupo 1, que puede variar entre 1 y 6 y en modo auto. Se debe configurar en ambos switches, lo que cambia en el otro que debe ser en modo desirable

Switch#showetherchannel summary
Switch#showetherchannel port-channel

4- WireLess
En las pcs en la parte física hay que ponerle la placa de red wireless(apagar pc y sacar la otra placa)
configurar pcs
seguir los pasos de configuración de la guia 14



COMANDOS ADICIONALES:
Ver la Mac de la VLAN:  show interface vlan 1
VER: copy running-config startup-config
Mac address: (#)show version

