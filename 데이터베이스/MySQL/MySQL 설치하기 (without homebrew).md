# MySQL 설치하기 (without homebrew)
### 1. **MySQL 공식 사이트에서 설치 프로그램 다운로드**
1. [MySQL 공식 다운로드 페이지](https://dev.mysql.com/downloads/mysql/)에 접속합니다.
2. "Select Operating System"에서 **macOS**를 선택합니다.
3. macOS용 **DMG Archive** 설치 파일을 선택한 후 다운로드 버튼을 클릭합니다.
    - 계정이 없으면 회원가입 없이도 하단의 "No thanks, just start my download"를 클릭하여 다운로드할 수 있습니다.

### 2. **MySQL 설치**
1. 다운로드한 `.dmg` 파일을 실행합니다.
2. 설치 마법사에 따라 **MySQL Installer**를 실행하고 설치를 진행합니다.
    - 설치하는 과정에서 사용할 **root 계정의 비밀번호**를 설정하라는 메시지가 나타납니다. 이 비밀번호는 MySQL 서버에 처음 접속할 때 필요하므로 기억해두세요.
3. 설치가 완료되면 MySQL 서버를 시작할지 묻는 옵션이 나오며, 자동으로 시작되도록 설정할 수 있습니다.

### 3. **MySQL 서버 실행 및 중지**
MySQL 설치가 완료되면 **System Preferences**(시스템 환경설정)에 **MySQL** 항목이 추가됩니다. 여기서 MySQL 서버를 쉽게 시작하거나 중지할 수 있습니다.
1. **시스템 환경설정** > **MySQL**로 이동합니다.
2. 여기서 MySQL 서버를 **Start** 및 **Stop**할 수 있습니다.

### 4. **터미널에서 MySQL 사용**
설치가 완료되면 터미널에서 MySQL 클라이언트에 접속할 수 있습니다.
```shell
/usr/local/mysql/bin/mysql -u root -p
```
- **root**는 MySQL 설치 중 설정한 관리자 계정이며, 접속할 때 설정한 **비밀번호**를 입력합니다.
- **MySQL 클라이언트에 경로를 추가**하려면, `.bash_profile` 또는 `.zshrc` 파일에 아래와 같은 경로를 추가해 터미널에서 `mysql` 명령을 직접 사용할 수 있도록 할 수 있습니다:
```bash
export PATH=$PATH:/usr/local/mysql/bin
```

이후 터미널에서 다음 명령어로 MySQL에 접속할 수 있습니다.
```shell
`mysql -u root -p`
```


### 5. **MySQL 설정 보안**
설치 후 MySQL의 보안을 강화하려면 아래 명령어로 보안 설정을 수행합니다.
```shell
sudo /usr/local/mysql/bin/mysql_secure_installation
```
여기서 root 비밀번호 변경, 익명 사용자 삭제, 원격 root 접속 비활성화 등의 설정을 수행할 수 있습니다.

### 6. **MySQL 자동 실행 설정**
MySQL을 매번 수동으로 시작하지 않고 Mac 부팅 시 자동으로 실행되도록 설정하려면, 다음 명령어를 사용하여 MySQL을 시스템의 `launchctl`에 등록합니다.
```bash
sudo cp /usr/local/mysql/support-files/mysql.server /Library/LaunchDaemons/ sudo launchctl load -w /Library/LaunchDaemons/mysql.server
```

### 7. **MySQL 서버 중지**
MySQL 서버를 중지하려면 다음 명령어를 사용할 수 있습니다.

```bash
sudo /usr/local/mysql/support-files/mysql.server stop
```
