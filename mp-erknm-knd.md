# Блок-схемы

```mermaid
---
title: Sequence diagram
---

sequenceDiagram
    participant Пользователь as User
    participant СистемаАвторизации as AuthSystem
    participant ОсновнаяСистема as MainSystem

    Note over User: Начинает процесс входа

    User->>AuthSystem: Отправляет логин и пароль
    activate AuthSystem
    AuthSystem-->>User: Возвращает токен аутентификации
    deactivate AuthSystem

    User->>MainSystem: Передаёт токен вместе с запросом
    activate MainSystem
    alt Токен действителен
        MainSystem-->>User: Обрабатывает запрос успешно
    else Токен недействителен
        MainSystem-->>User: Возвращает ошибку аутентификации
    end
    deactivate MainSystem

```
