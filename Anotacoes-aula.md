# Segurança de Redes — Resumo das Aulas 01, 02 e 03

## Aula 01 — Fundamentos de Segurança

### Tríade CIA

* **Confidencialidade:** somente pessoas autorizadas podem acessar.
* **Integridade:** os dados não podem ser alterados indevidamente.
* **Disponibilidade:** sistemas e dados devem estar disponíveis quando necessários.

### Conceitos importantes

| Termo               | Significado                                               |
| ------------------- | --------------------------------------------------------- |
| **Ativo**           | Algo que precisa ser protegido.                           |
| **Ameaça**          | Algo que pode causar dano.                                |
| **Vulnerabilidade** | Fraqueza que pode ser explorada.                          |
| **Risco**           | Possibilidade de uma ameaça explorar uma vulnerabilidade. |
| **Controle**        | Medida usada para diminuir o risco.                       |

### Defesa em profundidade

Utiliza várias camadas de segurança.

```text
Firewall
   ↓
Antivírus
   ↓
MFA
   ↓
Controle de acesso
```

Se uma proteção falhar, outra pode impedir o ataque.

### Zero Trust

> Nunca confie automaticamente. Sempre verifique.

---

# Aula 02 — Segurança de Redes

## Etapas básicas de uma invasão

```text
Reconhecimento
      ↓
Enumeração
      ↓
Exploração
```

### Reconhecimento

Busca informações sobre o alvo:

* IPs
* Hosts
* Serviços
* Sistemas

### Enumeração

Busca informações mais detalhadas:

* Portas
* Protocolos
* Usuários
* Versões

### Exploração

Tentativa de utilizar uma vulnerabilidade para obter acesso.

Essas técnicas devem ser utilizadas somente em ambientes autorizados.

---

## Senhas

### Boas práticas

* Usar senhas longas.
* Não reutilizar senhas.
* Ativar MFA.
* Utilizar gerenciador de senhas.

### Principais ataques

| Ataque                  | Como funciona                               |
| ----------------------- | ------------------------------------------- |
| **Phishing**            | Engana o usuário para obter informações.    |
| **Brute Force**         | Testa várias combinações.                   |
| **Password Spray**      | Testa senhas comuns contra vários usuários. |
| **Credential Stuffing** | Usa senhas vazadas em outros serviços.      |
| **Dicionário**          | Testa palavras e combinações conhecidas.    |

---

## LAN e WAN

### LAN

Rede local.

Exemplo:

```text
Computadores de uma empresa
```

### WAN

Interliga redes distantes.

Exemplo:

```text
Internet
```

---

# Modelo TCP/IP

O modelo TCP/IP possui quatro camadas:

| Camada            | Função                              | Exemplos             |
| ----------------- | ----------------------------------- | -------------------- |
| **Aplicação**     | Serviços utilizados pelos programas | HTTP, DNS, SSH       |
| **Transporte**    | Comunicação entre processos         | TCP, UDP             |
| **Internet**      | Endereçamento e roteamento          | IP, ICMP             |
| **Acesso à Rede** | Comunicação física e local          | Ethernet, Wi-Fi, ARP |

### Para memorizar

```text
Aplicação
    ↓
Transporte
    ↓
Internet
    ↓
Acesso à Rede
```

---

# Protocolos importantes

| Protocolo  | Porta | Função                         |
| ---------- | ----: | ------------------------------ |
| **HTTP**   |    80 | Web                            |
| **HTTPS**  |   443 | Web com criptografia           |
| **SSH**    |    22 | Acesso remoto seguro           |
| **DNS**    |    53 | Nome para IP                   |
| **FTP**    | 20/21 | Transferência de arquivos      |
| **DHCP**   | 67/68 | Configuração automática de IP  |
| **RDP**    |  3389 | Acesso remoto Windows          |
| **Telnet** |    23 | Acesso remoto sem criptografia |

### Atenção

* HTTPS é mais seguro que HTTP.
* SSH é preferível ao Telnet.
* Serviços expostos à Internet aumentam a superfície de ataque.

---

# TCP x UDP

## TCP

* Confiável.
* Orientado à conexão.
* Garante ordem.
* Garante entrega.

Three-way handshake:

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```

## UDP

* Mais rápido.
* Não garante entrega.
* Não garante ordem.
* Não estabelece conexão.

### Para memorizar

> TCP = confiabilidade
> UDP = velocidade

---

# IP

## IPv4

Possui 32 bits.

Exemplo:

```text
192.168.1.10
```

## IPv6

Possui 128 bits.

Exemplo:

```text
2001:db8::1
```

---

# IP Privado

Principais faixas:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

São utilizados dentro de redes privadas.

> IP privado não é roteável diretamente pela Internet pública.

---

# Sub-redes e CIDR

Exemplo:

```text
192.168.1.10/24
```

O `/24` indica o tamanho da parte da rede.

### Regra

> Quanto maior o número do CIDR, menor a quantidade de hosts.

### Fórmulas

```text
Bits de host = 32 - CIDR

Hosts utilizáveis = 2^bits - 2
```

### Exemplo /26

```text
32 - 26 = 6 bits

2⁶ - 2 = 62 hosts
```

---

# NAT

**NAT = Network Address Translation**

Traduz um endereço IP privado para um endereço público.

```text
Computador
192.168.1.10
      ↓
     NAT
      ↓
IP público
      ↓
Internet
```

### Funções

* Economizar endereços IPv4.
* Permitir que vários dispositivos compartilhem um IP público.
* Dificultar o acesso direto aos hosts internos.

> NAT não é firewall.

---

# Tipos de NAT

## Static NAT

```text
1 privado ↔ 1 público
```

Mapeamento fixo.

## Dynamic NAT

```text
IP privado → pool de IPs públicos
```

Utiliza temporariamente um endereço de um conjunto disponível.

## PAT / NAT Overload

```text
Vários IPs privados
        ↓
  1 IP público
```

Utiliza portas diferentes para identificar as conexões.

É o tipo mais comum em redes domésticas.

---

# Port Forwarding

Encaminha uma porta pública para um dispositivo interno.

```text
IP público:80
      ↓
192.168.1.20:8080
```

Pode ser usado para disponibilizar serviços internos externamente.

---

# Firewall

Controla o tráfego da rede.

Pode analisar:

* IP de origem.
* IP de destino.
* Porta.
* Protocolo.

### Regra importante

> Negar por padrão e liberar somente o necessário.

---

# ACL

**ACL = Access Control List**

Lista de regras que permite ou bloqueia tráfego.

Pode ser utilizada em:

* Roteadores.
* Switches.

---

# VLAN

**VLAN = Virtual LAN**

Divide uma rede física em redes lógicas.

Exemplo:

```text
VLAN 10 → Funcionários
VLAN 20 → Visitantes
VLAN 30 → Servidores
```

### Benefícios

* Isolamento.
* Maior segurança.
* Redução do movimento lateral.
* Organização da rede.

---

# Segurança Wi-Fi

### Rede aberta

Não possui senha e oferece pouca proteção.

### WPA2

Utiliza criptografia e é amplamente utilizado.

### WPA3

É mais moderno e oferece proteções adicionais.

> Prefira WPA2 ou WPA3 em vez de uma rede aberta.

---

# Ataques de Rede

## Sniffing

Captura de tráfego da rede.

Ferramenta:

```text
Wireshark
```

## Spoofing

Falsificação de identidade.

Exemplos:

* IP Spoofing.
* ARP Spoofing.

## MITM

**Man-in-the-Middle**

O atacante fica entre duas partes para tentar interceptar ou alterar a comunicação.

## DoS / DDoS

Sobrecarrega um serviço para deixá-lo indisponível.

Afeta principalmente:

> Disponibilidade.

---

# Mirai Botnet

Em 2016, a Mirai infectou muitos dispositivos IoT, como:

* Câmeras.
* Roteadores.
* Outros dispositivos conectados.

Um dos principais problemas explorados eram:

> Usuários e senhas padrão de fábrica.

Os dispositivos foram utilizados em ataques DDoS.

### Principal lição

> Nunca deixe senhas padrão em dispositivos conectados à rede.

---

# Pentest

**Pentest = Teste de Invasão**

É uma avaliação de segurança realizada de forma autorizada e controlada.

### Etapas

```text
Planejamento
     ↓
Reconhecimento
     ↓
Varredura
     ↓
Enumeração
     ↓
Exploração
     ↓
Pós-exploração
     ↓
Relatório
```

### Tipos

| Tipo          | Informação                |
| ------------- | ------------------------- |
| **Black Box** | Nenhuma informação prévia |
| **Grey Box**  | Informações parciais      |
| **White Box** | Informações completas     |

---

# Aspectos Legais

Nunca teste sistemas sem autorização.

Um pentest profissional precisa de:

* Autorização.
* Escopo.
* Regras de execução.
* Ambiente controlado.

> Testes de segurança devem ser realizados somente em sistemas autorizados.

---

# Aula 03 — DHCP e NAT

## DHCP

**DHCP = Dynamic Host Configuration Protocol**

Configura automaticamente os dispositivos da rede.

Pode fornecer:

* IP.
* Máscara.
* Gateway.
* DNS.

### Processo DORA

```text
D → Discover
O → Offer
R → Request
A → Acknowledge
```

### Para memorizar

> DORA = Discover → Offer → Request → Acknowledge

---

# IP Público x IP Privado

## Público

* Pode ser roteado pela Internet.
* É globalmente único.

## Privado

* Usado dentro da rede.
* Não é roteado diretamente pela Internet.

Faixas:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

---

# NAT na prática

```text
PC
192.168.1.10:50000
       ↓
      NAT
       ↓
203.0.113.7:40001
       ↓
    Internet
```

O NAT mantém uma tabela para saber qual dispositivo interno corresponde a cada conexão.

---

# NAT Traversal

Utilizado quando dispositivos atrás de NAT precisam se comunicar.

### STUN

Descobre como o dispositivo é visto externamente.

### TURN

Utiliza um servidor intermediário.

### ICE

Testa diferentes formas de conexão e escolhe uma que funcione.

### Para memorizar

```text
STUN → descobrir
TURN → intermediário
ICE  → escolher
```

---

# CGNAT

É um NAT realizado pelo provedor de Internet.

```text
Casa
 ↓
Roteador
 ↓
CGNAT
 ↓
Internet
```

Vários clientes podem compartilhar o mesmo IP público.

### Problemas

Pode dificultar:

* Servidores domésticos.
* Câmeras.
* Jogos.
* Port Forwarding.

---

# Ferramentas

| Ferramenta               | Função                                 |
| ------------------------ | -------------------------------------- |
| **Wireshark**            | Analisa tráfego                        |
| **ping**                 | Testa conectividade                    |
| **traceroute / tracert** | Mostra o caminho dos pacotes           |
| **nslookup**             | Consulta DNS                           |
| **dig**                  | Consulta DNS                           |
| **whois / RDAP**         | Consulta informações de domínios e IPs |

---

# Resumo Final

## 1. Tríade CIA

```text
C → Confidencialidade
I → Integridade
A → Disponibilidade
```

## 2. TCP/IP

```text
Aplicação
Transporte
Internet
Acesso à Rede
```

## 3. TCP x UDP

```text
TCP → confiável
UDP → rápido
```

## 4. DHCP

```text
DORA
↓
Discover
Offer
Request
Acknowledge
```

## 5. IP privado

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

## 6. NAT

```text
IP privado → NAT → IP público
```

## 7. PAT

```text
Vários IPs privados → 1 IP público
```

## 8. Pentest

```text
Planejamento
Reconhecimento
Varredura
Enumeração
Exploração
Pós-exploração
Relatório
```

## 9. Tipos de Pentest

```text
Black Box → nenhuma informação
Grey Box  → informação parcial
White Box → informação completa
```

## 10. NAT Traversal

```text
STUN → descobrir
TURN → intermediário
ICE  → escolher
```

---

# Resumo em 10 Frases

1. **CIA** significa Confidencialidade, Integridade e Disponibilidade.
2. **Vulnerabilidade** é uma fraqueza que pode ser explorada.
3. **TCP/IP** organiza a comunicação entre dispositivos e redes.
4. **TCP** prioriza confiabilidade, enquanto **UDP** prioriza velocidade.
5. **DHCP** configura automaticamente os dispositivos usando o processo DORA.
6. **IP privado** é utilizado dentro das redes e não é roteado diretamente pela Internet.
7. **NAT** traduz endereços privados para públicos.
8. **Firewall** controla o tráfego e não deve ser confundido com NAT.
9. **VLANs e sub-redes** ajudam a segmentar e proteger a rede.
10. **Pentest** deve ser realizado somente com autorização e dentro do escopo definido.
