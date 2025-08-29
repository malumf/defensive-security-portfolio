# 📂 Capturas de Tráfego (Wireshark)

Este diretório contém os arquivos **.pcapng** resultantes das análises realizadas com o **Wireshark** durante o projeto de **Análise de Tráfego de Rede (Baseline)**.  

As capturas foram feitas em diferentes cenários, com e sem a utilização de VPN, a fim de comparar o comportamento dos protocolos de rede.

---

## 📑 Estrutura dos Arquivos

- `g1semvpn.pcapng` → Tráfego capturado ao acessar **g1.com.br** sem VPN  
- `youtubesemvpn.pcapng` → Tráfego capturado ao assistir vídeo no **YouTube** sem VPN  
- `discordsemvpn.pcapng` → Tráfego capturado em chamada de voz no **Discord** sem VPN  
- `g1comvpn.pcapng` → Tráfego capturado ao acessar **g1.com.br** com **Riseup VPN**  
- `discordcomvpn.pcapng` → Tráfego capturado em chamada de voz no **Discord** com **Riseup VPN**

---

## 🔍 Como Abrir as Capturas

1. Abra o **Wireshark** em sua máquina.  
2. Vá em **File > Open** e selecione um dos arquivos `.pcapng`.  
3. Utilize os filtros do Wireshark para inspecionar protocolos específicos. Exemplos:  
   - `tcp` → Mostrar apenas pacotes TCP  
   - `udp` → Mostrar apenas pacotes UDP  
   - `tls` → Mostrar apenas tráfego TLS/SSL  
   - `ip.addr == X.X.X.X` → Filtrar tráfego por endereço IP  

---

## ⚠️ Observações

- As capturas foram realizadas **sem uso de credenciais ou dados pessoais**, para evitar exposição de informações sensíveis.  
- Estes arquivos são destinados **exclusivamente para fins educacionais e de pesquisa**.  
- O uso em ambientes de produção ou para análise de tráfego de terceiros **não é recomendado** sem consentimento.  

---

✍️ **Autor:** Projeto desenvolvido como parte do desafio *30 Dias, 30 Projetos em Cibersegurança*.
