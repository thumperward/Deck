ARG VARIANT="3.1"
FROM mcr.microsoft.com/vscode/devcontainers/dotnet:${VARIANT}

# This fixes dotnet test breaking tty
RUN touch ~/.bashrc
RUN echo ' \n\
  dotnet () \n\
  { \n\
  local RET_VAL; \n\
  local BEFORE=$(stty -g); \n\
  $(which dotnet) "$@"; \n\
  RET_VAL=$?; \n\
  sleep 0.33; \n\
  stty "${BEFORE}"; \n\
  return $RET_VAL \n\
  } ' >> /home/vscode/.bashrc

# This fixes omnisharp 
RUN apt-get install gnupg ca-certificates
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb https://download.mono-project.com/repo/ubuntu stable-focal main" | tee /etc/apt/sources.list.d/mono-official-stable.list
RUN apt-get update -y
RUN apt-get install mono-devel -y