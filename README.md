# 🔐 Análise de Ataque Brute Force com Wireshark

[![Status](https://img.shields.io/badge/status-concluído-brightgreen)]()
[![Nível](https://img.shields.io/badge/nível-iniciante-blue)]()
[![Ferramenta](https://img.shields.io/badge/ferramenta-Wireshark-purple)]()

---

```bash
📦 wireshark-brute-force/
├── images/                    <- Prints das capturas Wireshark
├── bruteforce.pcap           <- Arquivo analisado
└── README.md                 <- Este arquivo
```

---

## 📌 Objetivo

Detectar um ataque de força bruta no tráfego de rede utilizando o Wireshark. O projeto simula o que um SOC Analyst faz ao investigar tentativas de acesso malicioso via FTP.

---

## 🧠 Cenário

- **Tipo de ataque:** Brute Force (Força Bruta)
- **Protocolo usado:** FTP
- **Arquivo analisado:** `bruteforce.pcap` (fonte: Zeek GitHub)

---

## 🛠️ Ferramenta Utilizada

- [Wireshark](https://www.wireshark.org/)

---

## 🧪 Metodologia

1. Abrir o `.pcap` no Wireshark.
2. Aplicar filtros para identificar padrões de brute force:
   - `ftp.request.command == "USER"`
   - `ftp.request.command == "PASS"`
   - `ftp.response.code == 530`
   - `ftp.response.code == 230`
3. Analisar pacotes com comandos de login, respostas do servidor e repetições suspeitas.

---

## 📸 Evidências (Capturas de Tela)

### 1. Tentativas de Login com USER e PASS
> Pacotes contendo comandos USER e PASS repetidos com senhas simples.

📎 ![USER/PASS](./images/ftp-user-pass-filter.png)

---

### 2. Tentativas Falhas (Código 530)
> Servidor responde com erro de autenticação múltiplas vezes.

📎 ![530 Login incorrect](./images/ftp-code-530.png)

---

### 3. Tentativa Bem-sucedida (Código 230)
> Após várias falhas, senha correta é encontrada e o login tem sucesso.

📎 ![230 Login successful](./images/ftp-code-230.png)

---

### 4. Comandos PASS (Senhas Testadas)
> Mostra todas as senhas enviadas ao servidor antes de conseguir o acesso.

📎 ![PASS Commands](./images/ftp-pass-commands.png)

---

## 📊 Resumo

| Ataque       | Evidência Observada                                             | Filtro Usado                          |
|--------------|------------------------------------------------------------------|----------------------------------------|
| Brute Force  | USER/PASS com senhas simples + respostas 530 e depois 230       | `ftp.request.command`, `ftp.response.code` |

---

## ✅ Conclusão

Este projeto demonstra como ataques de brute force podem ser detectados via inspeção de pacotes. O uso do Wireshark permite visualizar claramente tentativas repetidas de login e respostas do servidor, ajudando analistas SOC a identificar comportamentos suspeitos.

---

## 📂 Como Rodar Localmente

1. Baixe o Wireshark: [https://www.wireshark.org/download.html](https://www.wireshark.org/download.html)
2. Abra o arquivo `bruteforce.pcap`
3. Aplique os filtros para observar as tentativas de ataque

