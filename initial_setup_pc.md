## 📝 Documentação – Projeto com ESP32 Configuração Inicial

### 📦 Componentes usados
- ESP32 USB Type-C (CP2102)
- Fonte 12V 3A
- Conversor de tensão LM2596
- Módulo Relé 5V de 1 Canal
- Display OLED 0.96" I2C SSD1306
- Trava Eletromagnética 12V
- Cabos jumper
- (Aguardando) Módulo RTC DS3231

---

## ⚙️ 1. Instalação da IDE

### 🧩 Baixar Arduino IDE (Nightly)
- Link: [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software)
- Versão usada: `arduino-ide_nightly-20250311_Windows_64bit.zip`

**⚠️ Observação:** Não é um instalador `.exe`, basta extrair a pasta e executar o `arduino-ide.exe`.

---

## 📥 2. Instalar ESP32 na Arduino IDE

1. Abrir a IDE Arduino
2. Ir em: `File > Preferences`
3. Em **"Additional Board URLs"**, adicionar:
   ```
   https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
   ```
4. Depois, vá em:  
   `Tools > Board > Board Manager`  
   Buscar por **esp32** e instalar a versão mais recente (v3.1.3 no seu caso).

---

## 🧱 3. Selecionar a placa correta
- Ir em: `Tools > Board > ESP32 Dev Module`
- Porta: será configurada após os drivers.

---

## 🔌 4. Instalar Driver CP2102

### 📥 Download do Driver
- Site oficial:  
  [https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)

### Versão usada:
- **CP210x Universal Windows Driver v11.4.0**

### 📂 Instalação correta:
- Dentro da pasta extraída, localize o arquivo:
  ```
  silabser.inf
  ```
- Clique com o botão direito sobre ele e selecione **"Instalar"**.

**⚠️ Observação:**  
Não há um arquivo `installer.exe`. O driver deve ser instalado manualmente via o `.inf`.

### 🧪 Verificar no Gerenciador de Dispositivos
- Categoria: **Portas (COM e LPT)**
- Nome esperado:  
  `Silicon Labs CP210x USB to UART Bridge (COMX)`

---

## 🔄 5. Selecionar Porta na IDE

- Vá em: `Tools > Port`
- Escolha a porta COM correspondente ao **CP2102**
- No seu caso: `COM6`

---

## 💾 6. Testar Upload de Código

Código de exemplo usado:
```cpp
void setup() {
  Serial.begin(115200);
  Serial.println("ESP32 conectado!");
}

void loop() {
  delay(1000);
}
```

- Clique em `Upload` para enviar.
- O terminal deve exibir:  
  `Hard resetting via RTS pin...`

---

## 📡 7. Verificar no Serial Monitor

- Vá em: `Tools > Serial Monitor`
- Velocidade: **115200 baud**
- Pressione o botão **RST** da placa.
- Deve aparecer:  
  ```
  ESP32 conectado!
  ```

---

## 📌 Dificuldades encontradas

| Etapa | Dificuldade | Solução |
|------|-------------|---------|
| Driver CP2102 | Nenhum `.exe` no ZIP | Instalar via `silabser.inf` com botão direito |
| Porta COM não aparecia | Driver não estava instalado | Após driver, COM6 apareceu |
| Upload falhava | Porta errada ou driver ausente | Corrigido após driver correto |
| Serial Monitor não mostrava nada | Reset manual necessário | Pressionar botão `RST` |

---

## 💻 Para configurar em outro PC:

1. **Instalar Arduino IDE**
2. **Adicionar URL ESP32 nas preferências**
3. **Instalar a board ESP32**
4. **Instalar driver CP2102 via `silabser.inf`**
5. **Selecionar placa e porta correta**
6. **Fazer upload e testar com Serial Monitor**
