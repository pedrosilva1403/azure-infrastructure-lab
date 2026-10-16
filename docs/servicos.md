# Serviços

## Identidade

Usei o `CORP-DC01` como controlador do domínio `corp.local`, com Active Directory e DNS no mesmo servidor. A CLIENT01 usa esse DNS para encontrar o domínio.

Também fiz um teste com o **Entra Cloud Sync**: o usuário `pedro.silva` foi lido no AD e criado no Microsoft Entra ID. O resultado cobre a criação da identidade na nuvem. Login e sincronização de senha não fizeram parte desse teste, e a sincronização automática continua desabilitada.

![Provisionamento sob demanda concluído](../screenshots/entra-provisionamento.jpg)

Para conferir a comunicação entre servidor, cliente e domínio, estes foram os testes realizados:

| Verificação | Resultado |
| --- | --- |
| Controlador do domínio | `CORP-DC01.corp.local` |
| Diagnóstico DNS (`dcdiag /test:dns`) | Teste DNS aprovado para o controlador e o domínio |
| Associação do cliente | `CLIENT01` em `corp.local`; `PartOfDomain: True` |
| DNS do cliente | `10.10.1.4`; registro SRV apontando para o controlador |
| Conectividade LDAP | Porta TCP 389 acessível no servidor |
| Canal seguro do cliente | `Test-ComputerSecureChannel` retornou `True` |

[Ver sessões Windows](../screenshots/README.md)

## Monitoramento

Reuni abaixo os componentes que configurei para acompanhar o ambiente. A tabela descreve a estrutura montada; a coleta de dados no workspace ainda não foi confirmada.

| Componente | Recurso |
| --- | --- |
| Agente | `AzureMonitorWindowsAgent` no servidor |
| Workspace | `law-corporate` |
| Regra de coleta | `msvmi-brazilsouth-vm-server` |
| Alertas | `Virtual Machine Consumption` e `VM Availability - vm-server` |
| Grupo de ações | `VMI-ActionGroup-vm-server` |

## Backup

Os backups ficam no cofre `vault236`, com a política `EnhancedPolicy-mv9vnv6q`. O backup do servidor terminou com êxito e gerou um ponto de recuperação.

[Ver captura dos backups](../screenshots/backup-das-vms.jpg) · [Voltar ao projeto](../README.md)

### Recuperação de disco

Para testar a recuperação, restaurei o disco Windows de **127 GiB** no grupo `rg-restore-validation`. Ele ficou separado da VM original, com origem **Restore** e referência ao backup usado.

O teste foi até a recuperação do disco. Não foi criada nem iniciada uma nova VM a partir dele.

![Disco restaurado](../screenshots/disco-restaurado.jpg)
