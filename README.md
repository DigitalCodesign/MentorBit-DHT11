# MentorBitDHT11

Esta librería está diseñada para que puedas medir la temperatura y la humedad de tu entorno de una forma muy sencilla usando tu placa MentorBit y el módulo de sensor DHT11.

Si estás empezando en el mundo de la electrónica, ¡no te preocupes! MentorBit está pensado para que aprender sea fácil y divertido. Esta placa ya incluye un montón de componentes (LEDs, pulsadores, pantallas, etc.) y utiliza conectores especiales (JST) para que puedas añadir nuevos sensores y módulos sin tener que pelearte con un montón de cables. Pásate por nuestra web para saber más de MentorBit y nuestros productos [pinchando aquí](https://digitalcodesign.com/).

![Render del Módulo MentorBit de sensor DHT-11.](https://github.com/DigitalCodesign/MentorBit-DHT11/blob/main/assets/DHT-11_Module.png)

Con esta librería, podrás saber qué temperatura y humedad hay en una habitación y usar esa información para crear proyectos increíbles.

## Descripción
### ¿Qué es un sensor de temperatura y humedad?

Es como tener un pequeño hombre del tiempo digital. Un sensor DHT11 mide dos de las variables ambientales más comunes:

- **Temperatura:** El calor o frío que hace en el ambiente, medido en grados Celsius.
- **Humedad Relativa:** La cantidad de vapor de agua que hay en el aire, expresada en un porcentaje (%).

Saber estos dos datos es fundamental para proyectos de control climático, estaciones meteorológicas o simplemente para conocer las condiciones de una habitación.

### ¿Qué hace esta librería?

La librería MentorBitDHT11 actúa como un "traductor" entre el sensor DHT11 y tu placa MentorBit. Se encarga de toda la comunicación y los cálculos complejos para que tú solo tengas que usar un par de comandos sencillos para obtener las mediciones.

Gracias a ella, podrás centrarte en lo más importante: ¡la creatividad de tu proyecto!

### ¿Qué puedes construir con este sensor?

- Una estación meteorológica casera que muestre los datos en una pantalla.
- Un sistema de ventilación inteligente que encienda un ventilador si la temperatura sube mucho.
- Un controlador para una incubadora o un terrario, manteniendo la temperatura y humedad constantes.
- Una alarma que te avise si la humedad en una habitación es demasiado alta para prevenir moho.

Esta librería es el primer paso para integrar la monitorización de temperatura y humedad ambiente en tus proyectos con MentorBit de una manera sencilla y profesional.

## Cómo empezar

Usar la librería es muy sencillo. Solo sigue estos pasos para tener tu sensor midiendo luz en pocos minutos.

1. **Conexión del Módulo**

Antes que nada, conecta tu módulo de sensor DHT11 a uno de los puertos **Digitales de Entrada/Salida** dentro de la zona de **Puertos para Módulos** en tu placa MentorBit. ¡Y listo! No necesitas más cables.

2. **Instalación de las Librerías**

Para que tu placa MentorBit pueda comunicarse con el sensor, solo necesitas instalar una librería. El gestor del IDE de Arduino se encargará del resto.

- Abre tu entorno de programación IDE de Arduino.
- Ve al menú *Programa -> Incluir Librería -> Administrar Librerías...*
- En el buscador, escribe ***MentorBitDHT11*** y haz clic en "Instalar".
- El IDE detectará que esta librería necesita otra para funcionar y te preguntará si quieres instalarla también. Haz clic en "Install all" o "Instalar todo".

![Ejemplo de búsqueda en el gestor de librerías del IDE de Arduino.](https://github.com/DigitalCodesign/MentorBit-DHT11/blob/main/assets/library_instalation_example.png)

¡Y ya está! Con eso tienes todo lo necesario para empezar a programar.

## Ejemplo Básico: Leer Temperatura y Humedad

El siguiente código es todo lo que necesitas para tomar una lectura cada dos segundos y mostrarla en tu ordenador.

### Copia y pega este código en tu IDE:

```c++
// 1. Incluimos la librería que acabamos de instalar.
#include <MentorBitDHT11.h>

// Definimos el pin digital al que hemos conectado el módulo.
#define DHT_PIN 2

// 2. Creamos un objeto 'miSensor' y le indicamos el pin que vamos a usar.
MentorBitDHT11 miSensor(DHT_PIN);

void setup() {
    // Inicializamos la comunicación con el ordenador para poder ver los mensajes.
    Serial.begin(9600);
    Serial.println("Sensor DHT11 listo para medir.");
}

void loop() {
    // El sensor DHT11 necesita al menos 2 segundos entre lecturas.
    delay(2000);

    // 3. Usamos las funciones para obtener las medidas.
    float humedad = miSensor.obtenerHumedad();
    float temperatura = miSensor.obtenerTemperatura();

    // 4. Comprobamos si la lectura ha sido exitosa.
    // A veces, el sensor puede fallar. isnan() comprueba si el valor no es un número.
    if (isnan(humedad) || isnan(temperatura)) {
        Serial.println("Error al leer del sensor DHT11");
        return;
    }

    // 5. Mostramos el resultado en el monitor serie.
    Serial.print("Humedad: ");
    Serial.print(humedad);
    Serial.print("%\t"); // \t es un tabulador para separar
    Serial.print("Temperatura: ");
    Serial.print(temperatura);
    Serial.println(" *C");
}
```
### Para ver el resultado:

1. Carga el código en tu placa MentorBit.
2. Abre el **Monitor Serie** del IDE de Arduino.
3. ¡Verás cómo aparecen las lecturas de luz cada segundo!

## Funciones Principales
Esta librería está diseñada para ser minimalista y fácil de usar. Solo necesitas conocer estas dos funciones:

- <code>MentorBitDHT11(uint8_t pin)</code>
   - **¿Qué hace?** Es el **constructor**. Crea el objeto que te permitirá controlar el sensor. Debes indicarle a qué pin digital de tu MentorBit has conectado el módulo.
   - **¿Cuándo se usa?** Al principio de tu código, antes del <code>setup()</code>, para declarar tu sensor.

- <code>float obtenerTemperatura()</code>
   - **¿Qué hace?** Le pide al sensor la temperatura ambiente y te la devuelve como un número decimal (de tipo <code>float</code>) en grados **Celsius**.
   - **¿Cuándo se usa?** La llamarás cada vez que quieras saber la temperatura, normalmente dentro de la función <code>loop()</code>.

## Recursos Adicionales

¿Quieres saber más sobre el módulo o necesitas comprar uno? Aquí tienes algunos enlaces que te serán de utilidad:

- [Web del fabricante](https://digitalcodesign.com/)
- [Tienda Online de Canarias](https://canarias.digitalcodesign.com/shop)
- [Tienda Online de Península](https://digitalcodesign.com/shop)
- [Web Oficial de MentorBit](https://digitalcodesign.com/mentorbit)
- [Web Oficial de MentorBit módulo de sensor DHT11](https://canarias.digitalcodesign.com/shop/00038829-mentorbit-modulo-de-sensor-dht11-8113)
- [Manual de usuario del MentorBit módulo de sensor DHT11](https://drive.google.com/file/d/1JxGucdgucjq6HDoMvd1QhYJZOeibbZIc/view?usp=drive_link)
- [Modelo 3D de MentorBit módulo de sensor DHT11 en formato .STEP](https://drive.google.com/file/d/1buEb29byPb-vlC7KWfUNIZiYcOM9mS6O/view?usp=drive_link)
