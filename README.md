# JapsikLauncher-Data

# 개발 가이드
**반드시 이 리포지토리를 Windows 환경에서 `C:\JapsikLauncher-Data\` 디렉토리에 클론 후 작업하세요.**

### 필요한 것들
- [JDK 17 LTS x64](https://adoptium.net/temurin/releases/?os=windows&arch=x64&package=jdk&version=17) 이상
- [Nebula](https://github.com/dscalzi/Nebula)
- [Node.js v20](https://nodejs.org/ko/download) LTS 이상
- [Git](https://git-scm.com/downloads/win)

## Nebula 셋업
Nebula 폴더 내에 다음과 같이 .env 파일을 생성해주세요.

```
JAVA_EXECUTABLE=C:\Program Files\OpenLogic\jdk-17.0.10.7-hotspot\bin\java.exe
ROOT=C:\JapsikLauncher-Data\live
BASE_URL=https://raw.githubusercontent.com/Japsik-Server/JapsikLauncher-Data/main/live/
HELIOS_DATA_FOLDER=<%appdata%>\Japsik Launcher
```

  - `<%appdata%>` : `%appdata%` 디렉토리(`C:\Users\<사용자 이름>\AppData\Roaming`)

## Git Subtree를 사용해 클라이언트 데이터 가져오기
클라이언트를 처음 생성 했을 때에는, 해당 폴더 내에 있는 파일들을 다른 리포지토리로 분리 후, 아래 명령어를 사용해 Subtree에 추가합니다.

`git subtree add -P live/servers/<ClientName>-<MC_VERSION> <REMOTE_URL> <branch or tag> [--squash]`

  - `<ClientName>` : 클라이언트 이름
  - `<MC_VERSION>` : 클라이언트의 마인크래프트 버전
  - `<REMOTE_URL>` : 클라이언트 리포지토리의 Remote URL
  - `<branch or tag>` : Subtree에 추가할 branch 또는 tag
  - `[--squash]` : Merge 시 여러개의 커밋을 하나로 합치기(권장)

예시) `git subtree add -P live/servers/Chosik-1.21.1 https://github.com/Japsik-Server/Chosik-Client.git 1.0.0 --squash`

클라이언트를 특정 branch 또는 tag의 버전으로 변경하고 싶다면, 아래 명령어를 사용해 Subtree의 branch를 변경합니다.

`git subtree pull -P live/servers/<ClientName>-<MC_VERSION> <REMOTE_URL> <branch or tag> [--squash]`

  - `<ClientName>` : 클라이언트 이름
  - `<MC_VERSION>` : 클라이언트의 마인크래프트 버전
  - `<REMOTE_URL>` : 클라이언트 리포지토리의 Remote URL
  - `<branch or tag>` : Subtree에 추가할 branch 또는 tag
  - `[--squash]` : Merge 시 여러개의 커밋을 하나로 합치기(권장)

예시) `git subtree pull -P live/servers/Chosik-1.21.1 https://github.com/Japsik-Server/Chosik-Client.git 1.0.1 --squash`