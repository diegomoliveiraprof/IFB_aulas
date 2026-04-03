# Simuladores e Emuladores de Rede

---

## 1. O que são simuladores de rede?
- **Simuladores** são softwares que **imitam o funcionamento de dispositivos e protocolos de rede** em um ambiente virtual.  
- Eles não executam o sistema operacional real dos equipamentos, mas simulam seu comportamento para fins de estudo e prática.  
- Exemplo: **Cisco Packet Tracer**.  

### Utilidades dos simuladores
- Treinar conceitos básicos de redes sem precisar de equipamentos físicos.  
- Criar topologias simples e médias de forma rápida.  
- Ideal para iniciantes e para disciplinas introdutórias de redes.  

---

## 2. O que são emuladores de rede?
- **Emuladores** vão além da simulação: eles **executam o sistema operacional real dos dispositivos** em um ambiente virtual.  
- Permitem usar imagens oficiais de roteadores, switches e firewalls e até de sistemas operacionais de dispositivos finais como PCs e servidores, reproduzindo fielmente o comportamento dos equipamentos.  
- Exemplo: **PNETLab** (semelhante ao GNS3 e EVE-NG).  

### Utilidades dos emuladores
- Treinar em ambientes complexos e realistas.  
- Testar configurações avançadas, como protocolos de roteamento dinâmico, VPNs, firewalls e integração com sistemas reais.  
- Usado por profissionais e estudantes avançados que precisam de prática próxima ao ambiente de produção.  

---

## 3. Diferenças principais entre simuladores e emuladores

| Aspecto         | Simulador (Packet Tracer) | Emulador (PNETLab) | Emulador (GNS3) |
|-----------------|----------------------------|---------------------|-----------------|
| **Natureza**    | Imita o funcionamento      | Executa o sistema real | Executa o sistema real |
| **Complexidade**| Mais simples               | Mais avançado       | Avançado, mas flexível |
| **Recursos**    | Limitados a funções básicas| Recursos completos dos equipamentos | Suporte a múltiplas imagens IOS e integração com VMs |
| **Uso típico**  | Ensino introdutório        | Treinamento profissional | Certificações (CCNP/CCIE) e ambientes de teste |
| **Exemplo**     | Cisco Packet Tracer        | PNETLab             | GNS3 |


---

## Packet Tracer
- Ferramenta oficial da Cisco voltada para **ensino e prática básica**.  
- Permite criar topologias, configurar IPs, roteamento estático, ACLs simples e servidores (DNS, Web, DHCP).  
- Interface amigável e leve, ideal para estudantes.
- Pode ser executado em máquinas simples e com recursos básicos de hardware.  

---

## PNETLab / GNS3
- Plataformas de **emulação** que suportam imagens reais de Cisco IOS, Juniper, Fortinet, Mikrotik, entre outros.  
- Permite criar laboratórios complexos, integrando com máquinas virtuais e sistemas externos.  
- Usado em certificações avançadas (CCNP, CCIE) e ambientes de teste profissional.
- Necessita de maiores recursos de hardware, quanto mais complexos os cenários e as VMs, mais hardware será necessário.

---

## 4. Conclusão sobre simuladores e emuladores
- **Simuladores** (como Packet Tracer) são ideais para começar, aprender fundamentos e praticar em cenários simples.  
- **Emuladores** (como PNETLab e GNS3) são voltados para quem precisa de realismo, complexidade e prática avançada.  
- Ambos são complementares: o simulador ajuda a aprender a lógica, e o emulador prepara para o mundo real.

[Principais opções de simuladores e emuladores >>](simuladores_emuladores_p2.md)

