# repositiory_1
This is my first repository.
Para calcular el diametro de una tuberia fue necesario realizar un programa que contenga las funciones necesarias en este caso llamado (sucesivas.py) con esto se puede obtener un cauldal estimado y los factores que se ven involucrados en el cálculo de ducho diametro
Mediante el proceso de aproximaciones sucesivas se va a estimar el dimetro y con ello se tomara en cuenta los mejores valores para cada paramétro
import numpy as np
import matplotlib.pyplot as plt
#nombre de la class indica el inicio de una clase en python
#la clase es un sonjunto de funciones, que se recomineda
#agrupen acorde a afinidad
class aproximaciones:
    def  __init__(self, LT, z1, z2, rho, nu, e_r, Qmax, Qmin):
        self.LT=LT
        self.z1=z1
        self.z2=z2
        self.rho=rho
        self.nu=nu
        self.e_r=e_r
        self.Qmax=Qmax
        self.Qmin=Qmin
    def ve(self,f,D):
        v = (2*9.81*(self.z1 - self.z2)/(1 + (f*self.LT /D)))**0.5;
        return v
    def fric(self,D,Re):
        ru = D /self.e_r
        L = (np.log10((1/(3.7*ru)) + (5.74/(Re**(0.9)))))**2;
        f = 0.25/L
        return f
    def Re(self,v,D):
        Rey = v*D*self.rho/self.nu
        return Rey
    def Q_t(self,D,v):
        Q =  np.pi*(D**2)/4
        return Q
con las funciones necesarias definidas se realizará el método de aproximaciones sucesivas para obtener el diamétro adecuado para la tuberia
Se importara el archivo sucesivas para reemplazar los valores dados por el ejercicio
import numpy as np
import matplotlib.pyplot as plt
from sucesivas import aproximaciones

LT = 84   # Longitud de tubería [m]
z1 = 50  # Cota inicial [m]
z2 = 1.5  # Cota final [m]
rho = 998  # Densidad del agua [kg/m3]
nu = 0.001005  # Viscosidad del agua [kg/(m*s)]
e_r = 0.0015  # Rugosidad de la tubería [mm]
Qmax = 20/1000  # Caudal máximo permitido [m3/s]
Qmin = 15/1000  # Caudal mínimo permitido [m3/s]

Ap = aproximaciones(LT, z1, z2, rho, nu, e_r, Qmax, Qmin)

# Valores asumidos
f = 0.0138 #Factor de fricción
D = (25.4)/1000 # Diametro en [m]

v=Ap.ve(f,D)

Re = Ap.Re(v,D)

fb = Ap.fric(D,Re)

Q = Ap.Q_t(D, v) *1000

print("Magnitud de velocidad =", v)
print("Número de Reynolds =", Re)
print("Factor de fricción f =", f)
print("Caudal estimado =", Q)

Con esto se obtienen los siguientes resultados:
Magnitud de velocidad = 4.517013254969275
Número de Reynolds = 113933.00736603695
Factor de fricción f = 0.0138
Caudal estimado = 0.5067074790974977
Modificando el parámetro del diametro se obtienen diferentes valores para los cuales se tendra que obtener el adecuado.

