Vinícius Nessler - DAS2

AULA 24/02
O Well-Architected Framework da AWS é composto por seis pilares que norteiam boas práticas de arquitetura em nuvem: excelência operacional, segurança, confiabilidade, eficiência em performance, otimização de custos e sustentabilidade.

AULA 27/02
O cache fica entre a aplicação e o banco de dados.
Ele armazena informações na memória e é acessado antes de fazer consultas ao banco.
O uso de cache pode sobrecarregar a memória RAM.
A troca de durabilidade por performance ocorre nesse processo.

O banco de dados é uma fonte de armazenamento persistente.

A Primeira Forma Normal visa reduzir a redundância de dados.

Para aumentar a disponibilidade de um sistema com limitações na linguagem, uma solução é adicionar mais computadores.
O "scale out" usa servidores adicionais por um período específico para melhorar a disponibilidade.

AULA 06/03
Trade Off - A nuvem oferece a alocação de servidores em momentos de pico e os remove quando o tráfego diminui.
IAC (Infrastructure as Code)
Acoplamento ocorre quando uma parte de um sistema não pode ser substituída sem que outras dependam dela.

ELB (Elastic Load Balancing) é um método de distribuição de tarefas para melhorar a performance.
Se uma máquina estiver inativa, o load balancer não direciona dados para ela, tornando as máquinas substituíveis sem acoplamento.

AULA 10/03
A infraestrutura global da AWS é complementada pelos Points of Presence (PoPs), que incluem Edge Locations, utilizados para entrega de conteúdo com baixa latência por meio de serviços como o CloudFront.

A segurança na nuvem é baseada no modelo de responsabilidade compartilhada. A AWS é responsável pela segurança da nuvem (infraestrutura física e serviços gerenciados), enquanto o cliente é responsável pela segurança dentro da nuvem (dados, permissões e configurações).

É essencial proteger dados tanto em trânsito quanto em repouso, utilizando HTTPS e criptografia. Segurança deve ser aplicada em todas as camadas, e os dados devem ser mantidos fora do alcance direto de pessoas, com rastreabilidade de acessos e eventos.

A preparação para incidentes de segurança envolve automação de boas práticas e monitoramento constante, com notificações e logs centralizados em serviços como o CloudWatch.

AULA 13/03
O modelo de responsabilidade compartilhada se aplica também ao gerenciamento de permissões de usuários através do serviço IAM (Identity and Access Management).

Contas IAM podem ser configuradas para acesso via console ou programático (API, SDK, CLI), e devem seguir boas práticas como uso de senhas fortes e rotativas, armazenamento seguro de credenciais e definição de tempo de vida das Access Keys.

A autenticação se baseia em múltiplos fatores: o que o usuário sabe (senha), o que ele é (biometria) e o que ele possui (dispositivo confiável). Já a autorização determina o que o usuário pode acessar, sendo ideal aplicar o princípio do privilégio mínimo — ou seja, conceder apenas as permissões estritamente necessárias.

AULA 17/03
As permissões no IAM podem ser configuradas com base em políticas identity-based, atribuídas diretamente a usuários, grupos ou roles. O controle de acesso baseado em papéis (RBAC) permite que usuários assumam permissões específicas de acordo com suas funções.

Em laboratórios ou ambientes controlados, podem ser criadas roles com permissões mínimas necessárias, garantindo acesso apenas aos recursos pertinentes.

As resource-based policies são utilizadas em serviços como o Amazon S3 para controlar diretamente o acesso a recursos, como buckets. Por padrão, todo bucket é privado, sendo necessário configurá-lo explicitamente como público caso queira expor arquivos. Isso é feito por meio do Amazon Resource Name (ARN), que identifica exclusivamente os recursos.

É possível conceder permissão para que instâncias EC2 acessem buckets S3, por exemplo, utilizando IAM Roles com políticas específicas.

Quanto ao armazenamento, a AWS oferece três principais tipos:

Block Storage: semelhante ao armazenamento de disco tradicional, ideal para sistemas operacionais e bancos de dados.

File Storage: estrutura hierárquica que simula um sistema de arquivos compartilhado.

Object Storage: baseado em metadados, ideal para armazenar arquivos não estruturados como imagens, vídeos e backups.

AULA 24/03
O CORS (Cross-Origin Resource Sharing) permite que um site acesse recursos hospedados em outro domínio. No S3, isso é configurado por meio de políticas que autorizam origens e métodos específicos (ex: GET, POST), sendo necessário para integrações web com front-ends externos.

O Amazon S3, por padrão, bloqueia qualquer acesso público a novos buckets ou objetos. As permissões precisam ser configuradas manualmente via IAM ou políticas específicas de bucket, e o bloqueio total de acesso público costuma vir ativado por padrão.

Além disso, é possível configurar criptografia automática no bucket. A criptografia padrão do S3 não é ativada automaticamente, mas pode ser habilitada para que todos os arquivos enviados sejam protegidos. A criptografia pode ser feita com SSE-S3 (chaves da AWS), SSE-KMS (chaves do KMS) ou SSE-C (chaves do cliente).

Aula de 27/03/2025
index.html

AULA 03/04
Máquinas Virtuais (VMs)

Amazon Elastic Compute Cloud (EC2): Fornece VMs de servidor.
Containers

Amazon Elastic Container Service (ECS)

Amazon Elastic Kubernetes Service (EKS)
Servidores Privados Virtuais (VPS)

Amazon Lightsail
Plataforma como Serviço (PaaS)

AWS Elastic Beanstalk
Serverless

AWS Lambda: Execução de trechos de código.

AWS Fargate: Serviço serverless para containers.

Escolhendo uma AMI

Ao escolher uma AMI, considere os seguintes fatores:

Região

Fonte da AMI:

Quick Start: AMIs Linux e Microsoft Windows fornecidas pela AWS.

My AMIs: AMIs criadas por você.

AWS Marketplace: Modelos pré-configurados de terceiros.

Community AMIs: AMIs compartilhadas por outros. Uso por sua conta e risco.

Ciclo de Vida de um EC2

AULA 07/04/2025
Amazon FSx for Windows File Server

Serviço de armazenamento de arquivos compatível com Windows.

Suporte a SMB, totalmente gerenciado pela AWS.

EC2 – User Data

Permite rodar scripts na inicialização da instância (shell script ou cloud-init).

Usado para automatizar instalações e configurações.

Metadados da Instância

Informações sobre a própria instância.

Acessíveis via: http://169.254.169.254/latest/meta-data/

Podem ser utilizados em scripts de inicialização.

Boas Práticas – Execução Manual

Preferir automação via user data.

Evitar alterações manuais sem controle.

Validar se a inicialização está correta após alterações.

Modelos de AMI

Basic AMI: imagem mínima, exige configuração manual.

Silver AMI: inclui parte dos softwares, requer ajustes.

Golden AMI: imagem totalmente configurada e pronta para uso.

Estratégias de Distribuição de Instâncias

Cluster: alta performance, baixa latência (HPC).

Spread: alta disponibilidade, instâncias distribuídas.

Partition: isolamento físico entre grupos de instâncias.


AULA 10/04/2025

Amazon RDS: banco relacional gerenciado com backup, failover e escalabilidade.

Bancos Relacionais: consistência e ACID (MySQL, PostgreSQL etc).

Bancos Não-Relacionais: escaláveis, flexíveis (DynamoDB, MongoDB etc).

Critérios de escolha: tipo de dado, padrão de acesso, consistência e volume.

RDS: serviço de banco relacional gerenciado (MySQL, PostgreSQL, Oracle, etc.).

Não-Relacionais: bancos como DynamoDB, MongoDB, voltados para dados flexíveis e escaláveis.

Discutimos como escolher o banco mais adequado baseado em necessidade de consistência, escalabilidade, modelo de dados e performance.


AULA 05/05

VPC (Virtual Private Cloud) define uma rede privada e isolada dentro da AWS.
CIDR (Classless Inter-Domain Routing) especifica o bloco de endereços IP utilizados na VPC.
Subnets dividem a VPC em partes menores.
Subnets públicas têm acesso à internet por meio de um Internet Gateway.
As rotas devem ser configuradas para direcionar o tráfego externo.
Instâncias em subnet pública devem ter IP público habilitado e associadas a uma tabela de rota que contenha o Internet Gateway.

AULA 12/05

Fazer os laboratórios Canvas
Guided lab: Creating a Virtual Private Cloud
Challenge (Cafe) lab: Creating a VPC Networking Environment for the Café

AULA 15/05

Fazer os laboratórios Canvas
Guided lab: Creating a Virtual Private Cloud
Challenge (Cafe) lab: Creating a VPC Networking Environment for the Café

AULA 19/05

VPC Peering permite a comunicação privada entre duas VPCs na mesma região ou em regiões diferentes.
Não permite tráfego transverso automático (ex: VPC A com VPC B e VPC B com VPC C não conecta A com C).
AWS VPN Site-to-Site estabelece uma conexão criptografada entre a VPC e a rede on-premises, utilizando o protocolo IPsec.
Requer Customer Gateway (CGW) e Virtual Private Gateway (VGW).
AWS Direct Connect oferece uma conexão física dedicada entre o data center do cliente e a AWS, com maior largura de banda e menor latência.
Útil para transferência de dados em larga escala e integrações corporativas.

AULA 26/05

IAM Groups permitem aplicar permissões a múltiplos usuários de forma centralizada.
Facilita o gerenciamento de políticas para perfis com a mesma função.
IAM Roles permitem conceder permissões temporárias para usuários ou serviços assumirem funções específicas.
AWS STS (Security Token Service) gera credenciais temporárias seguras com tempo de expiração definido.
Muito utilizado para autenticação entre contas ou serviços da AWS.
AWS Cognito permite autenticação e autorização de usuários em aplicações web e mobile.
Integra login com provedores externos (Google, Facebook, Apple) ou diretórios corporativos (via SAML).
Gera tokens JWT (ID, Access e Refresh) para controle de sessão e acesso.