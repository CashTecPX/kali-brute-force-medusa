# kali-brute-force-medusa


# Estudo: Ataque de Força Bruta com Medusa no Kali Linux

Repositório dedicado às anotações, comandos e exemplos práticos desenvolvidos durante os meus estudos de Cibersegurança com bolsa da **DIO (Digital Innovation One)**, explorando testes de força bruta utilizando **Medusa** no **Kali Linux**.

> **Aviso Legal:** Todo o conteúdo deste repositório tem fins exclusivamente educacionais e de aprendizado em segurança da informação. Execute testes apenas em ambientes próprios, máquinas virtuais de laboratório ou plataformas autorizadas.

## Contexto do Estudo
- **Formação:** Bootcamp / Bolsa de Estudos em Cibersegurança — **DIO (Digital Innovation One)**
- **Ambiente:** Máquina Virtual Kali Linux (ambiente isolado de laboratório)
- **Ferramenta principal:** Medusa

## O que foi aprendido na aula
- Conceitos fundamentais de autenticação e funcionamento de ataques de força bruta (*brute force*) e *credential stuffing*.
- Estrutura e sintaxe da ferramenta **Medusa** para testes automatizados em múltiplos protocolos.
- Utilização de *wordlists* de usuários e senhas em ambiente controlado.
- Estratégias de defesa e mitigação contra tentativas automatizadas de login.

## Exemplos de Comandos (Ambiente de Laboratório)

> Substitua `<IP_DO_ALVO>` pelo endereço da máquina virtual alvo do laboratório.

### Testando um único usuário com wordlist de senhas (SSH)
```bash

medusa -h <IP_DO_ALVO> -u admin -P /usr/share/wordlists/rockyou.txt -M ssh


medusa -h <IP_DO_ALVO> -U wordlists/usuarios.txt -P wordlists/senhas.txt -M ftp -t 4 -f

medusa -h <IP_DO_ALVO> -U wordlists/usuarios.txt -P wordlists/senhas.txt -M http -m DIR:/login -t 4 -f

Principais flags utilizadas
-h: endereço IP ou host do alvo.

-u / -U: usuário único ou arquivo (wordlist) contendo uma lista de usuários.

-p / -P: senha única ou arquivo (wordlist) contendo uma lista de senhas.

-M: módulo/protocolo do serviço testado (ssh, ftp, http, smbnt, mysql, etc.).

-t: número de threads (conexões simultâneas executadas ao mesmo tempo).

-f: interrompe a execução automaticamente ao encontrar a primeira credencial válida.


Como mitigar esse tipo de ataque
Autenticação Multifator (MFA): adiciona uma camada extra de verificação além da senha.

Políticas de Senhas Fortes: exigir senhas longas, complexas e únicas para cada serviço.

Bloqueio e Rate Limiting: configurar ferramentas como fail2ban para bloquear IPs após várias tentativas falhas consecutivas.

Hardening de Serviços: desativar login direto como root e priorizar autenticação por chaves criptográficas no SSH.


Referências
Documentação oficial da ferramenta Medusa (man medusa / medusa -d no Kali Linux)

Formação em Cibersegurança — DIO (Digital Innovation One)
