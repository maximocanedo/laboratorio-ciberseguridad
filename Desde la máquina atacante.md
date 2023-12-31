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

Pruebas 19/07/2023 12:00
	Direcciones IP
		`Metasploitable: 192.168.56.101`
		`Máquina atacante: 192.168.56.103`
	Visibilidad
		`Metasploitable es vista: SÍ`
		`Máquina atacante es vista: SÍ`
	Escaneo de puertos y servicios
		Resultado del escaneo
			Se encuentra en el archivo `~/Proyects/Escaneo/scan.md`
		Exploits encontrados
			`OpenSSH < 6.6 SFTP (x64) - Command Execution`
				`Path: linux_x86-64/remote/45000.c`
				`Puerto 22/TCP open`
				`Servicio: SSH`
				Explotación de vulnerabilidad.
					Intento 1.  #failed
						Se intentó compilar el archivo `45000.c` y ejecutarlo con el comando:
						`./exploit <Dirección IP Metasploitable> msfadmin 'ls -la'`
						Pero da error de conexión a host. Se intentará luego.
			`Apache - Arbitrary Long HTTP Headers Denial of Service`
				`Path: linux/dos/371.c`
				`Puerto: 80/TCP open`
				`Servicio: http`
				Explotación de vulnerabilidad.
					Intento 1. #failed
						Se intentó compilar el exploit y ejecutarlo con la IP de metasploitable, pero recibimos el error: `zsh: segmentation fault ./exploit 192.168.56.101`
			`Postfix SMTP 4.2.x < 4.2.48 - 'Shellshock' Remote Command Injection`
				`Path: linux/remote/34896.py`
				`Puerto: 25/TCP`
				`Servicio: SMTP`
				Explotación de vulnerabilidad.
					Intento 1. #in-progress
						