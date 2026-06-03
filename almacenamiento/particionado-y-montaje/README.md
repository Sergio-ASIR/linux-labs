# Particionado y montaje de discos en Linux

## Objetivo

Configurar un disco secundario en Linux mediante una tabla de particiones MBR, creando diferentes particiones para almacenamiento y espacio de intercambio (swap), formateándolas con ext4 y configurando su montaje persistente mediante `/etc/fstab`.

---

## Entorno utilizado

* Sistema operativo: Ubuntu
* Plataforma de virtualización: VirtualBox
* Disco principal: 40 GB
* Disco secundario: 100 GB

---

## 1. Identificación del disco

Se verifica la presencia del nuevo disco utilizando `lsblk`.

![Disco detectado](./01%20-%20lsblk-disco-limpio.png)

Se identifica el disco `/dev/sdb` como dispositivo disponible para la creación de particiones.

---

## 2. Creación de la tabla de particiones MBR

Se accede al disco mediante `fdisk` y se crea una tabla de particiones DOS (MBR).

![Tabla MBR](02%20-%20Resultado%20fdisk-o%20Particion%20MBR%20creada.png)

Comprobación de la tabla creada:

![Comprobación tabla de particiones](03%20-%20Comprobación%20con%20tecla%20-p-%20de%20tabla%20de%20particiones%20creada.png)

---

## 3. Creación de particiones

### Partición primaria

Se crea una partición primaria de 30 GB.

![Partición primaria](04%20-%20Partición%20Primaria%20Creada.png)

### Partición extendida

Se crea una partición extendida para alojar particiones lógicas.

![Partición extendida](05%20-%20Particion%20Extendida%20creada.png)

### Particiones lógicas

Primera partición lógica de 30 GB:

![Partición lógica 1](06%20-%20Primera%20particion%20logica.png)

Segunda partición lógica de 20 GB:

![Partición lógica 2](07%20-%20Segunda%20particion%20logica.png)

Resultado final de las particiones creadas:

![Particiones creadas](08%20-%20Todas%20particiones%20creadas.png)

---

## 4. Configuración de la partición Swap

Se crea una partición destinada a espacio de intercambio (swap).

![Partición swap](09%20-%20Particion%20Swap%20creada.png)

Una vez finalizada la configuración se guardan los cambios realizados en la tabla de particiones.

![Guardar cambios](10%20-%20cambios%20guardados%20en%20disco.png)

---

## 5. Formateo de particiones

Las particiones destinadas a almacenamiento se formatean utilizando el sistema de archivos ext4.

![Formateo ext4](11%20-%20Formateo%20ext.4%20de%20las%20particiones%201-5-6.png)

---

## 6. Creación y activación de Swap

Creación del área de intercambio:

![Creación swap](12-%20Swap%20creado.png)

Activación y comprobación:

![Activación swap](13%20-%20Activacion%20swapon%20y%20comprobacion.png)

---

## 7. Montaje de particiones

Se crean los puntos de montaje y se asocian las particiones correspondientes.

* `/mnt/apps`
* `/mnt/datos`
* `/mnt/copias`

![Montaje](14%20-%20Montaje%20de%20los%20discos%20y%20carpetas.png)

---

## 8. Obtención de UUID

Se obtienen los identificadores UUID de cada partición mediante `blkid`.

![UUID](15%20-%20comprobacion%20con%20sudo%20blkid.png)

---

## 9. Configuración persistente mediante fstab

Se configura el archivo `/etc/fstab` para que las particiones y el área swap se monten automáticamente tras cada reinicio.

![fstab](16%20-%20comprobacion%20con%20cat%20de%20fstab.png)

---

## 10. Verificación final

Comprobación final del estado de las particiones montadas y del área swap.

![Verificación final](16%20-%20Comprobacion%20final%20de%20discos.png)

---

## Resultado

Configuración completa de un disco secundario de 100 GB mediante:

* Tabla de particiones MBR.
* Partición primaria.
* Partición extendida.
* Particiones lógicas.
* Sistema de archivos ext4.
* Espacio de intercambio swap.
* Montaje manual.
* Montaje persistente mediante UUID y `/etc/fstab`.

---

## Conclusiones

Este laboratorio permite comprender el proceso completo de preparación de un disco para su uso en Linux, incluyendo particionado, formateo, configuración de swap, montaje de sistemas de archivos y persistencia de la configuración tras reinicios del sistema.

