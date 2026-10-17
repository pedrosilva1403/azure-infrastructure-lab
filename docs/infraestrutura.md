# Infraestrutura

Esta página reúne os nomes e endereços que usei no laboratório. Os recursos ficam no grupo **rg-corporate-lab**, na região **Brazil South**.

## Rede

| Recurso | Faixa de endereços | Uso |
| --- | --- | --- |
| `vnet-corporate` | `10.10.0.0/16` | Rede virtual |
| `AzureBastionSubnet` | `10.10.0.0/26` | Acesso administrativo |
| `subnet-servers` | `10.10.1.0/24` | Servidores |
| `subnet-users` | `10.10.2.0/24` | Estações de trabalho |

Separei servidor e estação de trabalho em sub-redes diferentes. Ambas usam o `nsg-servers`. A regra de prioridade 100 permite RDP da sub-rede do Bastion; a de prioridade 200 bloqueia essa porta para as demais origens.

A sub-rede de servidores usa a tabela `rt-corporate-servers`, com a rota padrão `0.0.0.0/0` apontando para **Internet**. O acesso ao armazenamento Blob passa pelo endpoint privado `stcorplab-blob-endpoint`, no IP `10.10.1.5`.

[Ver os ajustes de acesso e rede](ajustes-do-ambiente.md)

## Máquinas virtuais

| Propriedade | Servidor | Cliente |
| --- | --- | --- |
| Recurso Azure | `vm-server` | `CLIENT01` |
| Nome no Windows | `CORP-DC01` | `CLIENT01` |
| Sistema | Windows Server 2025 Datacenter | Windows 11 Pro |
| IP privado | `10.10.1.4` | `10.10.2.4` |
| IP público | Sem IP público | Sem IP público |
| Tamanho | Standard D2s v7 | Standard F2-1amds v7 |

O acesso às máquinas é feito pelo `bastion-corporate`. Para que a CLIENT01 encontre o domínio, configurei seu DNS com o endereço do servidor: `10.10.1.4`.

## Recursos de apoio

As VMs possuem seus próprios discos e interfaces de rede. O IP público `vnet-corporate-IPv4` faz parte do acesso pelo Bastion; nenhuma das duas máquinas possui IP público diretamente associado.

[Capturas da rede](../screenshots/README.md) · [Voltar ao projeto](../README.md)
