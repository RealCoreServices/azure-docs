---
title: Form Recognizer insurance card prebuilt model
titleSuffix: Azure Applied AI Services
description: Data extraction and analysis extraction using the insurance card model
author: laujan
manager: nitinme
ms.service: applied-ai-services
ms.subservice: forms-recognizer
ms.topic: conceptual
ms.date: 03/03/2023
ms.author: lajanuar
monikerRange: 'form-recog-3.0.0'
recommendations: false
---

# Azure Form Recognizer health insurance card model (preview)

**This article applies to:** ![Form Recognizer v3.0 checkmark](media/yes-icon.png) **Form Recognizer v3.0**.

> [!IMPORTANT]
>
> * The Form Recognizer Studio health insurance card model is currently in gated preview. Features, approaches and processes may change, prior to General Availability (GA), based on user feedback.
> * Complete and submit the [**Form Recognizer private preview request form**](https://aka.ms/form-recognizer/preview/survey) to request access.

The Form Recognizer health insurance card model combines powerful Optical Character Recognition (OCR) capabilities with deep learning models to analyze and extract key information from US health insurance cards. A health insurance card is a key document for care processing and can be digitally analyzed for patient onboarding, financial coverage information, cashless payments, and insurance claim processing. The health insurance card model analyzes health card images; extracts key information such as insurer, member, prescription, and group number; and returns a structured JSON representation.  Health insurance cards can be presented in various formats and quality including phone-captured images, scanned documents, and digital PDFs.

***Sample health insurance card processed using Form Recognizer Studio***

:::image type="content" source="media/studio/health-insurance-card.png" alt-text="Screenshot of sample health insurance card processed in the Form Recognizer Studio.":::

## Development options

Form Recognizer v3.0 supports the prebuilt health insurance card model with the following tools:

| Feature | Resources | Model ID |
|----------|-------------|-----------|
|**health insurance card model**|<ul><li> [**Form Recognizer Studio**](https://formrecognizer.appliedai.azure.com)</li><li>[**REST API**](https://westus.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-2022-08-31/operations/AnalyzeDocument)</li><li>[**C# SDK**](quickstarts/get-started-sdks-rest-api.md?view=form-recog-3.0.0&preserve-view=true#prebuilt-model)</li><li>[**Python SDK**](quickstarts/get-started-sdks-rest-api.md?view=form-recog-3.0.0&preserve-view=true#prebuilt-model)</li><li>[**Java SDK**](quickstarts/get-started-sdks-rest-api.md?view=form-recog-3.0.0&preserve-view=true#prebuilt-model)</li><li>[**JavaScript SDK**](quickstarts/get-started-sdks-rest-api.md?view=form-recog-3.0.0&preserve-view=true#prebuilt-model)</li></ul>|**prebuilt-healthInsuranceCard.us**|

### Try Form Recognizer

See how data is extracted from health insurance cards using the Form Recognizer Studio. You need the following resources:

* An Azure subscription—you can [create one for free](https://azure.microsoft.com/free/cognitive-services/)

* A [Form Recognizer instance](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesFormRecognizer) in the Azure portal. You can use the free pricing tier (`F0`) to try the service. After your resource deploys, select **Go to resource** to get your key and endpoint.

 :::image type="content" source="media/containers/keys-and-endpoint.png" alt-text="Screenshot of keys and endpoint location in the Azure portal.":::

#### Form Recognizer Studio

> [!NOTE]
> Form Recognizer studio is available with API version v3.0.

1. On the [Form Recognizer Studio home page](https://formrecognizer.appliedai.azure.com/studio), select **Health insurance cards**.

1. You can analyze the sample insurance card document or select the **➕ Add** button to upload your own sample.

1. Select the **Analyze** button:

    :::image type="content" source="media/studio/insurance-card-analyze.png" alt-text="Screenshot: analyze health insurance card window in the Form Recognizer Studio.":::

    > [!div class="nextstepaction"]
    > [Try Form Recognizer Studio](https://formrecognizer.appliedai.azure.com/studio/prebuilt?formType=healthInsuranceCard.us)

## Input requirements

[!INCLUDE [input requirements](./includes/input-requirements.md)]

## Supported languages and locales

| Model | Language—Locale code | Default |
|--------|:----------------------|:---------|
|prebuilt-healthInsuranceCard.us| <ul><li>English (United States)</li></ul>|English (United States)—en-US|

## Field extraction

| Field | Type | Description | Example |
|:------|:-----|:------------|:--------|
|`Insurer`|`string`|Health insurance provider name|PREMERA<br>BLUE CROSS|
|`Member`|`object`|||
|`Member.Name`|`string`|Member name|ANGEL BROWN|
|`Member.BirthDate`|`date`|Member date of birth|01/06/1958|
|`Member.Employer`|`string`|Member name employer|Microsoft|
|`Member.Gender`|`string`|Member gender|M|
|`Member.IdNumberSuffix`|`string`|Identification Number Suffix as it appears on some health insurance cards|01|
|`Dependents`|`array`|Array holding list of dependents, ordered where possible by membership suffix value||
|`Dependents.*`|`object`|||
|`Dependents.*.Name`|`string`|Dependent name|01|
|`IdNumber`|`object`|||
|`IdNumber.Prefix`|`string`|Identification Number Prefix as it appears on some health insurance cards|ABC|
|`IdNumber.Number`|`string`|Identification Number|123456789|
|`GroupNumber`|`string`|Insurance Group Number|1000000|
|`PrescriptionInfo`|`object`|||
|`PrescriptionInfo.Issuer`|`string`|ANSI issuer identification number (IIN)|(80840) 300-11908-77|
|`PrescriptionInfo.RxBIN`|`string`|Prescription issued BIN number|987654|
|`PrescriptionInfo.RxPCN`|`string`|Prescription processor control number|63200305|
|`PrescriptionInfo.RxGrp`|`string`|Prescription group number|BCAAXYZ|
|`PrescriptionInfo.RxId`|`string`|Prescription identification number. If not present, defaults to membership ID number|P97020065|
|`PrescriptionInfo.RxPlan`|`string`|Prescription Plan number|A1|
|`Pbm`|`string`|Pharmacy Benefit Manager for the plan|CVS CAREMARK|
|`EffectiveDate`|`date`|Date from which the plan is effective|08/12/2012|
|`Copays`|`array`|Array holding list of CoPay Benefits||
|`Copays.*`|`object`|||
|`Copays.*.Benefit`|`string`|Co-Pay Benefit name|Deductible|
|`Copays.*.Amount`|`currency`|Co-Pay required amount|$1,500|
|`Payer`|`object`|||
|`Payer.Id`|`string`|Payer ID Number|89063|
|`Payer.Address`|`address`|Payer address|123 Service St., Redmond WA, 98052|
|`Payer.PhoneNumber`|`phoneNumber`|Payer phone number|+1 (987) 213-5674|
|`Plan`|`object`|||
|`Plan.Number`|`string`|Plan number|456|
|`Plan.Name`|`string`|Plan name - If see Medicaid -> then Medicaid|HEALTH SAVINGS PLAN|
|`Plan.Type`|`string`|Plan type|PPO|

### Migration guide and REST API v3.0

* Follow our [**Form Recognizer v3.0 migration guide**](v3-migration-guide.md) to learn how to use the v3.0 version in your applications and workflows.

* Explore our [**REST API**](https://westus.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-2022-08-31/operations/AnalyzeDocument) to learn more about the v3.0 version and new capabilities.

## Next steps

* Try processing your own forms and documents with the [Form Recognizer Studio](https://formrecognizer.appliedai.azure.com/studio)

* Complete a [Form Recognizer quickstart](quickstarts/get-started-sdks-rest-api.md?view=form-recog-3.0.0&preserve-view=true) and get started creating a document processing app in the development language of your choice.
