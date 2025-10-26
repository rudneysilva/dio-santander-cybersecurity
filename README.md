## ⚠️ Aviso Legal

Este projeto foi desenvolvido **exclusivamente para fins educacionais** em ambiente controlado. A realização de testes de penetração sem autorização é **ilegal**. Sempre obtenha permissão explícita antes de testar sistemas que não sejam de sua propriedade.
___

# 🔐 Simulação de Ataques Brute Force com Medusa e Kali Linux

Este projeto tem como obejtivo documentar a implementação prática de ataques de força bruta em ambientes controlados, utilizando **Kali Linux** e a ferramenta **Medusa**, com foco em identificação de vulnerabilidades e recomendações de mitigação.

## 🎯 Objetivo

Demonstrar técnicas de auditoria de segurança através de simulações de ataques brute force em diferentes serviços (FTP, Web Forms e SMB), utilizando ambientes vulneráveis para fins educacionais e aprendizado prático de medidas defensivas.

## 🛠️ Tecnologias Utilizadas

- **Kali Linux** - Distribuição focada em testes de segurança
- **Medusa** - Ferramenta de brute force multi-protocolo
- **VMware** - Virtualização dos ambientes
- **Metasploitable 2** - VM intencionalmente vulnerável
- **DVWA (Damn Vulnerable Web Application)** - Aplicação web vulnerável para testes

## 📋 Pré-requisitos

- VMware Workstation
- Conhecimento básico de Linux e redes
- Compreensão dos aspectos éticos de testes de penetração

## 🔧 Configuração do Ambiente

### Configuração das Máquinas Virtuais

1. **Kali Linux** (Atacante)
   - Configurar adaptador de rede em modo Host-Only
   - IP: 192.168.10.16

2. **Metasploitable 2** (Alvo)
   - Configurar adaptador de rede em modo Host-Only
   - IP: 192.168.10.17

### Instalação do Medusa
```bash
sudo apt update
sudo apt install medusa
medusa -h  # Verificar instalação
```

## 🎭 Cenários de Ataque Simulados

### Cenário 1: Ataque Brute Force em FTP

### Enumerando os Serviços e Portas Via NMAP:
<img width="603" height="343" alt="image" src="https://github.com/user-attachments/assets/49d615f6-3176-4cb4-90ee-0a497394431a" />

-Sv: Mostra as versões dos Serviços que foram solicitados das Portas.  
-P: Para scanear nas seguintes portas.  
	
### Validando o acesso ao serviço e testando usuário e senha padrão:
<img width="770" height="254" alt="image" src="https://github.com/user-attachments/assets/a4dca226-aedc-4ea2-98d2-6a29514c002d" />
   
### Criação de Lista de usuários e senhas: 
<img width="759" height="209" alt="image" src="https://github.com/user-attachments/assets/bd2f6745-7199-4ccb-8229-331094f02093" />
	
### Realizando o Ataque via medusa em cima do Protocolo SFTP:
### Conta e senha encontrada. 

<img width="767" height="538" alt="image" src="https://github.com/user-attachments/assets/9f6b4da8-a496-4938-af2a-9f12eff44793" />
	
### Realizando o Teste no Servidor:
<img width="765" height="640" alt="image" src="https://github.com/user-attachments/assets/c49ea2dc-853e-47c5-92eb-2d9fdf4868db" />

### Cenário 2: Ataque em Formulário Web (DVWA)

**Objetivo:** Automatizar tentativas de login em aplicação web vulnerável.

**Resultado:**
**Acesso a Aplicação:**

<img width="1724" height="578" alt="image" src="https://github.com/user-attachments/assets/19e056ec-44bc-414c-a94f-3b1ba81d5077" />

**Criação da Lista de Senhas e Usuários:**
<img width="780" height="203" alt="image" src="https://github.com/user-attachments/assets/fdd3e9ea-0a5e-4667-a5b5-1b7c5fe0bf56" />

**Realizando ataque ao Formuário via Medusa:**

<img width="769" height="367" alt="image" src="https://github.com/user-attachments/assets/5acbc654-9c80-4864-a95d-2dcd3b65668c" />

### Cenário 3: Password Spraying em SMB

**Objetivo:** Testar senhas comuns em múltiplos usuários do serviço SMB.

**Enumeração de usuários:**
```bash
enum4linux -U 192.168.56.102
```
**Abrindo o arquivo e validando os usu[ario para criação da da WordList: **
less enum4output.txt

**Comando de ataque:**
```bash
medusa -h 192.168.56.102 -U users.txt -p Password123 -M smbnt -t 1
```
<img width="778" height="657" alt="image" src="https://github.com/user-attachments/assets/4fb6cbec-20f4-4f76-972b-fa11244d70c2" />
<img width="867" height="610" alt="image" src="https://github.com/user-attachments/assets/d6c9d7d0-a0da-44fe-a514-763743651ec6" />

**Validação do Acesso:** 

<img width="768" height="443" alt="image" src="https://github.com/user-attachments/assets/4d0275b2-b4f6-4704-a87a-24ece7c26b93" />


## 🛡️ Medidas de Mitigação Identificadas

### Recomendações Gerais
1. **Política de Senhas Robustas** - Implementar senhas com no mínimo 12 caracteres, combinando maiúsculas, minúsculas, números e símbolos
2. **Delay Incremental** - Adicionar atrasos progressivos após tentativas falhadas de login
3. **Autenticação Multifator (MFA)** - Adicionar camada extra de segurança além de usuário/senha
4. **Monitoramento de Eventos** - Implementar logs detalhados para detectar tentativas repetitivas
5. **Mensagens de Erro Genéricas** - Utilizar mensagens como "Usuário ou senha incorretos" ao invés de especificar qual campo está errado

### Medidas Específicas por Serviço
- **FTP**: Desabilitar acesso anônimo e limitar tentativas de login
- **Web**: Implementar CAPTCHA após tentativas falhadas
- **SMB**: Utilizar Kerberos e desabilitar NTLMv1

## 🎓 Aprendizados

Durante este projeto, foram explorados conceitos fundamentais de:
- Ataques de força bruta e suas variações (dictionary attack, password spraying)
- Configuração de ambientes de laboratório isolados
- Utilização de ferramentas de auditoria de segurança
- Importância de medidas defensivas em camadas
