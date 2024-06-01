# ECG-com-ESP32-na-plataforma-Ubidots

# Materiais necessários:

- Módulo ESP32.
  
O Microcontrolador ESP32-WROOM-32 é um módulo MCU Wi-Fi + BT + BLE poderoso e genérico que atende a uma ampla variedade de aplicações, desde redes de sensores de baixa potência até as tarefas mais exigentes, como codificação por voz, streaming de música e decodificação de MP3.  
No centro deste módulo está o chip ESP32-D0WDQ6. O chip incorporado foi projetado para ser escalonável e adaptável. Existem dois núcleos de CPU que podem ser controlados individualmente e a frequência de clock é ajustável de 80 MHz a 240 MHz. O usuário também pode desligar a CPU e usar o coprocessador de baixo consumo de energia para monitorar constantemente os periféricos em busca de alterações ou ultrapassagens de limites. ESP32 integra um rico conjunto de periféricos, que vão desde sensores de toque capacitivos, sensores Hall, interface de cartão SD, Ethernet, SPI de alta velocidade, UART, I2S e I2C. 
A integração de Bluetooth, Bluetooth LE e Wi-Fi garante que uma ampla gama de aplicações possa ser direcionada: o uso de Wi-Fi permite um grande alcance físico e conexão direta à Internet através de um roteador Wi-Fi, enquanto o uso do Bluetooth permite que o usuário se conecte ao telefone ou transmita sinais de baixa energia para sua detecção. A corrente de suspensão do chip é inferior a 5 µA, tornando-o adequado para aplicações eletrônicas alimentadas por bateria e vestíveis. ESP32 suporta uma taxa de dados de até 150 Mbps e potência de saída de 20,5 dBm na antena para garantir o mais amplo alcance físico. Como tal, o chip oferece especificações para um melhor desempenho para integração eletrônica, alcance, consumo de energia e conectividade. 



- Kit Sensor AD8232 + Eletrodos + Conectores para Eletrodos. 

Este sensor é uma placa com bom custo-benefício usada para medir a atividade elétrica do coração. Esta atividade elétrica pode ser mapeada como um ECG, ou eletrocardiograma, e emitida como uma leitura analógica. Os ECGs podem ser extremamente barulhentos, o monitor de frequência cardíaca de derivação única AD8232 atua como um amplificador operacional para ajudar a obter facilmente um sinal claro dos intervalos PR e QT.  
O AD8232 é um bloco de condicionamento de sinal integrado para ECG e outras aplicações de medição de biopotencial. Ele foi projetado para extrair, amplificar e filtrar pequenos sinais biopotenciais na presença de condições ruidosas, como aquelas criadas por movimento ou colocação remota de eletrodos.  
O módulo AD8232 separa nove conexões do IC nas quais você pode soldar pinos, fios ou outros conectores. SDN, LO+, LO-, OUTPUT, 3.3V, GND fornecem pinos essenciais para operar este monitor com um Arduino ou outra placa de desenvolvimento. Também são fornecidos nesta placa os pinos RA (braço direito), LA (braço esquerdo) e RL (perna direita) para conectar e usar seus próprios sensores personalizados. Além disso, há uma luz indicadora LED que pulsa ao ritmo de um batimento cardíaco. 



- Protoboard. 
 
Protoboard (ou Breadboard), também conhecida como matriz de contatos ou placa de prototipagem, é uma placa que possui furos e conexões internas para montagem de circuitos, utilizada para testes com componentes eletrônicos. Sua maior vantagem de uso é que ele dispensa a necessidade de solda para conectar tais circuitos, com placas variando entre 830 a 6000 furos. 
Na superfície de uma protoboard há uma base de plástico em que existem centenas de orifícios onde são encaixados os componentes. Em sua parte inferior, são instalados contatos metálicos que interligam eletricamente os componentes inseridos na placa. Geralmente suportam correntes entre 1 A e 3 A. Os contatos metálicos estão em diferentes sentidos na matriz. A placa possui a matriz principal em seu meio e duas linhas superiores e duas inferiores em cada matriz (alguns possuem apenas uma linha). Nestes últimos, os contatos estão na horizontal, enquanto na matriz principal eles estão na vertical. Em outras palavras, as linhas isoladas se conectam com os furos de baixo e as linhas agrupadas se conectam com os furos do lado. 
A protoboard é uma ferramenta muito útil para os profissionais da área de utilização porque possibilita conectar diversos componentes, como capacitores, resistores, circuitos integrados, diodos, transistores, entre outros, permitindo uma precisão maior na montagem de circuitos. 



- Jumper. 

Os fios jumper são fios que possuem pinos conectores em cada extremidade, permitindo que sejam usados para conectar dois pontos entre si sem soldar. Os fios jumper são normalmente usados com placas de ensaio (Protoboards) e outras ferramentas de prototipagem para facilitar a alteração de um circuito conforme necessário. 
Embora os fios jumper venham em uma variedade de cores, as suas cores na verdade não significam nada. Isso quer dizer que um fio jumper vermelho é tecnicamente igual a um preto. Mas as cores são utilizadas a seu favor para diferenciar tipos de conexões, como terra ou energia. 
Os fios jumper normalmente vêm em três versões: macho x macho, macho x fêmea e fêmea x fêmea. A diferença entre cada um está no ponto final do fio. As extremidades macho têm um pino saliente e podem ser conectadas a outros objetos, como as placas de ensaio, enquanto as extremidades fêmeas não têm e são usadas para serem conectadas por outros conectores. Os jumpers macho-macho são os mais comuns e os que você provavelmente encontrara com mais frequência. Ao conectar duas portas em uma placa de ensaio, você precisará de um fio macho para macho.
