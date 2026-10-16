# Infraestrutura

Recursos organizados no grupo **rg-corporate-lab**, na região **Brazil South**.

## Rede

| Recurso | Faixa de endereços | Uso |
| --- | --- | --- |
| `vnet-corporate` | `10.10.0.0/16` | Rede virtual |
| `AzureBastionSubnet` | `10.10.0.0/26` | Acesso administrativo |
| `subnet-servers` | `10.10.1.0/24` | Servidores |
| `subnet-users` | `10.10.2.0/24` | Estações de trabalho |

O `nsg-servers` está associado às sub-redes de servidores e usuários, com as regras padrão do Azure.

## Máquinas virtuais

| Propriedade | Servidor | Cliente |
| --- | --- | --- |
| Recurso Azure | `vm-server` | `CLIENT01` |
| Nome no Windows | `CORP-DC01` | `CLIENT01` |
| Sistema | Windows Server 2025 Datacenter | Windows 11 Pro |
| IP privado | `10.10.1.4` | `10.10.2.4` |
| IP público | Sem IP público | Sem IP público |
| Tamanho | Standard D2s v7 | Standard F2-1amds v7 |

O acesso administrativo utiliza o `bastion-corporate`. O DNS do cliente aponta para `10.10.1.4`.

## Recursos de apoio

Discos gerenciados e interfaces de rede acompanham as VMs. O IP público `vnet-corporate-IPv4` pertence à estrutura de rede e não está associado diretamente às VMs.

[Capturas da rede](../screenshots/README.md) · [Voltar ao projeto](../README.md)
