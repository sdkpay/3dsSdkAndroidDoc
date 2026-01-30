# [ThreedsSdkAndroidDoc](https://sdkpay.github.io/3dsSdkAndroidDoc/)

#### [Сценарии работы с SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario) | [Сущности и классы](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_classes) | [Актуальная версия SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_version)

<br>

# Классы в Threeds SDK

<br>

### Класс Sdk3DS

Входной класс в работу SDK.

Старт работы с SDK происходит через следующий код:

```kotlin
Sdk3DS.getInstance().setupSession(
    context = context
)
```

Старт процесса оплаты вызывается через данный код:

```kotlin
Sdk3DS.getInstance().launchSDK(
    config = ThreedsSdkMerchantOptionsConfig()
)
```

Функция принимает на вход класс ThreedsSdkMerchantOptionsConfig

### Класс ThreedsSdkMerchantOptionsConfig

Класс конфигурации работы SDK.

Принимает в конструктор следующие параметры:

context - базовый класс Context из Android,
scenario - сценарий работы SDK,
callback - лямбда, в которую будет отправляться состояние работы SDK.

### Интерфейс Sdk3dsResult

sealed interface, наследники которого будут отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig.

Актуальные типы наследников:

- SuccessThreedsMethod
- SuccessChallenges
- Error
- Cancel

### Класс SuccessThreedsMethod

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при успешном выполнении пункта 3 [базового сценария](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#базовый-сценарий-для-sdk)

### Класс SuccessChallenges

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при успешном выполнении пункта 5 [базового сценария](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#базовый-сценарий-для-sdk) или пункта 3 [быстрого сценария](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#быстрый-сценарий-для-sdk)

> Важно! Класс содержит 2 параметра: cRes и paRes. Один из них гарантированно будет отдан приложению мерчанта, а другой будет null.

### Класс Error

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при ошибках в работе SDK

### Класс Cancel

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при отмене работы SDK пользователем

### Класс Scenario

sealed class, наследники которого передаются в ThreedsSdkMerchantOptionsConfig, при выборе сценария работы SDK

### Класс ThreedsMethodScenario

Класс наследник Scenario, который выбирается для работы SDK в пункте 3 [базового сценария](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#базовый-сценарий-для-sdk)

### Класс ThreedsChallengesScenario

Класс наследник Scenario, который выбирается для работы SDK в пункте 5 [базового сценария](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#базовый-сценарий-для-sdk) или пункта 3 [быстрого сценария](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#быстрый-сценарий-для-sdk)

Параметры данного класса маппятся из одноимённых сущностей ответа сервера на метод [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder) или [finish3dsMethod.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsMethod)

### Класс PaymentOrderData

Параметр класса ThreedsMethodScenario

Параметры данного класса маппятся из одноимённых сущностей ответа сервера на метод [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder)

### Класс ChallengesData

Параметр класса ThreedsChallengesScenario

Параметры данного класса маппятся из одноимённых сущностей ответа сервера на метод [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder) или [finish3dsMethod.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsMethod)

Пример создания ChallengesData из данных полученных через метод [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder)
```kotlin
ChallangesData(
    termUrl = paymentOrderResponse.termUrl,
    acsUrl = paymentOrderResponse.acsUrl,
    paReq = paymentOrderResponse.paReq,
    cReq = paymentOrderResponse.cReq,
)
```

Пример создания ChallengesData из данных полученных через метод [finish3dsMethod.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsMethod)
```kotlin
ChallangesData(
    termUrl = finish3dsMethodResponse.termUrl,
    acsUrl = finish3dsMethodResponse.acsUrl,
    paReq = finish3dsMethodResponse.paReq,
    cReq = finish3dsMethodResponse.cReq,
)
```

> Важно! Опционально только одно из полей cReq или paReq (т.к. сервер вернёт только одно из них). Параметры termUrl и acsUrl нужно передать по наличию их в ответе сервера.












