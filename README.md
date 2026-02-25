# 🎮 NexHub

> Plataforma social de gaming com recomendação musical inteligente e sistema de bolões com moeda interna.

---

## 📖 Sobre o Projeto

O **NexHub** é uma plataforma que conecta jogadores, integrando dados de desempenho em jogos com recomendações musicais personalizadas e um sistema de apostas entre amigos. Você vincula sua conta da Riot Games, o NexHub analisa suas partidas e sugere playlists do Spotify de acordo com o seu humor — vitória ou derrota. Para tornar tudo mais divertido, há bolões entre amigos com uma moeda interna e notificações em tempo real.

---

## ✨ Funcionalidades

- 🔐 **Autenticação** — Cadastro, login com JWT e gerenciamento de perfil
- 🎮 **Riot Games** — Vinculação de conta, rank, KDA e histórico de partidas
- 🎵 **Spotify** — OAuth2, top músicas e recomendação de playlist por humor pós-partida
- 🎲 **Bolões** — Criar apostas, participar com moeda interna e resolver com ranking
- 🖥️ **App Desktop** — .NET MAUI + Blazor Hybrid com distribuição via `.exe`
- ⚡ **Tempo Real** — Notificações via SignalR: resultado de bolões e amigo em partida
- 👥 **Follow** — Seguir outros jogadores e acompanhar sua atividade

---

## 🛠️ Stack

| Camada | Tecnologias |
|---|---|
| **Backend** | .NET 8, ASP.NET Core, Clean Architecture, EF Core, JWT |
| **Frontend** | Blazor WebAssembly |
| **Desktop** | .NET MAUI + Blazor Hybrid |
| **Banco de dados** | PostgreSQL (Supabase) |
| **Tempo real** | SignalR |
| **Cache** | Redis |
| **Mensageria** | RabbitMQ |
| **Deploy** | Railway (API), GitHub Releases (Desktop) |
| **Integrações** | Riot Games API, Spotify API, Steam Web API |

---

## 🏗️ Arquitetura

```
NexHub/
├── NexHub.Domain/          # Entidades e interfaces
├── NexHub.Application/     # Casos de uso e serviços
├── NexHub.Infrastructure/  # EF Core, clients de API externas
├── NexHub.API/             # Controllers, SignalR Hub, middlewares
├── NexHub.Web/             # Blazor WebAssembly (frontend)
└── NexHub.Desktop/         # .NET MAUI + Blazor Hybrid
```

---

## 🚀 Como rodar localmente

### Pré-requisitos

- [.NET 8 SDK](https://dotnet.microsoft.com/download)
- [PostgreSQL](https://www.postgresql.org/) ou conta no [Supabase](https://supabase.com)
- Conta de desenvolvedor na [Riot Games](https://developer.riotgames.com) e no [Spotify](https://developer.spotify.com)

### 1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/nexhub.git
cd nexhub
```

### 2. Configure as variáveis de ambiente

Crie um arquivo `appsettings.Development.json` em `NexHub.API/`:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=...;Database=nexhub;Username=...;Password=..."
  },
  "Jwt": {
    "SecretKey": "sua-chave-secreta-aqui",
    "Issuer": "nexhub",
    "Audience": "nexhub-users"
  },
  "RiotApi": {
    "ApiKey": "RGAPI-..."
  },
  "Spotify": {
    "ClientId": "...",
    "ClientSecret": "...",
    "RedirectUri": "https://localhost:5001/auth/spotify/callback"
  }
}
```

### 3. Rode as migrations

```bash
cd NexHub.API
dotnet ef database update
```

### 4. Inicie a API

```bash
dotnet run --project NexHub.API
```

A API estará disponível em `https://localhost:5001` com Swagger em `/swagger`.

### 5. Inicie o frontend

```bash
dotnet run --project NexHub.Web
```

---

## 📦 Build do App Desktop

```bash
dotnet publish NexHub.Desktop -c Release -f net8.0-windows
```

O `.exe` gerado estará em `bin/Release/net8.0-windows/publish/`. Veja os releases prontos na aba [Releases](https://github.com/seu-usuario/nexhub/releases).

---

## 🗺️ Roadmap

### Fase 1 — Base
- [x] Setup do repositório e arquitetura Clean
- [ ] Autenticação com JWT
- [ ] Layout base do Blazor

### Fase 2 — Integrações
- [ ] Riot Games API (rank + histórico)
- [ ] Spotify OAuth2 + recomendação por humor

### Fase 3 — Bolões
- [ ] Sistema de bolões e moeda interna
- [ ] Ranking de usuários

### Fase 4 — Desktop & Tempo Real
- [ ] App MAUI com Blazor Hybrid
- [ ] Notificações via SignalR
- [ ] Sistema de follow

### Fase 5 — Qualidade
- [ ] Testes unitários (xUnit)
- [ ] Redis + RabbitMQ
- [ ] CI/CD com GitHub Actions
- [ ] Integração com Steam

---

## 📄 Licença

Este projeto está sob a licença **MIT**. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
