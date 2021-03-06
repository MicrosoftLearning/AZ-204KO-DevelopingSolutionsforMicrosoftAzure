---
lab:
    az204Title: '랩 12: Azure Content Delivery Network를 사용하여 웹 애플리케이션 향상'
    az204Module: '모듈 12: 솔루션 내에서 캐싱 및 콘텐츠 배달 통합'
    type: '해답'
---

# 랩 12: Azure Content Delivery Network를 사용하여 웹 애플리케이션 향상
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

Windows 10 데스크톱에서 작업 표시줄을 찾습니다. 작업 표시줄에 이 랩에서 사용할 애플리케이션의 아이콘이 포함되어 있습니다.
    
-   Microsoft Edge

### 연습 1: Azure 리소스 만들기

#### 작업 1: Azure Portal 열기

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 선택합니다.

1.  열려 있는 브라우저 창에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.

1.  Microsoft 계정의 전자 메일 주소를 입력하고 **다음**을 선택합니다.

1.  Microsoft 계정의 암호를 입력한 다음 **로그인**을 선택합니다.

    > **참고**: Azure Portal에 처음 로그인하는 경우 포털 둘러보기가 제공됩니다. 둘러보기를 건너뛰고 포털 사용을 시작하려면 **시작하기**를 선택합니다.


#### 작업 2: 스토리지 계정 만들기

1.  Azure Portal 탐색 창에서 **모든 서비스**를 선택합니다.

1.  **모든 서비스** 블레이드에서 **스토리지 계정**을 선택합니다.

1.  **스토리지 계정** 블레이드에서 스토리지 인스턴스 목록을 찾습니다.

1.  **스토리지 계정** 블레이드에서 **새로 만들기**를 선택합니다.

1.  **기본** 탭 등 **스토리지 계정 만들기** 블레이드에서 탭을 찾습니다.

    > **참고**: 각 탭은 새 스토리지 계정을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭에서 다음 작업을 수행합니다.
    
    1.  **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.

    1.  **리소스 그룹** 섹션에서 **새로 만들기**를 선택하고 **MarketingContent**를 입력한 다음 **확인**을 선택합니다.

    1.  **스토리지 계정 이름**텍스트 상자에 **contenthost[사용자 이름]** 을 입력합니다.

    1.  **위치** 드롭다운 목록에서 **(미국) 미국 동부** 지역을 선택합니다.

    1.  **성능** 섹션에서 **표준**을 선택합니다.

    1.  **계정 종류** 드롭다운 목록에서 **StorageV2(범용 v2)** 를 선택합니다.

    1.  **복제** 드롭다운 목록에서 **RA-GRS(읽기 액세스 지역 중복 스토리지)** 를 선택합니다.

    1.  **검토 + 만들기**를 선택합니다.

1.  **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 스토리지 계정을 만들려면 **만들기**를 선택합니다. 

    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.
    
#### 작업 3: Azure App Service를 사용하여 웹앱 만들기

1.  Azure Portal 탐색 창에서 **리소스 만들기**를 선택합니다.

1.  **새로 만들기** 블레이드에서 **Marketplace 검색** 텍스트 상자를 찾습니다.

1.  검색 상자에 **웹**을 입력하고 Enter 키를 누릅니다.

1.  **모든 항목** 검색 결과 블레이드에서 **웹앱** 결과를 선택합니다.

1.  **웹앱** 블레이드에서 **만들기**를 선택합니다.

1.  두 번째 **웹앱** 블레이드에서 **기본**과 같은 블레이드의 탭을 찾습니다.

    > **참고**: 각 탭은 새 웹앱을 만드는 워크플로의 단계를 나타냅니다. 언제든지 **검토 + 만들기**를 선택하여 나머지 탭을 건너뛸 수 있습니다.

1.  **기본** 탭에서 다음 작업을 수행합니다.
    
    1.  **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.
    
    1.  **리소스 그룹** 섹션에서 **MarketingContent**를 선택합니다.

    1.  **이름** 텍스트 상자에 **landingpage[사용자 이름]** 을/를 입력합니다.

    1.  **게시** 섹션에서 **Docker 컨테이너**를 선택합니다.

    1.  **운영 체제** 섹션에서 **Linux**를 선택합니다.

    1.  **지역** 드롭다운 목록에서 **미국 동부** 지역을 선택합니다.

    1.  **Linux 플랜(미국 동부)** 섹션에서 **새로 만들기**를 선택하고 **이름** 텍스트 상자에 **MarketingPlan** 값을 입력한 다음 **확인**을 선택합니다.

    1.  **SKU 및 크기** 섹션을 기본값으로 둡니다.

    1.  **다음: Docker**를 선택합니다.

1.  **Docker** 탭에서 다음 작업을 수행합니다.

    1.  **옵션** 드롭다운 목록에서 **단일 컨테이너**를 선택합니다.

    1.  **이미지 소스** 드롭다운 목록에서 **Docker Hub**를 선택합니다.

    1.  **액세스 형식** 드롭다운 목록에서 **공개**를 선택합니다.

    1.  **이미지 및 태그** 텍스트 상자에 **microsoftlearning/edx-html-landing-page:latest**를 입력합니다.

    1.  **검토 + 만들기**를 선택합니다.

1.  **검토 + 만들기** 탭에서 이전 단계에서 선택한 옵션을 검토합니다.

1.  지정된 구성을 사용하여 웹앱을 만들려면 **만들기**를 선택합니다. 

    > **참고**: 이 랩을 진행하기 전에 만들기 작업이 완료될 때까지 기다립니다.

1.  Azure Portal의 탐색 창에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 선택합니다.

1.  **MarketingContent** 블레이드에서 이 랩의 앞부분에서 만든 **landingpage[사용자 이름]** 웹앱을 선택합니다.

1.  **App Service** 블레이드의 **설정** 범주에서 **속성** 링크를 선택합니다.

1.  **속성** 섹션에서 **URL** 텍스트 상자의 값을 기록합니다. 이 값은 랩에서 나중에 사용합니다.

#### 복습

이 연습에서는 이 랩의 나중에 사용할 Azure Storage 계정과 Azure 웹앱을 만들었습니다.

### 연습 2: Content Delivery Network 및 엔드포인트 구성

#### 작업 1: Azure Cloud Shell 열기

1.  Azure Portal에서 **Cloud Shell** 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: **Cloud Shell**아이콘은 초과 기호 () 및 밑줄 문자(\_)로 표시됩니다.

1.  구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 **Azure Cloud Shell 시작 마법사**를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.
    
    -   셸을 구성하라는 메시지가 포함된 대화 상자가 나타납니다. **Bash**를 선택하고 선택한 구독을 검토한 다음 **스토리지 만들기**를 선택합니다. 

    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. **Cloud Shell**의 구성 옵션이 나타나지 않는 경우 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 수 있습니다. 랩은 새 구독을 사용한다는 가정 하에서 작성됩니다.

1.  포털의 **Cloud Shell** 명령 프롬프트에서 다음 명령을 입력한 다음 Enter 키를 선택하여 Azure CLI(Azure 명령줄 인터페이스) 도구의 버전을 가져옵니다.

    ```
    az --version
    ```

#### 작업 2: Microsoft.CDN 공급자 등록

1.  Portal의 **Cloud Shell** 명령 프롬프트에서 다음 작업을 수행합니다.

    1.  다음 명령을 입력하고 Enter 키를 눌러 Azure CLI의 루트 수준에서 하위 그룹 및 명령 목록을 가져옵니다.

        ```
        az --help
        ```

    1.  다음 명령을 입력한 다음 Enter 키를 눌러 리소스 공급자가 사용할 수 있는 명령 목록을 가져옵니다.

        ```
        az provider --help
        ```

    1.  다음 명령을 입력한 다음 Enter 키를 눌러 현재 등록된 모든 공급자를 나열합니다.

        ```
        az provider list
        ```

    1.  다음 명령을 입력한 다음 Enter 키를 눌러 현재 등록된 공급자의 네임스페이스만 나열합니다.

        ```
        az provider list --query "[].namespace"
        ```

    1.  현재 등록된 공급자 목록을 살펴봅니다. **Microsoft.CDN** 공급자는 현재 공급자 목록에 있지 않습니다.

    1.  다음 명령을 입력한 다음 Enter 키를 선택하여 새 공급자를 등록하는 데 필요한 플래그를 가져옵니다.

        ```
        az provider register --help
        ```

    1.  다음 명령을 입력한 다음 Enter 키를 선택한 후 현재 구독에 **Microsoft.CDN** 네임스페이스를 등록합니다.

        ```
        az provider register --namespace Microsoft.CDN
        ```

1.  포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: Content Delivery Network 프로필 만들기

1.  Azure Portal 탐색 창에서 **리소스 만들기**를 선택합니다.

1.  **새로 만들기** 블레이드에서 **Marketplace 검색** 텍스트 상자를 찾습니다.

1.  검색 상자에서 **CDN**을 입력한 다음 엔터를 선택합니다.

1.  **모두** 검색 결과 블레이드에서 **CDN** 결과를 선택합니다.

1.  **CDN** 블레이드에서 **만들기**를 선택합니다.

1.  **CDN 프로필** 블레이드에서 다음 작업을 수행합니다.

    1.  **이름** 텍스트 상자에 **contentdeliverynetwork**를 입력합니다.
    
    1.  **구독** 텍스트 상자의 값은 기본값으로 설정된 상태로 유지합니다.

    1.  **리소스 그룹** 섹션에서 **MarketingContent**를 선택합니다.
    
    1.  **리소스 그룹 위치** 드롭다운 목록을 기본값으로 둡니다.

    1.  **가격 책정 계층** 드롭다운 목록에서 **표준 Akamai**를 선택합니다.

    1.  **지금 새 CDN 엔드포인트 만들기** 체크 박스가 선택 해제되었는지 확인합니다.

    1.  **만들기**를 선택합니다.
  
    > **참고**: 랩을 진행하기 전에 Azure에서 CDN 프로필 만들기가 완료될 때까지 기다립니다. 앱을 만들 때 알림을 받게 됩니다.

#### 작업 4: 스토리지 컨테이너 구성

1.  Azure Portal의 탐색 창에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 선택합니다.

1.  **MarketingContent** 블레이드에서 이 랩의 앞부분에서 만든 **contenthost[사용자 이름]** 스토리지 계정을 선택합니다.

1.  **스토리지 계정** 블레이드에서 **Blob service** 섹션에 있는 **컨테이너** 링크를 선택합니다.

1.  **컨테이너** 섹션에서 **+ 컨테이너**를 선택합니다.

1.  **새 컨테이너** 팝업 창에서 다음 작업을 수행합니다.
    
    1.  **이름** 텍스트 상자에 **media**를 입력합니다.
    
    1.  **공용 액세스 수준** 드롭다운 목록에서 **Blob(Blob 전용 익명 읽기 권한)** 를 선택합니다. 
    
    1.  **만들기**를 선택합니다.

1.  **컨테이너** 섹션으로 가서 **+ 컨테이너**를 다시 선택합니다.

1.  **새 컨테이너** 팝업 창에서 다음 작업을 수행합니다.
    
    1.  **이름** 텍스트 상자에 **video**를 입력합니다.
    
    1.  **공용 액세스 수준** 드롭다운 목록에서 **Blob(Blob 전용 익명 읽기 권한)** 를 선택합니다. 
    
    1.  **만들기**를 선택합니다.

1.  업데이트된 컨테이너 목록을 살펴봅니다.

#### 작업 5: Content Delivery Network 엔드포인트 만들기

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 찾아서 선택합니다.

1.  **MarketingContent** 블레이드에서 이전에 랩에서 만든 **contentdeliverynetwork** CDN 프로필을 선택합니다.

1.  **CDN 프로필** 블레이드에서 **+ 엔드포인트**를 선택합니다.

1.  **엔드포인트 추가** 팝업 대화 상자에서 다음 작업을 수행합니다.

    1.  **이름** 텍스트 상자에 **cdnmedia[사용자 이름]** 을 입력합니다.

    1.  **원본 형식** 드롭다운 목록에서 **스토리지**를 선택합니다.

    1.  **원본 호스트 이름** 드롭다운 목록에서 이 랩의 앞부분에서 만든 스토리지 계정의 **contenthost[사용자 이름].blob.core.windows.net** 옵션을 선택합니다.

    1.  **원본 경로** 텍스트 상자에 **/media**를 입력합니다.

    1.  **원본 호스트 헤더** 텍스트 상자를 기본값으로 둡니다.

    1.  **프로토콜** 및 **원본 포트** 섹션을 기본값으로 둡니다.

    1.  **최적화 대상** 드롭다운 목록에서 **일반 웹 배달**을 선택합니다.

    1.  **추가**를 선택합니다.

1.  **CDN 프로필** 블레이드로 돌아가서 **+ 엔드포인트**를 다시 선택합니다.

1.  **엔드포인트 추가** 팝업 대화 상자에서 다음 작업을 수행합니다.

    1.  **이름** 텍스트 상자에 **cdnvideo[사용자 이름]** 을 입력합니다.

    1.  **원본 형식** 드롭다운 목록에서 **스토리지**를 선택합니다.

    1.  **원본 호스트 이름** 드롭다운 목록에서 이 랩의 앞부분에서 만든 스토리지 계정의 **contenthost[사용자 이름].blob.core.windows.net** 옵션을 선택합니다.

    1.  **원본 경로** 텍스트 상자에 **/video**를 입력합니다.

    1.  **원본 호스트 헤더** 텍스트 상자를 기본값으로 둡니다.

    1.  **프로토콜** 및 **원본 포트** 섹션을 기본값으로 둡니다.

    1.  **최적화 대상** 드롭다운 목록에서 **주문형 미디어 스트리밍 비디오**를 선택합니다.

    1.  **추가**를 선택합니다.

1.  **CDN 프로필** 블레이드로 돌아가서 **+ 엔드포인트**를 다시 선택합니다.

1.  **엔드포인트 추가** 팝업 대화 상자에서 다음 작업을 수행합니다.

    1.  **이름** 텍스트 상자에 **cdnweb[사용자 이름]** 을 입력합니다.

    1.  **원본 형식** 드롭다운 목록에서 **웹앱**을 선택합니다.

    1.  **원본 호스트 이름** 드롭다운 목록에서 이 랩의 앞부분에서 만든 웹앱의 **landingpage[사용자 이름].azurewebsites.net** 옵션을 선택합니다.

    1.  **원본 경로** 텍스트 상자를 기본값으로 둡니다.

    1.  **원본 호스트 헤더** 텍스트 상자를 기본값으로 둡니다.

    1.  **프로토콜** 및 **원본 포트** 섹션을 기본값으로 둡니다.

    1.  **최적화 대상** 드롭다운 목록에서 **일반 웹 배달**을 선택합니다.

    1.  **추가**를 선택합니다.

#### 복습

이 연습에서는 Content Delivery Network의 리소스 공급자를 등록하고 CDN 프로필과 엔드포인트 리소스를 모두 만드는 공급자를 사용했습니다.

### 연습 3: 정적 웹 콘텐츠 업로드 및 구성

#### 작업 1: 방문 페이지 살펴보기

1.  Azure Portal의 탐색 창에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 선택합니다.

1.  **MarketingContent** 블레이드에서 이 랩의 앞부분에서 만든 **landingpage[사용자 이름]** 웹앱을 선택합니다.

1.  **웹 서비스** 블레이드에서 **찾아보기**를 선택합니다. 새 브라우저 창 또는 탭이 열리고 현재 웹 사이트를 반환합니다.

1.  화면에 표시되는 오류 메시지를 살펴봅니다. 멀티미디어 콘텐츠를 참조하는 특정 설정을 구성할 때까지 웹 사이트가 작동하지 않습니다.

1.  Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

#### 작업 2: 저장소 Blob 업로드

1.  Azure Portal의 탐색 창에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 선택합니다.

1.  **MarketingContent** 블레이드에서 이 랩의 앞부분에서 만든 **contenthost[사용자 이름]** 스토리지 계정을 선택합니다.

1.  **스토리지 계정** 블레이드에서 **Blob service** 섹션에 있는 **컨테이너** 링크를 선택합니다.

1.  **컨테이너** 섹션에서 **미디어** 컨테이너를 선택합니다.

1.  **컨테이너** 블레이드에서 **업로드**를 선택합니다.

1.  **Blob 업로드** 팝업 창에서 다음 작업을 수행합니다.
    
    1.  **파일** 섹션에서 **폴더** 아이콘을 선택합니다.
    
    1.  **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\13\\Starter**로 이동하여 다음 파일을 선택하고 **열기**를 선택합니다.

        -   **campus.jpg**
        
        -   **conference.jpg**
        
        -   **poster.jpg**
    
    1.  **파일이 이미 있는 경우 덮어쓰기**가 선택되어 있는지 확인하고 **업로드**를 선택합니다.  

    > **참고**: 이 랩을 계속하기 전에 Blob이 업로드될 때까지 기다립니다.

1.  **컨테이너** 블레이드로 돌아가서 **설정** 섹션에 있는 **속성**을 선택합니다.

1.  **URL** 텍스트 상자에 값을 기록합니다. 이 값은 나중에 랩에서 사용합니다.

1.  **컨테이너** 블레이드를 닫습니다.

1.  **컨테이너** 블레이드로 돌아가서 **비디오** 컨테이너를 선택합니다.

1.  **컨테이너** 블레이드에서 **업로드**를 선택합니다.

1.  **Blob 업로드** 팝업 창에서 다음 작업을 수행합니다.
    
    1.  **파일** 섹션에서 **폴더** 아이콘을 선택합니다.
    
    1.  **파일 탐색기** 창에서 **Allfiles (F):\\Allfiles\\Labs\\13\\Starter**로 이동하여**welcome.mp4** 파일을 선택하고 **열기**를 선택합니다.
    
    1.  **파일이 이미 있는 경우 덮어쓰기**가 선택되어 있는지 확인하고 **업로드**를 선택합니다.  

    > **참고**: 이 랩을 계속하기 전에 Blob이 업로드될 때까지 기다립니다.

1.  **컨테이너** 블레이드로 돌아가서 **설정** 섹션에 있는 **속성**을 선택합니다.

1.  **URL** 텍스트 상자에 값을 기록합니다. 이 값은 나중에 랩에서 사용합니다.

#### 작업 3: 웹앱 설정 구성

1.  Azure Portal의 탐색 창에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 선택합니다.

1.  **MarketingContent** 블레이드에서 이 랩의 앞부분에서 만든 **landingpage[사용자 이름]** 웹앱을 선택합니다.

1.  **앱 서비스** 블레이드의 **설정** 범주에서 **구성** 링크를 선택합니다.

1.  **구성** 섹션에서 다음 작업을 수행합니다.
    
    1.  **애플리케이션 설정** 탭을 선택한 다음 **새 애플리케이션 설정**을 선택합니다.
    
    1.  **애플리케이션 설정 추가/편집** 팝업 창의 **이름** 텍스트 상자에 **CDNMediaEndpoint**를 입력합니다.
    
    1.  **값** 텍스트 상자에서 이 랩의 앞부분에서 기록한 **contenthost[사용자 이름]** 스토리지 계정에 **미디어** 컨테이너의 **URI** 값을 입력합니다.
    
    1.  **배포 슬롯 설정** 텍스트 상자를 기본값으로 두고, **확인**을 선택하여 팝업 창을 닫습니다.
    
    1.  **구성** 섹션으로 돌아가서 **새 애플리케이션 설정**을 선택합니다.
    
    1.  **애플리케이션 설정 추가/편집** 팝업 창의 **이름** 텍스트 상자에 **CDNVideoEndpoint**를 입력합니다.
    
    1.  **값** 텍스트 상자에 이전에 랩에서 기록한 **contenthost[사용자 이름]** 스토리지 계정에 **비디오** 컨테이너의 **URI** 값을 입력합니다.
    
    1.  **배포 슬롯 설정** 텍스트 상자를 기본값으로 두고, **확인**을 선택하여 팝업 창을 닫습니다.
    
    1.  **구성** 섹션으로 돌아가서 블레이드의 **저장**을 선택하여 설정을 유지합니다.  

    > **참고**: 랩을 진행하기 전에 애플리케이션 설정이 유지될 때까지 기다립니다.

#### 작업 4: 수정된 방문 페이지의 유효성 검사

1.  Azure Portal의 탐색 창에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 선택합니다.

1.  **MarketingContent** 블레이드에서 이 랩의 앞부분에서 만든 **landingpage[사용자 이름]** 웹앱을 선택합니다.

1.  **App Service** 블레이드에서 **다시 시작**을 선택합니다. 이 작업은 웹앱을 다시 시작합니다.

    > **참고**: 이 랩을 진행하기 전에 다시 시작 작업이 완료될 때까지 기다립니다. 작업이 완료되면 알림을 받습니다.

1.  **앱 서비스** 블레이드로 돌아가서 **찾아보기**를 선택합니다. 새 브라우저 창 또는 탭이 열리고 현재 웹 사이트를 반환합니다.

1.  다양한 유형의 멀티미디어 콘텐츠를 렌더링하는 업데이트된 웹 사이트를 살펴봅니다.

1.  Azure Portal을 표시하고 있고 현재 열려 있는 브라우저 창으로 돌아갑니다.

#### 복습

이 연습에서는 멀티미디어 콘텐츠를 스토리지 컨테이너에 Blob으로 업로드한 후 웹앱을 업데이트하여 스토리지 Blob을 직접 가리켰습니다.

### 연습 4: Content Delivery Network 끝점 사용

#### 작업 1: 끝점 URI 검색

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 찾아서 선택합니다.

1.  **MarketingContent** 블레이드에서 이전에 랩에서 만든 **contentdeliverynetwork** CDN 프로필을 선택합니다.

1.  **CDN 프로필** 블레이드에서 **cdnmedia[사용자 이름]** 끝점을 선택합니다.

1.  **엔드포인트** 블레이드에서 **엔드포인트 호스트 이름** 텍스트 상자의 값을 복사합니다. 이 값은 나중에 랩에서 사용합니다.

1.  **엔드포인트** 블레이드를 닫습니다.

1.  **CDN 프로필** 블레이드로 돌아가서 **cdnvideo[사용자 이름]** 끝점을 선택합니다.

1.  **엔드포인트** 블레이드에서 **엔드포인트 호스트 이름** 텍스트 상자의 값을 복사합니다. 이 값은 나중에 랩에서 사용합니다.

1.  **엔드포인트** 블레이드를 닫습니다.

#### 작업 2: 멀티미디어 콘텐츠 테스트

1.  랩의 앞부분에서 복사한 **cdnmedia[사용자 이름]** 끝점에서 **끝점 호스트 이름** URL을 **/campus.jpg**의 상대 경로와 결합하여 **campus.jpg** 리소스용 URL을 만듭니다.

    > **참고**: 예를 들어, **끝점 호스트 이름** URL이 **https://cdnmediastudent.azureedge.net/** 인 경우, 새로 만든 URL은 **https://cdnmediastudent.azureedge.net/campus.jpg** 가 됩니다.

1.  랩의 앞부분에서 복사한 **cdnmedia[사용자 이름]** 끝점에서 **끝점 호스트 이름** URL을 **/conference.jpg** 의 상대 경로와 결합하여 **conference.jpg** 리소스용 URL을 만듭니다.

    > **참고**: 예를 들어, **끝점 호스트 이름** URL이 **https://cdnmediastudent.azureedge.net/** 인 경우, 새로 만든 URL은 **https://cdnmediastudent.azureedge.net/conference.jpg** 가 됩니다.

1.  이전에 랩에서 복사한 **cdnmedia[사용자 이름]** 엔드포인트에서 **엔드포인트 호스트 이름** URL을 **/poster.jpg**의 상대 경로와 결합하여 **poster.jpg** 리소스용 URL을 구성합니다.

    > **참고**: 예를 들어, **엔드포인트 호스트 이름** URL이 **https://cdnmediastudent.azureedge.net/** 인 경우, 새로 만든 URL은 **https://cdnmediastudent.azureedge.net/poster.jpg** 가 됩니다.

1.  랩의 앞부분에서 복사한 **cdnmedia[사용자 이름]** 끝점에서 **끝점 호스트 이름** URL을 **/welcome.mp4**의 상대 경로와 결합하여**welcome.mp4** 리소스용 URL을 만듭니다.

    > **참고**: 예를 들어, **끝점 호스트 이름** URL이 **https://cdnvideostudent.azureedge.net/** 인 경우, 새로 만든 URL은 **https://cdnvideostudent.azureedge.net/welcome.mp4** 가 됩니다.

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 마우스 오른쪽 단추로 클릭하거나 바로 가기 메뉴를 활성화한 다음 **새 창**을 선택합니다.

1.  새 브라우저 창에서 **campus.jpg** 미디어 리소스용으로 구성한 URL로 이동한 다음 리소스를 성공적으로 찾았는지 확인합니다.

    > **참고**: 콘텐츠를 아직 사용할 수 없는 경우 CDN 끝점이 계속 초기화되고 있습니다. 이 초기화 작업은 5~15분 정도 걸릴 수 있습니다.

1.  **conference.jpg** 미디어 리소스용으로 만든 URL로 이동한 다음 리소스를 성공적으로 찾았는지 확인합니다.

1.  **poster.jpg** 미디어 리소스용으로 만든 URL로 이동한 다음 리소스를 성공적으로 찾았는지 확인합니다.

1.  **welcome.mp4** 비디오 리소스용으로 만든 URL로 이동한 다음 리소스를 성공적으로 찾았는지 확인합니다.

1.  이 작업에서 생성했던 브라우저 창을 닫습니다.

#### 작업 3: 웹앱 설정 업데이트

1.  Azure Portal의 탐색 창에서 **리소스 그룹**을 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 선택합니다.

1.  **MarketingContent** 블레이드에서 이 랩의 앞부분에서 만든 **landingpage[사용자 이름]** 웹앱을 선택합니다.

1.  **앱 서비스** 블레이드의 **설정** 범주에서 **구성** 링크를 선택합니다.

1.  **구성** 섹션에서 다음 작업을 수행합니다.
    
    1.  **애플리케이션 설정** 탭을 선택합니다.
    
    1.  기존의 **CDNMediaEndpoint** 애플리케이션 설정을 선택합니다.

    1.  **애플리케이션 설정 추가/편집** 팝업 대화 상자에서 랩의 앞부분에서 복사한 **cdnmedia[사용자 이름]** 엔드포인트에서 **엔드포인트 호스트 이름** URL을 입력하여 **값** 텍스트 상자를 업데이트한 후 **OK**를 선택합니다.
    
    1.  기존의 **CDNVideoEndpoint** 애플리케이션 설정을 선택합니다.

    1.  **애플리케이션 설정 추가/편집** 팝업 대화 상자에서 랩의 앞부분에서 복사한 **cdnvideo[사용자 이름]** 끝점에서 **끝점 호스트 이름** URL을 입력하여 **값** 텍스트 상자를 업데이트한 후 **확인**을 선택합니다.
    
    1.  블레이드 상단에 있는 **저장**을 선택하여 설정을 유지합니다.  

    > **참고**: 랩을 진행하기 전에 애플리케이션 설정이 유지될 때까지 기다립니다.

1.  **구성** 섹션으로 돌아가서 **개요**를 선택합니다.

1.  **개요** 섹션에서 **다시 시작**을 선택합니다. 이 작업은 웹앱을 다시 시작합니다.

    > **참고**: 이 랩을 진행하기 전에 다시 시작 작업이 완료될 때까지 기다립니다. 작업이 완료되면 알림을 받습니다.

#### 작업 4: 웹 콘텐츠를 테스트합니다.

1.  Azure Portal의 탐색 창에서 **리소스 그룹** 링크를 선택합니다.

1.  **리소스 그룹** 블레이드에서 이 랩의 앞부분에서 만든 **MarketingContent** 리소스 그룹을 찾아서 선택합니다.

1.  **MarketingContent** 블레이드에서 이전에 랩에서 만든 **contentdeliverynetwork** CDN 프로필을 선택합니다.

1.  **CDN 프로필** 블레이드에서 **cdnweb[사용자 이름]** 엔드포인트를 선택합니다.

1.  **엔드포인트** 블레이드에서 **엔드포인트 호스트 이름** 텍스트 상자의 값을 복사합니다.

1.  작업 표시줄에서 **Microsoft Edge** 아이콘을 마우스 오른쪽 단추로 클릭하거나 바로 가기 메뉴를 활성화한 다음 **새 창**을 선택합니다.

1.  새 브라우저 창에서 **cdnweb[사용자 이름]** 끝점용 **끝점 호스트 이름** URL로 이동합니다.

1.  Content Delivery Network를 사용하여 모두 제공되는 웹 사이트 및 멀티미디어 콘텐츠를 살펴봅니다.

#### 복습

이 연습에서는 Content Delivery Network를 사용하여 멀티미디어 콘텐츠를 제공하고 웹 애플리케이션 자체를 서비스하도록 웹앱을 업데이트했습니다.

### 연습 5: 구독 정리 

#### 작업 1: Azure Cloud Shell 열기 및 리소스 그룹 나열

1.  Azure Portal의 탐색 창에서 **Cloud Shell** 아이콘을 선택하여 새 셸 인스턴스를 엽니다.

    > **참고**: **Cloud Shell** 아이콘은 초과(\>) 기호와 밑줄 문자(\_)로 표시됩니다.

1.  구독을 사용하여 Cloud Shell을 처음으로 여는 경우, 처음 사용할 경우에만 **Azure Cloud Shell 시작 마법사**를 사용하여 Cloud Shell를 구성할 수 있습니다. 마법사에서 다음 작업을 수행합니다.
    
    1.  셸을 구성하라는 메시지가 포함된 대화 상자가 나타납니다. **Bash**를 선택하고 선택한 구독을 검토한 다음 **스토리지 만들기**를 선택합니다. 

    > **참고**: 랩으로 진행하기 전에 Cloud Shell이 초기 설치 절차를 완료할 때까지 기다립니다. Cloud Shell의 구성 옵션이 나타나지 않는 경우 이 과정의 랩에서 기존 구독을 사용하고 있기 때문일 가능성이 높습니다. 랩은 새 구독을 사용한다는 가정 하에서 작성됩니다.

#### 작업 2: 리소스 그룹 삭제

1.  다음 명령을 입력하고 Enter 키를 선택하여 **MarketingContent** 리소스 그룹을 삭제합니다.

    ```
    az group delete --name MarketingContent --no-wait --yes
    ```
    
1.  포털에서 Cloud Shell 창을 닫습니다.

#### 작업 3: 활성 애플리케이션 닫기

1.  현재 실행 중인 Microsoft Edge 애플리케이션.

#### 복습

이 연습에서는이 랩에 사용된 리소스 그룹을 제거하여 구독을 정리했습니다.
