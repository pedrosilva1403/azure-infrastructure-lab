# Serviços

## Identidade

AD DS e DNS integrado configurados no servidor `CORP-DC01`, com domínio `corp.local`. O ambiente também possui Provisioning Agent instalado e configuração inicial do Entra Cloud Sync.

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
