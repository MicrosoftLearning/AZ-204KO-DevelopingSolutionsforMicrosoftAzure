---
lab:
    az204Title: '랩 02: Azure Functions를 사용하여 작업 처리 논리 구현'
    az020Title: '랩 02: Azure Functions를 사용하여 작업 처리 논리 구현'
    az204Module: '모듈 02: Azure Functions 구현'
    az020Module: '모듈 02: Azure Functions 구현'
    type: '해답'
---

# 랩 02: Azure Functions를 사용하여 작업 처리 논리 구현
# 학생 랩 답변 키

## Microsoft Azure 사용자 인터페이스

Microsoft 클라우드 도구의 동적 특성을 감안할 때 이 교육 콘텐츠를 개발한 후 Azure 사용자 인터페이스(UI) 변경 사항이 발생할 수 있습니다. 이러한 변경으로 인해 랩 지침 및 랩 단계가 일치하지 않을 수 있습니다.

Microsoft는 커뮤니티가 필요한 변경 사항을 제공하면 이 교육 과정을 업데이트합니다. 그러나 클라우드 업데이트가 자주 발생하기 때문에 이 교육 콘텐츠가 업데이트되기 전에 UI가 먼저 변경될 수 있습니다. **이 경우 변경 사항에 적응하고 필요에 따라 랩에서 작업합니다.**

## 지침

### 시작하기 전 확인 사항

#### 랩 가상 머신에 로그인

다음 자격 증명을 사용하여 Windows 10 VM(가상 머신)에 로그인합니다.

- 사용자 이름: **Admin**
- 암호: **Pa55w.rd**

> **참고**: 강사가 가상 랩 환경 연결에 대한 지침을 제공합니다.

#### 설치된 애플리케이션 검토

Windows 10 데스크톱에서 작업 표시줄을 찾습니다. 작업 표시줄에는 이 랩에서 사용할 애플리케이션에 대한 아이콘이 포함되어 있습니다.

- Microsoft Edge
- 파일 탐색기
- Windows Terminal
- Visual Studio Code

### 연습 1: Azure 리소스 만들기

#### 작업 1: Azure Portal 열기

1. 작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.
1. 열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.
1. Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.
1. Microsoft 계정의 암호를 입력한 다음 로그인을 선택합니다.
    > **참고**: Azure Portal에 처음 로그인하는 경우 포털 둘러보기가 제공됩니다. 둘러보기를 건너뛰고 Portal 사용을 시작하려면 **시작하기**를 선택합니다.

#### 작업 2: Azure Storage 계정 만들기

1. Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.
1. **모든 서비스** 블레이드에서 **스토리지 계정**을 선택합니다.
1. **스토리지 계정** 블레이드에서 스토리지 계정 인스턴스 목록을 가져옵니다.
1. **스토리지 계정** 블레이드에서 **새로 만들기**를 선택합니다.
1. **스토리지 계정 만들기** 블레이드에서 **기본**, **태그**, **검토 + 만들기** 등의 블레이드 탭을 살펴봅니다.
    > **참고**: 각 탭은 새 스토리지 계정을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.
1. **기본** 탭을 선택하고 탭 영역 내에서 다음 작업을 수행합니다.
    1. **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **리소스 그룹** 섹션에서 **새로 만들기**를 선택하고 **Serverless**를 입력한 다음 **확인**을 선택합니다.
    1. **스토리지 계정 이름** 텍스트 상자에 **funcstor[사용자 이름]** 을 입력합니다.
    1. **위치** 목록에서 **(미국) 미국 동부** 지역을 선택합니다.
    1. **성능** 섹션에서 **표준**을 선택합니다.
    1. **계정 종류** 목록에서 **StorageV2(범용 v2)** 를 선택합니다.
    1. **복제** 목록에서 **LRS(로컬 중복 스토리지)** 를 선택합니다.
    1. **검토 + 만들기**를 선택합니다.
1. **검토+ 만들기** 탭에서 이전 단계에서 지정한 옵션을 검토합니다.
1. 지정된 구성을 사용하여 스토리지 계정을 만들려면 **만들기**를 선택합니다.
    > **참고**: 배포 블레이드에서 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.
1. Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.
1. **모든 서비스** 블레이드에서 **스토리지 계정**을 선택합니다.
1. **스토리지 계정** 블레이드에서 **funcstor[사용자 이름]** 스토리지 계정 인스턴스를 선택합니다.
1. **스토리지 계정** 블레이드에서 **설정** 섹션을 찾은 다음 **액세스 키**를 선택합니다.
1. **액세스 키** 블레이드에서 키 중 하나를 선택하고 **연결 문자열** 상자 중 하나의 값을 기록합니다.
    > **참고**: 이 값은 랩에서 나중에 사용합니다. 어떤 연결 문자열을 선택하든 상관없습니다. 서로 교환할 수 있습니다.

#### 작업 3: 함수 앱 만들기

1. Azure Portal의 탐색 창에서 **리소스 만들기** 링크를 선택합니다.
1. **새로 만들기** 블레이드에서 **Marketplace 검색** 텍스트 상자를 찾습니다.
1. 검색 상자에 **함수**를 입력하고 Enter 키를 누릅니다.
1. **모든 항목** 검색 결과 블레이드에서 **함수 앱** 결과를 선택합니다.
1. **함수 앱** 블레이드에서 **만들기**를 선택합니다.
1. **함수 앱** 블레이드에서 **기본** 등의 탭을 찾습니다.
    > **참고**: 각 탭은 새 함수 앱을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.
1. **기본** 탭에서 다음 작업을 수행합니다.
    1. **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **리소스 그룹** 섹션에서 **기존 항목 사용**을 선택한 다음 목록에서 **Serverless**를 선택합니다.
    1. **함수 앱 이름** 텍스트 상자에 **funclogic[사용자 이름]** 을 입력합니다.
    1. **게시** 섹션에서 **코드**를 선택합니다.
    1. **런타임 스택** 드롭다운 목록에서 **.NET**을 선택합니다.
    1. **버전** 드롭다운 목록에서 **3.1**을 선택합니다.
    1. **지역** 드롭다운 목록에서 **미국 동부** 지역을 선택합니다.
    1. **다음: 호스팅**을 선택합니다.
1. **호스팅** 탭에서 다음 작업을 수행합니다.
    1. **운영 체제** 섹션에서 **Linux**를 선택합니다.
    1. **스토리지 계정** 드롭다운 목록에서 이 랩의 앞부분에서 만든 **funcstor[사용자 이름]** 스토리지 계정을 선택합니다.
    1. **플랜 유형** 드롭다운 목록에서 **사용** 옵션을 선택합니다.
    1. **검토 + 만들기**를 선택합니다.
1. **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.
1. 지정된 구성을 사용하여 함수 앱을 만들려면 **만들기**를 선택합니다.
    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

> **복습**: 이 연습에서는 이 랩에 사용할 모든 리소스를 만들었습니다.

### 연습 2: 로컬 Azure Functions 프로젝트 구성

#### 작업 1: 함수 프로젝트 초기화

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 누릅니다. 이 명령은 **Azure Functions Core Tools**를 사용하여 **dotnet** 런타임을 통해 현재 디렉터리에 새 로컬 Azure Functions 프로젝트를 만듭니다.

    ```powershell
    func init --worker-runtime dotnet --force
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [새 프로젝트 만들기][azure-functions-core-tools-new-project] 방법을 파악할 수 있습니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

#### 작업 2: 연결 문자열 구성

1. **시작** 화면에서 **Visual Studio Code** 타일을 선택합니다.
1. **파일** 메뉴에서 **폴더 열기**를 선택합니다.
1. 열리는 **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 이동한 후 **폴더 선택**을 선택합니다.
1. **Visual Studio Code** 창의 탐색기 창에서 **local.settings.json** 파일을 엽니다.
1. **AzureWebJobsStorage** 설정의 현재 값을 살펴봅니다.

    ```json
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    ```

1. **AzureWebJobsStorage**의 값을 이 랩의 앞부분에서 기록한 스토리지 계정의 **연결 문자열**로 설정하여 업데이트합니다.

#### 작업 3: 프로젝트 빌드 및 유효성 검사

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 .NET Core 3.1 프로젝트를 **빌드**합니다.

    ```powershell
    dotnet build
    ```

> **복습**: 이 연습에서는 Azure Functions 개발에 사용할 로컬 프로젝트를 만들었습니다.

### 연습 3: HTTP 요청에 의해 트리거되는 함수 만들기

#### 작업 1: HTTP 트리거 함수 만들기

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 누릅니다. 이 명령은 **Azure Functions Core Tools**를 사용하여 **HTTP 트리거** 템플릿을 통해 새 함수 **Echo**를 만듭니다.

    ```powershell
    func new --template "HTTP trigger" --name "Echo"
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [새 함수 만들기][azure-functions-core-tools-new-function] 방법을 파악할 수 있습니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

#### 작업 2: HTTP 트리거 함수 코드 작성

1. **시작** 화면에서 **Visual Studio Code** 타일을 선택합니다.
1. **파일** 메뉴에서 **폴더 열기**를 선택합니다.
1. 열리는 파일 탐색기 창에서 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 이동한 후 **폴더 선택**을 선택합니다.
1. **Visual Studio Code** 창의 탐색기 창에서 **Echo.cs** 파일을 엽니다.
1. 코드 편집기에서 예제 구현을 살펴봅니다.

    ```csharp
    using System;
    using System.IO;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Extensions.Http;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;
    using Newtonsoft.Json;

    namespace func
    {
        public static class Echo
        {
            [FunctionName("Echo")]
            public static async Task<IActionResult> Run(
                [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
                ILogger log)
            {
                log.LogInformation("C# HTTP trigger function processed a request.");

                string name = req.Query["name"];

                string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
                dynamic data = JsonConvert.DeserializeObject(requestBody);
                name = name ?? data?.name;

                string responseMessage = string.IsNullOrEmpty(name)
                    ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                    : $"Hello, {name}. This HTTP triggered function executed successfully.";

                return new OkObjectResult(responseMessage);
            }
        }
    }
    ```

1. **Echo.cs** 파일 내의 모든 내용을 삭제합니다.
1. 다음 코드 줄을 추가하여 **Microsoft.AspNetCore.Mvc**, **Microsoft.Azure.WebJobs**, **Microsoft.AspNetCore.Http** 및 **Microsoft.Extensions.Logging** 네임스페이스에 **using 지시문**을 추가합니다.

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;
    ```

1. 새 **public static** 클래스 **Echo**를 만듭니다.

    ```csharp
    public static class Echo
    { }
    ```

1. **Echo.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;

    public static class Echo
    { }
    ```

1. **Echo** 클래스 내에서 다음 코드 블록을 추가하여 새 **public static** 메서드 **Run**을 만듭니다. 이 메서드는 **IActionResult** 유형 변수를 반환하며, **HttpRequest** 및 **ILogger** 유형 변수를 **request** 및 **logger** 매개 변수로 가져옵니다.

    ```csharp
    public static IActionResult Run(
        HttpRequest request,
        ILogger logger)
    { }
    ```

1. 다음 코드를 추가하여 **name** 매개 변수가 **Echo** 값으로 설정된 **FunctionNameAttribute** 유형 특성을 **Run** 메서드에 추가합니다.

    ```csharp
    [FunctionName("Echo")]
    public static IActionResult Run(
        HttpRequest request,
        ILogger logger)
    { }
    ```

1. 다음 코드를 추가하여 **methods** 매개 변수 배열이 단일 값 **POST**로 설정된 **HttpTriggerAttribute** 유형 특성을 **request** 매개 변수에 추가합니다.

    ```csharp
    [FunctionName("Echo")]
    public static IActionResult Run(
        [HttpTrigger("POST")] HttpRequest request,
        ILogger logger)
    { }
    ```

1. **Echo.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;

    public static class Echo
    {
        [FunctionName("Echo")]
        public static IActionResult Run(
            [HttpTrigger("POST")] HttpRequest request,
            ILogger logger)
        { }
    }
    ```

1. **Run** 메서드에서 다음 코드 줄을 입력하여 고정 메시지를 로깅합니다.

    ```csharp
    logger.LogInformation("Received a request");
    ```

1. HTTP 요청의 본문을 HTTP 응답으로 에코하는 다음 코드 줄을 입력합니다.

    ```csharp
    return new OkObjectResult(request.Body);
    ```

1. **Echo.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;

    public static class Echo
    {
        [FunctionName("Echo")]
        public static IActionResult Run(
            [HttpTrigger("POST")] HttpRequest request,
            ILogger logger)
        {
            logger.LogInformation("Received a request");
            return new OkObjectResult(request.Body);
        }
    }
    ```

1. **저장**을 선택하여 **Echo.cs** 파일의 변경 내용을 저장합니다.

#### 작업 3: httprepl을 사용하여 HTTP 트리거 함수 테스트

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 함수 앱 프로젝트를 실행합니다.

    ```powershell
    func start --build
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [로컬에서 함수 앱 프로젝트 시작][azure-functions-core-tools-start-function] 방법을 파악할 수 있습니다.
1. 작업 표시줄에서 **Windows 터미널** 아이콘을 다시 선택하여 **Windows 터미널** 애플리케이션의 새 인스턴스를 엽니다.
1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 **httprepl** 도구를 시작합니다. 기본 URI(Uniform Resource Identifier)는 ``http://localhost:7071``로 설정합니다.

    ```powershell
    httprepl http://localhost:7071
    ```

    > **참고**: httprepl 도구에서 오류 메시지가 표시됩니다. 이 메시지는 도구가 API를 "통과"하는 데 사용할 Swagger 정의 파일을 검색하기 때문에 발생합니다. 함수 프로젝트는 Swagger 정의 파일을 생성하지 않으므로 API를 수동으로 통과해야 합니다.
1. 도구 프롬프트가 표시되면 다음 명령을 입력하고 Enter 키를 눌러 상대 **api** 디렉터리를 찾습니다.

    ```powershell
    cd api
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 상대 **echo** 디렉터리를 찾습니다.

    ```powershell
    cd echo
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 **\-\-content** 옵션을 사용하여 HTTP 요청 본문을 전송하는 **post** 명령을 실행합니다. 요청 본문은 숫자 값 **3**으로 설정되어 있습니다.

    ```powershell
    post --content 3
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 **\-\-content** 옵션을 사용하여 HTTP 요청 본문을 전송하는 **post** 명령을 실행합니다. 요청 본문은 숫자 값 **5**로 설정되어 있습니다.

    ```powershell
    post --content 5
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 **\-\-content** 옵션을 사용하여 HTTP 요청 본문을 전송하는 **post** 명령을 실행합니다. 요청 본문은 문자열 값 **Hello**로 설정되어 있습니다.

    ```powershell
    post --content "Hello"
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 **\-\-content** 옵션을 사용하여 HTTP 요청 본문을 전송하는 **post** 명령을 실행합니다. 요청 본문은 JSON(JavaScript Object Notation) 값 **{"msg": "Successful"}** 로 설정되어 있습니다.

    ```powershell
    post --content "{"msg": "Successful"}"
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 **httprepl** 애플리케이션을 종료합니다.

    ```powershell
    exit
    ```

1. 현재 실행 중인 **Windows 터미널** 애플리케이션의 모든 인스턴스를 닫습니다.

> **복습**: 이 연습에서는 HTTP POST 요청을 통해 전송된 콘텐츠를 에코하는 기본 함수를 만들었습니다.

### 연습 4: 일정에 따라 트리거하는 함수 만들기

#### 작업 1: 일정에 따라 트리거되는 함수 만들기

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 누릅니다. 이 명령은 **Azure Functions Core Tools**를 사용하여 **타이머 트리거** 템플릿을 통해 새 함수 **Recurring**을 만듭니다.

    ```powershell
    func new --template "Timer trigger" --name "Recurring"
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [새 함수 만들기][azure-functions-core-tools-new-function] 방법을 파악할 수 있습니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

#### 작업 2: 함수 코드 관찰

1. **시작** 화면에서 **Visual Studio Code** 타일을 선택합니다.
1. **파일** 메뉴에서 **폴더 열기**를 선택합니다.
1. 열리는 **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 이동한 후 **폴더 선택**을 선택합니다.
1. **Visual Studio Code** 창의 탐색기 창에서 **Recurring.cs** 파일을 엽니다.
1. 코드 편집기에서 코드의 구현을 살펴봅니다.

    ```csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    using Microsoft.Extensions.Logging;

    namespace func
    {
        public static class Recurring
        {
            [FunctionName("Recurring")]
            public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, ILogger log)
            {
                log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
            }
        }
    }
    ```

#### 작업 3: 함수 실행 관찰

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 함수 앱 프로젝트를 실행합니다.

    ```powershell
    func start --build
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [로컬에서 함수 앱 프로젝트 시작][azure-functions-core-tools-start-function] 방법을 파악할 수 있습니다.
1. 5분마다 발생하는 함수 실행을 관찰합니다. 각 함수 실행은 로그에 간단한 메시지를 렌더링해야 합니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

#### 작업 4: 함수 통합 구성 업데이트

1. **시작** 화면에서 **Visual Studio Code** 타일을 선택합니다.
1. **파일** 메뉴에서 **폴더 열기**를 선택합니다.
1. 열리는 파일 탐색기 창에서 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 이동한 후 **폴더 선택**을 선택합니다.
1. **Visual Studio Code** 창의 탐색기 창에서 **Recurring.cs** 파일을 엽니다.
1. 코드 편집기에서 기존 **Run** 메서드 서명을 살펴봅니다.

    ```csharp
    [FunctionName("Recurring")]
    public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, ILogger log)
    ```

1. **Run** 메서드 서명 코드 블록을 업데이트하여 **30초**마다 실행되도록 일정을 변경합니다.

    ```csharp
    [FunctionName("Recurring")]
    public static void Run([TimerTrigger("*/30 * * * * *")]TimerInfo myTimer, ILogger log)
    ```

1. **저장**을 선택하여 **Recurring.cs** 파일의 변경 내용을 저장합니다.

#### 작업 5: 함수 실행 관찰

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 함수 앱 프로젝트를 실행합니다.

    ```powershell
    func start --build
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [로컬에서 함수 앱 프로젝트 시작][azure-functions-core-tools-start-function] 방법을 파악할 수 있습니다.
1. 약 30초마다 발생하는 함수 실행을 관찰합니다. 각 함수 실행은 로그에 간단한 메시지를 렌더링해야 합니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

> **복습**: 이 연습에서는 고정된 일정에 따라 자동으로 실행되는 함수를 만들었습니다.

### 연습 5: 다른 서비스와 통합되는 함수 만들기

#### 작업 1: Azure Blob Storage에 샘플 콘텐츠 업로드

1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **Serverless** 리소스 그룹을 찾아 선택합니다.
1. **Serverless** 블레이드에서 이 랩의 앞부분에서 만든 **funcstor[사용자 이름]** 스토리지 계정을 선택합니다.
1. **스토리지 계정** 블레이드에서 **Blob service** 섹션에 있는 **컨테이너** 링크를 선택합니다.
1. **컨테이너** 섹션에서 **+ 컨테이너**를 선택합니다.
1. **새 컨테이너** 팝업 창에서 다음 작업을 수행합니다.
    1. **이름** 텍스트 상자에 **content**를 입력합니다.
    1. **공용 액세스 수준** 드롭다운 목록에서 **비공개(익명 액세스 없음)** 를 선택합니다.
    1. **확인**을 선택합니다.
1. **컨테이너** 섹션으로 돌아가서 최근에 만든 **content** 컨테이너를 선택합니다.
1. **컨테이너** 블레이드에서 **업로드**를 선택합니다.
1. **Blob 업로드** 창에서 다음 작업을 수행합니다.
    1. **파일** 섹션에서 **폴더** 아이콘을 선택합니다.
    1. **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter**로 이동하여 **settings.json** 파일을 선택한 다음 **열기**를 선택합니다.
    1. **파일이 이미 있는 경우 덮어쓰기** 체크박스가 선택되어 있는지 확인하고 **업로드**를 선택합니다.
      > **참고**: 이 랩을 계속하기 전에 Blob이 업로드될 때까지 기다립니다.

#### 작업 2: HTTP 트리거 함수 만들기

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 누릅니다. 이 명령은 **Azure Functions Core Tools**를 사용하여 **HTTP 트리거** 템플릿을 통해 새 함수 **GetSettingInfo**를 만듭니다.

    ```powershell
    func new --template "HTTP trigger" --name "GetSettingInfo"
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [새 함수 만들기][azure-functions-core-tools-new-function] 방법을 파악할 수 있습니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

#### 작업 3: HTTP에서 트리거되어 Blob에 입력되는 함수 코드 작성

1. **시작** 화면에서 **Visual Studio Code** 타일을 선택합니다.
1. **파일** 메뉴에서 **폴더 열기**를 선택합니다.
1. 열리는 **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 이동한 후 **폴더 선택**을 선택합니다.
1. **Visual Studio Code** 창의 탐색기 창에서 **GetSettingInfo.cs** 파일을 엽니다.
1. 코드 편집기에서 예제 구현을 살펴봅니다.

    ```csharp
    using System;
    using System.IO;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Extensions.Http;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;
    using Newtonsoft.Json;
    
    namespace func
    {
        public static class GetSettingInfo
        {
            [FunctionName("GetSettingInfo")]
            public static async Task<IActionResult> Run(
                [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
                ILogger log)
            {
                log.LogInformation("C# HTTP trigger function processed a request.");
    
                string name = req.Query["name"];
    
                string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
                dynamic data = JsonConvert.DeserializeObject(requestBody);
                name = name ?? data?.name;
    
                string responseMessage = string.IsNullOrEmpty(name)
                    ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                    : $"Hello, {name}. This HTTP triggered function executed successfully.";
    
                return new OkObjectResult(responseMessage);
            }
        }
    }
    ```

1. **GetSettingInfo.cs** 파일 내의 모든 내용을 삭제합니다.

1. 다음 코드 줄을 추가하여 **Microsoft.AspNetCore.Http**, **Microsoft.AspNetCore.Mvc** 및 **Microsoft.Azure.WebJobs** 네임스페이스에 **using 지시문**을 추가합니다.

    ```csharp
    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    ```

1. 새 **public static** 클래스 **GetSettingInfo**를 만듭니다.

    ```csharp
    public static class GetSettingInfo
    { }
    ```

1. **GetSettingInfo.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;

    public static class GetSettingInfo
    { }
    ```

1. **GetSettingInfo** 클래스 내에서 다음 코드 블록을 추가하여 새 **public static** 식 본문 메서드 **Run**을 만듭니다. 이 메서드는 **IActionResult** 유형 변수를 반환하며, **HttpRequest** 및 **string** 유형 변수를 **request** 및 **json** 매개 변수로 가져옵니다.

    ```csharp
    public static IActionResult Run(
        HttpRequest request,
        string json)
        => null;
    ```

    > **참고**: 여기서는 임시로 반환 값을 **null**로 설정합니다.

1. 다음 코드를 추가하여 **name** 매개 변수가 **GetSettingInfo** 값으로 설정된 **FunctionNameAttribute** 유형 특성을 **Run** 메서드에 추가합니다.

    ```csharp
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        HttpRequest request,
        string json)
        => null;
    ```

1. 다음 코드를 추가하여 **methods** 매개 변수 배열이 단일 값 **GET**으로 설정된 **HttpTriggerAttribute** 유형 특성을 **request** 매개 변수에 추가합니다.

    ```csharp
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        [HttpTrigger("GET")] HttpRequest request,
        string json)
        => null;
    ```

1. 다음 코드를 추가하여 **blobPath** 매개 변수가 **content/settings.json** 값으로 설정된 **BlobAttribute** 유형 특성을 **json** 매개 변수에 추가합니다.

    ```csharp
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        [HttpTrigger("GET")] HttpRequest request,
        [Blob("content/settings.json")] string json)
        => null;
    ```

1. 다음 코드를 추가하여 단일 생성자 매개 변수로 **json** 메서드 매개 변수 값을 전달하면 **OkObjectResult** 클래스의 새 인스턴스가 반환되도록 **Run** 식 본문 메서드를 업데이트합니다.

    ```csharp
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        [HttpTrigger("GET")] HttpRequest request,
        [Blob("content/settings.json")] string json)
        => new OkObjectResult(json);
    ```

1. **GetSettingInfo.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;

    public static class GetSettingInfo
    {
        [FunctionName("GetSettingInfo")]
        public static IActionResult Run(
            [HttpTrigger("GET")] HttpRequest request,
            [Blob("content/settings.json")] string json)
            => new OkObjectResult(json);
    }
    ```

1. **저장**을 선택하여 **Recurring.cs** 파일의 변경 내용을 저장합니다.

#### 작업 4: Azure Storage Blob 확장 등록

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 [Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage/4.0.4) 확장을 **등록**합니다.

    ```powershell
    func extensions install --package Microsoft.Azure.WebJobs.Extensions.Storage --version 4.0.4
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 .NET 프로젝트를 **빌드**해 확장이 올바르게 설치되었는지 유효성을 검사합니다.

    ```powershell
    dotnet build
    ```

1. 현재 실행 중인 **Windows 터미널** 애플리케이션의 모든 인스턴스를 닫습니다.

#### 작업 5: httprepl을 사용하여 함수 테스트

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 함수 앱 프로젝트를 실행합니다.

    ```powershell
    func start --build
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [로컬에서 함수 앱 프로젝트 시작][azure-functions-core-tools-start-function] 방법을 파악할 수 있습니다.
1. 작업 표시줄에서 **Windows 터미널** 아이콘을 다시 선택하여 **Windows 터미널** 애플리케이션의 새 인스턴스를 엽니다.
1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 **httprepl** 도구를 시작합니다. 기본 URI(Uniform Resource Identifier)는 ``http://localhost:7071``로 설정합니다.

    ```powershell
    httprepl http://localhost:7071
    ```

    > **참고**: httprepl 도구에서 오류 메시지가 표시됩니다. 이 메시지는 도구가 API를 "통과"하는 데 사용할 Swagger 정의 파일을 검색하기 때문에 발생합니다. 함수 프로젝트는 Swagger 정의 파일을 생성하지 않으므로 API를 수동으로 통과해야 합니다.
1. 도구 프롬프트가 표시되면 다음 명령을 입력하고 Enter 키를 눌러 상대 **api** 엔드포인트를 찾습니다.

    ```powershell
    cd api
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 상대 **getsettinginfo** 엔드포인트를 찾습니다.

    ```powershell
    cd getsettinginfo
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 현재 엔드포인트에 대해 **get** 명령을 실행합니다.

    ```powershell
    get
    ```

1. 함수 앱에서 나온 응답의 JSON 콘텐츠를 살펴봅니다. 여기에는 다음이 포함되어야 합니다.

    ```json
    {
        "version": "0.2.4",
        "root": "/usr/libexec/mews_principal/",
        "device": {
            "id": "21e46d2b2b926cba031a23c6919"
        },
        "notifications": {
            "email": "joseph.price@contoso.com",
            "phone": "(425) 555-0162 x4151"
        }
    }
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 **httprepl** 애플리케이션을 종료합니다.

    ```powershell
    exit
    ```

1. 현재 실행 중인 **Windows 터미널** 애플리케이션의 모든 인스턴스를 닫습니다.

> **복습**: 이 연습에서는 저장소에서 JSON 파일의 콘텐츠를 반환하는 함수를 만들었습니다.

### 연습 6: Azure Functions 앱에 로컬 함수 프로젝트 배포

#### 작업 1: Azure Functions Core Tools를 사용하여 배포

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 Azure CLI(명령줄 인터페이스)에 로그인합니다.

    ```powershell
    az login
    ```

1. **Microsoft Edge** 브라우저 창에서 다음 작업을 수행합니다.
    1. Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.
    1. Microsoft 계정의 암호를 입력한 다음 **로그인**을 선택합니다.
1. 현재 열려 있는 **Windows 터미널** 창으로 돌아갑니다. 로그인 프로세스가 완료될 때까지 기다립니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 함수 앱 프로젝트를 게시합니다.

    ```powershell
    func azure functionapp publish <function-app-name>
    ```

    > **참고**: 예를 들어 **함수 앱 이름**이 **funclogicstudent**이면 ``func azure functionapp publish funclogicstudent`` 명령을 실행합니다. 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [로컬 함수 앱 프로젝트 게시][azure-functions-core-tools-publish-azure] 방법을 파악할 수 있습니다.
1. 랩을 진행하기 전에 배포가 마무리될 때까지 기다립니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

#### 작업 2: 배포 유효성 검사

1. 작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.
1. 열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.
1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **Serverless** 리소스 그룹을 찾아 선택합니다.
1. **Serverless** 블레이드에서 이 랩의 앞부분에서 만든 **funclogic[사용자 이름]** 함수 앱을 선택합니다.
1. **App Service** 블레이드에서 **Functions** 섹션의 **Functions** 옵션을 선택합니다.
1. **Functions** 창에서 기존 **GetSettingInfo** 함수를 선택합니다.
1. **함수** 블레이드의 **개발자** 섹션에서 **코드 + 테스트** 옵션을 선택합니다.
1. 함수 편집기에서 **테스트/실행**을 선택합니다.
1. 표시되는 팝업 대화 상자에서 다음 작업을 수행합니다.
    - **HTTP 메서드** 목록에서 **GET**을 선택합니다.
1. **실행**을 선택하여 함수를 테스트합니다.
1. 테스트 실행 결과를 관찰합니다. 이제 JSON 콘텐츠에 다음 내용이 포함되어 있어야 합니다.

    ```json
    {
        "version": "0.2.4",
        "root": "/usr/libexec/mews_principal/",
        "device": {
            "id": "21e46d2b2b926cba031a23c6919"
        },
        "notifications": {
            "email": "joseph.price@contoso.com",
            "phone": "(425) 555-0162 x4151"
        }
    }
    ```

> **복습**: 이 연습에서는 Azure Functions에 로컬 함수 프로젝트를 배포했으며 함수가 Azure에서 작동하는지 유효성을 검사했습니다.

### 연습 7: 구독 정리

#### 작업 1: Azure Cloud Shell 열기 및 리소스 그룹 나열

1.  Azure Portal에서 Cloud Shell 아이콘을 선택하여 새 셸 인스턴스를 엽니다.
    > **참고**: **Cloud Shell** 아이콘은 더 큼 기호(\>)와 밑줄 문자(\_)로 표시됩니다.
1. 구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 **Azure Cloud Shell 시작 마법사**를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.
    1. 셸을 구성하라는 메시지가 포함된 대화 상자가 나타납니다. **Bash**를 선택하고 선택한 구독을 검토한 다음 **스토리지 만들기**를 선택합니다.
    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. Cloud Shell 구성 옵션이 표시되지 않는 경우, 대부분은 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 수 있습니다. 랩은 새 구독을 사용한다는 가정 하에서 작성됩니다.

#### 작업 2: 리소스 그룹 삭제

1. 명령 프롬프트가 표시되면 다음 명령을 입력하고 Enter 키를 눌러 **Serverless** 리소스 그룹을 삭제합니다.

    ```powershell
    az group delete --name Serverless --no-wait --yes
    ```

1. 포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: 활성 애플리케이션 닫기

1. 현재 실행 중인 Microsoft Edge 애플리케이션을 닫습니다.

> **복습**: 이 연습에서는이 랩에 사용된 리소스 그룹을 제거하여 구독을 정리했습니다.

[azure-functions-core-tools-new-function]: https://docs.microsoft.com/azure/azure-functions/functions-run-local#create-func
[azure-functions-core-tools-new-project]: https://docs.microsoft.com/azure/azure-functions/functions-run-local#create-a-local-functions-project
[azure-functions-core-tools-start-function]: https://docs.microsoft.com/azure/azure-functions/functions-run-local#start
[azure-functions-core-tools-publish-azure]: https://docs.microsoft.com/azure/azure-functions/functions-run-local#publish
