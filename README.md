# Builder image for .NET Core 3.1 with React Spa, working with `react-snap`

![](https://github.com/murbanowicz/net-core-react-builder/workflows/CI/badge.svg)

# Why?

I am working on a .NET Core project, 
where I use a React based SPA as a frontend for the IdentityServer4.

I came across some issues while trying to build it:
* Missing NodeJS
* Missing Yarn
* `react-snap` was crashing due to the Puppeteer issue.

# What is inside?

* .NET Core 3.1 SDK Alpine
* Node 12
* Yarn
* Chromium

# How you can use it?

Just use it as base builder image

```dockerfile
FROM murbanowicz/net-core-react-builder AS builder

WORKDIR /build
COPY . .
RUN dotnet restore
RUN dotnet publish -c Release -o /app

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine AS final
WORKDIR /app
COPY --from=builder /app .
EXPOSE 5000
ENTRYPOINT ["dotnet", "YourApp.dll"]
```
