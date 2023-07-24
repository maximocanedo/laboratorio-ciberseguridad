Actualizar cosas
	`sudo apt update`
	`sudo apt upgrade`
Redes
	`ifconfig` | `ip address` para conocer la dirección IP

Pasos a seguir
	**Paso 1.** Comprobar la conexión
		*Ambas máquinas deben estar en el mismo rango de direcciones IP.*
		`ping <Dirección IP de Metasploitable>`
		`ping -cn`, donde `n` es el número de paquetes que se recibirá.
	**Paso 2.** Enumerar los servicios de Metasploitable
		Instalar nmap en caso de no tenerlo
			`sudo apt install nmap` para realizar la instalación.
		Escanear todo el stack de puertos y sus servicios
			`sudo nmap -sS -p- -sV -O -T5 <Dirección IP de Metasploitable> -vv`: 
				Enumera TCP/SYN (Requiere root), todos los puertos, determina detalles de servicios abiertos, fingerprint del sistema operativo, y a máxima potencia (Puede generar daños en la vida real y con sistemas reales).
	**Paso 3.** Buscar vulnerabilidades.
		Instalar la base de datos de exploits buscable, `exploitdb`
			Instalar usando: `sudo apt install exploitdb`
			Comando nuevo: `searchsploit (-h)`
		Buscar exploits con el *Banner gravy* : `searchsploit <query>`
		Obtener más información sobre el exploit.
			Creamos una carpeta nueva para descargar los datos
				`pwd` para saber en qué directorio estoy.
				`mkdir <name-of-new-folder>`
				`cd <name-of-new-folder>`
				Como lo organiza el profe:
					Carpeta `Proyects/`
					Carpeta `Proyects/exploits/`
					Carpeta `Proyects/exploits/<PORT_NUMBER>_<PROTOCOL>/`
			Descargamos los datos del exploit:
				`searchsploit -m <path-de-la-tabla>` para copiar un mirror.
			Leer, comprender qué hace el exploit:
				`cat <exploit-file>` para ver el contenido del archivo.
				`batcat (?)` un cat más user-friendly.
			