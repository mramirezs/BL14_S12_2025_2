# 🧬 Elementos de la sintaxis de Shell Scripting III

## 📚 Información del Curso
**Curso:** Principios de programación - Bioinformática  
**Universidad:** Universidad Peruana de Ciencias Aplicadas (UPC)  
**Programa:** Biología  
**Facultad:** Ciencias de la Salud  
**Semestre:** 2025-02  

### 👨‍🏫 Docentes:
- **Frank Guzman Escudero**
- **Manuel Ramírez Sáenz**

---

## 🎯 Objetivo de Aprendizaje

Al finalizar esta sesión, serás capaz de:

- ✅ **Crear y manipular arrays (listas)** en Bash
- ✅ **Acceder y modificar elementos** de arrays
- ✅ **Usar bucles `for`** para automatizar tareas repetitivas
- ✅ **Implementar bucles con tres expresiones** (inicialización, condición, incremento)
- ✅ **Aplicar estos conceptos** a análisis bioinformáticos
- ✅ **Automatizar procesamiento** de archivos y datos biológicos

**Palabras clave:** Arrays, bucles for, automatización, control de flujo, bioinformática

---

## 📑 Contenido de la Clase

1. [Arrays (listas) en Bash](#-arrays-listas-en-bash)
2. [Operaciones con Arrays](#-operaciones-con-arrays)
3. [Control de flujo: Bucles FOR](#-control-de-flujo-bucles-for)
4. [Bucles con tres expresiones](#-bucles-con-tres-expresiones)
5. [Aplicaciones en Bioinformática](#-aplicaciones-en-bioinformática)
6. [Actividad Asincrónica - Misión Imposible](#-actividad-asincrónica---misión-imposible)

---

## 🗃️ Arrays (listas) en Bash

### ¿Qué es un Array?
Un **array** es una variable que puede contener múltiples valores de distinta naturaleza, organizados de forma secuencial.

### Características importantes:
- **Valores secuenciales** con índices numéricos
- **No hay límite máximo** de elementos
- **El índice comienza en 0** (primer elemento = posición 0)
- Pueden contener **números, texto, nombres de archivos**, etc.

### 📝 Declaración de Arrays

#### Método 1: Declaración directa
```bash
# Crear un array con elementos
archivos=("a1.txt" "a2.txt" "a3.txt" "a4.txt" "a5.txt")
numeros=(1 2 3 4 5)
bases=("A" "T" "C" "G")
```

#### Método 2: Asignación individual
```bash
# Asignar elementos uno por uno
array[0]="primer_elemento"
array[1]="segundo_elemento"
array[2]="tercer_elemento"
```

#### Método 3: Rangos automáticos
```bash
# Crear rangos de letras y números
letras=({A..Z})                    # A B C ... Z
numeros=({1..100})                 # 1 2 3 ... 100
cromosomas=(chr{1..22} chrX chrY)  # chr1 chr2 ... chr22 chrX chrY
```

### 🔍 Ejemplo Bioinformático
```bash
#!/bin/bash
# Crear lista de genes relacionados con cáncer
genes_cancer=("BRCA1" "BRCA2" "TP53" "PTEN" "CHEK2")
echo "Genes de cáncer: ${genes_cancer[*]}"
```

---

## 🛠️ Operaciones con Arrays

### 📖 Mostrar contenido del array

```bash
# Mostrar todos los elementos
echo ${lista[@]}    # Método 1
echo ${lista[*]}    # Método 2

# Ejemplo práctico
secuencias=("ATCG" "GCAAG" "TTTT")
echo "Todas las secuencias: ${secuencias[*]}"
```

### 🎯 Acceder a elementos específicos

```bash
# Sintaxis: ${nombre_array[índice]}
numeros=(1 2 3 4 5)

echo ${numeros[0]}   # Primer elemento: 1
echo ${numeros[1]}   # Segundo elemento: 2
echo ${numeros[-1]}  # Último elemento: 5
echo ${numeros[-2]}  # Penúltimo elemento: 4
```

### ➕ Añadir elementos

```bash
# Añadir al final sin especificar índice
numeros+=(6 7 8)

# Modificar un elemento específico
numeros[5]=100

# Ejemplo con secuencias
secuencias=("ATCG" "GCAAG")
secuencias+=("AAAA")  # Añadir nueva secuencia
echo ${secuencias[*]}
```

### ❌ Eliminar elementos

```bash
# Eliminar un elemento específico
unset array[índice]

# Eliminar todo el array
unset array

# Ejemplo
numeros=(1 2 3 4 5)
unset numeros[0]     # Elimina el primer elemento
echo ${numeros[*]}   # Resultado: 2 3 4 5
```

### 📏 Información del Array

```bash
# Obtener longitud del array
echo ${#numeros[*]}

# Obtener índices del array
echo ${!numeros[*]}

# Ejemplo con genes
genes=("SOX13" "PAX5" "TC1" "ADF")
echo "Número de genes: ${#genes[*]}"
echo "Índices: ${!genes[*]}"
```

### 📂 Arrays con archivos

```bash
# Crear array con archivos del directorio
archivos=($(ls))              # Todos los archivos
archivos_txt=($(ls *.txt))    # Solo archivos .txt
archivos_sh=($(ls *.sh))      # Solo scripts .sh

echo "Archivos .txt encontrados: ${#archivos_txt[*]}"
```

---

## 🔄 Control de flujo: Bucles FOR

### ¿Por qué usar bucles?
Los bucles nos permiten **automatizar tareas repetitivas** que normalmente tendríamos que hacer manualmente muchas veces.

### 📋 Sintaxis básica del bucle FOR

```bash
for variable in lista_de_elementos
do
    comando1
    comando2
    comandoN
done
```

### 🧪 Ejemplos básicos

#### Ejemplo 1: Iterar sobre nombres
```bash
#!/bin/bash
for nombre in Mary John Keyla Bryan
do
    echo "Hello $nombre"
done
```

#### Ejemplo 2: Iterar sobre números
```bash
#!/bin/bash
for i in 1 2 3 4 5
do
    echo "Número: $i"
done
```

#### Ejemplo 3: Usando rangos
```bash
#!/bin/bash
# Números del 1 al 10
for i in {1..10}
do
    echo "Iteración $i"
done

# Números pares del 2 al 20
for i in {2..20..2}
do
    echo "Número par: $i"
done
```

### 🧬 Aplicaciones Bioinformáticas

#### Ejemplo 1: Análisis de bases nitrogenadas
```bash
#!/bin/bash
for base in Adenina Timina Citosina Guanina
do
    echo "La $base es una base nitrogenada"
done
```

#### Ejemplo 2: Iterar sobre arrays de genes
```bash
#!/bin/bash
genes=("SOX13" "PAX5" "TC1" "ADF")
for gen in ${genes[@]}
do
    echo "Analizando gen: $gen"
    echo "Longitud del nombre: ${#gen} caracteres"
done
```

#### Ejemplo 3: Crear directorios automáticamente
```bash
#!/bin/bash
# Crear 5 directorios para muestras
for i in {1..5}
do
    mkdir "muestra_$i"
    echo "Directorio muestra_$i creado"
done
```

#### Ejemplo 4: Procesar archivos
```bash
#!/bin/bash
# Listar información de todos los archivos .txt
for archivo in *.txt
do
    echo "Procesando: $archivo"
    ls -lh "$archivo"
done
```

---

## ⚙️ Bucles con tres expresiones

### Sintaxis de bucle C-style

```bash
for ((inicialización; condición; incremento))
do
    comandos
done
```

### 📊 Componentes:
- **EXP1 (Inicialización):** `c=1` - Define el valor inicial
- **EXP2 (Condición):** `c<=5` - Condición para continuar
- **EXP3 (Incremento):** `c++` - Cómo se modifica la variable

### 🔢 Ejemplos prácticos

#### Ejemplo 1: Contador básico
```bash
#!/bin/bash
for ((c=1; c<=5; c++))
do
    echo "Iteración número: $c"
done
```

#### Ejemplo 2: Contador descendente
```bash
#!/bin/bash
for ((c=10; c>=1; c--))
do
    echo "Cuenta regresiva: $c"
done
```

#### Ejemplo 3: Incrementos personalizados
```bash
#!/bin/bash
# Contar de 2 en 2
for ((i=0; i<=20; i+=2))
do
    echo "Número par: $i"
done
```

---

## 🧬 Aplicaciones en Bioinformática

### 📈 Ejemplo 1: Análisis de cuantificación de ADN
```bash
#!/bin/bash
# Array con valores de cuantificación
concentraciones=("26 ng/ul" "70 ng/ul" "80 ng/ul" "35 ng/ul")

echo "=== ANÁLISIS DE CUANTIFICACIÓN DE ADN ==="
for i in ${!concentraciones[@]}
do
    echo "Muestra $((i+1)): ${concentraciones[i]}"
done

# Añadir quinta muestra
concentraciones+=("150 ng/ul")
echo "Nueva muestra añadida: ${concentraciones[-1]}"
```

### 🧪 Ejemplo 2: Procesamiento de muestras
```bash
#!/bin/bash
# Crear estructura de directorios para experimento
echo "Creando estructura para experimento de PCR..."

for muestra in {1..10}
do
    mkdir -p "experimento_PCR/muestra_$muestra"
    echo "Directorio para muestra $muestra creado"
done

echo "Estructura de directorios completada"
```

### 📊 Ejemplo 3: Análisis de archivos FASTA
```bash
#!/bin/bash
# Simular análisis de archivos de secuencias
archivos_fasta=("secuencia1.fasta" "secuencia2.fasta" "secuencia3.fasta")

for archivo in ${archivos_fasta[@]}
do
    echo "Procesando $archivo..."
    echo "  - Verificando formato"
    echo "  - Contando secuencias"
    echo "  - Calculando estadísticas"
    echo "  ✅ $archivo procesado correctamente"
    echo ""
done
```

---

## 🎬 Actividad Asincrónica - MISIÓN IMPOSIBLE: OPERACIÓN BIOINFORMÁTICA

```
🎵 *Música de Misión Imposible sonando de fondo* 🎵
```

---

### 📼 MENSAJE SECRETO

```
Buenos días, Agente [TU NOMBRE].

Tu misión, si decides aceptarla, consiste en dominar las técnicas
avanzadas de manipulación de datos biológicos usando Arrays y Bucles
en Shell Scripting.

Un laboratorio rival ha comprometido nuestros sistemas de análisis
genómico y solo TÚ puedes restaurar la funcionalidad usando tus
nuevas habilidades con listas y automatización.

Este mensaje se autodestruirá en 10 segundos... 💥

Buena suerte, Agente.
```

---

### 🎯 BRIEFING DE LA MISIÓN

#### 📋 **INFORMACIÓN CLASIFICADA:**
- **Código de Operación:** ARRAY-LOOP-007
- **Nivel de Amenaza:** 🔴 CRÍTICO
- **Tiempo límite:** 7 días
- **Equipo requerido:** Terminal Linux/Mac o WSL en Windows
- **Armas secretas:** Arrays, bucles FOR, y automatización

#### 🕵️ **TU IDENTIDAD ENCUBIERTA:**
- **Nombre en clave:** Agente Automatizador
- **Especialidad:** Manipulación masiva de datos genómicos
- **Misión:** Restaurar los sistemas de análisis automático

---

### 🚨 MISIONES A COMPLETAR

#### 🧬 **MISIÓN 1: OPERACIÓN "DNA QUANTIFICATION RESCUE"**
**📍 Localización:** Laboratorio de Cuantificación

El villano Dr. Chaos ha mezclado los valores de cuantificación de ADN. Debes crear un sistema que identifique automáticamente los valores críticos.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision1_cuantificacion.sh`
2. Usar este array de valores comprometidos:
   ```bash
   valores=("26 ng/ul" "70 ng/ul" "80 ng/ul" "35 ng/ul")
   ```
3. Tu script debe:
   - Mostrar todos los valores usando un bucle
   - Identificar cuál es el menor valor (pista: extraer solo números)
   - Identificar cuál es el mayor valor
   - Añadir un quinto valor: "150 ng/ul"
   - Mostrar un resumen final con el mensaje: "Análisis completado. Sistema restaurado."

##### 📝 **Código de ejemplo para empezar:**
```bash
#!/bin/bash
# MISIÓN IMPOSIBLE - OPERACIÓN DNA QUANTIFICATION RESCUE
# Agente: [TU NOMBRE]
# Fecha: [FECHA ACTUAL]

echo "🧬 ACCESO CONCEDIDO - INICIANDO ANÁLISIS GENÓMICO"
echo "================================================="
echo "🔬 PROCESANDO VALORES DE CUANTIFICACIÓN..."

# Tu código aquí...
```

---

#### 🏗️ **MISIÓN 2: OPERACIÓN "AUTO DIRECTORY CREATOR"**
**📍 Localización:** Centro de Gestión de Archivos

Dr. Chaos ha borrado toda la estructura de directorios del laboratorio. Debes recrear automáticamente 100 directorios para muestras.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision2_directorios.sh`
2. Tu script debe:
   - Crear automáticamente 100 archivos .txt usando `touch`
   - Los archivos deben llamarse: `muestra_001.txt`, `muestra_002.txt`, etc.
   - Mostrar un contador del progreso cada 10 archivos
   - Al final, mostrar cuántos archivos se crearon en total
   - **BONUS:** Después de crearlos, ¡borrarlos todos automáticamente!

##### 🎪 **Diálogo dramático requerido:**
```bash
echo "📁 INICIANDO PROTOCOLO DE RECREACIÓN..."
echo "🔄 Generando estructura de directorios..."
echo "📊 Progreso: $contador/100 archivos creados"
echo "✅ MISIÓN COMPLETADA - ESTRUCTURA RESTAURADA"
```

---

#### 🔬 **MISIÓN 3: OPERACIÓN "GENETIC SEQUENCE ANALYZER"**
**📍 Localización:** Departamento de Análisis de Secuencias

El villano ha encriptado información sobre secuencias genéticas. Debes crear un sistema que analice automáticamente las propiedades de cada secuencia.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision3_secuencias.sh`
2. Usar este array de secuencias comprometidas:
   ```bash
   secuencias=("ATCGATCG" "GCTAGCTA" "AAAATTTT" "CCCCGGGG" "ATCGATCGATCG")
   ```
3. Tu script debe usar bucles para:
   - Mostrar cada secuencia con su número de posición
   - Calcular y mostrar la longitud de cada secuencia
   - Contar cuántas secuencias tienen más de 8 nucleótidos
   - Identificar la secuencia más larga
   - Crear un reporte final con estadísticas

##### 🎭 **Elemento dramático:**
```bash
echo "🧬 DESENCRIPTANDO SECUENCIAS GENÉTICAS..."
echo "📊 Analizando secuencia $i de ${#secuencias[@]}"
echo "🔬 ANÁLISIS GENÓMICO COMPLETADO EXITOSAMENTE"
```

---

#### 🚀 **MISIÓN 4 (BONUS): OPERACIÓN "CHROMOSOME MAPPER"**
**📍 Localización:** Laboratorio de Citogenética

Para agentes elite solamente. Crea un sistema que simule el análisis de todos los cromosomas humanos.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision4_cromosomas.sh`
2. Tu script debe:
   - Crear un array con todos los cromosomas humanos: chr1, chr2, ..., chr22, chrX, chrY
   - Usar un bucle para simular el "análisis" de cada cromosoma
   - Mostrar un tiempo aleatorio de procesamiento para cada uno (usando `sleep`)
   - Crear un reporte final con el total de cromosomas analizados

---

### 📋 INFORME DE MISIÓN (ENTREGABLE)

#### 📝 **Debes entregar:**

1. **📁 Carpeta con tus scripts:**
   - `mision1_cuantificacion.sh`
   - `mision2_directorios.sh`
   - `mision3_secuencias.sh`
   - `mision4_cromosomas.sh` (opcional)

2. **📸 Capturas de pantalla mostrando:**
   - La ejecución de cada script
   - Los resultados obtenidos
   - El comando `ls -la` mostrando los permisos de ejecución

3. **📄 Reporte de agente (`informe_mision.txt`):**
   ```
   ================================
   INFORME DE MISIÓN CLASIFICADO
   ================================
   Agente: [TU NOMBRE]
   Fecha: [FECHA]
   Operación: ARRAY-LOOP-007

   MISIÓN 1 - STATUS: [COMPLETADA/FALLIDA]
   Arrays utilizados: [Describe qué arrays creaste]
   Bucles implementados: [Qué tipos de bucles usaste]
   
   MISIÓN 2 - STATUS: [COMPLETADA/FALLIDA]
   Archivos creados: [Cantidad total]
   Método de eliminación: [Cómo los borraste]
   
   MISIÓN 3 - STATUS: [COMPLETADA/FALLIDA]
   Secuencias analizadas: [Número total]
   Secuencia más larga: [Cuál fue y su longitud]

   MISIÓN 4 - STATUS: [COMPLETADA/FALLIDA/NO INTENTADA]
   Cromosomas procesados: [Total]

   TÉCNICAS APRENDIDAS:
   - [¿Qué aprendiste sobre arrays?]
   - [¿Qué descubriste sobre bucles FOR?]
   - [¿Cómo te ayudó la automatización?]

   DESAFÍOS ENFRENTADOS:
   - [¿Qué dificultades tuviste?]
   - [¿Cómo las resolviste?]

   REFLEXIÓN FINAL:
   - [¿Cómo aplicarás esto en bioinformática real?]
   - [¿Qué otras tareas podrías automatizar?]
   
   FIN DEL INFORME
   ================================
   ```

### 🏆 CRITERIOS DE EVALUACIÓN

- **Funcionalidad:** ¿Los scripts funcionan correctamente?
- **Uso de Arrays:** ¿Implementaste arrays de manera efectiva?
- **Bucles FOR:** ¿Usaste bucles para automatizar tareas?
- **Creatividad:** ¿Añadiste elementos únicos a tus scripts?
- **Documentación:** ¿Comentaste bien tu código?

---

## 📚 Referencias bibliográficas

- Blum, R., & Bresnahan, C. (2021). Linux command line and Shell scripting bible (Fourth edition). Wiley. Capítulo 11.

---

## 💡 Consejos para el Éxito

1. **Practica incrementalmente:** Empieza con arrays simples antes de crear bucles complejos
2. **Comenta tu código:** Explica qué hace cada sección
3. **Prueba paso a paso:** Ejecuta pequeñas partes antes de completar el script entero
4. **Usa `echo` para debug:** Imprime valores intermedios para verificar que todo funciona
5. **No tengas miedo de experimentar:** Los errores son parte del aprendizaje

**¡La automatización es el futuro de la bioinformática! 🚀🧬**
