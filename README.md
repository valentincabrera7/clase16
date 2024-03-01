# GIT-HUB 
# Afterclass 2da pre-entrega

# Crear un programa que permita el modelamiento de clientes en una pagina de compras
# Crear un paquete que contenga dos modulos
# El primero debe tener la clase Clientes 
# El segundo crear la instancia Clientes
# Formato zip

# desde inicio utilizar el paquete entero


import json
import pathlib # asi se puede tambien

# siempre en el archivo que python va a llamar usamos importaciones absolutas
# las importaciones relativas las usamos dentro de paquete, utilizando el punto .

# main() ya tiene acceso a esta variable global
BASE_DIR = pathlib.Path(__file__).resolve().parent
RUTA_BASE_DATOS = BASE_DIR / "base_de_datos.json"
base_datos = [] # una vez que entran los datos se guardan en esta lista vacia que contiene dict

def entrar_datos(): # aca va a interactuar con el usuario  ##1
    usuarios = {}
    usuarios["nombre"] = input("Ingrese un nombre de usuario: ").capitalize()
    usuarios["contraseña"] = input("Ingrese una contraseña: ")
    base_datos.append(usuarios) # en la base de datos de arriba agrega los datos
    guardar_datos() # llamo a guardar datos

def guardar_datos(): # usa json, me crea el archvo con lo que tenga la base de datos ##2
    # aca tambien iria un try-except
    with open(RUTA_BASE_DATOS, "w") as archivo:
        json.dump(base_datos, archivo, indent=4)

def cargar_datos(): # usa json ##3
    try:
        with open(RUTA_BASE_DATOS, "r") as archivo:
            base_datos = json.load(archivo)
    except Exception as e: # para atrapar excepciones que no conozcamos
        print("Error:", type(e)) # para ver el tipo de error 
        pass # si no existe nada, que lo pase y muestre los datos 

def mostrar_datos(): ##4
    print(base_datos)

def main(): # main se dedica a llamar funciones
    cargar_datos()
    entrar_datos()
    mostrar_datos()

main()


#prentrega (lo de abajo va en una carpeta llamada prentrega)

# inicio.py

# desde inicio utilizar el paquete entero, o sea, llamamos desde inicio 
# git branch dev (crear una rama de pruebas, asi no nos paramos en la main())
# git checkout dev cambiamos a la rama dev y salimos de main (es una copia de main)
# git merge dev para combinar la rama dev con la rama main
# siempre en el archivo que python va a llamar usamos importaciones absolutas
# las importaciones relativas las usamos dentro de paquete, utilizando el punto .

from paquete.manejo_de_datos import cargar_datos, mostrar_datos  
from paquete.usuarios import entrar_datos
import pathlib # asi se puede tambien

# main() ya tiene acceso a esta variable global
# esta variable puede ser llamada desde cualquier funcion por ser global
BASE_DIR = pathlib.Path(__file__).resolve().parent
RUTA_BASE_DATOS = BASE_DIR / "base_de_datos.json"
base_datos = [] # una vez que entran los datos se guardan en esta lista vacia que contiene dict
# es una lista vacia de usuarios

def main(): # main se dedica a llamar funciones
    base_datos: list = cargar_datos(RUTA_BASE_DATOS)
    entrar_datos(RUTA_BASE_DATOS, base_datos) 
    mostrar_datos(base_datos)
    
main()


# manejo de datos.py

import json

# importamos base_datos en ambas porque la tiene inicio
def guardar_datos(RUTA_BASE_DATOS, base_datos): # usa json, me crea el archvo con lo que tenga la base de datos ##2
    # aca tambien iria un try-except
    with open(RUTA_BASE_DATOS, "w") as archivo:
        json.dump(base_datos, archivo, indent=4)

# importamos base_datos en embas porque las tiene inicio
def cargar_datos(RUTA_BASE_DATOS) -> list: # usa json
    # si no devuelve una lista me da error 
    base_datos = []
    try:
        with open(RUTA_BASE_DATOS, "r") as archivo:
            base_datos = json.load(archivo)
    except Exception as e: # para atrapar excepciones que no conozcamos
        print("Error:", type(e)) # para ver el tipo de error 
        pass # si no existe nada, que lo pase y muestre los datos 
    return base_datos

def mostrar_datos(base_datos): 
    print(base_datos)


# usuario.py

from .manejo_de_datos import guardar_datos


def entrar_datos(RUTA_BASE_DATOS, base_datos: list): # aca va a interactuar con el usuario  
    usuarios = {}
    usuarios["nombre"] = input("Ingrese un nombre de usuario: ").capitalize()
    usuarios["contraseña"] = input("Ingrese una contraseña: ")
    base_datos.append(usuarios) # en la base de datos de arriba agrega los datos
    guardar_datos(RUTA_BASE_DATOS, base_datos) # llamo a guardar datos y le paso la lista(base_datos) porque hice un append en la linea de arriba
