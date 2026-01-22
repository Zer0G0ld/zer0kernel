# zer0kernel

Documentando tudo em [docs](/doc/)

**Indice:**
- [Conceitos Fundamentais](/doc/ConceitoFundamental.md)
- [SMP](/doc/SMP.md)
- [Kernel Monolítico](/doc/KernelMonolitico.md)
- [Micro Kernel](/doc/MicroKernel.md)
- [ExoKernel](/doc/Exokernel.md)

---

# Primeiros Principios para o Zer0Kernel

**Princípio 1: Keep It Simple**
"Implemente apenas o necessário para o próximo passo"

**Princípio 2: Document as You Go**
"Cada função, cada decisão de design documentada"

**Princípio 3: Test Rigorously**
"Teste após cada mudança, mesmo pequena"

**Princípio 4: Learn Publicly**
"Compartilhe problemas e soluções - ajuda outros"

**Princípio 5: Embrace Iteration**
"Refatore sem medo - código é plástico"

## Recursos Teóricos Essenciais
### Livros:
- "Operating Systems: Three Easy Pieces" (gratuito online)
- "Understanding the Linux Kernel" (O'Reilly)
- "Modern Operating Systems" (Tanenbaum)

### Cursos:
- MIT 6.828: Operating System Engineering (xv6)
- Stanford CS140: Operating Systems
- University of Helsinki: Linux Kernel MOOC

### Referências:
- Intel Manuals (Volume 3: System Programming)
- OSDev Wiki (wiki.osdev.org)
- Linux Kernel Documentation

## Técnicas:
1. Qual arquitetura? **x64**
2. Kernel monolitico ou microkernel? **Hibrido** *(Acredito que seja a melhor escolha para juntar os pós de cada tipo)
3. Suporte a SMP desde o início? **Sim, suporte inicial**
4. Qual licença de software? **GNU3**