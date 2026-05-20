# UNIDAD-5
ejercicio 1 tabla inferencia

import numpy as np # importa numpy para manejo de arreglos y operaciones

x  = np.array([1,2,3]) # define los valores de x conocidas
y  = np.array([1,4,9]) # define los valoes de y conocidas

n = len(x) # calcula el numero de puntos

tabla = np.zeros((n,n)) # inicializa la tabla de diferencias divididas

tabla[:,0] = y #llena la primera columna con los valores de y

for j in range(1,n): #itera sobre las columnas de la tabla
    for i in range(n-j): #itera sobre las filas disponibles
        tabla [i,j] = (tabla[i+1,j-1] - tabla[i,j-1]) / (x[i+j] -x[i]) # calcula la diferencia

print("tabla de diferencias dividias : \n" ,tabla)# muestra la tabla

Ejercicio 2 
import numpy as np # importa numpy para manejo de arreglos y operaciones

x  = np.array([1,2,3]) # define los valores de x conocidas
y  = np.array([1,4,9]) # define los valoes de y conocidas

n = len(x) # calcula el numero de puntos

tabla = np.zeros((n,n)) # inicializa la tabla de diferencias divididas

tabla[:,0] = y #llena la primera columna con los valores de y

for j in range(1,n): #itera sobre las columnas de la tabla
    for i in range(n-j): #itera sobre las filas disponibles
        tabla [i,j] = (tabla[i+1,j-1] - tabla[i,j-1]) / (x[i+j] -x[i]) # calcula la diferencia

def newton_eval(x_data,tabla,x_val): #define funcion para evaluar el polinimio
  n = len(x_data) #numero de puntos
  resultado = tabla[0,0] # inicializa con primer coeficiente

  producto = 1  # inicializa el producto acumulado

  for i in range(1,n): # itera sobre terminos del polinomio
    producto *= (x_val - x_data[i-1]) # calcula el termino (x-x_i)
    resultado += tabla[0,i]*producto # suma el termino correspondiente

  return resultado # retorna valor interpolado

valor = newton_eval(x,tabla,2.5) # evalua el polinomio en x=2.5

print("valor interpolado : ",valor) #muestra resultado


EJERICIO 3 interpolacion de datos
import numpy as np # importa

x = np.array([0,1,2,3])
y = np.array([1,2,0,5])

n = len(x) # calcula el numero de puntos

tabla = np.zeros((n,n)) # inicializa la tabla de diferencias divididas

tabla[:,0] = y #llena la primera columna con los valores de y

for j in range(1,n): #itera sobre las columnas de la tabla
    for i in range(n-j): #itera sobre las filas disponibles
        tabla [i,j] = (tabla[i+1,j-1] - tabla[i,j-1]) / (x[i+j] -x[i]) # calcula la diferencia


def newton(x_data,tabla,x_val): #define funcion para evaluar el polinimio
  n = len(x_data) #numero de puntos
  resultado = tabla[0,0] # inicializa con primer coeficiente
  producto = 1

  for i in range(1,n): # itera sobre terminos del polinomio
    producto *= (x_val - x_data[i-1]) # calcula el termino (x-x_i)
    resultado += tabla[0,i]*producto # suma el termino correspondiente

  return resultado

x_interp = 1.5 # punto donde se quiere estimar el valor

y_interp = newton(x,tabla,x_interp) # interpolacion

print("valor estimado : ",y_interp) # resulatdo final

EJERCICIO IMPLEMENTACION DE LARANGE
import numpy as np # importa

x = np.array([1,2,3]) # Define los puntos conocidos en x
y = np.array([1,4,9]) # Define los valores correspodientes en y

def lagrange(x_data,y_data,x_val):  # define la funcion de interpolacion
  n = len(x_data) # obtiene el numero de puntos
  resultado = 0 #inicializa el resultado del polinomio


  for i in range(n): #itera sobre cada punto
    L = 1 #inicializa del polinomio base L_i

    for j in range(n): #itera sobre todos los puntos para construir L_i
        if j !=i: # evita entre 0 cuando i=j
            L *= (x_val - x_data[j]) / (x_data[i] - x_data[j]) # calcula el

    resultado += y_data[i] * L #acumula el termino correspondiente al polinomio

  return resultado # retorna el valor interpolado

valor = lagrange(x,y,2.5) # evalua el polinomio en x=2.5

print("Valor interpolado : ",valor)
EJERICIO COMPARACION CON FUNCION REAL 
import numpy as np  # Importa NumPy

def f(x):  # Define la función real
    return x**2  # Función cuadrática

x = np.array([1,2,3])  # Puntos conocidos
y = f(x)  # Evalúa la función en esos puntos

def lagrange(x_data,y_data,x_val):  # Función de interpolación
    n = len(x_data)  # Número de puntos
    resultado = 0  # Inicializa resultado

    for i in range(n):  # Itera sobre cada punto
        L = 1  # Inicializa polinomio base

        for j in range(n):  # Itera sobre puntos
            if j != i:  # Evita división por cero
                L *= (x_val - x_data[j])/(x_data[i] - x_data[j])  # Calcula término

        resultado += y_data[i]*L  # Suma contribución

    return resultado  # Retorna valor

x_test = 2.5  # Punto de prueba

interp = lagrange(x,y,x_test)  # Valor interpolado

real = f(x_test)  # Valor real

error = abs(real - interp)  # Calcula error

print("Interpolado:", interp)
print("Real:", real)
print("Error:", error)

EJERCICIO RECONSTRUCCION DE DATOS
import numpy as np  # Importa NumPy

x = np.array([0,1,2,3])  # Datos en x (pueden ser tiempos o features)
y = np.array([1,3,2,5])  # Datos observados (pueden tener ruido)

def lagrange(x_data,y_data,x_val):  # función de interpolación
    n = len(x_data)  # Número de puntos
    resultado = 0  # Inicializa salida

    for i in range(n):  # Itera sobre puntos
        L = 1  # Inicializa polinomio base

        for j in range(n):  # Itera para construir L_i
            if j != i:  # Evita división inválida
                L *= (x_val - x_data[j])/(x_data[i] - x_data[j])  # Calcula término

        resultado += y_data[i]*L  # Acumula resultado

    return resultado  # Retorna valor interpolado

x_interp = 1.5  # Punto donde falta dato

y_interp = lagrange(x,y,x_interp)  # Estima valor faltante

print("Valor estimado:",y_interp)  # Resultado
