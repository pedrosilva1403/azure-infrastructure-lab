# Capturas do Azure

Reuni aqui as capturas do laboratório: recursos no Azure, sessões Windows pelo Bastion e resultados dos testes. Clique nas imagens para ver os detalhes.

## Windows Server e Active Directory

Área de trabalho da VM com o computador CLIENT01 no domínio e a identificação do controlador CORP-DC01.

![Windows Server e Active Directory](windows-server-active-directory.png)

## Cliente no domínio

Propriedades do Windows mostrando `CLIENT01.corp.local`.

![Cliente associado ao domínio](cliente-no-dominio.png)

## Servidor

![Propriedades do servidor CORP-DC01](servidor-corp-dc01.jpg)

## Sub-redes

![Endereçamento e associação do NSG](sub-redes-e-nsg.jpg)

## Segurança de rede

RDP permitido a partir da sub-rede do Bastion, com bloqueio para as demais origens.

![Regras de acesso pelo Bastion](regras-do-nsg.jpg)

## Rota dos servidores

Rota padrão da tabela `rt-corporate-servers`, com próximo salto Internet.

![Rota padrão dos servidores](rota-dos-servidores.jpg)

## Armazenamento privado

Endpoint privado usado para acessar o armazenamento Blob pela rede do laboratório.

![Endpoint privado do armazenamento](armazenamento-privado.jpg)

## Backup

![Itens protegidos no cofre](backup-das-vms.jpg)

## Recursos consultados

![Recursos consultados no portal](recursos-do-laboratorio.jpg)

## Identidade híbrida

Resultado do teste com o Cloud Sync, mostrando as etapas concluídas e a criação do usuário de laboratório no Entra ID.

![Provisionamento concluído](entra-provisionamento.jpg)

## Recuperação do backup

Disco Windows de 127 GiB recuperado do backup, separado do servidor original.

![Disco restaurado](disco-restaurado.jpg)

[Voltar ao projeto](../README.md)
