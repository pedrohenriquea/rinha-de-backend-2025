# Mandioca Cozidinha para rinha de backend de 2025

Lapidado com o que coloca o leite na mesa das crian�a: 

- [.NET 9](https://dotnet.microsoft.com/download/dotnet/9.0)
- [RabbitMQ (do MassTransit)](https://hub.docker.com/r/masstransit/rabbitmq)
- [Redis](https://hub.docker.com/_/redis)
- [Nginx](https://hub.docker.com/_/nginx)

## Como � a solu��o?
![Diagrama da Solu��o](solution.png)

Fiz um sem�foro que indica se pode ou n�o passar requisi��es pro default ou fallback do payment processor. Peguei essa implementa��o de Channel para fila em mem�ria do .NET aqui e ajeitando pra esse desafio:
https://learn.microsoft.com/pt-br/aspnet/core/fundamentals/host/hosted-services?view=aspnetcore-9.0&tabs=visual-studio#:~:text=AddScoped%3CIScopedProcessingService%2C%20ScopedProcessingService%3E()%3B-,Tarefas%20em%20segundo%20plano%20na%20fila,-Uma%20fila%20de

## Como executar?
```docker-compose up -d```

E boa pa nois.