# Documentación 2DetalleAlarmas

## Descripción
Este proyecto permite la consulta, procesamiento y almacenamiento de datos de grabaciones de video obtenidas a través de una API externa. Utiliza `requests` para realizar peticiones HTTP, `pandas` para manipular los datos y `SQLAlchemy` para almacenar la información en una base de datos MySQL.

## Requisitos

### Dependencias
Antes de ejecutar el script, asegúrese de instalar las siguientes bibliotecas de Python:

```bash
pip install requests pandas sqlalchemy mysql-connector-python
```

### Configuración de la Base de Datos
El script se conecta a una base de datos MySQL. Es necesario configurar correctamente las credenciales de acceso:

- Usuario: `saocomct_camaras`
- Contraseña: `1t&F)DQG6BLq`
- Host: `190.90.160.5`
- Puerto: `3306`
- Base de datos: `saocomct_camaras`

## Estructura de Archivos

El proyecto se compone de los siguientes archivos:

```
/
├─ 2DetalleAlarmas.py           # Script de alarmas   
├─ README.md                    # Archivo de documentación

```

## 2DetalleAlarmas.py
    1. Diccionario de Alarmas

    El script define un diccionario data_alarmas con los códigos de las alarmas junto con su descripción en inglés y en español. Luego, este diccionario se convierte en un DataFrame de pandas (df_alarmas).

    2. Conexión a la Base de Datos

    Se crea un motor de conexión a MySQL utilizando sqlalchemy. El script obtiene la última fecha de una alarma registrada en la tabla detalle_alarmas.

    3. Generación de Fechas de Consulta

    El script extrae la fecha de la última alarma registrada y genera el intervalo de tiempo para la nueva consulta de alarmas.

    4. Obtención de la API Key

    Se realiza una solicitud HTTP a la API externa para obtener una clave de acceso (key) utilizando un usuario y contraseña.

    5. Obtención de Dispositivos

    Se consulta la API para obtener la lista de dispositivos y se extraen datos relevantes como terid y numero_unidad.

    6. Obtención de Alarmas Detalladas

    El script consulta la API para obtener las alarmas generadas entre la última fecha registrada y la fecha actual. Los datos se almacenan en df_detail_alarmas.

    7. Procesamiento y Almacenamiento en MySQL

    Los datos de las alarmas se enriquecen con información adicional y se almacenan en la base de datos MySQL en la tabla detalle_alarmas.

## Uso del Script 2: Obtención de Datos de Grabación

### 1. Consulta de Grabaciones por Fecha
Se obtienen los datos de grabaciones para cada dispositivo en función de los últimos 6 meses.

Ejemplo:
```python
for fecha in primer_dia_meses:
    url8_1 = 'http://181.143.106.68:12056/api/v1/basic/record/calendar?key=' + key + '&terid=' + terid + '&starttime=' + starttime + '&st=1'
    response8_1 = requests.get(url8_1)
```

### 2. Consulta de Horas de Grabación
Se obtiene la cantidad de horas de grabación para cada dispositivo por día.

Ejemplo:
```python
url8_2 = 'http://181.143.106.68:12056/api/v1/basic/record/filelist?key=' + key + '&terid=' + terid + '&starttime=' + starttime + '&endtime=' + endtime + '&chl=' + chl + '&st=' + st 
response8_2 = requests.get(url8_2)
```

---



