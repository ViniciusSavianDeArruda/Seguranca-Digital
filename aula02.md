# Segurança de Redes — Aula 02

## Unidade 1 — Segurança de Redes Locais e de Longa Distância

---

# 1. Revisão da Aula 01

## Segurança Digital

Proteção de informações, contas e sistemas contra acessos não autorizados, alterações ou indisponibilidade.

## Tríade CIA

* **Confidencialidade:** impedir acesso não autorizado.
* **Integridade:** impedir alterações indevidas.
* **Disponibilidade:** garantir que os recursos estejam acessíveis.

## Conceitos básicos

* **Ativo:** aquilo que precisa ser protegido.
* **Ameaça:** algo que pode causar dano.
* **Vulnerabilidade:** uma fraqueza que pode ser explorada.
* **Risco:** possibilidade de uma ameaça explorar uma vulnerabilidade.
* **Controle:** medida utilizada para reduzir riscos.

## Defesa em profundidade

Utilizar várias camadas de segurança, pois nenhum controle é perfeito sozinho.

## Zero Trust

Nenhum acesso deve ser considerado confiável automaticamente. Cada acesso deve ser verificado.

---

# 2. Segurança de Redes

A aula aborda:

* Segurança digital
* Invasão
* Crackers
* Servidores
* Procedimentos preventivos
* Testes de invasão

### Cracker

Pessoa que utiliza técnicas de invasão para fins maliciosos.

### Hacker ético

Utiliza as mesmas técnicas de forma autorizada para identificar e corrigir problemas de segurança.

---

# 3. Etapas Básicas de uma Invasão

## Reconhecimento

O invasor procura descobrir:

* Hosts ativos
* Serviços expostos
* Versões de software

## Enumeração

Detalhamento das informações encontradas:

* Portas abertas
* Protocolos
* Usuários
* Permissões

## Exploração

Utilização de uma vulnerabilidade para tentar obter acesso não autorizado.

```text
Reconhecimento
      ↓
Enumeração
      ↓
Exploração
```

---

# 4. Senhas

## Boas práticas

### Comprimento

Senhas longas são preferíveis a senhas curtas e artificialmente complexas.

### Não reutilizar

Uma senha diferente deve ser utilizada em cada serviço.

Se uma senha for vazada, reutilizá-la pode comprometer outros serviços.

### MFA

**MFA — Multi-Factor Authentication**

Adiciona um segundo fator de autenticação, como:

* Aplicativo
* Token
* Biometria

### Gerenciador de senhas

Permite utilizar senhas longas e únicas sem precisar memorizar todas.

---

# 5. Como Senhas São Comprometidas

## Vazamento de dados

A senha ou seu hash pode ser exposto em um incidente de segurança.

## Credential Stuffing

Uma senha vazada em um serviço é testada automaticamente em outros serviços.

## Phishing

O usuário é enganado e fornece sua senha em um site ou formulário falso.

## Brute Force

Tentativas automatizadas de várias combinações.

## Password Spray

Tentativa de senhas comuns contra vários usuários.

## Dicionário

Utilização de listas de palavras e combinações conhecidas.

### Ferramenta mencionada

[Have I Been Pwned](https://haveibeenpwned.com/) permite verificar se um e-mail apareceu em vazamentos conhecidos.

---

# 6. LAN e WAN

## LAN

**Local Area Network**

Rede local.

Exemplos:

* Sala
* Prédio
* Campus

Normalmente possui poucos hosts e utiliza comunicação local.

## WAN

**Wide Area Network**

Interliga redes locais que estão distantes.

A Internet é um exemplo de WAN.

## Internetworking

Permite que redes diferentes se comuniquem por meio da suíte de protocolos **TCP/IP**.

---

# 7. Modelo OSI x TCP/IP

## Modelo OSI

Possui **7 camadas**:

1. Física
2. Enlace
3. Rede
4. Transporte
5. Sessão
6. Apresentação
7. Aplicação

## Modelo TCP/IP

Possui **4 camadas**:

1. Acesso à Rede
2. Internet
3. Transporte
4. Aplicação

### Correspondência

| OSI          | TCP/IP        |
| ------------ | ------------- |
| Aplicação    | Aplicação     |
| Apresentação | Aplicação     |
| Sessão       | Aplicação     |
| Transporte   | Transporte    |
| Rede         | Internet      |
| Enlace       | Acesso à Rede |
| Física       | Acesso à Rede |

---

# 8. As 4 Camadas do TCP/IP

| Camada            | Função                           | Exemplos                  |
| ----------------- | -------------------------------- | ------------------------- |
| **Aplicação**     | Comunicação dos programas        | HTTP, DNS, SSH, FTP       |
| **Transporte**    | Entrega de dados entre processos | TCP, UDP                  |
| **Internet**      | Endereçamento e roteamento       | IP, ICMP                  |
| **Acesso à Rede** | Comunicação no meio físico       | Ethernet, Wi-Fi, MAC, ARP |

---

# 9. Camada de Aplicação

É onde usuários e programas efetivamente utilizam a rede.

## HTTP/HTTPS

Utilizados para navegação web.

* **HTTP:** protocolo web.
* **HTTPS:** utiliza criptografia.

## DNS

Traduz nomes, como:

```text
exemplo.com
```

para endereços IP.

## SSH

Utilizado para acesso remoto administrativo e possui criptografia.

## FTP

Utilizado para transferência de arquivos.

Historicamente, não possui criptografia.

### Pontos de atenção

Em testes de invasão podem ser analisados:

* Banners dos serviços
* Versões desatualizadas
* Credenciais fracas

---

# 10. Camada de Transporte

Organiza a entrega de dados entre processos.

## TCP

* Orientado à conexão.
* Confiável.
* Garante entrega.
* Garante ordem.

Utiliza o **three-way handshake**:

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```

Utilizado por:

* HTTP
* SSH
* FTP

## UDP

* Não orientado à conexão.
* Mais rápido.
* Não garante entrega.
* Não garante ordem.

Utilizado por:

* DNS
* Streaming
* VoIP

### Diferença principal

> **TCP prioriza confiabilidade.**
> **UDP prioriza velocidade.**

---

# 11. Camada de Internet

Responsável por endereçar hosts e encaminhar pacotes entre redes.

## IP

Endereça os hosts e permite que os pacotes sejam encaminhados da origem até o destino.

## Roteamento

Os roteadores utilizam tabelas de rotas para decidir para onde encaminhar os pacotes.

## ICMP

Protocolo utilizado para controle e diagnóstico.

Exemplos:

* `ping`
* `traceroute`

---

# 12. IPv4 x IPv6

## IPv4

* 32 bits
* Aproximadamente 4,3 bilhões de endereços
* Notação decimal
* Exemplo:

```text
192.168.1.10
```

## IPv6

* 128 bits
* Quantidade muito maior de endereços
* Notação hexadecimal
* Exemplo:

```text
2001:db8::1
```

---

# 13. Camada de Acesso à Rede

Responsável por colocar os dados no meio de transmissão:

* Cabo
* Fibra
* Rádio

## Ethernet

Utilizada em redes locais cabeadas.

Organiza os dados em **frames**.

## MAC

Identificador utilizado dentro do segmento de rede local.

## Wi-Fi

Comunicação de rede sem fio.

Possui desafios adicionais de segurança porque o meio de transmissão é aberto.

## ARP

Relaciona um endereço IP ao endereço MAC dentro da rede local.

### ARP Spoofing

É uma técnica que pode falsificar essa relação para possibilitar interceptação.

---

# 14. Classes de Endereços IPv4 e CIDR

As classes antigas de IPv4 eram:

| Classe | Faixa                         | CIDR tradicional | Uso                 |
| ------ | ----------------------------- | ---------------- | ------------------- |
| **A**  | `1.0.0.0 – 126.255.255.255`   | `/8`             | Redes muito grandes |
| **B**  | `128.0.0.0 – 191.255.255.255` | `/16`            | Redes médias        |
| **C**  | `192.0.0.0 – 223.255.255.255` | `/24`            | Redes pequenas      |

Atualmente, o **CIDR** permite definir o tamanho da rede de maneira mais flexível.

Exemplo:

```text
192.168.1.0/26
```

---

# 15. Endereçamento IP e Sub-redes

Exemplo:

```text
192.168.1.10/24
```

* `192.168.1` → identifica a rede
* `.10` → identifica o host
* `/24` → máscara de sub-rede

## Regra importante

> Quanto maior o número depois da `/`, menor a quantidade de hosts possíveis.

A segmentação de redes também funciona como controle de segurança, pois pode limitar o alcance de um ataque.

---

# 16. Cálculo de Sub-redes

Exemplo:

```text
192.168.5.0/24
```

Dividir em redes `/26`.

## 1. Bits emprestados

```text
26 - 24 = 2 bits
```

## 2. Quantidade de sub-redes

```text
2² = 4 sub-redes
```

## 3. Hosts por sub-rede

```text
32 - 26 = 6 bits para hosts

2⁶ - 2 = 62 hosts utilizáveis
```

## 4. Sub-redes resultantes

```text
192.168.5.0/26
192.168.5.64/26
192.168.5.128/26
192.168.5.192/26
```

---

# 17. NAT

**NAT — Network Address Translation**

Traduz endereços privados internos para um endereço público ao acessar a Internet.

## Faixas privadas

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

## Funções

* Economiza endereços IPv4 públicos.
* Permite que vários dispositivos utilizem um endereço público.
* Dificulta o acesso direto da Internet aos hosts internos.

> **NAT não substitui um firewall.**

---

# 18. Portas e Serviços

|    Porta | Protocolo | Serviço |
| -------: | --------- | ------- |
|   **22** | TCP       | SSH     |
|   **53** | TCP/UDP   | DNS     |
|   **80** | TCP       | HTTP    |
|  **443** | TCP       | HTTPS   |
|  **445** | TCP       | SMB     |
| **3389** | TCP       | RDP     |
|   **23** | TCP       | Telnet  |

## Pontos de segurança

* **22 — SSH:** alvo comum de força bruta.
* **53 — DNS:** pode revelar informações sobre a rede.
* **80 — HTTP:** não possui a proteção de criptografia do HTTPS.
* **443 — HTTPS:** utiliza criptografia.
* **445 — SMB:** possui histórico de vulnerabilidades graves.
* **3389 — RDP:** não deve ficar exposto diretamente à Internet.
* **23 — Telnet:** acesso remoto sem criptografia e considerado obsoleto por insegurança.

---

# 19. Firewall e ACL

## Firewall

Analisa o tráfego e permite ou bloqueia pacotes com base em regras.

Pode analisar:

* IP de origem
* IP de destino
* Porta
* Protocolo

## ACL

**Access Control List**

Lista ordenada de regras de:

* Permissão
* Negação

Pode ser aplicada em:

* Roteadores
* Switches

## Princípio

> Negar tudo por padrão e liberar explicitamente apenas o necessário.

---

# 20. VLAN e Segmentação

**VLAN — Virtual LAN**

Divide uma rede física em várias redes lógicas isoladas.

Exemplo:

```text
VLAN de convidados
VLAN administrativa
VLAN de servidores
```

## Benefícios

* Isolamento
* Redução da superfície de ataque
* Limitação do movimento lateral
* Organização da rede
* Redução de tráfego de broadcast

---

# 21. Segurança Wi-Fi

## Rede aberta

Sem senha.

O tráfego pode ser capturado por pessoas próximas.

## WPA2

* Padrão consolidado.
* Utiliza criptografia.
* Senhas fracas ainda podem ser atacadas.

## WPA3

* Sucessor do WPA2.
* Possui proteção adicional contra tentativas offline de quebra de senha.
* Utiliza criptografia individualizada por sessão.

---

# 22. Ataques Comuns de Rede

## Sniffing

Captura passiva do tráfego de rede.

Ferramenta mencionada:

```text
Wireshark
```

## Spoofing

Falsificação de identidade.

Exemplos:

* IP Spoofing
* ARP Spoofing

## Man-in-the-Middle — MITM

O atacante se posiciona entre duas partes e pode:

* Interceptar comunicação
* Alterar comunicação

## DoS/DDoS

Sobrecarrega um serviço com requisições para torná-lo indisponível.

Afeta principalmente:

> **Disponibilidade**

---

# 23. Caso Real — Mirai Botnet

Em **2016**, a Mirai infectou centenas de milhares de:

* Câmeras
* Roteadores
* Dispositivos IoT

A infecção explorava principalmente:

> **Usuários e senhas padrão de fábrica que não haviam sido alterados.**

Os dispositivos formaram uma **botnet** utilizada em ataques DDoS.

Um dos alvos foi a **Dyn**, provedora de DNS.

### Principal lição

> Serviços expostos e credenciais padrão podem permitir grandes ataques sem necessidade de técnicas sofisticadas.

---

# 24. Pentest — Teste de Invasão

Um teste de invasão deve ser realizado de maneira **autorizada e controlada**.

## Relação com as camadas estudadas

### Reconhecimento

Mapear:

* IPs
* Sub-redes
* Hosts ativos

### Varredura de portas

Descobrir:

* Portas TCP abertas
* Portas UDP abertas

### Enumeração de serviços

Identificar:

* Aplicação
* Serviço
* Versão

### Relatório

Documentar:

* Resultados
* Evidências
* Vulnerabilidades
* Recomendações

---

# 25. Fases de um Teste de Invasão

## 1. Planejamento e acordo

Define:

* Escopo
* Horários
* O que pode ser testado
* O que não pode ser testado
* Autorização formal

## 2. Reconhecimento

Coleta informações sobre o alvo.

## 3. Varredura e enumeração

Mapeia:

* Portas
* Serviços
* Vulnerabilidades potenciais

## 4. Exploração

Tenta utilizar uma vulnerabilidade de maneira controlada.

## 5. Pós-exploração

Avalia até onde o acesso obtido poderia chegar.

## 6. Relatório

Documenta:

* Falhas
* Evidências
* Recomendações de correção

```text
Planejamento
      ↓
Reconhecimento
      ↓
Varredura / Enumeração
      ↓
Exploração
      ↓
Pós-exploração
      ↓
Relatório
```

---

# 26. Tipos de Teste de Invasão

| Tipo          | Informação recebida       |
| ------------- | ------------------------- |
| **Black Box** | Nenhuma informação prévia |
| **Grey Box**  | Informações parciais      |
| **White Box** | Informações completas     |

## Black Box

Simula um atacante externo começando do zero.

## Grey Box

O testador recebe informações parciais.

Exemplo:

* Uma conta de usuário comum.

## White Box

O testador recebe informações completas.

Exemplos:

* Topologia da rede
* Código-fonte
* Credenciais

---

# 27. Aspectos Legais

> **Testar redes e sistemas sem autorização formal é crime.**

A aula menciona:

* **Lei 12.737/2012 — Lei Carolina Dieckmann**
* **Código Penal**

Um teste profissional precisa de:

* Autorização por escrito
* Escopo definido
* Regras de execução

A prática da disciplina deve ocorrer em:

> **Laboratórios controlados e autorizados.**

---

# 30. Glossário da Aula

| Termo            | Significado                                                |
| ---------------- | ---------------------------------------------------------- |
| **LAN**          | Rede local                                                 |
| **WAN**          | Rede de longa distância                                    |
| **TCP/IP**       | Suíte de protocolos utilizada para comunicação entre redes |
| **Porta**        | Identifica um serviço dentro de um host                    |
| **IP**           | Identificador lógico de um host                            |
| **Máscara/CIDR** | Define a parte do endereço que identifica a rede           |
| **NAT**          | Traduz IP privado para IP público                          |
| **Firewall**     | Controla o tráfego de entrada e saída                      |
| **ACL**          | Lista de regras de permissão e negação                     |
| **VLAN**         | Segmentação lógica de uma rede física                      |
| **MITM**         | Interceptação de comunicação                               |
| **Spoofing**     | Falsificação de identidade                                 |
| **Black Box**    | Teste sem informações prévias                              |
| **Grey Box**     | Teste com informações parciais                             |
| **White Box**    | Teste com informações completas                            |

---

# 32. Fórmulas da Aula

```text
Bits de host = 32 - CIDR

Hosts utilizáveis = 2^(bits de host) - 2

Sub-redes = 2^(bits emprestados)
```

## Exemplo

```text
/27

32 - 27 = 5 bits de host

2^5 - 2 = 30 hosts utilizáveis

Máscara:
255.255.255.224

