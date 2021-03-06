---
lab:
    az204Title: '랩 10: Azure Queue Storage를 사용하여 비동기적으로 메시지 처리'
    az020Title: '랩 10: Azure Queue Storage를 사용하여 비동기적으로 메시지 처리'
    az204Module: '모듈 10: 메시지 기반 솔루션 개발'
    az020Module: '모듈 10: 메시지 기반 솔루션 개발'
    type: '해답'
---

# 랩 10: Azure Queue Storage를 사용하여 비동기적으로 메시지 처리
# 학생 랩 답변 키

## Microsoft Azure 사용자 인터페이스

Microsoft 클라우드 도구의 동적 특성을 감안할 때, 이 교육 콘텐츠를 개발한 후 Azure UI가 변경될 수 있습니다. 이러한 변경으로 인해 랩 지침 및 랩 단계가 일치하지 않을 수 있습니다.

Microsoft는 커뮤니티가 필요한 변경 사항을 제공하면 이 교육 과정을 업데이트합니다. 그러나 클라우드 업데이트가 자주 발생하기 때문에 이 교육 콘텐츠가 업데이트되기 전에 UI가 먼저 변경될 수 있습니다. **이 경우 변경 사항에 적응하고 필요에 따라 랩에서 작업합니다.**

## 지침

### 시작하기 전 확인 사항

#### 랩 가상 머신에 로그인

다음 자격 증명을 사용하여 Windows 10 VM(가상 머신)에 로그인합니다.
    
-   사용자 이름: **Admin**

-   암호: **Pa55w.rd**

> **참고**: 강사가 가상 랩 환경 연결에 대한 지침을 제공합니다.

#### 설치된 애플리케이션 검토

Windows 10 데스크톱에서 작업 표시줄을 찾습니다. 작업 표시줄에는 이 랩에서 사용할 애플리케이션에 대한 아이콘이 포함되어 있습니다.
    
-   Microsoft Edge

-   Visual Studio Code

-   Azure Storage Explorer

### 연습 1: Azure 리소스 만들기

#### 작업 1: Azure Portal 열기

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.

1.  열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.

1.  Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.

1.  Microsoft 계정의 암호를 입력한 다음 로그인을 선택합니다.

    > **참고**: Azure Portal에 처음 로그인하는 경우 포털 둘러보기가 제공됩니다. 둘러보기를 건너뛰고 포털 사용을 시작하려면 시작하기를 선택합니다.

#### 작업 2: 스토리지 계정 만들기

1.  Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.

1.  **모든 서비스** 블레이드에서 **스토리지 계정**을 선택합니다.

1.  **스토리지 계정** 블레이드에서 스토리지 계정 인스턴스 목록을 가져옵니다.

1.  **스토리지 계정** 블레이드에서 **새로 만들기**를 선택합니다.

1.  **스토리지 계정 만들기** 블레이드에서 **기본**, **태그**, **검토 + 만들기** 등의 블레이드 탭을 살펴봅니다.

    > **참고**: 각 탭은 새 스토리지 계정을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭을 선택하고 탭 영역 내에서 다음 작업을 수행합니다.
    
    1.  **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    
    1.  **리소스 그룹** 섹션에서 **새로 만들기**를 선택하고 **AsyncProcessor**를 입력한 다음 **확인**을 선택합니다.
    
    1.  **스토리지 계정 이름** 텍스트 상자에 **asyncstor[사용자 이름]** 을 입력합니다.
    
    1.  **위치** 목록에서 **(미국) 미국 동부** 지역을 선택합니다.
    
    1.  **성능** 섹션에서 **표준**을 선택합니다.
    
    1.  **계정 종류** 목록에서 **StorageV2(범용 v2)** 를 선택합니다.
    
    1.  **복제** 목록에서 **LRS(로컬 중복 스토리지)** 를 선택합니다.
        
    1.  **검토 + 만들기**를 선택합니다.

1.  **검토+ 만들기** 탭에서 이전 단계에서 지정한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 스토리지 계정을 만들려면 만들기를 선택합니다.

    > **참고**: **배포** 블레이드에서 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

1.	**배포** 블레이드에서 **리소스로 이동** 단추를 선택하여 새로 만든 스토리지 계정으로 이동합니다.

1.	**스토리지 계정** 블레이드에서 **설정** 섹션을 찾은 다음 **액세스 키**를 선택합니다.

1.	**액세스 키** 블레이드에서 키 중 하나를 선택하고 **연결 문자열** 상자 중 하나의 값을 기록합니다. 나중에 이 랩에서 이 값을 사용하게 됩니다.

    > **참고**: 어떤 연결 문자열을 선택하든 상관없습니다. 서로 교환할 수 있습니다.

#### 복습

이 연습에서는 나머지 랩에서 사용할 새 Azure Storage 계정을 만들었습니다.

### 연습 2: .NET 프로젝트에서 Azure Storage SDK 구성 

#### 작업 1: .NET 프로젝트 만들기

1.  시작 화면에서 Visual Studio Code 타일을 선택합니다.

1.  **파일** 메뉴에서 **폴더 열기**를 선택합니다.

1.  열리는 **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\10\\Starter\\MessageProcessor**로 이동한 후 **폴더 선택**을 선택합니다.

1.  **Visual Studio Code** 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 **터미널에서 열기**를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 현재 폴더에 **MessageProcessor**라는 새 .NET 프로젝트를 만듭니다.

    ```
    dotnet new console --name MessageProcessor --output .
    ```

    > **참고**: dotnet new 명령은 새 콘솔 프로젝트를 프로젝트와 이름이 같은 폴더에 만듭니다.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 NuGet에서 **Azure.Storage.Queues** 버전 12.0.0을 가져옵니다.

    ```
    dotnet add package Azure.Storage.Queues --version 12.0.0
    ```

    > **참고**: **dotnet add package** 명령은 NuGet에서 **Azure.Storage.Queues** 패키지를 추가합니다. 자세한 내용은 [Azure.Storage.Queues](https://www.nuget.org/packages/Azure.Storage.Queues/12.0.0)로 이동하세요.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 빌드합니다.

    ```
    dotnet build
    ```

1.  **터미널 종료** 또는 **휴지통** 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 작업 2: Azure Storage에 액세스하는 코드 작성

1.  **Visual Studio Code** 창의 탐색기 창에서 **Program.cs** 파일을 엽니다.

1.  **Program.cs** 파일의 코드 편집기 탭에서 기존 파일의 모든 코드를 삭제합니다.

1.  다음 코드 줄을 추가하여 NuGet에서 가져온 **Azure.Storage.Queues** 패키지의 **Azure**, **Azure.Storage.Queues** 및 **Azure.Storage.Queues.Models** 네임스페이스를 가져옵니다.

    ```
    using Azure;
    using Azure.Storage.Queues;
    using Azure.Storage.Queues.Models;
    ```
    
1.  다음 코드 줄을 추가하여 이 파일에 사용할 기본 제공 네임스페이스에 대해 **using** 지시문을 추가합니다.

    ```
    using System;
    using System.Text;
    using System.Threading.Tasks;
    ```

1.  다음 코드를 입력하여 새 **Program** 클래스를 만듭니다.

    ```
    public class Program
    {
    }
    ``` 

1.  **Program** 클래스에서 다음 코드 줄을 입력하여 **storageConnectionString**라는 이름의 새 문자열 상수를 만듭니다.

    ```
    private const string storageConnectionString = "";
    ```

1.  이 랩의 앞부분에서 기록한 스토리지 계정의 **연결 문자열**로 값을 설정하여 **storageConnectionString** 문자열 상수를 업데이트합니다.

1.  **Program** 클래스에 다음 코드 줄을 입력하여 값이 **messagequeue**인 새 문자열 상수 **queueName**을 만듭니다.

    ```
    private const string queueName = "messagequeue";
    ```

1.  **Program** 클래스에서 다음 코드 줄을 입력하여 새 비동기 **Main** 메서드를 만듭니다.

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  **Program.cs** 파일을 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```
    using Azure;
    using Azure.Storage.Queues;
    using Azure.Storage.Queues.Models;
    using System;
    using System.Text;
    using System.Threading.Tasks;

    public class Program
    {
        private const string storageConnectionString = "<storage-connection-string>";
        private const string queueName = "messagequeue";

        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### 작업 3: Azure Storage 액세스 유효성 검사

1.  **Main** 메서드에서 **QueueClient** 형식의 새 변수 *client*를 만들어 스토리지 계정에 연결하는 다음 코드 줄을 추가합니다.

    ```
    QueueClient client = new QueueClient(storageConnectionString, queueName);  
    ```

1.  **Main** 메서드에서 큐가 아직 없으면 비동기식으로 큐를 만드는 다음 코드 줄을 추가합니다.

    ```        
    await client.CreateAsync();
    ```

1.  **Main** 메서드에서 "Account Metadata" 섹션의 헤더를 렌더링하는 다음 코드 줄을 추가합니다.

    ```
    Console.WriteLine($"---Account Metadata---");
    ```
    
1.  **Main** 메서드에서 큐 엔드포인트의 URI(Uniform Resource Identifier)를 렌더링하는 다음 코드 줄을 추가합니다.

    ```
    Console.WriteLine($"Account Uri:\t{client.Uri}");
    ```

1.  **Main** 메서드를 살펴봅니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```
    public static async Task Main(string[] args)
    {
        QueueClient client = new QueueClient(storageConnectionString, queueName);        
        await client.CreateAsync();

        Console.WriteLine($"---Account Metadata---");
        Console.WriteLine($"Account Uri:\t{client.Uri}");
    }
    ```

1.  **Program.cs** 파일을 저장합니다.

1.  **Visual Studio Code** 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 **터미널에서 열기**를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```
    dotnet run
    ```

    > **참고**: 빌드 오류가 있는 경우 **Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor** 폴더에 있는 **Program.cs** 파일을 검토합니다.

1.  현재 실행 중인 콘솔 애플리케이션의 출력을 살펴봅니다. 출력에는 큐 엔드포인트에 대한 메타데이터가 포함되어 있습니다.

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 복습

이 연습에서는 .NET 프로젝트를 구성하여 스토리지 서비스에 액세스하고 서비스를 통해 사용할 수 있는 큐를 조작했습니다.

### 연습 3: 큐에서 메시지 받기

#### 작업 1: 큐 메시지에 액세스하는 코드 작성

1.  **Main** 메서드에서 "Existing Messages" 섹션의 헤더를 렌더링하는 다음 코드 줄을 추가합니다.

    ```
    Console.WriteLine($"---Existing Messages---");
    ```

1.  **Main** 메서드 내에서 다음 작업을 수행하여 큐 메시지를 검색할 때 사용할 변수를 만듭니다.

    1.  값이 **10**인 **int** 형식 변수 *batchSize*를 만드는 다음 코드 줄을 추가합니다.

        ```
        int batchSize = 10;
        ```

    1.  값이 **2.5 seconds**인 **TimeSpan** 형식 변수 *visibilityTimeout*을 만드는 다음 코드 줄을 추가합니다.

        ```
        TimeSpan visibilityTimeout = TimeSpan.FromSeconds(2.5d);
        ```

1.  Main 메서드 내에서 다음 작업을 수행하여 큐 서비스에서 비동기적으로 메시지 배치를 검색합니다.

    1.  *batchSize* 및 *visibilityTimeout* 변수를 매개 변수로 전달하여 **QueueClient** 클래스의 **ReceiveMessagesAsync** 비동기 메서드를 호출하는 다음 코드 줄을 추가합니다.

        ```
        client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

    1.  **await** 키워드를 사용하여 식을 비동기식으로 처리하는 코드를 더 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

    1.  **[Response<QueueMessage[]>](https://docs.microsoft.com/dotnet/api/azure.response-1)** 형식의 새 변수 *messages*에 식의 결과를 저장하는 코드를 더 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        Response<QueueMessage[]> messages = await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

1.  **Main** 메서드 내에서 다음 작업을 수행하여 코드를 반복 실행해 각 메시지의 속성을 렌더링합니다.

    1.  **[QueueMessage[]](https://docs.microsoft.com/dotnet/api/azure.storage.queues.models.queuemessage)** 형식 *messages* 변수의 **[Value](https://docs.microsoft.com/dotnet/api/azure.response-1.value)** 속성에 저장된 각 메시지에 대해 반복 실행되는 **foreach** 루프를 만드는 다음 코드 줄을 추가합니다.

        ```
        foreach(QueueMessage message in messages?.Value)
        {
        }
        ```

    1.  **foreach** 루프 내에서 각 **QueueMessage** 인스턴스의 **MessageId** 및 **MessageText** 속성을 렌더링하는 다른 코드 줄을 추가합니다.
    
        ```
        Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
        ```

1.  **Main** 메서드를 살펴봅니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```
    public static async Task Main(string[] args)
    {
        // 간결성을 위해 기존 코드를 제거함

        Console.WriteLine($"---Existing Messages---");
        int batchSize = 10;
        TimeSpan visibilityTimeout = TimeSpan.FromSeconds(2.5d);
        
        Response<QueueMessage[]> messages = await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);

        foreach(QueueMessage message in messages?.Value)
        {
            Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
        }
    }
    ```

1.  **Program.cs** 파일을 저장합니다.

1.  Visual Studio Code 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 터미널에서 열기를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 빌드합니다.

    ```
    dotnet build
    ```

    > **참고**: 빌드 오류가 있는 경우 **Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor** 폴더에 있는 **Program.cs** 파일을 검토합니다.

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 작업 2: 메시지 큐 액세스 테스트

1.  Visual Studio Code 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 터미널에서 열기를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```
    dotnet run
    ```

    > **참고**: 빌드 오류가 있는 경우 **Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor** 폴더에 있는 **Program.cs** 파일을 검토합니다.

1.  현재 실행 중인 콘솔 애플리케이션의 출력을 살펴봅니다. 출력은 큐에 메시지가 없음을 나타냅니다.

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **AsyncProcessor** 리소스 그룹을 찾아 선택합니다.

1.  **AsyncProcessor** 블레이드에서 이 랩의 앞부분에서 만든 **asyncstor[사용자 이름]** 스토리지 계정을 선택합니다.

1.  **스토리지 계정** 블레이드에서 **개요**를 선택합니다. 

1.  **개요** 섹션에서 **탐색기에서 열기**를 선택합니다.

1.  **Azure Storage Explorer** 창에서 **Azure Storage Explorer 열기**를 선택합니다.

    > **참고**: 포털을 사용하여 Storage Explorer를 처음 여는 경우 포털에서 나중에 이러한 유형의 링크를 열 수 있도록 허용하라는 메시지가 표시될 수 있습니다. 메시지를 수락해야 합니다.

1.  **Azure Storage Explorer** 애플리케이션에서 Azure 계정에 로그인하라는 메시지가 표시됩니다. 다음 작업을 통해 로그인합니다.

    1.  팝업 대화 상자에서 **로그인**을 선택합니다.

    1.  **Azure Storage에 연결** 창에서 **Azure 계정 추가**를 선택하고 **Azure 환경** 목록에서 **Azure**를 선택한 후 **다음**을 선택합니다.

    1.  **사용자 계정 로그인** 팝업 창에서 Microsoft 계정의 전자 메일 주소를 입력하고 **다음**을 선택합니다.

    1.  계속해서 **사용자 계정 로그인** 팝업 창에 Microsoft 계정의 암호를 입력한 다음 **로그인**을 선택합니다.

    1.  **계정 관리** 창에서 **적용**을 선택합니다.

    1.  구독 정보가 입력된 **탐색기** 페이지가 다시 표시되는지 확인합니다.

1.  **Azure Storage Explorer** 애플리케이션의 **탐색기** 창에서 이 랩의 앞부분에서 만든 **asyncstor[사용자 이름]** 스토리지 계정을 찾아 확장합니다.

1.  **asyncstor[사용자 이름]** 스토리지 계정 내에서 **큐** 노드를 찾아 확장합니다.

1.  **큐** 노드에서 이 랩 앞부분에서 .NET 코드를 사용하여 만든 **messagequeue** 큐를 엽니다.

1.  **messagequeue** 탭에서 **메시지 추가**를 선택합니다.

1.  **메시지 추가** 팝업 창에서 다음 작업을 수행합니다.

    1.  **메시지 텍스트** 텍스트 상자에 **Hello World** 값을 입력합니다.

    1.  **만료일** 텍스트 상자에 **12** 값을 입력합니다.

    1.  **만료일** 드롭다운 목록에서 **시간**을 선택합니다.

    1.  **Base64로 메시지 본문 인코딩** 체크박스가 선택되어 있지 않은지 확인합니다.

    1.  **확인**을 선택합니다.

1.  **Visual Studio Code** 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 **터미널에서 열기**를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```
    dotnet run
    ```

    > **참고**: 빌드 오류가 있는 경우 **Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor** 폴더에 있는 **Program.cs** 파일을 검토합니다.

1.  현재 실행 중인 콘솔 애플리케이션의 출력을 살펴봅니다. 출력에는 회원님이 만든 새 메시지가 포함됩니다.

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 작업 3: 큐에 포함된 메시지 삭제

1.  Visual Studio Code 창의 탐색기 창에서 Program.cs 파일을 엽니다.

1.  **Program.cs** 파일의 코드 편집기 탭에서 **Main** 메서드 내에 있는 기존 **foreach** 루프를 찾습니다.

    ```
    foreach(QueueMessage message in messages?.Value)
    {
        Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
    }
    ```

1.  **foreach** 루프 내에서 **QueueMessage** 클래스의 **DeleteMessageAsync** 메서드를 호출하는 새 코드 줄을 추가합니다. 이 메서드에는 *message* 변수의 **MessageId** 및 **PopReceipt** 속성을 전달합니다.

    ```
    await client.DeleteMessageAsync(message.MessageId, message.PopReceipt);
    ```

1.  **Main** 메서드를 살펴봅니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```
    public static async Task Main(string[] args)
    {
        // 간결성을 위해 기존 코드를 제거함
        
        foreach(QueueMessage message in messages?.Value)
        {
            Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
            await client.DeleteMessageAsync(message.MessageId, message.PopReceipt);
        }
    }
    ```

1.  **Program.cs** 파일을 **저장**합니다.

1.  Visual Studio Code 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 터미널에서 열기를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```
    dotnet run
    ```

    > **참고**: 빌드 오류가 있는 경우 **Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor** 폴더에 있는 **Program.cs** 파일을 검토합니다.

1.  현재 실행 중인 콘솔 애플리케이션의 출력을 살펴봅니다. 랩에서 이전에 만든 메시지가 이전에 삭제되지 않았기 때문에 여전히 존재합니다.

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

1.  스토리지 탐색기로 돌아가서 이 랩의 앞부분에서 만든 **asyncstor[사용자 이름]** 스토리지 계정을 찾아 확장합니다.

1.  **asyncstor[사용자 이름]** 스토리지 계정 내에서 **큐** 노드를 찾아 확장합니다.

1.  **큐** 노드에서 이 랩 앞부분에서 .NET 코드를 사용하여 만든 **messagequeue** 큐를 엽니다.

1.  큐에 있는 빈 메시지 목록을 관찰합니다.

    > **참고**: 큐를 새로 고쳐야 할 수 있습니다.

#### 복습

이 연습에서는 .NET 라이브러리를 사용하여 저장소 큐에서 기존 메시지를 읽고 삭제했습니다.

### 연습 4: .NET을 사용하여 새 메시지를 큐에 포함

#### 작업 1: 큐 메시지를 만드는 코드를 작성합니다.

1.  Visual Studio Code 창의 탐색기 창에서 Program.cs 파일을 엽니다.

1.  **Program.cs** 파일의 코드 편집기 탭에서 기존 **Main** 메서드를 찾습니다.

1.  **Main** 메서드 내에서 "Existing Messages" 섹션의 헤더를 렌더링하는 다음 코드 줄을 추가합니다.

    ```
    Console.WriteLine($"---New Messages---");
    ```

1.  **Main** 메서드에서 다음 작업을 수행하여 메시지를 작성한 다음 비동기식으로 전송합니다.

    1.  값이 **Hi, Developer!** 인 새 문자열 변수 *greeting*을 만드는 다음 코드 줄을 추가합니다.

        ```
        string greeting = "Hi, Developer!";        
        ```

    1.  *greeting* 변수를 매개 변수로 사용하여 **QueueClient** 클래스의 **SendMessageAsync** 메서드를 호출하는 다음 코드 줄을 추가합니다.

        ```
        await client.SendMessageAsync(Convert.ToBase64String(Encoding.UTF8.GetBytes(greeting)));        
        ```

    1.  보낸 메시지의 내용을 렌더링하는 다음 코드 줄을 추가합니다.

        ```
        Console.WriteLine($"Sent Message:\t{greeting}");        
        ```

1.  **Main** 메서드를 살펴봅니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```
    public static async Task Main(string[] args)
    {
        // 간결성을 위해 기존 코드를 제거함
        
        Console.WriteLine($"---New Messages---");
        string greeting = "Hi, Developer!";
        await client.SendMessageAsync(Convert.ToBase64String(Encoding.UTF8.GetBytes(greeting)));
        
        Console.WriteLine($"Sent Message:\t{greeting}");
    }
    ```

1.  **Program.cs** 파일을 **저장**합니다.

1.  **Visual Studio Code** 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 **터미널에서 열기**를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```
    dotnet run
    ```

    > **참고**: 빌드 오류가 있는 경우 **Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor** 폴더에 있는 **Program.cs** 파일을 검토합니다.

1.  현재 실행 중인 콘솔 애플리케이션의 출력을 살펴봅니다. 보낸 새 메시지의 내용이 출력에 있어야 합니다.

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 작업 2: Storage Explorer를 사용하여 큐에 대기 중인 메시지 보기

1.  스토리지 탐색기로 돌아가서 이 랩의 앞부분에서 만든 **asyncstor[사용자 이름]** 스토리지 계정을 찾아 확장합니다.

1.  **asyncstor[사용자 이름]** 스토리지 계정 내에서 **큐** 노드를 찾아 확장합니다.

1.  **큐** 노드에서 이 랩 앞부분에서 .NET 코드를 사용하여 만든 **messagequeue** 큐를 엽니다.

1.  큐의 메시지 목록에서 하나의 새 메시지를 살펴봅니다.

    > **참고**: 큐를 새로 고쳐야 할 수 있습니다.

#### 복습

이 연습에서는 스토리지 큐에 .NET 라이브러리를 사용하여 큐에 새 메시지를 만들었습니다.

### 연습 5: 구독 정리 

#### 작업 1: Azure Cloud Shell 열기 및 리소스 그룹 나열

1.  Azure Portal의 탐색 창에서 **Cloud Shell** 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: Cloud Shell 아이콘은 더 큼 기호(\>)와 밑줄 문자(\_)로 표시됩니다.

1.  구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 **Azure Cloud Shell 시작 마법사**를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.
    
    -   셸을 구성하라는 메시지가 포함된 대화 상자가 나타납니다. Bash를 선택하고 선택한 구독을 검토한 다음 스토리지 만들기를 선택합니다. 

    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. Cloud Shell의 구성 옵션이 나타나지 않는 경우 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 가능성이 높습니다. 랩은 새 구독을 사용한다는 가정 하에서 작성됩니다.

#### 작업 2: 리소스 그룹 삭제

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 **AsyncProcessor** 리소스 그룹을 삭제합니다.

    ```
    az group delete --name AsyncProcessor --no-wait --yes
    ```
    
1.  포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: 활성 애플리케이션 닫기

1.  현재 실행 중인 Microsoft Edge 애플리케이션을 닫습니다.

1.  현재 실행 중인 Visual Studio Code 애플리케이션을 닫습니다.

1.  현재 실행 중인 Azure Storage Explorer 애플리케이션을 닫습니다.

#### 복습

이 연습에서는이 랩에 사용된 리소스 그룹을 제거하여 구독을 정리했습니다.
