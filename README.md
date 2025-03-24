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
O CORS (Cross-Origin Resource Sharing) é um mecanismo que permite que recursos hospedados em um domínio sejam acessados por páginas web de outro domínio diferente. Na AWS, ele é comumente configurado em serviços como o Amazon S3, permitindo que um site (ex: hospedado no domínio A) consiga acessar arquivos públicos armazenados em buckets S3 de outro domínio (domínio B).

Por padrão, o S3 bloqueia requisições feitas de origens diferentes por segurança. Para liberar esse acesso, é necessário configurar uma política CORS no bucket, definindo quais métodos (GET, POST, etc.) e origens estão autorizadas. Essa configuração é essencial quando se deseja integrar um front-end hospedado em um domínio com arquivos ou APIs hospedadas na AWS.