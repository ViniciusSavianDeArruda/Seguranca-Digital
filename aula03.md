# Segurança de Redes — Aula 03

## Protocolos de Rede e NAT

---

## 1. Protocolos de rede

Protocolos de rede definem como os dispositivos se comunicam e trocam informações.

### Principais protocolos

| Protocolo | Porta | Transporte | Função                         |
| --------- | ----: | ---------- | ------------------------------ |
| HTTP      |    80 | TCP        | Navegação web                  |
| HTTPS     |   443 | TCP        | Navegação web com criptografia |
| DNS       |    53 | TCP/UDP    | Traduz nomes de domínio em IP  |
| SSH       |    22 | TCP        | Acesso remoto administrativo   |
| FTP       | 20/21 | TCP        | Transferência de arquivos      |
| SMTP      |    25 | TCP        | Envio de e-mails               |
| POP3      |   110 | TCP        | Recebimento de e-mails         |
| IMAP      |   143 | TCP        | Acesso a e-mails               |
| DHCP      | 67/68 | UDP        | Atribuição automática de IP    |

---

# 2. DHCP

**DHCP (Dynamic Host Configuration Protocol)** é responsável por fornecer automaticamente configurações de rede para os dispositivos.

Um dispositivo normalmente recebe:

* Endereço IP
* Máscara de sub-rede
* Gateway
* Servidor DNS

## Processo DORA

O processo de obtenção do endereço IP ocorre em quatro etapas:

### 1. Discover

O dispositivo envia um broadcast procurando um servidor DHCP.

### 2. Offer

O servidor DHCP oferece um endereço IP disponível, junto com outras configurações.

### 3. Request

O dispositivo solicita formalmente o endereço oferecido.

### 4. Acknowledge

O servidor confirma a concessão do endereço.

**DORA = Discover → Offer → Request → Acknowledge**

O endereço recebido pelo dispositivo geralmente pertence a uma faixa privada.

---

# 3. Endereços IP válidos e inválidos

Nem todo endereço IPv4 pode ser utilizado diretamente na internet.

## Endereço público

É um endereço:

* Roteável pela internet
* Globalmente único
* Utilizado para comunicação entre redes pela internet
* Atribuído a provedores e organizações

Um servidor que precisa ser acessado diretamente pela internet precisa de um endereço público ou de algum mecanismo de encaminhamento.

## Endereço privado

É um endereço utilizado internamente em redes locais.

Ele:

* Não é roteável diretamente pela internet pública
* Pode ser utilizado simultaneamente em várias redes diferentes
* Normalmente precisa ser traduzido por NAT para acessar a internet

---

# 4. Faixas de endereços reservados

As principais faixas privadas definidas pela **RFC 1918** são:

| Faixa                           | CIDR  | Uso            |
| ------------------------------- | ----- | -------------- |
| `10.0.0.0 – 10.255.255.255`     | `/8`  | Redes privadas |
| `172.16.0.0 – 172.31.255.255`   | `/12` | Redes privadas |
| `192.168.0.0 – 192.168.255.255` | `/16` | Redes privadas |

Existem também outras faixas de uso especial:

| Faixa                           | CIDR  | Uso                |
| ------------------------------- | ----- | ------------------ |
| `127.0.0.0 – 127.255.255.255`   | `/8`  | Loopback           |
| `169.254.0.0 – 169.254.255.255` | `/16` | Link-local / APIPA |

### Loopback

O endereço mais conhecido é:

```text
127.0.0.1
```

Ele representa o próprio computador.

### Link-local / APIPA

A faixa `169.254.0.0/16` pode ser atribuída automaticamente quando um dispositivo não consegue obter um endereço através do DHCP.

---

# 5. Por que IP privado não funciona diretamente na internet?

Um endereço como:

```text
192.168.0.5
```

é privado e não pode ser roteado diretamente pela internet pública.

Os roteadores da internet não encaminham normalmente pacotes destinados ou originados dessas faixas privadas.

Portanto, um computador com:

```text
192.168.0.5
```

precisa passar por um dispositivo de borda, normalmente um roteador, que irá modificar o endereço antes de enviá-lo para a internet.

Esse processo é realizado pelo **NAT**.

---

# 6. NAT

**NAT (Network Address Translation)** é uma técnica utilizada para traduzir endereços IP.

O NAT normalmente funciona em um:

* Roteador
* Firewall
* Gateway
* Equipamento de borda da rede

Ele permite que dispositivos com endereços privados acessem a internet utilizando um ou mais endereços públicos.

### Exemplo

Uma rede pode possuir:

```text
PC       → 192.168.1.10
Notebook → 192.168.1.11
Celular  → 192.168.1.12
```

Todos podem acessar a internet utilizando um único endereço público:

```text
203.0.113.7
```

---

# 7. Como o NAT funciona

Quando um dispositivo interno acessa a internet, o roteador modifica as informações do pacote.

### Antes do NAT

```text
IP origem:      192.168.1.10
Porta origem:   51422
IP destino:     200.150.10.5
```

### Depois do NAT

```text
IP origem:      203.0.113.7
Porta origem:   40001
IP destino:     200.150.10.5
```

O roteador registra essa tradução em uma tabela.

Quando a resposta retorna:

```text
200.150.10.5:80
        ↓
203.0.113.7:40001
```

O roteador consulta sua tabela e descobre que a conexão pertence a:

```text
192.168.1.10:51422
```

Assim, a resposta é encaminhada para o dispositivo correto.

---

# 8. Tabela de tradução do NAT

No NAT, o roteador mantém informações para relacionar conexões internas e externas.

Exemplo:

| IP interno     | Porta interna | IP público    | Porta traduzida |
| -------------- | ------------: | ------------- | --------------: |
| `192.168.1.10` |       `51422` | `203.0.113.7` |         `40001` |
| `192.168.1.11` |       `50110` | `203.0.113.7` |         `40002` |
| `192.168.1.12` |       `51422` | `203.0.113.7` |         `40003` |

Mesmo que dois dispositivos utilizem a mesma porta internamente, o NAT pode atribuir portas externas diferentes.

Isso permite que vários dispositivos compartilhem o mesmo endereço público.

---

# 9. Tipos de NAT

## 9.1 Static NAT

É uma tradução fixa de **um endereço privado para um endereço público**.

```text
IP privado ↔ IP público
```

A associação permanece constante.

### Uso

Pode ser utilizado para servidores internos que precisam ser acessados externamente.

### Desvantagem

Cada endereço privado mapeado precisa de um endereço público.

---

## 9.2 Dynamic NAT

Utiliza um conjunto de endereços públicos, chamado de **pool**.

O roteador atribui temporariamente um endereço público para um host interno.

Exemplo:

```text
Pool público:
203.0.113.10
203.0.113.11
203.0.113.12
```

Quando todos os endereços estiverem ocupados, novos hosts não conseguirão utilizar o NAT até que um endereço seja liberado.

---

## 9.3 PAT / NAT Overload

**PAT (Port Address Translation)** permite que vários dispositivos compartilhem um único endereço público.

O diferencial são as **portas**.

Exemplo:

```text
192.168.1.10:50000
        ↓
203.0.113.7:40001

192.168.1.11:50000
        ↓
203.0.113.7:40002
```

O endereço público é o mesmo, mas as portas externas são diferentes.

### É o tipo mais comum

É utilizado normalmente em:

* Redes domésticas
* Pequenas empresas
* Redes corporativas

Quando falamos simplesmente em "NAT" no uso cotidiano, geralmente estamos falando de PAT/NAT Overload.

---

# 10. NAT de saída e NAT de entrada

## NAT de saída — Outbound

Quando um dispositivo interno inicia uma conexão:

```text
Rede interna → NAT → Internet
```

O roteador cria automaticamente uma tradução e sabe para onde devolver a resposta.

É o funcionamento típico de:

* Navegação web
* Aplicativos
* Downloads
* Serviços online

## NAT de entrada — Inbound

Quando alguém da internet tenta iniciar uma conexão com um dispositivo interno, o NAT normalmente não sabe para qual máquina privada deve encaminhar o tráfego.

Por isso, a conexão é geralmente descartada.

```text
Internet → NAT → X
```

Para permitir esse acesso, é necessária uma configuração específica.

---

# 11. Port Forwarding

**Port Forwarding** é uma regra que encaminha uma porta pública para um dispositivo interno.

Exemplo:

```text
IP público: porta 80
        ↓
192.168.1.20:8080
```

Ou seja:

```text
203.0.113.7:80
        ↓
192.168.1.20:8080
```

É utilizado para expor serviços específicos, como:

* Servidores web
* Servidores de jogos
* Câmeras
* Outros serviços internos

A regra deve ser criada explicitamente pelo administrador.

---

# 12. DMZ

Uma **DMZ (Demilitarized Zone)**, no contexto de roteadores domésticos, pode ser configurada para encaminhar para um determinado host o tráfego que não corresponde a outras regras.

Na prática, isso deixa esse equipamento muito mais exposto à internet.

Por isso:

> DMZ deve ser utilizada com muito cuidado e não deve ser considerada substituta de um firewall.

---

# 13. Problemas causados pelo NAT

Embora o NAT seja muito útil, ele pode causar dificuldades para aplicações que precisam receber conexões diretamente.

## P2P

Em sistemas peer-to-peer, os participantes precisam conseguir estabelecer conexões entre si.

Hosts atrás de NAT podem ter dificuldade para receber conexões diretamente.

## VoIP e videochamadas

Alguns protocolos podem transportar informações de IP dentro dos próprios dados.

O NAT pode ter dificuldade para interpretar e modificar essas informações corretamente.

## Jogos online

Jogos que utilizam conexões P2P podem precisar que jogadores recebam conexões externas.

Por isso, alguns jogos podem exigir:

* NAT traversal
* Port forwarding
* Configurações específicas no roteador

---

# 14. NAT Traversal

**NAT Traversal** reúne técnicas utilizadas para permitir comunicação entre dispositivos que estão atrás de NAT.

As principais técnicas estudadas são:

## STUN

**Session Traversal Utilities for NAT**

Permite descobrir:

* Qual endereço público está sendo utilizado
* Qual porta pública está sendo utilizada

Um servidor STUN informa ao dispositivo como ele está sendo visto externamente.

---

## TURN

**Traversal Using Relays around NAT**

É utilizado quando não é possível estabelecer uma conexão direta.

Nesse caso, um servidor intermediário retransmite o tráfego.

```text
Dispositivo A
      ↓
   Servidor TURN
      ↓
Dispositivo B
```

---

## ICE

**Interactive Connectivity Establishment**

É um mecanismo que testa diferentes possibilidades de conexão e escolhe a que funcionar melhor.

Pode utilizar:

* Conexão direta
* STUN
* TURN

É utilizado, por exemplo, pelo **WebRTC** em aplicações de comunicação em tempo real.

---

# 15. NAT e segurança

O NAT possui um efeito positivo para a segurança, mas **não é um mecanismo de segurança completo**.

## O que o NAT ajuda a resolver

### Ocultação da rede interna

Um dispositivo externo normalmente não consegue endereçar diretamente um host privado.

Por exemplo, um atacante externo não consegue simplesmente acessar:

```text
192.168.1.10
```

pela internet.

Ele normalmente enxerga apenas o endereço público do roteador.

Isso dificulta o reconhecimento direto da rede interna.

## O que o NAT não resolve

NAT não:

* Detecta malware
* Identifica ataques
* Autentica usuários
* Substitui firewall
* Faz análise completa dos pacotes
* Garante que o tráfego seja seguro

Por isso, NAT deve ser utilizado junto com controles de segurança, principalmente **firewalls e ACLs**.

---

# 16. CGNAT

**CGNAT (Carrier-Grade NAT)** é quando o próprio provedor de internet utiliza NAT para compartilhar um endereço público entre vários clientes.

### NAT tradicional

```text
Dispositivos
     ↓
Roteador
     ↓
IP público
     ↓
Internet
```

### CGNAT

```text
Dispositivos
     ↓
Roteador do cliente
     ↓
CGNAT do provedor
     ↓
IP público compartilhado
     ↓
Internet
```

Ou seja, existe uma camada adicional de NAT.

---

# 17. Consequências do CGNAT

O CGNAT é utilizado principalmente por causa da escassez de endereços IPv4.

Um único endereço público pode ser compartilhado por muitos clientes.

### Problema para o usuário

Serviços que precisam aceitar conexões diretamente da internet podem apresentar dificuldades.

Exemplos:

* Servidores próprios
* Câmeras
* Jogos
* Serviços hospedados em casa

Mesmo configurando Port Forwarding no roteador, o acesso pode não funcionar porque existe outro NAT no provedor.

### Problema para investigações

Vários clientes podem aparecer utilizando o mesmo endereço público.

Para identificar uma conexão específica, pode ser necessário utilizar:

* IP público
* Porta de origem
* Horário exato
* Logs de tradução do provedor

---

# 18. IPv6 e NAT

O NAT surgiu principalmente para ajudar a lidar com a escassez de endereços IPv4.

O IPv4 possui aproximadamente:

```text
4,3 bilhões de endereços
```

O IPv6 possui uma quantidade muito maior de endereços:

```text
128 bits
```

Com IPv6, cada dispositivo pode receber seu próprio endereço globalmente único.

Portanto, o NAT deixa de ser necessário para solucionar a escassez de endereços.

### Importante

Mesmo com IPv6, a segurança continua sendo necessária.

O controle principal deve ser feito por:

* Firewall
* Regras de acesso
* Segmentação
* Autenticação
* Outros mecanismos de segurança

NAT não deve ser confundido com firewall.

---

# 19. NAT e testes de invasão

O NAT influencia diretamente o reconhecimento de uma rede.

Em um teste **Black Box**, o testador normalmente começa observando o que está disponível externamente.

O NAT pode esconder:

```text
Rede interna
192.168.x.x
10.x.x.x
172.16.x.x
```

e apresentar externamente apenas:

```text
IP público
```

## Serviços expostos

O que normalmente pode ser alcançado externamente são serviços configurados através de:

* Port Forwarding
* DMZ
* Outros mecanismos de exposição

Esses serviços podem representar os primeiros pontos analisados em um teste autorizado.

## Após obter acesso interno

Se o testador autorizado conseguir acesso a um host dentro da rede, ele passa a estar atrás do NAT.

A partir desse ponto, pode analisar a rede interna dentro do escopo autorizado.

---

# 20. Ferramentas de reconhecimento

## traceroute / tracert

Utilizado para descobrir o caminho percorrido pelos pacotes até um destino.

No Linux:

```bash
traceroute exemplo.com
```

No Windows:

```cmd
tracert exemplo.com
```

### Funcionamento

A ferramenta utiliza valores crescentes de **TTL** para identificar os roteadores existentes no caminho.

Pode ajudar a identificar:

* Saltos da rede
* Roteadores intermediários
* Possíveis pontos de NAT

### Limitação

Firewalls podem bloquear ICMP ou outros tipos de resposta, fazendo com que alguns saltos não apareçam.

---

# 21. nslookup e dig

São ferramentas utilizadas para consultar informações de **DNS**.

### nslookup

Exemplo:

```bash
nslookup exemplo.com
```

### dig

Exemplo:

```bash
dig exemplo.com
```

Podem ajudar a descobrir:

* Endereço IP de um domínio
* Servidores DNS
* Registros MX
* Registros NS
* Informações relacionadas à infraestrutura pública

Também podem revelar subdomínios e serviços expostos, dependendo dos registros disponíveis.

---

# 22. whois

O **WHOIS** permite consultar informações públicas relacionadas a:

* Domínios
* Blocos de endereços IP
* Servidores de nome
* Datas de registro

Atualmente, informações de IP também podem ser consultadas através de **RDAP**.

### Privacidade

Muitos domínios utilizam mecanismos de proteção de privacidade, portanto os dados pessoais do proprietário podem não aparecer publicamente.

---

# 23. Falhas comuns em protocolos

Vulnerabilidades de rede podem surgir quando o comportamento real de um protocolo permite situações que não deveriam ocorrer.

## Confiança implícita

Protocolos como:

* ARP
* DHCP

possuem mecanismos que podem confiar em informações recebidas dentro da rede.

Isso pode possibilitar ataques de **spoofing** em determinados cenários.

## Ausência de criptografia

Protocolos antigos ou inseguros podem transmitir informações sem criptografia.

Exemplos:

* Telnet
* FTP
* HTTP

Isso pode permitir que informações sejam capturadas por alguém capaz de observar o tráfego.

## Serviços expostos

Serviços administrativos diretamente acessíveis pela internet aumentam a superfície de ataque.

Exemplos:

* RDP
* SSH
* Painéis administrativos

Por isso, exposição de serviços deve ser controlada através de mecanismos como:

* Firewall
* ACL
* VPN
* Autenticação forte
* Restrição de origem

---

# 24. Resumo para memorizar

## DHCP

```text
D → Discover
O → Offer
R → Request
A → Acknowledge
```

Serve para configurar automaticamente dispositivos na rede.

## IP privado

Não é roteável diretamente na internet.

Principais faixas:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

## NAT

Traduz endereços privados para endereços públicos.

```text
IP privado → NAT → IP público
```

## Static NAT

```text
1 privado ↔ 1 público
```

Mapeamento fixo.

## Dynamic NAT

```text
Privado → pool de IPs públicos
```

Mapeamento temporário.

## PAT / NAT Overload

```text
Vários privados → 1 IP público
```

Diferencia as conexões através das portas.

## Port Forwarding

Permite que uma porta pública seja encaminhada para um serviço interno específico.

## DMZ

Expõe um host interno de forma ampla e deve ser usada com cuidado.

## STUN

Descobre como o dispositivo está sendo visto externamente.

## TURN

Usa um servidor intermediário quando a conexão direta não funciona.

## ICE

Testa diferentes possibilidades e escolhe uma rota de comunicação.

## CGNAT

NAT realizado pelo provedor, fazendo vários clientes compartilharem um mesmo IP público.

## Ferramentas

```text
traceroute / tracert → caminho dos pacotes
nslookup / dig       → consultas DNS
whois / RDAP         → informações de domínios e IPs
```

## Ideia central da Aula 03

> **O NAT permite que dispositivos com IPs privados se comuniquem com a internet usando endereços públicos, mas também altera a forma como conexões de entrada, reconhecimento de rede e alguns protocolos funcionam.**
