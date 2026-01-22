# Microkernel
![Microkernel](/src/Microkernel.png "Microkernel")

Um Microkernel tenta executar a maioria dos serviços como rede, sistema de arquivos, etc. Como daemons / servidores no espaço do usuário. Tudo o que resta a fazer pelo kernel são serviços básicos, como alocação de memória física (a memória real **gerente** pode ser implementado no espaço do usuário), agendamento e mensagens (Comunicação entre Processos).

Em teoria, esse conceito torna o kernel mais responsivo (já que muitas funcionalidades residem em threads e processos preemptivos do espaço do usuário, eliminando a necessidade de troca de contexto para o kernel propriamente dito) e melhora a estabilidade do kernel ao reduzir a quantidade de código em execução no espaço do kernel. Existem também beneficios adicionais para sistemas operacionais que suportam computadores multi-CPU (Proteção de reentrada muito mais simples e melhor adequação para funcionalidade assíncrona) e sistemas operacionais distribuidos (o código pode usar serviços sem saber se o provedor de serviços está sendo executado no mesmo computador ou não). Uma desvantagem é a quantidade de mensagens e troca de contexto envolvidas, o que torna os microkernels conceitualmente mais lentos do que os kernels monolíticos. (Isso não quer dizer que um microkernel projetado de forma inteligente não possa superar um monolítico projetado tolamente.)

Na prática as coisas podem ser bem diferentes. Por exemplo, se o sistema de arquivos travasse, o kernel continuaria em execução, mas o usuário ainda perderia alguns dados - a menos que fossem tomadas providências para reiniciar o ervidor / daemon do sistema de arquivos e existisse um sistema de recuperação de dados. Os microkernels podem ser mais estáveis, mas exigem trabalho de design adicional; ele não vêm graça com a arquitetura. Da mesma forma, o trabalho de design adicional que precisa ser feito para obter um design de microkernel correto também pode ser gasto na criação de um kernel monolítico preemptivo.

O AmigaOS, por exemplo, era um microkernel - e incomum: como o AmigaOS original não tinha proteção de memória, suas mensagens eram tão rápidas quanto possível (passando um ponteiro para a memória), tornando o kernel do AmigaOS um dos mais rápidos já desenvolvidos. Por outro lado, essa falta de proteção de memória também significava que a arquitetura do microkernel não oferecia estabilidade adicional (versões posteriores implementavam suporte a MMU, mas com o mesmo custo de velocidade que afeta outros sistemas microkernel).

Um dos efeitos colaterais do uso de um design de microkernel (ou um kernel monolítico modular) sãoa as mudanças necessárias para inicializar o sistema operacional. Se o sistema de arquivos for manipulado por um processo de espaço do usuário carregado pelo kernel, o kernel em si não conterá nenhum código para manipular sistemas de arquivos ou drivers de dispositivos de armazenamento para carregar o processo do sistema de arquivos em primeiro lugar. Um método para resolver isso é carregador de inicialização carregar uma "imagem de disco RAM", contendo o kernel e vários arquivos de suporte (drivers de dispositivos, etc).

Também é possivel que um projeto de sistema operacional empreste conceitos de kernels monolíticos e microkernels para usar os benneficios de qualquer um dos métodos quando apropriado.

Exemplos de Sistemas que são Microkernel:
Mach, QNX, L4, AmigaOS, Minix

