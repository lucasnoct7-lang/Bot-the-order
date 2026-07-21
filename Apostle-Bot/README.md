# Apostle Bot

Bot de Discord em Python para administrar o clã, registrar atividades e organizar torneios equilibrados.

## Recursos

- logs de mensagens, edições, exclusões, entradas, saídas e convites
- tickets privados de suporte, recrutamento, parceria e denúncia
- moderação com warn, timeout, kick, ban, blacklist e vigia
- automod básico e alerta de possível raid
- painel de disponibilidade para ajuda
- torneios Solo, Duo e Time, criados exclusivamente pela staff
- sorteio de equipes equilibrado pelos cargos de nível dos participantes
- dashboard web opcional com dados operacionais

## Sistema de torneio

Use `/criar_torneio` com uma lista de membros. Apenas quem tem a permissão **Gerenciar Servidor** pode criar ou encerrar torneios.

- **Solo:** uma pessoa por equipe
- **Duo:** duas pessoas por equipe
- **Time:** a staff escolhe quantas pessoas haverá em cada equipe

O número de participantes precisa formar equipes completas. Por exemplo: 16 participantes funcionam em duplas ou em quatro equipes de quatro pessoas.

O sorteio distribui primeiro os cargos mais fortes entre equipes diferentes, reduzindo cenários como três Especial Grade no mesmo time. A ordem de equilíbrio é:

1. Especial Grade
2. Grade 1
3. Grade 2
4. Grade 3
5. Grade 4
6. Semi Grade 1
7. Semi Grade 2
8. Semi Grade 3
9. Semi Grade 4

Quem não tiver um desses cargos entra como `Sem grade`, com o menor peso. Os nomes dos cargos são comparados sem diferença entre maiúsculas, acentos ou estilos de número, então `Grade 1` e `Grade 𝟷` funcionam da mesma forma.

### Comandos

- `/criar_torneio` — cria e sorteia as equipes
- `/ver_torneio` — mostra o torneio aberto
- `/encerrar_torneio` — fecha o torneio atual
- `/configurar_canais`, `/painel_ajuda`, `/painel_tickets` e comandos de moderação continuam disponíveis

Os antigos sistemas de teste de grade, God Hand, ranking competitivo e Pontos de Apóstolo não são mais expostos pelo bot.

## Como rodar

1. Copie `.env.example` para `.env`.
2. Defina `DISCORD_TOKEN`.
3. Ative no Discord Developer Portal:
   - Server Members Intent
   - Message Content Intent
4. Instale as dependências:

```bash
py -m pip install -r requirements.txt
```

5. Inicie o bot:

```bash
py main.py
```

## Configuração

Depois de adicionar o bot ao servidor, use `/configurar_canais` para apontar os canais de logs, denúncias, ajuda, avaliações e vigia. Em seguida, use `/painel_ajuda` e `/painel_tickets` caso queira publicar os painéis.

O SQLite fica em `data/bot.sqlite3` por padrão. Para Railway, configure um volume em `/data` e use:

```env
DATABASE_PATH=/data/bot.sqlite3
BOT_LOG_PATH=/data/bot.log
DATA_DIR=/data
```

Se ativar o dashboard com `DASHBOARD_PORT`, defina também `DASHBOARD_TOKEN` antes de expor a porta publicamente.
