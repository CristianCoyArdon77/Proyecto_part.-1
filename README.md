# Proyecto_part.-1
Proyecto para programacion
# base_de_datos.json
import json

try:
    with open("base_de_datos.json", "r") as archivo_db:
        print("Leyendo base de datos...")
        lista_estudiantes = json.load(archivo_db)
        print("Base de datos cargada exitosamente")
except:
    print("Creando nueva base de datos...")
    lista_estudiantes = []

def calcular_promedio(lista_notas_estudiante):
    total_suma = 0
    for nota in lista_notas_estudiante:
        total_suma = total_suma + nota
    # obtener cantidad de notas
    cantidad_notas = len(lista_notas_estudiante)
    promedio = total_suma / cantidad_notas
    return promedio

    #APROBACION DE CURSOS
def cursos_aprobados(l_nots):
    c=0
    for nota in l_nots:        
        if nota > 61:
         c=c+1
    return c

    #AÑO INGRESO POR CARNET
def an_i(carnet_):
     x = carnet_.split("-")
     a = (x[0])     
     return a

    # aqui me quede no se como proceder
def busqueda (lista_e,carnet_):
    if lista_e: 
        for e_ in lista_e:
            for c_ in e_:
             if carnet_ == c_:
                return e_
    else:
        return False             
    return

    #PORCENTAJE DE CURSOS
def porcentaje (c_asignados,c_aprobados):
    c_asig = int(c_asignados)
    c_apr =int(c_aprobados)
    p = c_apr * 100 / c_asig
    return p

def ingresar_nuevo_estudiante():
    nombre = input("Ingrese nombre: ")
    carnet = input("Ingrese carnet: ")
    
    #d_ = busqueda(lista_estudiantes, carnet)
    #while d_ != False or isinstance(d_ , str):
        #print('El carnet ya existe, ingrese otro: ')
        #carnet = input("ingrese carnet")
        #d_ = busqueda(lista_estudiantes, carnet)
    curso = input("Ingrese cantidad de cursos asignados: ")
    lista_notas = []
    opcion_notas = input("Quiere ingresar una nota? (y / n): ")
    while opcion_notas == 'y' or opcion_notas == 'Y':
        nueva_nota = input("Ingrese la nota: ")
        # convertir en entero
        nueva_nota = int(nueva_nota)
        lista_notas.append(nueva_nota)
        opcion_notas = input("Quiere ingresar otra nota? (y / n): ")
    
    # llamar al calculo de promedio
    promedio_estudiante = calcular_promedio(lista_notas)
    # crear al nuevo estudiante
    anno = an_i(carnet)
    cur_apro = cursos_aprobados(lista_notas)
    porcen_ = str(porcentaje(curso,cur_apro))
    estudiante = {
        'nombre': nombre,
        'carnet': carnet,
        'cursos asignados': curso,
        'notas': lista_notas,
        'promedio': promedio_estudiante,
        'año de ingreso': anno,
        'cursos aprobados': cur_apro,
        'porcentaje de cursos aprobados': porcen_ + ' %'
    }
    # agregar el nuevo estudiante a la lista
    lista_estudiantes.append(estudiante)
    return


    

def mostrar_lista_estudiantes():
    print(lista_estudiantes)
    return

def mostrar_cantidad_estudiantes():
    cantidad = len(lista_estudiantes)
    print(f'Hay {cantidad} cantidad de estudiantes')
    return

    # no pude completarlo
def Busqueda_por_carnet():
    ct = input("Ingrese el carnet a buscar: ")
    r=busqueda(lista_estudiantes,ct)
    if r:
        print(r)
    else:
        print("El carnet no existe  ")
    return

    

def mostrar_menu():
    mensaje_menu = """Seleccione la opcion que quiera \n
    1. Ingresar un nuevo estudiante\n
    2. Ver la lista de estudiantes\n
    3. Mostrar cantidad de los estudiantes\n
    4. Buscar Estudiante por carnet\n
    0. Salir\n
    > 
    """
    opcion = input(mensaje_menu)
    opcion = int(opcion)
    if opcion == 1:
        ingresar_nuevo_estudiante()
    if opcion == 2:
        mostrar_lista_estudiantes()
    if opcion == 3:
        mostrar_cantidad_estudiantes()
    if opcion == 4:
        Busqueda_por_carnet()
    if opcion == 0:
        with open("base_de_datos.json", "w") as archivo_db:
            print("Guardando base de datos...")
            json.dump(lista_estudiantes, archivo_db)
        return
    mostrar_menu()
    return


mostrar_menu()
# CRISTIAN OMAR COY ARDÓN
# CARNET: 1990-17-4950
