# Azure Infrastructure Lab

Ambiente de estudo de **Infraestrutura no Microsoft Azure**, reunindo rede, servidores Windows, identidade, monitoramento e backup.

## Visão geral

| Área | Estrutura implementada |
| --- | --- |
| Rede | VNet com sub-redes para servidores, usuários e Bastion |
| Servidor | Windows Server 2025 — `CORP-DC01`, IP privado `10.10.1.4` |
| Cliente | Windows 11 Pro — `CLIENT01`, IP privado `10.10.2.4` |
| Identidade | AD DS e DNS configurados para `corp.local` |
| Acesso | Azure Bastion; VMs sem IP público |
| Monitoramento | Azure Monitor Agent, Log Analytics, DCR e regras de alerta |
| Backup | Recovery Services Vault; backup do servidor com êxito |

## Arquitetura

```mermaid
flowchart TB
    admin[Administrador] --> bastion[Azure Bastion]
    subgraph azure[rg-corporate-lab · Brazil South]
        subgraph net[vnet-corporate · 10.10.0.0/16]
            bastion --- sb[AzureBastionSubnet · 10.10.0.0/26]
            servers[subnet-servers · 10.10.1.0/24] --- dc[CORP-DC01 · 10.10.1.4]
            users[subnet-users · 10.10.2.0/24] --- client[CLIENT01 · 10.10.2.4]
            nsg[nsg-servers] --- servers
            nsg --- users
        end
        monitoring[Azure Monitor · Log Analytics]
        backup[Azure Backup · vault236]
    end
```

Diagrama de organização dos componentes do laboratório.

## Evidências do ambiente

### Windows Server e Active Directory

Sessão da VM acessada pelo Azure Bastion, com o domínio `corp.local`, a conta de computador `CLIENT01` no Active Directory e a identificação `CORP-DC01.corp.local` nas propriedades do Windows.

![Área de trabalho do Windows Server com Active Directory](screenshots/windows-server-active-directory.png)

### Cliente no domínio

A CLIENT01 está associada a `corp.local`. Em 16/10/2026, o teste de canal seguro retornou `True`, a consulta DNS localizou o controlador e a conexão LDAP foi bem-sucedida.

![Área de trabalho da CLIENT01 com associação ao domínio](screenshots/cliente-no-dominio.png)

### Servidor com endereço privado

Windows Server 2025, nome `CORP-DC01` e ausência de IP público registrados no portal.

![Servidor CORP-DC01](screenshots/servidor-corp-dc01.jpg)

### Backup do servidor

Último backup do `vm-server` com resultado **Êxito** e ponto de restauração disponível na captura.

![Itens de backup no Azure](screenshots/backup-das-vms.jpg)

[Ver rede e demais capturas →](screenshots/README.md)

## Documentação

[Infraestrutura](docs/infraestrutura.md) · [Serviços](docs/servicos.md)

---

**Pedro Henrique da Silva** · Laboratório de estudo · [Licença MIT](LICENSE)
