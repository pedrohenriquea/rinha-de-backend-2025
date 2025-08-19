Claro! Aqui está um **README.md** sugerido para o seu projeto **rinha-2025**, explicando as tecnologias utilizadas (Micronaut com GraalVM, PostgreSQL, Java 21, `ApplicationEventPublisher`) e fazendo referência ao repositório:

````markdown
# Rinha-2025

Projeto feito para a **Rinha de Backend 2025**, uma competição onde seu backend precisa gerenciar solicitações de pagamento entre dois processadores (default e fallback), com instabilidades constantes e otimizar o throughput/minimizar falhas.

Link do projeto: [pedrohenriquea/rinha-2025](https://github.com/pedrohenriquea/rinha-2025)

---

## Tecnologias utilizadas

###  Micronaut + GraalVM (Native Image + Java 21)
- O backend foi desenvolvido com o **Micronaut**, framework leve, modular e otimizado para **AOT (Ahead-of-Time) compilation**.
- Utilizando **GraalVM Native Image**, compilamos a aplicação em um binário nativo, eliminando a JVM, reduzindo o tempo de startup e o consumo de memória :contentReference[oaicite:0]{index=0}.
- A versão alvo da linguagem é **Java 21**, suportada pelo GraalVM e com compatibilidade nativa com Micronaut :contentReference[oaicite:1]{index=1}.

###  PostgreSQL
- Serve como banco de dados relacional leve para persistência dos pagamentos processados, crucial para consistência e auditoria.
- Inicializado a partir de `docker-compose`, com script SQL de criação/DDL incluído no container.

###  `io.micronaut.context.event.ApplicationEventPublisher`
- Usado para emitir eventos internos da aplicação — por exemplo, quando um pagamento é iniciado, concluído ou falha.
- Permite lidar com essas mudanças de estado de maneira reativa/event-driven, desacoplando componentes e tornando o sistema mais modular e testável.

---

## Estrutura do código (parte relevante)

- **Fonte principal**: o backend em `src/main/java`
  - **Controllers**, **Services** e lógica de negócios baseada em eventos.
  - Exemplo de uso de `ApplicationEventPublisher`:
    ```java
    @Inject
    ApplicationEventPublisher<EventType> publisher;

    // em algum método...
    publisher.publishEvent(new PaymentProcessedEvent(...));
    ```
- **Deploy e execução**:
  - Construção da imagem nativa com GraalVM via Gradle.
  - Deploy via Docker Compose para testes locais e perfil de carga, respeitando os limites de **1.5 CPU** e **350MB de memória**.

---

## Como executar localmente

1. Clone o repositório:
   ```bash
   git clone https://github.com/pedrohenriquea/rinha-2025.git
   cd rinha-2025
````

2. Compile a aplicação (nativa via GraalVM):

   ```bash
   ./gradlew buildNative
   ```

3. Inicie todos os serviços (backend, Postgres, load-balancer, etc.):

   ```bash
   docker-compose up
   ```

4. Acesse o endpoint (via nginx):

   ```
   http://localhost:9999/payments
   ```

---

## Resumo

| Componente  | Tecnologia                                   |
| ----------- | -------------------------------------------- |
| Framework   | Micronaut (Java 21) com GraalVM Native Image |
| Banco       | PostgreSQL via Docker                        |
| Arquitetura | Event-driven com ApplicationEventPublisher   |

---