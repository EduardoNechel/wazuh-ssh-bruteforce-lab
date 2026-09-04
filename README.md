# wazuh-ssh-bruteforce-lab
Laboratório de detecção de brute force em SSH utilizando Wazuh.
# Wazuh - SSH Brute Force Detection Lab

## Objetivo

Demonstrar a detecção de múltiplas tentativas
de autenticação SSH malsucedidas utilizando Wazuh.

## Ambiente

- Ubuntu
- Wazuh
- OpenSSH
- Wazuh Dashboard
- /var/log/auth.log

## Simulação

Foi utilizado um usuário inexistente para gerar
múltiplas tentativas de autenticação SSH:

for i in {1..6}; do ssh usuario-inexistente@localhost; done

## Detecção

O Wazuh identificou a sequência de falhas e acionou:

Rule ID: 5712
Level: 10

sshd: brute force trying to get access to the system.
Non existent user.

## Evidências

## Evidências

### 1. Simulação do ataque
[![Terminal com brute force SSH](WhatsAppImage2026-09-04at14.31.12.jpeg)](https://github.com/EduardoNechel/wazuh-ssh-bruteforce-lab/blob/82456b2e477c901f351f6e93e25d729abd382016/WhatsApp%20Image%202026-09-04%20at%2014.31.12.jpeg)

### 2. Detecção no Wazuh - Rule 5712 Level 10
[![Alerta Wazuh detectando brute force](WhatsAppImage2026-09-04at14.30.57.jpeg)](https://github.com/EduardoNechel/wazuh-ssh-bruteforce-lab/blob/82456b2e477c901f351f6e93e25d729abd382016/WhatsApp%20Image%202026-09-04%20at%2014.30.57.jpeg)

## Análise

Source IP: 127.0.0.1
User: usuario-inexistente
Log source: /var/log/auth.log

## Conclusão

O laboratório demonstrou o fluxo entre:

Tentativa de autenticação
        ↓
SSH
        ↓
/var/log/auth.log
        ↓
Wazuh
        ↓
Decoder
        ↓
Rule 5712
        ↓
Alert
        ↓
Dashboard
