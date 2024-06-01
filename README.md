# ECG-com-ESP32-na-plataforma-Ubidots


# Introdução

Este projeto visa a criação de um dispositivo de leitura cardiáca através da utilização de um módulo ESP32-WROOM-32 para fazer interface com o Sensor de ECG AD8232, e então gerar um sinal de ECG conectando os eletrodos do sensor ao peito. Usando a plataforma Ubidots como MQTT Broker para enviar os arquivos para a nuvem do próprio Ubidots que ira então criar um gráfico com os dados.


# Materiais necessários:

- Módulo ESP32.
  
O Microcontrolador ESP32-WROOM-32 é um módulo MCU Wi-Fi + BT + BLE poderoso e genérico que atende a uma ampla variedade de aplicações, desde redes de sensores de baixa potência até as tarefas mais exigentes, como codificação por voz, streaming de música e decodificação de MP3.  

- Kit Sensor AD8232 + Eletrodos + Conectores para Eletrodos. 

Este sensor é uma placa com bom custo-benefício usada para medir a atividade elétrica do coração.
O módulo AD8232 contem nove conexões. SDN, LO+, LO-, OUTPUT, 3.3V, GND fornecem pinos essenciais para operar este monitor com um Arduino ou outra placa de desenvolvimento. Também são fornecidos nesta placa os pinos RA (braço direito), LA (braço esquerdo) e RL (perna direita) para conectar e usar seus próprios sensores personalizados. Além disso, há uma luz indicadora LED que pulsa ao ritmo de um batimento cardíaco. 

- Protoboard. 
 
Protoboard (ou Breadboard), também conhecida como matriz de contatos ou placa de prototipagem, é uma placa que possui furos e conexões internas para montagem de circuitos, utilizada para testes com componentes eletrônicos. Sua maior vantagem de uso é que ele dispensa a necessidade de solda para conectar tais circuitos, com placas variando entre 830 a 6000 furos. 

- Jumper. 

Os fios jumper são fios que possuem pinos conectores em cada extremidade, permitindo que sejam usados para conectar dois pontos entre si sem soldar. Os fios jumper são normalmente usados com placas de ensaio (Protoboards) e outras ferramentas de prototipagem para facilitar a alteração de um circuito conforme necessário. 


# Configuração do dispositivo

- Para fazer a conexão do sensor de ECG AD8232 com o módulo ESP32, primeiro encaixe ambos nas protoboards e conecte com os jumpers o pino de 3.3V do AD8232 ao do ESP32, conecte o GND ao GND. O pino de OUTPUT do AD8232 é conectado ao pino VP do ESP32. Os pinos LO+ e L0- do AD8232 são conectados a D2 e D3 do ESP32.

# Configurando o Ubidots

O Ubidots funciona como o MQTT Broker, e oferece uma plataforma para desenvolvedores que lhes permite capturar facilmente dados de sensores e transformá-los em informações úteis.

- Passo 1: Criando uma conta Ubidots 

Acesse https://www.ubidots.com e crie uma conta clicando em “Sign Up”. 

- Passo 2: Criando Dispositivo e Adicionando Variáveis 

Vá para “My Account”, clique em “Devices”, crie um Device, selecione o “Blank Device”, digite o nome que quiser e clique em “Next” para criar o dispositivo. 

Clique no dispositivo recém-criado. Clique no sinal de “+” e escolha a opção “Raw variable”. Agora renomeie esta variável com algum nome. 

- Passo 3: Criando o Dashboard e Adicionando Widget 

Para criar um Dashboard, vá em “Data > Dashboards”. Clique no ícone “Add new Dashboard”, digite um nome e mantenha todos os outros campos nas configurações padrão e então crie-o clicando em “Save”.

Clique na opção “Add new Widget”, você será apresentado a várias opções de visualização de dados, escolha uma delas, para este projeto é a melhor escolha é o “Line Chart” para traçar o gráfico usando os dados carregados através do módulo ESP32. 

Depois, será solicitado que adicione uma variável, selecione o Device criado anteriormente e selecione a variável que foi criada em seguida. 

Clique em "Appearance" e de um nome para o Dashboard, mantenha o restante das opções no padrão, depois confirme. 

Como o dispositivo não se comunicou com Ubidots, ele mostrará que nenhum dado foi encontrado. Assim que o dispositivo começar a enviar dados, ele poderão ser vizualizados no Dashboard.


# Instalando a extensão para ESP32 e bibliotecas necessárias

É necessário que se faça o download e instale o software mais recente do Arduino IDE, pois é ele que usaremos para a programação. O software pode ser encontrado em https://www.arduino.cc/en/software. 
Após a intalação, abra o programa.


- Instalando o complemento ESP32 no Arduino IDE: 

- Passo 1: 

No seu Arduino IDE, vá em File> Preferences. 

- Passo 2: 

Digite no campo “Additional Board Manager URLs” os seguintes endereços e cofirme:

https://dl.espressif.com/dl/package_esp32_index.json, 
http://dan.drown.org/stm32duino/package_STM32duino_index.json, 
http://arduino.esp8266.com/stable/package_esp8266com_index.json. 

- Passo 3: 

Certifique-se das configurações de “Network”. Se o seu computador estiver conectado a um ponto de acesso de telefone celular ou roteador Wi-Fi sem proxy, você poderá selecionar as configurações de “No Proxy” ou “Auto-detect proxy settings”. 
Da mesma forma, se você estiver usando uma conexão de Internet com um proxy, selecione “Manual Proxy Configuration” e forneça os detalhes do proxy.  
Em seguida, clique no botão “OK”.

- Passo 4: 

Abra o Boards Manager. Vá em Tools> Board> Boards Manager… 
Procure por “ESP32” e instale a extensão “ESP32 by Espressif Systems”. 
A extensão para ESP32 será instalado após alguns segundos. Após uma instalação bem-sucedida, você pode fechar esta janela.


- Instalando bibliotecas necessárias: 

Serão usadas as bibliotecas abaixo. As duas primeiras bibliotecas estão pré-instaladas no Arduino IDE. 

#include <WiFi.h> 
#include <WiFiUdp.h> 
#include <PubSubClient.h> 
#include <NTPClient.h> 

É necessário instalar as outras duas bibliotecas. Podemos instalá-las a partir do próprio gerenciador de bibliotecas do Arduino. Vá para o "Library Manager", digite o nome da biblioteca que deseja instalar, no caso “PubSubClient” e instale-a. Repita o mesmo processo para “NTPClient”.

# Credenciais para conexão com a nuvem do Ubidots

Primeiro copie o código contido no "source-code" desse repositório para o Arduino IDE.
Depois modifique os seguintes campos do código para configurar a sua conexão com a nuvem Ubidots.

- Credenciais Wi-Fi

Fornecer SSID do seu Wi-Fi e senha para conexão com a Internet. 

#define WIFISSID "xxxxxxxxxxxxxxxxx" // Preencha com o SSID do seu Wi-Fi
#define PASSWORD "xxxxxxxxxx" // Preencha com a senha do seu Wi-Fi


- Credenciais Ubidots/ Protocolo MQTT 

Fornecer o token criado pleo Ubidots, podemos obtê-lo no próprio site Ubidots.  

Esse token é que faz a conexão com o Ubidots MQTT Broker, que autoriza o dispositivo a interagir com API do Ubidots. 

Em “My Account”, vá até a opção “API Credentials” e copie o que consta em “Default Token”. 

Insira um nome de cliente MQTT. Pode ser qualquer sequência alfanumérica. 

Em seguida, insira o nome da variável (Variable) e o nome do dispositivo(Device), que foi criado anteriormente no Ubidots. 

#define TOKEN "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" // Preencha com a "Default Token" fornecida pelo Ubidots
#define MQTT_CLIENT_NAME "xxxxxxxxxxxxx" // Preencha com qualquer sequencia alfanumérica
#define VARIABLE_LABEL "xxxxxxxxxx" // Preencha com o nome da "Variable" criada no Ubidots 
#define DEVICE_LABEL "xxxxxxxxxxxxxx" // Preencha com o nome do "Device" criado no Ubidots


# Upload 

Conecte o dispositivo através do módulo ESP32 ao laptop/computador e coloque os eletrodos no corpo da pessoa a ser examinada, lembrando de pedir para que ela não se mova durante todo o processo. É recomendado que o exame seja feito com a pessoa deitada.

Verifique na aba "Tools" do Arduino IDE se a configuração consta como “Board: ESP32 Dev Module, e depois selecione o “Port” correto de onde foi conectado o dispositivo. 

Em seguida, clique em “Upload” e segure o botão "boot" do módulo ESP32 até a conexão ser estabelecida. 


# Output 

Após o upload bem-sucedido, abra o Serial Monitor, nele podera ver o ESP32 conectado com sucesso ao Wi-Fi programado e alocado com endereço IP. Depois é iniciada a conexão MQTT com a nuvem Ubidots e conectada a ela.  

Em seguida, é iniciado o envio de dados de ECG junto com um “Timestamp”. Cada pacote de dados contém o nome da variável e 4 pontos de dados com o “Timestamp” de data/hora exato. 

Vá para o site Ubidots e recarregue a página com o Dashboard. Você pode ver o eletrocardiograma sendo traçado ao vivo no painel do Ubidots.  
