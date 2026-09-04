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

<img width="960" height="311" alt="WhatsApp Image 2026-09-04 at 14 31 12" src="https://github.com/user-attachments/assets/3d61102d-57b0-4df9-bc42-9da132eab561" />
<img width="960" height="813" alt="WhatsApp Image 2026-09-04 at 14 30 57" src="https://github.com/user-attachments/assets/f50808c9-d036-49ad-96ba-e79464061793" />


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
