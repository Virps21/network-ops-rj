# Lab 01 — VLAN + Trunk + Inter-VLAN (Router-on-a-stick)

## Objetivo
Configurar duas VLANs (**10 e 20**), trunk entre switches e roteamento entre VLANs via subinterfaces no roteador (router-on-a-stick).

## Topologia
- 2x Switch: SW1, SW2 (2960-24TT)
- 1x Router: R1 (1941)
- 2x PCs: PC10 (VLAN10), PC20 (VLAN20)

## Cabeamento (portas usadas)
- PC10 Fa0 → SW2 Fa0/1
- PC20 Fa0 → SW2 Fa0/2
- SW2 Fa0/24 ↔ SW1 Fa0/24 (TRUNK)
- SW1 Fa0/1 ↔ R1 G0/0 (TRUNK)

## Endereçamento
- VLAN10: 192.168.10.0/24
  - Gateway: 192.168.10.1
  - PC10: 192.168.10.10
- VLAN20: 192.168.20.0/24
  - Gateway: 192.168.20.1
  - PC20: 192.168.20.20

## Passo a passo (resumo)
1. Criar VLANs 10 e 20 nos switches
2. Colocar portas de acesso:
   - SW2 Fa0/1 → VLAN10
   - SW2 Fa0/2 → VLAN20
3. Configurar trunks:
   - SW2 Fa0/24 ↔ SW1 Fa0/24
   - SW1 Fa0/1 ↔ R1 G0/0
4. Criar subinterfaces no R1:
   - G0/0.10 com `encapsulation dot1q 10` e IP 192.168.10.1/24
   - G0/0.20 com `encapsulation dot1q 20` e IP 192.168.20.1/24
5. Testar conectividade PC10 ↔ PC20

## Comandos de verificação
### SW1 / SW2
- `show vlan brief`
- `show interfaces trunk`

### R1
- `show ip interface brief`
- `show running-config | section interface`

## Testes realizados
- PC10 → ping 192.168.10.1 (gateway VLAN10)
- PC10 → ping 192.168.20.1 (gateway VLAN20)
- PC10 → ping 192.168.20.20 (PC20)
- PC20 → ping 192.168.10.10 (PC10)

## Problemas encontrados e correções
- **STP bloqueou o trunk** (mensagem de “inconsistent port type / native vlan”).
  - Correção: permitir VLAN nativa (1) junto com 10 e 20 nos trunks:
  - `switchport trunk allowed vlan 1,10,20`

## Evidências
- Print da topologia
- Prints dos pings
- Outputs:
  - `show interfaces trunk` (SW1 e SW2)
  - `show ip interface brief` (R1)
