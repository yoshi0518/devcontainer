# Base Image
FROM --platform=linux/amd64 amazonlinux:2023.3.20240131.0

# Working Directory
WORKDIR /work

# Copy SSH Key file and Change permission
COPY ./* /root/.ssh/
RUN chmod 600 /root/.ssh/id_ed25519

# Update and Installation
RUN dnf update --releasever=2023.3.20240131 && \
  dnf install -y bzip2-devel gcc git libffi-devel openssl openssl-devel readline-devel sqlite sqlite-devel tar tk-devel wget xz-devel zlib-devel zsh

# Install aws cli v2
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
  unzip awscliv2.zip && \
  ./aws/install && \
  rm -fr aws*

# Install microsoft odbc driver for mssql
# Docs: https://learn.microsoft.com/ja-jp/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server
RUN curl https://packages.microsoft.com/config/rhel/9/prod.repo | tee /etc/yum.repos.d/mssql-release.repo && \
  dnf remove unixODBC-utf16 unixODBC-utf16-devel && \
  ACCEPT_EULA=Y dnf install -y msodbcsql18 mssql-tools18 && \
  echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bashrc && \
  source ~/.bashrc && \
  dnf install -y unixODBC-devel

# Install Python
# Docs: https://qiita.com/oiz-y/items/a314f53a751b4c46920a
RUN curl https://pyenv.run | bash && \
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc && \
    echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc && \
    echo 'eval "$(pyenv init -)"' >> ~/.bashrc && \
    source ~/.bashrc && \
    pyenv install 3.12.2 && \
    pyenv global 3.12.2 && \
    pip install poetry

# Port
EXPOSE 8000
