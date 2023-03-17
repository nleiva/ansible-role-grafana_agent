FROM docker.io/redhat/ubi8-minimal:8.7

ARG COLLECTIONS_DIR=/usr/share/ansible/collections
ARG ANSIBLE_DIR=/etc/ansible

ENV PIP_PACKAGES "ansible-core==2.14.3 setuptools==67.6.0 cryptography==39.0.2"

ENV PATH=/root/.local/bin:$PATH

RUN mkdir -p $COLLECTIONS_DIR
RUN mkdir -p $ANSIBLE_DIR

# Install dependencies
RUN microdnf --nodocs --disableplugin=subscription-manager install \
    python39 python39-devel python39-setuptools python39-wheel python39-pip \
    systemd iproute wget gcc-toolset-12-gcc \
    && alternatives --set python /usr/bin/python3 \
    && pip3.9 install --upgrade pip $PIP_PACKAGES \
    && microdnf clean all \
    && rm -rf /tmp/*

# Update curl -> RHSA-2023:1140
RUN microdnf --nodocs --disableplugin=subscription-manager update curl

# Install Ansible inventory file
RUN mkdir -p /etc/ansible
RUN echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

# Make sure systemd doesn't start agettys on tty[1-6].
RUN rm -f /lib/systemd/system/multi-user.target.wants/getty.target

VOLUME ["/sys/fs/cgroup"]
CMD ["/lib/systemd/systemd"]