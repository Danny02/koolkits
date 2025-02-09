FROM ubuntu:20.04
ENV JAVA_VERSION=21.0.2-tem
ENV MAVEN_VERSION=3.9.6
ENV VISUALVM_VERSION=2.1.7
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install --yes --no-install-recommends --quiet \
    bird \
    conntrack \
    ctop \
    curl \
    dhcping \
    dnsutils \
    fping \
    gdb \
    htop \
    httpie \
    iftop \
    iperf \
    ipset \
    iptraf-ng \
    iproute2 \
    iputils-ping \
    ipvsadm \
    jq \
    ldnsutils \
    liboping-dev \
    linux-tools-common \
    mtr \
    mycli \
    mysql-client \
    netcat \
    netgen \
    nftables \
    ngrep \
    nmap \
    pgcli \
    postgresql-client \
    redis-tools \
    scapy \
    socat \
    software-properties-common \
    strace \
    tcpdump \
    tcptraceroute \
    termshark \
    tmux \
    tshark \
    unzip \
    vim \
    wuzz \
    zip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /usr/local/bin
# Get sdkman (java version mgmt.)
RUN curl -s https://get.sdkman.io | bash && \
    bash -c "source /root/.sdkman/bin/sdkman-init.sh && \
    sdk install java $JAVA_VERSION && \
    sdk default java $JAVA_VERSION && \
    sdk install visualvm $VISUALVM_VERSION && \
    sdk default visualvm $VISUALVM_VERSION && \
    sdk install maven $MAVEN_VERSION && \
    sdk default maven $MAVEN_VERSION" && \
    # Get async-profiler-arm64
    curl -L https://github.com/jvm-profiling-tools/async-profiler/releases/download/v3.0/async-profiler-3.0-linux-arm64.tar.gz -o async-profiler.tar.gz && \
    tar -xzvf async-profiler.tar.gz && \
    rm async-profiler.tar.gz && \
    echo "alias async-profiler-arm64='/usr/local/bin/async-profiler-3.0-linux-arm64/profiler.sh'" >> /root/.bashrc && \
    # Get async-profiler-x64
    curl -L https://github.com/jvm-profiling-tools/async-profiler/releases/download/v3.0/async-profiler-3.0-linux-x64.tar.gz -o async-profiler.tar.gz && \
    tar -xzvf async-profiler.tar.gz && \
    rm async-profiler.tar.gz && \
    echo "alias async-profiler-x64='/usr/local/bin/async-profiler-3.0-linux-x64/profiler.sh'" >> /root/.bashrc && \
    # Get calicoctl (inside the pod)
    curl -L https://github.com/projectcalico/calico/releases/latest/download/calicoctl-linux-amd64 -o calicoctl && \
    chmod +x calicoctl && \
    # Get websocat (not available over apt)
    curl -L https://github.com/vi/websocat/releases/latest/download/websocat_linux64 -o websocat && \
    chmod +x websocat && \
    # Get mongo shell (not available over apt)
    curl -L https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/5.0/multiverse/binary-amd64/mongodb-org-shell_5.0.5_amd64.deb -o mongodb-org-shell_5.0.5_amd64.deb && \
    dpkg -i mongodb-org-shell_5.0.5_amd64.deb && \
    rm mongodb-org-shell_5.0.5_amd64.deb

CMD ["/bin/bash"]
