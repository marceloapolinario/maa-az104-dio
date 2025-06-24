# Curso DIO - az104

## SSPR  
- codigo do aplicativo movel
- email
- telefone celular
- telefone comercial
- perguntas e respostas

somente em nuvem: gratuito
hybrido: P1

posso cadastrar:  de 3 a 5 perguntas
voce pode exigir que seu usuario responda: de 3 a 5 perguntas

====================================================================================================================================================================

## Gerenciar identidades e governança do Azure
Autenticação - é seu usuario e senha mfa
Autorização - é suas funções dentro do tenant

Gerenciar contas de usuario
- administrador global
- administrador de usuario (para gerenciar usuarios)

Atualizações em massa
- serve para usuario e grupos
- precisa ser admin glbal ou admin de usuarios

Contas de grupo
- grupo de segurança
- grupo do 365

Tipos de atribuição Dinamica
- atribuido - grupo de segurança e grupo do 365
- usuario dinamico - grupo de segurança e grupo do 365
- dispositivo dinamico - grupo de segurança

Unidades Administrativas usado para separar filiais ex brasil, rj
- Precisa de P1
- É Possivel atribuir função.
- É Possivel atribuir associação dinamica

dominios no azure
- ao criar você pode gerar um TXT ou MX

criação de tenant
Ao criar um tenant dentro de outro tenant no primeiro momento somente você tem acesso
Você consegue trazer um usuário do tenant 1 para o tenant 2

GRUPO DE RECURSOS
- Não é possivel renomear
- É possivel mover  recursos para outros RG
- É possivel criar recursos de diferentes regioes dentro do mesmo grupo de recurso

Cotas
- solicitar a  microsoft. via chamado

Grupo de gerenciamento - management group
- uma assinatura só responde para um grupo de gerenciamento

grupo de recursos
- não pode ser renomeado
-  pode mover recursos para outro grupo de recursos
- pode criar diferentes recursos com localidades diferentes dentro de um grupo de recurso

tag
- não é herdavel, se vc adicionar ao RG uma tag não vai replicar para os recursos
- caso queira  aplicar em massa tem que criar um azure policy

azure policy
- executa avaliação e varreduras em busca de recursos nao compativeis
- imposição e conformidade
- aplicar politicas em escala
- remediação (ex: tem uma tag 5000 alterar todas 5000 para 1000)

Iniciativa - definição de politicas para distribuir para gerenciamento de grupo, assinatura ou RG
iniciativa - grupo de politicas dentro do azure policy
padronização - uma unica polica

RBAC
- Acesso granular a assinatura
- ARM
- JSON


Actions: ações permetidas ex: Microsoft.Compute/virtualMachines/start/action
NotActions: são subtraídos das Actions para definir a lista de operações permitidas.

Loks-bloqueios
- o bloqueio é Herdavel, se colocar no RG vai replicar para os recursos
- somente leitura - voce não consegue fazer nada, CONGELA..
- excluir - ele faz tudo menos excluir.

loks se tiver um bloqueio na conta de armazenamento como "somente leitura" NÃO é possivel visualizar as chaves de acesso keys

loks se eu mover o recurso e o lock estiver aplicado diretamente no recurso o loks é movido também e aplicado
           se eu mover o recurso e o lock estiver aplicado no RG o loks do recurso não é movido.


cloud shell precisa de uma conta de armazenamento
- 20minutos a sessão encerra
- pede pra usar bash ou powershell
  
powershell funciona em windows/linux/macos

azure resource manager ARM É um JSON das configurações do seu recurso

Bicep ferramenta de automação exclusiva da microsoft semelhante ao arm.

Blueprint

Você pode criar um Blueprint chamado "Ambiente Prod Padrão" que:

- Cria um grupo de recursos,
- Aplica uma política que bloqueia uso de regiões fora do Brasil,
- Implanta um template com VMs e storage.
Assim, toda vez que alguém usar esse Blueprint, o ambiente virá pronto, padronizado e seguro.

===================================================================================================================================================================

## Implementar e gerenciar redes virtuais




















