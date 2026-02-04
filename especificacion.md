# Especificación: app móvil para lectura de matrícula y registro de trayectos (Comunidad de Madrid)

## Objetivo
Crear una aplicación móvil que permita **leer la matrícula** de un coche y capturar datos operativos del trayecto. La app debe **guardar los datos en el dispositivo** y permitir **enviar un reporte como captura de pantalla**.

## Alcance funcional
### 1) Lectura de matrícula
- Captura mediante cámara con OCR/ANPR (reconocimiento automático de matrículas).
- Alternativa manual si el OCR falla.
- Validación de formato de matrícula española (ej.: 0000-XXX).

### 2) Registro de datos operativos
- **Oficina de recogida** (lista/selector + texto libre).
- **Oficina de entrega** (lista/selector + texto libre).
- **Kilometraje inicial** (número entero, obligatorio).
- **Kilometraje final** (número entero, obligatorio; debe ser ≥ al inicial).
- **Combustible inicial** (porcentaje o nivel 0–8 barras).
- **Combustible final** (porcentaje o nivel 0–8 barras).

### 3) Registro del recorrido (A → B) y tiempo medio
- Origen (A) y destino (B) con autocompletado de direcciones en la **Comunidad de Madrid**.
- Cálculo de distancia y **tiempo medio** basado en una ruta sugerida.
- Vista resumen del trayecto (distancia, tiempo estimado).

### 4) Evidencia y envío
- Generación de un **resumen en pantalla** con todos los datos.
- Opción de **exportar como captura de pantalla** (o PDF generado a partir de la vista).
- Compartir vía apps del sistema (WhatsApp, correo, etc.).

### 5) Almacenamiento local
- Guardado **offline** en el dispositivo (SQLite o almacenamiento interno).
- Historial de registros con búsqueda por matrícula/fecha.
- Opción de exportar en CSV desde el historial.

## Flujo de usuario propuesto
1. **Inicio** → botón “Nuevo registro”.
2. **Escaneo de matrícula** → OCR/ANPR + validación. Alternativa: “Ingresar manualmente”.
3. **Datos operativos** → oficinas, kilómetros, combustible.
4. **Trayecto A → B** → selección de direcciones en Madrid, cálculo de distancia/tiempo medio.
5. **Resumen** → confirmar y guardar.
6. **Compartir** → generar captura de pantalla y enviar.

## Requisitos no funcionales
- **Offline-first** (sin conexión obligatoria).
- **Privacidad**: datos sólo en el dispositivo salvo acción explícita de compartir.
- **Compatibilidad**: Android (prioritario) y iOS (deseable).

## Propuesta técnica (opcional)
- **Frontend móvil**: Flutter o React Native.
- **OCR/ANPR**: ML Kit (Android/iOS) o librerías ANPR.
- **Mapas/Rutas**: Mapbox/Google Maps con restricción a Comunidad de Madrid.
- **Persistencia**: SQLite + almacenamiento seguro para adjuntos.

## Modelo de datos (borrador)
- `registro_id`
- `matricula`
- `oficina_recogida`
- `oficina_entrega`
- `km_inicial`
- `km_final`
- `combustible_inicial`
- `combustible_final`
- `origen_A`
- `destino_B`
- `distancia_km`
- `tiempo_medio_min`
- `fecha_hora`
- `captura_path` (opcional)
