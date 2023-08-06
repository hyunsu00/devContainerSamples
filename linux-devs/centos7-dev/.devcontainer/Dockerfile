FROM centos:7

ARG REINSTALL_CMAKE_VERSION_FROM_SOURCE="none"

# Optionally install the cmake for vcpkg
COPY ./reinstall-cmake.sh /tmp/

RUN if [ "${REINSTALL_CMAKE_VERSION_FROM_SOURCE}" != "none" ]; then \
        chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${REINSTALL_CMAKE_VERSION_FROM_SOURCE}; \
    fi \
    && rm -f /tmp/reinstall-cmake.sh

# [Optional] Uncomment this section to install additional vcpkg ports.
# RUN su vscode -c "${VCPKG_ROOT}/vcpkg install <your-port-name-here>"

# [Optional] Uncomment this section to install additional packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# 패키지 업데이트 및 sudo 지원 추가
RUN yum update -y && yum clean all && yum install -y sudo

#
# Locale 설정
#
# centos7은 기본적으로 C, en_~, POSIX 만 설치되어 있으며
# 기본적으로 en_US.UTF-8로 설정되어 있어 한글 출력에는 이상이 없다.
# 그외 ko_KR.UTF-8 등은 직접 설치 해줘야 한다.
# 언어 설정 (LC_ALL > 나머지 카테고리 > LANG)
# 한국어로 설정
RUN localedef -i ko_KR -f UTF-8 ko_KR.utf8
ENV LANG ko_KR.utf8

#
# 타임존 설정
# 만약 호스트의 타임존을 따를 경우 주석 처리한다.
# 한국 타임존
# ENV TZ=Asia/Seoul
# RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime

#
# 유저 생성
#
# 빌드시점 UNAME, UID, GID 설정
ARG UNAME=devUser
ARG UID=1000
ARG GID=$UID
# 유저 생성
RUN groupadd --gid $GID $UNAME \
    && useradd --uid $UID --gid $GID -m $UNAME \
    && echo $UNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$UNAME \
    && chmod 0440 /etc/sudoers.d/$UNAME
# 작업디렉토리설정
WORKDIR /home/$UNAME
# 유저로 로그인
USER $UNAME