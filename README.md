# UE5 스타일 가이드 (ver. VLAST)

<br>

[ue5-style-guide](https://github.com/Allar/ue5-style-guide#structure-assettypes)를 기반으로 작성되었으며, 기존 VLAST 스타일 가이드와 아래의 자료들을 참고해 변형되었습니다.

>[UE4 코딩표준](https://docs.unrealengine.com/4.26/ko/ProductionPipelines/DevelopmentSetup/CodingStandard/)  
[POCU 아카데미용 C# 코딩 표준](https://docs.popekim.com/ko/coding-standards/pocu-csharp)  
[POCU 아카데미용 C++ 코딩 표준](https://docs.popekim.com/ko/coding-standards/pocu-cpp)  
[언리얼 엔진 마켓플레이스 가이드라인](https://www.unrealengine.com/ko/marketplace-guidelines?sessionInvalidated=true)  
[Recommended Asset Naming Conventions](https://docs.unrealengine.com/4.27/ko/ProductionPipelines/AssetNaming/)  
[LyraStarterGame 샘플 프로젝트](https://www.unrealengine.com/marketplace/en-US/product/lyra)  
메가스캔 폴더 디렉터리 구조

<br>
<br>

## **목차**
- [**중요한 용어들**](#중요한-용어들)
  - [맵(map)과 레벨(level)](#맵map과-레벨level)
  - [명명 규칙 종류](#명명-규칙-종류)
  - [변수(Variable)와 프로퍼티(Property)](#변수variable와-프로퍼티property))
    - [프로퍼티(Property)](#프로퍼티-property)
    - [변수(Variable)](#변수-variable)
  - [접근 제어자 (Access Modifier)](#접근-제어자-access-modifier)
    - [Public](#public)
    - [protected](#protected)
    - [private](#private)
  - [오류와 버그](#오류와-버그)
- [**00. 원칙들**](#00-원칙들)
  - [00.1 당신이 기존에 어떤 스타일을 가지고 있었든, VLAST 소속의 UE 작업자는 모두 이 스타일 가이드를 따라 작업해야 합니다.](#001-당신이-기존에-어떤-스타일을-가지고-있었든-vlast-소속의-ue-작업자는-모두-이-스타일-가이드를-따라-작업해야-합니다)
  - [00.2 프로젝트는 아무리 많은 사람이 참여했다 하더라도, 이 스타일 가이드에 따라 모두 한 사람이 작업한 것처럼 보여야 합니다.](#002-프로젝트는-아무리-많은-사람이-참여했다-하더라도-이-스타일-가이드에-따라-모두-한-사람이-작업한-것처럼-보여야-합니다)
  - [00.3 스타일 가이드를 지키지 않는 팀원을 그대로 내버려두어선 안됩니다.](#003-스타일-가이드를-지키지-않는-팀원을-그대로-내버려두어선-안됩니다)
- [**01. 금지된 사항들**](#01-금지된-사항들)
  - [01.1 금지된 문자](#011-금지된-문자)
- [**02. 엔진 기본 Config 설정**](#02-엔진-기본-config-설정)
  - [02.1 BaseEngine.ini](#021-baseengineini)
    - [02.1.1 공유 DCC 설정](#0211-공유-dcc-설정)
  - [02.2 BaseEditorPerProjectUserSettings.ini](#022-baseeditorperprojectusersettingsini)
    - [02.2.1 Developers 폴더 사용 편의를 위한 설정](#0221-developers-폴더-사용-편의를-위한-설정)
    - [02.2.2 블루프린트 코딩 표준 준수를 위한 설정](#0222-블루프린트-코딩-표준-준수를-위한-설정)
- [**1. 에셋 명명 규칙**](#1-에셋-명명-규칙)
  - [1.1 에셋명 기본 형식: `접두사_기본에셋명_세부변형_접미사`](#11-에셋명-기본-형식-접두사_기본에셋명_세부변형_접미사)
    - [1.1 에셋 명명 예](#11의-예시들)
  - [1.2 에셋 접두사 & 접미사 테이블](#12-에셋-접두사--접미사-테이블)
    - [1.2.1 흔히 사용되는 에셋](#121-흔히-사용되는-에셋)
    - [1.2.2 애니메이션 (Animations)](#122-애니메이션-animations)
    - [1.2.3 인공 지능 (Artificial Intelligence)](#123-인공-지능-artificial-intelligence)
    - [1.2.4 블루프린트 (Blueprints)](#124-블루프린트-blueprints)
    - [1.2.5 머티리얼 (Materials)](#125-머티리얼-materials)
    - [1.2.6 텍스처 (Textures)](#126-텍스처-textures)
      - [1.2.6.1 패킹된 텍스처 (Texture Packing)](#1261-패킹된-텍스처-texture-packing)
    - [1.2.7 기타 (Miscellaneous)](#127-기타-miscellaneous)
    - [1.2.8 페이퍼 2D (Paper 2D)](#128-페이퍼-2d-paper-2d)
    - [1.2.9 피직스 (Physics)](#129-피직스-physics)
    - [1.2.10 사운드 (Sounds)](#1210-사운드-sounds)
    - [1.2.11 유저 인터페이스 (User Interface)](#1211-유저-인터페이스-user-interface)
    - [1.2.12 FX](#1212-fx)
    - [1.2.13 미디어 (Media)](#1213-미디어-media)
- [**2. Content 폴더 디렉터리 구조**](#2-content-폴더-디렉터리-구조)
  - [2.0 Content 폴더 디렉터리 구조 예제](#20-content-폴더-디렉터리-구조-예제)
  - [2.1 폴더명 규칙](#21-폴더명-규칙)
    - [2.1.1 항상 파스칼 케이스(PascalCase)를 사용할 것](#211-항상-파스칼-케이스pascalcase를-사용할-것)
    - [2.1.2 공백(스페이스바)을 사용하지 말 것](#212-공백스페이스바을-사용하지-말-것)
    - [2.1.3 영문과 숫자 이외의 문자(특수문자 포함)를 사용하지 말 것](#213-영문과-숫자-이외의-문자특수문자-포함를-사용하지-말-것)
  - [2.2 최상위 폴더 규칙](#22-최상위-폴더-규칙)
    - [2.2.1 최상위 폴더 바깥에 에셋을 두어선 안됩니다.](#221-최상위-폴더-바깥에-에셋을-두어선-안됩니다)
    - [2.2.2 최상위 폴더 규칙은 이주 충돌을 감소시켜줍니다.](#222-최상위-폴더-규칙은-이주-충돌을-감소시켜줍니다)
      - [2.2.2.1 마스터 머티리얼 이주 충돌 예시](#2221-마스터-머티리얼-이주-충돌-예시)
    - [2.2.3 최상위 폴더 규칙을 준수하는 샘플, 템플릿, 마켓플레이스 콘텐츠는 폴더 구조를 수정하지 않습니다.](#223-최상위-폴더-규칙을-준수하는-샘플-템플릿-마켓플레이스-콘텐츠는-폴더-구조를-수정하지-않습니다)
    - [2.2.4 다른 프로젝트로 자주 이주될 수 있는 에셋 그룹은 별도의 최상위 폴더를 가져야 합니다.](#224-다른-프로젝트로-자주-이주될-수-있는-에셋-그룹은-별도의-최상위-폴더를-가져야-합니다)
  - [2.3 로컬 테스트는 `Developers` 폴더 내에서 해야합니다.](#23-로컬-테스트는-developers-폴더-내에서-해야합니다)
  - [2.4 모든 레벨 에셋은 `Maps` 폴더 내에 위치해야 합니다.](#24-모든-레벨-에셋은-maps-폴더-내에-위치해야-합니다)
  - [2.5 프로젝트에 핵심적인 블루프린트 및 기타 에셋은 `Core` 폴더 내에 위치합니다.](#25-프로젝트에-핵심적인-블루프린트-및-기타-에셋은-core-폴더-내에-위치합니다)
  - [2.6 이름이 `Assets`인 폴더를 만들지 마십시오.](#26-이름이-assets인-폴더를-만들지-마십시오)
  - [2.7 이름이 `Meshes`, `Textures`, `Materials`인 `에셋유형` 폴더를 만들지 마십시오.](#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오)
    - [2.7.1 `Characters` 이하 폴더에는 적용하지 않음.](#271-characters-이하-폴더에는-적용하지-않음)
  - [2.8 여러 에셋과 공유되는 에셋들은 `Common` 폴더 내에 위치합니다.](#28-여러-에셋과-공유되는-에셋들은-common-폴더-내에-위치합니다)
  - [2.9 `MaterialLibrary`](#29-materiallibrary)
  - [2.10 리디렉터, 비어있는 폴더](#210-리디렉터-비어있는-폴더)
- [**3. 블루프린트 코딩 표준**](#3-블루프린트-코딩-표준)
  - [시작하기 전](#시작하기-전)
  - [3.0 기본 원칙](#30-기본-원칙)
  - [3.1 컴파일과 런타임](#31-컴파일과-런타임)
    - [3.1.1 컴파일](#311-컴파일)
    - [3.1.2 런타임](#312-런타임)
  - [3.2 변수](#32-변수)
    - [3.2.1 변수 이름은 명사여야 합니다.](#321-변수-이름은-명사여야-합니다)
    - [3.2.2 Public 변수에는 파스칼 케이스를 사용합니다.](#322-public-변수에는-파스칼-케이스를-사용합니다)
    - [3.2.3 불리언 변수는 b- 접두사를 가집니다.](#323-불리언-변수는-b--접두사를-가집니다)
    - [3.2.4 불리언 변수는 Is, Can, Has, Should와 같은 의문형 동사를 가질 수 있습니다.](#324-불리언-변수는-is-can-has-should와-같은-의문형-동사를-가질-수-있습니다)
    - [3.2.5 불리언 변수로 복잡한 상태를 정의하지 마십시오.](#325-불리언-변수로-복잡한-상태를-정의하지-마십시오)
    - [3.2.6 private, protected 변수에는 접두사 m-을 붙입니다.](#326-private-protected-변수에는-접두사-m-을-붙입니다)
      - [3.2.6.1 private 변수](#3261-private-변수)
      - [3.2.6.2 protected로 의도된 변수](#3262-protected로-의도된-변수)
      - [3.2.6.3 private/protected 변수 이름 예시](#3263-privateprotected-변수-이름-예시)
    - [3.2.7 변수가 속한 클래스를 고려해 불필요한 의미 중복을 피하십시오.](#327-변수가-속한-클래스를-고려해-불필요한-의미-중복을-피하십시오)
    - [3.2.8 기본 자료형 변수에 자료형 이름을 포함하지 마십시오.](#328-기본-자료형-변수에-자료형-이름을-포함하지-마십시오)
    - [3.2.9 배열은 복수형 이름을 가져야 합니다.](#329-배열은-복수형-이름을-가져야-합니다)
    - [3.2.10 구조체의 멤버변수는 모두 파스칼 케이스를 따릅니다.](#3210-구조체의-멤버변수는-모두-파스칼-케이스를-따릅니다)
    - [3.2.11 런타임 중 변경되어선 안되는 상수](#3211-런타임-중-변경되어선-안되는-상수)
    - [3.2.12 변수 툴팁](#3212-변수-툴팁)
    - [3.2.13 슬라이더 및 값 범위](#3213-슬라이더-및-값-범위)
    - [3.2.14 카테고리](#3214-카테고리)
    - [3.2.15 고급 디스플레이 옵션](#3215-고급-디스플레이-옵션)
    - [3.2.16 기타 고급(Advanced) 변수 설정](#3216-기타-고급advanced-변수-설정)
  - [3.3 함수(Functions), 이벤트(Events), 이벤트 디스패처(Event Dispatchers)](#33-함수functions-이벤트events-이벤트-디스패처event-dispatchers)
    - [3.3.1 Function Naming](#bp-funcs-naming)
    - [3.3.1.1 All Functions Should Be Verbs](#bp-funcs-naming-verbs)
    - [3.3.1.2 Property RepNotify Functions Always `OnRep_Variable`](#bp-funcs-naming-onrep)
    - [3.3.1.3 Info Functions Returning Bool Should Ask Questions](#bp-funcs-naming-bool)
    - [3.3.1.4 Event Handlers and Dispatchers Should Start With `On`](#bp-funcs-naming-eventhandlers)
    - [3.3.1.5 Remote Procedure Calls Should Be Prefixed With Target](#bp-funcs-naming-rpcs)
    - [3.3.2 All Functions Must Have Return Nodes](#bp-funcs-return)
    - [3.3.3 No Function Should Have More Than 50 Nodes](#bp-graphs-funcs-node-limit)
    - [3.3.4 All Public Functions Should Have A Description](#bp-graphs-funcs-description)
    - [3.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name](#bp-graphs-funcs-plugin-category)
  - [3.4 Blueprint Graphs](#bp-graphs)
    - [3.4.1 No Spaghetti](#bp-graphs-spaghetti)
    - [3.4.2 Align Wires Not Nodes](#bp-graphs-align-wires)
    - [3.4.3 White Exec Lines Are Top Priority](#bp-graphs-exec-first-class)
    - [3.4.4 Graphs Should Be Reasonably Commented](#bp-graphs-block-comments)
    - [3.4.5 Graphs Should Handle Casting Errors Where Appropriate](#bp-graphs-cast-error-handling)
    - [3.4.6 Graphs Should Not Have Any Dangling / Loose / Dead Nodes](#bp-graphs-dangling-nodes)
- [4. Static Meshes](#4)
  - [4.1 Static Mesh UVs](#s-uvs)
    - [4.1.1 All Meshes Must Have UVs](#s-uvs-no-missing)
    - [4.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps](#s-uvs-no-overlapping)
  - [4.2 LODs Should Be Set Up Correctly](#s-lods)
  - [4.3 Modular Socketless Assets Should Snap To The Grid Cleanly](#s-modular-snapping)
  - [4.4 All Meshes Must Have Collision](#s-collision)
  - [4.5 All Meshes Should Be Scaled Correctly](#s-scaled)
- [5. Niagara](#Niagara)
  - [5.1 No Spaces, Ever](#ng-rules)
- [6. Levels / Maps](#levels)
  - [6.1 No Errors Or Warnings](#levels-no-errors-or-warnings)
  - [6.2 Lighting Should Be Built](#levels-lighting-should-be-built)
  - [6.3 No Player Visible Z Fighting](#levels-no-visible-z-fighting)
  - [6.4 Marketplace Specific Rules](#levels-mp-rules)
    - [6.4.1 Overview Level](#levels-mp-rules-overview)
    - [6.4.2 Demo Level](#levels-mp-rules-demo)
- [7. Textures](#textures)
  - [7.1 Dimensions Are Powers of 2](#textures-dimensions)
  - [7.2 Texture Density Should Be Uniform](#textures-density)
  - [7.3 Textures Should Be No Bigger than 8192](#textures-max-size)
  - [7.4 Textures Should Be Grouped Correctly](#textures-group)




<br>
<br>

## **중요한 용어들**


### 맵(map)과 레벨(level)

맵(map)은 일반적으로 게임플레이의 월드가 되는 레벨(level)을 의미합니다.  

<br>

### 명명 규칙 종류
 #### 파스칼 케이스 (PascalCase)  
 - 띄어쓰기를 모두 붙여서 표현합니다. 즉, 공백이 없습니다.  
 - 각 단어의 첫 글자는 대문자가 됩니다.   
 - 예시는 다음과 같습니다.  
 `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.

 #### 카멜 케이스 (camelCase) 
 - 파스칼 케이스와 비슷하지만 첫 문자는 항상 소문자입니다
 - 예시는 다음과 같습니다.  
 `desertEagle`, `styleGuide`, `aSeriesOfWords`.

 #### 스네이크 케이스 (snake_case)
 - 띄어쓰기를 밑줄(언더바)로 표시합니다.  
 - 일반적으로 모두 소문자로 표시하지만, 경우에 따라 모두 대문자로 표시하기도 합니다.  
 - 예시는 다음과 같습니다.  
 `desert_Eagle`, `style_guide`, `A_SERIES_OF_WORDS`.

<br>

### 변수(Variable)와 프로퍼티(Property)
 일반적인 맥락에서, 변수와 프로퍼티는 서로 혼용이 가능합니다. 만약 동일한 문맥 내에서 두 용어가 혼용되는 경우 정확한 의미는 다음과 같습니다.  

 

 #### 프로퍼티 (Property)
 일반적으로 클래스 내부 멤버로서 정의된 변수를 의미합니다. 예를 들어, `BP_Bomb` 클래스가 변수 `bExploded`를 멤버로 가지고 있다면, `bExploded`는 `BP_Bomb`의 프로퍼티입니다.  
 
 
 
 #### 변수 (Variable)
 일반적으로 함수의 매개변수 또는 함수 내부의 지역변수로 정의된 변수를 의미합니다.  
 
<br>

### 접근 제어자 (Access Modifier)
접근 제어자는 클래스의 멤버 변수와 함수를 선언할 때 이 변수와 함수에 접근 가능한 대상의 범위를 제한하는 역할을 합니다. 블루프린트에서 사용할 수 있는 접근 제어자는 `Public`, `protected`, `private`가 있습니다.  

#### Public
멤버가 공개되어 클래스 외부 어디에서든 접근 가능  

#### protected 
하위 클래스로만 멤버가 공개되어 상속받은 클래스까지만 접근 가능  

#### private 
공개가 제한되어 멤버를 선언한 클래스 자신만 접근 가능

<br>

### 오류와 버그

#### 오류
컴파일 오류는 잘못된 문법 사용 등 컴파일 자체를 불가능하게 만드는 문제를 말합니다.  
런타임 오류는 게임 실행 도중 만난 예기치 못한 상황들을 말합니다. 이런 오류의 예시는 플레이어로부터 입력받은 값이 잘못되었거나, 라이브링크 데이터가 갑자기 끊기는 상황 등이 있습니다. 런타임 오류는 실행 도중 발생할 수도 있다고 미리 예측 가능한 것들이기 때문에, 런타임 오류가 발생하더라도 여전히 프로그램을 진행시킬 수 있도록 프로그램은 이런 예외 상황에 대비한 적절한 예외처리 로직을 가지고 있어야 합니다.


#### 버그
버그는 게임(프로그램) 실행 도중 일어날 수 없다고 가정한 상황이 일어난 것입니다. 함수 실행의 전제조건이 충족되었는데 함수 실행 결과가 예상과 다르게 나오는 상황이 좋은 예시입니다. 버그는 오류와 같은 예기치 못한 상황이 아닌, 프로그램의 로직 자체가 잘못된 상황입니다. 때문에 버그가 발생한다면 그 게임의 진행은 더이상 예측 자체가 불가능해집니다. 버그 상황에서도 올바르게 작동하도록 대처하는 것은 불가능하며, 버그는 발견 즉시 다시 일어나지 않도록 로직 자체를 고쳐야 합니다.


**[⬆ Back to Top](#목차)**

<br>
<br>


## **00. 원칙들**


### **00.1** 당신이 기존에 어떤 스타일을 가지고 있었든, VLAST 소속의 UE 작업자는 모두 이 스타일 가이드를 따라 작업해야 합니다.  

만약 이 스타일 가이드에 변경이 필요하다 생각한다면, 팀에 새로운 스타일을 제시하고 논의하시면 됩니다.  


### **00.2** 프로젝트는 아무리 많은 사람이 참여했다 하더라도, 이 스타일 가이드에 따라 모두 한 사람이 작업한 것처럼 보여야 합니다.

하나의 스타일 가이드를 따라 협업하는 프로젝트는 마치 한 사람이 제작한 것처럼 일관성이 유지됩니다. 이는 작업 과정에서의 모호성을 없애고 다른 팀원의 작업에 대한 불확실한 짐작을 할 필요가 없도록 만들어 줍니다. 그 결과 팀은 더 나은 생산성을 얻게 되며, 유지보수가 쉬워지게 됩니다.


### **00.3** 스타일 가이드를 지키지 않는 팀원을 그대로 내버려두어선 안됩니다.

만약 당신이 스타일 가이드를 지키지 않은 구조, 에셋명, 코드 등을 보게 된다면, 당신은 즉시 그것을 작성한 팀원에게 이를 알리고 스타일 가이드를 지키도록 정정해주어야 합니다.

모든 사람이 같은 스타일 가이드를 지킨다는 것은 팀원 간의 질문과 답변을 더욱 쉽게 해줍니다. 아무렇게나 꼬아놓은 블루프린트를 풀거나 알 수 없는 변수명으로 가려진 머티리얼에 생긴 문제를 해결해주는 걸 좋아하는 사람은 없습니다.

명확한 스타일 가이드가 없는 팀은 협업 능력이 없는 팀입니다.

**[⬆ Back to Top](#목차)**

<br>
<br>

## **01. 금지된 사항들**


### **01.1** 금지된 문자

아래의 문자들은 에셋명, 폴더명, 변수명 등 프로젝트 내 어디에서도 사용되어선 안됩니다.  
* ` ` 공백 (스페이스바)
* `\` 백슬래시 기호
* `#!@$%` 대부분의 특수 기호
* 한글 등 모든 유니코드 문자 (즉, 영문이 아닌 대부분의 문자)


즉, 다음의 문자들만 허용됩니다.
* `A-Z` ABCDEFGHIJKLMNOPQRSTUVWXYZ
* `a-z` abcdefghijklmnopqrstuvwxyz
* `0-9` 0123456789
* `_` 밑줄(언더바)

금지된 문자를 사용하지 않는 것은 모든 데이터의 모든 플랫폼으로의 포팅 호환성을 높여줍니다.

**[⬆ Back to Top](#목차)**

<br>
<br>

## **02. 엔진 기본 Config 설정**

엔진의 디폴트 환경변수로 설정해두면 유용한 환경변수 설정들을 다룹니다.  
엔진 기본 환경변수 파일은 다음 경로 내에 위치합니다.
> 엔진설치경로\엔진버전\Engine\Config
> 
> UE5 Config파일 경로 예시  
> C:\Program Files\Epic Games\UE_5.0\Engine\Config

### 02.1 BaseEngine.ini

#### 02.1.1 공유 DCC 설정

사내 네트워크에 연결되어있는 PC의 경우, 셰이더를 새로 컴파일하는 속도보다 네트워크를 통해 공유받는 속도가 더 빠릅니다.  
사무실 내의 PC 중 한 대만 셰이더 컴파일을 해두면 다른 PC들은 셰이더 컴파일을 할 필요가 없도록 공유 DCC 경로를 설정해줍니다.  

재택근무 등 사무실 네트워크 외의 환경에서는 로컬 컴파일이 빠르므로 설정하지 않습니다.

> `BaseEngine.ini` 파일 내의 다음 구문 변경
>
> `Ctrl + F`로 `InstalledDerivedDataBackendGraph` 검색한 뒤,
> 
> `Local=` 라인의 `Path="%ENGINEVERSIONAGNOSTICUSERDIR%DerivedDataCache"` 라인을 다음과 같이 변경.  
> Path="`공유 DCC 경로`"   
> 
> *DCC 경로는 VLAST 문서 위키에 있음*

### 02.2 BaseEditorPerProjectUserSettings.ini

#### 02.2.1 [Developers 폴더](#23-로컬-테스트는-developers-폴더-내에서-해야합니다) 사용 편의를 위한 설정

`Developers` 폴더를 언제나 개인화된 실험실로 사용할 수 있게 보장해주기 위한 설정입니다. 자세한 내용은 [Developers 폴더](#23-로컬-테스트는-developers-폴더-내에서-해야합니다) 항목 참조. 

> `BaseEditorPerProjectUserSettings.ini` 파일 내의 다음 구문 변경
> 
> `Ctrl + F`로 `bSCCAutoAddNewFiles` 검색한 뒤, `True`를 `False`로 변경.  
> `bSCCAutoAddNewFiles=False` 저장

#### 02.2.2 [블루프린트 코딩 표준](#3-블루프린트-코딩-표준) 준수를 위한 설정

엔지니어, 테크니컬 아티스트 등 블루프린트 협업 빈도가 높은 팀원들의 [블루프린트 코딩 표준](#3-블루프린트-코딩-표준) 준수 과정에서의 [혼선](#시작하기-전)을 없애기 위한 설정입니다.  

아티스트, 게임 디자이너 등 주로 만들어진 블루프린트를 사용하는 팀원들은 설정하지 않습니다.
> `BaseEditorPerProjectUserSettings.ini` 파일 내의 다음 구문 변경
> 
> `Ctrl + F`로 `bShowFriendlyNames` 검색한 뒤, `True`를 `False`로 변경.  
> `bShowFriendlyNames=False` 저장

**[⬆ Back to Top](#목차)**

<br>
<br>

## 1. 에셋 명명 규칙

스타일 가이드의 모든 부분이 그렇지만, 에셋 명명 규칙은 반드시 지켜야 합니다.  
명명 규칙에 따라 일관되게 지어진 에셋 이름은 에셋 관리, 검색, 분석, 유지보수를 매우 쉽게 만들어줍니다.

명명 규칙의 큰 틀은 다음과 같이 `_`(밑줄)에 의해 에셋의 종류, 이름 등을 구분합니다.

<br>

### 1.1 에셋명 기본 형식: `접두사_기본에셋명_세부변형_접미사`  

`접두사`와 `접미사`는 에셋 형식에 따라 다음의 [에셋 접두사 & 접미사 테이블](#12-에셋-접두사--접미사-테이블)에 의해 결정됩니다.

모든 에셋들은 기본이 되는 에셋 이름인 `기본에셋명`을 가져야만 합니다. `기본에셋명`은 그 에셋이 속한 그룹의 문맥에 연관되는 짧고 쉬운 이름일수록 좋습니다. 예를 들어 캐릭터의 이름이 `Nina`라면, 모든 Nina 에셋들의 `기본에셋명`이 `Nina`가 되어야 합니다.

`세부변형`은 기본에셋에서 `파생된 다양한 변형의 이름`을 지칭합니다. 예를 들어 `Nina` 캐릭터 에셋에는 다양한 `스킨 변형`이 있을 수 있습니다. Nina 스켈레탈 메시 중 `캐주얼 스타일`의 스킨이 있다면 에셋명은 SKM_Nina_`Casual` 이 됩니다.  
또다른 예로 `레트로 스타일`의 스킨이 있다면, 에셋명은 SKM_Nina_`Retro` 가 됩니다.  

이 스켈레탈 메시에 사용되는 텍스처 에셋명의 좋은 예는 캐주얼 스킨의 경우 `T_Nina_Casual_Top_D`, `T_Nina_Casual_Top_N`, `T_Nina_Casual_Feet_D`, 레트로의 경우 `T_Nina_Retro_Top_D`, `T_Nina_Retro_Bottom_D` 가 좋은 예시가 됩니다.

만약 기본에셋명에서 파생되는 `세부변형`이 특정 이름으로 표현하기에는 애매한 눈에 띄는 특징이 없는 경우, `세부변형` 이름을 숫자로 대신할 수 있습니다. 예를 들어 모델러가 다양한 종류의 암석을 디자인했을 때, 그것들의 변형은 SM_Rock_`01`, SM_Rock_`02`, SM_Rock_`03` 같은 형태가 될 수 있습니다. 또는 다음과 같이 특정 `세부변형` 다음에 `변형숫자`가 올 수도 있습니다. SM_Rock_`Basalt_01`, SM_Rock_`Basalt_02`


#### 1.1의 예시들

##### 기본에셋명 `Nina`의 `CasualOffice`변형 예

| 에셋 유형                      | 에셋명                            |
| ------------------------------ | -------------------------------- |
| 스켈레탈 메시 (캐릭터 상의)      | SKM_Nina_Suit_Shirt               |
| 스켈레탈 메시 (캐릭터 하의)      | SKM_Nina_Suit_Slacks              |
| 머티리얼 (캐릭터 상의)           | M_Nina_Suit_Shirt                 |
| 텍스처 *Diffuse/Albedo*         | T_Nina_Suit_Shirt_D               |
| 텍스처 *Normal*                 | T_Nina_Suit_Shirt_N               |

##### 기본에셋명 `Rock`의 `불특정 변형` 예

| 에셋 유형                                      | 에셋명                            |
| --------------------------------------------- | --------------------------------- |
| 스태틱 메시 (변형1)                            | SM_Rock_01                        |
| 스태틱 메시 (변형2)                            | SM_Rock_02                        |
| 스태틱 메시 (변형3)                            | SM_Rock_03                        |
| 머티리얼 (변형들의 마스터)                     | M_Rock                             |
| 머티리얼 인스턴스 (변형1의 인스턴스)            | MI_Rock_01                         |
| 머티리얼 인스턴스 (눈쌓인 세부변형의 인스턴스)   | MI_Rock_Snow                       |

<br>

### 1.2 에셋 접두사 & 접미사 테이블

[1.1 에셋명 기본 형식](#11-에셋명-기본-형식-접두사_기본에셋명_세부변형_접미사)의 `접두사`, `접미사` 규칙입니다.  
이 스타일 가이드는 [텍스처](#126-텍스처-textures)를 제외한 에셋유형에는 가능한 한 접미사를 사용하지 않습니다.


#### 1.2.1 흔히 사용되는 에셋

| 에셋 유형          | 접두사   | 접미사  | Notes                            |
| ----------------- | -------- | ------ | -------------------------------- |
| 레벨              |          |         | `Maps` 폴더 안에 있어야 한다.      |
| 블루프린트         | BP_      |         |                                  |
| 머티리얼           | M_       |         |                                  |
| 머티리얼 인스턴스   | MI_      |         |                                  |
| 스태틱 메시        | SM_      |         |                                  |
| 스켈레탈 메시      | SKM_     |         |                                  |
| 텍스처            | T_       | _?      | 접미사 디테일은 [텍스처 (Textures)](#126-텍스처-textures) 항목을 봐주세요.    |
| 나이아가라 시스템  | NS_      |         |                                  |
| 위젯 블루프린트    | WBP_     |         |                                  |


#### 1.2.2 애니메이션 (Animations)

| 에셋 유형                       | 접두사     | 접미사     | Notes                            |
| ------------------------------ | ---------- | ---------- | -------------------------------- |
| 에임 오프셋                     | AO_        |            |                                  |
| 에임 오프셋 1D                  | AO_        |            |                                  |
| 애니메이션 블루프린트            | ABP_       |            |                                  |
| 애니메이션 컴포짓               | AC_        |            |                                  |
| 애니메이션 몽타주               | AM_        |            |                                  |
| 애니메이션 시퀀스               | A_         |            |                                  |
| 블렌드 스페이스                 | BS_        |            |                                  |
| 블렌드 스페이스 1D              | BS_        |            |                                  |
| 레벨 시퀀스                    | LS_         |            |                                  |
| 컨트롤 릭 *Control Rig*        | CR_         |            |                                  |
| IK 릭 *IK Rig*                 | IK_        |            |                                  |
| IK 리타기터 *IK Retargeter*    | RTG_       |            |                                  |
| 스켈레탈 메시 *Skeletal Mesh*  | SKM_       |            |                                  |
| 스켈레톤 *Skeleton*            | SKEL_      |            |                                  |


#### 1.2.3 인공 지능 (Artificial Intelligence)

| 에셋 유형                | 접두사       | 접미사     | Notes                            |
| ----------------------- | ------------ | ---------- | -------------------------------- |
| AI Controller           | AIC_         |            |                                  |
| Behavior Tree           | BT_          |            |                                  |
| Blackboard              | BB_          |            |                                  |
| Decorator               | BTDecorator_ |            |                                  |
| Service                 | BTService_   |            |                                  |
| Task                    | BTTask_      |            |                                  |
| Environment Query       | EQS_         |            |                                  |
| EnvQueryContext         | EQS_         | Context    |                                  |


#### 1.2.4 블루프린트 (Blueprints)

| 에셋 유형                     | 접두사  | 접미사     | Notes                            |
| ---------------------------- | ------- | ---------- | -------------------------------- |
| 블루프린트                    | BP_    |            |                                  |
| 블루프린트 컴포넌트           | BPC_    |            |                                  | 
| 블루프린트 함수 라이브러리    | BPFL_   |            |                                  |
| 블루프린트 인터페이스         | BPI_    |            |                                  |
| 블루프린트 매크로 라이브러리  | BPML_    |            | 가능한 한 사용하지 않는다.         |
| 열거형 *Enumeration*        | E        |            | 접두사 후 밑줄 없음. eg. `ECharacterState` |
| 구조체 *Structure*          | S        |            | 접두사 후 밑줄 없음.               |
| 위젯 블루프린트              | WBP_     |            |                                  |
| 게임플레이 어빌리티          | GA_      |            |                                  |


#### 1.2.5 머티리얼 (Materials)

| 에셋 유형                               | 접두사     | 접미사     | Notes                            |
| -------------------------------------- | ---------- | ---------- | -------------------------------- |
| 머티리얼                                | M_         |            |                                  |
| 머티리얼 (포스트 프로세스)                | M_PP_     |            |                                  |
| 머티리얼 (데칼)                          | M_Decal_  |            |                                  |
| 머티리얼 인스턴스                        | MI_       |            |                                  |
| 머티리얼 인스턴스 (포스트 프로세스)       | MI_PP_    |            |                                  |
| 머티리얼 인스턴스 (데칼)                 | MI_Decal_ |            |                                  |
| 머티리얼 함수                           | MF_       |            |                                  |
| 머티리얼 파라미터 컬렉션                 | MPC_      |            |                                  |
| 서브서피스 프로파일 *Subsurface Profile* | SSP_      |            |                                  |
| 피직스 머티리얼                          | PM_       |            |                                  |


#### 1.2.6 텍스처 (Textures)

| 에셋 유형                        | 접두사     | 접미사     | Notes                            |
| ------------------------------- | ---------- | ---------- | -------------------------------- |
| 텍스처                           | T_        |            |                                  |
| - Diffuse/Albedo/Base Color     | T_         | _D         |                                  |
| - Normal                        | T_         | _N         |                                  |
| - Roughness                     | T_         | _R         |                                  |
| - Alpha/Opacity                 | T_         | _A         |                                  |
| - Mask                          | T_         | _A         | *똑같이 Opacity 채널에 들어가므로 Alpha/Opacity와 동일합니다.*  |
| - Ambient Occlusion             | T_         | _O         |                                  |
| - Bump                          | T_         | _B         |                                  |
| - Emissive                      | T_         | _E         |                                  |
| - Specular                      | T_         | _S         |                                  |
| - Metallic                      | T_         | _M         |                                  |
| - RGB채널에 패킹된 텍스처         | T_         | _*         | 아래의 [패킹된 텍스처 (Texture Packing)](#1261-패킹된-텍스처-texture-packing)를 참고해주세요. |
| 텍스처 큐브 *Texture Cube*       | TC_        |            |                                  |
| 미디어 텍스처 *Media Texture*    | MT_        |            |                                  |
| 렌더 타깃 *Render Target*        | RT_        |            |                                  |
| 큐브 렌더 타깃                    | RTC_       |            |                                  |


##### 1.2.6.1 패킹된 텍스처 (Texture Packing)

`Roughness`, `Ambient Occlusion`, `Metallic` 등 여러 개의 맵을 RGB채널에 각각 할당해 하나의 텍스처로 패킹하는 것이 일반적입니다. 패킹된 텍스처의 접미사는 RGB 채널에 할당된 맵의 순서를 따릅니다.  
예를 들어, `Emissive`, `Roughness`, `Ambient Occlusion` 맵을 각각 `Red`, `Green`, `Blue` 채널에 할당한 경우, `접미사`는 RGB에 할당된 순서에 따라 `_ERO`가 됩니다.

> RGBA 4채널 패킹은 추천하지 않습니다.  
> 기본 텍스처 압축 포맷이 알파채널 압축을 지원하지 않아, 4채널 압축을 위한 추가적인 연산이 필요해지기 때문입니다. 


#### 1.2.7 기타 (Miscellaneous)

| 에셋 유형                   | 접두사     | 접미사     | Notes                            |
| -------------------------- | ---------- | ---------- | -------------------------------- |
| 데이터 에셋                 | DA_        |            |                                  |
| 데이터 테이블               | DT_        |            |                                  |
| 플롯 커브                   | CV_Float_  |            |                                  |
| 벡터 커브                   | CV_Vector_ |            |                                  |
| 컬러 커브                   | CV_Color_  |            |                                  |
| 커브 테이블                 | CV_Table_  |            |                                  |
| 벡터 필드                   | VF_        |            |                                  |
| HLOD 레이어                 | HLODLayer_ |            |                                  |
| 그룸 *Groom*                | Groom_     |            |                                  |


#### 1.2.8 페이퍼 2D (Paper 2D)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Paper Flipbook          | PFB_       |            |                                  |
| Sprite                  | SPR_       |            |                                  |
| Sprite Atlas Group      | SPRG_      |            |                                  |
| Tile Map                | TM_        |            |                                  |
| Tile Set                | TS_        |            |                                  |


#### 1.2.9 피직스 (Physics)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| --------------------- | ---------- | ---------- | -------------------------------- |
| 피직스 머티리얼        | PM_        |            |                                  |
| 피직스 에셋            | PA_        |            |                                  |
| 지오메트리 컬렉션       | GC_        |            |                                  |
| 지오메트리 컬렉션 캐시  | GC_        | _Cache     |                                  |
| 카오스 솔버            | Solver_    |            |                                  |
| 카오스 캐시 컬렉션      | Chaos_     | _Cache     |                                  |


#### 1.2.10 사운드 (Sounds)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Dialogue Voice          | DV_        |            |                                  |
| Dialogue Wave           | DW_        |            |                                  |
| Reverb Effect           | Reverb_    |            |                                  |
| Sound Attenuation       | ATT_       |            |                                  |
| Sound Class             |            |            | No prefix/suffix. Should be put in a folder called SoundClasses |
| Sound Concurrency       |            | _SC        | Should be named after a SoundClass |
| Sound Cue               | A_         | _Cue       |                                  |
| Sound Mix               | Mix_       |            |                                  |
| Sound Wave              | A_         |            |                                  |
| 메타 사운드              | MS_        |            |                                  |
| 메타 사운드 소스         | MSS_       |            |                                  |
| 컨트롤 버스              | CB_        |            |                                  |
| 컨트롤 버스 믹스         | CBM_       |            |                                  |


#### 1.2.11 유저 인터페이스 (User Interface)

| 에셋 유형                | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Font                    | Font_      |            |                                  |
| 위젯 블루프린트          | WBP_       |            |                                  |


#### 1.2.12 FX

| 에셋 유형                        | 접두사       | 접미사     | Notes                            |
| ------------------------------- | ------------ | ---------- | -------------------------------- |
| 나이아가라 시스템                | NS_          |            |                                  |
| 나이아가라 모듈                 | NM_           |            |                                  |
| Niagara Dynamic Input Script   | NM_           |            |                                  |
| 나이아가라 이미터                | NE_          |            |                                  |
| 나이아가라 이펙트 타입           | EffectType_  |            |                                  |
| 나이아가라 파라미터 컬렉션       | NPC_         |            |                                  |
| - 인스턴스                      | NPCI_        |            |                                  |


#### 1.2.13 미디어 (Media)

| 에셋 유형                | 접두사       | 접미사      | Notes                            |
| ----------------------- | ------------ | ---------- | -------------------------------- |
| File Media Source       | MS_File_     |            |                                  |
| Img Media Source        | MS_Img_      |            |                                  |
| Stream Media Source     | MS_Stream_   |            |                                  |
| Media Player            | MP_          |            |                                  |
| Media Texture           | MT_          |            |                                  |


**[⬆ Back to Top](#목차)**

<br>
<br>

## 2. Content 폴더 디렉터리 구조

에셋 명명 규칙과 마찬가지로, 프로젝트 디렉터리 구조 스타일 역시 반드시 지켜주셔야 합니다.  
에셋 이름과 Content 디렉터리 구조는 서로 연관이 깊으며, 둘 중 하나를 위반한다면 불필요한 혼란이 생기게 됩니다.  

<br>

### 2.0 Content 폴더 디렉터리 구조 예제

프로젝트 이름 `MySampleProject`의 `Content`폴더 디렉터리 구조 예제
<pre>
|-- Content
    |-- <a href="#22-최상위-폴더-규칙">MySampleProject</a>
        |-- <a href="#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오">3D_Assets</a>
            |-- Building
                |-- Balcony
                |-- Wall
            |-- Nature
                |-- Rock
                |-- Tree
            |-- Props
                |-- OldWoodenBench
            |-- OldSchool
        |-- <a href="#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오">3D_Plants</a>
            |-- Desert
                |-- Cactus
                |-- DesertYellowHead
            |-- Arctic
                |-- Moss
        |-- <a href="#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오">Decals</a>
            |-- Concrete
            |-- Metal
        |-- <a href="#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오">Surfaces</a>
            |-- Asphalt
            |-- Fabric
        |-- <a href="#271-characters-이하-폴더에는-적용하지-않음">Characters</a>
            |-- <a href="#28-여러-에셋과-공유되는-에셋들은-common-폴더-내에-위치합니다">Common</a>
                |-- Animations
                |-- Audio
            |-- Nina
                |-- Animations
                |-- Blueprints
                |-- Meshes
                |-- Materials
                |-- Textures
            |-- Abo
                |-- Animations
                |-- Blueprints
                |-- Meshes
                |-- Materials
                |-- Textures
        |-- <a href="#25-프로젝트에-핵심적인-블루프린트-및-기타-에셋은-core-폴더-내에-위치합니다">Core</a>
            |-- Characters
            |-- Engine
            |-- GameModes
            |-- Interactables
            |-- Weapons
        |-- Effects
            |-- Electrical
            |-- Fire
            |-- Weather
        |-- Blueprints
        |-- <a href="#24-모든-레벨-에셋은-maps-폴더-내에-위치해야-합니다">Maps</a>
            |-- Campaign1
            |-- Campaign2
        |-- <a href="#29-materiallibrary">MaterialLibrary</a>
            |-- Debug
            |-- Functions
            |-- Textures
            |-- Utility
        |-- GUI
    |-- <a href="#223-최상위-폴더-규칙을-준수하는-샘플-템플릿-마켓플레이스-콘텐츠는-폴더-구조를-수정하지-않습니다">Megascans</a>
    |-- <a href="#223-최상위-폴더-규칙을-준수하는-샘플-템플릿-마켓플레이스-콘텐츠는-폴더-구조를-수정하지-않습니다">StarterContent</a>
    |-- <a href="#223-최상위-폴더-규칙을-준수하는-샘플-템플릿-마켓플레이스-콘텐츠는-폴더-구조를-수정하지-않습니다">ThirdPerson</a>
</pre>

#### 2.0.1 예제의 폴더들에 대한 설명

##### 일반
| 폴더 이름          | Notes                            |
| ----------------- | -------------------------------- |
| MySampleProject   | [최상위 폴더 규칙](#22-최상위-폴더-규칙)에 따라 생성된 프로젝트의 최상위 폴더         |
| Core              | 프로젝트에 핵심 기능을 하는 에셋들이 모인 폴더. 자세한 내용은 [Core](#25-프로젝트에-핵심적인-블루프린트-및-기타-에셋은-core-폴더-내에-위치합니다) 참조.           |
| Blueprints        | 프로젝트에 핵심적이지는 않은 블루프린트 에셋이 모인 폴더           |
| Maps              | Level 에셋 폴더           |
| MaterialLibrary   | 프로젝트 공용 마스터 머티리얼, 함수, 텍스처 등이 모인 폴더. 자세한 내용은 [MaterialLibrary](#29-materiallibrary) 참조.           |
| GUI               | 위젯 블루프린트, 미디어소스 등 유저 UI/UX 에셋들이 모인 폴더           |

##### 3D 에셋, 재질 관련
| 폴더 이름          | Notes                            |
| ----------------- | -------------------------------- |
| 3D_Assets         | 구조물, 소품, 장식, 환경요소 등의 에셋들이 위치한다. 단순한 스켈레탈 메시 에셋들도 포함된다. |
| 3D_Plants         | 폴리지(Foliage) 기능에 사용될 꽃, 풀, 잡초와 같은 작은 식생 에셋들이 위치한다. |
| Decals            | 데칼에 사용되는 머티리얼, 텍스처 에셋들이 위치한다. |
| Surfaces          | 표면 재질에 사용되는 머티리얼, 텍스처 에셋들이 위치한다. 마스크 같은 맵에 의해 특정 3D 에셋에 종속되지 않고 머티리얼 레이어, 랜드스케이프, 버텍스 페인팅 등에 사용되는 재질들이 속한다. |

위의 `3D_Assets`, `3D_Plants`, `Decals`, `Surfaces` 폴더들은 3D 에셋, 재질, 데칼 등 개체화된 아트 에셋들이 저장되는 경로입니다.  
가장 말단의 폴더는 개체화된 아트 에셋의 [기본에셋명](#11-에셋명-기본-형식-접두사_기본에셋명_세부변형_접미사)이며, 개체화된 에셋들을 아우르는 상위 테마 폴더를 가질 수 있습니다. 예를 들어 사막의 식물 `Cactus`, `DesertYellowHead` 개체의 폴더는 `Content\ProjectName\3D_Plants\Desert\` 이하 경로에 모여있습니다.  

만약 전체가 모여 하나의 컬렉션, 테마를 이루는 개체 집단이 있을 경우, 테마 이름의 폴더만 두고 그 하위에 개체별 폴더는 따로 두지 않습니다. `OldSchool` 테마가 있을 경우, `책상`, `의자`, `교탁`, `깨진 창문` 등 테마에 속하는 모든 개체는 `Content\ProjectName\3D_Assets\OldSchool` 경로에 별도의 개체폴더 없이 모든 리소스를 모아둡니다. 

개체폴더 이하에 `Meshes`, `Textures`, `Materials`, `Blueprints` 폴더는 생성하지 않습니다. 자세한 내용은 [2.7](#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오) 항목을 참고해주세요.

##### 캐릭터 관련
| 폴더 이름           | Notes                                            |
| ------------------ | ------------------------------------------------ |
| Characters         | 본 구조를 가지면서 캐릭터로서 사용되는 에셋들을 가진다. *본 구조를 가졌으나 캐릭터로 사용되지 않는 단순한 에셋들은 `3D_Assets` 경로에 포함된다.* |
| Common         | 여러 캐릭터에 공유될 수 있는 에셋들을 가진다. 자세한 내용은 [2.8](#28-여러-에셋과-공유되는-에셋들은-common-폴더-내에-위치합니다) 항목 참조. |

캐릭터 폴더들은 [2.7](#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오)의 예외로 적용됩니다.  
`Characters` 폴더 이하에는 구체적인 개별 캐릭터 폴더들이 존재합니다. 각각의 캐릭터 폴더는 캐릭터에 사용되는 `Blueprints`, `Meshes`, `Materials`, `Textures` 등 `에셋유형` 폴더를 하위 폴더로 가집니다. 자세한 내용은 [2.7.1](#271-characters-이하-폴더에는-적용하지-않음) 항목을 참고해주세요.

##### 기타
이외의 `Megascans`, `StarterContent`, `ThirdPerson` 폴더는 외부에서 이주되어온 [최상위 폴더](#22-최상위-폴더-규칙)로, [2.2.3](#223-최상위-폴더-규칙을-준수하는-샘플-템플릿-마켓플레이스-콘텐츠는-폴더-구조를-수정하지-않습니다)에 따라 Content 폴더 최상위 경로에 그대로 존재합니다.

보다 자세한 설명과 세부 원칙들은 이하의 항목에서 다룹니다.

<br>

### 2.1 폴더명 규칙

Content 폴더 내의 모든 폴더 이름에 적용되는 공통 규칙들입니다.


#### 2.1.1 항상 파스칼 케이스(PascalCase)를 사용할 것

파스칼 케이스는 첫 문자가 대문자로 시작하며, 각 단어의 시작을 대문자로 구분합니다.
`GameModes`, `DesertEagle` 등이 그 예입니다. 자세한 설명은 [파스칼 케이스(PascalCase)](#파스칼-케이스-pascalcase)를 참고해주세요.  
대문자가 연속으로 오는 등 파스칼 케이스를 그대로 적용하기 애매할 경우, 드물게 `_`(밑줄)을 사용할 수 있습니다. (eg. `3D_Assets`)

> Maya 작업자의 경우 Maya 내에서는 [카멜 케이스(camelCase)](#카멜-케이스-camelcase)가 표준 스타일인 경우가 많아 이 스타일을 그대로 언리얼 엔진에 적용하시는 경우가 많습니다.  
> 언리얼 엔진에서는 [파스칼 케이스(PascalCase)](#파스칼-케이스-pascalcase)가 표준임을 유념해주세요.

#### 2.1.2 공백(스페이스바)을 사용하지 말 것

[금지된 문자](#011-금지된-문자)에 따라 폴더 이름에 ` `공백을 사용해선 안됩니다.

#### 2.1.3 영문과 숫자 이외의 문자(특수문자 포함)를 사용하지 말 것

폴더 이름에 허용되는 문자는 `A-Z`, `a-z`, `0-9` 뿐입니다. [금지된 문자](#011-금지된-문자)의 허용된 문자 항목을 참고해주세요.

<br>

### 2.2 최상위 폴더 규칙

프로젝트의 모든 에셋은 프로젝트 이름을 딴 최상위 폴더 내에 위치해야 합니다. 예를 들어, 프로젝트 이름이 `MySampleProject`이라면 `MySampleProject` 프로젝트를 위해 생성된 모든 에셋은 `Content\MySampleProject\` 내에 위치해야 합니다. 만약 프로젝트 이름이 너무 길거나 프로젝트 이름을 그대로 최상위 폴더명으로 따기에 부적합하다 느낄 경우, 적합한 이름으로 변경할 수 있습니다. 

프로젝트 내의 모든 에셋이 프로젝트의 최상위 폴더에 위치해야하는 것은 아닙니다. 다른 프로젝트에서 이주해오거나 프로젝트에 추가한 마켓플레이스 콘텐츠 등이 있을 경우 이주해온 프로젝트의 에셋들도 `최상위 폴더 규칙`에 따라 각자의 최상위 폴더를 가질 것이므로, 한 프로젝트는 다수의 최상위 폴더를 가질 수 있습니다. 자세한 내용은 [다음](#223-최상위-폴더-규칙을-준수하는-샘플-템플릿-마켓플레이스-콘텐츠는-폴더-구조를-수정하지-않습니다)을 확인해주세요.

> `Developers` 폴더는 프로젝트에 종속된 폴더가 아니므로, 프로젝트별로 구분되지 않습니다. 자세한 내용은 [Developers 폴더](#23-로컬-테스트는-developers-폴더-내에서-해야합니다) 항목을 참고해주세요.

최상위 폴더 규칙에 대한 세부 사항은 다음과 같습니다.

#### 2.2.1 최상위 폴더 바깥에 에셋을 두어선 안됩니다. 

에셋이 프로젝트의 최상위 폴더 바깥에 위치하는 것은 허용되지 않습니다. 구체적인 예시는 다음과 같습니다.  
프로젝트 `MySampleProject` 내의 `T_Rock` 에셋이 최상위 폴더 외의 경로에 잘못 위치한 예시들:  
> `Content\T_Rock.uasset`  
> `Content\Textures\T_Rock.uasset`  
> `Content\Temp\T_Rock.uasset`  
> `Content\Test\T_Rock.uasset`  

최상위 폴더 바깥에 위치한 에셋은 팀원들에게 정리할 필요가 없는 에셋이라는 암시를 주게 되며, 이러한 경로의 존재는 에셋을 정리하지 않는 나쁜 습관을 조장하여 올바른 스타일을 따르는 것을 매우 어렵게 만듭니다.  

최상위 폴더 바깥에 에셋이 위치할 경우 그래야만 하는 명확한 목적이 있어야 합니다. 만약 실험적인 목적을 위한 로컬 테스트 에셋이라면 [Developers 폴더](#23-로컬-테스트는-developers-폴더-내에서-해야합니다) 내에 위치해야 합니다.


#### 2.2.2 최상위 폴더 규칙은 이주 충돌을 감소시켜줍니다.

여러 프로젝트에서 작업이 이루어지면서 다른 모든 프로젝트에 유용하게 사용될 에셋이 있는 경우, 한 프로젝트에서 다른 프로젝트로 에셋 그룹을 `이주(Migrate)`하는 것이 일반적입니다. 콘텐츠 브라우저의 이주 기능을 사용하여 에셋을 다른 프로젝트로 복사하는 경우, 에디터의 종속성 검사에 의해 이와 관련된 에셋 일체가 함께 복사됩니다. 

두 프로젝트 사이에 [최상위 폴더 규칙](#22-최상위-폴더-규칙)이 제대로 지켜지지 않는 경우, 에셋의 이주는 쉽게 문제를 일으키게 됩니다. 구체적인 충돌 예시는 다음과 같습니다. 

##### 2.2.2.1 마스터 머티리얼 이주 충돌 예시

`ProjectA`에서 마스터 머티리얼을 만들었고, 이 머티리얼이 `ProjectB`에도 유용하다 판단해 이주하는 상황을 가정합니다. 만약 프로젝트가 [최상위 폴더 규칙](#22-최상위-폴더-규칙)을 지키지 않는 경우, 마스터 머티리얼은 `Content\MaterialLibrary\M_Master`와 같은 경로에 위치할 확률이 높아집니다.

문제는 `ProjectB`도 최상위 경로 규칙을 지키지 않으며 동일한 경로에 이미 자체적인 마스터 머티리얼이 있을 경우 발생합니다. `ProjectB`의 아티스트들은 지시받은 대로 `Content\MaterialLibrary\M_Mater`의 인스턴스를 생성해 여러 에셋에 이미 이를 적용해두었습니다. 이 상태에서 `ProjectA`의 `M_Master`가 이주되면 기존의 `M_Master`를 덮어씌우며 의도치 않게 기존의 모든 에셋의 룩을 변경하는 결과가 발생하게 됩니다.

이러한 충돌 문제는 이주를 실행하는 당사자가 아티스트라면 미리 예측하기 어려우며, 충돌이 발생한 후에도 문제가 발생한 이유를 쉽게 발견하지 못할 수 있습니다. 스태틱 메시를 이주하는 아티스트는 종속성에 의해 `Content\MaterialLibrary\M_Mater` 에셋이 함께 이주되는 것을 미리 파악하지 못할 수 있으며, 일반적으로 아티스트는 마스터 머티리얼 개발에 익숙한 사람이 아닐 가능성이 높기 때문에 잘못된 덮어씌움으로 기존 에셋에도 문제가 발생했다는 사실을 파악하지 못할 수 있습니다. 

이처럼 [최상위 폴더 규칙](#22-최상위-폴더-규칙)이 지켜지지 않은 두 프로젝트 사이의 이주는 기존 에셋과의 충돌을 일으킬 확률이 매우 높아집니다. 만일 두 프로젝트가 모두 [최상위 폴더 규칙](#22-최상위-폴더-규칙)을 지키고 있었다면, `ProjectB`로의 이주 결과는 다음과 같이 되며 충돌을 피할 수 있습니다. 
<pre>
|-- Content
    |-- ProjectA
        |-- MaterialLibrary
            |-- M_Master.uasset
    |-- ProjectB
        |-- MaterialLibrary
            |-- M_Master.uasset 
</pre>


이는 에픽이 마켓플레이스 가이드라인에 동일한 규칙을 적용하는 이유입니다.

#### 2.2.3 최상위 폴더 규칙을 준수하는 샘플, 템플릿, 마켓플레이스 콘텐츠는 폴더 구조를 수정하지 않습니다.

[2.2.2](#222-최상위-폴더-규칙은-이주-충돌을-감소시켜줍니다)의 예를 보듯, 마켓플레이스 콘텐츠, 템플릿 등은 [최상위 폴더 규칙](#22-최상위-폴더-규칙)을 준수하기 때문에 이러한 에셋의 추가는 프로젝트에 방해가 되지 않습니다.

하지만 마켓플레이스 콘텐츠가 언제나 [최상위 폴더 규칙](#22-최상위-폴더-규칙)을 준수한다고 신뢰할 수는 없습니다. 마켓플레이스 콘텐츠를 본 프로젝트에 추가하기 전 반드시 테스트 프로젝트에 먼저 추가해본 뒤, 규칙을 준수하는 경우에만 본 프로젝트로 이주합니다. 그렇지 않을 경우 규칙에 따라 정리한 뒤 이주합니다.

[최상위 폴더 규칙](#22-최상위-폴더-규칙)을 준수하는 패키지를 올바르게 프로젝트에 추가한 뒤에는 이주된 상태 그대로 별도의 최상위 폴더에 둡니다. 추가한 패키지의 폴더 구조를 변경하거나 기존 프로젝트의 최상위 폴더에 병합하는 일은 해당 패키지가 업데이트되거나 패키지에서 추가로 이주할 에셋이 생길 경우 중복된 에셋을 만들거나 이주 충돌 가능성을 높입니다. 이주해온 패키지에 일부 변형을 주고 싶은 경우, `Content\이주 패키지의 최상위폴더\Modified` 폴더를 만들어 패키지에서 변경된 사항은 `Modified` 폴더에 모아 추가 이주로 인한 충돌 가능성을 줄여야 합니다.

추가한 패키지의 최상위 폴더 구조를 변경하는 경우는 해당 패키지를 프로젝트에 완전히 병합하려는 경우에 한합니다.


#### 2.2.4 다른 프로젝트로 자주 이주될 수 있는 에셋 그룹은 별도의 최상위 폴더를 가져야 합니다.

만약 프로젝트의 일부 작업사항을 다른 프로젝트로 이주할 계획이 있거나, 빈번하게 다른 프로젝트와 공유되는 작업이 있을 경우 이러한 작업들을 모아 별도의 최상위 폴더에 두는 것을 고려해야 합니다. 이 결정은 주로 프로그래머 또는 마스터 머티리얼 등을 제작하는 테크니컬 아티스트가 내리게 됩니다.  

자주 이주되는 에셋 그룹을 별도의 최상위 폴더에 두는 것은 이 그룹을 메인 프로젝트와 분리된 별도의 모듈처럼 만들어, 다른 프로젝트로의 이주를 쉽게 만들어줍니다. 분리된 최상위 폴더의 에셋들은 본 프로젝트의 에셋을 참조해서는 안됩니다. 본 프로젝트에서 분리된 에셋들이 다시 본 프로젝트의 에셋을 참조할 경우, 분리된 최상위 폴더의 이주는 본 프로젝트의 에셋까지 함께 이주해버리며 간편한 이주를 불가능하게 만듭니다. 

프로젝트 최상위 폴더에서 분리된 최상위 폴더로의 방향으로만 참조가 이루어져야 모듈화된 에셋 그룹이라는 장점이 보장됩니다. 이렇게 분리된 최상위 폴더는 개념상 모듈화된 에셋 그룹이 되어, 에셋을 변경해 다른 프로젝트에 패치로서 이주하거나, 다른 프로젝트로부터 다시 이주해와 패치를 적용하는 일을 분리된 최상위 폴더의 이주만으로 간단히 가능하게 만들어주며 본 프로젝트에 영향을 최소화해줍니다.

<br>

### 2.3 로컬 테스트는 `Developers` 폴더 내에서 해야합니다.

팀원들은 프로젝트에 영향을 끼치지 않으면서도 자유롭게 이런저런 실험을 해보기를 원할 수 있습니다. 다른 팀원과 공유될 필요가 전혀 없는 완전히 실험적인 에셋을 `소스컨트롤(VLAST의 경우 PlasticSCM)`에 추가하는 행위는 프로젝트의 디렉터리 구조를 혼잡하게 만들며, 팀원이 실수로 완전히 실험적인 에셋을 사용할 위험까지 생기게 됩니다. 이러한 실험적인 에셋을 소스컨트롤에 제출한 채로 장기간 방치할 경우, 그것의 제거는 광범위한 문제를 일으킬 수도 있습니다.

소스컨트롤에 영향을 끼치지 않으며 마음껏 테스트해보기 위해 사본 프로젝트를 만든 뒤 사본 프로젝트에 테스트 환경을 구축할 수도 있지만, 보다 나은 방법은 `Developers` 폴더를 이용하는 것입니다.

`Developers` 폴더는 로컬에만 존재하는 완전히 실험적인 에셋이 저장되는 공간입니다. `Developers` 폴더 내의 환경은 프로젝트 소스컨트롤과 분리된 완전히 개인화된 실험실 같은 것입니다. 따라서 소스컨트롤은 `Developers` 폴더 내의 어떠한 에셋도 관리하지 않으며, 실수 또는 모종의 이유로 `Developers` 폴더 내의 에셋이 체크인되었다 하더라도 팀원들은 `Developers` 폴더 내의 어떠한 에셋도 참조해서는 안됩니다. `Developers` 폴더에서 충분한 실험이 이루어져 프로젝트 폴더로 이동해도 되겠다는 판단이 설 경우, 해당 에셋을 올바른 경로로 이동시킨 뒤 리디렉터를 고쳐주기만 하면 됩니다.

`Developers` 폴더는 콘텐츠 브라우저에서 기본적으로 숨겨져 있습니다. 콘텐츠 브라우저 세팅의 `개발자 콘텐츠 표시(Show Developers Content)` 항목을 체크해야 콘텐츠 브라우저에 노출됩니다. 

`Developers` 폴더 내의 모든 에셋은 `소스컨트롤(PlasticSCM)`의 `ignore.conf` 설정에 의해 무시되도록 설정되어있습니다. 하지만 에디터 개인설정에서 `변경 시 새 파일 추가(Add New Files when Modified)` 옵션이 켜져있을 경우, `Developers` 폴더 내에 에셋을 추가할 경우 `ignore.conf` 규칙을 무시한 채 체크인 대기 항목에 올라가며 소스컨트롤에 잘못 체크인할 확률을 높이게 됩니다. 이 항목을 꺼두었다 하더라도 `Saved` 폴더를 삭제할 경우 에디터 개인설정이 엔진 기본설정으로 초기화됩니다.  
때문에 `Developers` 폴더를 완전히 개인화된 실험실로 사용하기 위해서는 [Developers 폴더 사용 편의를 위한 설정](#0221-developers-폴더-사용-편의를-위한-설정)이 되어있어야 합니다.

<br>

### 2.4 모든 레벨 에셋은 `Maps` 폴더 내에 위치해야 합니다.

<br>

### 2.5 프로젝트에 핵심적인 블루프린트 및 기타 에셋은 `Core` 폴더 내에 위치합니다.

프로젝트의 근본을 이루는 매우 중요한 에셋에는 `Content\Project\Core` 경로를 사용하십시오. 예를 들어 프로젝트의 기본이 되는 `GameMode`, `Character`, `PlayerController`, `GameState`, `PlayerState`와 이와 관련된 블루프린트 등이 여기에 위치할 수 있습니다.

`Core` 폴더를 사용하면 팀원들에게 이 안의 에셋은 수정해선 안된다는 사실을 명확히 암시할 수 있습니다. 아티스트들이 흔히 접근하는 경로에는 `Core` 블루프린트로부터 파생된 자식 블루프린트들이 위치하게 되며, 아티스트들은 `Core` 블루프린트를 직접 다루는 대신 그 자식을 다루며 게임 플레이를 제작하게 됩니다. 이 가이드에 따라 아티스트들은 `Core` 폴더에 접근할 이유가 거의 사라지게 됩니다.

예를 들어, 프로젝트에는 레벨에 배치할 수 있는 기본 아이템 클래스가 존재할 수 있으며, 그 기본 동작을 정의한 클래스가 `Content\Project\Core\Item`에 위치할 수 있습니다. 게임 디자이너가 흔히 접근하는 경로에는 이 부모 블루프린트로부터 파생된 자식 블루프린트가 존재하며, 게임 디자이너는 자유롭게 이 파생 블루프린트를 조정하며 게임 플레이를 구성할 수 있습니다. 이러한 분리는 게임 디자이너가 `Core`에 정의된 부모 블루프린트를 직접 수정해 프로젝트 전체에 문제를 일으키는 일을 방지합니다.


<br>

### 2.6 이름이 `Assets`인 폴더를 만들지 마십시오.

`Assets` 폴더가 암묵적으로 3D 에셋들에 사용되는 경로임을 알지만, 3D 에셋 외의 모든 에셋들도 `Assets`이기에 이 스타일 가이드에서는 권장하지 않습니다.  
이 스타일 가이드는 메가스캔의 스타일에 영향을 받아 3D 에셋들에는 `3D_Assets` 경로를 사용합니다.

<br>

### 2.7 이름이 `Meshes`, `Textures`, `Materials`인 `에셋유형` 폴더를 만들지 마십시오.

이 규칙은 `3D_Assets`, `3D_Plants`, `Surfaces`, `Decals` 등 폴더 내의 에셋이 주로 `스태틱 메시`, `머티리얼`, `텍스처` 유형인 폴더들에 강제됩니다.  
예외 상황은 [`Characters` 폴더 이하에는 적용하지 않음](#271-characters-이하-폴더에는-적용하지-않음)를 확인해주세요.

모든 에셋 이름은 이미 접두사에 자신의 에셋 유형을 담고있습니다. `Meshes`, `Textures`, `Materials`와 같은 에셋 유형 폴더는 중복된 정보를 제공할 뿐입니다.

잘 정리된 에셋 이름은 이미 접두사에 의해 유형별로 잘 정돈되어 폴더에 추가로 정리하는 것의 이득이 적습니다. 만일 특정 유형의 에셋만 모아서 보고 싶다면, `콘텐츠 브라우저`의 `필터 기능`을 이용하는 것으로 에셋유형 폴더를 간단히 대체할 수 있습니다. 스태틱 메시만을 보고싶다면, `Meshes` 폴더에 정리하는 대신 단지 `스태틱 메시 필터`를 켜기만 하면 됩니다. 머티리얼과 텍스처만 보고싶다면, `Materials`, `Textures` 폴더에 정리하는 대신 `머티리얼과 텍스처 필터`를 켜기만 하면 됩니다. 

이 규칙은 불필요하게 깊어진 폴더 구조를 간소화해 폴더 탐색 피로도를 줄여줍니다. 또한 이러한 유형의 에셋을 자주 임포트해야하는 아티스트들이 `Materials` 폴더에 텍스처를 넣는 등의 실수도 방지해줍니다. 전체 파일경로 길이를 줄여주며 `쿠킹 파일 경로 길이` 제한에 걸리는 일도 줄여줍니다.

이 규칙의 핵심은 3D 에셋 폴더들을 에셋유형 단위로 해체하지 않고 실제로 월드에 배치될 개체 단위로 `폴더 자체를 개체화`하는 데 있습니다.

<pre>
|-- Content
    |-- ProjectName
      |-- 3D_Assets
          |-- Building
              |-- Balcony
              |-- Wall
          |-- Nature
              |-- Rock
              |-- Tree
          |-- Props
              |-- Book
              |-- OldWoodenBench
      |-- 3D_Plants
          |-- Desert
              |-- Cactus
              |-- DesertYellowHead
          |-- Arctic
              |-- Moss
      |-- Decals
          |-- Concrete
          |-- Blood
          |-- Metal
      |-- Surfaces
          |-- Grass
          |-- Asphalt
          |-- Fabric
</pre>

다음과 같이 실제로 배치될 개체 단위로 잘 정리된 폴더구조는 아티스트가 `Meshes`와 같은 불필요한 에셋유형 정보가 아닌, 실제로 찾으려는 `개체이름`에 집중해 폴더를 탐색할 수 있게 해줍니다. 개체이름의 폴더 안에는 그 개체에 필요한 모든 `스태틱 메시`, `머티리얼`, `텍스처` 등이 포함되어있으며, 아티스트는 콘텐츠 브라우저의 필터링 시스템을 활용해 구체적인 에셋 유형을 찾으면 됩니다.


#### 2.7.1 `Characters` 이하 폴더에는 적용하지 않음.

캐릭터 에셋은 개체폴더 내에 `스켈레탈 메시`, `머티리얼`, `텍스처` 외에도 `애니메이션 블루프린트`, `애니메이션 시퀀스`, `블루프린트`, `애니메이션 몽타주`, `피직스 에셋`, `사운드` 등 매우 다양한 에셋유형을 가지게 되며, 단순한 3D 모델이나 재질 에셋과는 달리 체계적으로 구조화됩니다.  

이러한 특징을 가지는 폴더에까지 [2.7](#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오)의 규칙을 적용하는 것은 콘텐츠 브라우저에 5개 이상의 다양한 필터를 준비해두게 만들어 필터 시스템의 전반적인 편의 자체를 해치게 됩니다. 또한 [2.7](#27-이름이-meshes-textures-materials인-에셋유형-폴더를-만들지-마십시오)의 규칙은 캐릭터와 같은 복잡하게 구조화된 폴더에는 적합하지 않습니다.  

따라서, `Characters` 경로 이하의 캐릭터 폴더들은 다음과 같은 관습적인 스타일을 따라 `에셋유형` 폴더를 만들어줍니다. 
<pre>
|-- Content
    |-- ProjectName
      |-- Characters
          |-- Nina
              |-- Audio
              |-- Animations
              |-- Blueprints
              |-- Meshes
              |-- Materials
              |-- Textures
</pre>

<br>

### 2.8 여러 에셋과 공유되는 에셋들은 `Common` 폴더 내에 위치합니다.

다른 개체 에셋들과 쉽게 공유되고 호환되는 특정 에셋 유형들이 있습니다. 가장 일반적인 예는 `애니메이션`과 `오디오` 에셋입니다. 

예를 들어, `애니메이션`의 경우 여러 스켈레톤에 걸쳐 공유되는 애니메이션이 있을 수 있습니다. UE5에서부터는 유사한 본 구조를 지닌 캐릭터 사이에서의 애니메이션 공유가 특히 쉬워졌으므로, 이런 유형의 에셋들에 `Content\Project\Characters\Common\Animations`와 같은 경로를 적용할 수 있습니다.

<br>

### 2.9 `MaterialLibrary`

프로젝트 전체에 걸쳐 광범위하게 사용되는 `마스터 머티리얼`, `머티리얼 함수`, `텍스처` 등은 `Content/Project/MaterialLibrary` 경로에 있어야 합니다.

이 규칙은 아티스트들이 `머티리얼 인스턴스만 사용` 규칙을 따르는 것을 매우 쉽게 만들어줍니다. 프로젝트에 `머티리얼 인스턴스만 사용` 정책을 사용할 경우, 전체적인 룩에 변경이 필요할 때 3D 에셋 각각의 머티리얼을 수정할 필요 없이 마스터 머티리얼 하나만 변경하는 것으로 전체에 변경사항을 적용할 수 있습니다. `머티리얼 인스턴스만 사용` 정책은 생산성을 높이고 유지보수를 쉽게 만들어주며, `MaterialLibrary` 폴더의 사용은 정책을 따르는 것을 쉽게 만들어줍니다. 

`MaterialLibrary`는 순수 머티리얼만으로 구성되지 않습니다. 프로젝트 전체에 사용되는 `텍스처`, `머티리얼 함수`, 또는 이러한 목적을 지닌 셰이더 관련 에셋들은 모두 `MaterialLibrary` 이하에 위치합니다. 예를 들어, 공용 노이즈 텍스처는 `Content\Project\MaterialLibrary\Textures` 경로에 위치하며, 공용 노이즈 함수는 `Content\Project\MaterialLibrary\Functions` 경로에 위치합니다.

모든 테스트 또는 디버깅을 위한 머티리얼은 `MaterialLibrary\Debug` 폴더 내에 있어야 합니다. 이는 프로젝트가 배포용으로 패키징되기 이전에 디버깅을 위한 요소들을 제거하는 것을 쉽게 만들어주며, 참조 오류가 발생할 경우 디버깅을 위한 에셋을 사용하고 있지는 않은지 확인하는 것을 쉽게 만들어줍니다.

<br>

### 2.10 리디렉터, 비어있는 폴더

에셋의 이름 또는 경로 변경은 그 자리에 동일한 이름의 리디렉터 파일을 남기게 됩니다. 이를 인식하지 못하고 다시 리디렉터와 동일한 이름으로 파일을 생성하거나 가져올 경우, 리디렉터로 덮어씌워지며 파일이 사라져 작업사항을 잃어버릴 수 있습니다. 

리디렉터의 제거는 콘텐츠 브라우저에서 폴더를 우클릭한 뒤 `폴더의 리디렉터 고치기(Fix Up Redirectors in Folder)`로 수행할 수 있으며, 에셋의 이름이나 경로를 변경한 후에는 곧바로 리디렉터를 고쳐줘야 합니다.

`Content` 폴더 안에 빈 폴더를 남겨두지 마십시오. 만약 삭제되지 않는 빈 폴더가 있다면, 폴더 내에 리디렉터 파일이 있는 것입니다. `폴더의 리디렉터 고치기` 기능으로 리디렉터를 제거한 뒤 빈 폴더를 삭제해주세요. 리디렉터는 기본적으로 감춰져있으며, 콘텐츠 브라우저 설정을 통해 볼 수 있습니다.

**[⬆ Back to Top](#목차)**

<br>
<br>
<br>
<br>

## 3. 블루프린트 코딩 표준

<br>

### 시작하기 전
`친숙한 변수 이름 보기(Show Friendly Name)`를 끄는 것은 블루프린트 코딩 표준 준수 과정에서의 불필요한 혼란을 줄여줍니다. Saved 폴더를 삭제해도 항상 이 설정이 적용되도록 하려면 [블루프린트 코딩 표준 준수를 위한 설정](#0222-블루프린트-코딩-표준-준수를-위한-설정)을 따라 설정해주시면 됩니다.

`친숙한 변수 이름 보기`로 인해 발생할 수 있는 혼란은 다음과 같습니다.  
사진  
1. 접두사 b-가 자동으로 생략됨
1. 단어의 첫 문자가 대문자로 변경되며 [카멜 케이스](#카멜-케이스-camelcase)와 [파스칼 케이스](#파스칼-케이스-pascalcase)를 구분할 수 없어짐
1. [파스칼 케이스](#파스칼-케이스-pascalcase)의 단어구분 사이에 자동으로 공백이 추가됨
1. 밑줄이 자동으로 공백으로 변환됨
1. 3-4의 문제로 겉보기상 동일한 변수명에 [파스칼 케이스](#파스칼-케이스-pascalcase), [스네이크 케이스](#스네이크-케이스-snake_case), [공백](#011-금지된-문자)이 모두 사용되는 문제 발생  

`친숙한 변수 이름 보기`를 끄는 것은 모두가 변수 이름을 원형 그대로 볼 수 있도록 하여 이러한 혼란을 피하게 해줍니다.

<br>

### 3.0 기본 원칙

1. 코드 자체가 문서 역할을 하도록, 가독성을 최우선으로 삼아야 합니다.
2. 컴파일과 런타임 모두에서 단 하나의 경고나 오류도 없어야 합니다.

<br>

### 3.1 컴파일과 런타임

#### 3.1.1 컴파일

모든 블루프린트는 반드시 컴파일 결과에 경고 및 오류가 없어야 합니다. 블루프린트 경고 및 오류는 예기치 못한 동작으로 이어질 수 있으므로 발견 즉시 고쳐야 합니다.

망가진 블루프린트는 잘못된 참조, 예상치 못한 실행결과, 쿠킹 실패, 잦은 재컴파일 등 여러 문제를 일으킵니다. 망가진 블루프린트의 방치는 프로젝트 전체를 망가뜨리므로, 컴파일되지 않는 블루프린트를 소스컨트롤에 제출하지 마십시오.

#### 3.1.2 런타임

런타임이란 게임의 실행 도중을 의미합니다. 컴파일 결과에 경고 및 [오류](#오류)가 없었다 할지라도, 런타임 도중에 문제가 발생할 수도 있습니다. 예를 들어 컴파일할 때는 정상적으로 참조하던 개체가 런타임 도중 Destroy 되었는데 다시 참조하는 경우, 런타임 도중 None 참조 오류가 발생하게 됩니다. 또한 런타임 중에는 프로그램 로직 자체의 결함으로 [버그](#버그)가 발생할 수 있습니다. 런타임 도중 이런 문제를 발견하는 즉시 원인을 파악하고 고쳐야합니다. 

경고는 지금 당장 문제를 일으키지는 않기 때문에 가볍게 여겨지고 방치되기 쉽습니다. 방치된 채 누적된 경고는 언젠가 정말 중요한 문제가 발생했을 때 경고 사이에서 정말 중요한 단서를 찾아내는 일을 어렵게 만드므로, 경고도 발견 즉시 고쳐야 합니다.

<br>

### 3.2 변수

[변수와 프로퍼티](#변수variable와-프로퍼티property)는 일반적인 문맥에서 서로 바꿔서 사용할 수 있습니다. 블루프린트에서는 변수 용어 사용이 흔하므로, 이 스타일 가이드에서는 프로퍼티도 모두 변수로 표현합니다. 

#### 3.2.1 변수 이름은 명사여야 합니다.
변수 이름은 그 자체로 명확하게 이해할 수 있는 명사여야 합니다.  
누구나 이해할 수 있도록 충분히 설명적인 명사여야 하며, 지나친 축약을 피해야 합니다.

*[불리언 변수](#324-불리언-변수는-is-can-has-should와-같은-의문형-동사를-가질-수-있습니다)는 동사가 사용될 수 있습니다.*


#### 3.2.2 Public 변수에는 파스칼 케이스를 사용합니다.
기본적으로 모든 변수 이름은 [파스칼 케이스](#파스칼-케이스-pascalcase)를 따릅니다.  
불리언 변수와 Public 이외의 변수에는 특정한 접두사가 붙습니다.

즉, [불리언을 제외한](#323-불리언-변수는-b--접두사를-가집니다) `모든 Public 변수`는 [파스칼 케이스](#파스칼-케이스-pascalcase)를 따릅니다.  

*불리언이 아닌 Public 변수 이름의 예:*
* `Score`
* `Kills`
* `TargetPlayer`
* `Range`
* `PlayerID`


#### 3.2.3 불리언 변수는 b- 접두사를 가집니다.
모든 `불리언 변수`는 `소문자 b`를 접두사로 가집니다.

예를 들어 사망 상태를 체크하는 변수는 `Dead`에 `b-`를 붙여 `bDead`가 되어야 합니다.

#### 3.2.4 불리언 변수는 Is, Can, Has, Should와 같은 의문형 동사를 가질 수 있습니다.
몇몇 스타일 가이드에서는 불리언 변수에 동사를 사용하는 것은 함수와 혼동을 일으키므로 사용을 금지하고 있습니다. 하지만 예/아니오를 담는 불리언 변수에 접근할 때 그 이름이 의문형인 것은 자연스러우며, 더 나은 가독성을 제공합니다.  

`불리언 변수`에는 `b-` 접두사가 오기 때문에 함수와의 혼동을 피할 수 있고 에픽의 코딩 표준도 불리언 변수에 의문형 동사를 사용하므로, 이 스타일 가이드에서는 불리언 변수에 의문형 동사를 허용합니다.

*다음은 모두 올바른 이름입니다.* 
* `bDead`
* `bIsDead`
* `bHostile`
* `bIsHostile`
* `bAlive`
* `bHasChild`


#### 3.2.5 불리언 변수로 복잡한 상태를 정의하지 마십시오.
불리언 변수는 언제나 변수 하나로 하나의 상태를 온전히 정의할 수 있어야 합니다. 하나의 상태를 온전히 정의하는 데 두 개 이상의 불리언 변수가 필요하다면 `열거형`을 사용하십시오.

예를 들어 캐릭터의 걸음걸이 상태를 정의하는 상황을 가정해보겠습니다. `캐릭터의 걸음걸이`에는 `Walking`, `Running`, `Sprinting` 등 `세 가지 이상의 상태`가 존재할 수 있습니다.
이런 상태를 불리언으로 정의하려면 각각의 상태에 각각의 변수 `bWalking`, `bRunning`, `bSprinting`가 필요하며, 하나의 상태를 정의하기 위해선 다른 모든 상태 변수를 false로 변경해줘야 합니다. 여기에 기어가거나 절뚝거리는 상태가 또다시 추가된다면 로직의 크기에 따라 이 작업은 매우 번거로워질 수 있습니다. 불리언 대신 `열거형`을 사용하면 `PlayerWalkState` 변수 하나로 상태를 정의할 수 있으며, 상태의 추가/제거도 간편해집니다.

#### 3.2.6 private, protected 변수에는 접두사 m-을 붙입니다.

`Public`, `protected`, `private`에 대한 설명은 [접근 제어자](#접근-제어자-access-modifier) 항목을 참고해주세요.

##### 3.2.6.1 private 변수
외부에서 접근해서는 안되며 자식 블루프린트에서도 사용해서는 안되는 게 확실한 변수는 [private](#private)로 설정하십시오. 즉, 현재 클래스 내부에서만 사용할 것이 확실한 변수는 [private](#private)로 설정해야 합니다. 이런 변수를 [private](#private)로 선언하는 것은 변수의 외부 노출을 원천 차단해 게임 디자이너가 블루프린트를 더 안전하게 사용할 수 있도록 해줍니다.

[private](#private) 변수에는 접두사 `m-`을 붙입니다. 모든 변수에 파스칼 케이스만을 사용하면 어떤 변수가 private인지 확인하기 위해서는 매번 변수의 디테일 패널을 확인해야 합니다. `private 변수`에 접두사 `m-`을 붙이면 내부용 변수가 명확히 보이므로 코드 작성이 편리해집니다.

##### 3.2.6.2 protected로 의도된 변수
블루프린트 변수는 [protected](#protected) 접근 제어자를 지원하지 않습니다. 때문에 현재로서는 자식 클래스에서도 사용되거나 잠재적으로 그럴 가능성이 있는 변수는 [Public](#public)으로 열어둘 수밖에 없습니다. 

이처럼 외부에서 접근해서는 안되지만 불가피하게 Public으로 공개된 변수의 문제를 보완하기 위해, `protected로 의도된 변수`에도 접두사 `m-`을 붙이십시오. 이 규칙을 따르면 외부에서 접근하는 사용자는 `m` 접두사가 붙은 변수는 내부용임을 알고 접근하지 않을 것입니다.

이 문제는 `외부에서는 언제나 함수 호출로 변수 접근` 규칙으로 추가로 보완됩니다.

##### 3.2.6.3 private/protected 변수 이름 예시
즉, `Public이 아닌 모든 변수`에는 `접두사 m-`이 붙습니다. 추가로 `불리언 변수는 접두사 b-가 뒤이어 오게 됩니다.`  

*이 규칙에 따른 예는 다음과 같습니다.*
* `mbFired`  
* `mAge`
* `mName`
* `mProcessState`

#### 3.2.7 변수가 속한 클래스를 고려해 불필요한 의미 중복을 피하십시오.
클래스의 변수들은 이미 그 클래스에 소속되어있음이 명확합니다. 이런 문맥을 고려하지 않은 의미 중복을 피하십시오.

예를 들어 `BP_PlayerCharacter` 개체의 변수에 접근하는 상황을 가정해봅니다.

*나쁜 예:*
* `PlayerScore`
* `PlayerKills`
* `MyCharacterName`
* `CharacterSkills`
* `CharacterSkin`

호출자 입장에서 이런 변수의 호출은 `BP_PlayerCharacter.PlayerScore` 형태가 됩니다. 이미 `PlayerCharacter` 소속임이 명확하므로 `BP_PlayerCharacter.Score` 형태가 되는 것이 더 바람직합니다.

*좋은 예:*
* `Score`
* `Kills`
* `Name`
* `Skills`
* `Skin`


#### 3.2.8 기본 자료형 변수에 자료형 이름을 포함하지 마십시오.
`기본 자료형`에는 `불리언(Bool)`, `정수(Int)`, `실수(Float)`, `열거형(Enum)` 등이 있습니다. `문자열(String)`과 `벡터(Vector)`는 기본 자료형은 아니지만 `블루프린트에서는 기본 자료형처럼 간주`됩니다.  
>	텍스트(Text) 변수는 기본 자료형으로 간주되지 않습니다. 텍스트 변수는 현지화 기능을 숨기고 있습니다. 기본 자료형으로 간주하는 문자열 형태의 변수는 문자열(String) 변수입니다.

*잘못된 예:*
* `ScoreFloat`
* `FloatDamage`
* `DescriptionString`

기본 자료형 이름과 유사하거나 겹치더라도, `NumPosts`, `PostsCount`, `PlayerName`과 같이 문맥상 단지 일반 명사로서 사용된 경우라면 해당하지 않습니다.


#### 3.2.9 배열은 복수형 이름을 가져야 합니다.

*나쁜 예:*
* `TargetList`
* `HatArray`
* `EnemyPlayerArray`

*좋은 예:*
* `Targets`
* `Hats`
* `EnemyPlayers`

#### 3.2.10 구조체의 멤버변수는 모두 파스칼 케이스를 따릅니다.

#### 3.2.11 런타임 중 변경되어선 안되는 상수
컴파일 단계에서 값을 결정하고 런타임 중 절대 변경되어선 안되는 변수는 `블루프린트 읽기 전용(Blueprint Read Only)`으로 선언해줍니다. 

변수 이름은 [스네이크 표기법](#스네이크-케이스-snake_case)을 따르되, `모든 문자를 대문자`로 표시해 `상수`임을 알립니다.

게임 또는 개체의 초기화 단계에서 값을 읽어와 설정한 뒤 나머지 시간동안 변경되어선 안되는 `상수 성격의 변수`도 같은 이름 규칙을 따릅니다.

*상수, 상수형 변수 이름의 올바른 예:*
* `PLAYER_HP`
* `TARGET_FPS`
* `NUM_PLAYERS`

#### 3.2.12 변수 툴팁
모든 `인스턴스 편집 가능(Instance Editable)`, `스폰시 노출(Exposure on Spawn)` 변수는 툴팁으로 이 변수가 블루프린트 동작에 어떤 영향을 미치는지에 대한 설명을 제공해야 합니다. 

그렇지 않은 변수라도 변수 이름만으로 변수의 목적이 명확히 드러나지 않을 경우 툴팁으로 설명을 보충할 수 있습니다.

#### 3.2.13 슬라이더 및 값 범위

특히 `인스턴스 편집 가능 변수`에서 변수에 허용되지 않는 값이 있을 경우 `슬라이더`로 변수의 값을 제한해줘야 합니다. 예를 들어 절차적으로 울타리를 생성하는 블루프린트의 경우 `FenceCount` 변수에 음수를 입력하는 것은 아무런 의미가 없습니다. 슬라이더 최소값을 0으로 제한해 방지할 수 있습니다. 또한, 지나치게 큰 값을 입력해 에디터를 망가뜨리는 것을 막기 위해 정상범위라 생각하는 최대값도 설정해주면 좋습니다.

특히 슬라이더 최댓값 설정은 해당 변수가 `컨스트럭션 스크립트`에서 사용될 때 중요합니다. 최댓값이 설정되어있지 않으면 드래그 실수로 지나치게 큰 값을 입력하기 쉬우므로, 실수로 인해 에디터 크래시가 나지 않도록 적절한 최댓값을 설정해야 합니다.
	
슬라이더는 값을 드래그할 때 허용되는 범위를 제한할 뿐, 실제 값의 입력을 제한하지는 않습니다. `값 범위`는 실제로 입력될 수 있는 값 자체를 제한하므로, 변수에 허용되는 값 범위가 명확한 경우 정의해줍니다.

#### 3.2.14 카테고리
클래스가 적은 수의 변수만 가지고 있다면 `카테고리`는 필요하지 않습니다.

만약 클래스가 한 눈에 파악하기 어려운 많은 변수를 가진다면, 카테고리로 분류하여 사용자가 변수의 용도를 파악하기 쉽게 해야합니다. `인스턴스 편집 가능 변수`들은 사용자에게 개체의 기본설정을 위한 변수라는 것을 암시하기 위해 `Config` 카테고리에 할당됩니다.

변수 분류의 계층이 깊다면 `|` 를 사용해 하위 카테고리를 만들 수 있습니다. 

*무기 클래스 변수들의 카테고리 예:*

    |-- Config
    |    |-- Animations
    |    |-- Effects
    |    |-- Audio
    |    |-- Recoil
    |    |-- Timings
    |-- Animations
    |-- State
    |-- Visuals

#### 3.2.15 고급 디스플레이 옵션
변수가 수정 가능해야 하기는 하지만 매우 드물게 수정되거나 그 변수에 대해 잘 아는 사람이 아니라면 수정하기를 원치 않을 경우, `고급(Advanced)` 설정의 `고급 디스플레이(Advanced Display)` 옵션으로 변수를 접어 가려줍니다.

#### 3.2.16 기타 `고급(Advanced)` 변수 설정
C++ 수준의 이해도를 가진 작업자가 아니라면 `환경설정 변수(Config Variable)`, `트랜션트(Transient)` 등의 설정은 사용하지 않습니다.

<br>

### 3.3 함수(Functions), 이벤트(Events), 이벤트 디스패처(Event Dispatchers)

This section describes how you should author functions, events, and event dispatchers. Everything that applies to functions also applies to events, unless otherwise noted.

<a name="3.3.1"></a>
<a name="bp-funcs-naming"></a>
#### 3.3.1 Function Naming

The naming of functions, events, and event dispatchers is critically important. Based on the name alone, certain assumptions can be made about functions. For example:

* Is it a pure function?
* Is it fetching state information?
* Is it a handler?
* Is it an RPC?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

<a name="3.3.1.1"></a>
<a name="bp-funcs-naming-verbs"></a>
#### 3.3.1.1 All Functions Should Be Verbs

All functions and events perform some form of action, whether its getting info, calculating data, or causing something to explode. Therefore, all functions should all start with verbs. They should be worded in the present tense whenever possible. They should also have some context as to what they are doing.

`OnRep` functions, event handlers, and event dispatchers are an exception to this rule.

Good examples:

* `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class.
* `Jump` - Good example if in a Character class, otherwise, needs context.
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy` - ["Is" is a verb.](http://writingexplained.org/is-is-a-verb)

Bad examples:

* `Dead` - Is Dead? Will deaden?
* `Rock`
* `ProcessData` - Ambiguous, these words mean nothing.
* `PlayerState` - Nouns are ambiguous.
* `Color` - Verb with no context, or ambiguous noun.

<a name="3.3.1.2"></a>
<a name="bp-funcs-naming-onrep"></a>
#### 3.3.1.2 Property RepNotify Functions Always `OnRep_Variable`

All functions for replicated with notification variables should have the form `OnRep_Variable`. This is forced by the Blueprint editor. If you are writing a C++ `OnRep` function however, it should also follow this convention when exposing it to Blueprints.

<a name="3.3.1.3"></a>
<a name="bp-funcs-naming-bool"></a>
#### 3.3.1.3 Info Functions Returning Bool Should Ask Questions

When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a yes/no value, it should ask a question. This should also follow [the verb rule](#bp-funcs-naming-verbs).

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether that action succeeded.

Good examples:

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'.
* `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

Bad examples:

* `Fire` - Is on fire? Will fire? Do fire?
* `OnFire` - Can be confused with event dispatcher for firing.
* `Dead` - Is dead? Will deaden?
* `Visibility` - Is visible? Set visibility? A description of flying conditions?

<a name="3.3.1.4"></a>
<a name="bp-funcs-naming-eventhandlers"></a>
#### 3.3.1.4 Event Handlers and Dispatchers Should Start With `On`

Any function that handles an event or dispatches an event should start with `On` and continue to follow [the verb rule](#bp-funcs-naming-verbs). The verb may move to the end however if past-tense reads better.

[Collocations](http://dictionary.cambridge.org/us/grammar/british-grammar/about-words-clauses-and-sentences/collocation) of the word `On` are exempt from following the verb rule.

`Handle` is not allowed. It is 'Unreal' to use `On` instead of `Handle`, while other frameworks may prefer to use `Handle` instead of `On`.

Good examples:

* `OnDeath` - Common collocation in games
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

Bad examples:

* `OnData`
* `OnTarget`
* `HandleMessage`
* `HandleDeath`

<a name="3.3.1.5"></a>
<a name="bp-funcs-naming-rpcs"></a>
#### 3.3.1.5 Remote Procedure Calls Should Be Prefixed With Target

Any time an RPC is created, it should be prefixed with either `Server`, `Client`, or `Multicast`. No exceptions.

After the prefix, follow all other rules regarding function naming.

Good examples:

* `ServerFireWeapon`
* `ClientNotifyDeath`
* `MulticastSpawnTracerEffect`

Bad examples:

* `FireWeapon` - Does not indicate its an RPC of some kind.
* `ServerClientBroadcast` - Confusing.
* `AllNotifyDeath` - Use `Multicast`, never `All`.
* `ClientWeapon` - No verb, ambiguous.


<a name="3.3.2"></a>
<a name="bp-funcs-return"></a>
#### 3.3.2 All Functions Must Have Return Nodes

All functions must have return nodes, no exceptions.

Return nodes explicitly note that a function has finished its execution. In a world where blueprints can be filled with `Sequence`, `ForLoopWithBreak`, and backwards reroute nodes, explicit execution flow is important for readability, maintenance, and easier debugging.

The Blueprint compiler is able to follow the flow of execution and will warn you if there is a branch of your code with an unhandled return or bad flow if you use return nodes.

In situations like where a programmer may add a pin to a Sequence node or add logic after a for loop completes but the loop iteration might return early, this can often result in an accidental error in code flow. The warnings the Blueprint compiler will alert everyone of these issues immediately.

<a name="3.3.3"></a>
<a name="bp-graphs-funcs-node-limit"></a>
#### 3.3.3 No Function Should Have More Than 50 Nodes

Simply, no function should have more than 50 nodes. Any function this big should be broken down into smaller functions for readability and ease of maintenance.

The following nodes are not counted as they are deemed to not increase function complexity:

* Comment
* Route
* Cast
* Getting a Variable
* Breaking a Struct
* Function Entry
* Self

<a name="3.3.4"></a>
<a name="bp-graphs-funcs-description"></a>
#### 3.3.4 All Public Functions Should Have A Description

This rule applies more to public facing or marketplace blueprints, so that others can more easily navigate and consume your blueprint API.

Simply, any function that has an access specificer of Public should have its description filled out.

<a name="3.3.5"></a>
<a name="bp-graphs-funcs-plugin-category"></a>
#### 3.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name

If your project includes a plugin that defines `static` `BlueprintCallable` functions, they should have their category set to the plugin's name or a subset category of the plugin's name.

For example, `Zed Camera Interface` or `Zed Camera Interface | Image Capturing`.

<a name="3.4"></a>
<a name="bp-graphs"></a>
### 3.4 Blueprint Graphs

This section covers things that apply to all Blueprint graphs.

<a name="3.4.1"></a>
<a name="bp-graphs-spaghetti"></a>
#### 3.4.1 No Spaghetti

Wires should have clear beginnings and ends. You should never have to mentally untangle wires to make sense of a graph. Many of the following sections are dedicated to reducing spaghetti.

<a name="3.4.2"></a>
<a name="bp-graphs-align-wires"></a>
#### 3.4.2 Align Wires Not Nodes

Always align wires, not nodes. You can't always control the size and pin location on a node, but you can always control the location of a node and thus control the wires. Straight wires provide clear linear flow. Wiggly wires wear wits wickedly. You can straighten wires by using the Straighten Connections command with BP nodes selected. Hotkey: Q

Good example: The tops of the nodes are staggered to keep a perfectly straight white exec line.
![Aligned By Wires](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-good.png?raw=true "Aligned By Wires")

Bad Example: The tops of the nodes are aligned creating a wiggly white exec line.
![Bad](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-bad.png?raw=true "Wiggly")

Acceptable Example: Certain nodes might not cooperate no matter how you use the alignment tools. In this situation, try to minimize the wiggle by bringing the node in closer.
![Acceptable](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-acceptable.png?raw=true "Acceptable")

<a name="3.4.3"></a>
<a name="bp-graphs-exec-first-class"></a>
#### 3.4.3 White Exec Lines Are Top Priority

If you ever have to decide between straightening a linear white exec line or straightening data lines of some kind, always straighten the white exec line.

<a name="3.4.4"></a>
<a name="bp-graphs-block-comments"></a>
#### 3.4.4 Graphs Should Be Reasonably Commented

Blocks of nodes should be wrapped in comments that describe their higher-level behavior. While every function should be well named so that each individual node is easily readable and understandable, groups of nodes contributing to a purpose should have their purpose described in a comment block. If a function does not have many blocks of nodes and its clear that the nodes are serving a direct purpose in the function's goal, then they do not need to be commented as the function name and  description should suffice.

<a name="3.4.5"></a>
<a name="bp-graphs-cast-error-handling"></a>
#### 3.4.5 Graphs Should Handle Casting Errors Where Appropriate

If a function or event assumes that a cast always succeeds, it should appropriately report a failure in logic if the cast fails. This lets others know why something that is 'supposed to work' doesn't. A function should also attempt a graceful recover after a failed cast if it's known that the reference being casted could ever fail to be casted.

This does not mean every cast node should have its failure handled. In many cases, especially events regarding things like collisions, it is expected that execution flow terminates on a failed cast quietly.

<a name="3.4.6"></a>
<a name="bp-graphs-dangling-nodes"></a>
#### 3.4.6 Graphs Should Not Have Any Dangling / Loose / Dead Nodes

All nodes in all blueprint graphs must have a purpose. You should not leave dangling blueprint nodes around that have no purpose or are not executed.

**[⬆ Back to Top](#table-of-contents)**


<a name="4"></a>
<a name="Static Meshes"></a>
<a name="s"></a>
## 4. Static Meshes

This section will focus on Static Mesh assets and their internals.

<a name="4.1"></a>
<a name="s-uvs"></a>
### 4.1 Static Mesh UVs

If Linter is reporting bad UVs and you can't seem to track it down, open the resulting `.log` file in your project's `Saved/Logs` folder for exact details as to why it's failing. I am hoping to include these messages in the Lint report in the future.

<a name="4.1.1"></a>
<a name="s-uvs-no-missing"></a>
#### 4.1.1 All Meshes Must Have UVs

Pretty simple. All meshes, regardless how they are to be used, should not be missing UVs.

<a name="4.1.2"></a>
<a name="s-uvs-no-overlapping"></a>
#### 4.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps

Pretty simple. All meshes, regardless how they are to be used, should have valid non-overlapping UVs.

<a name="4.2"></a>
<a name="s-lods"></a>
### 4.2 LODs Should Be Set Up Correctly

This is a subjective check on a per-project basis, but as a general rule any mesh that can be seen at varying distances should have proper LODs.

<a name="4.3"></a>
<a name="s-modular-snapping"></a>
### 4.3 Modular Socketless Assets Should Snap To The Grid Cleanly

This is a subjective check on a per-asset basis, however any modular socketless assets should snap together cleanly based on the project's grid settings.

It is up to the project whether to snap based on a power of 2 grid or on a base 10 grid. However if you are authoring modular socketless assets for the marketplace, Epic's requirement is that they snap cleanly when the grid is set to 10 units or bigger.

<a name="4.4"></a>
<a name="s-collision"></a>
### 4.4 All Meshes Must Have Collision

Regardless of whether an asset is going to be used for collision in a level, all meshes should have proper collision defined. This helps the engine with things such as bounds calculations, occlusion, and lighting. Collision should also be well-formed to the asset.

<a name="4.5"></a>
<a name="s-scaled"></a>
### 4.5 All Meshes Should Be Scaled Correctly

This is a subjective check on a per-project basis, however all assets should be scaled correctly to their project. Level designers or blueprint authors should not have to tweak the scale of meshes to get them to confirm in the editor. Scaling meshes in the engine should be treated as a scale override, not a scale correction.

**[⬆ Back to Top](#table-of-contents)**


<a name="5"></a>
<a name="Niagara"></a>
<a name="ng"></a>
## 5. Niagara

This section will focus on Niagara assets and their internals.

<a name="5.1"></a>
<a name="ng-rules"></a>
### 5.1 No Spaces, Ever

As mentioned in [00.1 Forbidden Identifiers](#00), spaces and all white space characters are forbidden in identifiers. This is especially true for Niagara systems as it makes working with things significantly harder if not impossible when working with HLSL or other means of scripting within Niagara and trying to reference an identifier.

(Original Contribution by [@dunenkoff](https://github.com/Allar/ue5-style-guide/issues/58))


**[⬆ Back to Top](#table-of-contents)**


<a name="6"></a>
<a name="Levels"></a>
<a name="levels"></a>
## 6. Levels / Maps

[See Terminology Note](#terms-level-map) regarding "levels" vs "maps".

This section will focus on Level assets and their internals.

<a name="6.1"></a>
<a name="levels-no-errors-or-warnings"></a>
### 6.1 No Errors Or Warnings

All levels should load with zero errors or warnings. If a level loads with any errors or warnings, they should be fixed immediately to prevent cascading issues.

You can run a map check on an open level in the editor by using the console command "map check".

Please note: Linter is even more strict on this than the editor is currently, and will catch load errors that the editor will resolve on its own.

<a name="6.2"></a>
<a name="levels-lighting-should-be-built"></a>
### 6.2 Lighting Should Be Built

It is normal during development for levels to occasionally not have lighting built. When doing a test/internal/shipping build or any build that is to be distributed however, lighting should always be built.

<a name="6.3"></a>
<a name="levels-no-visible-z-fighting"></a>
### 6.3 No Player Visible Z Fighting

Levels should not have any [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) in all areas visible to the player.

<a name="6.4"></a>
<a name="levels-mp-rules"></a>
### 6.4 Marketplace Specific Rules

If a project is to be sold on the UE4 Marketplace, it must follow these rules.

<a name="6.4.1"></a>
<a name="levels-mp-rules-overview"></a>
#### 6.4.1 Overview Level

If your project contains assets that should be visualized or demoed, you must have a map within your project that contains the name "Overview".

This overview map, if it is visualizing assets, should be set up according to [Epic's guidelines](http://help.epicgames.com/customer/en/portal/articles/2592186-marketplace-submission-guidelines-preparing-your-assets#Required%20Levels%20and%20Maps).

For example, `InteractionComponent_Overview`.

<a name="6.4.2"></a>
<a name="levels-mp-rules-demo"></a>
#### 6.4.2 Demo Level

If your project contains assets that should be demoed or come with some sort of tutorial, you must have a map within your project that contains the name "Demo". This level should also contain documentation within it in some form that illustrates how to use your project. See Epic's Content Examples project for good examples on how to do this.

If your project is a gameplay mechanic or other form of system as opposed to an art pack, this can be the same as your "Overview" map.

For example, `InteractionComponent_Overview_Demo`, `ExplosionKit_Demo`.

**[⬆ Back to Top](#table-of-contents)**


<a name="7"></a>
<a name="textures"></a>
## 7. Textures

This section will focus on Texture assets and their internals.

<a name="7.1"></a>
<a name="textures-dimensions"></a>
### 7.1 Dimensions Are Powers of 2

All textures, except for UI textures, must have its dimensions in multiples of powers of 2. Textures do not have to be square.

For example, `128x512`, `1024x1024`, `2048x1024`, `1024x2048`, `1x512`.

<a name="7.2"></a>
<a name="textures-density"></a>
### 7.2 Texture Density Should Be Uniform

All textures should be of a size appropriate for their standard use case. Appropriate texture density varies from project to project, but all textures within that project should have a consistent density.

For example, if a project's texture density is 8 pixel per 1 unit, a texture that is meant to be applied to a 100x100 unit cube should be 1024x1024, as that is the closest power of 2 that matches the project's texture density.

<a name="7.3"></a>
<a name="textures-max-size"></a>
### 7.3 Textures Should Be No Bigger than 8192

No texture should have a dimension that exceeds 8192 in size, unless you have a very explicit reason to do so. Often, using a texture this big is simply just a waste of resources.

<a name="7.4"></a>
<a name="textures-group"></a>
### 7.4 Textures Should Be Grouped Correctly

Every texture has a Texture Group property used for LODing, and this should be set correctly based on its use. For example, all UI textures should belong in the UI texture group.

**[⬆ Back to Top](#table-of-contents)**


## 스타일 변경 이력



