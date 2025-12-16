# Trabajo Práctico N°6 - Simulación de Barras de un Festival
## Simulación - UTN FRBA

---

## 📋 Descripción del Proyecto

Este proyecto consiste en el modelado y simulación de un sistema de optimización de la barra de bebidas en un festival, con el objetivo de analizar y mejorar la eficiencia del servicio mediante la gestión del personal y la redirección de clientes, con base en datos históricos de llegadas, tiempos de servicio y probabilidad de abandono.

## 🎯 Objetivo General

Desarrollar un modelo de simulación de eventos discretos para optimizar la operación de una barra de bebidas en un festival, permitiendo analizar y mejorar:

- Tiempos de espera  
- Abandono de clientes  
- Utilización de bartenders  
- Impacto de la redirección de clientes  

**Objetivos Específicos**
1. Analizar el comportamiento real de llegadas y servicios a partir del dataset
2. Ajustar distribuciones estadísticas a:
- Intervalo entre arribos
- Tiempos de preparación
3. Implementar generación de variables aleatorias mediante distribuciones ajustadas
4. Construir la lógica evento a evento del sistema
5. Obtener métricas de rendimiento y proponer mejoras operativas

---

## 📊 Dataset

**Fuente:** Datos históricos de un festival de bebidas.  
**Registros:** Datos históricos de llegadas de clientes, tiempos de preparación y abandono  

**Variables Principales:**
| Variable               | Descripción                                   |
| ---------------------- | --------------------------------------------- |
| `customer_id`          | Identificador único del cliente               |
| `arrival_time`         | Timestamp de llegada del cliente              |
| `arrival_seconds`      | Tiempo de llegada en segundos desde el inicio |
| `interarrival_seconds` | Tiempo entre llegadas consecutivas            |
| `service_time`         | Tiempo de atención del cliente (segundos)     |
| `drink`                | Tipo de bebida (cerveza / cóctel)             |
| `amount`               | Monto total consumido                         |
| `quantity`             | Cantidad de bebidas                           |
| `payment_method`       | Medio de pago                                 |
| `age`                  | Edad del cliente                              |
| `id_bartender`         | Identificador del bartender                   |
| `type_bartender`       | Tipo de bartender (cerveza / cóctel)          |


## 🔍 Análisis Previo Realizado
### 1. Clasificación del Modelo

**Tipo de Modelo:** Simulación de Eventos Discretos (DES)  
**Sistema:** Estocástico, dinámico, de cola  

###  2. Variables del Sistema
#### 📥 Variables de Entrada (Exógenas – Datos)

| Código | Variable                          | Descripción                                                         |
| ------ | --------------------------------- | ------------------------------------------------------------------- |
| IA     | Intervalo entre Arribos           | Tiempo entre llegadas consecutivas de clientes al sistema (minutos) |
| TPCoct | Tiempo de Preparación de Cócteles | Tiempo requerido para preparar un cóctel (minutos)                  |
| TPCerv | Tiempo de Preparación de Cerveza  | Tiempo requerido para servir una cerveza (minutos)                  |

#### 🎛️ Variables de Control

| Código | Variable               | Descripción                                                                                                      |
| ------ | ---------------------- | ---------------------------------------------------------------------------------------------------------------- |
| BCoct  | Bartenders de Cócteles | Cantidad de bartenders especializados en cócteles                                                                |
| BCerv  | Bartenders de Cervezas | Cantidad de bartenders especializados en cervezas                                                                |
| UR     | Umbral de Redirección  | Longitud de la fila de cervezas que activa la redirección de un cliente cervecero hacia un bartender de cócteles |

#### 📊 Variables de Resultado
| Código     | Variable                             | Descripción                                                 |
| ---------- | ------------------------------------ | ----------------------------------------------------------- |
| PACoct     | Porcentaje de Abandono de Cocteleros | Proporción de clientes de cócteles que abandonan el sistema |
| PACerv     | Porcentaje de Abandono de Cerveceros | Proporción de clientes cerveceros que abandonan el sistema  |
| PTOCoct(j) | Tiempo Ocioso Bartender Cóctel       | Porcentaje de tiempo ocioso del bartender de cócteles *j*   |
| PTOCerv(i) | Tiempo Ocioso Bartender Cerveza      | Porcentaje de tiempo ocioso del bartender de cervezas *i*   |
| PTECerv    | Tiempo de Espera Cerveceros          | Tiempo promedio de espera de los clientes cerveceros        |
| PTECoct    | Tiempo de Espera Cocteleros          | Tiempo promedio de espera de los clientes cocteleros        |

#### 🔄 Variables de Estado
| Código | Variable                           | Descripción                                                            |
| ------ | ---------------------------------- | ---------------------------------------------------------------------- |
| NSCerv | Número de Cerveceros en el Sistema | Cantidad de clientes cerveceros (en cola o siendo atendidos) |
| NSCoct | Número de Cocteleros en el Sistema | Cantidad de clientes cocteleros (en cola o siendo atendidos) |

---

## 📈 Resultados del Análisis de Datos

### 🔑 Parámetros Clave para la Simulación:  

**1️⃣ Tiempo entre Llegadas de Clientes**  
Distribución ajustada basada en los datos históricos de llegada.  

**2️⃣ Probabilidad de Abandono**  
**Cerveceros:** 30% si la fila supera las 10 personas, 50% si supera las 12.  
**Cocteleros:** 40% si la fila supera las 5 personas, 100% si supera las 7.  

## 📊 Distribuciones Estadísticas Ajustadas
Tiempo de Servicio  
Se ajustaron distribuciones de tiempo de servicio para cada tipo de bebida:  
Cerveza: Distribución beta  
Cócteles: Distribución johnsonsb  

## 🛠️ Tecnologías y Herramientas

- Python 3.12+
- Pandas: Manipulación y análisis de datos
- NumPy: Operaciones numéricas
- Matplotlib: Visualización de datos
- SciPy: Distribuciones estadísticas
- Fitter: Ajuste automático de distribuciones
- Jupyter Notebook / Google Colab: Entorno de desarrollo

---

## 📁 Estructura del Proyecto
```simulacion_barras_festival/
│
├── README.md                               # Este archivo
├── TP__Barras_Festival_Colab_2025.ipynb    # Notebook principal con análisis y simulación
├── Datos/
│   └── Grupo5-Festival_barras.csv          # Dataset original
├── Diagramas/                             
│   └──  Grupo5-DiagramaFlujo.pdf           # Diagrama de flujo de la rutina principal
└── Documentos/
    └── Grupo5-Enunciado-Análisis.docx      # Documentación del análisis previo
    └── Grupo5-PPT.pptx
    └── Grupo5-Paper.docx
```

## 🚀 Cómo Ejecutar
1. Clonar el repositorio  
``` git clone <URL_del_repositorio> cd simulacion_barras_festival ```
2. Instalar dependencias  
``` pip install pandas numpy matplotlib scipy simpy  ```
3. Ejecutar el notebook  
``` jupyter notebook Simulacion_Barras_Festival.ipynb O subir a Google Colab y ejecutar las celdas en orden. ```

---

## 📝 Metodología de Trabajo  
### **Fase 1: Análisis Previo**  
Definición del modelo y las variables clave  
Identificación de distribuciones de llegada y servicio  

### **Fase 2: Análisis de Datos**    
Carga y limpieza del dataset  
Ajuste de distribuciones estadísticas  
Identificación de patrones de abandono  

### **Fase 3: Simulación 🔄**  
Implementación de la simulación con eventos discretos  
Análisis de métricas de rendimiento  
Optimización de la operación de la barra  

---

## 👥 Integrantes

- Facundo CahuÉ  
- Leonel Contreras  
- Roger Ramos  
- Nicolas Ross

**Universidad:** UTN FRBA  
**Año:** 2025  

---

## 📚 Referencias

- Ross, S. M. (2013). *Simulation* (5th ed.). Academic Press.
- Law, A. M. (2015). *Simulation Modeling and Analysis* (5th ed.). McGraw-Hill.
- Documentación de Python: https://docs.python.org/
- SciPy Statistical Distributions: https://docs.scipy.org/doc/scipy/reference/stats.html
- Fitter Library: https://fitter.readthedocs.io/

## 📄 Licencia
Este proyecto es de carácter académico para la UTN FRBA.

---

## ✉️ Contacto
Para consultas sobre este proyecto, contactar a través del mail rogerramosaw@gmail.com





