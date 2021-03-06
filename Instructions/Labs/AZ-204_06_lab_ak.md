---
lab:
    az204Title: '랩 06: MSAL 및 .NET SDK를 사용하여 Microsoft Graph 인증 및 쿼리'
    az020Title: '랩 06: MSAL 및 .NET SDK를 사용하여 Microsoft Graph 인증 및 쿼리'
    az204Module: '모듈 06: 사용자 인증 및 권한 부여 구현'
    az020Module: '모듈 06: 사용자 인증 및 권한 부여 구현'
    type: '해답'
---

# 랩 06: MSAL 및 .NET SDK를 사용하여 Microsoft Graph 인증 및 쿼리
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

### 연습 1: Azure Active Directory) 애플리케이션 등록 만들기

#### 작업 1: Azure Portal 열기

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.

1.  열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.

1.  Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.

1.  Microsoft 계정의 암호를 입력한 다음 **로그인**을 선택합니다.

    > **참고**: Azure Portal에 처음 로그인하는 경우 포털 둘러보기가 제공됩니다. 둘러보기를 건너뛰고 포털 사용을 시작하려면 시작하기를 선택합니다.

#### 작업 2: 애플리케이션 등록 만들기

1.  Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.

1.  **모든 서비스** 블레이드에서 **Azure Active Directory**를 선택합니다.

1.  **Azure Active Directory** 블레이드의 **관리** 섹션에서 **앱 등록**을 선택합니다.

1.  **앱 등록** 섹션에서 **새 등록**을 선택합니다.

1.  **애플리케이션 등록** 섹션에서 다음 작업을 수행합니다.

    1.  **이름** 텍스트 상자에 **graphapp**을 입력합니다.

    1.  **지원되는 계정 유형** 목록에서 **이 조직 디렉터리의 계정만(기본 디렉터리만 - 단일 테넌트)** 체크 박스를 선택합니다.

    1.  **리디렉션 URI** 드롭다운 목록에서 **공용 클라이언트/네이티브(모바일 및 데스크톱)** 를 선택합니다.

    1.  **리디렉션 URI** 텍스트 상자에 **http\://localhost**를 입력합니다.

    1.  **등록**을 선택합니다.

#### 작업 3: 기본 클라이언트 유형 사용

1.  **graphapp** 애플리케이션 등록 블레이드의 **관리** 섹션에서 **인증**을 선택합니다.

1.  **인증** 섹션에서 다음 작업을 수행합니다.

    1.  **고급 설정** - **공용 클라이언트 흐름 허용** 하위 섹션에서 **예**를 선택합니다.

    1.  **저장**을 선택합니다.

#### 작업 4: 고유 식별자 기록

1.  **graphapp** 애플리케이션 등록 블레이드에서 **개요**를 선택합니다.

1.  **개요** 섹션에서 **애플리케이션(클라이언트) ID** 텍스트 상자의 값을 찾아 기록합니다. 이 값은 랩에서 나중에 사용합니다.

1.  **개요** 섹션에서 **디렉터리(테넌트) ID** 텍스트 상자의 값을 찾아 기록합니다. 이 값은 랩에서 나중에 사용합니다.

#### 복습

이 연습에서는 새 애플리케이션 등록을 만들고 나중에 랩에서 필요한 중요한 값을 기록했습니다.

### 연습 2: MSAL.NET 라이브러리를 사용하여 토큰을 가져옵니다.

#### 작업 1: .NET 프로젝트 만들기

1.  시작 화면에서 Visual Studio Code 타일을 선택합니다.

1.  **파일** 메뉴에서 **폴더 열기**를 선택합니다.

1.  열리는 **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\06\\Starter\\GraphClient**로 이동한 후 **폴더 선택**을 선택합니다.

1.  Visual Studio Code 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 터미널에서 열기를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 현재 폴더에 **GraphClient**라는 새 .NET 프로젝트를 만듭니다.

    ```
    dotnet new console --name GraphClient --output .
    ```

    > **참고**: dotnet new 명령은 새 콘솔 프로젝트를 프로젝트와 이름이 같은 폴더에 만듭니다.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 NuGet에서 **Microsoft.Identity.Client**의 버전 4.7.1을 가져옵니다.

    ```
    dotnet add package Microsoft.Identity.Client --version 4.7.1
    ```

    > **참고**: dotnet add package 명령은 NuGet에서 Microsoft.Identity.Client 패키지를 추가합니다. 자세한 내용은 [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client/4.7.1)를 참조하세요.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 빌드합니다.

    ```
    dotnet build
    ```

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 작업 2: Program 클래스 수정

1.  Visual Studio Code 창의 탐색기 창에서 Program.cs 파일을 엽니다.

1.  Program.cs 파일의 코드 편집기 탭에서 기존 파일의 모든 코드를 삭제합니다.

1.  다음 코드 줄을 추가하여 NuGet에서 가져온 **Microsoft.Identity.Client** 패키지에서 **Microsoft.Identity.Client** 네임스페이스를 가져옵니다.

    ```
    using Microsoft.Identity.Client;
    ```
    
1.  다음 코드 줄을 추가하여 이 파일에 사용할 기본 제공 네임스페이스에 대해 **using** 지시문을 추가합니다.

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    ```

1.  다음 코드를 입력하여 새 **Program** 클래스를 만듭니다.

    ```
    public class Program
    {
    }
    ``` 
    
1.  **Program** 클래스에서 다음 코드 줄을 입력하여 새 비동기 **Main** 메서드를 만듭니다.

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  **Program** 클래스에서 다음 코드 줄을 입력하여 **_clientId**라는 이름의 새 문자열 상수를 만듭니다.

    ```
    private const string _clientId = "";
    ```

1.  이 랩 앞부분에서 기록한 **_clientId** **애플리케이션(클라이언트) ID** 로 값을 설정하여 **clientId** 문자열 상수를 업데이트합니다.

1.  **Program** 클래스에서 다음 코드 줄을 입력하여 **_tenantId**라는 이름의 새 문자열 상수를 만듭니다.

    ```
    private const string _tenantId = "";
    ```

1.  이 랩 앞부분에서 기록한 디렉터리(테넌트) ID로 값을 설정하여 **_tenantId** 문자열 상수를 업데이트합니다.

1.  **Program.cs** 파일을 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```
    using Microsoft.Identity.Client;
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;

    public class Program
    {
        private const string _clientId = "<app-reg-client-id>";        
        private const string _tenantId = "<aad-tenant-id>";

        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### 작업 3: MSAL(Microsoft 인증 라이브러리) 토큰을 가져옵니다

1.  **Main** 메서드에서 다음 코드 줄을 추가하여 **[IPublicClientApplication](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.ipublicclientapplication)** 형식의 새 변수 *app*을 만듭니다.

    ```
    IPublicClientApplication app;
    ```

1.  **Main** 메서드에서 다음 작업을 수행하여 정적 **[PublicClientApplicationBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder)** 클래스를 사용해 공용 클라이언트 애플리케이션 인스턴스를 빌드한 다음 *app* 변수에 저장합니다.

    1.  정적 **[PublicClientApplicationBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder)** 클래스 액세스를 위해 다음 코드 줄을 추가합니다.

        ```
        PublicClientApplicationBuilder
        ```

    1.  **PublicClientApplicationBuilder** 클래스의 **[Create()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder.create)** 메서드를 사용하도록 다른 코드 줄을 추가하여 이전 코드 줄을 업데이트합니다. 이 메서드에는 *_clientId*를 매개 변수로 전달합니다.

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
        ```

    1.  기본 **[AbstractApplicationBuilder<>](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1)** 클래스의 **[WithAuthority()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1.withauthority)** 메서드를 사용하기 위해 다른 코드 줄을 추가하여 이전 코드 줄을 업데이트합니다. 이 메서드에는 열거 값 **[AzureCloudInstance.AzurePublic](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.azurecloudinstance)** 및 *_tenantId* 변수를 매개 변수로 전달합니다.

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
        ```

    1.  기본 **AbstractApplicationBuilder<>** 클래스의 **[WithRedirectUri()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1.withredirecturi)** 메서드를 사용하도록 다른 코드 줄을 추가하여 이전 코드 줄을 업데이트합니다. 이 메서드에는 문자열 값 **http://localhost** 를 전달합니다.

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
        ```

    1.  **PublicClientApplication** 클래스의 **[Build()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder.build)** 메서드를 사용하도록 다른 코드 줄을 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();
        ```

    1.  *app* 변수에 식의 결과를 저장하는 코드를 더 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();
        ```

1.  **Main** 메서드에서 다음 코드 줄을 추가하여 단일 값 **user.read**를 사용해 새 일반 문자열 **[List<>](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)** 를 만듭니다.

    ```
    List<string> scopes = new List<string> 
    { 
        "user.read" 
    };
    ```

1.  **Main** 메서드에서 다음 코드 줄을 추가하여 **[AuthenticationResult](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.authenticationresult)** 형식의 새 변수 *result*를 만듭니다.

    ```
    AuthenticationResult result;
    ```

1.  **Main** 메서드에서 다음 작업을 수행하여 토큰을 대화형으로 가져온 다음 *result* 변수에 출력을 저장합니다.

    1.  다음 코드 줄을 추가하여 *app* 변수에 액세스합니다.

        ```
        app
        ```

    1.  **IPublicClientApplicationBuilder** 인터페이스의 **[AcquireTokenInteractive()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.ipublicclientapplication.acquiretokeninteractive)** 메서드를 사용하도록 다른 코드 줄을 추가하여 이전 코드 줄을 업데이트합니다. 이 메서드에는 *scopes* 변수를 매개 변수로 전달합니다.

        ```
        app
            .AcquireTokenInteractive(scopes)
        ```

    1.  **[AbstractAcquireTokenParameterBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractacquiretokenparameterbuilder-1)** 클래스의 **[ExecuteAsync()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractacquiretokenparameterbuilder-1.executeasync)** 메서드를 사용하도록 다른 코드 줄을 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

    1.  **await** 키워드를 사용하여 식을 비동기식으로 처리하는 코드를 더 추가하여 이전 코드 줄을 업데이트합니다.
    
        ```
        await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

    1.  *result* 변수에 식의 결과를 저장하는 코드를 더 추가하여 이전 코드 줄을 업데이트합니다.
    
        ```
        result = await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

1.  **Main** 메서드에서 **Console.WriteLine** 메서드를 사용하여 **[AuthenticationResult.AccessToken](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.authenticationresult.accesstoken)** 멤버의 값을 콘솔에 렌더링하도록 다음 코드 줄을 추가합니다.

    ```
    Console.WriteLine($"Token:\t{result.AccessToken}");
    ```

1.  **Main** 메서드를 살펴봅니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read"
        };

        AuthenticationResult result;
        
        result = await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();

        Console.WriteLine($"Token:\t{result.AccessToken}");
    }
    ```

1.  **Program.cs** 파일을 저장합니다.

#### 작업 4: 업데이트된 애플리케이션 테스트

1.  Visual Studio Code 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 터미널에서 열기를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```
    dotnet run
    ```

    > **참고**: 빌드 오류가 있는 경우, **Allfiles (F):\\Allfiles\\Labs\\06\\Solution\\GraphClient** 폴더에 있는 **Program.cs** 파일을 검토하세요.

1.  실행 중인 콘솔 애플리케이션은 기본 브라우저의 인스턴스를 자동으로 엽니다.

1.  열린 브라우저 창에서 다음 작업을 수행합니다.

    1.  Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.

    1.  Microsoft 계정의 암호를 입력한 다음 로그인을 선택합니다.

    > **참고**: 다시 로그인하는 대신 기존 Microsoft 계정을 선택하는 옵션이 있을 수 있습니다.

1.  브라우저 창에서 **요청한 사용 권한** 웹 페이지가 자동으로 열립니다. 이 웹사이트에서 다음 작업을 수행합니다.

    1.  요청된 사용 권한을 검토합니다.

    1.  **수락**을 선택합니다.

1.  현재 실행 중인 Visual Studio Code 애플리케이션으로 돌아갑니다.

1.  현재 실행 중인 콘솔 애플리케이션의 출력에서 렌더링된 토큰을 관찰합니다.

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 복습

이 연습에서는 MSAL.NET 라이브러리를 사용하여 Microsoft ID 플랫폼에서 토큰을 획득했습니다.

### 연습 3: .NET SDK를 사용하여 Microsoft Graph를 쿼리합니다.

#### 작업 1: NuGet에서 Microsoft Graph SDK 가져오기

1.  Visual Studio Code 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 터미널에서 열기를 선택합니다.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 NuGet에서 **Microsoft.Graph**의 버전 1.21.0을 가져옵니다.

    ```
    dotnet add package Microsoft.Graph --version 1.21.0
    ```

    > **참고**: dotnet add package 명령은 NuGet에서 Microsoft.Graph 패키지를 추가합니다. 더 자세한 내용은 [Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/1.21.0)를 참조하십시오.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 NuGet에서 **Microsoft.Graph.Auth**의 버전 1.0.0-preview.2를 가져옵니다.

    ```
    dotnet add package Microsoft.Graph.Auth --version 1.0.0-preview.2
    ```

    > **참고**: dotnet add package 명령은 NuGet에서 Microsoft.Graph.Auth 패키지를 추가합니다. 더 자세한 내용은 [Microsoft.Graph.Auth](https://www.nuget.org/packages/Microsoft.Graph.Auth/1.0.0-preview.2)를 참조하세요.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 빌드합니다.

    ```
    dotnet build
    ```

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 작업 2: Program 클래스 수정

1.  Visual Studio Code 창의 탐색기 창에서 Program.cs 파일을 엽니다.

1.  **Program.cs** 파일의 코드 편집기 탭에서 다음 코드 줄을 추가하여 NuGet에서 가져온 **Microsoft.Graph** 패키지에서 **Microsoft.Graph** 네임스페이스를 가져옵니다.

    ```
    using Microsoft.Graph;
    ```
    
1.  다음 코드 줄을 추가하여 NuGet에서 가져온 **Microsoft.Graph.Auth** 패키지에서 **Microsoft.Graph.Auth** 네임스페이스를 가져옵니다.

    ```
    using Microsoft.Graph.Auth;
    ```

1.  **Program.cs** 파일을 살펴봅니다. 이제 파일에 다음 **using** 지시문이 포함되어 있어야 합니다.

    ```
    using Microsoft.Graph;    
    using Microsoft.Graph.Auth;
    using Microsoft.Identity.Client;
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    ```

#### 작업 3: Microsoft Graph SDK를 사용하여 사용자 프로필 정보 쿼리

1.  **Main** 메서드 내에서 다음 작업을 수행하여 불필요한 코드를 제거합니다.

    1.  다음 코드 줄을 삭제합니다.

        ```
        AuthenticationResult result;
        ```
    
    1.  다음 코드 블록을 삭제합니다.

        ```
        result = await app
                .AcquireTokenInteractive(scopes)
                .ExecuteAsync();
        ```
    
    1.  다음 코드 줄을 삭제합니다.

        ```
        Console.WriteLine($"Token:\t{result.AccessToken}");
        ```

1.  **Main** 메서드를 살펴봅니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read"
        };
    }
    ```

1.  **Main** 메서드에서 다음 코드 줄을 추가하여 *app* 및 *scopes*를 생성자 매개 변수로 전달하는 **DeviceCodeProvider** 형식의 새 변수 *provider*를 만듭니다.

    ```
    DeviceCodeProvider provider = new DeviceCodeProvider(app, scopes);
    ```

1.  **Main** 메서드에서 다음 코드 줄을 추가하여 변수 *provider*를 생성자 매개 변수로 전달하는 **GraphServiceClient** 형식의 새 변수 *client*를 만듭니다.

    ```
    GraphServiceClient client = new GraphServiceClient(provider);
    ```

1.  **Main** 메서드에서 다음 작업을 수행합니다. 이 작업에서는 **GraphServiceClient** 인스턴스를 사용하여 REST API의 상대 **/Me** 디렉터리를 대상으로 실행한 HTTP 요청의 응답을 비동기식으로 가져옵니다.

    1.  *client* 변수의 **Me** 속성을 가져오는 다음 코드 줄을 추가합니다.

        ```
        client.Me
        ```

    1.  **Request()** 메서드를 사용하여 HTTP 요청을 나타내는 개체를 가져오는 다른 코드 줄을 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        client.Me
            .Request()
        ```

    1.  **GetAsync()** 메서드를 사용하여 비동기식으로 요청을 실행하는 다른 코드 줄을 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        client.Me
            .Request()
            .GetAsync()
        ```

    1.  **await** 키워드를 사용하여 식을 비동기식으로 처리하는 코드를 더 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        await client.Me
            .Request()
            .GetAsync()
        ```

    1.  **User** 형식의 새 변수 *myProfile*에 식의 결과를 저장하는 코드를 더 추가하여 이전 코드 줄을 업데이트합니다.

        ```
        User myProfile = await client.Me
            .Request()
            .GetAsync();
        ```

1.  **Main** 메서드에서 **Console.WriteLine** 메서드를 사용하여 **User.DisplayName** 멤버의 값을 콘솔에 렌더링하도록 다음 코드 줄을 추가합니다.

    ```
    Console.WriteLine($"Name:\t{myProfile.DisplayName}");
    ```

1.  **Main** 메서드에서 **Console.WriteLine** 메서드를 사용하여 **User.Id** 멤버의 값을 콘솔에 렌더링하도록 다음 코드 줄을 추가합니다.

    ```
    Console.WriteLine($"AAD Id:\t{myProfile.Id}");
    ```

1.  **Main** 메서드를 살펴봅니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read" 
        };

        DeviceCodeProvider provider = new DeviceCodeProvider(app, scopes);

        GraphServiceClient client = new GraphServiceClient(provider);

        User myProfile = await client.Me
            .Request()
            .GetAsync();

        Console.WriteLine($"Name:\t{myProfile.DisplayName}");
        Console.WriteLine($"AAD Id:\t{myProfile.Id}");
    }
    ```

1.  **Program.cs** 파일을 저장합니다.

#### 작업 4: 업데이트된 애플리케이션 테스트

1.  Visual Studio Code 창에서 탐색기 창의 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭하거나 활성화한 다음 터미널에서 열기를 선택합니다.

1.  열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```
    dotnet run
    ```

    > **참고**: 빌드 오류가 있는 경우, **Allfiles (F):\\Allfiles\\Labs\\06\\Solution\\GraphClient** 폴더에 있는 **Program.cs** 파일을 검토하세요.

1.  현재 실행 중인 콘솔 애플리케이션의 출력에서 메시지를 살펴봅니다. 메시지에 코드 값을 기록합니다. 이 값은 랩에서 나중에 사용합니다.

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.

1.  열린 브라우저 창에서 <https://microsoft.com/devicelogin>로 이동합니다.

1.  **코드 입력** 웹 페이지에서 다음 작업을 수행합니다.

    1.  **코드** 텍스트 상자에 랩의 앞부분에서 복사한 코드 값을 입력합니다.

    1.  **다음**을 선택합니다.  

1.  로그인 웹 페이지에서 다음 작업을 수행합니다.

    1.  Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.

    1.  Microsoft 계정의 암호를 입력한 다음 로그인을 선택합니다.

    > **참고**: 다시 로그인하는 대신 기존 Microsoft 계정을 선택하는 옵션이 있을 수 있습니다.

1.  현재 실행 중인 Visual Studio Code 애플리케이션으로 돌아갑니다.

1.  현재 실행 중인 콘솔 애플리케이션에서 Microsoft Graph 요청의 출력을 살펴봅니다.

1.  터미널 종료 또는 휴지통 아이콘을 선택하여 현재 열려 있는 터미널 및 관련된 모든 작업을 종료합니다.

#### 복습

이 연습에서는 SDK 및 MSAL 기반 인증을 사용하여 Microsoft Graph를 쿼리했습니다.

### 연습 4: 구독 정리 

#### 작업 1: Azure AD에서 애플리케이션 등록 삭제

1.  Azure Portal을 사용하여 브라우저 창으로 돌아갑니다.

1.  Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.

1.  모든 서비스 블레이드에서 Azure Active Directory를 선택합니다.

1.  Azure Active Directory 블레이드의 관리 섹션에서 앱 등록을 선택합니다.

1.  **앱 등록** 섹션에서 이 랩의 앞부분에서 만든 **graphapp** Azure AD 애플리케이션 등록을 선택합니다.

1.  **graphapp** 섹션에서 다음 작업을 수행합니다.

    1.  **삭제**를 선택합니다.

    1.  확인 팝업 대화 상자에서 **예**를 선택합니다.

#### 작업 2: 활성 애플리케이션 닫기

1.  현재 실행 중인 Microsoft Edge 애플리케이션을 닫습니다.

1.  현재 실행 중인 Visual Studio Code 애플리케이션을 닫습니다.

#### 복습

이 연습에서는 이 랩에 사용된 애플리케이션 등록을 제거하여 구독을 정리했습니다.
