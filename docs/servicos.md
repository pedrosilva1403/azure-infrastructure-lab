# Serviços e testes

## Domínio e DNS

Usei o `CORP-DC01` como controlador do domínio `corp.local`, com Active Directory e DNS no mesmo servidor. O DNS da CLIENT01 aponta para `10.10.1.4`.

| Verificação | Resultado |
| --- | --- |
| Controlador do domínio | `CORP-DC01.corp.local` |
| Serviços DNS e AD DS | Em execução durante os testes |
| Diagnóstico DNS (`dcdiag /test:dns`) | Aprovado para o controlador e o domínio |
| Registros SRV do domínio | Apontam para `CORP-DC01`, IP `10.10.1.4` |
| Encaminhador DNS do servidor | `168.63.129.16` |
| Associação do cliente | `CLIENT01` em `corp.local`; `PartOfDomain: True` |
| Conectividade LDAP | Porta TCP 389 acessível no servidor |
| Canal seguro do cliente | `Test-ComputerSecureChannel` retornou `True` |

![Cliente associado ao domínio](../screenshots/cliente-no-dominio.png)

## Identidade híbrida

No **Entra Cloud Sync**, fiz o provisionamento individual do usuário `pedro.silva`: a identidade foi lida no AD e criada no Microsoft Entra ID.

O resultado cobre a criação do usuário na nuvem. Login e sincronização de senha não fizeram parte desse teste. A sincronização periódica permanece desabilitada.

No servidor, iniciei o serviço `AADConnectProvisioningAgent` e configurei a inicialização como **automática com atraso**. O estado em execução foi confirmado durante a conferência.

![Provisionamento sob demanda concluído](../screenshots/entra-provisionamento.jpg)

## Monitoramento

Na conferência do servidor, a extensão **Azure Monitor Agent** estava saudável, com código de sucesso, e seus processos estavam em execução. O resultado dessa verificação se limita ao agente instalado no servidor.

| Componente | Recurso |
| --- | --- |
| Agente | `AzureMonitorWindowsAgent` |
| Regra de coleta | `msvmi-brazilsouth-vm-server` |
| Destino de métricas da regra | Azure Monitor Workspace `defaultazuremonitorworkspace-cq` |
| Log Analytics separado | `law-corporate` |
| Alertas | `Alerta-CPU-Alta-Server`, `Virtual Machine Consumption` e `VM Availability - vm-server` |
| Grupo de ações | `VMI-ActionGroup-vm-server` |

O alerta `Alerta-CPU-Alta-Server` está configurado para CPU média acima de **80%**, em uma janela de **5 minutos**.

## Backup e recuperação

Os backups ficam no cofre **vault236**, com a política `EnhancedPolicy-mv9vnv6q`. O backup do servidor terminou com êxito e gerou um ponto de recuperação.

![Itens protegidos pelo Azure Backup](../screenshots/backup-das-vms.jpg)

Para testar a recuperação, restaurei o disco Windows de **127 GiB** no grupo `rg-restore-validation`. Ele ficou separado da VM original, com origem **Restore** e referência ao backup usado.

O teste foi até a recuperação do disco. Não foi criada nem iniciada uma VM a partir dele.

![Disco restaurado](../screenshots/disco-restaurado.jpg)

[Ver infraestrutura](infraestrutura.md) · [Todas as capturas](../screenshots/README.md) · [Voltar ao projeto](../README.md)
