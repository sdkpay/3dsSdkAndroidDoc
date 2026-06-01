# [ThreedsSdkAndroidDoc](https://sdkpay.github.io/3dsSdkAndroidDoc/)

#### [Сценарии работы с SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario) | [Сущности и классы](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_classes) | [Актуальная версия SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_version) | [Различия_версий SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_differences)

<br>

# Классы в Threeds SDK

<br>

### Класс Sdk3DS

Входной класс в работу SDK.

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

- context (context из приложения мерчанта)
- orderId (orderId из метода [register.do](https://ecomtest.sberbank.ru/doc#tag/basicServices/operation/register))
- formUrl (formUrl из метода [paymentOrder.do](https://ecomtest.sberbank.ru/doc#tag/paymentServices/operation/paymentOrder))
- callback (лямбда, в которую будет отправляться состояние работы SDK)

### Интерфейс Sdk3dsResult

sealed interface, наследники которого будут отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig.

Актуальные типы наследников:

- ThreedsStarted
- SuccessThreedsPayment
- SdkError
- InvalidInitSdkError
- Cancel

### Класс ThreedsStarted

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при успешном cтарте 3DS SDK

### Класс SuccessThreedsPayment

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при успешном выполнении пункта 3 [базового сценария](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario#базовый-сценарий-для-sdk)

### Класс SdkError

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при ошибках в работе SDK

### Класс InvalidInitSdkError

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при неправильном заполнении полей ThreedsSdkMerchantOptionsConfig

### Класс Cancel

Класс, экземпляр которого будет отправляться в лямбду класса ThreedsSdkMerchantOptionsConfig при отмене работы SDK пользователем
