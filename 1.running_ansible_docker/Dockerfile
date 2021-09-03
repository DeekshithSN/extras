
RUN mkdir /etc/ansible /ansible
RUN mkdir ~/.ssh
# Over rides SSH Hosts Checking
RUN echo "host *" >> ~/.ssh/config &&\
    echo "StrictHostKeyChecking no" >> ~/.ssh/config
# Downloads the Ansible tar (curl) and saves it (-o)
RUN \
  curl -fsSL https://releases.ansible.com/ansible/ansible-2.9.3.tar.gz -o ansible.tar.gz
# Extracts Ansible from the tar file
RUN \
  tar -xzf ansible.tar.gz -C ansible --strip-components 1 && \
  rm -fr ansible.tar.gz /ansible/docs /ansible/examples /ansible/packaging
# Makes a directory for ansible playbooks
RUN mkdir -p /ansible/playbooks
# Makes the playbooks directory the working directory
WORKDIR /ansible/playbooks
# Sets environment variables
ENV ANSIBLE_GATHERING smart
ENV ANSIBLE_HOST_KEY_CHECKING False
ENV ANSIBLE_RETRY_FILES_ENABLED False
ENV ANSIBLE_ROLES_PATH /ansible/playbooks/roles
ENV ANSIBLE_SSH_PIPELINING True
ENV PATH /ansible/bin:$PATH
ENV PYTHONPATH /ansible/lib
# Sets entry point (same as running ansible-playbook)
#ENTRYPOINT ["ansible-playbook"]
# Can also use ["ansible"] if wanting it to be an ad-hoc command version
#ENTRYPOINT ["ansible"]
