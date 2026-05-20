# VPN e Roteamento Estático — MikroTik PPTP

Laboratório simulado no **EVE-NG** com roteadores **MikroTik**, demonstrando a configuração de um túnel VPN PPTP entre duas redes remotas e roteamento estático bidirecional.

---

## Objetivo

Interligar duas redes distintas (Matriz e Filial) através de um túnel PPTP, permitindo comunicação end-to-end entre os dispositivos de cada rede via roteamento estático.

---

## Tecnologias

- **Simulador:** EVE-NG (VMware)
- **Roteadores:** MikroTik RouterOS
- **VPN:** PPTP (Point-to-Point Tunneling Protocol)
- **Roteamento:** Estático (rotas manuais via túnel)
- **Diagrama:** Draw.io

---

## Topologia

```
[Network Matriz]              [Network Filial]
192.168.136.129/24            192.168.136.135/24
       |                             |
    [Matriz]                      [Filial]
  PPTP Server                  PPTP Client
  10.30.10.1/32  <-- Túnel -->  10.30.10.100/32
  192.168.1.1/24                10.10.10.1/24
       |                             |
   [Linux]                        [VPC]
192.168.1.200/24              10.10.10.200/24
```

---

## Endereçamento

| Dispositivo | Interface     | Endereço IP          | Função              |
|-------------|---------------|----------------------|---------------------|
| Matriz      | ether1 (WAN)  | 192.168.136.129/24   | Simulação de WAN    |
| Matriz      | ether2 (LAN)  | 192.168.1.1/24       | Gateway LAN         |
| Matriz      | pptp-vpn      | 10.30.10.1/32        | Túnel VPN           |
| Filial      | ether1 (WAN)  | 192.168.136.135/24   | Simulação de WAN    |
| Filial      | ether2 (LAN)  | 10.10.10.1/24        | Gateway LAN         |
| Filial      | pptp-matriz   | 10.30.10.100/32      | Túnel VPN           |
| Linux       | ether0        | 192.168.1.200/24     | End device Matriz   |
| VPC         | ether0        | 10.10.10.200/24      | End device Filial   |

---

## Testes Realizados

| Teste | Resultado |
|-------|-----------|
| Servidor PPTP ativo (Matriz) | ✔ OK |
| Cliente PPTP conectado (Filial) | ✔ OK |
| IPs do túnel atribuídos corretamente | ✔ OK |
| Rota estática Matriz → 10.10.10.0/24 | ✔ OK |
| Rota estática Filial → 192.168.1.0/24 | ✔ OK |
| Linux → Gateway Matriz (192.168.1.1) | ✔ OK |
| VPC → Gateway Filial (10.10.10.1) | ✔ OK |
| Linux → VPC pelo túnel (10.10.10.200) | ✔ OK |
| VPC → Linux pelo túnel (192.168.1.200) | ✔ OK |

---

## Estrutura do Repositório

```
