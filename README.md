## Descrição do projeto
A placa principal utilizada é o Arduino Uno, responsável pelo controle de toda a prototipagem. Ela é conectada via porta USB com um notebook, que serve como gateway através do protocolo Firmata e do Node-RED para estabelecer a conexão entre o dispenser de remédios e o message broker HiveMQ, utilizando o protocolo MQTT.  Para integrar todas as placas, sensores e atuadores, é utilizada uma protoboard de 400 pontos.

Pensando na melhor implementação possível do dispenser de remédios, o objetivo é utilizar o Display LCD 16x2, junto a botões auxiliares, para permitir ao usuário administrador configurar os horários de dispensação. Além disso, ele deve exibir a mensagem "Remédio!" no momento em que a medicação é liberada ao paciente. 

Porém, por dificuldades de implementação, foi realizada a simplificação do projeto: o disparo da dispensação é realizado através do smartphone, no aplicativo IoT MQTT Panel, através do botão “Dispensar comprimidos”. No momento da dispensação, o Buzzer Passivo 5v emite um sinal, juntamente a um LED de cor vermelha. O som deixa de ser emitido e o LED é desligado após 1 minuto, ou quando o botão de confirmação é pressionado. Este botão de confirmação, ao ser apertado pelo usuário paciente, emite um alerta ao IoT MQTT Panel do usuário administrador. Este alerta contém o dia e horário em que o botão foi clicado, como no exemplo a seguir: “Usuário pressionou o botão no dia 19/05, 21:39:37”.

A dispensação física dos medicamentos é realizada pelo Micro Servo 9g SG90, que fornece um pequeno "empurrão" nos comprimidos a serem disponibilizados. Por fim, a segunda implementação que não foi realizada com sucesso por dificuldades técnicas, mas é possível de ser realizada, é o uso do Sensor de Distância Ultrassônico HC-SR04. Ele deve monitorar a área próxima ao copo com os medicamentos. Se não houver movimentação em até 5 minutos após a dispensação dos remédios, ele deve acionar o protocolo MQTT para informar ao usuário administrador que o copo com os comprimidos não foi retirado.

## Como executar o projeto
1) Instale o Arduino IDE;
2) Realize o upload do arquivo "codigo-fonte-firmata.ino" para o Arduino Uno. Desta maneira, a placa fica habilitada para a utilização do protocolo Firmata através do USB serial;
3) Instale o Node.js na versão LTS mais recente;
4) Instale o Node-RED;
5) Instale os pacotes adicionais serialport e node-red-node-arduino;
6) Importe o arquivo "codigo-fonte-node-red.json" para a instância do Node-RED que está sendo executada em sua máquina. Antes de implementá-la, verifique se as portas COM dos nodes do Arduino estão conforme as portas utilizadas em seu computador.
