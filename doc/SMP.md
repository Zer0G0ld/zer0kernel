# SMP - Symmetric Multi-Processing

## Definição:
**SMP (sYMMETRIC mULTI-pROCESSING)** = Múltiplos processadores idênticos compartilhando a mesma memória e sendo controlados por um único kernel.

## Como funciona:
```text
Antes (Single CPU):           Agora (SMP):
┌─────────────────┐        ┌─────────────────┐
│     CPU 1       │        │     CPU 1       │
│   [KERNEL]      │        │   [KERNEL]      │
│   [Process A]   │        │   [Process A]   │
│                 │        │                 │
│    Memória      │        │    Memória      │
│   Compartilhada │        │   Compartilhada │
└─────────────────┘        │                 │
                           │     CPU 2       │
                           │   [KERNEL]      │
                           │   [Process B]   │
                           └─────────────────┘
```
## Desafios do SMP:
```c
// 1. Concorrência REAL (não simulada)
Duas CPUs podem executar:
CPU1: counter++; // Lê counter=5
CPU2: counter++; // Lê counter=5 (ao mesmo tempo!)
// Resultado: counter=6 em vez de 7

// 2. Cache Coherence
CPU1 tem cache local com dado X=10
CPU2 modifica X=20 na memória
CPU1 ainda vê X=10 no seu cache

// 3. Escalonamento balanceado
Como distribuir processos entre CPUs?
```
