1_a)con respecto al tiempo el codigo con hilos es mas rapido en ejecucion que el codigo sin hilos, es predecible ya que utiliza mas procesos el codigo con hilos ya que varia de tu cpu y la memoria
1_b)No son iguales ya que poseemos diferentes caracteristicas en lo que respecta la computadora
1_c)al borrar # el tiempo de ejecucion se hace mas extenso,ya que descomentar las lineas se activan otros procesos en el codigo 

Punto2_a)
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

#define NUMBER_OF_THREADS 2
#define CANTIDAD_INICIAL_HAMBURGUESAS 20

int cantidad_restante_hamburguesas = CANTIDAD_INICIAL_HAMBURGUESAS;
int turno = 0;

void *comer_hamburguesa(void *tid) {
    while (1) { 
        while(turno != (int)tid); 

        
        if (cantidad_restante_hamburguesas > 0) {
            printf("Hola! soy el hilo(comensal) %d, me voy a comer una hamburguesa! Ya que todavia queda/n %d \n", (int) tid, cantidad_restante_hamburguesas);
            cantidad_restante_hamburguesas--;
        } else {
            printf("SE TERMINARON LAS HAMBURGUESAS :( \n");
            turno = (turno + 1) % NUMBER_OF_THREADS;
            pthread_exit(NULL); 
        }
       
        turno = (turno + 1) % NUMBER_OF_THREADS;
    }
}

int main() {
    pthread_t threads[NUMBER_OF_THREADS];
    int thread_ids[NUMBER_OF_THREADS];
    for (int i = 0; i < NUMBER_OF_THREADS; i++) {
        thread_ids[i] = i;
        pthread_create(&threads[i], NULL, comer_hamburguesa, (void *)&thread_ids[i]);
    }
    for (int i = 0; i < NUMBER_OF_THREADS; i++) {
        pthread_join(threads[i], NULL);
    }
    return 0;
}
![Screenshot 2024-07-05 at 14-54-49 Trabajo práctico N3 pdf](https://github.com/SantiiFigarra/ASO2024TPs/assets/169952593/79a6d57f-c643-4743-a5a5-f59fa5e3ee2e)


