---
lab:
    az204Title: '랩 11: Azure에 배포된 서비스 모니터링'
    az020Title: '랩 11: Azure에 배포된 서비스 모니터링'
    az204Module: '모듈 11: Azure 솔루션 모니터링 및 최적화'
    az020Module: '모듈 11: Azure 솔루션 모니터링 및 최적화'
    type: '해답'
---

# 랩 11: Azure에 배포된 서비스 모니터링
# 학생 랩 답변 키

## Microsoft Azure 사용자 인터페이스

Microsoft 클라우드 도구의 동적 특성을 감안할 때, 이 교육 콘텐츠를 개발한 후 Azure UI가 변경될 수 있습니다. 이러한 변경으로 인해 랩 지침 및 단계가 일치하지 않을 수 있습니다.

Microsoft는 커뮤니티에서 주목해야 할 변경 사항이 있을 때 이 학습 과정을 업데이트합니다. 그러나 클라우드 업데이트가 자주 이루어지기 때문에 이 학습 콘텐츠가 업데이트되기 전에 UI가 변경될 수 있습니다. **이 경우 변경 사항에 적응하고 필요에 따라 랩에서 작업합니다.**

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

-   파일 탐색기

-   Visual Studio Code

-   Windows PowerShell

### 연습 1: Azure 리소스 만들기 및 구성

#### 작업 1: Azure Portal 열기

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.

1.  열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.

1.  로그인 페이지에서 Microsoft 계정의 전자 메일 주소를 입력한 후 **다음**을 선택합니다.

1.  Microsoft 계정의 암호를 입력한 다음 로그인을 선택합니다.

> **참고**: Azure Portal에 처음 로그인하는 경우 대화 상자에 포털 둘러보기 제안이 표시됩니다. 둘러보기를 건너뛰고 포털 사용을 시작하려면 시작하기를 선택합니다.

#### 작업 2: Application Insights 리소스 만들기

1.  Azure Portal 탐색 창에서 **리소스 만들기**를 선택합니다.

1.  **새로 만들기** 블레이드에서 **Marketplace 검색** 텍스트 상자를 찾습니다.

1.  검색 상자에 **Insights**를 입력하고 Enter 키를 누릅니다.

1.  **Marketplace** 검색 결과 블레이드에서 **Application Insights** 결과를 선택합니다.

1.  **Application Insights** 블레이드에서 **만들기**를 선택합니다.

1.  두 번째 **Application Insights** 블레이드에서 **기본** 등의 탭을 찾습니다.

    > **참고**: 각 탭은 새 Application Insights 인스턴스를 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭에서 다음 작업을 수행합니다.
    
    1.  **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    
    1.  **리소스 그룹** 섹션에서 **새로 만들기**를 선택하고 **MonitoredAssets**를 입력한 다음 **확인**을 선택합니다.
    
    1.  **이름** 텍스트 상자에 **instrm[사용자 이름]** 을 입력합니다.
    
    1.  **지역** 드롭다운 목록에서 **(미국) 미국 동부** 지역을 선택합니다.
    
    1.  **리소스 모드** 섹션에서 **클래식** 옵션을 선택합니다.
    
    1.  **검토 + 만들기**를 선택합니다.

1.  **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 Application Insights 인스턴스를 만들려면 **만들기**를 선택합니다.   

    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

1.  Azure Portal의 탐색 창에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MonitoredAssets** 리소스 그룹을 선택합니다.

1.  **MonitoredAssets** 블레이드에서 이 랩의 앞부분에서 만든 **instrm[사용자 이름]** Application Insights 계정을 선택합니다.

1.  **Application Insights** 블레이드의 **구성** 범주에서 **속성** 링크를 선택합니다.

1.  **속성** 섹션에서 **계측 키** 텍스트 상자의 값을 확인합니다. 이 키는 클라이언트 애플리케이션에서 Application Insights에 연결하는 데 사용합니다.

#### 작업 3: Azure App Services 리소스를 사용하여 웹앱 만들기

1.  Azure Portal 탐색 창에서 **리소스 만들기**를 선택합니다.

1.  새로 만들기 블레이드에서 Marketplace 검색 텍스트 상자를 찾습니다.

1.  검색 상자에 **웹**을 입력하고 Enter 키를 누릅니다.

1.  **Marketplace** 검색 결과 블레이드에서 **웹앱** 결과를 선택합니다.

1.  **웹앱** 블레이드에서 **만들기**를 선택합니다.

1.  두 번째 **웹앱** 블레이드에서 **기본** 등의 탭을 찾습니다.

    > **참고**: 각 탭은 새 웹앱을 만드는 워크플로의 단계를 나타냅니다. 언제든지 검토 + 만들기를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  기본 탭에서 다음 작업을 수행합니다.
    
    1.  구독 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    
    1.  **리소스 그룹** 드롭다운 목록에서 **MonitoredAssets**를 선택합니다.
    
    1.  **이름** 텍스트 상자에 **smpapi[사용자 이름]** 을 입력합니다.

    1.  **게시** 섹션에서 **코드**를 선택합니다.

    1.  **런타임 스택** 드롭다운 목록에서 **.NET Core 3.1(LTS)** 을 선택합니다.

    1.  **운영 체제** 섹션에서 **Windows**를 선택합니다.

    1.  **지역** 드롭다운 목록에서 **미국 동부** 지역을 선택합니다.

    1.  **Windows 플랜(미국 동부)** 섹션에서 **새로 만들기**를 선택하고 **이름** 텍스트 상자에 **MonitoredPlan** 값을 입력한 다음 **확인**을 선택합니다.

    1.  **SKU 및 크기** 섹션을 기본값으로 둡니다.

    1.  **다음: 모니터링**을 선택합니다.

1.  **모니터링** 탭에서 다음 작업을 수행합니다.

    1.  **Application Insights 사용** 섹션에서 **예**를 선택합니다.

    1.  **Application Insights** 드롭다운 목록에서, 이 랩의 앞부분에서 만든 **instrm[사용자 이름]** Application Insights 계정을 선택합니다.

    1.  **검토 + 만들기**를 선택합니다.

1.  **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 웹앱을 만들려면 **만들기**를 선택합니다.   

    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

1.  Azure Portal의 탐색 창에서 리소스 그룹을 선택합니다.

1.  리소스 그룹 블레이드에서 이 랩의 앞부분에서 만든 MonitoredAssets 리소스 그룹을 선택합니다.

1.  **MonitoredAssets** 블레이드에서, 이 랩의 앞부분에서 만든 **smpapi[사용자 이름]** 웹앱을 선택합니다.

1.  **App Service** 블레이드의 **설정** 범주에서 **구성** 링크를 선택합니다.

1.  **구성** 섹션에서 다음 작업을 수행합니다.
    
    1.  **애플리케이션 설정** 탭을 선택합니다.

    1.  **값 표시**를 선택하여 API와 연결된 비밀을 가져옵니다.

    1.  **APPINSIGHTS\_INSTRUMENTATIONKEY** 키에 해당하는 값을 찾습니다. 이 값은 Web Apps 리소스를 빌드할 때 자동으로 설정되었습니다.

1.  **App Service** 블레이드의 **설정** 범주에서 **속성** 링크를 선택합니다.

1.  **속성** 섹션에서 **URL** 텍스트 상자의 값을 기록합니다. 이 값을 나중에 랩에서 사용하여 API에 대한 요청을 합니다.

#### 작업 4: 웹앱 자동 크기 조정 옵션 구성

1.  **App Service** 블레이드의 **설정** 범주에서 **확장(App Service 계획)** 링크를 선택합니다.

1.  **확장** 섹션에서 다음 작업을 수행합니다.
    
    1.  **사용자 지정 자동 크기 조정**을 선택합니다.
    
    1.  **자동 크기 조정 설정 이름** 텍스트 상자에 **ComputeScaler**를 입력합니다.
    
    1.  **리소스 그룹** 목록에서 **MonitoredAssets**을 선택합니다.
    
    1.  크기 조정 모드 섹션에서 메트릭에 따라 크기 조정을 선택합니다.
    
    1.  **인스턴스 제한** 섹션의 **최소값** 텍스트 상자에 **2**를 입력합니다.
    
    1.  **인스턴스 제한** 섹션의 **최대값** 텍스트 상자에 **8**을 입력합니다.
    
    1.  **인스턴스 제한** 섹션의 기본값 텍스트 상자에 **3**을 입력합니다.
    
    1.  **규칙 추가**를 선택합니다. **크기 조정 규칙** 팝업 대화 상자에서 모든 상자를 기본값으로 설정하고 **추가**를 선택합니다.
    
    1.  섹션 내에서 **저장**을 선택합니다. 

    > **참고**: 이 랩을 진행하기 전에 저장 작업이 완료될 때까지 기다립니다.

#### 복습

이 연습에서는 랩의 나머지 부분에 사용할 리소스를 만들었습니다.

### 연습 2: Application Insights를 사용하여 로컬 웹 애플리케이션 모니터링 

#### 작업 1: .NET 웹 API 프로젝트 빌드

1.  작업 표시줄에서 **Visual Studio Code** 아이콘을 선택합니다.

1.  **파일** 메뉴에서 **폴더 열기**를 선택합니다.

1.  **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\11\\Starter\\Api**로 이동하여 **폴더 선택**을 선택합니다.

1.  **Visual Studio Code** 창에서 탐색기 창을 마우스 오른쪽 단추로 클릭하거나 바로 가기 메뉴를 활성화한 다음 **터미널에서 열기**를 선택합니다.

1.  **열기** 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 현재 디렉터리에서 **SimpleApi**라는 새 .NET 웹 API 애플리케이션을 만듭니다.

    ```
    dotnet new webapi --output . --name SimpleApi
    ```

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 NuGet에서 현재 프로젝트로 **Microsoft.ApplicationInsights** 버전 2.14.0을 가져옵니다.

    ```
    dotnet add package Microsoft.ApplicationInsights --version 2.14.0
    ```

    > **참고**: **dotnet add package** 명령은 NuGet에서 **Microsoft.ApplicationInsights** 패키지를 추가합니다. 더 자세한 내용은 [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/2.14.0)로 이동하십시오.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 **NuGet에서 Microsoft.ApplicationInsights.AspNetCore**의 버전 2.14.0을 가져옵니다.

    ```
    dotnet add package Microsoft.ApplicationInsights.AspNetCore --version 2.14.0
    ```

    > **참고**: **dotnet add package** 명령은 NuGet에서 **Microsoft.ApplicationInsights.AspNetCore** 패키지를 추가합니다. 더 자세한 내용은 [Microsoft.ApplicationInsights.AspNetCore](https://www.nuget.org/packages/Microsoft.ApplicationInsights.AspNetCore/2.14.0)를 참조하세요.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 NuGet에서 현재 프로젝트로 **Microsoft.ApplicationInsights.PerfCounterCollector**의 버전 2.14.0을 가져옵니다.

    ```
    dotnet add package Microsoft.ApplicationInsights.PerfCounterCollector  --version 2.14.0
    ```

    > **참고**: **dotnet add package** 명령은 NuGet에서 **Microsoft.ApplicationInsights.PerfCounterCollector** 패키지를 추가합니다. 더 자세한 내용은 [Microsoft.ApplicationInsights.PerfCounterCollector](https://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector/2.14.0)를 참조하세요.


1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹앱을 빌드합니다.

    ```
    dotnet build
    ```
    
#### 작업 2: HTTPS를 사용하지 않도록 설정하고 Application Insights를 사용하여 애플리케이션 코드를 업데이트합니다.

1.  **Visual Studio Code** 창의 탐색기 창에서 **Startup.cs** 파일을 선택하여 편집기에서 파일을 엽니다.

1.  편집기에서 **Startup** 클래스의 39줄에 있는 다음 코드 줄을 찾아 삭제합니다.

    ```
    app.UseHttpsRedirection();
    ```

    > **참고**: 이 코드 줄은 웹앱이 HTTPS를 사용하도록 강제합니다. 이 랩에서는 필요가 없습니다.

1.  Startup 클래스 내에서, 이 랩의 앞에서 만든 Application Insights 리소스에서 복사한 계측 키로 값이 설정된 **INSTRUMENTATION_KEY**라는 새 정적 문자열 상수를 추가합니다.

    ```
    private const string INSTRUMENTATION_KEY = "{your_instrumentation_key}";
    ```

    > **참고**: 예를 들어 계측 키가 ``d2bb0eed-1342-4394-9b0c-8a56d21aaa43``이면 코드 줄은 ``private const string INSTRUMENTATION_KEY = "d2bb0eed-1342-4394-9b0c-8a56d21aaa43";``이 됩니다.

1.  **Startup** 클래스 내에서 **ConfigureServices** 메서드를 찾습니다.

    ```
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllers();
    }
    ```

1.  제공된 계측 키를 사용하여 Application Insights를 구성할 수 있도록 **ConfigureServices** 메서드 끝에 새 코드 줄을 추가합니다.

    ```    
    services.AddApplicationInsightsTelemetry(INSTRUMENTATION_KEY);
    ```

1.  **ConfigureServices** 메서드를 살펴봅니다. 이제 메서드에 다음 코드가 포함되어 있어야 합니다.

    ```
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllers();
        services.AddApplicationInsightsTelemetry(INSTRUMENTATION_KEY);        
    }
    ```

1.  Startup.cs 파일을 저장합니다.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET Core 웹 애플리케이션을 빌드합니다.

    ```
    dotnet build
    ```

#### 작업 3: API 애플리케이션 로컬 테스트

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 .NET 웹 애플리케이션을 실행합니다.

    ```
    dotnet run
    ```

1.  작업 표시줄에서 **Microsoft Edge** 아이콘의 컨텍스트 메뉴를 열고 새 브라우저 창을 엽니다.

1.  열린 브라우저 창에서 포트 5000의 localhost에서 호스팅되는 테스트 애플리케이션의 /weatherforecast 상대 경로로 이동합니다.
    
    > **참고**: 전체 URL은 http://localhost:5000/weatherforecast입니다.

1.  http://localhost:5000/weatherforecast 주소를 표시하는 브라우저 창을 닫습니다.

1.  현재 실행 중인 Visual Studio Code 애플리케이션을 닫습니다.

#### 작업 4: Application Insights 메트릭 보기

1.  Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

1.  Portal에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MonitoredAssets** 리소스 그룹을 찾아서 선택합니다.

1.  MonitoredAssets 블레이드에서 이 랩의 앞부분에서 만든 **instrm[사용자 이름]** Application Insights 계정을 선택합니다.

1.  블레이드 중앙에 있는 타일의 **Application Insights** 블레이드에서 표시된 메트릭을 찾습니다. 특히 발생한 서버 요청 수 및 평균 서버 응답 시간을 확인합니다.

    > **참고**: Application Insights 메트릭 차트에 요청이 표시되는 데 최대 5분이 걸릴 수 있습니다.

#### 복습

이 연습에서는 ASP.NET을 사용하여 API를 만들고 애플리케이션 메트릭을 Application Insights로 스트리밍하도록 구성했습니다. 다음 Application Insights 대시보드를 사용하여 API 에 대한 성능 세부 정보를 볼 수 있습니다.

### 연습 3: Application Insight를 사용해 웹앱을 모니터링합니다.

#### 작업 1: 웹앱에 애플리케이션 배포

1.  작업 표시줄에서 Visual Studio Code 아이콘을 선택합니다.

1.  파일 메뉴에서 폴더 열기를 선택합니다.

1.  파일 탐색기 창에서 **Allfiles (F):\\Allfiles\\Labs\\11\\Starter\\Api**로 이동하여 폴더 선택을 선택합니다.

1.  Visual Studio Code 창에서 탐색기 창을 마우스 오른쪽 단추로 클릭하거나 바로 가기 메뉴를 활성화한 다음 **터미널에서 열기**를 선택합니다.

1.  열린 명령 프롬프트에 다음 명령을 입력하고 Enter 키를 눌러 Azure CLI(명령줄 인터페이스)에 로그인합니다.

    ```
    az login
    ```

1.  브라우저 창에서 다음 작업을 수행합니다.
    
    1.  Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.
    
    1.  Microsoft 계정의 암호를 입력한 다음 로그인을 선택합니다.

1.  현재 열려 있는 명령 프롬프트 애플리케이션으로 돌아갑니다.  

    > **참고**: 로그인 프로세스가 완료될 때까지 기다립니다.

1.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 **MonitoredAssets** 리소스 그룹의 모든 앱을 나열합니다.

    ```
    az webapp list --resource-group MonitoredAssets
    ```

1.  다음 명령을 입력하고 Enter 키를 눌러 접두사가 **smpapi\*** 인 앱을 찾습니다.

    ```
    az webapp list --resource-group MonitoredAssets --query "[?starts_with(name, 'smpapi')]"
    ```

1.  다음 명령을 입력하고 Enter 키를 눌러 **smpapi\*** 가 있는 단일 앱의 이름만 렌더링합니다.

    ```
    az webapp list --resource-group MonitoredAssets --query "[?starts_with(name, 'smpapi')].{Name:name}" --output tsv
    ```

1.  다음 명령을 입력하고 Enter 키를 눌러 현재 디렉터리를 배포 파일이 포함된 **Allfiles (F):\\Allfiles\\Labs\\11\\Starter** 디렉터리로 변경합니다.

    ```
    cd F:\Allfiles\Labs\12\Starter\
    ```

1.  다음 명령을 입력하고 Enter 키를 눌러 이 랩의 앞부분에서 만든 웹앱에 **api.zip** 파일을 배포합니다.

    ```
    az webapp deployment source config-zip --resource-group MonitoredAssets --src api.zip --name <name-of-your-api-app>
    ```

    > **참고**: *name-of-your-api-app* 자리 표시자를 이 랩의 앞부분에서 만든 웹앱의 이름으로 바꿉니다. 최근에 이전 단계에서 이 앱의 이름을 쿼리했습니다.   

    > **참고**: 이 랩을 진행하기 전에 배포가 완료될 때까지 기다립니다.

1.  현재 실행 중인 Visual Studio Code 애플리케이션을 닫습니다.

1.  Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

1.  Azure Portal의 탐색 창에서 리소스 그룹을 선택합니다.

1.  리소스 그룹 블레이드에서 이 랩의 앞부분에서 만든 MonitoredAssets 리소스 그룹을 선택합니다.

1.  MonitoredAssets 블레이드에서, 이 랩의 앞부분에서 만든 **smpapi[사용자 이름]** 웹앱을 선택합니다.

1.  **App Service** 블레이드에서 **찾아보기**를 선택합니다. 새 브라우저 창 또는 탭이 열리고 "404(찾을 수 없음)" 오류가 반환됩니다.

1.  브라우저 주소 표시줄에서 현재 URL의 끝에 **/weatherforecast** 접미사를 추가하여 URL을 업데이트하고 Enter 키를 누릅니다.

    > **참고**: 예를 들어 URL이 https://smpapistudent.azurewebsites.net 이 경우 새 URL은 https://smpapistudent.azurewebsites.net/weatherforecast 가 됩니다.

1.  API를 사용한 결과로 반환되는 JSON(JavaScript Object Notation) 배열을 찾습니다.

#### 작업 2: Web Apps에 대한 심층 메트릭 컬렉션 구성

1.  Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

1.  Azure Portal의 탐색 창에서 리소스 그룹을 선택합니다.

1.  리소스 그룹 블레이드에서 이 랩의 앞부분에서 만든 MonitoredAssets 리소스 그룹을 선택합니다.

1.  MonitoredAssets 블레이드에서, 이 랩의 앞부분에서 만든 **smpapi[사용자 이름]** 웹앱을 선택합니다.

1.  **App Service** 블레이드에서 **Application Insights**를 선택합니다.

1.  **Application Insights** 블레이드에서 다음 작업을 수행합니다.

    1.  **Application Insights** 섹션이 **사용**으로 설정되어 있는지 확인합니다.

    1.  **애플리케이션 계측** 섹션에서 **.NET** 탭을 선택합니다.

    1.  **컬렉션 수준** 섹션에서 **추천**을 선택합니다.

    1.  **프로파일러** 섹션에서 **켜짐**을 선택합니다.

    1.  **스냅샷 디버거** 섹션에서 **꺼짐**을 선택합니다.

    1.  **SQL 명령** 섹션에서 **꺼짐**을 선택합니다.

    1.  **적용**을 선택합니다.

    1.  확인 대화 상자에서 **예**를 선택합니다.

1.  **Application Insights** 블레이드를 닫습니다.

1.  **App Service** 블레이드로 돌아가서 **찾아보기**를 선택합니다. 새 브라우저 창 또는 탭이 열리고 "404(찾을 수 없음)" 오류가 반환됩니다.

1.  브라우저 주소 표시줄에서 현재 URL의 끝에 /weatherforecast 접미사를 추가하여 URL을 업데이트하고 Enter 키를 누릅니다.

    > **참고**: 예를 들어 URL이 https://smpapistudent.azurewebsites.net 이 경우 새 URL은 https://smpapistudent.azurewebsites.net/weatherforecast 가 됩니다.

1.  API를 사용하여 반환되는 JSON 배열을 관찰합니다.

1.  JSON 배열에 액세스하는 데 사용한 URL을 기록합니다.

    > **참고**: 이전 단계의 예제를 사용하는 경우 기록하는 URL은 ``https://smpapistudent.azurewebsites.net/weatherforecast``가 됩니다.

#### 작업 3: Application Insights에서 업데이트된 메트릭 가져오기

1.  Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

1.  Portal에서 리소스 그룹을 선택합니다.

1.  리소스 그룹 블레이드에서 이 랩의 앞부분에서 만든 MonitoredAssets 리소스 그룹을 찾아서 선택합니다.

1.  MonitoredAssets 블레이드에서 이 랩의 앞부분에서 만든 **instrm[사용자 이름]** Application Insights 계정을 선택합니다.

1.  블레이드 중앙에 있는 타일의 Application Insights 블레이드에서 표시된 메트릭을 찾습니다. 특히 발생한 서버 요청 수 및 평균 서버 응답 시간을 확인합니다.

    > **참고**: Application Insights 메트릭 차트에 요청이 표시되는 데 최대 5분이 걸릴 수 있습니다.

#### 작업 4: Application Insights에서 실시간 메트릭 보기

1.  Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

1.  Portal에서 리소스 그룹을 선택합니다.

1.  리소스 그룹 블레이드에서 이 랩의 앞부분에서 만든 MonitoredAssets 리소스 그룹을 찾아서 선택합니다.

1.  MonitoredAssets 블레이드에서 이 랩의 앞부분에서 만든 **instrm[사용자 이름]** Application Insights 계정을 선택합니다.

1.  **Application Insights** 블레이드의 **조사** 섹션에서 **라이브 메트릭 스트림**을 선택합니다.

1.  작업 표시줄에서 Microsoft Edge 아이콘의 컨텍스트 메뉴를 열고 새 브라우저 창을 엽니다.

1.  새 브라우저 창에서 이 랩의 앞부분에서 복사한 URL로 이동합니다.

1.  JSON 배열 결과를 관찰합니다.

1.  Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

1.  업데이트된 **라이브 메트릭 스트림** 블레이드를 관찰합니다.

    > **참고**: **들어오는 요청** 섹션은 초 단위로 업데이트되어 웹앱에 대한 요청을 표시해야 합니다.

#### 복습

이 연습에서는 웹 애플리케이션을 Azure App Service에 배포하고 동일한 Application Insights 인스턴스에서 메트릭을 모니터링했습니다.

### 연습 4: 구독 정리 

#### 작업 1: Azure Cloud Shell 열기

1.  Azure Portal에서 Cloud Shell 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: **Cloud Shell** 아이콘은 더 큼 기호(\>)와 밑줄 문자(\_)로 표시됩니다.

1.  구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 **Azure Cloud Shell 시작 마법사**를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.
    
    1.  셸을 구성하라는 메시지가 포함된 대화 상자가 나타납니다. **Bash**를 선택하고 선택한 구독을 검토한 다음 **스토리지 만들기**를 선택합니다. 

    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. Cloud Shell의 구성 옵션이 나타나지 않는 경우 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 수 있습니다. 랩은 새 구독을 사용한다는 가정 하에서 작성됩니다.

#### 작업 2: 리소스 그룹 삭제

1.  다음 명령을 입력하고 Enter 키를 눌러 MonitoredAssets 리소스 그룹을 삭제합니다.

    ```
    az group delete --name MonitoredAssets --no-wait --yes
    ```
    
1.  포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: 활성 애플리케이션 닫기

1.  현재 실행 중인 Microsoft Edge 애플리케이션을 닫습니다.

1.  현재 실행 중인 Visual Studio Code 애플리케이션을 닫습니다.

#### 복습

이 연습에서는 이 랩에 사용된 리소스 그룹을 제거하여 구독을 정리했습니다.
