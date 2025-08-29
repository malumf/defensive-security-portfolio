# 🖼️ Prints de Análise de Tráfego

Este diretório contém **capturas de tela (prints)** geradas no **Wireshark**, ilustrando a análise de proporção de hierarquias de protocolos em diferentes cenários.  

Esses gráficos e estatísticas visuais complementam os relatórios de cada experimento, permitindo observar de forma clara a distribuição de protocolos em cada tipo de tráfego.

---

## 📑 Estrutura dos Arquivos

- `g1_sem_vpn.png` → Hierarquia de protocolos durante acesso ao **g1.com.br** sem VPN  
- `youtube_sem_vpn.png` → Hierarquia de protocolos durante streaming no **YouTube** sem VPN  
- `discord_sem_vpn.png` → Hierarquia de protocolos durante comunicação em tempo real no **Discord** sem VPN  
- `g1_com_vpn.png` → Hierarquia de protocolos durante acesso ao **g1.com.br** com VPN (**Riseup**)  
- `discord_com_vpn.png` → Hierarquia de protocolos durante comunicação no **Discord** com VPN (**Riseup**)  

---

## 🔍 Como Utilizar

- Use estas imagens como **apoio visual** ao relatório localizado na pasta principal.  
- A visualização permite **comparar rapidamente** o impacto do uso de uma **VPN** sobre os protocolos utilizados.  
- Exemplos de observação:  
  - Predominância de **UDP** em streaming de vídeo (YouTube).  
  - Encapsulamento em **TCP** quando a VPN está ativa.  
  - Mistura de **TCP/TLS e UDP** no Discord (chat vs. voz).  

---

## ⚠️ Observações

- As imagens são para **uso educacional** e documentam o comportamento da rede durante os testes.  
- Nenhum dado pessoal ou credencial foi incluído nas capturas.  
- Para análise detalhada, consulte os arquivos `.pcapng` na pasta [`capturas`](../Capturas) e o relatório na pasta principal.  

---

✍️ **Autor:** Projeto desenvolvido como parte do desafio *30 Dias, 30 Projetos em Cibersegurança*.  
