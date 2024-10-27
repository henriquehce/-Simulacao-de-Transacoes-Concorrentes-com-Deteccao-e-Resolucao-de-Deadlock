
# Simulação de Transações Concorrentes com Detecção e Resolução de Deadlock

<!-- link do video:https://www.youtube.com/watch?v=d6Ml6XFzKFg&ab_channel=Henriquereis -->

Este projeto implementa uma simulação de transações concorrentes em Python, usando threads que competem por recursos compartilhados. O objetivo é provocar deadlocks e utilizar uma técnica de detecção e resolução para gerenciá-los, aplicando o protocolo *wound-wait* com base em timestamps.

## Funcionalidades
- **Simulação de Transações**: Threads simulam transações que acessam recursos compartilhados (`X` e `Y`) de forma concorrente.
- **Controle de Acesso com Bloqueio Binário**: Utiliza mutexes para garantir acesso exclusivo aos recursos `X` e `Y`.
- **Detecção e Resolução de Deadlock**: Implementa o protocolo *wound-wait*, onde threads mais novas liberam recursos para mais antigas, evitando deadlocks.
- **Estado e Mensagens no Terminal**: Exibe o estado das threads e recursos em tempo real, incluindo:
  - Início e finalização de cada thread;
  - Aquisição e liberação de bloqueios;
  - Espera por recursos e término em caso de deadlock.

## Estrutura do Código
- **`transacao(thread_name)`**: Função principal de cada thread. Define a ordem de acesso aos recursos (aleatoriamente) e executa a lógica de aquisição de recursos e controle de deadlock.
- **`acessar_recurso(thread_name, lock_primario, lock_secundario)`**: Implementa a lógica de aquisição de recursos com base no protocolo *wound-wait*, detectando e resolvendo deadlocks.
- **`wound_wait(t1, t2, lock_primario)`**: Protocolo de detecção e resolução de deadlock. Libera o recurso se uma thread mais nova tenta acessar um recurso ocupado por uma thread mais antiga.
- **Funções auxiliares**:
  - **`verificar_lock`**: Verifica o estado de cada recurso.
  - **`liberar_recurso_se_bloqueado`**: Libera o recurso se estiver bloqueado.

## Funcionamento do Código

1. **Criação de Recursos**: Define dois mutexes (`lock_X` e `lock_Y`) como bloqueios binários para simular o controle de acesso exclusivo aos recursos `X` e `Y`.
2. **Inicialização de Threads**: A função `main` dispara cinco threads, cada uma representando uma "transação". Cada thread tenta acessar `X` e `Y` de forma aleatória, provocando situações de deadlock.
3. **Controle de Deadlock com Wound-Wait**: Ao detectar deadlock, o protocolo *wound-wait* permite que a thread mais antiga (com timestamp mais antigo) continue e força a thread mais nova a liberar o recurso.
4. **Liberação de Recursos**: Após cada operação, a thread libera o recurso, permitindo que outras threads continuem o processamento.
5. **Exibição de Estados no Terminal**: Mensagens exibem em tempo real os estados das threads, como "executando", "aguardando", "finalizada" ou "terminada por deadlock".

## Quantidade de Threads

O programa cria cinco threads (`Thread-1` a `Thread-5`), que concorrem pelos recursos compartilhados `X` e `Y`. Esse número de threads foi escolhido para simular um ambiente de concorrência e provocar possíveis deadlocks.

## Como Executar
1. Clone o repositório.
2. Execute o código com o comando:
   ```bash
   python <nome_do_arquivo>.py
   ```
3. Observe as mensagens no terminal, que exibem o progresso e a resolução de deadlocks entre threads.

## Requisitos
- Python 3.x
- Biblioteca padrão `threading`

## Exemplo de Saída
O programa exibirá mensagens como:
- Estado atual dos recursos (bloqueado ou livre);
- Aquisição e liberação de recursos por cada thread;
- Detecção e resolução de deadlock;
- Finalização de threads após execução ou resolução de deadlock.

## Observações
Este projeto oferece uma simulação prática de controle de concorrência com resolução de deadlock, útil para entender como lidar com recursos compartilhados em sistemas multi-threaded. 
