# [ThreedsSdkAndroidDoc](https://sdkpay.github.io/3dsSdkAndroidDoc/)

#### [Сценарии работы с SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_scenario) | [Сущности и классы](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_classes) | [Актуальная версия SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_version) | [Различия_версий SDK](https://sdkpay.github.io/3dsSdkAndroidDoc/sdk_differences)

<br>

# Актуальная версия 1.1.0

## Отличия от 1.0.*

1. Добавлен единый сценарий для мерчанта ()
2. Обновлены метрики для анализа ошибок
3. Упрощён ThreedsSdkMerchantOptionsConfig для более лёгкого внедрения в приложение мерчанта
4. Больше нет потребности мерчанту выполнять методы [finish3dsMethod.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsMethod) и [finish3dsPayment.do](https://ecomtest.sberbank.ru/doc#tag/additionalThreeDSServices/operation/finish3dsPayment) (SDK сразу вернёт результат оплаты в callback)



