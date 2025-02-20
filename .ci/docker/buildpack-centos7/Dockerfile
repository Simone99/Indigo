FROM centos:7

ARG DEVTOOLSET_VERSION=11
ARG GIT_VERSION=227

RUN yum install -y epel-release centos-release-scl
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-SCLo
RUN yum update -y
RUN yum install -y devtoolset-${DEVTOOLSET_VERSION}-gcc-c++ devtoolset-${DEVTOOLSET_VERSION}-libasan-devel devtoolset-${DEVTOOLSET_VERSION}-liblsan-devel freetype-devel fontconfig-devel make python3 rh-git${GIT_VERSION}
RUN yum clean -y all
RUN echo $'leak:libfontconfig\nleak:libc\n' >> /opt/external.supp

# Enable the SCL for all bash scripts.
ENV MANPATH=/opt/rh/rh-git${GIT_VERSION}/root/usr/share/man:/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/share/man \
    X_SCLS="devtoolset-${DEVTOOLSET_VERSION} rh-git${GIT_VERSION}" \
    PCP_DIR=/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root \
    PATH=/opt/rh/rh-git${GIT_VERSION}/root/usr/bin:/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    PKG_CONFIG_PATH=/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/lib64/pkgconfig \
    LD_LIBRARY_PATH=/opt/rh/httpd24/root/usr/lib64:/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/lib64:/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/lib:/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/lib64/dyninst:/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/lib/dyninst:/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/lib64:/opt/rh/devtoolset-${DEVTOOLSET_VERSION}/root/usr/lib \
    LSAN_OPTIONS=suppressions=/opt/external.supp \
    ASAN_OPTIONS=alloc_dealloc_mismatch=0


RUN PIP_ONLY_BINARY="cmake" python3 -m pip install cmake

RUN cmake --version && \
    gcc --version && \
    g++ --version && \
    git --version && \
    make --version && \
    python --version && \
    python3 --version
