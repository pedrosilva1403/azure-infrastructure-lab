# Serviços

## Identidade

AD DS e DNS integrado configurados no servidor `CORP-DC01`, com domínio `corp.local`. O Provisioning Agent foi utilizado no teste individual sob demanda do Entra Cloud Sync: o usuário `pedro.silva` foi importado do AD e criado com sucesso no Microsoft Entra ID. O teste não inclui validação de login ou sincronização de senha; a sincronização periódica permanece desabilitada.

![Provisionamento sob demanda concluído](../screenshots/entra-provisionamento.jpg)

Verificações realizadas:

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

| Componente | Recurso |
| --- | --- |
| Agente | `AzureMonitorWindowsAgent` no servidor |
| Workspace | `law-corporate` |
| Regra de coleta | `msvmi-brazilsouth-vm-server` |
| Alertas | `Virtual Machine Consumption` e `VM Availability - vm-server` |
| Grupo de ações | `VMI-ActionGroup-vm-server` |

## Backup

A proteção utiliza o cofre `vault236` e a política `EnhancedPolicy-mv9vnv6q`. A captura do portal registra o último backup do servidor com resultado **Êxito** e ponto de restauração disponível.

[Ver captura dos backups](../screenshots/backup-das-vms.jpg) · [Voltar ao projeto](../README.md)

### Recuperação de disco

O Azure Backup recuperou o disco Windows de 127 GiB no grupo temporário rg-restore-validation, separado do ambiente original. O disco ficou desanexado, com origem de criação **Restore** e referência ao ponto de recuperação do backup. Esse teste confirma a recuperação do disco, sem avaliar a inicialização de uma VM restaurada.

![Disco restaurado](../screenshots/disco-restaurado.jpg)
