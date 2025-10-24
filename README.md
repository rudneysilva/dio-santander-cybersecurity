---

# 🔐 Simulação de Ataques Brute Force com Medusa e Kali Linux

Este projeto documenta a implementação prática de ataques de força bruta em ambientes controlados, utilizando **Kali Linux** e a ferramenta **Medusa**, com foco em identificação de vulnerabilidades e recomendações de mitigação.[1][2]

## 🎯 Objetivo

Demonstrar técnicas de auditoria de segurança através de simulações de ataques brute force em diferentes serviços (FTP, Web Forms e SMB), utilizando ambientes vulneráveis para fins educacionais e aprendizado prático de medidas defensivas.[3][4]

## 🛠️ Tecnologias Utilizadas

- **Kali Linux** - Distribuição focada em testes de segurança
- **Medusa** - Ferramenta de brute force multi-protocolo
- **VirtualBox** - Virtualização dos ambientes
- **Metasploitable 2** - VM intencionalmente vulnerável
- **DVWA (Damn Vulnerable Web Application)** - Aplicação web vulnerável para testes

## 📋 Pré-requisitos

- VirtualBox instalado
- Conhecimento básico de Linux e redes
- Compreensão dos aspectos éticos de testes de penetração

## 🔧 Configuração do Ambiente

### Configuração das Máquinas Virtuais

1. **Kali Linux** (Atacante)
   - Configurar adaptador de rede em modo Host-Only
   - IP: 192.168.56.101

2. **Metasploitable 2** (Alvo)
   - Configurar adaptador de rede em modo Host-Only
   - IP: 192.168.56.102

### Instalação do Medusa
```bash
sudo apt update
sudo apt install medusa
medusa -h  # Verificar instalação
```

## 🎭 Cenários de Ataque Simulados

### Cenário 1: Ataque Brute Force em FTP

**Objetivo:** Comprometer credenciais do serviço FTP através de força bruta.[5][1]

**Comando utilizado:**
```bash
medusa -h 192.168.56.102 -u admin -P /usr/share/wordlists/rockyou.txt -M ftp -t 4
```

**Parâmetros:**
- `-h`: IP do alvo
- `-u`: Usuário testado
- `-P`: Wordlist de senhas
- `-M`: Módulo/protocolo (ftp)
- `-t`: Número de threads

**Resultado:** [Documentar se obteve sucesso e qual credencial foi descoberta]

### Cenário 2: Ataque em Formulário Web (DVWA)

**Objetivo:** Automatizar tentativas de login em aplicação web vulnerável.[6][3]

**Comando utilizado:**
```bash
medusa -h 192.168.56.102 -u admin -P wordlist.txt -M web-form -m FORM:"/dvwa/login.php" -t 2
```

**Resultado:** [Documentar taxa de sucesso e tempo necessário]

### Cenário 3: Password Spraying em SMB

**Objetivo:** Testar senhas comuns em múltiplos usuários do serviço SMB.[3][5]

**Enumeração de usuários:**
```bash
enum4linux -U 192.168.56.102
```

**Comando de ataque:**
```bash
medusa -h 192.168.56.102 -U users.txt -p Password123 -M smbnt -t 1
```

**Resultado:** [Documentar usuários comprometidos]

## 🛡️ Medidas de Mitigação Identificadas

### Recomendações Gerais
1. **Política de Senhas Robustas** - Implementar senhas com no mínimo 12 caracteres, combinando maiúsculas, minúsculas, números e símbolos[4][3]
2. **Delay Incremental** - Adicionar atrasos progressivos após tentativas falhadas de login[3]
3. **Autenticação Multifator (MFA)** - Adicionar camada extra de segurança além de usuário/senha[3]
4. **Monitoramento de Eventos** - Implementar logs detalhados para detectar tentativas repetitivas[3]
5. **Mensagens de Erro Genéricas** - Utilizar mensagens como "Usuário ou senha incorretos" ao invés de especificar qual campo está errado[3]

### Medidas Específicas por Serviço
- **FTP**: Desabilitar acesso anônimo e limitar tentativas de login
- **Web**: Implementar CAPTCHA após tentativas falhadas
- **SMB**: Utilizar Kerberos e desabilitar NTLMv1

## 📊 Wordlists Utilizadas

```
wordlist_simples.txt (10 senhas)
- password
- admin
- 123456
- welcome
- qwerty
...
```

## 📸 Evidências

[Adicione capturas de tela na pasta `/images`]
- Configuração da rede
- Execução dos comandos
- Resultados dos ataques
- Logs do sistema alvo

## 🎓 Aprendizados

Durante este projeto, foram explorados conceitos fundamentais de:
- Ataques de força bruta e suas variações (dictionary attack, password spraying)
- Configuração de ambientes de laboratório isolados
- Utilização de ferramentas de auditoria de segurança
- Importância de medidas defensivas em camadas

## ⚠️ Aviso Legal

Este projeto foi desenvolvido **exclusivamente para fins educacionais** em ambiente controlado. A realização de testes de penetração sem autorização é **ilegal**. Sempre obtenha permissão explícita antes de testar sistemas que não sejam de sua propriedade.[1][5]
