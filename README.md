# labsforBASE
Лабораторные работы по Базам Данных  
Анциферов Никита 02261-ДБ  
Вариант 7. Учет наличия товара на складе
## ER-диаграмма
<img alt="diagramm" src="er.png" />



## Логическая модель по диаграмме
**Сущность "Склады"**

Ключевой атрибут: номер_склада (уникальный идентификатор)

Описательные атрибуты: фио_кладовщика (строка, обязательный)

**Сущность "Товары"**

Ключевой атрибут: код_товара (уникальный идентификатор)

Описательные атрибуты: наименование_товара (строка, обязательный), цена_за_единицу (число, обязательный)

**Сущность "Накладные"**

Ключевой атрибут: номер_накладной (уникальный идентификатор)

Описательные атрибуты:

дата_документа (дата, обязательный)

тип_накладной (перечисление: "приход", "расход", обязательный)

Атрибуты-связи: склад (внешний ключ к сущности "Склады", обязательный)

**Сущность "Позиции_накладных"**

Ключевой атрибут: идентификатор_позиции (уникальный идентификатор)

Описательные атрибуты: количество (целое число, обязательный, больше 0)


## Физическая модель
```mermaid
erDiagram
    СКЛАДЫ ||--o{ НАКЛАДНЫЕ : "склад → накладные"
    НАКЛАДНЫЕ ||--|{ ПОЗИЦИИ_НАКЛАДНЫХ : "накладная → позиции"
    ТОВАРЫ ||--o{ ПОЗИЦИИ_НАКЛАДНЫХ : "товар → позиции"

    СКЛАДЫ {
        int номер_склада PK "NOT NULL"
        varchar фио_кладовщика "NOT NULL"
    }

    НАКЛАДНЫЕ {
        int номер_накладной PK "NOT NULL"
        date дата_документа "NOT NULL"
        varchar тип_накладной "NOT NULL CHECK приход расход"
        int склад FK "NOT NULL"
    }

    ТОВАРЫ {
        int код_товара PK "NOT NULL"
        varchar наименование_товара "NOT NULL"
        decimal цена_за_единицу "NOT NULL CHECK >0"
    }

    ПОЗИЦИИ_НАКЛАДНЫХ {
        int идентификатор_позиции PK "NOT NULL"
        int накладная FK "NOT NULL"
        int товар FK "NOT NULL"
        int количество "NOT NULL CHECK >0"
    }
```
 **Описание физической модели:**
1. Таблицы и их назначение:
СКЛАДЫ - хранит информацию о складах

ТОВАРЫ - справочник товаров с ценами

НАКЛАДНЫЕ - документы прихода/расхода товаров

ПОЗИЦИИ_НАКЛАДНЫХ - детализация накладных по товарам

2. Типы данных:
INTEGER - для идентификаторов

VARCHAR(n) - для текстовых полей

DECIMAL - для цен

DATE - для дат

3. Ограничения целостности:
PRIMARY KEY - первичные ключи

FOREIGN KEY - внешние ключи

NOT NULL - обязательные поля

CHECK - проверочные ограничения
## 2 лабораторная
<img width="853" height="292" alt="image" src="https://github.com/user-attachments/assets/a1a56901-a51d-4cc4-a1f4-54a440bfae88" />
<img width="507" height="579" alt="image" src="https://github.com/user-attachments/assets/37f076f7-2bf7-4feb-8707-0eea06d9aae0" />
<img width="726" height="708" alt="image" src="https://github.com/user-attachments/assets/9e783e5c-6691-420f-9207-f17953fa8880" />
<img width="722" height="728" alt="image" src="https://github.com/user-attachments/assets/bb1ed36a-538d-4285-94c0-9a4bb3a549a2" />
<img width="968" height="737" alt="image" src="https://github.com/user-attachments/assets/46e9a356-ed54-4cb4-8152-34b19f822072" />
<img width="534" height="629" alt="image" src="https://github.com/user-attachments/assets/5eb342e5-9cd2-4ecf-9aeb-9057df12cbfe" />


**Запросы с JOIN**

1 документ
<img width="1253" height="589" alt="image" src="https://github.com/user-attachments/assets/57c77512-eddf-4485-b57f-ac7ca65aa26d" />
2 документ
<img width="1143" height="638" alt="image" src="https://github.com/user-attachments/assets/3722e9a8-f6c8-458c-ab50-f4520feb43c6" />

## 3 лабораторная

**1. Процедура: Добавление новой приходной накладной**

<img width="510" height="612" alt="image" src="https://github.com/user-attachments/assets/c6514e0c-230c-4f66-8449-7992f0786c36" />
<img width="857" height="692" alt="image" src="https://github.com/user-attachments/assets/6f611f8a-08a1-491d-bd2f-6a90b9f9ddb1" />

**2. Процедура: Расчет стоимости накладной**
<img width="641" height="607" alt="image" src="https://github.com/user-attachments/assets/f19fd4f8-707b-4828-89d8-2ca9b7ee8e30" />
<img width="498" height="655" alt="image" src="https://github.com/user-attachments/assets/1ccd9f2b-5364-4bae-9a9c-39b24d430eba" />

**3. Представление: Остатки товаров на складах**
<img width="645" height="624" alt="image" src="https://github.com/user-attachments/assets/0613e637-778a-44bd-9dc4-eb8beb1fbf24" />
<img width="941" height="724" alt="image" src="https://github.com/user-attachments/assets/87ba297c-2ab2-4760-80d7-393486c9614d" />

**4. Представление: Ежемесячный отчет по движению товаров**
<img width="719" height="621" alt="image" src="https://github.com/user-attachments/assets/fe629df8-1189-4733-af7a-8776eff77b3e" />
<img width="500" height="703" alt="image" src="https://github.com/user-attachments/assets/2118ac09-8a81-4457-ae97-994bc00fa550" />

**5. Процедура для обновления цены товара**
<img width="779" height="731" alt="image" src="https://github.com/user-attachments/assets/814c9652-b757-45e1-bd19-44ca7f1cff57" />
<img width="953" height="691" alt="image" src="https://github.com/user-attachments/assets/427dcc79-e6c1-408c-87a2-43f2ff701a6b" />
<img width="574" height="538" alt="image" src="https://github.com/user-attachments/assets/868d0994-7dd2-4bb0-bc95-36f1fa40e65d" />

**6. Процедура: Изменить кладовщика на складе**
<img width="1031" height="729" alt="image" src="https://github.com/user-attachments/assets/02367164-bd5d-434c-b936-bb8c0c5581c0" />
<img width="698" height="617" alt="image" src="https://github.com/user-attachments/assets/8039d091-caf6-4915-a314-6eb48fe9ed7f" />

## 4 лаба
 **1. Генератор для таблицы СКЛАДЫ (20,000 записей)**
<img width="786" height="628" alt="image" src="https://github.com/user-attachments/assets/6c48ab99-4820-4dd9-bfa3-2f025589dbfb" />
<img width="349" height="238" alt="image" src="https://github.com/user-attachments/assets/5043e83d-36e6-4b0c-97ed-fefe31ce116e" />
**2. Генератор для таблицы ТОВАРЫ (20,000 записей)**
<img width="756" height="626" alt="image" src="https://github.com/user-attachments/assets/7388d58f-655d-4f55-a099-c460f737e9d6" />
<img width="414" height="243" alt="image" src="https://github.com/user-attachments/assets/94fb716c-1c8c-4a69-90b2-08d94ab47b6a" />

**3. Генератор для таблицы НАКЛАДНЫЕ (20,000 записей)**
<img width="697" height="720" alt="image" src="https://github.com/user-attachments/assets/e9cb61fd-affb-4de8-9a8c-365723fd86d6" />
<img width="371" height="301" alt="image" src="https://github.com/user-attachments/assets/cb4119aa-7f87-4a71-a9d3-f6184f75d261" />

**4 Генератор позиций накладных (20000 записей)**

<img width="697" height="797" alt="image" src="https://github.com/user-attachments/assets/9ac1ca75-5936-4ead-8304-fac7f7d2bf5b" />
<img width="686" height="255" alt="image" src="https://github.com/user-attachments/assets/85703561-84d1-4adf-b5d2-552e550a3abd" />
<img width="341" height="277" alt="image" src="https://github.com/user-attachments/assets/b7fe8752-4a69-4c62-8ed9-f84d4bc82645" />

## Оптимизация
<img width="985" height="335" alt="image" src="https://github.com/user-attachments/assets/b826ba1f-f7b3-4aa4-859c-40b12f55a202" />
<img width="447" height="285" alt="image" src="https://github.com/user-attachments/assets/fb7cb5d9-b06b-42c9-82f4-7b97b2c54cf5" />
<img width="940" height="504" alt="image" src="https://github.com/user-attachments/assets/ddd9317f-d4b0-4e41-8cdf-e2a2488b2eb5" />
<img width="437" height="302" alt="image" src="https://github.com/user-attachments/assets/6b1fdd23-48cb-4f98-9d56-0cd97db4fae1" />
<img width="1074" height="561" alt="image" src="https://github.com/user-attachments/assets/d06e316f-e1d4-4af0-b957-99470946a958" />
**Итог: с индексами производительность быстрее**


