# Взаимодействие ЕРКНМ и приложения "Мобильный инспектор"

## Содержание

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Взаимодействие ЕРКНМ и приложения "Мобильный инспектор"](#взаимодействие-еркнм-и-приложения-мобильный-инспектор)
  - [Содержание](#содержание)
  - [sequence sample](#sequence-sample)
  - [Создание паспорта КНМ (ПМ) в ЕРКНМ](#создание-паспорта-кнм-пм-в-еркнм)
  - [Создание карточки КНМ в приложении "Мобильный инспектор"](#создание-карточки-кнм-в-приложении-мобильный-инспектор)
  - [Взаимодействие с контролируемым лицом](#взаимодействие-с-контролируемым-лицом)

<!-- /code_chunk_output -->


## sequence sample
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
## Создание паспорта КНМ (ПМ) в ЕРКНМ

```mermaid
sequenceDiagram

    box
        actor Inspector as Инспектор
        participant Erknm as ЕРКНМ
    end

    Inspector->>Erknm: Создает карточку КНМ
    activate Erknm
    Erknm-->>Inspector: Выдает номер КНМ
    deactivate Erknm
```

## Создание карточки КНМ в приложении "Мобильный инспектор"

![alt text](images/mp-inspector.jpg)

```mermaid
flowchart TD
    A[Авторизоваться в приложении с помощью ЕСИА]-->B["Выбрать __Другие мероприятия__"]
    B-->C["Нажать кнопку __Создать__"]
    C-->D[Ввести номер ЕРКНМ]
    D-->E["Нажать кнопку __Создать__"]

```

## Взаимодействие с контролируемым лицом

```mermaid
sequenceDiagram
        
    box
        actor Inspector as Инспектор
        actor Organization as Контролируемое лицо
    end
    Inspector->>Organization: Уведомление о проведении проверки в Госуслугах
    activate Organization
        Organization-->>Inspector: Подтверждение участия
        Inspector->>Organization: Ссылка на мероприятие
    deactivate Organization
```