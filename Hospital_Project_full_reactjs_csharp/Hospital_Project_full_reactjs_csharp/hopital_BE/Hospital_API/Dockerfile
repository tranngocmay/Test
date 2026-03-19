FROM mcr.microsoft.com/dotnet/sdk:9.0 as build
# cài thư viện dotnet, đặt tên môi trường là build

WORKDIR /build
# thư mục làm việc

COPY  . .
# COppy hết tất cả, ngang với docker file

RUN dotnet publish -o ./publish
# -o: tạo ra 1 output bỏ source vào

# Môi trường ở trên là môi trường build để có thư mục publish để làm việc nhanh
# 

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS deploy
# cài thư viện dotnet, đặt tên môi trường là deploy

WORKDIR /app
# copy bỏ vào /app

COPY --from=build /build/publish .
# --from=build: lấy source từ môi trường build
# /build/publish: path tới source
# build: lấy từ môi trường ở trên, WORKDIR
# publish: output của môi trường trên

EXPOSE 8080
# port quy định của dotnet là 5000

CMD ["dotnet", "Hospital_API.dll"]
# chạy lệnh dotnet, chạy file Hospital_API.dll


# docker rm -f cons-dotnet && docker rmi img-dotnet
# docker build . -t img-dotnet

# docker run -d -p 8080:8080 --name cons-dotnet img-dotnet