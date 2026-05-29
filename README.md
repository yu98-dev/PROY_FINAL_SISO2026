# Mini Kernel - Simulación de Sistema Operativo en C
 
Proyecto final Sistemas Operativos 2026A  
Universidad Santiago de Cali · Facultad de Ingeniería
 
## Integrantes
 
| Nombre | ID |
|--------|--------|
| Julián Andrés Gómez Cabrera | 1107838827 |
| Samuel Orozco Varela | 1107838996 |
| Juliana Pérez Rocha | 1144103598 |
 
## Descripción
 
Simulación funcional de un sistema operativo básico implementada en ANSI C. Integra cuatro módulos independientes: gestión de memoria, planificación de procesos, sistema de archivos y coordinación central del kernel.
 
## Estructura del proyecto
 
```
PROYECTO_FINAL/
├── kernel.c        # Núcleo coordinador — punto de entrada del sistema
├── memory.c        # Administrador de memoria (fija, dinámica, paginación, segmentación)
├── memory.h        # Contratos públicos del módulo de memoria
├── processes.c     # Planificador de procesos (FCFS, RR, SJF, Prioridad, CFS)
├── processes.h     # Contratos públicos del módulo de procesos
├── files.c         # Sistema de archivos sobre disco real (carpeta archivos/)
├── files.h         # Contratos públicos del módulo de archivos
└── README.md       # Este archivo
```
 
## Compilación
 
Requiere `gcc` instalado. En Linux / GitHub Codespaces:
 
```bash
gcc -Wall -std=c99 kernel.c memory.c processes.c files.c -o mini_kernel
```
 
## Ejecución
 
```bash
./mini_kernel
```
 
Al iniciar, el sistema solicita configurar la sesión:
 
- **Algoritmo de memoria:** Dinámica Best Fit / Worst Fit · Fija Best Fit / Worst Fit
- **Algoritmo de planificación:** FCFS · Round Robin · SJF · Prioridad · CFS
- **Mecanismo de traducción:** Paginación · Segmentación · Ambos
## Flujo básico de uso
 
```
1. Crear proceso        (opción 1)
2. Crear archivo        (opción 5)
3. Abrir archivo        (opción 7) — requiere PID del proceso
4. Escribir archivo     (opción 9)
5. Leer archivo         (opción 8)
6. Cerrar archivo       (opción 10)
7. Apagar sistema       (opción 0) — muestra estado final y libera recursos
```
 
Los archivos creados se guardan en la carpeta `archivos/` dentro del directorio de ejecución.
 
## Módulos
 
| Módulo | Responsabilidad |
|--------|----------------|
| `memory.c` | Asignación y liberación de memoria, traducción de direcciones |
| `processes.c` | Ciclo de vida del PCB, algoritmos de planificación, algoritmo del banquero |
| `files.c` | Operaciones CRUD sobre archivos reales, control de acceso con lock binario |
| `kernel.c` | Coordinación entre módulos, tabla de procesos activos, menú principal |
 
## Notas técnicas
 
- Los archivos `.h` declaran los contratos públicos de cada módulo: funciones, estructuras y constantes accesibles entre archivos.
- Al apagar el sistema, `terminar_proceso_kernel()` garantiza el cierre de todos los archivos y la liberación de memoria de cada proceso activo.
