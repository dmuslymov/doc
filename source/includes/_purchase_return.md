## Документ Возврат поставщику
Средствами JSON API можно создавать и обновлять сведения о Возвратах поставщикам, запрашивать списки Возвратов поставщикам и сведения по отдельным Возвратам поставщикам. Позициями Возвратов поставщикам можно управлять как в составе отдельного Возврата, так и отдельно - с помощью специальных ресурсов для управления позициями Возврата поставщику. Кодом сущности для Возврата поставщику в составе JSON API является ключевое слово **purchasereturn**.
### Возвраты поставщикам 
#### Атрибуты сущности
+ **meta** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о Возврате поставщику
+ **id** - ID в формате UUID `Только для чтения`
+ **accountId** - ID учетной записи `Только для чтения`
+ **syncId** - ID синхронизации. После заполнения недоступен для изменения.
+ **updated** - Момент последнего обновления сущности `Только для чтения`
+ **deleted** - Момент последнего удаления сущности `Только для чтения`
+ **name** - номер Возврата поставщику
+ **description** - Комментарий Возврата поставщику
+ **externalCode** - Внешний код Возврата поставщику
+ **moment** - Дата Возврата поставщику
+ **applicable** - Отметка о проведении
+ **vatEnabled** - Учитывается ли НДС
+ **vatIncluded** - Включен ли НДС в цену
+ **sum** - Сумма Возврата поставщику в копейках `Только для чтения`
+ **rate** - Валюта
+ **owner** - Ссылка на Владельца (Сотрудника) в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **shared** - Общий доступ
+ **group** - Отдел сотрудника в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **organization** - Ссылка на ваше юрлицо в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные) `Необходимое`
+ **agent** - Ссылка на контрагента в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **store** - Ссылка на склад в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные) `Необходимое`
+ **contract** - Ссылка на договор в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **project** - Ссылка на проект в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **state** - Статус Возврата поставщику в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **organizationAccount** - Ссылка на счёт вашего юрлица в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **agentAccount** - Ссылка на счёт контрагента в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **attributes** - Коллекция доп. полей в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
<br>Поля при expand'е:</br>
  - **name** - номер документа
  - **moment** - дата печати
  - **href** - ссылка на файл печатной формы
  - **fileName** - название файла печатной формы
  - **updated** - дата последнего изменения
+ **created** - Дата создания `Только для чтения`
+ **vatSum** - Сумма НДС `Только для чтения`
#### Связи с другими документами
+ **positions** - Ссылка на позиции Возврата поставщику в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **supply** - Ссылка на приёмку, по которой произошёл возврат в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные) Поле является необходимым для возврата с основанием.
+ **factureOut** - Ссылка на счет-фактура выданный в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **payedSum** - Сумма входящих платежей по возврату поставщику
+ **payments** - Массив ссылок на связанные платежи в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)

#### Позиции Возврата поставщику
Позиции Возврата поставщику - это список товаров/услуг/модификаций/серий.
Объект позиции Возврата поставщику содержит следующие поля:
+ **id** - ID товара в формате UUID `Только для чтения`
+ **accountId** - ID учетной записи `Только для чтения`
+ **quantity** - Количество товаров/услуг данного вида в позиции. Если позиция - товар, у которого включен учёт по серийным номерам, то значение в этом поле всегда будет равно количеству серийных номеров для данной позиции в документе.
+ **price** - Цена товара/услуги в копейках
+ **discount** - Процент скидки или наценки. Должен совпадать с указанным в приёмке (игнорируется для возвратов без основания)
+ **vat** - НДС, которым облагается текущая позиция
+ **assortment** - Ссылка на товар/услугу/серию/модификацию, которую представляет собой позиция, в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **pack** - Упаковка товара
+ **things** - Серийные номера
Значение данного атрибута игнорируется, если товар позиции не находится на серийном учете.
В ином случае количество товаров в позиции будет равно количеству серийных номеров, переданных в значении атрибута.

С позициями можно работать с помощью специальных [ресурсов для управления позициями Возврата поставщику](#документ-возврат-поставщику-позиции-возврата-поставщику),
а также в составе отдельного Возврата поставщику. При работе в составе отдельного Возврата поставщику,
вы можете отправлять запросы на создание отдельного Возврата поставщику с включенным в тело запроса
массивом позиций Возврата поставщику. Если количество позиций превышает максимально допустимое, то для
дальнейшего пополнения позиций нужно будет работать со специальным ресурсом "Позиции Возврата поставщику".
Также, при работе в составе отдельного Возврата поставщику, можно отправлять запросы на обновление списка позиций
с включенным в тело запроса массивом позиций Возврата поставщику. При этом важно помнить, что коллекция позиций будет
восприниматься как "все позиции Возврата поставщику" и полностью заменит уже существующую коллекцию при обновлении объекта - лишние
позиции будут удалены, новые добавлены, существующие - изменены.

О работе с доп. полями Возвратов поставщикамых возвратов можно прочитать [здесь](/api/remap/1.2/doc/index.html#header-работа-с-дополнительными-полями)

### Получить Возвраты поставщикам 
Запрос всех Возвратов поставщикам на данной учётной записи.
Результат: Объект JSON, включающий в себя поля:
- **meta** [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о выдаче,
- **context** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о сотруднике, выполнившем запрос.
- **rows** - Массив JSON объектов, представляющих собой Возвраты поставщикам.

**Параметры**

| Параметр                | Описание  |
| ------------------------------ |:---------------------------|
|limit |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|offset |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить Возвраты поставщикам

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка Возвратов поставщикам.

```json
{
  "context": {
    "employee": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/context/employee",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    }
  },
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json",
    "size": 4,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/b875cc8f-313f-11e6-8a84-bae500000093",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
        "type": "purchasereturn",
        "mediaType": "application/json"
      },
      "id": "b875cc8f-313f-11e6-8a84-bae500000093",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "owner": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
          "type": "employee",
          "mediaType": "application/json"
        }
      },
      "shared": false,
      "group": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
          "type": "group",
          "mediaType": "application/json"
        }
      },
      "updated": "2016-06-13 11:20:55",
      "name": "00001",
      "externalCode": "E4l6sMtVixklOjgfK6VQt3",
      "moment": "2016-06-13 11:20:00",
      "applicable": true,
      "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "sum": 0,
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/faf44002-2e58-11e6-8a84-bae500000053",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/b875cc8f-313f-11e6-8a84-bae500000093/positions",
          "type": "purchasereturnposition",
          "mediaType": "application/json",
          "size": 1,
          "limit": 1000,
          "offset": 0
        }
      },
      "supply": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/b1008773-313f-11e6-8a84-bae500000089",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
          "type": "supply",
          "mediaType": "application/json"
        }
      },
      "payedSum": 0
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/d43161ea-3140-11e6-8a84-bae5000000c6",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
        "type": "purchasereturn",
        "mediaType": "application/json"
      },
      "id": "d43161ea-3140-11e6-8a84-bae5000000c6",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "owner": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
          "type": "employee",
          "mediaType": "application/json"
        }
      },
      "shared": false,
      "group": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
          "type": "group",
          "mediaType": "application/json"
        }
      },
      "updated": "2016-06-13 11:28:34",
      "name": "00002",
      "externalCode": "-5xto6PjiGhuL8RAky-9c3",
      "moment": "2016-06-13 11:22:00",
      "applicable": true,
      "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "sum": 273000,
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/faf44002-2e58-11e6-8a84-bae500000053",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/d43161ea-3140-11e6-8a84-bae5000000c6/positions",
          "type": "purchasereturnposition",
          "mediaType": "application/json",
          "size": 2,
          "limit": 1000,
          "offset": 0
        }
      },
      "supply": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/f39a60f5-313f-11e6-8a84-bae5000000b4",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
          "type": "supply",
          "mediaType": "application/json"
        }
      },
      "payedSum": 0
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/dc194230-41bd-11e6-8a84-bae5000000a9",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
        "type": "purchasereturn",
        "mediaType": "application/json"
      },
      "id": "dc194230-41bd-11e6-8a84-bae5000000a9",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "owner": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
          "type": "employee",
          "mediaType": "application/json"
        }
      },
      "shared": false,
      "group": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
          "type": "group",
          "mediaType": "application/json"
        }
      },
      "updated": "2016-07-04 11:03:57",
      "name": "00003",
      "externalCode": "-SmYzmhBjSFQBveIJQ6uV0",
      "moment": "2016-07-04 11:03:00",
      "applicable": true,
      "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "sum": 28000,
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "contract": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/2b34d43f-3f52-11e6-8a84-bae500000066",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
          "type": "contract",
          "mediaType": "application/json"
        }
      },
      "project": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/722e39f0-313e-11e6-8a84-bae500000008",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/project/metadata",
          "type": "project",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1489a08d-32ca-11e6-8a84-bae50000000d",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "agentAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1489a08d-32ca-11e6-8a84-bae50000000d/accounts/1489ad8d-32ca-11e6-8a84-bae50000000e",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/dc194230-41bd-11e6-8a84-bae5000000a9/positions",
          "type": "purchasereturnposition",
          "mediaType": "application/json",
          "size": 7,
          "limit": 1000,
          "offset": 0
        }
      },
      "supply": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/ceec2ca6-41bd-11e6-8a84-bae500000097",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
          "type": "supply",
          "mediaType": "application/json"
        }
      },
      "payedSum": 0
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
        "type": "purchasereturn",
        "mediaType": "application/json"
      },
      "id": "e699b298-41bd-11e6-8a84-bae5000000ba",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "owner": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
          "type": "employee",
          "mediaType": "application/json"
        }
      },
      "shared": false,
      "group": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
          "type": "group",
          "mediaType": "application/json"
        }
      },
      "updated": "2016-07-04 11:04:15",
      "name": "00004",
      "externalCode": "tBSZzXSgggWNL5MZ7IrYE2",
      "moment": "2016-07-04 11:04:00",
      "applicable": true,
      "rate": {
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
      },
      "sum": 43156000,
      "organization": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
          "type": "organization",
          "mediaType": "application/json"
        }
      },
      "store": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
          "type": "store",
          "mediaType": "application/json"
        }
      },
      "contract": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/91287d9a-41bc-11e6-8a84-bae500000082",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
          "type": "contract",
          "mediaType": "application/json"
        }
      },
      "project": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/722e39f0-313e-11e6-8a84-bae500000008",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/project/metadata",
          "type": "project",
          "mediaType": "application/json"
        }
      },
      "agent": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/14bfc067-32ca-11e6-8a84-bae50000003f",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
          "type": "counterparty",
          "mediaType": "application/json"
        }
      },
      "organizationAccount": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
          "type": "account",
          "mediaType": "application/json"
        }
      },
      "vatEnabled": true,
      "vatIncluded": true,
      "positions": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions",
          "type": "purchasereturnposition",
          "mediaType": "application/json",
          "size": 7,
          "limit": 1000,
          "offset": 0
        }
      },
      "supply": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/80d04ebc-41bd-11e6-8a84-bae500000085",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
          "type": "supply",
          "mediaType": "application/json"
        }
      },
      "payedSum": 0
    }
  ]
}
```

### Создать Возврат поставщику 
Обязательные поля при создании нового Возврата поставщику:
+ **name** - Номер возврата
+ **organization** - Ссылка на ваше юрлицо в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **store** - Ссылка на склад в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **supply** - Ссылка на приёмку, по которой произошёл возврат в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные), обязательное поле только для возврата по основанию
+ **agent** - Ссылка на контрагента в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
Контрагент, указанный в запросе на создание возврата, должен совпадать с контрагентом, указанном в документе,
по которому создаётся возврат.

При создании возврата:
+ При создании возврата без основания поле **supply** указывать не нужно
+ Контрагент в возврате и в документе, по которому он создаётся, должны совпадать
+ Валюта и юрлицо в возврате и в документе так же должны совпадать
+ При передаче коллекции **positions** в теле запроса на создание возврата, передаваемые позиции
должны соответствовать позициям в документе. Различие может быть только в количестве товара в позиции
(меньшее либо равное количеству в документе). Нельзя передать позиции, которых нет в документе.

> Пример создания нового Возврата поставщику на основании приемки.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn"
    -H "Authorization: Basic <Access-Token>"
    -H "Content-Type: application/json"
      -d '{
            "name": "77887",
            "owner": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json"
              }
            },
            "shared": false,
            "group": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                "type": "group",
                "mediaType": "application/json"
              }
            },
            "description": "Возврат поставщику созданный через API",
            "code": "8865255398",
            "externalCode": "fruitsareawesome124",
            "moment": "2016-11-21 14:37:00",
            "applicable": true,
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "agent": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "store": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
                "value": "отломана деталь"
              },
              {
                "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
                "value": false
              }
            ],
            "positions": [
              {
                "quantity": 1,
                "price": 1241200,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 24100,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                    "type": "service",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 2421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              }
            ],
            "supply": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
                "type": "supply",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json"
  },
  "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": false,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2016-07-04 11:29:29",
  "name": "77887",
  "description": "Возврат поставщику созданный через API",
  "code": "8865255398",
  "externalCode": "fruitsareawesome124",
  "moment": "2016-11-21 14:37:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 4107300,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
      "name": "Брак продукции",
      "type": "boolean",
      "value": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
      "name": "Причина, отличная от брака",
      "type": "text",
      "value": "отломана деталь"
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "created": "2007-02-07 17:16:41",
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 1000,
      "offset": 0
    }
  },
  "supply": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
      "type": "supply",
      "mediaType": "application/json"
    }
  },
  "payedSum": 0
}
```

> Пример создания нового Возврата поставщику без основания.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn"
    -H "Authorization: Basic <Access-Token>"
    -H "Content-Type: application/json"
      -d '{
            "name": "77887",
            "owner": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json"
              }
            },
            "shared": false,
            "group": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                "type": "group",
                "mediaType": "application/json"
              }
            },
            "description": "Возврат поставщику созданный через API",
            "code": "8865255398",
            "externalCode": "fruitsareawesome124",
            "moment": "2016-11-21 14:37:00",
            "applicable": true,
            "organization": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                "type": "organization",
                "mediaType": "application/json"
              }
            },
            "agent": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                "type": "counterparty",
                "mediaType": "application/json"
              }
            },
            "store": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                "type": "store",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
                "value": "отломана деталь"
              },
              {
                "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
                "value": false
              }
            ],
            "positions": [
              {
                "quantity": 1,
                "price": 1241200,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 24100,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                    "type": "service",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 2421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданного Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json"
  },
  "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": false,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2016-07-04 11:29:29",
  "name": "77887",
  "description": "Возврат поставщику созданный через API",
  "code": "8865255398",
  "externalCode": "fruitsareawesome124",
  "moment": "2016-11-21 14:37:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 4107300,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
      "name": "Брак продукции",
      "type": "boolean",
      "value": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
      "name": "Причина, отличная от брака",
      "type": "text",
      "value": "отломана деталь"
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "created": "2007-02-07 17:16:41",
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 4,
      "limit": 100,
      "offset": 0
    }
  },
  "payedSum": 0
}
```

### Массовое создание и обновление Возвратов поставщику 
[Массовое создание и обновление](/api/remap/1.2/doc/index.html#header-создание-и-обновление-нескольких-объектов) Возвратов поставщику.
В теле запроса нужно передать массив, содержащий JSON представления Возвратов поставщику, которые вы хотите создать или обновить.
Обновляемые Возвраты поставщику должны содержать идентификатор в виде метаданных.

> Пример создания и обновления нескольких Возвратов поставщику

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn"
    -H "Authorization: Basic <Access-Token>"
    -H "Content-Type: application/json"
      -d '[
            {
              "name": "77887",
              "owner": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                  "type": "employee",
                  "mediaType": "application/json"
                }
              },
              "shared": false,
              "group": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                  "type": "group",
                  "mediaType": "application/json"
                }
              },
              "description": "Возврат поставщику созданный через API",
              "code": "8865255398",
              "externalCode": "fruitsareawesome124",
              "moment": "2016-11-21 14:37:00",
              "applicable": true,
              "organization": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
                  "type": "organization",
                  "mediaType": "application/json"
                }
              },
              "agent": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
                  "type": "counterparty",
                  "mediaType": "application/json"
                }
              },
              "store": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
                  "type": "store",
                  "mediaType": "application/json"
                }
              },
              "attributes": [
                {
                  "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
                  "value": "отломана деталь"
                },
                {
                  "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
                  "value": false
                }
              ],
              "positions": [
                {
                  "quantity": 1,
                  "price": 1241200,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 24100,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 421000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                      "type": "service",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 2421000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                }
              ],
              "supply": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
                  "type": "supply",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
                "type": "purchasereturn",
                "mediaType": "application/json"
              },
              "name": "763457",
              "owner": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/1205364b-7f01-455a-a1b5-4ba0988c8308",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                  "type": "employee",
                  "mediaType": "application/json"
                }
              },
              "shared": true,
              "group": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/348d910b-6dc0-483f-b916-2237bc54a04e",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                  "type": "group",
                  "mediaType": "application/json"
                }
              },
              "description": "Возврат поставщику созданный и обновлённый через API",
              "code": "8865255398",
              "externalCode": "fruitsareawesome!!!",
              "moment": "2016-11-21 14:27:00",
              "applicable": false,
              "state": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
                  "type": "state",
                  "mediaType": "application/json"
                }
              },
              "attributes": [
                {
                  "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
                  "value": true
                }
              ],
              "positions": [
                {
                  "quantity": 1,
                  "price": 1241200,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 24100,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 421000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                      "type": "service",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 2421000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                },
                {
                  "quantity": 1,
                  "price": 263000,
                  "discount": 0,
                  "vat": 0,
                  "assortment": {
                    "meta": {
                      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/20485cfd-2e62-11e6-8a84-bae500000112",
                      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                      "type": "product",
                      "mediaType": "application/json"
                    }
                  }
                }
              ]
            }
          ]'  
```

> Response 200 (application/json)
Успешный запрос. Результат - массив JSON представлений созданных и обновленных Возвратов поставщику.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
      "type": "purchasereturn",
      "mediaType": "application/json"
    },
    "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "owner": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    },
    "shared": false,
    "group": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
        "type": "group",
        "mediaType": "application/json"
      }
    },
    "updated": "2016-07-04 11:29:29",
    "name": "77887",
    "description": "Возврат поставщику созданный через API",
    "code": "8865255398",
    "externalCode": "fruitsareawesome124",
    "moment": "2016-11-21 14:37:00",
    "applicable": true,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      }
    },
    "sum": 4107300,
    "organization": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
        "type": "organization",
        "mediaType": "application/json"
      }
    },
    "store": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
        "type": "store",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "organizationAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "agentAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "attributes": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
        "name": "Брак продукции",
        "type": "boolean",
        "value": false
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "name": "Причина, отличная от брака",
        "type": "text",
        "value": "отломана деталь"
      }
    ],
    "vatEnabled": true,
    "vatIncluded": true,
    "created": "2007-02-07 17:16:41",
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
        "type": "purchasereturnposition",
        "mediaType": "application/json",
        "size": 4,
        "limit": 1000,
        "offset": 0
      }
    },
    "supply": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
        "type": "supply",
        "mediaType": "application/json"
      }
    },
    "payedSum": 0
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
      "type": "purchasereturn",
      "mediaType": "application/json"
    },
    "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "owner": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/1205364b-7f01-455a-a1b5-4ba0988c8308",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    },
    "shared": true,
    "group": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/348d910b-6dc0-483f-b916-2237bc54a04e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
        "type": "group",
        "mediaType": "application/json"
      }
    },
    "updated": "2016-07-04 11:35:26",
    "name": "763457",
    "description": "Возврат поставщику созданный и обновлённый через API",
    "code": "8865255398",
    "externalCode": "fruitsareawesome!!!",
    "moment": "2016-11-21 14:27:00",
    "applicable": false,
    "rate": {
      "currency": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
          "type": "currency",
          "mediaType": "application/json"
        }
      }
    },
    "sum": 4370300,
    "organization": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
        "type": "organization",
        "mediaType": "application/json"
      }
    },
    "store": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
        "type": "store",
        "mediaType": "application/json"
      }
    },
    "agent": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json"
      }
    },
    "state": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
        "type": "state",
        "mediaType": "application/json"
      }
    },
    "organizationAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "agentAccount": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
        "type": "account",
        "mediaType": "application/json"
      }
    },
    "attributes": [
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
        "name": "Брак продукции",
        "type": "boolean",
        "value": true
      },
      {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
          "type": "attributemetadata",
          "mediaType": "application/json"
        },
        "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "name": "Причина, отличная от брака",
        "type": "text",
        "value": "отломана деталь"
      }
    ],
    "vatEnabled": true,
    "vatIncluded": true,
    "created": "2007-02-07 17:16:41",
    "positions": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
        "type": "purchasereturnposition",
        "mediaType": "application/json",
        "size": 5,
        "limit": 1000,
        "offset": 0
      }
    },
    "supply": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
        "type": "supply",
        "mediaType": "application/json"
      }
    },
    "payedSum": 0
  }
]
```

### Удалить Возврат поставщику

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
 
> Запрос на удаление Возврата поставщику с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешное удаление Возврата поставщику.

### Метаданные Возвратов поставщикам 
#### Метаданные Возвратов поставщикам 
Запрос на получение метаданных Возвратов поставщикам. Результат - объект JSON, включающий в себя:
+ **meta** - Ссылка на метаданные Возвратов поставщикам
+ **attributes** - Массив объектов доп. полей Возвратов поставщикам в формате [Метаданных](/api/remap/1.2/doc/index.html#header-метаданные)
+ **states** - Массив статусов Возвратов поставщикам
+ **createShared** - создавать новые Возвраты поставщикам с меткой "Общий"

Структура отдельного объекта, представляющего доп. поле подробно описана в разделе [Работа с дополнительными полями](/api/remap/1.2/doc/index.html#header-работа-с-дополнительными-полями).

> Метаданные Возвратов поставщикам

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление доп. полей Возвратов поставщикам.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "mediaType": "application/json"
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
      "name": "Брак продукции",
      "type": "boolean",
      "required": false
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
      "name": "Причина, отличная от брака",
      "type": "text",
      "required": false
    }
  ],
  "states": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e394ff-41be-11e6-8a84-bae5000000d0",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "69e394ff-41be-11e6-8a84-bae5000000d0",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Оформлен",
      "color": 9245744,
      "stateType": "Regular",
      "entityType": "purchasereturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39958-41be-11e6-8a84-bae5000000d1",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "69e39958-41be-11e6-8a84-bae5000000d1",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Произведён частично",
      "color": 4354177,
      "stateType": "Regular",
      "entityType": "purchasereturn"
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
        "type": "state",
        "mediaType": "application/json"
      },
      "id": "69e39d04-41be-11e6-8a84-bae5000000d2",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "name": "Произведён",
      "color": 8825440,
      "stateType": "Regular",
      "entityType": "purchasereturn"
    }
  ],
  "createShared": false
}
```

### Отдельное доп. поле

#### Отдельное доп. поле

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Доп. поля.|
 
> Запрос на получение информации по отдельному дополнительному полю.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельного доп. поля.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
    "type": "attributemetadata",
    "mediaType": "application/json"
  },
  "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
  "name": "Причина, отличная от брака",
  "type": "text",
  "required": false
}
```

### Шаблон возврата поставщику 
#### Шаблон возврата поставщику 
Запрос на получение предзаполненого стандартными значениями шаблона возврата поставщику без связи с каким-либо документом.

> Создание шаблона возврата поставщику с пустым телом запроса

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/new"
    -H "Authorization: Basic <Access-Token>"
    -H "Content-Type: application/json"
      -d ''  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного Возврата поставщику.

```json
{
  "applicable": false,
  "sum": 0,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "created": "2007-02-07 17:16:41",
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    },
    "rows": []
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "payedSum": 0
}
```

### Шаблон возврата поставщику на основе 
Запрос на получение предзаполненного шаблона возврата поставщику на основе переданной приёмки.
В ответ на запрос вернётся предзаполненный шаблон возврата поставщику, который
затем можно будет использовать для создания нового возврата с помощью POST запроса.

> Пример запроса на создание шаблона возврата поставщику на основе приёмки.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/new"
    -H "Authorization: Basic <Access-Token>"
    -H "Content-Type: application/json"
      -d '{
            "supply": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/373d2925-4a98-11e6-8a84-bae500000069",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
                "type": "supply",
                "mediaType": "application/json"
              }
            }
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление предзаполненного Возврата поставщику.

```json
{
  "applicable": false,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 0,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/1485d676-32ca-11e6-8a84-bae500000009/accounts/1485e43e-32ca-11e6-8a84-bae50000000a",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "created": "2007-02-07 17:16:41",
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 0,
      "limit": 1000,
      "offset": 0
    },
    "rows": []
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "supply": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/373d2925-4a98-11e6-8a84-bae500000069",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
      "type": "supply",
      "mediaType": "application/json"
    }
  },
  "payedSum": 0
}
```

### Возврат поставщику
 
### Получить Возврат поставщику

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
 
> Запрос на получение отдельного Возврата поставщику с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление Возврата поставщику с указанным id.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json"
  },
  "id": "e699b298-41bd-11e6-8a84-bae5000000ba",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/faba7f37-2e58-11e6-8a84-bae500000028",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": false,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/f97aa1fb-2e58-11e6-8a84-bae500000002",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2016-07-04 11:04:15",
  "name": "00004",
  "externalCode": "tBSZzXSgggWNL5MZ7IrYE2",
  "moment": "2016-07-04 11:04:00",
  "applicable": true,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 43156000,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "contract": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/contract/91287d9a-41bc-11e6-8a84-bae500000082",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/contract/metadata",
      "type": "contract",
      "mediaType": "application/json"
    }
  },
  "project": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/project/722e39f0-313e-11e6-8a84-bae500000008",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/project/metadata",
      "type": "project",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/14bfc067-32ca-11e6-8a84-bae50000003f",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "vatEnabled": true,
  "vatIncluded": true,
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 7,
      "limit": 1000,
      "offset": 0
    }
  },
  "supply": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/80d04ebc-41bd-11e6-8a84-bae500000085",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
      "type": "supply",
      "mediaType": "application/json"
    }
  },
  "payedSum": 0
}
```

### Изменить Возврат поставщику 
Запрос на обновление Возврата поставщику с указанным id.
В теле запроса можно указать только те поля, которые необходимо изменить у Возврата поставщику, кроме тех, что
помечены `Только для чтения` в описании [атрибутов Возврата поставщику](#документ-возврат-поставщику-возвраты-поставщикам).
При обновлении полей **organization** и **agent** нужно также обновить поля **organizationAccount** и
**agentAccount** соответственно, иначе произойдёт ошибка.
Контрагент должен совпадать с контрагентом, указанным в документе, по которому создаётся возврат.

При обновлении возврата:
+ Нельзя изменять следующие поля: **agentAccount**, **agent**, **supply**
+ Нельзя выставить валюту отличную от валюты в документе
+ Нельзя добавить позиции, отсутствующие среди позиций документа.

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|

> Пример запроса на обновление Возврата поставщику.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19"
    -H "Authorization: Basic <Access-Token>"
    -H "Content-Type: application/json"
      -d '{
            "name": "763457",
            "owner": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/1205364b-7f01-455a-a1b5-4ba0988c8308",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json"
              }
            },
            "shared": true,
            "group": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/348d910b-6dc0-483f-b916-2237bc54a04e",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
                "type": "group",
                "mediaType": "application/json"
              }
            },
            "description": "Возврат поставщику созданный и обновлённый через API",
            "code": "8865255398",
            "externalCode": "fruitsareawesome!!!",
            "moment": "2016-11-21 14:27:00",
            "applicable": false,
            "state": {
              "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
                "type": "state",
                "mediaType": "application/json"
              }
            },
            "attributes": [
              {
                "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
                "value": true
              }
            ],
            "positions": [
              {
                "quantity": 1,
                "price": 1241200,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e6447ee7-3303-11e6-8a84-bae5000149c2",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 24100,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8517bc4-3303-11e6-8a84-bae500014de1",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/service/6767bc73-3d19-11e6-8a84-bae500000002",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/service/metadata",
                    "type": "service",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 2421000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/e8563cc5-3303-11e6-8a84-bae500014df0",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              },
              {
                "quantity": 1,
                "price": 263000,
                "discount": 0,
                "vat": 0,
                "assortment": {
                  "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/20485cfd-2e62-11e6-8a84-bae500000112",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                    "type": "product",
                    "mediaType": "application/json"
                  }
                }
              }
            ]
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновлённого Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c",
    "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata",
    "type": "purchasereturn",
    "mediaType": "application/json"
  },
  "id": "6d5371fc-41c1-11e6-8a84-bae50000001c",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "owner": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/1205364b-7f01-455a-a1b5-4ba0988c8308",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
      "type": "employee",
      "mediaType": "application/json"
    }
  },
  "shared": true,
  "group": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/group/348d910b-6dc0-483f-b916-2237bc54a04e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/group/metadata",
      "type": "group",
      "mediaType": "application/json"
    }
  },
  "updated": "2016-07-04 11:35:26",
  "name": "763457",
  "description": "Возврат поставщику созданный и обновлённый через API",
  "code": "8865255398",
  "externalCode": "fruitsareawesome!!!",
  "moment": "2016-11-21 14:27:00",
  "applicable": false,
  "rate": {
    "currency": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/currency/baac25f0-50ac-11e5-300d-c79b00000055",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/currency/metadata",
        "type": "currency",
        "mediaType": "application/json"
      }
    }
  },
  "sum": 4370300,
  "organization": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/organization/metadata",
      "type": "organization",
      "mediaType": "application/json"
    }
  },
  "store": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/store/faf3ff5b-2e58-11e6-8a84-bae500000050",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/store/metadata",
      "type": "store",
      "mediaType": "application/json"
    }
  },
  "agent": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/metadata",
      "type": "counterparty",
      "mediaType": "application/json"
    }
  },
  "state": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/states/69e39d04-41be-11e6-8a84-bae5000000d2",
      "type": "state",
      "mediaType": "application/json"
    }
  },
  "organizationAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/organization/fae3561a-2e58-11e6-8a84-bae50000004e/accounts/fae39d66-2e58-11e6-8a84-bae50000004f",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "agentAccount": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/counterparty/147c1f1b-32ca-11e6-8a84-bae500000004/accounts/147c3231-32ca-11e6-8a84-bae500000005",
      "type": "account",
      "mediaType": "application/json"
    }
  },
  "attributes": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e124-41be-11e6-8a84-bae5000000cb",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e124-41be-11e6-8a84-bae5000000cb",
      "name": "Брак продукции",
      "type": "boolean",
      "value": true
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/metadata/attributes/4fc7e7e7-41be-11e6-8a84-bae5000000cc",
        "type": "attributemetadata",
        "mediaType": "application/json"
      },
      "id": "4fc7e7e7-41be-11e6-8a84-bae5000000cc",
      "name": "Причина, отличная от брака",
      "type": "text",
      "value": "отломана деталь"
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "created": "2007-02-07 17:16:41",
  "positions": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/6d5371fc-41c1-11e6-8a84-bae50000001c/positions",
      "type": "purchasereturnposition",
      "mediaType": "application/json",
      "size": 5,
      "limit": 1000,
      "offset": 0
    }
  },
  "supply": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/supply/7585391b-41c0-11e6-8a84-bae5000000de",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/supply/metadata",
      "type": "supply",
      "mediaType": "application/json"
    }
  },
  "payedSum": 0
}
```

### Позиции Возврата поставщику 
Отдельный ресурс для управления позициями Возврата поставщику. С его помощью вы можете управлять позициями большого документа, количество строк в котором превышает лимит на количество строк, сохраняемых вместе с документом. Этот лимит равен 100. Более подробно о лимитах на количество строк документа и работе с большими документами можно прочитать [тут](/api/remap/1.2/doc/index.html#header-работа-с-позициями-документов).

### Получить Позиции 
Запрос на получение списка всех позиций данной Возврата поставщику.
- **meta** [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о выдаче,
- **context** - [Метаданные](/api/remap/1.2/doc/index.html#header-метаданные) о сотруднике, выполнившем запрос.
- **rows** - Массив JSON объектов, представляющих собой позиции Возврата поставщику.

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
|limit |  `number` (optional) **Default: 1000** *Example: 1000* Максимальное количество сущностей для извлечения.`Допустимые значения 1 - 1000`.|
|offset |  `number` (optional) **Default: 0** *Example: 40* Отступ в выдаваемом списке сущностей.|

> Получить Позиции

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление списка позиций Возврата поставщику.

```json
{
  "context": {
    "employee": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/context/employee",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json"
      }
    }
  },
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions",
    "type": "purchasereturnposition",
    "mediaType": "application/json",
    "size": 7,
    "limit": 1000,
    "offset": 0
  },
  "rows": [
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699bc75-41bd-11e6-8a84-bae5000000bb",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699bc75-41bd-11e6-8a84-bae5000000bb",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 40,
      "price": 34400,
      "discount": 0,
      "vat": 0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/a69fe5c3-3303-11e6-8a84-bae50000dfab",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699c2b5-41bd-11e6-8a84-bae5000000bc",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699c2b5-41bd-11e6-8a84-bae5000000bc",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 52,
      "price": 556000,
      "discount": 0,
      "vat": 0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0464a192-3304-11e6-8a84-bae500017f51",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699c804-41bd-11e6-8a84-bae5000000bd",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699c804-41bd-11e6-8a84-bae5000000bd",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 32,
      "price": 200000,
      "discount": 0,
      "vat": 0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/044e812a-3304-11e6-8a84-bae500017f34",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699cd72-41bd-11e6-8a84-bae5000000be",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699cd72-41bd-11e6-8a84-bae5000000be",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 112,
      "price": 34000,
      "discount": 0,
      "vat": 0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/048b1a8b-3304-11e6-8a84-bae500017f84",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699d288-41bd-11e6-8a84-bae5000000bf",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699d288-41bd-11e6-8a84-bae5000000bf",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 76,
      "price": 35000,
      "discount": 0,
      "vat": 0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/27eba7b5-3303-11e6-8a84-bae500002b72",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699d76d-41bd-11e6-8a84-bae5000000c0",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699d76d-41bd-11e6-8a84-bae5000000c0",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 6000,
      "price": 0,
      "discount": 0,
      "vat": 0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/130a02d7-3303-11e6-8a84-bae500001887",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json"
        }
      }
    },
    {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699dcb4-41bd-11e6-8a84-bae5000000c1",
        "type": "purchasereturnposition",
        "mediaType": "application/json"
      },
      "id": "e699dcb4-41bd-11e6-8a84-bae5000000c1",
      "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
      "quantity": 75,
      "price": 0,
      "discount": 0,
      "vat": 0,
      "assortment": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0475cacb-3303-11e6-8a84-bae500000765",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
          "type": "product",
          "mediaType": "application/json"
        }
      }
    }
  ]
}

```

### Создать Позицию 
Запрос на создание новой позиции в Возврате поставщику.
Для успешного создания необходимо в теле запроса указать следующие поля:
+ **assortment** - Ссылка на товар/услугу/серию/модификацию, которую представляет собой позиция.
Также можно указать поле с именем **service**, **consignment**, **variant** в соответствии с тем,
чем является указанная позиция. Подробнее об этом поле можно прочитать в описании [позиции Возврата поставщику](#header-позиции-возврата-поставщику).
+ **quantity** - Количество указанной позиции. Должно быть положительным, иначе возникнет ошибка.
Одновременно можно создать как одну так и несколько позиций Возврата поставщику. Все созданные данным запросом позиции
будут добавлены к уже существующим.
Нельзя создавать позиции, отличные от позиций в документе, по которому создаётся возврат. Допустимо только
отличие в **quantity** позиций (количество в позиции в возврате м.б. меньше или равно количеству в позиции в документе).

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|

> Пример запроса на создание позиций в Возврате поставщику.

```shell
  curl -X POST
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions"
    -H "Authorization: Basic <Access-Token>"
    -H "Content-Type: application/json"
      -d '[
            {
              "quantity": 1,
              "price": 263000,
              "discount": 0,
              "vat": 0,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/20485cfd-2e62-11e6-8a84-bae500000112",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            },
            {
              "quantity": 1,
              "price": 10000,
              "discount": 0,
              "vat": 0,
              "assortment": {
                "meta": {
                  "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0744d71b-2e59-11e6-8a84-bae50000007f",
                  "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
                  "type": "product",
                  "mediaType": "application/json"
                }
              }
            }
          ]
'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление созданных позиций.

```json
[
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/9cfa8b56-41bf-11e6-8a84-bae500000014",
      "type": "purchasereturnposition",
      "mediaType": "application/json"
    },
    "id": "9cfa8b56-41bf-11e6-8a84-bae500000014",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "quantity": 1,
    "price": 263000,
    "discount": 0,
    "vat": 0,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/20485cfd-2e62-11e6-8a84-bae500000112",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json"
      }
    }
  },
  {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/9cfa9b0e-41bf-11e6-8a84-bae500000015",
      "type": "purchasereturnposition",
      "mediaType": "application/json"
    },
    "id": "9cfa9b0e-41bf-11e6-8a84-bae500000015",
    "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
    "quantity": 1,
    "price": 10000,
    "discount": 0,
    "vat": 0,
    "assortment": {
      "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/0744d71b-2e59-11e6-8a84-bae50000007f",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json"
      }
    }
  }
]

```

### Позиция Возврата поставщику
 
### Получить Позицию

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
|positionID|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Возврата поставщику.|
 
> Запрос на получение отдельной позиции Возврата поставщику с указанным id.

```shell
curl -X GET
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление отдельной позиции Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699d288-41bd-11e6-8a84-bae5000000bf",
    "type": "purchasereturnposition",
    "mediaType": "application/json"
  },
  "id": "e699d288-41bd-11e6-8a84-bae5000000bf",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "quantity": 76,
  "price": 35000,
  "discount": 0,
  "vat": 0,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/27eba7b5-3303-11e6-8a84-bae500002b72",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json"
    }
  }
}

```

### Изменить Позицию 
Запрос на обновление отдельной позиции Возврата поставщику.
При обновлении отдельной позиции в возврате можно только изменить количество данной позиции.
Причём это количество должно быть в пределах , где n - кол-во данной позиции в документе, по которому создан возврат.

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
|positionID|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Возврата поставщику.|

> Пример запроса на обновление отдельной позиции в Возврате поставщику.

```shell
  curl -X PUT
    "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
    -H "Authorization: Basic <Access-Token>"
    -H "Content-Type: application/json"
      -d '{
            "quantity": 6754
          }'  
```

> Response 200 (application/json)
Успешный запрос. Результат - JSON представление обновлённой позиции Возврата поставщику.

```json
{
  "meta": {
    "href": "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/e699b298-41bd-11e6-8a84-bae5000000ba/positions/e699d76d-41bd-11e6-8a84-bae5000000c0",
    "type": "purchasereturnposition",
    "mediaType": "application/json"
  },
  "id": "e699d76d-41bd-11e6-8a84-bae5000000c0",
  "accountId": "f976ed28-2e58-11e6-8a84-bae500000001",
  "quantity": 6754,
  "price": 0,
  "discount": 0,
  "vat": 0,
  "assortment": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/product/130a02d7-3303-11e6-8a84-bae500001887",
      "metadataHref": "https://online.moysklad.ru/api/remap/1.2/entity/product/metadata",
      "type": "product",
      "mediaType": "application/json"
    }
  }
}
```

### Удалить позицию

**Параметры**

|Параметр   |Описание   | 
|---|---|
|id |  `string` (required) *Example: 7944ef04-f831-11e5-7a69-971500188b19* id Возврата поставщику.|
|positionID|  `string` (required) *Example: 34f6344f-015e-11e6-9464-e4de0000006c* id позиции Возврата поставщику.|
 
> Запрос на удаление отдельной позиции Возврата поставщику с указанным id.

```shell
curl -X DELETE
  "https://online.moysklad.ru/api/remap/1.2/entity/purchasereturn/7944ef04-f831-11e5-7a69-971500188b19/positions/34f6344f-015e-11e6-9464-e4de0000006c"
  -H "Authorization: Basic <Access-Token>"
```

> Response 200 (application/json)
Успешное удаление позиции Возврата поставщику.
