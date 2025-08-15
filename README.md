#CALCULO_ESTOCASTICOS
import numpy as np
import matplotlib.pyplot as plt
import math
import random

t = 1 #tiempo al que queremos ver el proceso
n = 500 #numero de subintervalos de 0 a 1
N = 100 #Numero de Trayectorias
Δt = 1/n
Δx = math.sqrt(Δt)

W_0 = 0 #Procesos de Weiner al tiempo CERO
vector_t = np.arange(0, (math.floor(n*t)+1))*Δt

#Matriz tamaño Nxnt
M = np.zeros((N, math.floor(n*t)+1))
#Generamos a +1, -1, hacia donde se mueve
for i in range(0, N):
  gen = np.cumsum(random.choices([-1, 1], [1/2, 1/2], k = math.floor(n*t)))*Δx
  W_t = np.array([W_0] + list(gen))
  M[i:] = W_t

media  = np.mean(M, axis  = 0)
varianza = np.var(M, axis = 0)

plt.plot(vector_t, np.transpose(M))
plt.plot(vector_t, media, color = "black")
plt.plot(vector_t, varianza, color = "orange")

plt.xlabel("Tiempo")
plt.ylabel("W(t)")
plt.title("Procesos de Weiner")
plt.grid(True)
plt.show()
