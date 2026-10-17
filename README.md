# Azure Infrastructure Lab

Criei este laboratório para praticar **infraestrutura no Microsoft Azure**, conectando rede, Windows Server, domínio, identidade, monitoramento e backup. Aqui apresento o ambiente por assunto, com os principais resultados e capturas reais do projeto.

[Visão geral](#visão-geral) · [Rede](#rede-e-segurança) · [Domínio](#servidor-e-domínio) · [Armazenamento](#armazenamento-privado) · [Identidade](#identidade-híbrida) · [Monitoramento e backup](#monitoramento-e-backup)

## Visão geral

Organizei os recursos no grupo `rg-corporate-lab`, na região **Brazil South**. O ambiente reúne um servidor de domínio e uma estação Windows 11 em sub-redes separadas.

![Recursos do laboratório no Azure](screenshots/recursos-do-laboratorio.jpg)

[Ver a arquitetura](diagrams/arquitetura.mmd)

## Rede e segurança

Na `vnet-corporate`, separei servidores, usuários e Bastion. O acesso administrativo passa pelo **Azure Bastion**, com as VMs sem IP público.

- RDP permitido somente da sub-rede do Bastion, na regra de prioridade **100**.
- Bloqueio da porta 3389 para as demais origens, na prioridade **200**.
- Rota padrão dos servidores com próximo salto **Internet**; conexão HTTPS com o serviço de identidade da Microsoft testada.

![Regras de acesso pelo Bastion](screenshots/acesso-bastion-nsg.jpg)

[Ver endereçamento, regras e rota](docs/infraestrutura.md#rede-e-acesso)

## Servidor e domínio

Configurei o **Windows Server 2025**, identificado como `CORP-DC01` (`10.10.1.4`), com Active Directory e DNS para o domínio `corp.local`. Organizei o diretório em unidades para computadores, servidores, usuários e grupos.

- **CLIENT01**, com Windows 11 Pro, incluída no domínio.
- DNS do cliente apontando para o servidor.
- Resolução do domínio, conexão LDAP e canal seguro testados com êxito.

![Windows Server com Active Directory e identificação do domínio](screenshots/windows-server-active-directory.png)

[Ver os testes e a captura do cliente](docs/servicos.md#domínio-e-dns)

## Armazenamento privado

O acesso ao Blob Storage usa o endpoint privado `stcorplab-blob-endpoint`, no IP `10.10.1.5`. No servidor, confirmei a resolução do nome da conta para esse endereço e a conexão à porta **443**.

![Conexão aprovada do endpoint privado do armazenamento](screenshots/armazenamento-privado.jpg)

[Ver rede privada e DNS](docs/infraestrutura.md#armazenamento-privado)

## Identidade híbrida

Testei a integração do Active Directory com o **Microsoft Entra ID** pelo Cloud Sync. O usuário de laboratório `pedro.silva` foi criado na nuvem a partir do diretório local, em um provisionamento individual sob demanda.

![Provisionamento individual concluído no Microsoft Entra ID](screenshots/entra-provisionamento.jpg)

[Ver o escopo do teste](docs/servicos.md#identidade-híbrida)

## Monitoramento e backup

Configurei agente, regra de coleta, workspaces e alertas para acompanhar o servidor. Na verificação local, a extensão **Azure Monitor Agent** estava saudável e seus processos estavam em execução.

- Backup do servidor concluído no cofre **vault236**, com ponto de recuperação disponível.
- Disco Windows de **127 GiB** recuperado em um grupo separado, preservando a VM original.
- O teste de recuperação foi até o disco restaurado, sem iniciar uma VM a partir dele.

![Itens protegidos pelo Azure Backup](screenshots/backup-das-vms.jpg)

[Monitoramento](docs/servicos.md#monitoramento) · [Recuperação do disco](docs/servicos.md#backup-e-recuperação)

---

[Infraestrutura](docs/infraestrutura.md) · [Serviços e testes](docs/servicos.md) · [Todas as capturas](screenshots/README.md)

**Pedro Henrique da Silva** · Laboratório de estudo · [Licença MIT](LICENSE)
