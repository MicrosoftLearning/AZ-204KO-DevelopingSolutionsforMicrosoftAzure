---
lab:
    az204Title: '랩 09: Event Grid 이벤트 게시 및 구독'
    az020Title: '랩 09: Event Grid 이벤트 게시 및 구독'
    az204Module: '모듈 09: 이벤트 기반 솔루션 개발'
    az020Module: '모듈 09: 이벤트 기반 솔루션 개발'
    type: '해답'
---
    
# 랩 09: Event Grid 이벤트 게시 및 구독
# 학생 랩 답변 키

## Microsoft Azure 사용자 인터페이스

Microsoft 클라우드 도구의 동적 특성을 감안할 때, 이 교육 콘텐츠를 개발한 후 Azure UI가 변경될 수 있습니다. 이러한 변경으로 인해 랩 지침 및 랩 단계가 일치하지 않을 수 있습니다.

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

- Microsoft Visual Studio Code

### 연습 1: Azure 리소스 만들기

#### 작업 1: Azure Portal 열기

1. 작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.

1. 열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.

1. Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.

1. Microsoft 계정의 암호를 입력한 다음 **로그인**을 선택합니다.

    > **참고**: Azure Portal에 처음 로그인하는 경우 포털 둘러보기가 제공됩니다. 둘러보기를 건너뛰고 포털 사용을 시작하려면 시작하기를 선택합니다.

#### 작업 2: Azure Cloud Shell 열기

1. Azure Portal에서 Cloud Shell 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: Cloud Shell 아이콘은 더 큼 기호(\>)와 밑줄 문자(\_)로 표시됩니다.

1. 구독을 사용하여 Cloud Shell을 처음 여는 경우 Azure Cloud Shell 시작 마법사를 사용하여 Cloud Shell을 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.

    - 셸을 사용하기 위해 새 스토리지 계정을 생성하라는 대화 상자가 표시되면 기본 설정을 수락한 다음 **스토리지 만들기**를 선택합니다.

    > **참고**: 랩을 계속 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. **Cloud Shell**의 구성 옵션이 나타나지 않는 경우 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 수 있습니다. 랩은 새 구독을 사용한다는 가정 하에서 작성됩니다.

1. Azure Portal에서 **Cloud Shell** 명령 프롬프트에 따라 다음 명령을 입력한 다음 Enter 키를 눌러 Azure CLI(Azure 명령줄 인터페이스) 도구의 버전을 가져옵니다.

    ```bash
    az --version
    ```

#### 작업 3: Microsoft.EventGrid 공급자 등록 보기

1. Portal의 **Cloud Shell** 명령 프롬프트에서 다음 작업을 수행합니다.

    1. 다음 명령을 입력하고 Enter 키를 눌러 Azure CLI의 루트 수준에서 하위 그룹 및 명령 목록을 가져옵니다.

        ```bash
        az --help
        ```

    1. 다음 명령을 입력한 다음 Enter 키를 눌러 리소스 공급자가 사용할 수 있는 명령 목록을 가져옵니다.

        ```bash
        az provider --help
        ```

    1. 다음 명령을 입력한 다음 Enter 키를 눌러 현재 등록된 모든 공급자를 나열합니다.

        ```bash
        az provider list
        ```

    1. 다음 명령을 입력한 다음 Enter 키를 눌러 현재 등록된 공급자의 네임스페이스만 나열합니다.

        ```bash
        az provider list --query "[].namespace"
        ```

    1. 현재 등록된 공급자 목록을 검토합니다. **Microsoft.EventGrid** 공급자가 현재 공급자 목록에 포함되어 있습니다.

1. Cloud Shell 창을 닫습니다.

#### 작업 4: 사용자 지정 Event Grid 항목 만들기

1. Azure Portal 탐색 창에서 **리소스 만들기**를 선택합니다.

1. **새로 만들기** 블레이드에서 **Marketplace 검색** 텍스트 상자를 찾습니다.

1. 검색 상자에 **Event Grid 항목**을 입력하고 Enter 키를 누릅니다.

1. **모든 항목** 검색 결과 블레이드에서 **Event Grid 항목** 결과를 선택합니다.

1. **Event Grid 항목** 블레이드에서 **만들기**를 선택합니다.

1. **항목 만들기** 블레이드에서 다음 작업을 수행합니다.

    1. **이름** 텍스트 상자에 **hrtopic[사용자 이름]** 을 입력합니다.

    1. **리소스 그룹** 섹션에서 **새로 만들기**를 선택하고 **PubSubEvents**를 입력한 다음 **확인**을 선택합니다.

    1. **위치** 드롭다운 목록에서 **(미국) 미국 동부** 지역을 선택합니다.

    1. **이벤트 스키마** 드롭다운 목록에서 **Event Grid 스키마**를 선택한 후 **만들기**를 선택합니다.
  
    > **참고**: 랩을 진행하기 전에 Azure가 토픽을 만들 때까지 기다립니다. 항목이 생성되면 알림을 받게 됩니다.

#### 작업 5: Azure Event Grid 뷰어를 웹앱에 배포하기

1. Azure Portal 탐색 창에서 **리소스 만들기**를 선택합니다.

1. 새로 만들기 블레이드에서 Marketplace 검색 텍스트 상자를 찾습니다.

1. 검색 상자에 웹을 입력하고 Enter 키를 누릅니다.

1. **모든 항목** 검색 결과 블레이드에서 **웹앱** 결과를 선택합니다.

1. **웹앱** 블레이드에서 **만들기**를 선택합니다.

1. 두 번째 **웹앱** 블레이드에서 **기본**과 같은 블레이드의 탭을 찾습니다.

    > **참고**: 각 탭은 새 웹앱을 만드는 워크플로의 단계를 나타냅니다. 언제든지 검토 + 만들기를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1. **기본** 탭에서 다음 작업을 수행합니다.

    1. 구독 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.

    1. **리소스 그룹** 섹션에서 **PubSubEvents**를 선택합니다.

    1. **이름** 텍스트 상자에 **eventviewer[사용자 이름]** 을 입력합니다.

    1. **게시** 섹션에서 **Docker 컨테이너**를 선택합니다.

    1. **운영 체제** 섹션에서 **Linux**를 선택합니다.

    1. **지역** 드롭다운 목록에서 **미국 동부** 지역을 선택합니다.

    1. **Linux 플랜(미국 동부)** 섹션에서 **새로 만들기**를 선택합니다. 

    1. **이름** 텍스트 상자에 **EventPlan** 값을 입력하고 **확인**을 선택합니다.

    1. SKU 및 크기 섹션을 기본값으로 둡니다.

    1. **다음: Docker**를 선택합니다.

1. **Docker** 탭에서 다음 작업을 수행합니다.

    1. **옵션** 드롭다운 목록에서 **단일 컨테이너**를 선택합니다.

    1. **이미지 원본** 드롭다운 목록에서 **Docker Hub**를 선택합니다.

    1. **액세스 형식** 드롭다운 목록에서 **공개**를 선택합니다.

    1. **이미지 및 태그** 텍스트 상자에 **microsoftlearning/azure-event-grid-viewer:latest**를 입력합니다.

    1. **검토 + 만들기**를 선택합니다.

1. **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1. 지정된 구성을 사용하여 웹앱을 만들려면 **만들기**를 선택합니다. 
  
    > **참고**: 랩을 계속하기 전에 Azure에서 웹앱을 만들 때까지 기다립니다. 앱을 만들 때 알림을 받게 됩니다.

#### 복습

이 연습에서는 랩의 나머지 부분에서 사용할 Event Grid 토픽과 웹앱을 만들었습니다.

### 연습 2: Event Grid 구독 만들기

#### 작업 1: Event Grid 뷰어 웹 애플리케이션 액세스

1. Azure Portal의 탐색 창에서 리소스 그룹을 선택합니다.

1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **PubSubEvents** 리소스 그룹을 선택합니다.

1. **PubSubEvents** 블레이드에서 이 랩의 앞부분에서 만든 **eventviewer[사용자 이름]** 웹앱을 선택합니다.

1. **App Service** 블레이드의 **설정** 범주에서 **속성** 링크를 선택합니다.

1. **속성** 섹션에서 **URL** 텍스트 상자의 값을 기록합니다. 이 값은 랩에서 나중에 사용합니다.

1. **개요**를 선택합니다.

1. **개요** 섹션에서 **찾아보기**를 선택합니다.

1. 현재 실행 중인 Azure Event Grid 뷰어 웹 애플리케이션을 관찰합니다. 이 웹 애플리케이션은 랩의 나머지 부분에서 실행되도록 둡니다.

    > **참고**: 이 웹 애플리케이션은 이벤트가 엔드포인트로 전송될 때 실시간으로 업데이트됩니다. 이것을 사용하여 랩 전체의 이벤트를 모니터링합니다.

1. Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

#### 작업 2: 새 구독 만들기

1. Azure Portal의 탐색 창에서 리소스 그룹을 선택합니다.

1. 리소스 그룹 블레이드에서 이 랩의 앞부분에서 만든 PubSubEvents 리소스 그룹을 선택합니다.

1. **PubSubEvents** 블레이드에서 이 랩의 앞부분에서 만든 **hrtopic[사용자 이름]** Event Grid 항목을 선택합니다.

1. **Event Grid 항목** 블레이드에서 **+ 이벤트 구독**을 선택합니다.

1. **이벤트 구독 만들기** 블레이드에서 다음 작업을 수행합니다.

    1. **이름** 텍스트 상자에 **basicsub**를 입력합니다.

    1. **이벤트 스키마** 목록에서 **Event Grid 스키마**를 선택합니다.

    1. **엔드포인트 유형** 목록에서 **웹 후크**를 선택합니다.

    1. **엔드포인트**를 선택합니다.

    1. **웹 후크 선택** 대화 상자의 **구독자 엔드포인트** 텍스트 상자에 이전에 기록한 **웹앱 URL** 값을 입력합니다. 그런 다음 해당 URL에 **https://** 접두사가 사용되는지 확인하고 **/api/updates** 접미사를 추가한 후에 **선택 확인**을 선택합니다.

        > **참고**: 예를 들어 **웹앱 URL** 값이 ``http://eventviewerstudent.azurewebsites.net/``인 경우 **구독자 엔드포인트**는 ``https://eventviewerstudent.azurewebsites.net/api/updates``가 됩니다.

    1. **만들기**를 선택합니다.
  
    > **참고**: 랩을 계속하기 전에 Azure에서 구독을 만들 때까지 기다립니다. 구독이 생성되면 알림을 받게 됩니다.

#### 작업 3: 구독 유효성 검사 이벤트 관찰

1. **Azure Event Grid 뷰어** 웹 애플리케이션을 표시하는 브라우저 창으로 돌아갑니다.

1. 구독 만들기 작업의 일부로 만든 **Microsoft.EventGrid.SubscriptionValidationEvent** 이벤트를 검토합니다.

1. 이벤트를 선택하여 JSON 콘텐츠를 검토합니다.

1. Azure Portal을 통해 현재 열려 있는 브라우저 창으로 돌아갑니다.

#### 작업 4: 구독 자격 증명 기록

1. Azure Portal의 탐색 창에서 리소스 그룹을 선택합니다.

1. 리소스 그룹 블레이드에서 이 랩의 앞부분에서 만든 PubSubEvents 리소스 그룹을 선택합니다.

1. PubSubEvents 블레이드에서 이 랩의 앞부분에서 만든 **hrtopic[사용자 이름]** Event Grid 항목을 선택합니다.

1. **Event Grid 항목** 블레이드에서 **항목 엔드포인트** 필드의 값을 기록합니다. 이 값은 랩에서 나중에 사용합니다.

1. **설정** 범주에서 **액세스 키** 링크를 선택합니다.

1. **액세스 키** 섹션에서 **키 1** 텍스트 상자의 값을 기록합니다. 이 값은 랩에서 나중에 사용합니다.

#### 복습

이 연습에서는 새 구독을 만들고 등록의 유효성을 검사한 다음 토픽에 새 이벤트를 게시하는 데 필요한 자격 증명을 기록했습니다.

### 연습 3: .NET에서 Event Grid 이벤트 게시

#### 작업 1: .NET 프로젝트 만들기

1. **시작** 화면에서 **Visual Studio Code** 타일을 선택합니다.

1. 파일 메뉴에서 폴더 열기를 선택합니다.

1. 열리는 **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\09\\Starter\\EventPublisher** 로 이동한 후 **폴더 선택**을 선택합니다.

1. **Visual Studio Code** 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 **터미널에서 열기**를 선택합니다.

1. 열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 현재 폴더에 **EventPublisher**라는 새 .NET 프로젝트를 만듭니다.

    ```powershell
    dotnet new console --name EventPublisher --output .
    ```

    > **참고**: dotnet new 명령은 새 콘솔 프로젝트를 프로젝트와 이름이 같은 폴더에 만듭니다.

1. 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 NuGet에서 **Azure.Messaging.EventGrid**의 버전 4.1.0을 가져옵니다.

    ```powershell
    dotnet add package Azure.Messaging.EventGrid --version 4.1.0
    ```

    > **참고**: **dotnet add package** 명령은 NuGet에서 **Microsoft.Azure.EventGrid** 패키지를 추가합니다. 더 자세한 내용은 [Azure.Messaging.EventGrid](https://www.nuget.org/packages/Azure.Messaging.EventGrid/4.1.0)를 참조하세요.

1. 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 빌드합니다.

    ```powershell
    dotnet build
    ```

1. **터미널 종료** 또는 **휴지통** 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 작업 2: Program 클래스를 수정하여 Event Grid에 연결

1. **Visual Studio Code** 창의 탐색기 창에서 **Program.cs** 파일을 엽니다.

1. **Program.cs** 파일의 코드 편집기 탭에서 기존 파일의 모든 코드를 삭제합니다.

1. 다음 코드 줄을 추가하여 NuGet에서 가져온 **Azure.Messaging.EventGrid** 패키지의 **Azure** 및 **Azure.Messaging.EventGrid** 네임스페이스를 가져옵니다.

    ```csharp
    using Azure;
    using Azure.Messaging.EventGrid;
    ```

1. 다음 코드 줄을 추가하여 이 파일에 사용할 기본 제공 네임스페이스에 대해 **using** 지시문을 추가합니다.

    ```csharp
    using System;
    using System.Threading.Tasks;
    ```

1. 다음 코드를 입력하여 새 **Program** 클래스를 만듭니다.

    ```csharp
    public class Program
    {
    }
    ```

1. **Program** 클래스에서 다음 코드 줄을 입력하여 **topicEndpoint**라는 이름의 새 문자열 상수를 만듭니다.

    ```csharp
    private const string topicEndpoint = "";
    ```

1. 이 랩의 앞부분에서 기록한 Event Grid 항목의 **항목 엔드포인트**로 값을 설정하여 **topicEndpoint** 문자열 상수를 업데이트합니다.

1. **Program** 클래스에서 다음 코드 줄을 입력하여 **topicKey** 라는 이름의 새 문자열 상수를 만듭니다.

    ```csharp
    private const string topicKey = "";
    ```

1. 이 랩의 앞부분에서 기록한 Event Grid 항목의 키에 값을 설정하여 topicKey 문자열 상수의 값을 업데이트합니다.

1. **Program** 클래스에서 다음 코드 줄을 입력하여 새 비동기 **Main** 메서드를 만듭니다.

    ```csharp
    public static async Task Main(string[] args)
    {
    }
    ```

1. **Program.cs** 파일을 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using System;
    using System.Threading.Tasks;
    using Azure;
    using Azure.Messaging.EventGrid;

    public class Program
    {
        private const string topicEndpoint = "<topic-endpoint>";
        private const string topicKey = "<topic-key>";
        
        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### 작업 3: 새 이벤트 게시

1. **Main** 메서드에서 다음 작업을 수행하여 이벤트 목록을 항목 엔드포인트에 게시합니다.

    1. 다음 코드 줄을 추가하여 **Uri** 형식의 새 변수 **endpoint**를 만듭니다. 이때 생성자 매개 변수로는 **topicEndpoint** 문자열 상수를 사용합니다.

        ```csharp
        Uri endpoint = new Uri(topicEndpoint); 
        ```

    1. 다음 코드 줄을 추가하여 **[AzureKeyCredential](https://docs.microsoft.com/dotnet/api/azure.azurekeycredential)** 형식의 새 변수 **credential**을 만듭니다. 이때 생성자 매개 변수로는 **topicKey** 문자열 상수를 사용합니다.

        ```csharp
        AzureKeyCredential credential = new AzureKeyCredential(topicKey);
        ```

    1. 다음 코드 줄을 추가하여 **[EventGridPublisherClient](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient)** 형식의 새 변수 **client**를 만듭니다. 이때 생성자 매개 변수로는 **endpoint** 및 **credential** 변수를 사용합니다.

        ```csharp
        EventGridPublisherClient client = new EventGridPublisherClient(endpoint, credential);
        ```

    1. 다음 코드 블록을 추가하여 [EventGridEvent](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridevent) 형식의 새 변수 firstEvent를 만든 다음, 샘플 데이터로 EventGridEvent 변수를 채웁니다.

        ```csharp
        EventGridEvent firstEvent = new EventGridEvent(
            subject: $"New Employee: Alba Sutton",
            eventType: "Employees.Registration.New",
            dataVersion: "1.0",
            data: new
            {
                FullName = "Alba Sutton",
                Address = "4567 Pine Avenue, Edison, WA 97202"
            }
        );
        ```

    1. 다음 코드 블록을 추가하여 [EventGridEvent](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridevent) 형식의 새 변수 secondEvent를 만든 다음, 샘플 데이터로 EventGridEvent 변수를 채웁니다.

        ```csharp
        EventGridEvent secondEvent = new EventGridEvent(
            subject: $"New Employee: Alexandre Doyon",
            eventType: "Employees.Registration.New",
            dataVersion: "1.0",
            data: new
            {
                FullName = "Alexandre Doyon",
                Address = "456 College Street, Bow, WA 98107"
            }
        );
        ```

    1. 다음 코드 줄을 추가하여 **firstEvent** 변수를 매개 변수로 사용해 **[EventGridPublisherClient.SendEventAsync](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient.sendeventasync)** 메서드를 비동기식으로 호출합니다.

        ```csharp
        await client.SendEventAsync(firstEvent);
        ```

    1. 다음 코드 줄을 추가하여 **"First event published"** 메시지를 콘솔에 렌더링합니다.

        ```csharp
        Console.WriteLine("First event published");
        ```

    1. 다음 코드 줄을 추가하여 **secondEvent** 변수를 매개 변수로 사용해 **[EventGridPublisherClient.SendEventAsync](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient.sendeventasync)** 메서드를 비동기식으로 호출합니다.

        ```csharp
        await client.SendEventAsync(secondEvent);
        ```

    1. 다음 코드 줄을 추가하여 **"Second event published"** 메시지를 콘솔에 렌더링합니다.

        ```csharp
        Console.WriteLine("Second event published");
        ```

1. **Main** 메서드를 검토합니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    public static async Task Main(string[] args)
    {
        Uri endpoint = new Uri(topicEndpoint);
        AzureKeyCredential credential = new AzureKeyCredential(topicKey);
        EventGridPublisherClient client = new EventGridPublisherClient(endpoint, credential);
        
        EventGridEvent firstEvent = new EventGridEvent(
            subject: $"New Employee: Alba Sutton",
            eventType: "Employees.Registration.New",
            dataVersion: "1.0",
            data: new
            {
                FullName = "Alba Sutton",
                Address = "4567 Pine Avenue, Edison, WA 97202"
            }
        );

        EventGridEvent secondEvent = new EventGridEvent(
            subject: $"New Employee: Alexandre Doyon",
            eventType: "Employees.Registration.New",
            dataVersion: "1.0",
            data: new
            {
                FullName = "Alexandre Doyon",
                Address = "456 College Street, Bow, WA 98107"
            }
        );

        await client.SendEventAsync(firstEvent);
        Console.WriteLine("First event published");

        await client.SendEventAsync(secondEvent);
        Console.WriteLine("Second event published");
    }
    ```

1. **Program.cs** 파일을 저장합니다.

1. Visual Studio Code 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 터미널에서 열기를 선택합니다.

1. 열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```powershell
    dotnet run
    ```

    > **참고**: 빌드 오류가 있는 경우, **Allfiles (F):\\Allfiles\\Labs\\09\\Solution\\EventPublisher** 폴더에 있는 **Program.cs** 파일을 검토하세요.

1. 현재 실행 중인 콘솔 애플리케이션의 성공 메시지 출력을 관찰합니다.

1. 터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 작업 4: 게시된 이벤트 살펴보기

1. **Azure Event Grid 뷰어** 웹 애플리케이션이 있는 브라우저 창으로 돌아갑니다.

1. 콘솔 애플리케이션으로 생성한 Employees.Registration.New 이벤트를 검토합니다.

1. 아무 이벤트나 선택하고 JSON 콘텐츠를 검토합니다.

1. Azure Portal로 돌아갑니다.

#### 복습

이 연습에서는 .NET 콘솔 애플리케이션을 사용하여 Event Grid 항목에 새 이벤트를 게시했습니다.

### 연습 4: 구독 정리

#### 작업 1: Azure Cloud Shell 열기

1. Azure Portal에서 **Cloud Shell** 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: Cloud Shell 아이콘은 더 큼 기호(\>)와 밑줄 문자(\_)로 표시됩니다.

1. 구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 Azure Cloud Shell 시작 마법사를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.

    1. 셸을 구성하라는 메시지가 포함된 대화 상자가 나타납니다. Bash를 선택하고 선택한 구독을 검토한 다음 스토리지 만들기를 선택합니다.

    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. Cloud Shell의 구성 옵션이 나타나지 않는 경우 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 수 있습니다. 랩은 새 구독을 사용한다는 가정 하에서 작성됩니다.

#### 작업 2: 리소스 그룹 삭제

1. 다음 명령을 입력하고 Enter 키를 눌러 PubSubEvents 리소스 그룹을 삭제합니다.

    ```bash
    az group delete --name PubSubEvents --no-wait --yes
    ```

1. 포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: 활성 애플리케이션 닫기

1. 현재 실행 중인 Microsoft Edge 애플리케이션을 닫습니다.

1. 현재 실행 중인 Visual Studio Code 애플리케이션을 닫습니다.

#### 복습

이 연습에서는 이 랩에 사용된 리소스 그룹을 제거하여 구독을 정리했습니다.
