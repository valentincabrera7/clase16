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
