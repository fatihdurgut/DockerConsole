FROM mcr.microsoft.com/dotnet/framework/sdk:4.7.2-windowsservercore-ltsc2019 AS build
WORKDIR /app

 

# copy csproj and restore as distinct layers
COPY ../*.sln .
COPY *.csproj ./
COPY *.config ./
RUN nuget restore

 

# copy everything else and build app
COPY . .
WORKDIR /app
RUN msbuild /p:Configuration=Release -r:False

 


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.7.2-windowsservercore-ltsc2019 AS runtime
WORKDIR .
COPY --from=build app/ .

ENTRYPOINT ["dockerconsole.exe"]