# Import Check — результаты проверки

## Наблюдаемые статусы новых файлов

| Файл | Статус в git status | Правило | Должен ли попасть в следующий коммит |
|------|---------------------|---------|--------------------------------------|
| src/TaskTracker.Domain/bin/rebuild.txt | `!!` (игнорируется) | `bin/` (на любом уровне) | Нет |
| src/TaskTracker.Domain/TaskStatus.cs | `??` (неотслеживаемый) | — (не игнорируется) | Да |

## Дополнительные четыре строки

| Файл | В текущем отслеживаемом составе? | Правило | Должен ли попасть в следующий коммит |
|------|----------------------------------|---------|--------------------------------------|
| .env.example | Нет | Не игнорируется (точное `/.env` не совпадает) | Да |
| .vscode/extensions.json | Нет | Разрешено `!/.vscode/extensions.json` | Да |
| docs/drafts/idea.md | Нет | Исключено `/docs/drafts/*` | Нет |
| notes.tmp | Нет (удалён из индекса) | Исключено `*.tmp` | Нет |

## Наблюдаемые результаты (команды)
```bash
$ git check-ignore -v -- src/TaskTracker.Domain/bin/rebuild.txt
.gitignore:3:bin/	src/TaskTracker.Domain/bin/rebuild.txt

$ git ls-files -- src/TaskTracker.Domain/bin/rebuild.txt
# (пусто — не отслеживается)

$ git ls-files -- src/TaskTracker.Domain/TaskStatus.cs
src/TaskTracker.Domain/TaskStatus.cs

$ git show HEAD:src/TaskTracker.Domain/TaskStatus.cs
public enum TaskStatus { New, Done }
