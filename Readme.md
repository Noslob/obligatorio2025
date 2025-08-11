Funcionamiento de los siguientes comandos para el correcto funcionamiento de los playbooks.

Funcionamiento para los comandos ansible: 

1)	ansible-inventory -i inventarios/host.ini –-list 

Es importante la aplicación de la herramienta de Ansible que muestra y valida la información del inventario, dicha herramienta te permite ver qué hosts y grupos tiene registrados el inventario y si está bien escrito para su correcta ejecución. La opción -i indica la fuente del inventario que Ansible debe de usar que en este caso es inventarios/host.ini. 
Por último, la opción –list muestra todo el inventario en formato JSON, específicamente indica todos los grupos definidos, los hosts que pertenecen a cada grupo y las variables asociadas a cada host o grupo. 

2)	ansible -i inventarios/host.ini all -m ping

El siguiente comando es un ad-hoc de Ansible para probar la conectividad de todos los hosts especificados en el archivo host.ini, el patrón all indica que a punta a todos los hosts del inventario.  Se comprueba realmente si los hosts del inventario se resuelven, es decir, la IP y los hostname correctos, que la conexión SSH en Linux es posible y que las credenciales usuario/contraseña funcionen.



Funcionamiento de los comandos Playbook nfs_setup.yaml:

En un principio para el correcto funcionamiento del Playbook nfs_setup_yaml se deberá de instalar el ansible-core con el siguiente comando: sudo dnf install -y ansible-core y ansible-galaxy collection install -r requirements.yaml

Para el funcionamiento del playbook se deberá de seguir ciertos pasos previos para llegar a su ejecución. Se deberá modificar el archivo host.ini ubicado en ./obligatorio2025/inventarios/host.ini usando Vim o  nano.
Dentro del inventario ../inventarios/host.ini se modificará las ip de los host Ubuntu y Centos. 

Para ejecutar el playbook de NFS, se deberá de verificar las colecciones disponibles con ansible-galaxy collection list e instala las necesarias: ansible.posix

Posteriormente se deberá de ejecutar el siguiente comando:

1)	ansible-playbook -i inventarios/host.ini playbooks/nfs_setup.yaml -K -k

El siguiente comando ejecuta un playbook de Ansible para configurar NFS, usando la carga del inventario específico indicado en /inventario/host.ini  y pidiendo contraseñas de SSH y de sudo. 
El playbook a ejecutar las tareas de NFS esta indicado en el archivo nfs_setup.yaml, por último, los parámetros -k (--ask-pass) se pide la contraseña de SSH para conectarse a los archivos hosts y -K (--ask-become-pass) se pide la contraseña de sudo para elevar privilegios cuando las tareas lo requieran. 



Funcionamiento de los comandos Playbook hardening.yml:

En un principio para el correcto funcionamiento de hardening.yml se deberá realizar un update al sistema y correr el siguiente comando: sudo apt update && sudo apt install -y ansible-core, finalmente se deberá de verificar la versión con el comando ansible --version.

Posteriormente para el funcionamiento del playbook hardening.yml, se deberá de verificar las colecciones disponibles con community.general. Lo más recomendable es gestionarlas mediante un archivo requirements.yaml y ejecutar ansible-galaxy collection install -r requirements.yaml.

Posteriormente se deberá de ejecutar el siguiente comando: 

2) Comando: ansible-playbook -i inventarios/host.ini playbooks/hardening.yaml -K -k


El siguiente comando ejecutará el playbook hardening.yaml sobre los hosts definidios en inventarios/host.ini solicitando la contraseña SSH con -k y la contraseña de sudo con el parámetro -K.
En el host Ubuntu01 se actualizó el sistema, se recogieron los facts del sistema en Gathering Facts, chequeo si estaba instalado ufw, se verifico si se permitió conexiones SSH, se bloqueo el tráfico entrante, no se permitó login ssh con root, se instaló fail2ban y se configuró correctamente.


