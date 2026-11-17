# rede-corporativa
Rede corporativa com VLANs, DHCP e ACL no Cisco Packet Tracer.

## Sobre o projeto

Este projeto simula a rede de uma empresa com três departamentos:
Administrativo, Financeiro e TI.

O laboratório foi desenvolvido no Cisco Packet Tracer para
a segmentação de redes, a distribuição automática de endereços IP,
a comunicação entre VLANs e o controle de acesso.

## Ferramenta e equipamentos

- Cisco Packet Tracer
- 1 roteador Cisco 1941
- 2 switches Cisco 2960
- 3 computadores, representando os departamentos da empresa

## Topologia

A rede é composta por um roteador, dois switches e três computadores.
O roteador realiza a comunicação entre as redes dos departamentos.

![Topologia da rede corporativa](imagens/topologia.png)

## Organização da rede

| Setor | VLAN | Rede | Máscara | Gateway |
|---|---:|---|---|---|
| Administrativo | 10 | 192.168.10.0/24 | 255.255.255.0 | 192.168.10.1 |
| Financeiro | 20 | 192.168.20.0/24 | 255.255.255.0 | 192.168.20.1 |
| TI | 30 | 192.168.30.0/24 | 255.255.255.0 | 192.168.30.1 |

### VLANs no SW1

O comando `show vlan brief` mostra as VLANs criadas no SW1 e as portas
associadas aos computadores do Administrativo e do Financeiro.

![VLANs configuradas no SW1](imagens/vlans-sw1.png)

## Configurações realizadas

- Criação de VLANs para separar os departamentos.
- Configuração de portas de acesso para os computadores.
- Configuração de enlaces trunk para transportar as VLANs entre equipamentos.
- Configuração de subinterfaces no roteador para comunicação entre VLANs.
- Configuração de DHCP para distribuir endereços IP automaticamente.
- Criação de uma ACL para bloquear o tráfego do Administrativo
  para o Financeiro.

## Teste de DHCP

O computador do Financeiro recebeu automaticamente o endereço
`192.168.20.11`, a máscara `255.255.255.0` e o gateway `192.168.20.1`.

![Configuração DHCP do computador do Financeiro](imagens/dhcp.png)

O laboratório não utiliza um servidor DNS; os testes abaixo foram
realizados diretamente pelos endereços IP.

## Testes de comunicação

Os testes foram realizados com o comando `ping` no Packet Tracer.

| Teste | Resultado observado |
|---|---|
| Administrativo → Financeiro antes da ACL | Respondeu |
| Administrativo → Financeiro após a ACL | Não respondeu |
| Administrativo → TI após a ACL | Respondeu |
| Administrativo → próprio gateway após a ACL | Respondeu |
| TI → Financeiro | Respondeu |

### Antes da ACL

O computador do Administrativo conseguiu alcançar o gateway,
o computador do Financeiro e o computador da TI.

![Pings do Administrativo antes da ACL](imagens/ping-administrativo-antes-acl.jpeg)

### Após a ACL

O ping do Administrativo para o Financeiro não foi concluído.
Os testes do Administrativo para a TI e para seu gateway receberam resposta.

![Pings do Administrativo após a ACL](imagens/ping-administrativo-apos-acl.jpeg)

### Comunicação da TI com o Financeiro

O computador da TI conseguiu se comunicar com o computador do Financeiro.

![Ping da TI para o Financeiro](imagens/ping-ti-financeiro-permitido.jpeg)

## Aprendizados

- A separação de departamentos por VLANs.
- A configuração de switches e roteador pela CLI.
- O uso de DHCP para distribuição de endereços.
- A criação de uma ACL para controlar o tráfego entre setores.
- A realização e a interpretação de testes de comunicação com ping.

## Como abrir o projeto

1. Baixe o arquivo `.pkt` disponível neste repositório.
2. Abra o Cisco Packet Tracer.
3. Clique em **File → Open** e selecione o arquivo baixado.
