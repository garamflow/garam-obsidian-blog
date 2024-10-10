# Docker 설치하기
## 1. 다운받아 설치하기
https://docs.docker.com/desktop/install/mac-install/
https://www.docker.com/get-started/

두 곳 중 한 곳에서 다운받아 설치하면 된다.

## 2. 설치 확인하기
```bash
docker -v
Docker version 27.2.0, build 3ab4256
```

> [!Note] 설치 확인이 안될 때
> `zsh: command not found: docker` 와 같이 docker를 찾을 수 없다면
> 1. docker desktop을 연다
> 2. 오른쪽 하단에 있는 터미널을 연다
> 3. which docker를 입력해서 docker 위치를 알아낸다.
> 4. 터미널에 `nano ~/.zshrc` 혹은 `nano ~/.bash_profile`을 입력해서 경로를 추가해준다.
> 5. 맨 아래 `export PATH="~~docker 설치 위치~~/bin:$PATH"` 를 입력해주고 저장하고 파일 수정을 끝낸다.
> 6. `source ~/.zshrc` 혹은 `source ~/.bash_profile`를 통해 저장 및 적용한다.
> 7. 로컬의 터미널을 재시작해준다.
> 8. 다시 한 번 `docker -v`를 입력하면 docker desktop과 동일한 버전이 출력된다.

