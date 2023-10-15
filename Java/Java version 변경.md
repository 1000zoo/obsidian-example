Mac / Linux
# 현재 버전확인
- 아래 커멘드를 통해 현재 깔려있는 자바 버전을 확인할 수 있다.
```shell
java -version
```
![[스크린샷 2023-09-25 오후 10.36.37.png]]
나의 경우에는 17.0.1 버전이 깔려있다.

- 아래 커멘드를 통해 로컬에 깔려있는 버전들을 확인한다.
```bash
/usr/libexec/java_home -V
```
![[스크린샷 2023-09-25 오후 10.33.35.png]]
총 세개의 버전이 있는 것을 확인할 수 있다.

# 원하는 버전 다운 받기
이전 버전들은 오라클의 [아카이브](https://www.oracle.com/kr/java/technologies/downloads/archive/)에서 설치할 수 있다.
![[Pasted image 20230925224107.png]]
이 중에서 나는 `macOS ARM64 DMG Installer`를 설치해주었다.
dmg 파일을 실행시키고 설치를 마무리 해준 뒤, 다시 버전확인을 해주면, 아래와 같이 새로운 버전이 생긴 것을 볼 수있다.
![[스크린샷 2023-09-25 오후 10.33.47.png]]

# 원하는 버전으로 변경하기
아래의 커멘드를 입력하고, {version} 에 위에서 설치한 버전을 입력해준다.
```shell
export JAVA_HOME=$(/usr/libexec/java_home -v 11.0.20)
```
재시동 하여도 변경사항이 유지되도록, 아래의 커멘드까지 입력해준다.
```shell
source ~/.bash_profile
```

다시 자바 버전을 확인해주면 잘 바뀐 것을 확인할 수 있다.
![[Pasted image 20230925224603.png]]