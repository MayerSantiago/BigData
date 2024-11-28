# Informe de Pruebas y Resultados del Modelo MNIST

Este documento resume las pruebas realizadas y analiza las razones por las cuales el modelo no ha logrado superar el 90% de precisión en los datos de validación y prueba. Además, se incluyen hipótesis sobre los posibles problemas y propuestas de mejora.

---

## **1. Pruebas Realizadas**

### **1.1 Entrenamiento con Validación**
- **Configuración**:
  - Datos de validación: 10,000 imágenes de prueba (MNIST).
  - Épocas: 5.
  - Optimizador: `adam`.
  - Tamaño del lote: 32.
- **Resultados**:
  - Precisión en entrenamiento: ~88%.
  - Precisión en validación: ~87%.
- **Observación**:
  - La precisión mejora inicialmente, pero se estanca alrededor del 87%.

### **1.2 Entrenamiento sin Validación**
- **Configuración**:
  - Sin uso de `validationData`.
  - Evaluación final con `data.testX` y `data.testY` usando `model.evaluate`.
- **Resultados**:
  - Precisión en entrenamiento: ~89%.
  - Precisión en pruebas: ~88%.
- **Observación**:
  - El rendimiento del modelo sigue limitado en datos de prueba.

### **1.3 Ajuste de Hiperparámetros**
- **Cambios**:
  - Incremento de épocas: 5 → 20.
  - Optimizador: Cambio de `sgd` a `adam`.
  - Tamaño del lote: 32 → 16.
- **Resultados**:
  - Precisión en entrenamiento: ~89%.
  - Precisión en validación/prueba: ~88%.
- **Observación**:
  - Más épocas no mejoran significativamente la precisión.
  - Tamaños de lote más pequeños aumentan fluctuaciones, pero no generalización.

### **1.4 Cambios en la Arquitectura del Modelo**
- **Cambios**:
  - Filtros en capas convolucionales: 6 → 32.
  - Función de activación: `tanh` → `relu`.
  - Regularización: Se añadió `dropout` con `rate: 0.5`.
- **Resultados**:
  - Precisión en entrenamiento: ~90%.
  - Precisión en validación/prueba: ~89%.
- **Observación**:
  - Cambios arquitectónicos mejoran ligeramente los resultados, pero no logran superar el 90%.

### **1.5 Preprocesamiento de Datos**
- **Cambios**:
  - Normalización: De [0, 1] → [-1, 1].
  - Aumento de datos: Rotación, traslación, escalado.
- **Resultados**:
  - Precisión en entrenamiento: ~90%.
  - Precisión en validación/prueba: ~88%.
- **Observación**:
  - El aumento de datos no mejora significativamente los resultados.

---

## **2. Hipótesis sobre el Estancamiento**

1. **Complejidad del Modelo**:
   - El modelo podría ser demasiado simple para capturar todas las características de las imágenes MNIST.

2. **Cantidad de Datos**:
   - Aunque MNIST tiene 60,000 imágenes de entrenamiento, puede no ser suficiente para un modelo más complejo.

3. **Sobreajuste y Generalización**:
   - La precisión alta en entrenamiento (~90%) pero baja en validación (~88%) indica un posible sobreajuste.

4. **Representación de Características**:
   - La arquitectura puede no estar capturando características relevantes.

5. **Hiperparámetros Subóptimos**:
   - Tasas de aprendizaje y tamaños de batch podrían no ser ideales.

6. **Limitación del Dataset MNIST**:
   - MNIST es un conjunto de datos clásico y relativamente fácil. Las mejoras más allá del 90% suelen requerir arquitecturas avanzadas.

7. **Errores en el Preprocesamiento**:
   - Algunos datos podrían no estar bien procesados desde el sprite.

---

## **3. Propuestas de Mejora**

### **3.1 Arquitectura del Modelo**
- Probar modelos más complejos:
  - Redes convolucionales profundas como ResNet o MobileNet.

### **3.2 Transfer Learning**
- Usar un modelo preentrenado:
  - MobileNet o EfficientNet como base para extracción de características.

### **3.3 Optimización Avanzada**
- Implementar estrategias como:
  - Decay dinámico del learning rate.
  - Optimizadores avanzados como AdamW.

### **3.4 Aumento Extremo de Datos**
- Generar más datos artificialmente:
  - Deformaciones no lineales.
  - Inversiones parciales.

### **3.5 Uso de Conjuntos Modernos**
- Probar datasets como:
  - Fashion-MNIST.
  - CIFAR-10.

---

## **4. Conclusión**

El estancamiento en ~89% se debe probablemente a una combinación de:
1. Arquitectura insuficientemente compleja.
2. Limitaciones del dataset MNIST.
3. Regularización y optimización subóptimas.

---
