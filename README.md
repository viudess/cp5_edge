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
- TOPIC_SUB: tópico onde o ESP32 recebe comandos (ON / OFF).
- TOPIC_PUB: tópico onde o ESP32 publica os dados do sensor.

---

## 💻 Funcionalidades
1. Monitoramento de sensores:
- Temperatura (°C)
- Umidade (%)
- Nível de luminosidade (%)
2. Controle de LED via MQTT
- Comando ON → LED acende
- Comando OFF → LED apaga
3. Publicação periódica de dados
- A cada 4 segundos

Formato JSON enviado pelo ESP32:
```json
{
  "temp": 25.4,
  "umid": 60.2,
  "lum": 75
}
```

---

## 🚀 Como Usar

Para interagir com o projeto, acesse a simulação no Wokwi através do link abaixo. A plataforma permite que você execute o código e interaja com o ESP32 virtualmente, sem a necessidade de hardware físico.

[**Acessar o Projeto no Wokwi**](https://wokwi.com/projects/444915840852511745)

### Passos para Operação

1.  **Conecte o ESP32 à sua rede Wi-Fi:** No ambiente Wokwi, o ESP32 irá se conectar automaticamente à rede Wi-Fi virtual configurada no código. Se estiver usando um ESP32 físico, certifique-se de inserir as credenciais da sua rede no código-fonte.

2.  **Acessibilidade do Broker MQTT:** O projeto está configurado para usar um broker MQTT público (como o HiveMQ Broker). A conexão será estabelecida automaticamente.

3.  **Monitore a Saída:** Abra o "Serial Monitor" na simulação do Wokwi para visualizar os logs de conexão e os dados que estão sendo enviados e recebidos pelo ESP32.

4.  **Controle o LED:** Para controlar o LED, você precisará de um cliente MQTT (pode ser um aplicativo de celular, um software para desktop ou uma interface web como a do [HiveMQ](https://www.hivemq.com/demos/websocket-client/)) para publicar mensagens no tópico `viudes1407/cmd`.
    * Envie a mensagem `ON` para acender o LED.
    * Envie a mensagem `OFF` para apagar o LED.

## Diagrama do ESP32

A imagem abaixo ilustra a pinagem de um ESP32 genérico, semelhante ao utilizado no projeto. O LED integrado geralmente está conectado ao pino `GPIO 2`.

![ESP32 Pinout](/images/esp32.png)

---

## 📄 Bibliotecas utilizadas

- WiFi.h - Conexão Wi-Fi
- PubSubClient - Cliente MQTT
- DHT.h - Sensor DHT22

---

## 💡 Dicas
- Se usar outro broker MQTT, altere MQTT_BROKER e MQTT_PORT.
- Ajuste os pinos se necessário, dependendo do seu hardware.
- Pode-se integrar com plataformas IoT, como Node-RED, Home Assistant ou Grafana, para visualizar os dados.
