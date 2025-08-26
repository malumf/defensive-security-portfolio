# Dia 01: Estruturação do Repositório do Portfólio

## Objetivo

O presente documento detalha o processo de planejamento e a execução técnica para a criação do repositório `defensive-security-portfolio`.

## Planejamento e Decisões de Estrutura

Para assegurar a integridade e a clareza do projeto, foram definidas as seguintes diretrizes:

* **Plataforma de Versionamento:** O GitHub foi selecionado como plataforma para hospedagem do código e da documentação. A escolha baseia-se em sua ampla adoção na indústria de tecnologia e no robusto sistema de controle de versão Git.
* **Nomenclatura do Repositório:** O nome `defensive-security-portfolio` foi adotado por ser descritivo e alinhar-se com as convenções de nomenclatura para projetos de portfólio técnico.
* **Estrutura de Diretórios:** A organização consiste em diretórios nomeados sequencialmente (ex: `01-Setup`, `02-HomeLab`). Cada diretório corresponde a um dia do desafio e contém todos os artefatos pertinentes àquela tarefa. Tal estrutura facilita a navegação e a consulta ordenada dos projetos.

## Passos Técnicos Executados

A inicialização e a configuração do repositório foram realizadas por meio da execução dos seguintes comandos no terminal:

```bash
#Para a inicialização do repositório Git local
git init

#Criação da estrutura de diretórios e arquivos base
mkdir 01-Setup 02-HomeLab
touch README.md 01-Setup/README.md

#Adição dos arquivos ao staging para versionamento
git add .

#Execução do commit inicial para registrar a estrutura base
git commit -m

#Vinculação do repositório local ao repositório remoto no GitHub
git remote add origin [https://github.com/malumf/defensive-security-portfolio.git](https://github.com/malumf/defensive-security-portfolio.git)

#Push do commit inicial para a branch principal do repositório remoto
git push -u origin main
