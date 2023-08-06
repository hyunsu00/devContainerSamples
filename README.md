# devContainerSamples

```bash
# 리눅스 버전 확인
$ grep . /etc/*-release
# 로케일 확인
$ locale
$ locale -a
# 타임존 확인
$ date
$ ls -l /etc/localtime
$ more /etc/timezone
$ cat /etc/timezone
# 유저 정보
# 유저 전체 목록 확인
$ cat /etc/passwd
# 유저 전체 목록 확인(아이디만)
$ cut -f1 -d: /etc/passwd
# 유저 USERADD 를 통해 등록된 계정만 보기
$ grep /bin/bash /etc/passwd
$ grep /bin/bash /etc/passwd | cut -f1 -d:
```