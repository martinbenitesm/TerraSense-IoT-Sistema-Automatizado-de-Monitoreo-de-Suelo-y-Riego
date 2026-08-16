# TerraSense IoT: Sistema Automatizado de Monitoreo de Suelo y Riego para Agricultura de Precisión

**TerraSense IoT** es una solución integral diseñada para optimizar el uso del recurso hídrico en el sector agrónomo mediante un ecosistema de **Agricultura de Precisión**. El sistema permite el monitoreo en tiempo real de variables climatológicas y edafológicas (humedad del suelo y temperatura ambiental) para automatizar el riego de forma inteligente, reduciendo el desperdicio de agua y maximizando la rentabilidad del cultivo.

## 🚀 Características Principales

- **Arquitectura de 4 Capas:** Estructura robusta dividida en Percepción, Red (Transporte), Procesamiento (Nube) y Aplicación.
- **Edge Computing:** Toma de decisiones autónoma en el borde (MCU ESP32) para activar el riego con latencia mínima y sin dependencia total de Internet.
- **Protocolo MQTT 5.0:** Comunicación ligera y eficiente mediante un modelo de Publicación/Suscripción, optimizando el ancho de banda y el consumo energético.
- **Topología en Estrella:** Diseño de red que garantiza el aislamiento de fallos y una alta eficiencia energética mediante dispositivos que operan de forma independiente hacia un Gateway central.
- **Seguridad Multicapa:** Blindaje de datos basado en los 4 pilares de la ciberseguridad: Confidencialidad, Control de Acceso, Autenticación e Integridad.

## 🏗️ Arquitectura del Sistema

El flujo de datos se distribuye de la siguiente manera:

1. **Capa de Percepción (Edge):** Nodos con sensores de humedad y temperatura junto a electroválvulas de riego.
2. **Capa de Red (Fog):** Enlaces inalámbricos (Wi-Fi/LoRa) y un Gateway AgroIoT que centraliza la telemetría.
3. **Capa de Procesamiento (Cloud):** Servidores IoT para análisis de datos masivos y modelos predictivos.
4. **Capa de Aplicación:** Dashboard web y móvil para la supervisión y control remoto del agricultor.

## 🛠️ Stack Tecnológico

- **Hardware:** Microcontroladores **ESP32** (o equivalentes arquitectónicos), sensores de humedad de suelo, sondas de temperatura P-N y aspersores (actuadores).
- **Protocolos:** MQTT 5.0 (Troncal), LoRaWAN (Campo), HTTPS/TLS (Nube) y Wi-Fi (Simulación).
- **Simulación:** Cisco Packet Tracer v9.
- **Lenguajes:** JavaScript (Lógica de control de borde).

## 💻 Lógica de Control (Edge Scripting)

El sistema opera bajo un algoritmo de decisión autónomo inyectado en el firmware del MCU. El riego se activa automáticamente si la humedad del suelo cae por debajo del **umbral crítico del 10%** (400 unidades en el ADC):

```javascript
// Fragmento de la lógica principal
if (lecturaHumedad < umbralSequedad) {
    // El suelo está seco: se activa el riego
    digitalWrite(pinAspersor, HIGH);
    Serial.println("-> Alerta: Suelo seco. Aspersor ENCENDIDO.");
} else {
    // Humedad óptima: conservación de recursos
    digitalWrite(pinAspersor, LOW);
    Serial.println("-> Estado: Humedad óptima. Aspersor APAGADO.");
}
```
## 🔒 Ciberseguridad

El sistema implementa medidas de protección avanzadas para garantizar la integridad de la producción agrícola:

- **Cifrado de grado bancario (AES-256)** para datos en reposo y en tránsito. 
- **Autenticación robusta** mediante tokens de identidad única por cada placa ESP32. 
- **Firmas digitales** para actualizaciones de firmware vía OTA (Over The Air). 
- **Listas de Control de Acceso (ACL)** estrictas en el bróker MQTT. 

## 👨‍💻 Autor

- **Benites Marin Martin Alberto** - *Desarrollo y Diseño Arquitectónico*. 

*Este proyecto fue desarrollado bajo la supervisión del Prof. Wilmer Berrospi Taquire en el curso de Internet de las Cosas (2026) en la Universidad Nacional de Ingeniería.*
