FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine

WORKDIR /tmp/

ADD \
https://github.com/coinfoundry/miningcore/archive/v47.tar.gz \
.

RUN \
apk add --no-cache build-base cmake boost-dev libsodium-dev libzmq openssl-dev pkgconfig \
&& tar -xvf v47.tar.gz \
&& cd miningcore-47/src/Miningcore/ \
&& dotnet publish -c Release --framework netcoreapp2.2 -o ../../build/ \
&& mkdir /usr/local/miningcore/ \
&& mv ../../build/* /usr/local/miningcore/ \
&& rm -r * \
&& apk del build-base cmake boost-dev libsodium-dev libzmq openssl-dev pkgconfig


FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-alpine

LABEL maintainer="R3GISTRY"
LABEL description="Miningcore in Docker. This is a mining pool software."

COPY --from=0 /usr/local/miningcore/ /usr/local/miningcore/

RUN \
apk add --no-cache boost-date_time boost-system openssl

VOLUME ["/mnt/miningcore/"]

ENTRYPOINT ["dotnet", "/usr/local/miningcore/Miningcore.dll"]
CMD ["--help"]
