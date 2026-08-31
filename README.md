# PlameApps — GitHub Sync

Эта версия специально подготовлена для GitHub Pages.

## Что работает

- Игра публикуется напрямую через GitHub Pages.
- GitHub Actions автоматически проверяет `data/game.json` и публикует сайт.
- Браузер периодически читает общий `data/game.json` без токена.
- Общий рынок/объявления можно хранить в `data/game.json`.
- Токен GitHub НЕ находится в `index.html`.

## Важное ограничение

GitHub Pages + GitHub Actions сами по себе не являются realtime-сервером.

Браузер не должен получать Personal Access Token: тогда любой посетитель сможет его украсть.
GitHub Actions получает секреты только внутри workflow. Поэтому этот репозиторий реализует безопасную **синхронизацию чтения**, а не полноценную запись от каждого игрока в realtime.

Для настоящего мультиплеера с:
- регистрацией всех игроков на сервере,
- общим балансом,
- покупкой/продажей в реальном времени,
- чатами,
- админской выдачей денег,

нужен сервер/API (Node.js, Cloudflare Worker, Supabase, Firebase и т.п.) или другой безопасный backend.

## Как включить Pages

1. Создай GitHub repository.
2. Загрузи содержимое этого проекта в ветку `main`.
3. Settings → Pages → Source → GitHub Actions.
4. Дождись workflow `Validate and publish PlameApps`.
5. Открой URL GitHub Pages.

## Если нужен GitHub PAT

Не добавляй PAT в `index.html`, `config.js` или другой публичный файл.

Для серверной автоматизации GitHub рекомендует встроенный `GITHUB_TOKEN`; отдельные токены, если они действительно нужны, следует хранить как GitHub Actions Secret.
