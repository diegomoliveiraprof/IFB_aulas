# Roteiro do Experimento 06

## Desafio de resolução de problemas.

# Soluções dos Problemas

## 1. Computadores da TI não navegam na rede

- **Teste inicial:** renovar o endereço IP e verificar se o IP obtido pertence à rede 192.168.10.0/24.
  
- **Causa provável:** presença de um *Rogue AP* (roteador intruso) distribuindo endereços IP na VLAN 10.
  
- **Soluções possíveis:**
  
  - **Opção 1:** desabilitar portas não utilizadas para evitar que usuários conectem roteadores indevidos.
    
  - **Opção 2:** identificar e desconectar o roteador intruso.
    
  - **Opção 3 (recomendada):** ativar **DHCP Snooping** em todos os switches para prevenir atribuição de endereços IP não autorizados.
    
- **Teste final:** após aplicar a solução, renovar IP novamente e confirmar que o endereço pertence à rede correta.
  

## 2. Impressoras inacessíveis

- **Teste inicial:** ping para os endereços das impressoras (192.168.40.10–12).
  
- **Causa provável:** o Switch0 (core) não possui a VLAN 40 configurada.
  
- **Solução:** criar a VLAN 40 no Switch0, mesmo sem portas atribuídas, garantindo que o tráfego seja roteado corretamente.
  
- **Teste final:** ping para as impressoras deve responder normalmente.
  

## 3. Link Aggregation / EtherChannel entre Switch0 e Switch3 não funciona

- **Teste inicial:** executar `show interfaces port-channel 3` → deve indicar `Port-channel3 is up`.
  
- **Causa provável:** cabo conectado em portas diferentes das configuradas para o EtherChannel.
  
- **Solução:** verificar quais portas foram configuradas no `channel-group 3` e reconectar os cabos nas portas corretas.
  
- **Teste final:** `show etherchannel summary` deve mostrar o canal ativo (estado **SU**).
  

## 4. Switch3 inacessível via SSH ou ping

- **Teste inicial:** ping para o IP de gerência (192.168.10.5) ou tentativa de acesso via `ssh -l admin 192.168.10.5`.
  
- **Causa provável:** endereço IP de gerência na VLAN 10 não foi configurado.
  
- **Solução:** configurar IP e gateway na interface VLAN 10 do Switch3 conforme documentação:
  
  bash
  
  ```
  interface vlan 10 ip address 192.168.10.5 255.255.255.0 no shutdown
  exit
  ip default-gateway 192.168.10.1
  ```
  
- **Teste final:** ping e acesso SSH devem funcionar corretamente.
