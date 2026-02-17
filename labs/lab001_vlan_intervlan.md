# Lab 01 - VLAN + Trunk + Inter-VLAN (Router-on-a-stick)

## Objetivo 
Configurar duas VLANs (10 a 20), trunk entre switches e roteamento entre VLANs via subinterfaces no roteador.

## Topologia
- 2x Swith (SW1, SW2)
- 1x Router (R1)
- 2x PCs (PC10 na VLAN 10, PC20 na VLAN 20)

## Endereçamento 
- VLAN10: 192.168.10.0/24
  - Gateway: 192.168.10.1
  - PC10: 192.168.10.10
- VLAN20: 192.168.20.0/24
  - Gateway: 192.168.20.1
  - PC20: 192.168.20.20

# Passo a Passo (resumo)
1. Criar VLANs 10 e 20 nos switches
2. Colocar portas de acesso dos PCs nas VLANs corretas
3. Configurar trunk entre SW1 <-> SW2 e SW1 <-> R1
4. Criar subinterfaces no R1
   - G0/0.10 com encapsulation dot1q 10 e IP 192.168.10.1
   - G0/0.20 com encapsulation dot1q 20 e IP 192.168.20.1
5. Testar conectividade PC10 <-> PC20

## Comando de verificação (colar outputs)
### SW1 / SW2
- `show vlan brief`
- `show interfaces trunk`

### R1
- `show ip interface brief`
- `show running-config | sextion interface`

## Testes
- Ping PC10 -> 192.168.10.1 (gateway)
- Ping PC20 -> 192.168.20.1 (gateway)
- Ping PC10 -> PC20 (192.168.20.20)

## Problemas encontrados
(em breve)

## Evidências
- print da topologia
- Prints dos pings funcionando
