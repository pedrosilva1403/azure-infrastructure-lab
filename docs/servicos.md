# Serviços

## Identidade

AD DS e DNS integrado configurados no servidor `CORP-DC01`, com domínio `corp.local`. O ambiente também possui Provisioning Agent instalado e configuração inicial do Entra Cloud Sync.

Verificações realizadas em **16/10/2026**:

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
