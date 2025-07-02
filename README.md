
# Sistema de Pesaje Automatizado para Raspberry Pi

Este proyecto permite controlar hasta **4 básculas electrónicas**, cada una con su **electroválvula**, usando una **Raspberry Pi 1 Modelo B**. Cuenta con:

- Interfaz gráfica en Tkinter.
- Control de salidas oscilantes.
- Sensor de tolva para presencia de producto.
- Calibración individual de básculas.
- Gestión de recetas desde base de datos SQLite.
- Registro de verificaciones en `.log`.

---

## ⚙️ Requisitos

- Raspberry Pi 1 Modelo B (u otra con GPIO).
- MCP3008 (conversor ADC SPI).
- Celdas de carga con amplificador analógico.
- Electroválvulas (controladas vía relés o drivers).
- Sensor de nivel en tolva (ej: inductivo, infrarrojo).
- Resistencias, cables Dupont, fuente 5V.

---

## 🔌 Diagrama de Conexiones

![Diagrama de Conexiones](diagrama_conexiones_rpi.png)



- MCP3008:
  - VDD ↔ 3.3V
  - VREF ↔ 3.3V
  - AGND ↔ GND
  - CLK ↔ GPIO11 (SCLK)
  - DOUT ↔ GPIO9 (MISO)
  - DIN ↔ GPIO10 (MOSI)
  - CS ↔ GPIO8 (CE0)
  - CH0–CH3 ↔ Salidas analógicas de amplificadores de las 4 básculas

- Electroválvulas:
  - GPIO17, GPIO27, GPIO22, GPIO23 ↔ Relé 1-4

- Osciladores (vibradores):
  - GPIO5, GPIO6, GPIO13, GPIO19 ↔ Relé vibrador 1-4

- Sensor Tolva:
  - GPIO26 ↔ Salida digital del sensor

---

## 🧪 Modo Manual y Calibración

- Se accede desde la pestaña **“Manual”**.
- Opción para calibrar con **200g o 1000g**.
- Verificación visual de error y registro en `verificaciones.log`.

---

## 📦 Recetas

- Configura:
  - Peso objetivo por balanza.
  - Tiempos ON/OFF para vibradores.
  - Retardos para válvulas.
- Guarda, edita, elimina o aplica recetas desde la pestaña **“Recetas”**.

---

## 🧰 Instalación

1. En Raspberry Pi OS:
```bash
sudo apt-get update
sudo apt-get install python3-tk sqlite3
pip3 install RPi.GPIO spidev
```

2. Conecta el hardware como en el esquema.

3. Ejecuta:
```bash
python3 main.py
```

---

## 📁 Archivos del proyecto

- `main.py`: Interfaz principal.
- `adc_reader.py`: Lectura de celdas de carga.
- `valve_control.py`: Control de electroválvulas.
- `oscillator_control.py`: Salidas ON/OFF configurables.
- `sensor_tolva.py`: Control de sensor superior.
- `manual_control.py`: Modo manual/calibración.
- `config_loader.py`: Configuración y persistencia.
- `recetas.db`: Base de datos de recetas.
- `verificaciones.log`: Registro de calibraciones y verificaciones.

---

## 📷 Interfaz

- Pantalla principal con lectura de peso por balanza.
- Indicadores y botones grandes estilo industrial.
- Todo en español y táctil amigable.

---

## 🛠️ Créditos

Desarrollado por [twfsapack](https://github.com/twfsapack) con soporte para sistemas embebidos industriales.
