# 🔒 Linux_PAM

### PAM 사용해서 비밀번호를 8자리 이상으로 제한하기

# 📋 목차
### Step 01: myserver01 복제 후 myserver03 생성
### Step 02: myserver03의 IP 주소 변경
### Step 03: 포트 변경 및 포트 포워딩 설정
### Step 04: PAM 모듈 설치 및 비밀번호 최소 길이 제한

## Step 01: 🖥️ myserver01 복제 후 myserver03 생성

![image](https://github.com/user-attachments/assets/f475f8b2-5a77-431c-b6e0-2805975f1018)

## Step 02: 🌐 myserver03의 IP 주소 변경

1. ip를 변경하기 위해 yaml 파일 오픈
```bash
sudo vi /etc/netplan/00-installer-config.yaml
```
2. ip 주소 설정
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      addresses:
        - 10.0.2.19/24  # 변경된 고정 IP 주소
      routes:
        - to: default
          via: 10.0.2.1  # 게이트웨이
      nameservers:
        addresses:
          - 8.8.8.8
      dhcp4: false
```

![image](https://github.com/user-attachments/assets/db3e7cb3-4c36-43b9-83d2-ecddc45d3975)

3. 설정 후 적용
```
sudo netplan apply
```

4. 적용 확인
```
ip a  또는 ip addr
```

![image](https://github.com/user-attachments/assets/aee04340-b0e9-4757-a00a-6b4548015022)

## Step 03: 🔄 포트 변경 및 포트 포워딩 설정

1. config 파일 수정

![image](https://github.com/user-attachments/assets/d7128bcb-203e-461e-aac1-43da4883377a)

2.  포트포워딩

![image](https://github.com/user-attachments/assets/d2414206-2275-47f8-8373-f6ef92f90716)

## Step 04: ⚙️ PAM 모듈 설치 및 비밀번호 최소 길이 제한
1. PAM 모듈 설치
```
sudo apt update
sudo apt install libpam-pwquality
```

2. PAM 설정 파일 수정
```
sudo nano /etc/pam.d/common-password
```

![image](https://github.com/user-attachments/assets/551694d4-6193-47d9-8b27-d6bb58024bc0)

```
minlen = 8 추가
```

3. passwd 로 변경사항 확인

![image](https://github.com/user-attachments/assets/c77f8e28-c24f-4c2e-b92f-e01298d705e6)

