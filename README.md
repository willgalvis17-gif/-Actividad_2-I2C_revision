# -Actividad_2-I2C_revision
Análisis del protocolo I2C utilizando una Raspberry Pi Pico, MicroPython y una pantalla OLED SSD1306. El proyecto incluye reconocimiento de tramas con analizador lógico, pruebas ACK/NACK, escaneo de direcciones I2C y análisis de comandos enviados al controlador SSD1306.
# Análisis de Tramas I2C con Raspberry Pi Pico y OLED SSD1306

Proyecto de laboratorio enfocado en el análisis y reconocimiento de tramas del protocolo **I2C (Inter-Integrated Circuit)** utilizando una **Raspberry Pi Pico**, una pantalla **OLED SSD1306**, **MicroPython** y un analizador lógico mediante **Logic 2**.

El objetivo principal es relacionar el funcionamiento del código con las señales eléctricas presentes en las líneas **SCL** y **SDA**, identificando los diferentes elementos que componen una comunicación I2C.

## Objetivos

- Identificar la estructura de una trama I2C.
- Reconocer las condiciones de **Start** y **Stop**.
- Analizar el byte de dirección y el bit **R/W**.
- Diferenciar respuestas **ACK** y **NACK**.
- Detectar dispositivos conectados utilizando `i2c.scan()`.
- Analizar comandos enviados a una pantalla OLED SSD1306.
- Medir la frecuencia real de la señal SCL mediante un analizador lógico.

## Hardware utilizado

- Raspberry Pi Pico
- Pantalla OLED SSD1306
- Analizador lógico
- Resistencias pull-up para SDA y SCL
- Protoboard
- Cables de conexión

## Software utilizado

- MicroPython
- Thonny IDE
- Logic 2
- Decodificador I2C de Logic 2

## Protocolo I2C

I2C utiliza dos líneas principales:

- **SCL (Serial Clock):** señal de reloj generada por el maestro.
- **SDA (Serial Data):** línea utilizada para transmitir los datos.

Cada transacción contiene normalmente:

1. Condición **Start**
2. Dirección del dispositivo de 7 bits
3. Bit **R/W**
4. Bit de reconocimiento **ACK/NACK**
5. Datos
6. Condición **Stop**

## Conexión utilizada

Para las principales pruebas se utilizó el bus `I2C1` de la Raspberry Pi Pico:

| Señal | GPIO |
|------|------|
| SCL | GP15 |
| SDA | GP14 |

Ejemplo de configuración:

```python
import machine

i2c = machine.I2C(
    1,
    scl=machine.Pin(15),
    sda=machine.Pin(14),
    freq=100000
)
