# Laboratório de infraestrutura no Azure

Montei este ambiente para praticar redes, Windows Server, Active Directory e serviços de infraestrutura no Microsoft Azure.

O projeto conecta um servidor de domínio, uma estação Windows 11 e uma rede de filial, com acesso administrativo pelo Bastion. Também reúne identidade híbrida, armazenamento privado, monitoramento e recuperação de backup.

## Conheça o projeto

**[Ver o projeto completo: etapas e todos os prints](docs/projeto.md)**

| Parte do ambiente | O que foi configurado |
| --- | --- |
| Rede e acesso | Sub-redes, Bastion, regras de RDP e rota dos servidores |
| Servidor e cliente | Windows Server 2025 com AD DS e DNS; Windows 11 no domínio |
| Identidade | Provisionamento individual do AD para o Microsoft Entra ID |
| Monitoramento e backup | Agente, coleta, alertas, backup e recuperação de disco |
| Armazenamento | Endpoint privado para Blob Storage e DNS privado |
| Filial | Segunda rede virtual conectada à rede corporativa por peering |

A documentação reúne as configurações do ambiente e os resultados dos testes realizados. As capturas estão organizadas junto à etapa correspondente.

**Pedro Henrique da Silva** · Laboratório de estudo · [Licença MIT](LICENSE)
