# Análise de Tráfego de Rede com Wireshark (Baseline)

Este projeto faz parte do meu portfólio em Redes, Segurança e Cloud Computing, tendo como objetivo a análise do tráfego de rede para a criação de uma **linha de base**.  
O estudo foi realizado por meio da ferramenta **Wireshark**, com foco na identificação e compreensão dos protocolos de comunicação em diferentes cenários.  
A análise busca demonstrar como diversas aplicações utilizam a rede, bem como o impacto de uma ferramenta de privacidade (**VPN**) na natureza do tráfego.

---

## 1. Metodologia

A metodologia consistiu na captura e análise de pacotes de rede em três cenários distintos, tanto com a rede local padrão quanto com a utilização da **Riseup VPN**.  
A duração de cada captura variou entre **45 segundos e 2 minutos**.  

> ⚠️ Para evitar a exposição de dados sensíveis, as capturas foram realizadas **sem inserção de credenciais ou informações pessoais**.  

A análise concentrou-se nos seguintes pontos:

- **Comunicação Padrão**: Navegação nos sites *g1.com.br* e *YouTube*, além de comunicação em tempo real no **Discord**, para identificar o comportamento natural de cada serviço.  
- **Comunicação com VPN**: Repetição dos cenários acima com a **Riseup VPN** ativada, para observar o encapsulamento do tráfego.

---

## 2. Análise dos Resultados

Os resultados obtidos demonstram as particularidades de cada tipo de tráfego, bem como o efeito consolidado de uma **VPN**.

### 2.1. Cenário sem VPN

A análise do tráfego sem VPN revelou a diversidade de protocolos utilizados:

- **g1.com.br (Navegação)**  
  - 94,6% dos pacotes utilizando **IPv4** e **TCP**  
  - **TLS** representa 46,2% do tráfego, garantindo comunicação criptografada  
  - 📎 *Anexo: Hierarquia de Protocolos - G1 (Sem VPN)*

- **YouTube (Streaming)**  
  - 99,4% dos pacotes utilizando **IPv6**  
  - **UDP** corresponde a 97,4% do tráfego, priorizando baixa latência  
  - 📎 *Anexo: Hierarquia de Protocolos - YouTube (Sem VPN)*

- **Discord (Comunicação em tempo real)**  
  - **TCP + TLS** para chat/login  
  - **UDP** para chamadas de voz em tempo real  
  - 📎 *Anexo: Hierarquia de Protocolos - Discord (Sem VPN)*

---

### 2.2. Cenário com VPN

O uso da **Riseup VPN** consolidou e mascarou o tráfego, protegendo a privacidade:

- **Discord e G1 (com VPN)**  
  - A VPN encapsulou os dados originais em **um único protocolo de transporte: TCP**  
  - Isso mascara a natureza real da atividade online  
  - 📎 *Anexo: Hierarquia de Protocolos - Discord (Com VPN)*  
  - 📎 *Anexo: Hierarquia de Protocolos - G1 (Com VPN)*

---

## 3. Conclusão

A análise comparativa do tráfego de rede demonstrou a importância de uma **linha de base** para a **segurança cibernética**, permitindo identificar comportamentos anômalos.  

Além disso, o estudo validou a eficácia de uma **VPN** na consolidação e criptografia do tráfego, **mascarando a natureza da atividade online** do usuário e protegendo sua privacidade.  

> 🔐 A consolidação de protocolos e a ocultação dos endereços de destino, como observado nas capturas com VPN, são elementos fundamentais para a proteção de dados em redes públicas.

É possível validar os arquivos capturados pelo Wireshark na subpasta "Capturas" acima.
