
# Firewall iptables - Configuração e Análise

## Introdução

Este documento descreve a configuração do firewall `iptables` implementado em uma instância Oracle Cloud Infrastructure (OCI) como parte do portfólio. O objetivo principal é reforçar a segurança do servidor Linux por meio de regras restritivas de controle de tráfego de rede.

A configuração atual permite acesso web público enquanto restringe o acesso administrativo a um IP específico, seguindo o **princípio do menor privilégio**.

---

## Metodologia

### Configuração Padrão vs. Configuração Implementada

#### Configuração Padrão (Antes das Alterações)
```bash
INPUT ACCEPT [0:0]
FORWARD ACCEPT [0:0]
OUTPUT ACCEPT [0:0]

Todo tráfego é permitido por padrão
````

#### Configuração Implementada (Após as Alterações)

```bash
:INPUT DROP [142:17332]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [1787:158966]
-A INPUT -s 177.*.*.*/32 -p tcp -m tcp --dport 22 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
-A INPUT -i lo -j ACCEPT
```

> **Arquivo de referência das regras atuais**: [`ip-tables-atual.txt`](ip-tables-atual.txt)

### Análise das Mudanças Realizadas

| Item                   | Configuração Anterior  | Configuração Atual          | Impacto na Segurança                   |
| ---------------------- | ---------------------- | --------------------------- | -------------------------------------- |
| **Política INPUT**     | `ACCEPT` (permissiva)  | `DROP` (restritiva)         | Melhoria significativa             |
| **Política FORWARD**   | `ACCEPT`               | `DROP`                      | Prevenção de roteamento não autorizado |
| **Acesso SSH**         | Liberado para todos    | Restrito ao IP da minha máquina | Proteção contra brute force        |
| **Serviços Web**       | Sem regras específicas | Portas 80/443 liberadas     | Acesso controlado aos serviços         |
| **Interface Loopback** | Sem regra explícita    | Liberada explicitamente     | Estabilidade de serviços locais        |

---

## Resultados

### Regras Implementadas - Descrição Detalhada

#### 1. Regra de Acesso SSH Restrito

```bash
-A INPUT -s 177.*.*.*/32 -p tcp -m tcp --dport 22 -j ACCEPT
```

* **Propósito**: Permitir acesso administrativo apenas do IP autorizado
* **IP Autorizado**: 177... (IP da máquina que está conectando ao servidor remotamente)
* **Porta**: 22 (SSH)
* **Protocolo**: TCP
* **Efeito**: Bloqueia tentativas de acesso SSH de qualquer outro IP

#### 2. Regras de Serviços Web

```bash
-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
```

* **Propósito**: Permitir tráfego web público
* **Portas**: 80 (HTTP) e 443 (HTTPS)
* **Acesso**: Liberado para qualquer origem
* **Importância**: Essencial para funcionamento do servidor web

#### 3. Regra de Interface Loopback

```bash
-A INPUT -i lo -j ACCEPT
```

* **Propósito**: Permitir comunicação interna entre serviços
* **Interface**: lo (loopback)
* **Necessidade**: Crítica para funcionamento de aplicações locais

### Evidências de Funcionamento

#### Print 1: Status Completo do iptables

```bash
ubuntu@serv-teste$ sudo iptables -L -n -v
Chain INPUT (policy DROP 142 packets, 17332 bytes)
 pkts bytes target     prot opt in     out     source               destination         
   15  1200 ACCEPT     tcp  --  *      *       177.*.*.*            0.0.0.0/0            tcp dpt:22
   89  7120 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:80
   32  2560 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:443
    6   452 ACCEPT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0           

Chain FORWARD (policy DROP 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination         

Chain OUTPUT (policy ACCEPT 1787 packets, 158966 bytes)
 pkts bytes target     prot opt in     out     source               destination         
```

*Figura 1: Saída detalhada mostrando pacotes processados por cada regra*

#### Print 2: Teste de Conectividade SSH

```bash
# De IP autorizado
$ ssh - i [endereço/da/chave/editado] ubuntu@[ipdamaquina-editado]
Connection established successfully.

# De IP não autorizado
$ ssh - i [endereço/da/chave/editado] ubuntu@[ipdamaquina-editado]
ssh: connect to host servidor port 22: Connection timed out
```

*Figura 2: Verificação do controle de acesso SSH*


---

## Conclusão

A configuração do firewall iptables foi aplicada com sucesso, garantindo:

1. **Segurança Fortalecida**: Política DROP como padrão previne acessos não autorizados.
2. **Acesso Controlado**: SSH restrito ao IP autorizado impede ataques de força bruta.
3. **Serviços Web Funcionais**: Portas 80 e 443 acessíveis publicamente.
4. **Comunicação Interna Preservada**: Interface loopback liberada para serviços locais.

### Recomendações Futuras

1. Implementar **logging** para tentativas de acesso bloqueadas.
2. Adicionar **rate limiting** em conexões SSH.
3. Configurar DDNS se o IP autorizado for dinâmico.
4. Manter backup das regras em local seguro.

---

**Arquivo de Configuração**: [`ip-tables-atual.txt`](ip-tables-atual.txt)

**Data da Implementação**: 22 de Setembro de 2025
