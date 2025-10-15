# ESP32 IoT Sensor - DHT22 & LDR com MQTT

Este projeto demonstra como usar um **ESP32** para monitorar temperatura, umidade e luminosidade, controlando um LED remotamente via **MQTT**. Os dados são enviados a um broker MQTT público e comandos podem ser recebidos para ligar/desligar o LED.

---

## 👥 Participantes do Grupo

- **Kazys Tatarunas** – RM: 564020  
- **Eduardo Viudes** – RM: 564075  
- **Frederico de Paula** – RM: 562109 
- **Victor Tadashi** – RM: 563582  

---

## 📦 Componentes necessários

- ESP32
- Sensor DHT22 (Temperatura e Umidade)
- Sensor LDR (Luminosidade)
- LED + resistor (220Ω)
- Jumpers / Protoboard

---

## 🔌 Conexões

| Componente | ESP32 |
|------------|-------|
| DHT22 Data | GPIO 15 |
| LDR        | GPIO 34 (ADC) |
| LED        | GPIO 2  |
| GND        | GND    |
| VCC        | 3.3V/5V|

> Observação: ajuste os pinos no código se necessário.

---

## ⚙️ Configuração de rede e MQTT

No arquivo `main.ino`:

```cpp
const char* WIFI_SSID = "Wokwi-GUEST";
const char* WIFI_PASS = "";
const char* MQTT_BROKER = "broker.hivemq.com";
const int MQTT_PORT = 1883;

const char* TOPIC_SUB = "viudes1407/cmd";
const char* TOPIC_PUB = "viudes1407/attrs";
const char* CLIENT_ID = "ESP32_Viudes1407";
```
TOPIC_SUB: tópico onde o ESP32 recebe comandos (ON / OFF).

TOPIC_PUB: tópico onde o ESP32 publica os dados do sensor.

💻 Funcionalidades

Monitoramento de sensores:

Temperatura (°C)

Umidade (%)

Nível de luminosidade (%)

Controle de LED via MQTT

Comando ON → LED acende

Comando OFF → LED apaga

Publicação periódica de dados

A cada 4 segundos

Formato JSON enviado pelo ESP32:

{
  "temp": 25.4,
  "umid": 60.2,
  "lum": 75
}

🚀 Como usar

Conecte o ESP32 à sua rede Wi-Fi.

Certifique-se de que o broker MQTT está acessível (ex.: HiveMQ Broker
).

Abra o monitor serial para ver logs e dados enviados.

Envie mensagens para o tópico viudes1407/cmd para controlar o LED:

ON → acende

OFF → apaga

📄 Bibliotecas utilizadas

WiFi.h
 - Conexão Wi-Fi

PubSubClient
 - Cliente MQTT

DHT.h
 - Sensor DHT22

💡 Dicas

Se usar outro broker MQTT, altere MQTT_BROKER e MQTT_PORT.

Ajuste os pinos se necessário, dependendo do seu hardware.

Pode-se integrar com plataformas IoT, como Node-RED, Home Assistant ou Grafana, para visualizar os dados.
