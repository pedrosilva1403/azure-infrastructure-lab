# Infraestrutura

Os recursos ficam no grupo **rg-corporate-lab**, na região **Brazil South**. Esta página reúne os nomes, endereços e configurações de rede do laboratório.

## Rede e acesso

| Recurso | Endereço | Uso |
| --- | --- | --- |
| `vnet-corporate` | `10.10.0.0/16` | Rede virtual |
| `AzureBastionSubnet` | `10.10.0.0/26` | Acesso administrativo |
| `subnet-servers` | `10.10.1.0/24` | Servidores |
| `subnet-users` | `10.10.2.0/24` | Estações de trabalho |

![Sub-redes e associação do NSG](../screenshots/sub-redes-e-nsg.jpg)

O `nsg-servers` atende às sub-redes de servidores e usuários. Para administrar as VMs, uso o `bastion-corporate`, sem IP público diretamente nas máquinas.

| Prioridade | Regra | Resultado |
| --- | --- | --- |
| 100 | `Allow_Bastion_RDP` | Permite TCP 3389 de `10.10.0.0/26` para `10.10.1.0/24` e `10.10.2.0/24` |
| 200 | `Deny_Direct_RDP_Internet` | Bloqueia TCP 3389 para as demais origens |

![Regras de acesso pelo Bastion](../screenshots/acesso-bastion-nsg.jpg)

### Rota dos servidores

A tabela `rt-corporate-servers` está associada à `subnet-servers`. A rota `0.0.0.0/0` usa **Internet** como próximo salto; seu nome foi mantido como `forcas-via-nva`.

Na conferência do servidor, a conexão HTTPS com `login.microsoftonline.com` passou.

![Rota padrão dos servidores](../screenshots/rota-dos-servidores.jpg)

## Máquinas virtuais

| Propriedade | Servidor | Cliente |
| --- | --- | --- |
| Recurso Azure | `vm-server` | `CLIENT01` |
| Nome no Windows | `CORP-DC01` | `CLIENT01` |
| Sistema | Windows Server 2025 Datacenter | Windows 11 Pro |
| IP privado | `10.10.1.4` | `10.10.2.4` |
| IP público | Sem IP público | Sem IP público |
| Tamanho | Standard D2s v7 | Standard F2-1amds v7 |

A CLIENT01 usa `10.10.1.4` como DNS para localizar o domínio. O IP público `vnet-corporate-IPv4` faz parte do acesso pelo Bastion.

![Servidor no Azure](../screenshots/servidor-corp-dc01.jpg)

## Armazenamento privado

O endpoint `stcorplab-blob-endpoint` conecta a rede ao Blob Storage da conta `stcorplabrestore1403`, com IP privado **10.10.1.5**. A zona `privatelink.blob.core.windows.net` permite resolver o nome da conta para esse endereço.

No servidor, a resolução DNS e a conexão TCP **443** passaram.

![Endpoint privado com conexão aprovada](../screenshots/armazenamento-privado.jpg)

## Proteção e custos

O grupo `rg-corporate-lab` tem bloqueio contra exclusão. O cofre `vault236` e o Log Analytics `law-corporate` também possuem bloqueios específicos.

Ao encerrar os testes, deixei a CLIENT01 e o servidor **desalocados**, interrompendo a cobrança de processamento dessas VMs. Discos, Bastion e outros recursos mantidos têm cobrança própria.

[Ver serviços e testes](servicos.md) · [Voltar ao projeto](../README.md)
