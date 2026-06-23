# 위치 기반 커플 추억 기록 및 데이트 관리 앱

| | |
|---|---|
| **Project Name** | [위치 기반 커플 추억 기록 및 데이트 관리 앱] |
| **Project Manager** | |
| **Company Name** | |
| **Date** | 2026-04-08 |

---
## 1. Project Overview
---
### Category
> Lifestyle / Daily

### Topic
위치 기반 커플 추억 기록 및 데이트 관리 앱

### Background
기존 커플 앱들이 데이트 기록에 어려움을 겪거나, 데이트 아이디어 부족, 관계 소홀, 혹은 식상한 앱 디자인에 대한 불만을 가지고 있습니다. 이러한 문제들을 해결하고, 기술적으로 진보된 기능을 통해 차별화된 경험을 제공하고자 합니다.

### User Problem
커플들이 데이트 기록을 체계적으로 남기기 어렵고, 새로운 데이트 아이디어를 찾기 힘들며, 기존 커플 앱들이 디자인적으로 만족스럽지 못하고 지루하다는 불만이 있습니다.

### Solution
휴대폰 위치 추적 기능을 활용한 데이트 경로 자동 기록 및 지도 시각화, 사진첩 연동 갤러리 일기 작성, 다른 커플들의 방문 장소 추천, 그리고 블랙 앤 화이트 톤의 쿨하고 세련된 UI/UX를 제공하여 이러한 문제들을 해결합니다.

### Differentiator
휴대폰 위치 기반의 데이트 경로 자동 기록 및 지도 시각화 기능이 핵심 차별점입니다. 또한, 기존 앱들과 달리 쿨하고 세련된 블랙 앤 화이트 디자인으로 '귀여움'에서 벗어나 독특한 브랜드 아이덴티티를 구축하며, 다른 커플들의 방문 장소 정보를 공유하여 데이트 아이디어 탐색 기능을 강화합니다.

### Target Users
기술 친화적이고 트렌디한 커플 (20대 후반 ~ 30대 초반). 스마트폰 사용에 능숙하며 새로운 기술과 미니멀한 디자인에 관심이 많고, 자신들만의 특별한 추억을 세련된 방식으로 기록하고 공유하기를 원하는 커플을 대상으로 합니다.

### Usage Scenario
커플이 데이트 중 앱을 켜두면, 앱이 자동으로 이동 경로와 방문 장소를 기록합니다. 데이트를 마친 후, 기록된 경로와 함께 그날 찍은 사진들을 선택하여 갤러리 일기를 작성하고 서로에게 편지를 보냅니다. 일상에서는 앱을 통해 다음 데이트를 위한 디데이를 확인하거나, 다른 커플들이 방문한 인기 장소를 검색하여 새로운 데이트 아이디어를 얻습니다.

### Core Objective
휴대폰 위치 기반으로 둘만의 기록을 지도에 남기고, 이동 거리 확인, 데이트 경로 기록, 사진첩 연동 일기 작성 등을 통해 데이트를 생생하게 기록하고 공유하여 커플 관계를 더욱 돈독하게 만들며, 새로운 데이트 아이디어를 제공하여 관계에 활력을 불어넣는 세련된 경험을 제공합니다.

### Key KPI
월간 활성 사용자 수 (MAU), 주간 데이트 기록 건수, 갤러리 일기 작성 빈도, 앱 내 데이트 장소 추천 기능 사용률, 사용자 유지율 (Retention Rate).

### Risk/Issue
개인 정보(위치 정보) 유출 및 오용에 대한 보안 우려, 배터리 소모량 증가로 인한 사용자 불편, 위치 추적 정확도 문제, 경쟁 앱들의 유사 기능 출시 또는 강력한 마케팅, 블랙 앤 화이트 디자인이 특정 사용자층에게는 매력적이지 않을 수 있다는 점입니다.

### User Roles
> User

### Devices (Devices)
> iOS, Android

## 2. Key Features List
---

## 1. 위치 기반 데이트 기록 및 지도 시각화
> **Priority**: 🔴 High | **Progress**: ⚪ To Do

휴대폰의 위치 추적 기능을 활용하여 데이트 중 이동한 경로를 자동으로 기록하고, 지도 위에 시각적으로 표시하여 둘만의 발자취를 남길 수 있습니다. 이동 거리와 방문 시간을 함께 기록합니다.

**Acceptance Criteria:**
```
1. ○ 사용자 동의 하에 백그라운드에서 위치 정보를 수집하여 이동 경로를 정확히 기록해야 한다.
2. ○ 기록된 이동 경로가 지도 위에 선으로 명확하게 표시되어야 한다.
3. ○ 총 이동 거리 및 데이트 시작/종료 시간이 기록되어야 한다.
4. ○ 기록된 경로를 특정 날짜별로 조회할 수 있어야 한다.
```


### 1.1 위치 권한 요청 및 백그라운드 추적
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

앱 초기 실행 시 사용자에게 위치 접근 권한을 요청하고, 데이트 기록 중 백그라운드에서 지속적으로 위치 정보를 수집합니다.


#### 1.1.1 iOS 위치 권한 요청 구현

iOS 앱 시작 시 사용자에게 '항상 허용', '앱 사용 중만 허용', '거부' 옵션을 포함한 위치 권한 다이얼로그를 표시합니다. Info.plist에 NSLocationWhenInUseUsageDescription 및 NSLocationAlwaysAndWhenInUseUsageDescription을 설정합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS


#### 1.1.2 백그라운드 위치 추적 서비스

데이트 기록 시작 시 백그라운드 위치 서비스를 활성화하여 지속적으로 GPS 좌표(위도, 경도, 정확도, 타임스탬프)를 수집합니다. 배터리 효율성을 위해 5~10초 간격의 위치 업데이트 방식을 사용합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.1.3 위치 수집 동의 및 개인정보 보호 안내

위치 권한 요청 전에 개인정보 수집 및 이용 동의 화면을 표시합니다. 위치 데이터의 용도, 저장 기간, 삭제 방법 등을 명확히 안내합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 1.2 경로 기록 및 지도 시각화
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

수집된 위치 데이터를 바탕으로 이동 경로를 지도 위에 선으로 표시하고, 방문 지점들을 마커로 표현합니다.


#### 1.2.1 경로 선 렌더링

수집된 위치 데이터를 연결하여 지도 위에 경로를 선(polyline)으로 표시합니다. 검은색 또는 흰색 톤의 일관된 색상으로 렌더링합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.2.2 방문 지점 마커 표시

데이트 경로의 시작점, 종료점, 그리고 주요 방문 지점(지정된 위치에서 일정 시간 이상 체류한 곳)을 지도 위에 마커로 표시합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.2.3 지도 상호작용 기능

사용자가 지도를 줌 인/아웃, 드래그, 회전할 수 있도록 지도 조작 기능을 제공합니다. 경로와 마커가 화면에 모두 보이도록 자동 줌 기능을 추가합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.2.4 지도 API 통합

Google Maps API(iOS/Android)를 사용하여 지도를 표시하고, 경로 및 마커를 렌더링합니다. API 키 관리 및 보안을 위해 환경 변수를 활용합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 1.3 이동 거리 및 시간 기록
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

데이트 중 총 이동 거리, 시작 시간, 종료 시간을 자동으로 계산하고 기록합니다.


#### 1.3.1 총 이동 거리 계산

수집된 위치 데이터의 연속된 좌표 간 거리를 Haversine 공식을 사용하여 계산하고, 정확도가 낮은 데이터는 필터링하여 최종 이동 거리를 산출합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.3.2 시작 시간 및 종료 시간 기록

데이트 기록 시작 시 시작 시간을 타임스탬프로 저장하고, 기록 종료 시 종료 시간을 기록합니다. 사용자가 수동으로 조정할 수 있는 옵션도 제공합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.3.3 소요 시간 계산

종료 시간에서 시작 시간을 차감하여 데이트에 소요된 총 시간(시간, 분)을 계산합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.3.4 기록 데이터 저장 및 로컬 데이터베이스

이동 거리, 시작 시간, 종료 시간을 포함한 기록 데이터를 로컬 데이터베이스(SQLite 또는 Realm)에 저장합니다. 데이터 동기화를 위해 서버와의 동기화도 고려합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 1.4 날짜별 경로 조회
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

특정 날짜의 데이트 경로, 이동 거리, 시간을 조회하고 과거 기록을 열람할 수 있습니다.


#### 1.4.1 날짜 선택 캘린더 UI

사용자가 특정 날짜를 선택할 수 있는 캘린더 인터페이스를 제공합니다. 데이트 기록이 있는 날짜는 시각적으로 표시합니다(예: 점, 배지).
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.4.2 날짜별 경로 데이터 로드

선택된 날짜에 해당하는 경로 데이터(좌표, 타임스탐프, 거리, 시간)를 데이터베이스에서 조회합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.4.3 과거 기록 상세 조회 화면

선택된 날짜의 경로를 지도에 표시하고, 이동 거리, 시작/종료 시간, 소요 시간, 방문 장소 목록을 표시합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 1.4.4 기록 삭제 및 수정 기능

사용자가 선택된 날짜의 데이트 기록을 삭제하거나, 특정 데이터(시작/종료 시간)를 수정할 수 있는 기능을 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 2. 사진첩 연동 갤러리 일기 작성
> **Priority**: 🔴 High | **Progress**: ⚪ To Do

데이트 후, 해당 날짜에 찍은 사진들 중 일부를 선택하여 기록된 경로와 함께 갤러리 일기를 작성할 수 있습니다. 각 일기에 텍스트 메모를 추가할 수 있습니다.

**Acceptance Criteria:**
```
1. ○ 사용자 사진첩 접근 권한 동의 후 사진을 불러올 수 있어야 한다.
2. ○ 하나의 일기에 여러 장의 사진을 첨부할 수 있어야 한다.
3. ○ 사진과 함께 자유로운 텍스트 입력을 지원해야 한다.
4. ○ 작성된 일기가 날짜별로 정렬되어 표시되어야 한다.
```


### 2.1 사진첩 접근 권한 및 사진 불러오기
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

사용자의 사진첩 접근 권한을 요청하고, 특정 날짜의 사진들을 앱 내에서 불러올 수 있습니다.


#### 2.1.1 iOS 사진첩 접근 권한 요청

iOS 앱에서 PHPhotoLibrary 프레임워크를 사용하여 사진첩 접근 권한을 요청합니다. Info.plist에 NSPhotoLibraryUsageDescription을 설정합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS


#### 2.1.2 특정 날짜 사진 로드

선택된 날짜(또는 날짜 범위)에 촬영된 사진들을 사진첩에서 조회하여 앱 내에 그리드 형태로 표시합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.1.3 사진 선택 및 다중 선택

사용자가 하나 이상의 사진을 선택할 수 있도록 체크박스 또는 탭 기반의 다중 선택 인터페이스를 제공합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.1.4 사진 썸네일 및 미리보기

선택된 사진들의 썸네일을 표시하고, 탭 시 전체 사이즈의 미리보기를 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 2.2 갤러리 일기 작성
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

선택한 사진들을 하나의 일기에 추가하고, 각 사진에 텍스트 메모를 작성할 수 있습니다.


#### 2.2.1 갤러리 일기 작성 화면 설계

선택된 사진들, 텍스트 입력 영역, 저장 버튼 등을 포함한 일기 작성 화면의 UI/UX를 설계합니다. 블랙 앤 화이트 미니멀 디자인을 적용합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.2.2 각 사진에 대한 개별 텍스트 메모 기능

일기에 포함된 각 사진에 개별적으로 텍스트 메모를 작성할 수 있는 기능을 제공합니다(예: 각 사진 아래에 메모 입력 필드).
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.2.3 전체 일기 텍스트 입력 기능

일기 전체에 대한 자유로운 텍스트 입력을 지원합니다(예: 그날의 감정, 경험, 회상 등). 텍스트 길이 제한 및 서식 옵션(볼드, 이탤릭 등)을 고려합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.2.4 일기 저장 및 로컬 데이터베이스 저장

작성된 일기(사진, 메모, 텍스트, 작성 날짜, 타임스탬프)를 로컬 데이터베이스에 저장합니다. 동시에 파트너와 공유할 수 있도록 준비합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.2.5 사진 순서 변경 기능

일기에 포함된 사진들의 순서를 드래그 앤 드롭 또는 화살표 버튼으로 변경할 수 있는 기능을 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 2.3 일기 목록 및 날짜별 정렬
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

작성된 갤러리 일기들을 날짜 순서대로 정렬하여 목록으로 표시하고, 과거 일기를 조회할 수 있습니다.


#### 2.3.1 일기 목록 UI 설계

작성된 모든 갤러리 일기를 날짜 역순(최신순)으로 표시하는 목록 화면을 설계합니다. 각 일기의 첫 번째 사진, 날짜, 제목 또는 첫 글자를 미리보기로 표시합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.3.2 날짜별 정렬 기능

일기 목록을 최신순, 오래된 순 등으로 정렬할 수 있는 옵션을 제공합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.3.3 과거 일기 조회 및 세부 보기

목록에서 일기를 선택하면 해당 일기의 전체 사진(갤러리 형식), 텍스트 메모, 전체 텍스트를 상세하게 표시하는 화면을 제공합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.3.4 일기 검색 및 필터링

특정 날짜 범위, 키워드로 일기를 검색할 수 있는 기능을 제공합니다(예: 월별 검색, 텍스트 검색).
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 2.3.5 일기 수정 및 삭제 기능

사용자가 선택된 일기를 수정(사진 추가/삭제/순서 변경, 텍스트 수정)하거나 전체 삭제할 수 있는 기능을 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 3. 커플 소통 및 기념일/디데이 관리
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do

서로에게 편지를 작성하고 공유할 수 있는 기능, 중요한 기념일이나 다음 데이트까지 남은 시간을 계산해주는 디데이 카운트 기능을 제공합니다.

**Acceptance Criteria:**
```
1. ○ 서로에게 편지를 작성하고 앱 내에서 공유할 수 있어야 한다.
2. ○ 등록된 기념일과 디데이를 정확하게 계산하여 표시해야 한다.
3. ○ 기념일 임박 시 알림을 설정할 수 있어야 한다.
```


### 3.1 편지 작성 및 전송
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

파트너에게 전달할 편지를 작성하고 앱 내에서 전송하는 기능입니다.


#### 3.1.1 편지 작성 화면 설계

파트너에게 보낼 편지를 작성할 수 있는 텍스트 입력 화면을 설계합니다. 제목, 본문, 작성 날짜, 발신자 정보를 포함합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.1.2 편지 저장 및 전송 기능

작성된 편지를 로컬 데이터베이스에 저장하고, 파트너 계정으로 전송합니다. 전송 상태(발송, 수신, 읽음)를 추적합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.1.3 수신 편지 목록 및 조회

파트너로부터 받은 편지들을 목록으로 표시하고, 선택 시 전체 내용을 조회할 수 있는 기능을 제공합니다. 읽지 않은 편지는 배지나 하이라이트로 표시합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.1.4 편지 삭제 및 보관 기능

사용자가 받은 편지를 삭제하거나 보관 폴더로 이동할 수 있는 기능을 제공합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 3.2 기념일 및 디데이 관리
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

커플의 중요한 기념일을 등록하고, 현재 날짜로부터 남은 일수를 자동으로 계산하여 표시합니다.


#### 3.2.1 기념일 등록 화면

커플이 함께 기념할 날짜(연애 시작일, 결혼기념일, 첫 만난 날 등)를 등록할 수 있는 화면을 제공합니다. 날짜 선택 캘린더 및 기념일 이름, 설명 입력 필드를 포함합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.2.2 디데이 계산 로직

등록된 기념일과 현재 날짜를 비교하여 남은 일수(D-Day)를 계산합니다. 음수 값이 나오는 경우(과거 날짜) 경과 일수로 표시합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.2.3 기념일 목록 및 디데이 표시

등록된 모든 기념일을 목록으로 표시하고, 각 항목 옆에 디데이를 시각적으로 강조하여 표시합니다(예: 'D-30', 'D+365'). 다음 기념일을 메인 화면에 우선 표시합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.2.4 기념일 수정 및 삭제

등록된 기념일의 날짜, 이름, 설명을 수정하거나 전체 삭제할 수 있는 기능을 제공합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 3.3 기념일 알림 설정
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

등록된 기념일 임박 시 사용자에게 푸시 알림을 전송합니다.


#### 3.3.1 알림 설정 화면

각 기념일별로 알림을 활성화/비활성화하고, 알림 시간(예: D-7, D-1, 당일 오전 9시)을 설정할 수 있는 화면을 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.3.2 푸시 알림 구현

iOS(APNs)와 Android(FCM)를 활용하여 설정된 시간에 푸시 알림을 전송합니다. 알림 제목, 메시지, 액션(앱 열기, 무시)을 포함합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.3.3 로컬 알림 스케줄링

디바이스 로컬 시간을 기반으로 정기적인 알림 스케줄을 설정합니다. 시스템 재부팅 후에도 알림이 유지되도록 보장합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 3.3.4 알림 내역 조회 및 관리

사용자가 전송된 알림 목록을 조회하고, 이미 본 알림을 삭제하거나 관리할 수 있는 기능을 제공합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 4. 쿨하고 세련된 UI/UX 디자인
> **Priority**: 🔴 High | **Progress**: ⚪ To Do

기존 커플 앱의 '귀염귀염'한 스타일에서 벗어나, 블랙 앤 화이트를 기반으로 한 미니멀하고 쿨하며 세련된 디자인을 제공하여 사용자에게 차별화된 시각적 경험을 선사합니다.

**Acceptance Criteria:**
```
1. ○ 앱 전체 테마가 블랙 앤 화이트 톤을 유지해야 한다.
2. ○ 아이콘, 폰트, 레이아웃 등 모든 디자인 요소가 미니멀하고 세련된 느낌을 주어야 한다.
3. ○ 사용자 경험(UX) 흐름이 직관적이고 간결해야 한다.
```


### 4.1 블랙 앤 화이트 테마 적용
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

앱의 모든 화면과 요소에 블랙 앤 화이트를 기본으로 하는 일관된 색상 테마를 적용합니다.


#### 4.1.1 앱 전체 색상 팔레트 정의

블랙 앤 화이트를 기반으로 한 일관된 색상 팔레트를 정의합니다. 예: 주 배경색(검정), 보조 배경색(짙은 회색), 텍스트색(흰색), 액센트색(밝은 회색) 등. 다크 모드 대응을 고려합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.1.2 테마 시스템 구현

iOS/Android 네이티브 테마 시스템(예: Material Design 3, iOS 외형 API)을 활용하여 일관된 블랙 앤 화이트 테마를 모든 화면에 자동으로 적용합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.1.3 다크/라이트 모드 지원

시스템 설정에 따라 다크 모드와 라이트 모드를 자동으로 전환합니다. 또는 앱 설정에서 사용자가 모드를 강제 선택할 수 있도록 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 4.2 미니멀 디자인 요소 구성
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

아이콘, 폰트, 버튼, 레이아웃 등 모든 디자인 요소를 미니멀하고 세련된 스타일로 통일합니다.


#### 4.2.1 아이콘 디자인 및 통일

모든 기능별 아이콘(위치, 사진, 편지, 달력 등)을 미니멀한 라인 스타일 또는 솔리드 스타일로 디자인하고, 크기, 굵기, 스타일을 통일합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.2.2 타이포그래피 규칙 정의

제목(헤더), 본문, 캡션 텍스트에 대해 폰트 종류, 크기, 굵기, 라인 높이, 자간을 명확히 정의합니다. 세련되고 가독성 높은 폰트 조합을 선정합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.2.3 버튼 및 입력 요소 스타일

버튼, 텍스트 입력 필드, 토글, 체크박스 등을 미니멀한 디자인으로 통일합니다. 스테이트(활성, 비활성, 호버, 포커스)별 시각적 피드백을 제공합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.2.4 공백 및 레이아웃 그리드 시스템

일관된 패딩, 마진, 간격 규칙(예: 8px 기반 그리드)을 정의하여 모든 화면에서 일관된 레이아웃을 유지합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 4.3 직관적 UX 흐름 설계
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

사용자가 주요 기능들을 쉽게 접근할 수 있도록 간결하고 직관적인 네비게이션 및 정보 구조를 설계합니다.


#### 4.3.1 메인 네비게이션 구조 설계

앱의 주요 기능들(지도/경로, 갤러리 일기, 편지, 기념일, 인기 장소 등)에 접근할 수 있는 하단 탭 네비게이션 또는 사이드 메뉴를 설계합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.3.2 온보딩 및 초기 설정 흐름

앱 첫 실행 시 권한 요청(위치, 사진첩), 계정 설정, 파트너와의 연동, 기본 설정 등을 단계별로 안내하는 온보딩 화면을 설계합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.3.3 메인 홈 화면 레이아웃

사용자의 주요 관심사(다음 기념일, 최근 일기, 진행 중인 데이트 등)를 한 눈에 볼 수 있도록 홈 화면을 설계합니다. 직관적인 카드/섹션 기반 레이아웃을 사용합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.3.4 검색 및 필터 UX

일기, 기념일, 장소 검색 시 직관적인 검색 창(텍스트 입력, 필터 아이콘)과 결과 표시 방식을 설계합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 4.3.5 설정 화면 구조

프로필, 권한 관리, 알림 설정, 테마 설정, 데이터 내보내기 등 부가 기능들을 정리한 설정 화면을 설계합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 5. 다른 커플들의 인기 데이트 장소 탐색
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do

다른 커플들이 자주 방문하고 기록한 인기 있는 장소나 가게 정보를 확인할 수 있는 기능을 제공하여, 데이트 아이디어를 얻고 새로운 장소를 탐색할 수 있도록 돕습니다.

**Acceptance Criteria:**
```
1. ○ 사용자들이 기록한 데이트 장소 중 인기 있는 곳들을 목록 또는 지도에 표시해야 한다.
2. ○ 장소별 간략한 정보(예: 카테고리, 평점)를 제공해야 한다.
3. ○ 필터링 및 검색 기능을 통해 원하는 유형의 장소를 찾을 수 있어야 한다.
```


### 5.1 인기 데이트 장소 목록 및 지도 표시
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

다른 커플들이 기록한 방문 장소 중 인기 있는 곳들을 목록 또는 지도에 마커로 표시합니다.


#### 5.1.1 인기 장소 데이터 수집 로직

앱 사용자들이 기록한 데이트 장소를 집계하여, 방문 빈도, 평균 체류 시간 등을 기반으로 인기도 점수를 계산합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.1.2 인기 장소 목록 화면

인기 순서대로 정렬된 장소 목록을 표시합니다. 각 장소의 이름, 카테고리, 평점, 방문 수, 간단한 설명을 포함합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.1.3 인기 장소 지도 표시

수집된 인기 장소들을 지도 위에 마커로 표시합니다. 마커의 크기 또는 색상으로 인기도를 시각적으로 표현합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.1.4 사용자 개인정보 보호 및 익명화

인기 장소 정보를 표시할 때 개별 사용자의 신원이 노출되지 않도록 익명화 처리합니다. 또한 위치 프라이버시를 준수하기 위해 필요한 방지 조치를 취합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 5.2 장소 정보 조회
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

인기 장소들의 카테고리, 평점, 방문 빈도 등의 간략한 정보를 제공합니다.


#### 5.2.1 장소 상세 정보 페이지

선택된 인기 장소의 상세 정보를 보여주는 페이지를 설계합니다. 장소명, 주소, 카테고리, 평점, 방문 수, 사용자 리뷰/코멘트를 포함합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.2.2 카테고리 정보 제공

각 인기 장소를 카페, 음식점, 공원, 영화관 등의 카테고리로 분류하고 표시합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.2.3 평점 및 방문 통계

해당 장소를 방문한 커플들의 평점(1~5별), 평균 평점, 총 방문 수, 평균 체류 시간 등을 계산하여 표시합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.2.4 사용자 리뷰 및 코멘트

방문한 다른 커플들의 리뷰와 코멘트를 표시합니다. 개인정보는 노출하지 않으면서 장소에 대한 의견을 공유할 수 있도록 합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 5.3 장소 검색 및 필터링
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

카테고리, 지역, 평점 등을 기준으로 인기 장소를 검색하고 필터링하여 원하는 데이트 장소를 쉽게 찾을 수 있습니다.


#### 5.3.1 장소 검색 기능

텍스트 입력으로 장소명을 검색할 수 있는 기능을 제공합니다. 검색 결과는 실시간으로 표시되며, 검색 이력을 저장할 수 있습니다(선택).
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.3.2 카테고리별 필터링

카페, 음식점, 공원, 영화관 등 다양한 카테고리 필터를 제공하여 사용자가 원하는 유형의 장소를 빠르게 찾을 수 있도록 합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.3.3 지역별 필터링

지역(동작구, 강남구, 종로구 등) 또는 거리(내 위치 기준 반경 1km, 5km 등) 필터를 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.3.4 평점 기반 필터링

평점 4.0 이상, 3.5 이상 등으로 필터링하여 평가가 좋은 장소들만 표시할 수 있도록 합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 5.3.5 필터 조합 및 정렬

여러 필터를 조합하여 사용할 수 있도록 합니다. 결과를 평점순, 방문 수순, 거리순 등으로 정렬할 수 있는 옵션을 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 6. 데일리 관계 질문 및 답변 아카이브
> **Priority**: 🔴 High | **Progress**: ⚪ To Do

매일 하나의 관계 질문을 양쪽에게 보내고, 두 사람이 답하면 서로의 답을 공개합니다. 답변이 누적되어 둘만의 문답 아카이브가 됩니다. 썸원·Paired에서 검증된 리텐션 훅으로, "매일 한 번 앱을 여는 이유"를 만드는 핵심 장치입니다. 하루 1질문으로 제한해 소진을 막습니다.

**Acceptance Criteria:**
```
1. ○ 매일 정해진 시각에 양쪽에게 동일한 질문이 푸시로 전달되어야 한다.
2. ○ 두 사람이 모두 답해야 상대 답변이 공개되어야 한다(동시 공개).
3. ○ 과거 질문과 답변이 날짜별로 누적 조회되어야 한다.
4. ○ 질문은 관계 단계/관심사 기반 카테고리(가치관, 추억, 미래, 친밀감 등)로 분류되어야 한다.
```


### 6.1 데일리 질문 발송 및 공개 로직
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

매일 한 질문을 양쪽에 발송하고, 양쪽 답변이 모두 들어왔을 때만 서로의 답을 공개합니다.


#### 6.1.1 질문 큐레이션 및 카테고리 분류

가치관·추억·미래·친밀감·일상 등 카테고리별 질문 풀을 구성하고, 관계 시작일·이전 답변 패턴을 고려해 매일 1개를 선정합니다. 초기에는 1,000개 이상의 질문 데이터셋을 준비합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 6.1.2 동시 공개(블라인드) 로직

한쪽이 먼저 답해도 상대 답은 가려진 상태로 두고, 양쪽 답변이 모두 제출된 시점에 동시에 공개합니다. 상대가 아직 답하지 않았으면 "기다리는 중" 상태를 표시합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 6.1.3 답변 입력 형식(텍스트/사진/음성)

기본 텍스트 답변에 더해 사진·짧은 음성으로도 답할 수 있게 합니다(프롬의 영상 답변 사례 참고). 답변 길이 제한과 입력 형식별 UI를 정의합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 6.2 문답 아카이브 및 회고
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

누적된 질문과 답변을 타임라인으로 모아 보고, 특정 시기의 생각 변화를 되돌아볼 수 있게 합니다.


#### 6.2.1 문답 타임라인 화면

지난 질문과 양쪽 답변을 날짜순으로 표시하는 아카이브 화면을 설계합니다. 카테고리·키워드 검색을 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 6.2.2 답변 연속 기록(스트릭) 및 알림

며칠 연속 함께 답했는지 스트릭을 표시하고, 답을 놓친 날에는 부드러운 리마인드 알림을 보냅니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 6.3 관계 케어 콘텐츠(확장)
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

다툼·기념일·장거리 등 상황별 대화 카드와 가이드 콘텐츠를 제공해 질문 기능을 관계 케어로 확장합니다. 장기적으로 AI 코치 형태(상황 입력 시 대화 주제·데이트 제안)로 발전시킵니다.


#### 6.3.1 상황별 대화 카드 덱

친밀감·가치관·가족·돈 등 주제 덱을 만들어 오프라인에서 함께 펼쳐 보며 대화하도록 합니다(Lovewick·Agape 사례 참고).
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 6.3.2 AI 관계 코치(확장)

다툼 후 화해, 기념일 준비, 장거리 팁 등을 상황 입력 기반으로 제안하는 AI 코치를 검토합니다(Flamme·Paired 트렌드). 데이터 학습 시 개인정보 비식별 처리를 전제로 합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 7. 폰 네이티브 실시간 인터랙션(두들·메모·위젯)
> **Priority**: 🔴 High | **Progress**: ⚪ To Do

내 폰에서 메모를 쓰거나 그림을 그리면 상대 폰에 즉시 뜨고, 잠금화면 위젯과 라이브 액티비티로 "지금 서로"를 앰비언트하게 공유합니다. Dumpling·Widgetable·Couple Widget이 검증한 영역이지만, 위치 기반 종합 추억앱과 결합한 사례는 아직 없어 차별화 여지가 큽니다.

**Acceptance Criteria:**
```
1. ○ 한쪽이 그린 두들/메모가 수 초 내 상대 화면(또는 위젯)에 표시되어야 한다.
2. ○ 잠금화면·홈화면 위젯으로 상대 상태/거리/디데이를 별도 앱 실행 없이 확인할 수 있어야 한다.
3. ○ "보고싶어" 등 원탭 신호를 보내면 상대에게 즉시 푸시로 도착해야 한다.
4. ○ 위젯과 라이브 액티비티가 배터리·네트워크를 과도하게 쓰지 않아야 한다.
```


### 7.1 두 폰 간 실시간 두들/메모 공유
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

한 사람이 캔버스에 손그림을 그리거나 짧은 메모를 남기면 상대 폰에 실시간으로 전달합니다.


#### 7.1.1 손그림 캔버스 및 메모 입력

펜 굵기·색(블랙앤화이트 팔레트 내), 지우개, 짧은 텍스트 메모를 지원하는 캔버스를 구현합니다. 한 장의 그림을 빠르게 그려 보내는 데 최적화합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 7.1.2 실시간 전송 채널

두들/메모를 상대에게 수 초 내 전달하기 위한 실시간 채널(WebSocket 또는 푸시 기반)을 구축합니다. 오프라인 상대에게는 푸시로 대기 후 다음 접속 시 표시합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 7.1.3 잠금화면/위젯 표시 및 보관

전달된 두들을 상대의 위젯·잠금화면에 띄우고, 받은 그림은 "둘만의 낙서함"에 보관해 다시 볼 수 있게 합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 7.2 위젯 및 라이브 액티비티
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

앱을 열지 않아도 디데이·상대 상태·실시간 거리를 홈/잠금화면에서 확인하게 합니다.


#### 7.2.1 디데이/기념일 위젯

다음 기념일 디데이와 사귄 일수를 홈·잠금화면 위젯으로 표시합니다(기능 3의 디데이 데이터 연동).
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 7.2.2 실시간 거리/상태 위젯

양쪽이 동의한 경우 둘 사이 실시간 거리(예: "12km 떨어져 있음")와 간단한 상태(이동 중/집/수면)를 위젯에 표시합니다. 공유 범위는 기능 9의 프라이버시 토글을 따릅니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 7.2.3 데이트 라이브 액티비티

데이트 기록 중에는 iOS 라이브 액티비티/다이내믹 아일랜드에 진행 시간·이동 거리를 실시간 표시합니다(기능 1 연동).
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS


### 7.3 감정 신호 및 앰비언트 공유
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

"보고싶어" 같은 원탭 신호와 기분·상태를 가볍게 주고받습니다.


#### 7.3.1 원탭 감정 신호("보고싶어")

위젯이나 홈에서 버튼 한 번으로 "보고싶어/생각나" 신호를 보내면 상대에게 즉시 푸시로 도착합니다(Couple Widget의 "I'm thinking of you" 사례).
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 7.3.2 기분/상태 체크인

오늘의 기분을 이모지·짧은 한마디로 등록하면 상대 위젯에 반영됩니다(Widgetable Mood 사례). 수면 상태 공유도 옵션으로 검토합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 8. 위치 연동 데이트 코스 추천
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do

둘의 방문 이력·위치·취향을 바탕으로 다음 데이트 코스(여러 장소를 묶은 동선)를 추천합니다. 단일 장소 추천(기능 5)을 넘어 코스 단위로 제안하고, 제휴 할인으로 수익화 경로를 만듭니다. 데이트팝(제휴 커머스)과 Flamme(AI 추천)의 검증된 모델을 결합합니다.

**Acceptance Criteria:**
```
1. ○ 여러 장소를 묶은 코스(예: 카페 → 전시 → 식당) 단위로 추천해야 한다.
2. ○ 현재 위치/지역과 둘의 취향·방문 이력을 반영해야 한다.
3. ○ 추천 코스를 데이트 기록(기능 1)으로 바로 연결할 수 있어야 한다.
4. ○ 제휴 장소의 할인/예약 정보를 노출할 수 있어야 한다.
```


### 8.1 코스 추천 엔진
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

장소 데이터와 사용자 취향을 묶어 동선이 자연스러운 코스를 생성합니다.


#### 8.1.1 취향/이력 기반 추천 로직

방문 이력·저장 장소·카테고리 선호·평점을 입력으로 코스를 생성합니다. 초기에는 규칙 기반(지역·카테고리·동선 거리), 데이터 축적 후 AI 개인화로 확장합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 8.1.2 동선 최적화 및 코스 구성

추천 장소들을 이동 거리·영업시간·소요 시간을 고려해 순서로 묶고, 코스 총 소요 시간/예상 동선을 지도에 표시합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 8.1.3 테마/상황 필터(날씨·예산·실내외)

날씨, 예산대, 실내/실외, 기념일/일상 등 상황 필터로 코스를 좁힐 수 있게 합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 8.2 코스 저장·기록 연동 및 커뮤니티 연계
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

추천 코스를 저장하고, 실제 데이트 기록 및 커뮤니티 후기와 연결합니다.


#### 8.2.1 코스 저장 및 데이트 기록 연동

마음에 든 코스를 저장하고, 데이트 시작 시 해당 코스를 기준으로 기능 1의 경로 기록을 시작할 수 있게 합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 8.2.2 유저 큐레이션 코스(커뮤니티 연계)

사용자들이 자신의 데이트 코스를 익명으로 공유하고, 다른 커플이 따라 갈 수 있게 합니다(기능 10 커뮤니티와 연동). 인기 코스를 별도 큐레이션합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 8.2.3 제휴 장소 할인/예약(수익화)

제휴 매장의 할인·예약 정보를 코스에 노출하고, 전환을 추적합니다. 구독(프리미엄 추천) 또는 제휴 수수료 모델을 검토합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 9. 추억 영구 보존 및 프라이버시 신뢰
> **Priority**: 🔴 High | **Progress**: ⚪ To Do

"추억 저장소"를 표방하는 앱에서 데이터 영속성과 프라이버시는 기능이자 신뢰 자산입니다. 2025년 비트윈의 데이터 영구 삭제 사태로 사진·영상을 잃은 사용자가 다수 발생했고, 위치 기반 앱은 감시 우려도 동반합니다. 이를 정면으로 다뤄 "추억은 사라지지 않는다 + 위치는 내가 통제한다"를 차별점으로 만듭니다.

**Acceptance Criteria:**
```
1. ○ 사용자 데이터(사진·일기·기록)는 이중화 백업으로 단일 장애 시에도 보존되어야 한다.
2. ○ 위치 공유는 상시/임시/끄기를 사용자가 직접 토글할 수 있어야 한다.
3. ○ 사용자가 전체 데이터를 내보내기(export)하고 완전 삭제할 수 있어야 한다.
4. ○ 헤어짐 등 관계 종료 시 데이터 분리·보관·삭제 정책이 명확해야 한다.
```


### 9.1 데이터 영속성 및 백업
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

추억 데이터를 다중화해 보관하고, 사용자가 직접 백업/복구할 수 있게 합니다.


#### 9.1.1 이중화 백업 아키텍처

원본 스토리지 외 별도 리전/저장소에 정기 백업하고, 삭제 요청 시에도 일정 유예 기간(휴지통) 후 영구 삭제하도록 설계합니다. 단일 스토리지 오류로 데이터가 소실되지 않도록 합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 9.1.2 사용자 백업/내보내기

전체 추억(사진·일기·문답·지도 기록)을 사용자가 직접 내보내기(ZIP/PDF 앨범)할 수 있게 합니다. 휴지통·복구 UI를 제공합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 9.1.3 "추억 보존" 신뢰 안내

백업 정책·암호화·보존 약속을 온보딩과 설정에서 투명하게 안내합니다. 마케팅 차별 메시지로도 활용합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 9.2 위치 프라이버시 제어
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

위치 공유를 사용자가 능동적으로 통제하게 해 감시 우려를 해소합니다.


#### 9.2.1 위치 공유 토글(상시/임시/끄기)

실시간 위치 공유를 상시·임시(예: 데이트 중에만)·끄기로 전환할 수 있게 합니다. 기본값은 최소 공유로 설정합니다.
> **Priority**: 🔴 High | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 9.2.2 관계 종료 시 데이터 정책

헤어짐 등 커플 연결 해제 시 공동 데이터의 분리·보관·삭제 절차를 정의하고, 양쪽 동의 흐름을 설계합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 10. 커플 커뮤니티(익명·주제 한정)
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do

장기 목표인 커뮤니티는 커플앱의 2인 폐쇄성과 충돌하기 쉬우므로, 익명·주제 한정으로 좁혀 안전하게 시작합니다. 데이트 후기·관계 고민 Q&A처럼 둘만의 공간을 침범하지 않는 주제만 다룹니다. 충분한 사용자가 모인 뒤 단계적으로 개방합니다.

**Acceptance Criteria:**
```
1. ○ 게시는 익명(닉네임)으로 이루어지고 개인·파트너 신원이 드러나지 않아야 한다.
2. ○ 주제가 데이트 후기/코스/관계 Q&A 등으로 한정되어야 한다.
3. ○ 신고·차단·필터링 등 안전 장치가 갖춰져야 한다.
4. ○ 커뮤니티 콘텐츠가 데이트 코스 추천(기능 8)과 연계되어야 한다.
```


### 10.1 익명 게시 및 주제 보드
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

익명 닉네임으로 한정된 주제 보드에 글을 쓰고 반응합니다.


#### 10.1.1 익명 프로필 및 주제별 보드

데이트 후기, 데이트 코스, 관계 Q&A 등 주제 보드를 만들고 익명 닉네임으로 게시·댓글·좋아요를 지원합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 10.1.2 후기-코스 연계

데이트 후기에 방문 장소/코스를 태그해 기능 8의 코스 추천 데이터로 환류합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 10.2 커뮤니티 안전 및 운영
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

익명 공간의 부작용을 막는 안전 장치를 갖춥니다.


#### 10.2.1 신고·차단·필터링

부적절 게시물 신고, 사용자 차단, 금칙어·스팸 필터를 제공합니다. 운영 정책과 처리 흐름을 정의합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 10.2.2 단계적 개방 전략

초기에는 읽기 중심·소수 보드로 시작하고, 사용자 규모와 신고율을 보며 보드·기능을 단계적으로 확장합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 11. 추억 회고 및 결산
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do

쌓인 위치·사진·문답 데이터를 회고 자산으로 되돌려줍니다. "N년 전 오늘 여기 왔어요" 회상 알림, 한 해를 정리하는 결산 리포트, AI 자동 하이라이트 앨범으로 과거 기록의 재방문과 공유를 유도합니다. 위치 데이터를 보유한 우리만이 "함께 간 곳"을 축으로 한 회고를 제공할 수 있어 차별점이 큽니다.

**Acceptance Criteria:**
```
1. ○ 과거 같은 날짜/장소의 기록을 찾아 회상 알림으로 띄울 수 있어야 한다.
2. ○ 기간별(연말·기념일) 결산 리포트를 자동 생성해야 한다.
3. ○ 결산/하이라이트를 이미지·영상 형태로 공유할 수 있어야 한다.
4. ○ 회고 콘텐츠 생성 시 개인정보·위치 데이터를 외부로 노출하지 않아야 한다.
```


### 11.1 위치 기반 추억 회상
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

과거 같은 날짜 또는 현재 위치 근처의 지난 기록을 찾아 자연스럽게 떠올리게 합니다.


#### 11.1.1 같은 날짜 회상("N년 전 오늘")

오늘과 같은 월/일에 작성된 과거 일기·데이트 기록을 찾아 회상 카드로 보여주고, 알림으로 제안합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 11.1.2 장소 기반 회상("여기 와봤어요")

현재 위치가 과거 방문 지점과 가까우면 "이곳에 N개월 전 왔었어요" 알림과 당시 기록을 띄웁니다(기능 1의 위치 데이터 연동).
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 11.1.3 회상 카드 및 공유

회상 콘텐츠를 사진+지도+메모 카드로 구성하고, 둘만 보기 또는 외부 공유(이미지 저장)를 선택할 수 있게 합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 11.2 기간별 결산 리포트
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

연말·기념일에 일정 기간의 활동을 집계해 요약 리포트로 제공합니다(Spotify Wrapped 형식).


#### 11.2.1 결산 지표 집계

해당 기간의 함께 간 장소 수, 총 이동 거리, 데이트 횟수, 작성한 일기·문답 수, 가장 자주 간 지역 등을 집계합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 11.2.2 결산 리포트 화면 및 카드 생성

집계 지표를 스토리 형식의 카드 시퀀스로 구성하고, 블랙앤화이트 톤의 공유용 이미지로 내보낼 수 있게 합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 11.2.3 기념일 결산(디데이 연동)

연애 N주년 등 기념일 시점에 그간의 기록을 모은 미니 결산을 자동 생성합니다(기능 3 디데이 연동).
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 11.3 AI 자동 하이라이트 앨범
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

사진·기록을 자동 선별해 하이라이트 앨범이나 짧은 영상으로 묶어줍니다.


#### 11.3.1 사진 자동 선별 및 앨범화

기간·장소·인물 기준으로 대표 사진을 자동 선별해 앨범 또는 슬라이드 영상을 생성합니다. 사용자가 직접 편집·교체할 수 있게 합니다.
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 11.3.2 온디바이스 처리 우선

사진 선별·요약은 가능한 한 온디바이스에서 처리해 프라이버시를 보장합니다(기능 9 정책 연동).
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 12. 장거리 연애 지원
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do

떨어져 있는 커플이 일상을 함께 느끼도록 돕습니다. 영상·콘텐츠 동시 시청, 서로의 시차·날씨, 다음 만남까지의 카운트다운, 동시 취침/모닝 알림으로 물리적 거리를 메웁니다. Flamme가 롱디 카운트다운·LDR 코치를 별도로 다룰 만큼 수요가 검증된 세그먼트입니다.

**Acceptance Criteria:**
```
1. ○ 두 사람이 같은 영상/콘텐츠를 동기화된 상태로 함께 볼 수 있어야 한다.
2. ○ 서로의 현지 시각과 날씨를 한 화면에서 확인할 수 있어야 한다.
3. ○ 다음 만남까지 남은 시간을 카운트다운으로 표시할 수 있어야 한다.
4. ○ 거리 차이가 큰 경우에도 위치 정밀도가 프라이버시 설정(기능 9)을 따라야 한다.
```


### 12.1 함께 보기(동기화 시청)
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

영상이나 콘텐츠를 두 사람이 동기화된 상태로 함께 보고 반응을 나눕니다.


#### 12.1.1 재생 동기화 세션

한쪽의 재생/일시정지/탐색을 상대 화면과 동기화하는 세션을 구현합니다. 지원 콘텐츠 범위(앱 내 영상, 외부 링크 등)와 동기화 채널을 정의합니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 12.1.2 함께 보기 중 반응/채팅

시청 중 이모지 반응·짧은 채팅을 주고받을 수 있게 합니다(기능 7 실시간 채널 재사용).
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 12.2 시차·날씨·거리 위젯
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

서로 다른 지역에 있는 두 사람의 현지 정보를 한눈에 보여줍니다.


#### 12.2.1 양쪽 현지 시각/날씨 표시

두 사람의 현지 시각과 날씨를 나란히 표시하는 화면·위젯을 구현합니다(기능 7.2 위젯 시스템 연동).
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 12.2.2 거리 표시 및 프라이버시 연동

둘 사이 거리(예: "8,200km 떨어져 있음")를 표시하되, 정밀도와 노출 여부는 기능 9의 위치 공유 토글을 따릅니다.
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


### 12.3 만남 카운트다운 및 동시 알림
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android

다음 만남까지의 시간을 카운트다운하고, 취침·기상 같은 일상 리듬을 함께 맞춥니다.


#### 12.3.1 다음 만남 카운트다운

다음 만남 예정일을 등록하면 디데이 카운트다운을 홈·위젯에 표시합니다(기능 3 디데이 로직 재사용).
> **Priority**: 🟡 Medium | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


#### 12.3.2 동시 취침/모닝 알림

"같이 자자"·"잘 잤어?" 같은 동시 취침·기상 신호를 주고받고, 상대 수면 상태를 옵션으로 공유합니다(기능 7.3 감정 신호 연동).
> **Priority**: 🟢 Low | **Progress**: ⚪ To Do | **Roles**: User | **Devices**: iOS, Android


---


## 부록 A. 시장 분석 요약 (2026-06-20 조사)
---

### A.1 경쟁 구도

- **한국**: 비트윈(채팅·앨범·캘린더·디데이 종합, 5백만+), 썸원(데일리 질문 리텐션, 1천만+), 프롬(영상 답변), 커플릭스(신생). 국내 앱은 **위치 기능이 거의 없음**(공백).
- **글로벌**: Paired·Lovewick·Agape·Evergreen(데일리 질문/대화), Cupla(공유 캘린더), Flamme(AI 코치+데이트 플래너+위젯). 데일리 질문은 사실상 표준 기능.
- **위젯·실시간 전용**: Couple Widget·Widgetable·LiveStatus·Dumpling이 실시간 거리·잠금화면·두들·기분 공유를 선도. 단 추억 기록·위치 종합은 없음.
- **데이트 코스**: 데이트팝(600만+, 큐레이션+제휴 커머스+구독)이 검증된 수익 모델.

### A.2 핵심 페인포인트

1. **데이터 영속성 신뢰 붕괴** — 비트윈 2025-09 AWS 오류로 사진·영상 영구 삭제, 다수 피해(평생권·환불 보상). 추억앱의 최대 리스크.
2. **운영사 잦은 매각·약관 변경**으로 인한 개인정보 불신(비트윈 사례).
3. **서버/동기화 지연**(썸원 급성장기 불만).
4. **위치 공유의 감시 vs 안심 긴장** — Life360류 효용은 크나 과잉 감시·데이터 판매 우려.
5. **기능 파편화** — 추억·질문·위젯·위치·코스가 각각 다른 앱에 흩어짐(통합 부재).

### A.3 차별화 3축

- **(A) 위치 + 추억의 결합** — 경쟁사 공백. 우리만의 정체성(메모리 맵).
- **(B) 디바이스 네이티브 인터랙션** — 두들·위젯·라이브 액티비티를 종합앱에 최초 결합.
- **(C) 데이터 영속성·프라이버시를 신뢰 자산화** — 비트윈 사태의 반사이익을 진입 명분으로.


## 부록 B. 단계별 로드맵
---

| 단계 | 목표 | 포함 기능 |
|---|---|---|
| **P0 (정체성·진입 명분)** | 위치+추억 결합, 신뢰 확보 | 기능 1(메모리 맵), 기능 2(갤러리 일기), 기능 9(영구 보존·프라이버시), 기능 7.2(위젯·라이브 액티비티) |
| **P1 (리텐션·수익)** | 매일 여는 이유 + 수익 경로 | 기능 6(데일리 질문), 기능 8(데이트 코스 추천+제휴), 기능 7.1·7.3(두들·보고싶어 푸시), 기능 12.3(만남 카운트다운) |
| **P2 (회고·확장)** | 데이터 회고 자산화 | 기능 5(인기 장소), 기능 6.2(문답 회고), 기능 11(추억 회상·연말 결산), 기능 12.1·12.2(함께 보기·시차/날씨 위젯) |
| **P3 (커뮤니티·코치)** | 네트워크 효과 진입 | 기능 10(익명 커뮤니티), 기능 6.3(관계 케어·AI 코치), 기능 11.3(AI 하이라이트 앨범) |

> 출처: 앱스토어·구글플레이 리뷰, 언론 보도(머니투데이방송·아시아경제), 비교 리뷰(Flamme·Habi·다이티), 각 앱 공식 페이지. 상세 출처는 기획 조사 노트 참고.
