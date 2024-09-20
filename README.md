# Linux_PAM

## myserver03 새로 생성하여 ip를 수정해 다른 vm끼리 통신할 수 있게 하고 PAM 사용해서 비밀번호를 8자리 이상으로 규제하기

### Step01 myserver01을 복제해 myserver03 생성

![image](https://github.com/user-attachments/assets/f475f8b2-5a77-431c-b6e0-2805975f1018)

### Step02 myserver03의 ip 주소 변경하기

1. ip를 변경하기 위해 yaml 파일 오픈
   ```
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

5. 동시 실행, 통신을 위해 포트변경 및 포트포워딩

   5.1 config 파일 수정

   ![image](https://github.com/user-attachments/assets/d7128bcb-203e-461e-aac1-43da4883377a)

   5.2 포트포워딩

   ![image](https://github.com/user-attachments/assets/d2414206-2275-47f8-8373-f6ef92f90716)

