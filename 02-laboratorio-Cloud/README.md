# Projeto 02: Arquitetura de Laboratório de Análise em Nuvem

## Introdução

O presente projeto detalha o planejamento, a implementação e a validação de um laboratório de cibersegurança funcional e seguro. O objetivo principal é a criação de um ambiente controlado para a execução de estudos práticos em segurança ofensiva e defensiva.

O planejamento inicial previa a implementação de um laboratório em ambiente local, por meio do hipervisor Oracle VirtualBox. Contudo, uma análise de diagnóstico do hardware disponível revelou limitações impeditivas, especificamente a ausência de suporte do processador à tecnologia de virtualização Intel VT-x. Esta tecnologia é um requisito mandatório para a execução de máquinas virtuais de 64-bit, que são o padrão para os sistemas operacionais de análise modernos.

Diante desta restrição, o projeto foi migrado para um ambiente de nuvem, utilizando os recursos da Oracle Cloud Infrastructure (OCI). Esta adaptação não apenas contornou a limitação de hardware, mas também agregou ao projeto a componente de arquitetura e segurança em nuvem, uma competência de alta relevância no cenário tecnológico atual.

## Arquitetura do Laboratório

A arquitetura final foi implementada na região São Paulo (sa-saulo-1) da OCI. A estrutura consiste nos componentes a seguir:

* **Rede Virtual (VCN):** Foi provisionada uma Virtual Cloud Network com um bloco de endereços IP privados (`10.0.0.0/16`). A VCN foi segmentada em duas sub-redes para isolar os recursos:
    
    * **Sub-rede Pública:** Destinada a recursos que necessitam de uma interface com a internet.
    
    * **Sub-rede Privada:** Destinada a recursos que devem permanecer isolados, sem acesso direto pela internet.

* **Máquina Atacante (Jump Box):**
   
    * **Sistema:** Ubuntu Server 24.04.
    
    * **Recursos:** Instância `VM.Standard.E2.1.Micro` (Always Free).
    
    * **Localização:** Posicionada na Sub-rede Pública com um Endereço IP Público associado. Funciona como o único ponto de entrada para o laboratório (Bastion Host).
    
    * **Software:** Ferramentas de análise e exploração instaladas, como `Nmap` e `Metasploit-Framework`.

* **Máquina Alvo (Vítima):**
   
    * **Sistema:** Ubuntu Server 18.04 (como base para o contêiner Docker).
    
    * **Recursos:** Instância `VM.Standard.E2.1.Micro` (Always Free).
    
    * **Localização:** Posicionada na Sub-rede Privada, sem Endereço IP Público, garantindo seu isolamento.
    
    * **Software:** Serviço FTP vulnerável (`vsftpd 2.3.4`) executado por meio de um contêiner Docker customizado.


* **Segurança:** O controle de tráfego é realizado por meio de *Security Lists*. Foi configurada uma regra de entrada (*ingress rule*) na sub-rede pública para permitir acesso à porta 22 (SSH) a partir da internet, enquanto a comunicação interna entre as sub-redes foi liberada para a execução dos testes.

### Diagrama da Arquitetura

O diagrama a seguir ilustra a topologia de rede e a disposição dos componentes do laboratório.

`[INSERIR A IMAGEM DO SEU DIAGRAMA AQUI]`

## Metodologia

O desenvolvimento do projeto seguiu um processo iterativo de diagnóstico e implementação. A metodologia pode ser dividida nas fases subsequentes:

1.  **Fase 1 - Diagnóstico de Hardware:** Análise inicial do ambiente local. Por meio de ferramentas de sistema, constatou-se a ausência do recurso de virtualização de hardware, o que motivou a migração estratégica para a nuvem.

2.  **Fase 2 - Provisionamento em Nuvem:** Criação da infraestrutura de rede na OCI, incluindo a VCN, sub-redes pública e privada, e as respectivas *Security Lists*. Em seguida, as duas instâncias de computação foram provisionadas com imagens Ubuntu Server, em conformidade com os limites da camada gratuita.

3.  **Fase 3 - Configuração da Máquina Alvo:** Preparação do ambiente da vítima. Tentativas iniciais de compilar o software `vsftpd 2.3.4` diretamente no sistema operacional moderno encontraram erros de dependência e de linkagem de bibliotecas. Para solucionar o problema de forma robusta e replicável, optou-se pela criação de uma imagem Docker customizada. Um `Dockerfile` foi desenvolvido para automatizar a compilação do software em um ambiente compatível (Debian 7), empacotando o serviço vulnerável de forma isolada.

4.  **Fase 4 - Configuração da Máquina Atacante:** Instalação e configuração das ferramentas de pentest (`Nmap`, `Metasploit-Framework`) na instância Ubuntu designada como atacante.

5.  **Fase 5 - Validação do Ambiente:** Execução de testes de conectividade (`ping`) e de varredura de portas (`nmap`) a partir da máquina atacante contra a máquina alvo para validar a topologia da rede, as regras de firewall e a correta exposição do serviço vulnerável.

## Resultados

O ambiente de laboratório foi implementado com sucesso, e os testes de validação confirmaram sua funcionalidade.

* **Implantação do Serviço Vulnerável:** O contêiner Docker com o `vsftpd 2.3.4` foi construído e executado com sucesso na máquina alvo.
    `[INSERIR PRINT DO COMANDO 'docker ps' MOSTRANDO O CONTÊINER ATIVO]`

* **Verificação de Conectividade e Reconhecimento:** O scan de portas executado a partir da máquina atacante identificou corretamente as portas abertas na máquina alvo, incluindo a porta 22 (SSH) e a porta 21 (FTP) do serviço vulnerável.
    `[INSERIR PRINT DO RESULTADO DO 'nmap -Pn <IP_PRIVADO>']`

* **Acesso Seguro e Isolado:** O acesso ao ambiente foi realizado conforme o planejado, utilizando a máquina atacante como *Jump Box* para alcançar a máquina alvo, que permaneceu inacessível pela internet.
    `[INSERIR PRINT DO TERMINAL MOSTRANDO A SESSÃO SSH DE DENTRO DA VM ATACANTE PARA A VM VÍTIMA]`

## Conclusão

Este projeto resultou na criação de um laboratório de cibersegurança funcional, seguro e de custo zero, superando as limitações de hardware iniciais por meio da adoção de tecnologias de nuvem e contêineres.

A migração de um plano de implementação local para a nuvem demonstrou capacidade de adaptação e resolução de problemas. Além disso, a utilização do Docker para empacotar um serviço legado e problemático evidencia uma habilidade moderna e relevante em automação e Infraestrutura como Código (IaC). O laboratório, como configurado, serve como uma plataforma robusta para a execução dos próximos projetos práticos deste portfólio.
