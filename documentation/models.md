
- [Models](#models)
  - [`VerifyMetaData`](#verifymetadata)
  - [`VerifyMetaData.NextStep`](#verifymetadatanextstep)
  - [`Wallet`](#wallet)
  - [`MercuryoUser`](#mercuryouser)
  - [`SanctionStatusType`](#sanctionstatustype)
  - [`VerificationStatusType`](#verificationstatustype)
  - [`DocumentDetails`](#documentdetails)
    - [`DocumentDetails.Error`](#documentdetailserror)
  - [`Card`](#card)
  - [`Bank`](#bank)
    - [`Bank.Color`](#bankcolor)
  - [`ConverterResult`](#converterresult)
  - [`Rate`](#rate)
  - [`TransactionStatus`](#transactionstatus)
  - [`Redirect`](#redirect)
    - [`Redirect.FormItem`](#redirectformitem)
  - [`TransactionType`](#transactiontype)
  - [`EstimateWithdrawFee`](#estimatewithdrawfee)
  - [`Fee`](#fee)
  - [`EstimatedTime`](#estimatedtime)
  - [`Limit`](#limit)
  - [`LimitPair`](#limitpair)

# Models

## `VerifyMetaData`

Модель содержит информацию о следующем шаге для подтверждения действий.


| Название   | Тип                     | Описание                                                |
| ---------- | ----------------------- | ------------------------------------------------------- |
| key        | String                  | Публичный ключ для верификации                          |
| codeLength | Int                     | Длина кода                                              |
| step       | [`NextStep`](#nextstep) | Модель указывающая тип верификации                      |
| timeout    | Int                     | Период между запроса нового кода подтверждения          |
| recipient  | String?                 | Получатель куда было отправлен код подтверждения        |


## `VerifyMetaData.NextStep` 

Модель, указывающая на следующий шаг сценария.


| Тип               | Описание                              |
| ----------------- | ------------------------------------- |
| PHONE             | Верификация по смс                    |
| EMAIL             | Код отправлен на электронную почту    |
| SET_PASSWORD      | Необходимо ввести номер пароль        |
| SET_EMAIL         | Необходимо ввести электронную почту   |
| SET_PERSONAL_DATA | Необходимо ввести персональные данные |


## `Wallet`

Модель, содержащая информацию о балансе кошелька

| Название     | Тип    | Описание                       |
| ------------ | ------ | ------------------------------ |
| currency     | String | Название криптовалюты кошелька |
| balance      | Double | Баланс кошелька в криптовалюте |
| fiatCurrency | String | Название фиатной валюты        |
| fiatBalance  | Double | Баланс кошелька в фиате        |

## `MercuryoUser`

Модель содержащая информацию пользователя.

| Название           | Тип                                                 | Описание                                                              |
| ------------------ | --------------------------------------------------- | --------------------------------------------------------------------- |
| uuid               | String                                              | Уникальный ключ пользователя                                          |
| firstName          | String                                              | Имя пользователя                                                      |
| lastName           | String                                              | Фамилия пользователя                                                  |
| fullName           | String                                              | Полное имя пользователя                                               |
| birthday           | String                                              | Дата рождения пользователя, формат dd-MM-yyyy                         |
| email              | String                                              | Электронная почта пользователя                                        |
| referral           | String                                              | Реферальный код пользователя                                          |
| countryCode        | String                                              | Код страны пользователя                                               |
| phone              | String                                              | Номер телефона пользователя                                           |
| sendPromo          | Boolean                                             | Согласие на получения информации об акциях                            |
| fiatCurrency       | String                                              | Валюта пользователя                                                   |
| sanctionStatus     | [`SanctionStatusType`](#sanctionstatustype)         | Статус пользователя в системе                                         |
| verificationStatus | [`VerificationStatusType`](#verificationstatustype) | Статус идентификации пользователя                                     |
| documentDetails    | [`DocumentDetails`](#documentdetails)               | Информация о предоставленных документах для идентификации пользователя |

## `SanctionStatusType`

Модель указывает на санкицонный статус. Возможные варианты `INCOMPLETE`, `UNDER_REVIEW`, `COMPLETED`, `FAILED`.

## `VerificationStatusType`

Модель указывает на статус идентификации личности. Возможные варианты `INCOMPLETE`, `UNDER_REVIEW`, `COMPLETED`, `FAILED`.

## `DocumentDetails`

Модель содержит информацию о проблемах предоставленных документов. 
| Название    | Тип                                      | Описание                                   |
| ----------- | ---------------------------------------- | ------------------------------------------ |
| checkEnable | Boolean                                  | Возможность проходить верификацию          |
| errors      | List\<[`Error`](#documentdetails.error)> | Список ошибок при верификации пользователя |
### `DocumentDetails.Error`

| Название     | Тип    | Описание           |
| ------------ | ------ | ------------------ |
| documentType | String | Документ с ошибкой |
| message      | String | Описание ошибки    |
 
## `Card`

Модель содержит информацию о карте.

| Название        | Тип             | Описание                             |
| --------------- | --------------- | ------------------------------------ |
| id              | String          | Уникальный ключ карты                |
| createdAt       | Long            | Время добавления карты               |
| paymentSystem   | String          | Информации о платежной системе карты |
| number          | String          | Последние четыре цифры номера карты  |
| expirationMonth | String          | Месяц окончания действия карты       |
| expirationYear  | String          | Год окончания действия карты         |
| bank            | [`Bank`](#bank) | Информация о банке                   |

## `Bank`

Модель содержит информацию о банке карты.

| Название | Тип                   | Описание           |
| -------- | --------------------- | ------------------ |
| title    | String,               | Название банка     |
| icon     | String,               | Url логотипа банка |
| color    | [`Color`](#bankcolor) |

### `Bank.Color`

| Название   | Тип    | Описание                         |
| ---------- | ------ | -------------------------------- |
| background | String | Цвет заднего фона карточки банка |
| foreground | String | Цвет информации о карте          |

## `ConverterResult`

Модель содержит токен для совершение покупки, продажи и дополнительную информацию о состоянии конвертора.

| Название     | Тип    | Описание                                                                                         |
| ------------ | ------ | ------------------------------------------------------------------------------------------------ |
| token        | String | Ключ для пары значений конвертора, необходимый для совершения транзакции с заданными параметрами |
| currency     | String | Криптовалюта                                                                                     |
| amount       | String | Сумма криптовалюты                                                                               |
| fiatCurrency | String | Фиатная валюта                                                                                   |
| fiatAmount   | String | Сумма для фиатной валюты                                                                         |

## `Rate`

Модель содержит информацию о курсе выбраной валюты.

| Название | Тип    | Описание                                         |
| -------- | ------ | ------------------------------------------------ |
| from     | String | Валюта относительно который был сформирован курс |
| to       | String | Валюта в которую был сформирован курс            |
| type     | String | Тип операции `buy`, `sell`                       |
| rate     | String | Курс для валюты `to`                             |

## `TransactionStatus`

Модель содержит информацию о транзакции, такие как идентификатор и статус. Возможны промежуточные состояния статуса с одним из опциональных полей, например для покупки может придти [`Redirect`](#redirect) указывающий на необходимость пройти 3ds, или `isVerifyDescription` указывающий о необходимости ввода дескриптора, для завершения транзакции.


| Название            | Тип                      | Описание                                                                 |
| ------------------- | ------------------------ | ------------------------------------------------------------------------ |
| redirect            | [`Redirect?`](#redirect) | Информацию о формирование Url для подтверждения транзакции               |
| id                  | String                   | Идентификатор транзакции в системе Меркурио                              |
| status              | String                   | Статус транзакции                                                        |
| isVerifyDescription | Boolean                  | Флаг указывающий на необходимость подтвердить дескриптор следующим шагом |

## `Redirect`

Модель указывает на необходимость перехода по URL указанном в объекте

| Название    | Тип             | Описание                                              |
| ----------- | --------------- | ----------------------------------------------------- |
| form        | List\<FormItem> | Список дополнительной информации для формирования URL |
| requestType | String          | Тип запроса `GET`, `POST`                             |
| uriTemplate | String          | Адрес                                                 |

### `Redirect.FormItem`

Модель содержит дополнительную информацию для формирования адреса 

| Название | Тип    | Описание            |
| -------- | ------ | ------------------- |
| key      | String | Ключ                |
| template | String | Информация по ключу |

## `TransactionType`
 | Тип      | Описание                                    |
 | -------- | ------------------------------------------- |
 | DEPOSIT  | Транзакции поплнения с другого кошелька     |
 | BUY      | Покупка припты через карту                  |
 | SELL     | Продажа крипты через карту                  |
 | WITHDRAW | Перевод крипты на другой кошелек            |
 | REFERRAL | Пополнение кошелька по реферальной програме |

## `EstimateWithdrawFee`

Модель содержит список доступных комиссий.

| Название       | Тип                 | Описание                  |
| -------------- | ------------------- | ------------------------- |
| cryptoCurrency | String              | Название криптовалюты     |
| fiatCurrency   | String              | Название фиатной валюты   |
| fees           | List<[`Fee`](#fee)> | Список доступных комиссий |

## `Fee`

Модель содержит информацию о комиссии.

| Название      | Тип           | Описание                                                     |
| ------------- | ------------- | ------------------------------------------------------------ |
| id            | String        | Идентификатор комиссии                                       |
| level         | String        | Скорость транзакции, возможные типы `slow`, `medium`, `fast` |
| fee           | String        | Комиссия в криптоввалюте                                     |
| fiatAmount    | String        | Комиссия в фиате                                             |
| isPaidByUser  | Boolean       | Указывает будет ли комиссия снята с пользователя             |
| estimatedTime | EstimatedTime | Ориентировачное время выполнения транзакции                  |

## `EstimatedTime`

Модель содержит информацию о времени совершения транзакции.


| Название | Тип  | Описание                    |
| -------- | ---- | --------------------------- |
| max      | Int? | Максимальное время перевода |
| min      | Int? | Минимальное время перевода  |

## `Limit`

 Модель содержит информацию о лимитах для транзакции.

| Название       | Тип    | Описание                                                     |
| -------------- | ------ | ------------------------------------------------------------ |
| initDay        | Double | Дневной лимит 
| day            | Double | Остатки по дневному лимиту
| initWeek       | Double | Недельный лимит пользователя                                 |
| week           | Double | Остатки по недельному лимиту                                 |
| initMonth      | Double | Месячный лимит пользователя                                  |
| month          | Double | Остатки по месячному лимиту                                  |
| operationMin   | Double | Минимальная сумма транзакции без учёта баланса пользователя  |
| operationMax   | Double | Максимальная сумма транзакции без учёта баланса пользователя |

## `LimitPair`

Модель содержит пару лимитов для крипто и фиатной валют.


| Название    | Тип               | Описание                 |
| ----------- | ----------------- | ------------------------ |
| fiatLimit   | [`Limit`](#limit) | Лимит для фиатной валюты |
| cryptoLimit | [`Limit`](#limit) | Лимит для криптовалюты   |