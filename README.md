# 🧠 AI Handwritten Equation Recognition

Sistema de reconocimiento de ecuaciones matemáticas a partir de imágenes, utilizando visión por computadora y modelos secuenciales avanzados.
El proyecto evolucionó desde un enfoque clásico CNN + RNN hacia una arquitectura moderna tipo encoder–decoder con mecanismos de atención.

---

## 📌 Descripción

Este proyecto tiene como objetivo convertir imágenes de ecuaciones matemáticas (escritas a mano) en una representación textual estructurada (tokens / LaTeX).

Pipeline general:

```text
Imagen → CNN → Representación secuencial → Decoder → Tokens → Texto
```

---

## 🚀 Evolución del Proyecto

### 🔹 v1 — CNN + BiLSTM (Baseline)

**Arquitectura:**

* CNN con bloques residuales
* Transformación de imagen a secuencia
* Capas bidireccionales LSTM
* Clasificación con softmax

**Características:**

* Pipeline directo imagen → secuencia
* Entrenamiento con `sparse_categorical_crossentropy`
* Sin separación encoder–decoder
* Sin mecanismos de atención

**Limitaciones:**

* ❌ Predicciones inestables en secuencias largas
* ❌ Falta de alineación imagen–texto
* ❌ Sensible al padding (sin masking)
* ❌ Generación poco estructurada

---

### 🔹 v2 — Encoder–Decoder con Atención (Versión actual)

Se rediseñó completamente el modelo incorporando conceptos modernos de modelado secuencial.

---

#### 🧠 1. Arquitectura Encoder–Decoder

* Encoder: extrae características visuales desde la imagen
* Decoder: genera la secuencia de tokens

**Impacto:**

* Mejor modelado de dependencias secuenciales
* Separación clara de responsabilidades

---

#### 🎯 2. Teacher Forcing

```python
decoder_in = labels[:, :-1]
target     = labels[:, 1:]
```

**Impacto:**

* Entrenamiento más estable
* Convergencia más rápida

---

#### 🧮 3. Enmascaramiento de Padding

```python
mask = tf.cast(tf.not_equal(target, 0), tf.float32)
```

**Impacto:**

* Evita que el modelo aprenda ruido
* Métricas más representativas

---

#### 👁️ 4. Mecanismos de Atención

* Self-Attention (en decoder)
* Cross-Attention (imagen ↔ secuencia)

**Impacto:**

* Mejor alineación entre regiones de la imagen y tokens
* Mayor precisión en símbolos complejos

---

#### 🔄 5. Generación Autoregresiva

```python
greedy_decode(...)
```

**Antes:**

* Predicción paralela

**Ahora:**

* Generación token por token

**Impacto:**

* Salidas más coherentes
* Base para futuras mejoras (beam search)

---

#### 🧱 6. Mejora en Representación

* Proyección densa intermedia
* Normalización de capas

**Impacto:**

* Mayor estabilidad en entrenamiento
* Mejor generalización

---

#### 📏 7. Manejo de Secuencias Más Largas

* Eliminación de truncamiento rígido

**Impacto:**

* Soporte para ecuaciones más complejas

---

## 📊 Resultados

### Comparación general

| Aspecto                 | v1 (Baseline) | v2 (Actual) |
| ----------------------- | ------------- | ----------- |
| Coherencia secuencial   | Baja          | Alta        |
| Manejo de longitud      | Limitado      | Mejorado    |
| Alineación imagen-texto | Débil         | Fuerte      |
| Estabilidad             | Media         | Alta        |

---

## 🖼️ Ejemplos

### Ejemplo 1


**v1:**

<img width="989" height="202" alt="Captura de pantalla 2026-05-05 142459" src="https://github.com/user-attachments/assets/7b3e48d4-6ec4-43f5-8929-41d9141f5079" />


**v2:**

<img width="848" height="654" alt="Captura de pantalla 2026-05-05 142400" src="https://github.com/user-attachments/assets/f69d229e-85f1-45f0-8475-ffce8a45149a" />

---


## 📈 Entrenamiento

Incluye gráficas en:

* `<img width="691" height="475" alt="descarga (1)" src="https://github.com/user-attachments/assets/c45c80a0-8c64-4082-9767-ce7a6fde46f2" />

`
* `<img width="708" height="475" alt="descarga" src="https://github.com/user-attachments/assets/fa2bd223-8c72-44e9-9752-f478fd4967ec" />

`

Observaciones:

* Convergencia más estable en v2
* Menor sobreajuste
* Mejor desempeño en validación

---

## 🛠️ Tecnologías

* Python
* TensorFlow / Keras
* NumPy
* Matplotlib

---

## 🧪 Aprendizajes Clave

* Encoder–decoder mejora significativamente tareas secuenciales
* La atención es clave para alinear visión y lenguaje
* Teacher forcing acelera la convergencia
* El masking es crítico en modelos con padding

---

## 🔮 Trabajo Futuro

* Implementar beam search
* Migrar a arquitectura Transformer completa
* Data augmentation para imágenes
* Métricas más robustas (BLEU, edit distance)
* Conversión directa a LaTeX

---

## 👨‍💻 Autor

Gerardo Espinosa
Física + Inteligencia Artificial

---

## ⭐ Notas

Este proyecto forma parte de mi portafolio en IA aplicada, con enfoque en:

* Computer Vision
* Modelos secuenciales
* Aplicaciones en educación

---

