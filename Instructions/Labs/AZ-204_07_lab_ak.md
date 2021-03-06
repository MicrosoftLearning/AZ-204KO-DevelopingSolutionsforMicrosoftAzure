---
lab:
    az204Title: '랩 07: 서비스 전반에서 리소스 비밀에 보다 안전하게 액세스'
    az020Title: '랩 07: 서비스 전반에서 리소스 비밀에 보다 안전하게 액세스'
    az204Module: '모듈 07: 보안 클라우드 솔루션 구현'
    az020Module: '모듈 07: 보안 클라우드 솔루션 구현'
    type: '해답'
---

# 랩 07: 서비스 전반에서 리소스 비밀에 보다 안전하게 액세스
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
1. 열려 있는 브라우저 창에서 **Azure Portal**(<https://portal.azure.com>)로 이동합니다.
1. Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.
1. Microsoft 계정의 **암호**를 입력한 다음 **로그인**을 선택합니다.
    > **참고**: Azure Portal에 처음 로그인하는 경우 포털 둘러보기 기능이 제공됩니다. 둘러보기를 건너뛰고 Portal 사용을 시작하려면 **시작하기**를 선택합니다.

#### 작업 2: Azure Storage 계정 만들기

1. Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.
1. **모든 서비스** 블레이드에서 **스토리지 계정**을 선택합니다.
1. **스토리지 계정** 블레이드에서 스토리지 인스턴스 목록을 확인합니다.
1. **스토리지 계정** 블레이드에서 **새로 만들기**를 선택합니다.
1. **스토리지 계정 만들기** 블레이드에서 **기본** 등의 탭을 찾습니다.
    > **참고**: 각 탭은 새 스토리지 계정을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.
1. **기본** 탭에서 다음 작업을 수행합니다.
    1. **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **리소스 그룹** 섹션에서 **새로 만들기**를 선택하고 **ConfidentialStack**을 입력한 다음 **확인**을 선택합니다.
    1. **스토리지 계정 이름** 텍스트 상자에 **securestor[사용자 이름]** 을 입력합니다.
    1. **위치** 드롭다운 목록에서 **(미국) 미국 동부** 지역을 선택합니다.
    1. **성능** 섹션에서 **표준**을 선택합니다.
    1. **계정 종류** 드롭다운 목록에서 **StorageV2(범용 v2)** 를 선택합니다.
    1. **복제** 드롭다운 목록에서 **LRS(로컬 중복 스토리지)** 를 선택합니다.
    1. **검토 + 만들기**를 선택합니다.
1. **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.
1. 지정된 구성을 사용하여 스토리지 계정을 만들려면 **만들기**를 선택합니다.
    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.
1. Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.
1. **모든 서비스** 블레이드에서 **스토리지 계정**을 선택합니다.
1. **스토리지 계정** 블레이드에서 이 랩의 앞부분에서 만든 **securestor[사용자 이름]** 스토리지 계정을 선택합니다.
1. **스토리지 계정** 블레이드에서 **설정** 섹션을 찾은 다음 **액세스 키** 링크를 선택합니다.
1. **액세스 키** 블레이드에서 키 중 하나를 선택하고 **연결 문자열** 상자 중 하나의 값을 기록합니다. 나중에 이 랩에서 이 값을 사용하게 됩니다.
    > **참고**: 어떤 연결 문자열을 선택하든 상관없습니다. 서로 교환할 수 있습니다.

#### 작업 3: Azure Key Vault 만들기

1. Azure Portal의 탐색 창에서 **리소스 만들기** 링크를 선택합니다.
1. **새로 만들기** 블레이드에서 주요 서비스 목록 위의 **Marketplace 검색** 텍스트 상자를 찾습니다.
1. 검색 상자에 **자격 증명 모음**을 입력하고 Enter 키를 누릅니다.
1. **Marketplace** 검색 결과 블레이드에서 **키 자격 증명 모음** 결과를 선택합니다.
1. **키 자격 증명 모음** 블레이드에서 **만들기**를 선택합니다.
1. **키 자격 증명 모음 만들기** 블레이드에서 **기본** 등의 탭을 찾습니다.
    > **참고**: 각 탭은 새 키 자격 증명 모음을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.
1. **기본** 탭에서 다음 작업을 수행합니다.
    1. **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **리소스 그룹** 섹션에서 **기존 항목 사용**을 선택한 다음 목록에서 **ConfidentialStack**을 선택합니다.
    1. **키 자격 증명 모음 이름** 텍스트 상자에 **securevault[사용자 이름]** 을 입력합니다.
    1. **지역** 드롭다운 목록에서 **미국 동부** 지역을 선택합니다.
    1. **가격 책정 계층** 드롭다운 목록에서 **표준**을 선택합니다.
    1. **검토 + 만들기**를 선택합니다.
1. **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.
1. 지정된 구성을 사용하여 키 자격 증명 모음을 만들려면 **만들기**를 선택합니다.
    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

#### 작업 4: Azure Functions 앱 만들기

1. Azure Portal의 탐색 창에서 **리소스 만들기** 링크를 선택합니다.
1. **새로 만들기** 블레이드에서 주요 서비스 목록 위의 **Marketplace 검색** 텍스트 상자를 찾습니다.
1. 검색 상자에 **함수**를 입력하고 Enter 키를 누릅니다.
1. **Marketplace** 검색 결과 블레이드에서 **함수 앱** 결과를 선택합니다.
1. **함수 앱** 블레이드에서 **만들기**를 선택합니다.
1. **함수 앱** 블레이드에서 **기본** 등의 탭을 찾습니다.
    > **참고**: 각 탭은 새 함수 앱을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.
1. **기본** 탭에서 다음 작업을 수행합니다.
    1. **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **리소스 그룹** 섹션에서 **기존 항목 사용**을 선택한 다음 목록에서 **ConfidentialStack**을 선택합니다.
    1. **함수 앱 이름** 텍스트 상자에 **securefunc[사용자 이름]** 을 입력합니다.
    1. **게시** 섹션에서 **코드**를 선택합니다.
    1. **런타임 스택** 드롭다운 목록에서 **.NET**을 선택합니다.
    1. **버전** 드롭다운 목록에서 **3.1**을 선택합니다.
    1. **지역** 드롭다운 목록에서 **미국 동부** 지역을 선택합니다.
    1. **다음: 호스팅**을 선택합니다.
1. **호스팅** 탭에서 다음 작업을 수행합니다.
    1. **운영 체제** 섹션에서 **Linux**를 선택합니다.
    1. **스토리지 계정** 드롭다운 목록에서 이 랩의 앞부분에서 만든 **securestor[사용자 이름]** 스토리지 계정을 선택합니다.
    1. **계획 유형** 드롭다운 목록에서 **사용(서버리스)** 옵션을 선택합니다.
    1. **검토 + 만들기**를 선택합니다.
1. **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.
1. 지정된 구성을 사용하여 함수 앱을 만들려면 **만들기**를 선택합니다.
    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

> **복습**: 이 연습에서는 이 랩에 사용할 모든 리소스를 만들었습니다.

### 연습 2: 비밀 및 ID 구성

#### 작업 1: 시스템이 할당한 관리 서비스 ID 구성

1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **ConfidentialStack** 리소스 그룹을 찾아 선택합니다.
1. **ConfidentialStack** 블레이드에서 이 랩의 앞부분에서 만든 **securefunc[사용자 이름]** 함수 앱을 선택합니다.
1. **App Service** 블레이드의 **설정** 섹션에서 **ID** 옵션을 선택합니다.
1. **ID** 창에서 **시스템 할당** 탭을 찾아 다음 작업을 수행합니다.
    1. **상태** 섹션에서 **켜기**를 선택한 다음 **저장**을 선택합니다.
    1. 확인 대화 상자에서 **예**를 선택합니다.
    > **참고**: 이 랩을 진행하기 전에 할당된 시스템에서 관리 ID가 만들어질 때까지 기다립니다.

#### 작업 2: Key Vault 비밀 만들기

1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **ConfidentialStack** 리소스 그룹을 찾아 선택합니다.
1. **ConfidentialStack** 블레이드에서 이 랩의 앞부분에서 만든 **securevault[사용자 이름]** 키 자격 증명 모음을 선택합니다.
1. **키 자격 증명 모음** 블레이드에서 **설정** 섹션에 있는 **비밀** 링크를 선택합니다.
1. **비밀** 창에서 **생성/가져오기**를 클릭합니다.
1. **비밀 만들기** 블레이드에서 다음 작업을 수행합니다.
    1. **업로드 옵션** 드롭다운 목록에서 **수동**을 선택합니다.
    1. **이름** 텍스트 상자에 **storagecredentials**를 입력합니다.
    1. **값** 텍스트 상자에 이 랩 앞부분에서 기록한 스토리지 계정 연결 문자열을 입력합니다.
    1. **콘텐츠 형식** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **활성화 날짜 설정** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **만료 날짜 설정** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **사용** 섹션에서 **예**를 선택한 다음 **만들기**를 선택합니다.
    > **참고**: 이 랩을 진행하기 전에 비밀이 만들어질 때까지 기다립니다.
1. 비밀 창으로 돌아가서 목록의 **storagecredentials** 항목을 선택합니다.
1. 버전 창에서 **storagecredentials** 비밀의 최신 버전을 선택합니다.
1. 비밀 버전 창에서 다음 작업을 수행합니다.
    1. 최신 버전의 비밀에 대한 메타데이터를 찾습니다.
    1. 비밀 값을 보려면 **비밀 값 표시**를 선택합니다.
    1. 나중에 랩에서 이 값을 사용하기 때문에 **비밀 식별자** 텍스트 상자의 값을 기록합니다.
    > **참고**: **비밀 값** 텍스트 상자가 아닌 **비밀 식별자** 텍스트 상자의 값을 기록해야 합니다.

#### 작업 3: Key Vault 액세스 정책 구성

1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **ConfidentialStack** 리소스 그룹을 찾아 선택합니다.
1. **ConfidentialStack** 블레이드에서 이 랩의 앞부분에서 만든 **securevault[사용자 이름]** 키 자격 증명 모음을 선택합니다.
1. **키 자격 증명 모음** 블레이드에서 **설정** 섹션에 있는 **액세스 정책** 링크를 선택합니다.
1. 액세스 정책 창에서 **액세스 정책 추가**를 선택합니다.
1. **액세스 정책 추가** 블레이드에서 다음 작업을 수행합니다.
    1. **주체 선택** 링크를 선택합니다.
    1. **주체** 블레이드에서 **securefunc[사용자 이름]** 서비스 주체를 찾아 선택한 다음 **선택**을 선택합니다.
        > **참고**: 이 랩의 앞에서 만든 시스템 할당 관리 ID는 Azure Function 리소스와 이름이 동일합니다.
    1. **키 권한** 목록의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **비밀 권한** 드롭다운 목록에서 **GET** 권한을 선택합니다.
    1. **인증서 권한** 목록의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **권한 있는 애플리케이션** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **추가**를 선택합니다.
1. 액세스 정책 창으로 돌아가서 **저장**을 선택합니다.
    > **참고**: 이 랩을 진행하기 전에 액세스 정책에 대한 변경 내용이 저장될 때까지 기다립니다.

#### 작업 4: Key Vault 파생 애플리케이션 설정 만들기

1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **ConfidentialStack** 리소스 그룹을 찾아 선택합니다.
1. **ConfidentialStack** 블레이드에서 이 랩의 앞부분에서 만든 **securefunc[사용자 이름]** 함수 앱을 선택합니다.
1. **App Service** 블레이드의 **설정** 섹션에서 **구성** 옵션을 선택합니다.
1. **구성** 창에서 다음 작업을 수행합니다.
    1. **애플리케이션 설정** 탭을 선택한 다음 **새 애플리케이션 설정**을 선택합니다.
    1. **애플리케이션 설정 추가/편집** 팝업 창의 **이름** 텍스트 상자에 **StorageConnectionString**을 입력합니다.
    1. **값** 텍스트 상자에서 ``@Microsoft.KeyVault(SecretUri=*Secret Identifier*)`` 구문을 사용하여 값을 생성합니다.
        > **참고**: 위의 구문을 사용하여 ***비밀 식별자***에 대한 참조를 빌드해야 합니다. 예를 들어, 비밀 식별자가 ``https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf``인 경우 값은 ``@Microsoft.KeyVault(SecretUri=https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf)``가 됩니다.
    1. **배포 슬롯 설정** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    1. **확인**을 선택하여 팝업 창을 닫고 **구성** 섹션으로 돌아갑니다.
    1. 블레이드에서 **저장**을 선택하여 설정을 저장합니다.  
    1. **변경 내용 저장** 확인 팝업 대화 상자에서 **계속**을 선택합니다.
    > **참고**: 랩을 진행하기 전에 애플리케이션 설정이 저장될 때까지 기다립니다.

> **복습**: 이 연습에서는 함수 앱에 대한 시스템 할당 관리 서비스 ID를 만든 다음 해당 ID에 키 자격 증명 모음에서 비밀 값을 얻을 수 있는 적절한 권한을 부여했습니다. 마지막으로 비밀을 만들어 함수 앱 구성 설정 내에서 참조했습니다.

### 연습 3: Azure Functions 앱 빌드

#### 작업 1: 함수 프로젝트 초기화

1. 작업 표시줄에서 Windows 터미널 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다. 이 명령은 **Azure Functions Core Tools**를 사용하여 **dotnet** 런타임을 통해 현재 디렉터리에 새 로컬 Functions 프로젝트를 만듭니다.

    ```powershell
    func init --worker-runtime dotnet --force
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [새 프로젝트 만들기][azure-functions-core-tools-new-project] 방법을 파악할 수 있습니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 .NET Core 3.1 프로젝트를 **빌드**합니다.

    ```powershell
    dotnet build
    ```

#### 작업 2: HTTP 트리거 함수 만들기

1. 계속해서 열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다. 이 명령은 **Azure Functions Core Tools**를 사용하여 **HTTP 트리거** 템플릿을 통해 새 함수 **FileParser**를 만듭니다.

    ```powershell
    func new --template "HTTP trigger" --name "FileParser"
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [새 함수 만들기][azure-functions-core-tools-new-function] 방법을 파악할 수 있습니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

#### 작업 3: 애플리케이션 설정 구성 및 읽기

1. **시작** 화면에서 **Visual Studio Code** 타일을 선택합니다.
1. **파일** 메뉴에서 **폴더 열기**를 선택합니다.
1. 열리는 **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func**로 이동한 후 **폴더 선택**을 선택합니다.
1. **Visual Studio Code** 창의 탐색기 창에서 **local.settings.json** 파일을 엽니다.
1. **Values** 개체의 현재 값을 살펴봅니다.

    ```json
    "Values": {
        "AzureWebJobsStorage": "UseDevelopmentStorage=true",
        "FUNCTIONS_WORKER_RUNTIME": "dotnet"
    }
    ```

1. 새 설정 **StorageConnectionString**을 추가한 다음 문자열 값 **[TEST VALUE]** 로 설정하여 **Values** 개체 값을 업데이트합니다.

    ```json
    "Values": {
        "AzureWebJobsStorage": "UseDevelopmentStorage=true",
        "FUNCTIONS_WORKER_RUNTIME": "dotnet",
        "StorageConnectionString": "[TEST VALUE]"
    }
    ```

1. 이제 **local.settings.json** 파일에 다음 코드가 포함되어 있어야 합니다.

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "FUNCTIONS_WORKER_RUNTIME": "dotnet",
            "StorageConnectionString": "[TEST VALUE]"
        }
    }
    ```

1. **Visual Studio Code** 창의 탐색기 창에서 **FileParser.cs** 파일을 엽니다.
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
        public static class FileParser
        {
            [FunctionName("FileParser")]
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

1. **FileParser.cs** 파일 내의 모든 내용을 삭제합니다.
1. 다음 코드 줄을 추가하여 **Microsoft.AspNetCore.Mvc**, **Microsoft.Azure.WebJobs**, **Microsoft.AspNetCore.Http**, **System** 및 **System.Threading.Tasks** 네임스페이스에 **using 지시문**을 추가합니다.

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;
    ```

1. 새 **public static** 클래스 **FileParser**를 만듭니다.

    ```csharp
    public static class FileParser
    { }
    ```

1. **FileParser.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    { }
    ```

1. **FileParser** 클래스 내에서 다음 코드 블록을 추가하여 새 **public static** *asynchronous* 메서드 **Run**을 만듭니다. 이 메서드는 **Task\<IActionResult\>** 유형 변수를 반환하며, **HttpRequest** 유형 변수 *request*를 가져옵니다.

    ```csharp
    public static async Task<IActionResult> Run(
        HttpRequest request)
    { }
    ```

1. 다음 코드를 추가하여 **name** 매개 변수가 **FileParser** 값으로 설정된 **FunctionNameAttribute** 유형 특성을 **Run** 메서드에 추가합니다.

    ```csharp
    [FunctionName("FileParser")]
    public static async Task<IActionResult> Run(
        HttpRequest request)
    { }
    ```

1. 다음 코드를 추가하여 **methods** 매개 변수 배열이 단일 값 **GET**으로 설정된 **HttpTriggerAttribute** 유형 특성을 **request** 매개 변수에 추가합니다.

    ```csharp
    [FunctionName("FileParser")]
    public static async Task<IActionResult> Run(
        [HttpTrigger("GET")] HttpRequest request)
    { }
    ```

1. **FileParser.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        { }
    }
    ```

1. **Run** 메서드에서 다음 코드 줄을 입력하여 **StorageConnectionString** 애플리케이션 설정의 값을 검색합니다. 이렇게 하려면 **Environment.GetEnvironmentVariable** 메서드를 사용하고, 메서드가 반환하는 결과를 **string** 변수 **connectionString**에 저장합니다.

    ```csharp
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1. **connectionString** 변수의 값을 HTTP 응답으로 반환하는 다음 코드 줄을 입력합니다.

    ```csharp
    return new OkObjectResult(connectionString);
    ```

1. **FileParser.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        {
            string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
            return new OkObjectResult(connectionString);
        }
    }
    ```

1. **저장**을 선택하여 **FileParser.cs** 파일의 변경 내용을 저장합니다.

#### 작업 4: 로컬 함수 유효성 검사

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 함수 앱 프로젝트를 실행합니다.

    ```powershell
    func start --build
    ```

    > **참고**: 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [로컬에서 함수 앱 프로젝트 시작][azure-functions-core-tools-start-function] 방법을 파악할 수 있습니다.
1. 작업 표시줄에서 **Windows 터미널** 아이콘을 다시 선택하여 Windows 터미널 애플리케이션의 새 인스턴스를 엽니다.
1. 명령 프롬프트가 열리면 다음 명령을 입력하고 Enter 키를 눌러 **httprepl** 도구를 시작합니다. 기본 URI(Uniform Resource Identifier)는 ``http://localhost:7071``로 설정합니다.

    ```powershell
    httprepl http://localhost:7071
    ```

    > **참고**: httprepl 도구에서 오류 메시지가 표시됩니다. 이 메시지는 도구가 API를 "통과"하는 데 사용할 Swagger 정의 파일을 검색하기 때문에 발생합니다. 함수 프로젝트는 Swagger 정의 파일을 생성하지 않으므로 API를 수동으로 통과해야 합니다.
1. 도구 프롬프트가 표시되면 다음 명령을 입력하고 Enter 키를 눌러 상대 **api** 디렉터리를 찾습니다.

    ```powershell
    cd api
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 상대 **fileparser** 디렉터리를 찾습니다.

    ```powershell
    cd fileparser
    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 **get** 명령을 실행합니다.

    ```powershell
    get
    ```

1. HTTP 요청 결과로 반환되는 **StorageConnectionString**의 **[TEST VALUE]** 값을 살펴봅니다.

    ```powershell
    HTTP/1.1 200 OK
    Content-Type: text/plain; charset=utf-8
    Date: Tue, 01 Sep 2020 23:35:39 GMT
    Server: Kestrel
    Transfer-Encoding: chunked

    [TEST VALUE]

    ```

1. 다음 명령을 입력하고 Enter 키를 눌러 **httprepl** 애플리케이션을 종료합니다.

    ```powershell
    exit
    ```

1. 현재 실행 중인 **Windows 터미널** 애플리케이션의 모든 인스턴스를 닫습니다.

#### 작업 5: Azure Functions Core Tools를 사용하여 배포

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 열린 명령 프롬프트에 다음 명령을 입력하고 Enter 키를 눌러 Azure CLI(명령줄 인터페이스)에 로그인합니다.

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

    > **참고**: 예를 들어 **함수 앱 이름**이 **securefuncstudent**이면 ``func azure functionapp publish securefuncstudent`` 명령을 실행합니다. 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [로컬 함수 앱 프로젝트 게시][azure-functions-core-tools-publish-azure] 방법을 파악할 수 있습니다.
1. 랩을 진행하기 전에 배포가 마무리될 때까지 기다립니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.

#### 작업 6: Key Vault 파생 애플리케이션 설정 테스트

1. 작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.
1. 열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.
1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **ConfidentialStack** 리소스 그룹을 찾아 선택합니다.
1. **ConfidentialStack** 블레이드에서 이 랩의 앞부분에서 만든 **securefunc[사용자 이름]** 함수 앱을 선택합니다.
1. **App Service** 블레이드에서 **Functions** 섹션의 **Functions** 옵션을 선택합니다.
1. **Functions** 창에서 기존 **FileParser** 함수를 선택합니다.
1. **함수** 블레이드의 **개발자** 섹션에서 **코드 + 테스트** 옵션을 선택합니다.
1. 함수 편집기에서 **테스트/실행**을 선택합니다.
1. 표시되는 팝업 대화 상자에서 다음 작업을 수행합니다.
    - **HTTP 메서드** 목록에서 **GET**을 선택합니다.
1. **실행**을 선택하여 함수를 테스트합니다.
1. 테스트 실행 결과를 관찰합니다. Azure Storage 연결 문자열이 결과에 포함되어 있어야 합니다.

> **복습**: 이 연습에서는 서비스 ID를 사용하여 Key Vault에 저장된 비밀의 값을 읽고 함수 앱의 결과로 해당 값을 반환했습니다.

### 연습 4: Azure Blob Storage 데이터 액세스

#### 작업 1: 샘플 Storage Blob 업로드

1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **ConfidentialStack** 리소스 그룹을 찾아 선택합니다.
1. **ConfidentialStack** 블레이드에서 이 랩의 앞부분에서 만든 **securestor[사용자 이름]** 스토리지 계정을 선택합니다.
1. **스토리지 계정** 블레이드에서 **Blob service** 섹션에 있는 **컨테이너** 링크를 선택합니다.
1. **컨테이너** 섹션에서 **+ 컨테이너**를 선택합니다.
1. **새 컨테이너** 팝업 창에서 다음 작업을 수행합니다.
    1. **이름** 텍스트 상자에 **drop**을 입력합니다.
    1. **공용 액세스 수준** 드롭다운 목록에서 **Blob(Blob에 대해서만 익명 읽기 액세스)** 을 선택하고 **만들기**를 선택합니다.
1. **컨테이너** 섹션으로 돌아가서 새로 만든 **drop** 컨테이너를 선택합니다.
1. **컨테이너** 블레이드에서 **업로드**를 선택합니다.
1. **Blob 업로드** 팝업 창에서 다음 작업을 수행합니다.
    1. **파일** 섹션에서 **폴더** 아이콘을 선택합니다.
    1. **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\07\\Starter**로 이동하여 **records.json** 파일을 선택한 다음 **열기**를 선택합니다.
    1. **파일이 이미 있는 경우 덮어쓰기**가 선택되어 있는지 확인하고 **업로드**를 선택합니다.  
    > **참고**: 이 랩을 계속하기 전에 Blob이 업로드될 때까지 기다립니다.
1. **컨테이너** 블레이드로 돌아가서 Blob 목록에서 **records.json** Blob을 선택합니다.
1. **Blob** 블레이드에서 Blob 메타데이터를 찾은 다음 Blob의 URL을 복사합니다.
1. 작업 표시줄에서 **Microsoft Edge** 아이콘을 마우스 오른쪽 단추로 클릭하거나 바로 가기 메뉴를 활성화한 다음 **새 창**을 선택합니다.
1. 새 브라우저 창에서 blob에 대해 복사한 URL로 이동합니다.
1. 이제 Blob의 JSON(JavaScript Object Notation) 내용이 표시되어야 합니다. JSON 내용을 표시하는 브라우저 창을 닫습니다.
1. Azure Portal이 표시된 브라우저 창으로 돌아가서 **Blob** 블레이드를 닫습니다.
1. **컨테이너** 블레이드로 돌아가서 **액세스 수준 정책 변경**을 선택합니다.
1. **액세스 수준 변경** 팝업 창에서 다음 작업을 수행합니다.
    1. **공용 액세스 수준** 드롭다운 목록에서 **비공개(익명 액세스 없음)** 를 선택합니다.
    1. **확인**을 선택합니다.
1. 작업 표시줄에서 **Microsoft Edge** 아이콘을 마우스 오른쪽 단추로 클릭하거나 바로 가기 메뉴를 활성화한 다음 **새 창**을 선택합니다.
1. 새 브라우저 창에서 blob에 대해 복사한 URL로 이동합니다.
1. 이제 리소스를 찾을 수 없다는 오류 메시지가 표시됩니다.
    > **참고**: 오류 메시지가 표시되지 않으면 브라우저에서 파일을 캐시했을 수 있습니다. 이 경우에는 Ctrl+F5를 눌러 오류 메시지가 표시될 때까지 페이지를 새로 고칩니다.

#### 작업 2: .NET용 Azure SDK 끌어오기 및 구성

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 열린 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 NuGet에서 **Azure.Storage.Blobs** 패키지의 버전 **12.6.0**을 가져옵니다.

    ```powershell
    dotnet add package Azure.Storage.Blobs --version 12.6.0
    ```

    > **참고**: [Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs/12.6.0) NuGet 패키지는 Azure Blob Storage용 코드를 작성하는 데 필요한 .NET용 Azure SDK의 하위 집합을 참조합니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.
1. **시작** 화면에서 **Visual Studio Code** 타일을 선택합니다.
1. **파일** 메뉴에서 **폴더 열기**를 선택합니다.
1. 열리는 파일 탐색기 창에서 **Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func**로 이동한 후 **폴더 선택**을 선택합니다.
1. **Visual Studio Code** 창의 탐색기 창에서 **FileParser.cs** 파일을 엽니다.
1. **Azure.Storage.Blobs** 네임스페이스에 **using 지시문**을 추가합니다.

    ```csharp
    using Azure.Storage.Blobs;
    ```

1. **FileParser.cs** 파일을 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Azure.Storage.Blobs;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        {
            string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
            return new OkObjectResult(connectionString);
        }
    }
    ```

#### 작업 3: .NET용 Azure SDK를 사용하여 Azure Blob Storage 코드 작성

1. **FileParser** 클래스의 **Run** 메서드 내에서 다음 코드 줄을 삭제합니다.

    ```csharp
    return new OkObjectResult(connectionString);
    ```

1. 계속해서 **Run** 메서드 내에서 다음 코드 블록을 추가하여 **BlobClient** 클래스의 새 인스턴스를 만듭니다. 이렇게 하려면 *connectionString* 변수, ``"drop"`` 문자열 값 및 ``"records.json"`` 문자열 값을 생성자에 전달합니다.

    ```csharp
    BlobClient blob = new BlobClient(connectionString, "drop", "records.json");
    ```

1. 계속해서 **Run** 메서드 내에서 다음 코드 블록을 추가합니다. 이 코드 블록은 **BlobClient.DownloadAsync** 메서드를 사용하여 참조된 Blob의 내용을 비동기적으로 다운로드하고 결과를 *response* 변수에 저장합니다.

    ```csharp
    var response = await blob.DownloadAsync();
    ```

1. 계속해서 **Run** 메서드 내에서 다음 코드 블록을 추가합니다. 이 코드 블록은 **FileStreamResult** 클래스 생성자를 사용하여 **content** 변수에 저장된 다양한 콘텐츠의 값을 반환합니다.

    ```csharp
    return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    ```

1. **FileParser.cs** 파일을 다시 살펴봅니다. 이제 파일에 다음 코드가 포함되어 있어야 합니다.

    ```csharp
    using Azure.Storage.Blobs;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        {
            string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
            BlobClient blob = new BlobClient(connectionString, "drop", "records.json");
            var response = await blob.DownloadAsync();
            return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
        }
    }
    ```

1. **저장**을 선택하여 **FileParser.cs** 파일의 변경 내용을 저장합니다.

#### 작업 4: Azure Functions 앱 배포 및 유효성 검사

1. 작업 표시줄에서 **Windows 터미널** 아이콘을 선택합니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 현재 디렉터리를 빈 디렉터리 **Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func**로 변경합니다.

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 열린 명령 프롬프트에 다음 명령을 입력한 후 Enter 키를 눌러 Azure CLI에 로그인합니다.

    ```powershell
    az login
    ```

1. **Microsoft Edge** 브라우저 창에서 다음 작업을 수행합니다.
    1. Microsoft 계정의 전자 메일 주소를 입력하고 다음을 선택합니다.
    1. Microsoft 계정의 암호를 입력한 다음 **로그인**을 선택합니다.
1. 현재 열려 있는 **Windows 터미널** 창으로 돌아갑니다. 로그인 프로세스가 완료될 때까지 기다립니다.
1. 다음 명령을 입력한 후 Enter 키를 눌러 함수 앱 프로젝트를 다시 게시합니다.

    ```powershell
    func azure functionapp publish <function-app-name>
    ```

    > **참고**: 예를 들어 **함수 앱 이름**이 **securefuncstudent**이면 ``func azure functionapp publish securefuncstudent`` 명령을 실행합니다. 설명서의 내용을 검토하여 **Azure Functions Core Tools**를 사용한 [로컬 함수 앱 프로젝트 게시][azure-functions-core-tools-publish-azure] 방법을 파악할 수 있습니다.
1. 랩을 진행하기 전에 배포가 마무리될 때까지 기다립니다.
1. 현재 실행 중인 **Windows 터미널** 애플리케이션을 닫습니다.
1. 작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.
1. 열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.
1. Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.
1. **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **ConfidentialStack** 리소스 그룹을 찾아 선택합니다.
1. **ConfidentialStack** 블레이드에서 이 랩의 앞부분에서 만든 **securefunc[사용자 이름]** 함수 앱을 선택합니다.
1. **App Service** 블레이드에서 **Functions** 섹션의 **Functions** 옵션을 선택합니다.
1. **Functions** 창에서 기존 **FileParser** 함수를 선택합니다.
1. **함수** 블레이드의 **개발자** 섹션에서 **코드 + 테스트** 옵션을 선택합니다.
1. 함수 편집기에서 **테스트/실행**을 선택합니다.
1. 표시되는 팝업 대화 상자에서 다음 작업을 수행합니다.
    - **HTTP 메서드** 목록에서 **GET**을 선택합니다.
1. **실행**을 선택하여 함수를 테스트합니다.
1. 테스트 실행 결과를 관찰합니다. 출력에는 스토리지 계정에 저장된 **$/drop/records.json** Blob의 내용이 포함됩니다.

> **복습**: 이 연습에서는 C\# 코드를 사용하여 스토리지 계정에 액세스한 다음 Blob의 내용을 다운로드했습니다.

### 연습 5: 구독 정리

#### 작업 1: Azure Cloud Shell 열기 및 리소스 그룹 나열

1. Azure Portal의 탐색 창에서 **Cloud Shell** 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: Cloud Shell 아이콘은 더 큼 기호(\>)와 밑줄 문자(\_)로 표시됩니다.

1. 구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 **Azure Cloud Shell 시작 마법사**를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.

    1. 셸을 구성하라는 메시지가 포함된 대화 상자가 나타납니다. **Bash**를 선택하고 선택한 구독을 검토한 다음 **스토리지 만들기**를 선택합니다.

    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. Cloud Shell 구성 옵션이 표시되지 않는 경우, 대부분은 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 수 있습니다. 랩은 새 구독을 사용 한다는 가정에서 작성됩니다.

#### 작업 2: 리소스 그룹 삭제

1. 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 눌러 **ConfidentialStack** 리소스 그룹을 삭제합니다.

    ```powershell
    az group delete --name ConfidentialStack --no-wait --yes
    ```

1. 포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: 활성 애플리케이션 닫기

1. 현재 실행 중인 Microsoft Edge 애플리케이션을 닫습니다.

> **복습**: 이 연습에서는 이 랩에 사용된 리소스 그룹을 제거하여 구독을 정리했습니다.
