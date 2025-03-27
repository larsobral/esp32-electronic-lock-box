### 📟 Teste do Display OLED 0.96" I2C SSD1306 com ESP32

#### ✅ Objetivo
Realizar a conexão física e o teste de funcionamento do display OLED com o ESP32, exibindo a mensagem `"Display funcionando!"`.

---

### 🧱 Materiais Utilizados
- ESP32 DevKitC (CP2102 - USB-C)
- Display OLED 0.96" I2C (SSD1306)
- Cabos jumper macho-fêmea
- Protoboard
- Arduino IDE

---

### ⚙️ Esquema de Conexão

| Pino no Display | Função       | Conectar no ESP32 | Identificação na sua placa |
|-----------------|--------------|-------------------|-----------------------------|
| GND             | Terra        | GND               | Pino com etiqueta `GND`     |
| VCC             | Alimentação  | 3V3               | Pino com etiqueta `3V3`     |
| SCL             | Clock I2C    | GPIO 22           | Pino com etiqueta `P22`     |
| SDA             | Dados I2C    | GPIO 21           | Pino com etiqueta `P21`     |

---

### 🧪 Passo a Passo

#### 1. **Soldar os pinos do display**
- O display veio sem os pinos soldados.
- Foi necessário soldar os 4 pinos (GND, VCC, SCL, SDA) antes da conexão com o ESP32.

#### 2. **Instalar as bibliotecas na Arduino IDE**
- Acesse `Sketch > Include Library > Manage Libraries`
- Busque e instale as bibliotecas:
  - `Adafruit SSD1306`
  - `Adafruit GFX`

#### 3. **Código utilizado**

```cpp
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET     -1
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

void setup() {
  Serial.begin(115200);
  
  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println(F("Display não encontrado!"));
    while (true); // trava aqui se não encontrar
  }

  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);
  display.setCursor(0, 10);
  display.println(F("Display funcionando!"));
  display.display();
}

void loop() {
  // Não precisa repetir nada no loop nesse teste
}
```

---

### 📷 Resultado

No monitor serial apareceu:

```
Display funcionando!
```

E no display OLED a mensagem foi exibida corretamente 🎉

---

### 📝 Observações Importantes

- O endereço I2C padrão do display é `0x3C`. Alguns modelos podem vir com `0x78` ou `0x7A`. Se não funcionar, utilize o scanner I2C para descobrir.
- Certifique-se de conectar o **VCC no 3.3V**, e **não no 5V**, pois o display é de 3.3V!
- Se o display não mostrar nada: verifique a solda dos pinos, os fios, a conexão I2C e a alimentação.

### Imagens

![image](https://github.com/user-attachments/assets/c9a01ae3-07ee-46f0-b581-c983c3dee6a9)
![image](https://github.com/user-attachments/assets/73ef861e-a66f-4202-a3cc-ec1f8f6d988b)

![1000008935](https://github.com/user-attachments/assets/6cd8e777-e28d-4a1c-bb25-bd54d2e516af)
![1000008937](https://github.com/user-attachments/assets/11324af5-f679-42d4-bb59-5a0c6a84f569)
