# Curso DIO - az104
====================================================================================================================================================================
## Gerenciar identidades e governança do Azure


Autenticação - é seu usuario e senha mfa
Autorização - é suas funções dentro do tenant

SSPR  
- codigo do aplicativo movel
- email
- telefone celular
- telefone comercial
- perguntas e respostas

somente em nuvem: gratuito
hybrido: P1

posso cadastrar:  de 3 a 5 perguntas
voce pode exigir que seu usuario responda: de 3 a 5 perguntas

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

ip publico ex: ecomerce, as pessoas vao acessar o web app
- pode ser associado a adaptadores de rede
- pode ser associado a VM
- pode ser associado a Balanceador de carga voltado para internet
- pode ser associado a gateways de VPN
- pode ser associado a gateways de app

NSG  Possui prioridade apartir de 100
- aplicado na subnet
- ou aplicado na placa de rede
- não é possivel excluir as regras padrões.
- é possivel aplicar NSG nas duas mas a subnet vem primeiro na hierarquia
- as duas NSG tem que estar iguais para funcionar.

NSG ela lê por ordem de prioridade se eu tiver a regra 120 e a regra 150 se ela lê a regra 120 e atender aos requisitos ela nao vai ler a regra 150

ASG Grupo de segurança de aplicativo 
para aplicar o ASG é dentro do NSG na parte de "origem" "Destino"

emparelhamento-peering
- usado para fazer as Vnet1 se comunicar com a Vnet2
- peering regional é feito para duas vnets na mesma região.
- peering global é feito para duas vnets de região diferentes

Pergunta: Você está criando uma conexão entre duas redes virtuais. O desempenho é uma preocupação fundamental
R: SKU de gatway ex: VpnGw1, VpnGw2, VpnGw3

Pergunta: O tráfego entre máquinas virtuais em redes virtuais com peering é roteado _____.
R: diretamente através da infraestrutura de backbone da Microsoft

quando conectamos a nossa rede LOCAL com a rede do AZURE existe o GATEWAY DE VPN (rede de HUB)
Existem outras redes que se conectam com a rede de hub

tabela rotas
- direciona o trafego de rede entre maquinas virtuais, redes locais e a internet.
- ex: para maquina chegar em tal destino, tem as tabelas de rota.
- ROTAS DE SISTEMA não é possivel alterar
- ROTAS PERSONALIZADAS é possivel editar, para personalizar o trafego de rede

ponto de extremidade de serviço
- limitam o o acesso a rede a serviços especificos
- Pontos de extremidade de serviço são usados para limitar o acesso à rede e permitir comunicação entre máquinas virtuais dentro de uma rede virtual, sem precisar de acesso à internet.

privite link - linksprivado
- conectividade particular com serviços do azure ex: do meu computador acessar o web app somente, via link privado
- sem acesso  a internet publica

Pergunta: Sua empresa está se preparando para implementar uma VPN Site-to-Site no Microsoft Azure. Você faz tudo o seguinte, exceto?
R: Obtenha um dispositivo VPN para o ambiente Azure.


VPN site a site - conecta o ambiente local ao ambiente do azure via azure vpn gateway
VPN ponto a site - conecta um dispositivo individual ao azure.
VPN Vnet para Vnet conecta duas Vnets dentro do azure, não tem local onpremisses

Network Watcher / Observador de Rede ferramenta utilizada para testar a conectividade
-  ex: se uma vm ta comunicando com a outra vm

Balanceador de Carga - Load Balancer vai receber a requisição e atribuir para quem estar disponivel para atender ex. melhor link de internet

- USADO INTERNAMENTE UDP/TCP baseado em IP

Balanceador de Carga -Gateway de aplicativo
- para quem sai para internet
- recomendado usar o WAF porque protege contra DDoS
- USO PRA FORA HTTPS

Balanceador de Carga -Front Door
- para quem sai para internet
- uso de aplicativos globais
- recomendado usar o WAF porque protege contra DDoS
- USO PRA FORA HTTPS

Balanceador de Carga - CDN Gerenciador de trafego
- USA qualquer tipo de protocolo
- oferece trafego para serviços entre regios globais do azure
- oferece disponibilidade e dinamismo ao mesmo tempo

Balanceador de carga Publico externo
- ele recebe o endereço de ip publico e faz a distribuição para ip privado

Balanceador de carga Interno
- ele direciona o trafego a recursos dentro de uma Vnet para acessar o azure.
- não precisa de ip publico

SKU Básico - 300 instancias 
                      - SLA não tem
                      - http
 
SKU Standard - até 5k instancias
                           - SLA 99,99%
                          - https

Regras para o balanceador de carga
- mapeia a combinação de porta e ip
- é possivel adicionar NAT Apenas para VMs

Pergunta: Qual é o principal benefício de usar um dispositivo virtual de rede?
R: dispositivo virtual de rede (NVA – Network Virtual Appliance) no Azure é geralmente uma máquina virtual personalizada que executa funções de rede

Tipos de Load Balancer no Azure:

Público (Public)	IP público	Tráfego de internet para VMs na VNet
Interno (Internal)	IP privado	Balanceamento dentro da VNet (por ex: entre sub-redes)

se for balanceador de carga para NVA - o indicado é o gateway, e é interno, não pode ser publico

Pergunta: Azure Load Balancer, qual configuração é obrigatória para determinar como ele distribuirá o tráfego entre as VMs?
R: Criar um Pool de Back-end que defina as máquinas que irão processar as requisições

O Azure Load Balancer, por padrão, utiliza o método de distribuição baseado em hash de cinco tuplas (5-tuple hash).

O que é o hash de cinco tuplas?

- IP de origem
- Porta de origem
- IP de destino
- Porta de destino
- Protocolo (TCP ou UDP)

GATEWAY DE APLICATIVO
- faz via FQDN 
- Tem WAF
- faz resolução de nomes
- o nome do host a porta a URL
- layer 7 
- http https 
- TLS

Network Watcher / Observador de Rede

-  tem 3 fases Monitoring,  diagnóstico de rede e Tráfeg

Health Probe verifica o status das máquinas no back-end pool e, caso uma máquina falhe, redireciona o tráfego para outra instância saudável.


===================================================================================================================================================================

## Implementar e gerenciar o armazenamento

contas de armazenamento
* armazena arquivos/tabelas/mensagens

LRS - 3 replicas em uma região (no mesmo data center em servidores e racks diferentes) indicado apenas para testes

ZRS - 3 replicas em uma região (em data center diferentes) indicado para produção

GRS - 6 replicas em 2 regiões (em tres por região) - indicado para desastres regionais

sincrono - é escrito ao mesmo tempo

assincrono -  cópia para a segunda região

RA-GRS - Igual ao GRS + acesso de leitura a regiao secundaria  - usado em  ex: power bi

GZRS - 6 replicas em 2 regiões (em tres por região) 3+1 zonas
 nas tres primeiras zonas é sincronas
na zona segundaria é assincrona

RA-GZRS GZRS +  acesso de leitura a regiao secundaria


contas de armazenamento cada objeto tem uma URL exclusiva
* Container = blob .core.windows.net
* Tabela = table .core.windows.net
* Fila = queue .core.windows.net
* Arquivo = file .core.windows.net

armazenamento de blob
Conta de armazenamento > Container > Blob
- armazenamento de objetos e dados nao estrutirados
- pode armazenar qualquer tipo de dados binarios ou textos

container
- privado - para acessar precisa da chave key compartilhada
- blob - acesso de leitura anonimo somente no blob
- contêiner - acesso anonimo geral
- containers são ilimitados

camadas de acesso
- Hot tier (agradavel) (Quente)
- Cool tier (frio) 30 days
- Cold tier (archive) (arquivar) 90 days.
- Archive tier (arquive offline) 180 days SLA para restauração

ciclo de vida de dados
- é possivel criar regras ex: mover de hot para cool se o arquivo nao for alterardo após 30 dias

o acesso anonimo não permite edição apenas leitura.

é recomendado usar o SAS gerar o token com expiração direto no container ou blob e não usar a chave para a conta de armazenamento.


nomenclatura de conta de armazenamento = O nome deve ser único globalmente ele nao pode existir em outra assinatura, com 3 a 24 caracteres, sem letras maiúsculas ou caracteres especiais.

azure files - arquivos do azure
* windows / linux / macos
* liberar porta 445 no firewall
* pra migrar grandes quantidades usar o DATA BOX
* para migrar pequenas quantidades usar o AzCopy linha de comando

===================================================================================================================================================================

## implantar e gerenciar os recursos de computação do Azure

VMs






















































===================================================================================================================================================================

## Monitorar e manter os recursos do Azure


































  




