# Exokernel
![Exokernel](/src/Exokernel.png)

Exokernels são uma tentativa de separar a segurança da abstração, fazendo com que partes não substituíveis do sistema operacional não façam quase nada além de multiplexar o hardware com seguraça. O objeto é evitar forçar qualquer abstração especifica sobre os aplicativos, permitindo que eles usem ou implementem quaisquer abstrações mais adequadas à sua tarefa sem ter que colocá-las sobre outras abstrações que podem impor limites ou sobrecarga desnecessária. Isso é feito movendo abstrações para bibliotecas de espaço de usuário não confiaveis chamadas "sistemas operacionais de biblioteca" (libOSes), que são vinculadas a aplicativos e chamam o sistema operacional em seu nome.

Os exokernels são frequentemente comparados (ou confundidos com) hipervisores,, e as implementações de ambos são geralmente bastante semelhantes, especialmente quando a virtualização de hardware é usada; a maioria dos exokernels pode, de fato, servir como hipervisor para outros sistemas operacionais, se assim o desejar, No entanto, os casos de uso são radicalmente diferentes - o objetivo de um hipervisor é fornecendo uma abstração sobre o hardware, enquanto o objeto de um exokernel é tomar tal abstração desnecessária. Além disso, na maioria dos usos atuais, o próprio hipervisor é executado como ou em uma instância de um sistema operacional de uso geral. Emboraa mudança para clientes "contêinerizados" para hipervisores possa ser vista como um híbrido das duas ideias (pelo menos em um nivel conceitual), na pratica elas não são a mesma coisa.

## Conceito de Exokernel
O conceito de Exokernel é ortogonal ao de kernels micro vs monolítos. Não é importante se a multiplexação segura é realizada em código de kernel privilegiado ou servidores de modo de usuário, apenas que não há abstrações forçadas.

*Exemplo*
Considere a abstração tipica de um arquivo. Os arquivos, como o aplicativo os vê, não existem no disco. No disco, existem setores de disco. O sistema operacional abstrai a realidade do disco para criar a ilusão mais conveniente de arquivos e um sistema de arquivos. Normalmente, a segurança também é forneceida neste nivel ACLs, permissões no estilo Unix, etx. são aplicadas aos arquivos. A segurança é combinada com abstração.

Em exokernels, a segurança é fornecida no nivel de hardware não abstrato, neste exemplo, para setores de disco. Os LibOSes fornecem quaisquer abstrações desejadas sobre esta interface. A segurança não substituível é colocada no exokernel e a abstração substituível é implementada em um libOS. A segurança é separada da abstração.

## Vantagens
A vantagem disso é que os aplicativos de espaço do usuario podem implementar seu próprio gerenciamento de memória otimizado (acessando diretamente, por exemplo, tabletas de memória), acesso a arquivos (por acesso "bruto" ao disco), etc. Isso pode, para aplicativos especiais, resultar em aumentos significativos de desempenho. Engler et al. compararam um serviodr web, p Cheetah, executado em um exokernel até oito vezes mais rápido que o da concorrência. Cheetah, entre outras coisas, usa conhecimento de HTTP para combinar solicitações IO, conhecimento de HTTML para colocar recursos adequadamente no disco, evita copiar dados enviando recursos aos clientes diretamente do cache arquivos e armazena em cache pacotes de rede pré-gerados. Ver [Desempenho e flexibilidade de aplicativos em sistemas Exokernel](https://pdos.csail.mit.edu/papers/exo-sosp97/exo-sosp97.html).

Além disso, ao estar ciente da disponibilidade, revogação e alocação de recursos, espera-se que os aplicativos possam fazer uso mais eficiente e inteligente dos recursos de hardware. Por exemplo, um servidor saberia que não deve tornar seu cache na memória maior do que a quantidade de memória que ele realmente possui. Em sistemas tradicionais, o sistema operacional falsificava o quanto o servidor havia alocado com memória virtual, e o servidor continuava, ignorando quaisquer falhas de página, trocando e paginando.

Espera-se também que os exokernels, de forma semelhante aos microkernels, facilitam o desenvolvimento e o teste de novas ideias de sistemas operacionais. Novas técnicas de agendamento, métodos de gerenciamento de memória, sistemas de arquivos, etc. podem ser desenvolvidos e testados em libOSes, que são modificados de forma mais rápida e fácil do que os sistemas operacionais atuais.

## Desvantagens
A tecnologia Exokernel ainda não foi completamente pesquisada, então surpresas podem estar por toda parte. Além disso, a flexibilidade adicional para programas de espaço do usuário também significa consistência reduzida. Embora fosse teoricamente possivel fornecer libOSes que permitissem, por exemplo MacOS, Windows e Linux para serem executados simultaneamente no mesmo sistema, o que também significaria uma aparência diferente para cada um deles. Além disso, diferentes libOSes podem ter niveis variados de compatibilidade e interoperabilidade entre si.

Pode ser dificil projetar interfaces exokernel. O projetista deve desenvolver interfaces adequadas e apropriadas para hardware de baixo nivel e equilibrar delicadamente potência e minismalismo versus proteção suficiente. Engler et al. observam que suas interfaces de exokernel passaram por muitas revisões.

A facilidade de criação e mixagem de libOSes pode levar a bagunças de código que seriam um pesadel para codificadores de manutenção e administradores de sistema. Os codificadores de manutenção teriam que lidar não apenas como o código do aplicativo, mas também como quaisquer abstrações substituindas dou novas implementações.

Informações que de outra forma poderiam ser úteis para um kernel podem ser perdidas se as abstrações relacionadas forem implementadas em libOSes e não no kernel.

## Derivados do Exokernel
Embora kernel monolitico e microkernel sejam termos bastante bem definidos, os defensores da tecnologia semelhante ao exokernel cunharam muitos termos diferentes - nanokernel, picokernel, kernel de cache, kernel de virtualização, etc. A maioria deles são variações relativamente pequenas um do outro.

**Nanokernel/Picokernel**
Nanokernel e picokernel sõa geralmente pequenos kernels considerados por seus criadores como ainda menores do que microkernels. Exemplos incluem: Adeos, Chave KOS, e LSE/OS. Outro explo muito famoso é o kernel simbiano EKA2. Este nanokernel implementa drivers dentro do kernel, o que o torna não totalmente um microkernel.
