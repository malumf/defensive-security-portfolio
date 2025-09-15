# Da Anomalia ao Incidente: Uma Análise Detalhada com Wireshark

---

### Resumo do Incidente

Este projeto documenta a análise de um arquivo PCAP que, inicialmente, apresentava uma anomalia em consultas DNS. A investigação, no entanto, expôs um incidente de segurança de maior gravidade: uma **sessão de acesso remoto não criptografada** a um sistema comprometido. A análise do tráfego revelou que um atacante se conectou com sucesso, realizou o reconhecimento do sistema e coletou dados antes de encerrar a conexão.

---

### Metodologia de Análise

A investigação foi conduzida em etapas, transformando pistas iniciais em evidências concretas de um incidente de segurança.

* **Identificação de Anomalias:** A análise começou com a busca por tráfego incomum. Consultas DNS para domínios estranhos e uma alta frequência de retransmissões TCP (indicando possíveis problemas de conectividade ou bloqueios) serviram como os primeiros indícios de uma atividade suspeita.
* **A Descoberta da Ameaça:** Aprofundando a análise, o tráfego **Telnet** foi identificado. A simples presença deste protocolo obsoleto e sem criptografia foi o principal indicador de comprometimento do sistema. O Telnet é raramente usado hoje e é um vetor de ataque conhecido para sessões de comando e controle (C2).
* **Reconstrução do Ataque:** A sessão Telnet foi reconstruída para visualizar a interação entre o atacante e o host comprometido.

---

### A Narrativa do Ataque

A análise do fluxo de pacotes permitiu reconstruir a linha do tempo do incidente:

1.  **Acesso e Reconhecimento:** O atacante estabeleceu uma conexão Telnet a um host rodando **Windows XP**. Em seguida, executou comandos para **mapear o sistema de arquivos** e coletar informações de diretórios e arquivos específicos, como **`aierrorlog.txt`** e **`autoexec.uh`**.
2.  **Coleta de Dados:** O atacante enviou um comando de sistema para coletar informações detalhadas, gerando vários **payloads, um deles de aproximadamente 1011 bytes**.
3.  **Saída Limpa:** A sessão foi encerrada com um comando **`exit`**, o que sugere um acesso controlado e uma operação bem-sucedida de coleta de informações antes de o atacante se desconectar.

---

### Conclusão e Habilidades Demonstradas

Este projeto vai além da simples análise de pacotes. Ele demonstra a capacidade de:

* **Correlacionar Eventos:** Conectar uma anomalia DNS a um fluxo TCP problemático e, finalmente, a um ataque em Telnet.
* **Identificar Riscos:** Reconhecer que o uso de protocolos inseguros, como o Telnet, é um risco de segurança crítico.
* **Reconstruir um Incidente:** Utilizar dados brutos para construir uma narrativa coerente sobre as ações de um atacante, do reconhecimento à exfiltração de dados.

A análise completa deste incidente é uma prova da habilidade em **análise de tráfego de rede** e **resposta a incidentes**.
