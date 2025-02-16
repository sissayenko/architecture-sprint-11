
# Задание 2. Разделение системы на домены

## Домены
Для обеспечения независимого развития бизнес-направлений предлагается разделить систему на следующие домены:

    Домен "Управление клиникой":
        Функции: Ведение медицинских карт, учет пациентов, управление персоналом, учет инвентаря.
        Данные: Медицинские карты, истории болезни, данные о пациентах, данные о персонале, данные об инвентаре.
        Сервисы: DWH (мигрированный и оптимизированный), API для доступа к медицинским данным, сервисы для управления персоналом и инвентарем.
    Домен "Финансовые услуги":
        Функции: Ведение счетов, обработка платежей, кредитование, финансовая отчетность.
        Данные: Данные о клиентах, данные о счетах, данные о кредитах, финансовая отчетность.
        Сервисы: Финтех-сервисы (Golang и Java), API для доступа к финансовым данным, сервисы для обработки платежей и кредитования.
    Домен "Искусственный интеллект":
        Функции: Обработка медицинских данных, анализ изображений, постановка диагнозов, разработка рекомендаций по лечению.
        Данные: Медицинские данные (изображения, результаты анализов), данные о пациентах, данные о заболеваниях.
        Сервисы: ИИ-сервисы (Python), API для доступа к ИИ-сервисам, сервисы для обработки данных и обучения моделей.
    Домен "Витрина данных":
        Функции: Предоставление доступа к аналитическим данным для бизнес-пользователей, создание отчетов, визуализация данных.
        Данные: Агрегированные данные из других доменов.
        Сервисы: BI Platform, API Gateway, сервисы для управления доступом и авторизацией.

## Data Flow Diagram
```mermaid
graph LR
    subgraph "Домен \"Управление клиникой\""
        A[Пациент] --> B((Регистрация пациента))
        B --> C[База данных пациентов]
        A --> D((Запись на прием))
        D --> C
        C --> E((Ведение медицинской карты))
        E --> F[База данных медицинских карт]
        F --> G((Просмотр медицинской карты))
        G --> A
        H[Персонал] --> I((Управление персоналом))
        I --> J[База данных персонала]
        K[Инвентарь] --> L((Учет инвентаря))
        L --> M[База данных инвентаря]
        N[DWH] --> O((API для доступа к медицинским данным))
        O --> G
        O --> E
    end

    subgraph "Домен \"Финансовые услуги\""
        P[Клиент] --> Q((Открытие счета))
        Q --> R[База данных клиентов]
        P --> S((Платеж))
        S --> T[База данных счетов]
        P --> U((Кредитование))
        U --> V[База данных кредитов]
        R --> W((Финансовая отчетность))
        T --> W
        V --> W
        X[Финтех-сервисы Golang и Java] --> S
        X --> U
        Y((API для доступа к финансовым данным)) --> W
    end

    subgraph "Домен \"Искусственный интеллект\""
        F --> Z((Обработка медицинских данных))
        Z --> AA[Сервисы для обработки данных и обучения моделей]
        AA --> BB[База данных заболеваний]
        F --> CC((Анализ изображений))
        CC --> AA
        AA --> DD((Постановка диагнозов))
        DD --> EE((Разработка рекомендаций по лечению))
        EE --> G
        FF[ИИ-сервисы Python] --> Z
        FF --> CC
        GG((API для доступа к ИИ-сервисам)) --> DD
        GG --> EE
    end

    subgraph "Домен \"Витрина данных\""
        C --> HH((Агрегация данных))
        F --> HH
        J --> HH
        M --> HH
        R --> HH
        T --> HH
        V --> HH
        BB --> HH
        HH --> II[BI Platform]
        II --> JJ[Бизнес-пользователи]
        KK((API Gateway)) --> II
        LL((Сервисы для управления доступом и авторизацией)) --> KK
    end

    style A fill:#ccf,stroke:#888,stroke-width:2px
    style H fill:#ccf,stroke:#888,stroke-width:2px
    style K fill:#ccf,stroke:#888,stroke-width:2px
    style P fill:#ccf,stroke:#888,stroke-width:2px
    style JJ fill:#ccf,stroke:#888,stroke-width:2px

    style B fill:#aaf,stroke:#555,stroke-width:2px
    style D fill:#aaf,stroke:#555,stroke-width:2px
    style E fill:#aaf,stroke:#555,stroke-width:2px
    style G fill:#aaf,stroke:#555,stroke-width:2px
    style I fill:#aaf,stroke:#555,stroke-width:2px
    style L fill:#aaf,stroke:#555,stroke-width:2px
    style Q fill:#aaf,stroke:#555,stroke-width:2px
    style S fill:#aaf,stroke:#555,stroke-width:2px
    style U fill:#aaf,stroke:#555,stroke-width:2px
    style W fill:#aaf,stroke:#555,stroke-width:2px
    style Z fill:#aaf,stroke:#555,stroke-width:2px
    style CC fill:#aaf,stroke:#555,stroke-width:2px
    style DD fill:#aaf,stroke:#555,stroke-width:2px
    style EE fill:#aaf,stroke:#555,stroke-width:2px
    style HH fill:#aaf,stroke:#555,stroke-width:2px

    style C fill:#88f,stroke:#333,stroke-width:2px
    style F fill:#88f,stroke:#333,stroke-width:2px
    style J fill:#88f,stroke:#333,stroke-width:2px
    style M fill:#88f,stroke:#333,stroke-width:2px
    style R fill:#88f,stroke:#333,stroke-width:2px
    style T fill:#88f,stroke:#333,stroke-width:2px
    style V fill:#88f,stroke:#333,stroke-width:2px
    style BB fill:#88f,stroke:#333,stroke-width:2px

    style N fill:#8ff,stroke:#333,stroke-width:2px
    style O fill:#8ff,stroke:#333,stroke-width:2px
    style X fill:#8ff,stroke:#333,stroke-width:2px
    style Y fill:#8ff,stroke:#333,stroke-width:2px
    style FF fill:#8ff,stroke:#333,stroke-width:2px
    style GG fill:#8ff,stroke:#333,stroke-width:2px
    style KK fill:#8ff,stroke:#333,stroke-width:2px
    style LL fill:#8ff,stroke:#333,stroke-width:2px

    style AA fill:#77f,stroke:#222,stroke-width:2px
    style II fill:#77f,stroke:#222,stroke-width:2px
```

## Преимущества разделения на домены:

    Независимое развитие: Каждый домен может развиваться независимо от других, что ускоряет time-to-market для новых функций и сервисов.

    Масштабируемость: Каждый домен может масштабироваться независимо от других, что обеспечивает гибкость и эффективность использования ресурсов.

    Улучшение производительности: Разделение данных и сервисов по доменам позволяет оптимизировать производительность каждого домена в отдельности.

    Безопасность: Разделение данных по доменам повышает безопасность и конфиденциальность информации.

    Упрощение интеграции: Integration bus обеспечивает единую точку доступа к данным и сервисам для всех потребителей, что упрощает интеграцию между доменами.