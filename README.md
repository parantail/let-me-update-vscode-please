# WSL2에서 VSCode 업데이트가 안 돼서 고통받고 있는 사람들을 위한 해결 방법

WSL2 에서 아래의 커맨드로 VSCode를 열려고 시도할 때
```
code .
```

아래와 같은 메시지와 함께 다운로드가 세월아네월아 진행되는 경우를 흔히 볼 수 있습니다. 매우 열받습니다...
```
Updating VS Code Server to version 1ad8d514439d5077d2b0b7ee64d2ce82a9308e5a
Removing previous installation...
Installing VS Code Server for x64 (1ad8d514439d5077d2b0b7ee64d2ce82a9308e5a)
Downloading:   0%
```

실제로 이 파일은 아래 링크에서 다운로드 되는데요,
> https://update.code.visualstudio.com/commit:1ad8d514439d5077d2b0b7ee64d2ce82a9308e5a/server-linux-x64/stable

직접 받아보시면 역시나 원활하지 않음을 알 수 있습니다.
원인을 추정해보건데, 아마도 visualstudio.com이 제공하는 CDN이 한국까지 원활하게 닿지 않는 것 같습니다. 특히 업데이트 배포 초기에 말이죠..

저 파일을 어떻게든 다운로드 받으면 일단 문제는 해결할 수 있는데, VPN, Cloud등 파일 다운로드가 원활한 (한국이 아닌) 곳에서 다운로드 후 옮겨오는 방법을 생각해 볼 수 있겠습니다.

가장 쉬울 것 같은 'Save to Google Drive' Chrome Extension은 용량 제한 때문에 사용할 수 없고요..

무료로 손쉽게 사용할 수 있는 방법 중에 

> https://www.multcloud.com/

이곳을 사용하는 방법이 있습니다. (월 5GB 전송까지 무료) 회원가입하고 본인의 구글 드라이브 연결해주시고요,

* Remote Upload 메뉴에서 Create Task 한 후 위의 링크를 붙여넣기 해 줍니다.
  * (MD5 해시값은 실제 다운로드 메시지의 값으로 대체)
* 그리고 다운받을 구글 드라이브 경로를 지정하고 저장

지정한 경로의 구글 드라이브에 가서 다운로드된 파일을 로컬에 다시 다운로드 합니다.
그 과정에서 파일명이 바뀌어 있다면 적당히 아무이름.tar.gz 로 바꾸어 줍니다.

이제 이 파일을 아래 경로를 통해 WSL2에 넣어 주시고요

```
\\wsl$\Ubuntu\home\YOUR_USER_NAME\.vscode-server\bin
```

WSL2 환경에서 해당 디렉토리로 가서 아래 커맨드로 압축을 풀어줍니다.

```
tar -xvf downloaded.tar.gz
```

그리고 생겨난 디렉토리를 해시값으로 바꿔줍니다.

```
mv vscode-server-linux-x64 1ad8d514439d5077d2b0b7ee64d2ce82a9308e5a
```

끝!

```
code .
```

으로 Visual Studio Code 가 열리는 걸 확인할 수 있습니다.
