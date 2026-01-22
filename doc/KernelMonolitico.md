# Kernel Monolítico
Nesta arquitetura, todos os serviços principais do sistema operacional (gerenciamento de memória, sistemas de arquivos, drivers de hardware e escalonamento) funcionam dentro do **espaço do kernel**.
- **Vantagem:** Maior desempenho, pois a comunicação entre os componentes é direta e rápida.
- **Desvantagem:** Menor estabilidade. Se um único driver falhar, todo o sistema pode travar (como a "tela azul").
- **Exemplos:** Linux, FreeBSD e núcleos de sistemas Unix tradicionais.
---
Um Kernel Monolítico inclui todos (ou pelo menos a maioria) de seus serviços no kernel propriamente dito.

Isso reduz a quantidade de trocas de contexto e mensagens envolvidas, tomando o conceito mais rápido do que um Microkernel. Por outro lado, a quantidade de código em execução no espaço do kernel toma o kernel mais propenso a bugs fatais.

A palavra "Monolíto" por si só significa uma única peça (mono) que é de ou como pedra (lítica), no entanto, quando aplicada a fãos, o significado exato é mais geral. A maioria das pessoas consideram que um kerenl onde drivers de dispositivo e serviços são executados como parte do kernel é um kernel monolítico, independentemente de as partes serem "módulos de kernel" carregados dinamicamente ou se tudo for um verdadeiro binário único e imutável. Por esta razão, pode-se fazer uma distinção entre "monolítico" e "monolítico puro".

Versões modernas do Linux são um exemplo bem conhecido de um kernel monolítico - enquanto os drivers são enviados como "modúlos de kernel" carregados dinamicamente, eles ainda sõa carregados e executados no espaço do kernel. Kernels monolíticos são comuns para a arquitetura 80x86/PC.

Exemplos de kernels "monolíticos puros" são raros para a arquitetura 80x86/PC(mas mais comuns em sistemas embarcados). Isso ocorre devido à grande variedade de dispostivos, hardware e recusos de CPU que podem estar presentes em um PC moderno. Um kernel monolítico puro precisaria ser muito grande ou compulado especificamente para o computador antes do uso.

Em geral, a maioria dos sistemas operacionais não são "monolíticos puros" ou "mickrokernel puro", mas ficam em algum lugar entre esses extremos para aproveitar as vantagens de ambos os métodos.

![Monolithic Kernel](/src/Monolithic.png "Monolithic Kernel")