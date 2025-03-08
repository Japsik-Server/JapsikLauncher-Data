# JapsikLauncher-Data

# 개발 가이드
**반드시 이 리포지토리를 Windows 환경에서 `C:\JapsikLauncher-Data\` 디렉토리에 클론 후 작업하세요.**

### 필요한 것들
- [JDK 17 LTS x64](https://adoptium.net/temurin/releases/?os=windows&arch=x64&package=jdk&version=17) 이상
- [Nebula](https://github.com/dscalzi/Nebula)
- [Node.js v20](https://nodejs.org/ko/download) LTS 이상
- [Git](https://git-scm.com/downloads/win)

## Nebula 셋업
###### 자세한 정보는 Nebula 폴더 내의 `README.md` 파일을 참조하세요.
Nebula 폴더 내에 다음과 같이 .env 파일을 생성해주세요.

```
JAVA_EXECUTABLE=C:\Program Files\Eclipse Adoptium\jdk-17.0.14.7-hotspot\bin\java.exe # Eclipse Temurin™ JDK 17, 필요 시 변경
ROOT=C:\JapsikLauncher-Data\live
BASE_URL=https://raw.githubusercontent.com/Japsik-Server/JapsikLauncher-Data/main/live/
HELIOS_DATA_FOLDER=<%appdata%>\Japsik Launcher
```

  - `<%appdata%>` : `%appdata%` 디렉토리(`C:\Users\<사용자 이름>\AppData\Roaming`)

Nebula 폴더에서 터미널을 연 후, 아래 명령어를 실행하세요.

- `npm run start -- init root`

## Git Subtree를 사용해 클라이언트 데이터 가져오기
클라이언트를 처음 생성 했을 때에는, 해당 폴더 내에 있는 파일들을 다른 리포지토리로 분리 후, 아래 명령어를 사용해 Subtree에 추가합니다.

- `git subtree add -P live/servers/<CLIENT_NAME>-<MC_VERSION> <REMOTE_URL> <BRANCH_OR_TAG> [--squash]`

  - `<CLIENT_NAME>` : 클라이언트 이름
  - `<MC_VERSION>` : 클라이언트의 마인크래프트 버전
  - `<REMOTE_URL>` : 클라이언트 리포지토리의 Remote URL
  - `<BRANCH_OR_TAG>` : Subtree에 추가할 branch 또는 tag
  - `[--squash]` : Merge 시 여러개의 커밋을 하나로 합치기(권장)

예시) `git subtree add -P live/servers/Chosik-1.21.1 https://github.com/Japsik-Server/Chosik-Client.git 1.0.0 --squash`

클라이언트를 특정 branch 또는 tag의 버전으로 변경하고 싶다면, 아래 명령어를 사용해 Subtree의 branch를 변경합니다.

- `git subtree pull -P live/servers/<CLIENT_NAME>-<MC_VERSION> <REMOTE_URL> <BRANCH_OR_TAG> [--squash]`

  - `<CLIENT_NAME>` : 클라이언트 이름
  - `<MC_VERSION>` : 클라이언트의 마인크래프트 버전
  - `<REMOTE_URL>` : 클라이언트 리포지토리의 Remote URL
  - `<BRANCH_OR_TAG>` : Subtree에 추가할 branch 또는 tag
  - `[--squash]` : Merge 시 여러개의 커밋을 하나로 합치기(권장)

예시) `git subtree pull -P live/servers/Chosik-1.21.1 https://github.com/Japsik-Server/Chosik-Client.git 1.0.1 --squash`

### 주의사항
- 클라이언트의 모든 Merge 커밋들은 `<CLIENT_NAME> <VERSION>` 형식으로 이름을 짓습니다.

  - 예시) `Chosik-Client 1.0.0`

- 만약 Subtree를 추가하거나 pull 할 때 오류가 발생한다면 이 명령어를 사용해 보세요. `git reset --hard`

  - 이 명령어는 현재까지의 모든 작업 내용 *(push 하지 않은 커밋들 또는 커밋을 생성하지 않은 작업 내용들)* 을 초기화합니다.

## 채널 업데이트
클라이언트의 업데이트를 적용했다면, Nebula 폴더에서 아래 명령어를 사용해 `distribution.json`을 생성해야 합니다.

- `npm run start -- g distro`

해당 커밋의 이름은 `live 채널 업데이트` 로 합니다.