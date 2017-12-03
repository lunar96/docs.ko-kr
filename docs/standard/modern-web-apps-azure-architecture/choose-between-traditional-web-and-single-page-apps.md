---
title: "일반적인 웹 앱 및 단일 페이지 응용 프로그램 중에서 선택"
description: "ASP.NET Core 및 Microsoft Azure로 웹 응용 프로그램을 설계 합니다."
author: ardalis
ms.author: wiwagn
ms.date: 10/06/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.openlocfilehash: 5bae77fc4e0df9d0bc7fecfad25adfcee2419084
ms.sourcegitcommit: bbde43da655ae7bea1977f7af7345eb87bd7fd5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2017
---
# <a name="choose-between-traditional-web-apps-and-single-page-apps-spas"></a>일반적인 웹 앱 및 단일 페이지 응용 프로그램 (SPAs) 중에서 선택

> "Atwood의 법칙: javascript에서 JavaScript에서 작성할 수 있는 응용 프로그램을 작성할 결국 됩니다."  
> _\-제프 Atwood_

## <a name="summary"></a>요약

두 가지 일반적인 방법은 오늘 웹 응용 프로그램을 작성 하려면: 서버 및 웹 브라우저에서 대부분의 사용자 인터페이스 논리를 수행 하는 단일 페이지 응용 프로그램 (SPAs)에서 대부분의 응용 프로그램 논리를 수행 하는 기존 웹 응용 프로그램 기본적으로 웹 Api를 사용 하 여 웹 서버와 통신 합니다. 혼합 접근 방식을 가능, 가장 간단한 되는 하나 이상의 풍부한 SPA 모양의 하위 응용 프로그램을 호스트할 큰 기존 웹 응용 프로그램 내에서.

기존 웹 응용 프로그램을 사용 해야 경우:

-   응용 프로그램의 클라이언트 쪽 요구 사항은 단순 또는 읽기 전용입니다.

-   응용 프로그램에서 JavaScript 지원 하지 않는 브라우저에서 작동 해야 합니다.

-   팀 개발 기술을 JavaScript 또는 TypeScript에 익숙하지 않습니다.

SPA를 사용 해야 경우:

-   응용 프로그램에 다양 한 기능을 다양 한 사용자 인터페이스를 노출 해야 합니다.

-   팀은 JavaScript 또는 TypeScript 개발을 알고 있습니다.

-   이미 응용 프로그램 (내부 또는 공용) 다른 클라이언트에 대 한 API를 노출 해야 합니다.

또한 SPA 프레임 워크 필요한 큰 아키텍처 및 보안 전문 지식을 구할 합니다. 기존 웹 응용 프로그램 보다 자주 업데이트 되 고 새 프레임 워크도 인해 큰 변동이 될 있습니다. 자동화 된 빌드 및 배포 프로세스를 구성 하 고 컨테이너와 같은 배포 옵션을 활용 하는 보다 일반적인 웹 앱 SPA 응용 프로그램과 함께 더 어렵습니다.

SPA 모델을 통해 가능해졌습니다 사용자 경험의 향상 된 이러한 고려 사항에 대 한 가중치가 적용 되어야 합니다.

## <a name="when-to-choose-traditional-web-apps"></a>일반적인 웹 앱을 선택 하는 경우

다음은 자세한 설명은 기존 웹 응용 프로그램을 선택 하는 이전에 명시 된 이유입니다.

**응용 프로그램에 단순, 가능한 읽기 전용으로, 클라이언트 쪽 요구 사항**

많은 웹 응용 프로그램에서 대부분의 사용자에 게는 읽기 전용 방식 주로 사용 됩니다. 읽기 전용 (대부분 읽기 전용인) 응용 프로그램을 유지 하 고 있는 다양 한 상태를 조작 하는 것 보다 훨씬 더 간단 경향이 있습니다. 예를 들어 검색 엔진 textbox 및 검색 결과 표시 하기 위한 두 번째 페이지를 사용 하 여 단일 액세스 지점을 포함 될 수 있습니다. 익명 사용자가 요청을 쉽게 만들 수 및 클라이언트 측 논리에 대 한 필요는 없습니다. 마찬가지로, 블로그 또는 콘텐츠 관리 시스템의 공용 웹 응용 프로그램 일반적으로 작은 클라이언트 쪽 동작으로 콘텐츠의 주로 구성 됩니다. 이러한 응용 프로그램 웹 서버에서 논리를 수행 하 고 브라우저에 표시 되는 HTML을 렌더링 하는 기존 서버 기반 웹 응용 프로그램으로 쉽게 작성 됩니다. 책갈피가 표시 하 고 (기본적으로이 응용 프로그램의 별도 기능으로 추가 하지 않고도) 검색 엔진에서 인덱싱할 수 있는 자체 URL이 사이트의 각 고유 페이지를 갖는다는 사실은 이러한 시나리오에서 분명 한 이점이 이기도 합니다.

**JavaScript 지원 하지 않는 브라우저에서 작동 하기 위해 필요한 응용 프로그램**

제한 되거나 JavaScript가 지원 브라우저에서 작동 하는 웹 응용 프로그램 일반적인 웹 앱 워크플로 사용 하 여 작성 해야 하거나 이러한 동작으로 대체할 수 이상. SPAs 있어야만 클라이언트 쪽 JavaScript 실행 합니다. 사용할 수 없는 경우 SPAs는 적합 하지 않습니다.

**팀은 JavaScript 또는 TypeScript 개발 기법에 익숙하지 않습니다.**

팀은 JavaScript 또는 TypeScript에 익숙하지 않은 서버 쪽 웹 응용 프로그램 개발에 익숙한 다음 항목은 일반적인 웹 앱을는 SPA 보다 더 빨리 제공할 수 있을 경우. 프로그램 SPAs 배우는 목표 이거나는 SPA 제공 사용자 경험 필요, 일반적인 웹 앱은 이미 익숙한을 작성 하는 팀은 생산성을 높일 선택.

## <a name="when-to-choose-spas"></a>SPAs를 선택 하는 경우

웹 앱에 대 한 개발의 단일 페이지 응용 프로그램 스타일을 선택 하는 경우의 자세한 설명은 다음과 같습니다.

**응용 프로그램에서 다양 한 기능을 다양 한 사용자 인터페이스를 노출 해야 합니다.**

SPAs는 사용자가 작업을 수행 하거나 응용 프로그램의 영역 간에 이동 페이지를 다시 로드 필요 하지 않은 다양 한 클라이언트 쪽 기능을 지원할 수 있습니다. SPAs 수 로드 보다 신속 하 게 백그라운드에서 데이터를 인출 하 고 개별 사용자 작업은 전체 페이지가 다시 로드 경우는 드물기 때문에 더 빠르게 대응. SPAs 양식 전송 단추를 클릭 하지는 사용자 없이 부분적으로 완료 된 양식 또는 문서를 저장 하는 증분 업데이트를 지원할 수 있습니다. SPAs는 기존의 응용 프로그램 보다 훨씬 더 쉽게 끌어서 놓기, 등의 리치 클라이언트 동작을 지원할 수 있습니다. SPAs 결국 연결이 다시 설정 되 면 서버에 다시 동기화 되는 클라이언트 쪽 모델을 업데이트할 연결이 끊어진된 모드에서 실행 되도록 지정할 수 있습니다. 응용 프로그램의 요구 사항이 일반적인 HTML 폼의 제공을 초과 하는 다양 한 기능을 포함 하는 경우에 SPA 스타일 적용을 선택 해야 합니다.

SPAs 자주의 주소 표시줄에서 현재 작업을 반영 하 (및 책갈피를 사용자나이 URL에 딥 링크를으로 돌아갈)의 의미 있는 URL을 표시 하는 등 일반적인 웹 앱에 기본 제공 되는 기능을 구현 해야 하는 참고 합니다. 또한 sPAs 편리한 기능을 결과 함께 브라우저의 뒤로 및 앞으로 단추를 사용 하는 사용자가 허용 해야 합니다.

**팀은 JavaScript 또는 TypeScript 개발에 익숙한**

JavaScript 또는 TypeScript 및 클라이언트 쪽 프로그래밍 방법 및 라이브러리를 필요 SPAs 작성 합니다. 팀은 각 같은 SPA 프레임 워크를 사용 하 여 최신 JavaScript 작성에 있으며 수 있어야 합니다.

> ### <a name="references--spa-frameworks"></a>참조-SPA 프레임 워크
> - **AngularJS**  
> <https://angularjs.org/>
> - **4 인기 있는 JavaScript 프레임 워크의 비교**  
> <https://www.developereconomics.com/feature-comparison-of-4-popular-js-mv-frameworks>

**응용 프로그램에 이미 다른 (내부 또는 공용) 클라이언트에 대 한 API를 노출 해야 합니다.**

이미 다른 클라이언트에서 사용 하기 위해 web API를 지원 되는, 하는 경우 서버 쪽 형태로 논리를 재현 하는 대신 이러한 Api를 활용 하 여 SPA 구현을 만들려면 적은 노력을 해야 합니다. SPAs 광범위 하 게 사용 웹 Api의 데이터를 쿼리하고 업데이트 응용 프로그램과 사용자가 조작 합니다.

## <a name="decision-table--traditional-web-or-spa"></a>의사 결정 테이블 – 기존 웹 또는 SPA

다음 의사 결정 테이블에는 기존 웹 응용 프로그램과 SPA 간에 선택할 때 고려해 야 할 기본 요소 중 일부를 요약 합니다.

  | **비율** | **기존 웹 응용 프로그램** | **단일 페이지 응용 프로그램** |
  |---|---|---|
  | JavaScript/TypeScript 필요한 팀 경험 | **최소** | **필수** |
  | 스크립팅 없이 브라우저를 지원 합니다. | **지원됨** | **지원 안 함** |
  | 클라이언트 쪽 응용 프로그램을 최소한의 동작 | **잘 맞는** | **개념을 세우** |
  | 다양 하 고 복잡 한 사용자 인터페이스 요구 사항 | **제한** | **잘 맞는** |

>[!div class="step-by-step"]
[이전] (현대-웹-응용 프로그램-characteristics.md) [다음](architectural-principles.md)