# [ThreedsSdkAndroidDoc](https://sdkpay.github.io/3dsSdkAndroidDoc/)

#### [Сценарии работы с SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario) | [Сущности и классы](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_classes) | [Актуальная версия SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_version)

<br>

# Сценарии работы SDK

#### [Базовый сценарий](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#Базовый-сценарий)
#### [Быстрый сценарий](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#Быстрый-сценарий)

<br>

## Базовый сценарий

Включает в себя следующий флоу из методов:

1. [register.do](https://ecomtest.sberbank.ru/doc#tag/basicServices/operation/register) - Запрос предназначен для регистрации (создания) заказа в Шлюзе. При успешной обработке запроса заказу присваивается номер (идентификатор), уникальный в рамках Шлюза. Метод используется для регистрации заказа с последующией оплатой любым способом.
2. [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder) - Запрос предназначен для блокировки средств на карте Плательщика для проведения дальнейших расчетов между банками-участниками.
3. Работа 3DS SDK со сценарием [ThreedsMethodScenario](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_classes#Класс_ThreedsMethodScenario) - Запускается SDK. Приложение мерчанта ожидает успех/ошибку аутентификации плательщика.
4. [finish3dsMethod.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsMethod) - Запрос предназначен для завершения 3DS аутентификации Плательщика при проведении операции оплаты.
5. Работа 3DS SDK со сценарием [ThreedsChallengesScenario](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_classes#Класс_ThreedsChallengesScenario) - Запускается SDK. Пользователь проходит челленджи, мерчант ожидает успех/ошибку.
6. [finish3dsPayment.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsPayment) - Запрос предназначен для передачи результата 3DS аутентификации Плательщиа при прямом взаимодействии с сервером ACS.

##### Подробнее о пункте 3.

Вызываем Sdk3DS, стартуем launchSDK и передаём в config ThreedsSdkMerchantOptionsConfig, который принимает
context, ThreedsMethodScenario и ждём в лямбде параметр ответа SuccessThreedsMethod.

```kotlin
Sdk3DS.getInstance().launchSDK(
    config = ThreedsSdkMerchantOptionsConfig(
        context,
        Sdk3DS.Scenario.ThreedsMethodScenario(paymentOrderData)
    ) { result ->
        if (result is ThreedsSdkMerchantOptionsConfig.Sdk3dsResult.SuccessThreedsMethod) {
            // do gw/partner/api/v1/finish3dsMethod.do
        }
    }
)
```

> paymentOrderData - экземпляр класса с одноимёнными параметрами из ответа метода [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder) из пункта 2.

##### Подробнее о пункте 5.

Вызываем Sdk3DS, стартуем launchSDK и передаём в config ThreedsSdkMerchantOptionsConfig, который принимает
context, ThreedsChallengesScenario и ждём в лямбде параметр ответа SuccessChallenges.

```kotlin
Sdk3DS.getInstance().launchSDK(
    config = ThreedsSdkMerchantOptionsConfig(
        context,
        Sdk3DS.Scenario.ThreedsChallengesScenario(challengesData)
    ) { result ->
        if (result is ThreedsSdkMerchantOptionsConfig.Sdk3dsResult.SuccessChallenges) {
            // do gw/partner/api/v1/finish3dsPayment.do
        }
    }
)
```

> challengesData - экземпляр класса получить параметры которого можно из [finish3dsMethod.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsMethod)


## Быстрый сценарий

Включает в себя следующий флоу из методов:

1. [register.do](https://ecomtest.sberbank.ru/doc#tag/basicServices/operation/register) - Запрос предназначен для регистрации (создания) заказа в Шлюзе. При успешной обработке запроса заказу присваивается номер (идентификатор), уникальный в рамках Шлюза. Метод используется для регистрации заказа с последующией оплатой любым способом.
2. [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder) - Запрос предназначен для блокировки средств на карте Плательщика для проведения дальнейших расчетов между банками-участниками.
3. Работа 3DS SDK со сценарием [ThreedsChallengesScenario](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_classes#Класс_ThreedsChallengesScenario) - Запускается SDK. Пользователь проходит челленджи, мерчант ожидает успех/ошибку.
4. [finish3dsPayment.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsPayment) - Запрос предназначен для передачи результата 3DS аутентификации Плательщиа при прямом взаимодействии с сервером ACS.

##### Подробнее о пункте 3.

Вызываем Sdk3DS, стартуем launchSDK и передаём в config ThreedsSdkMerchantOptionsConfig, который принимает
context, ThreedsChallengesScenario и ждём в лямбде параметр ответа SuccessChallenges.

```kotlin
Sdk3DS.getInstance().launchSDK(
    config = ThreedsSdkMerchantOptionsConfig(
        context,
        Sdk3DS.Scenario.ThreedsChallengesScenario(challengesData)
    ) { result ->
        if (result is ThreedsSdkMerchantOptionsConfig.Sdk3dsResult.SuccessChallenges) {
            // do gw/partner/api/v1/finish3dsPayment.do
        }
    }
)
```

> challengesData - экземпляр класса получить параметры которого можно из [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder)

## В чём разница сценариев?

Если метод [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder) вернул cReq или paReq, то выбираем второй сценарий. 
В противном случае cReq или paReq мы получаем из метода [finish3dsMethod.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsMethod) первого сценария.
