# 02_ EC2 인스턴스에 private repository 연동

EC2 인스턴스에는 `git clone` 명령어를 통해 원하는 git repository를 연동할 수 있다.

`public` repository의 경우 평소와 똑같은 방식으로 git clone해오면 되지만, `private` repository의 경우 그렇지 않다.

경우에 따라 민감한 정보를 담고 있어 public으로 공개하기 어려운 repository의 경우 private으로 설정해놓는데,  EC2에 clone해올 수 없다면 당황스러울 것이다.

private repository의 경우 특별한 key가 없으면 git clone해올 시, 에러가 발생한다.

그래서 키를 발급받고 EC2 인스턴스에 private repository를 연동하는 방법을 소개하겠다.

## 1. 연동 과정

### 1) ssh 키 페어(key-pair) 생성

메일 주소는 본인의 github와 연결된 메일이나 자기 자신임을 나타낼 수 있는 메일 주소를 입력한다.

```bash
ssh-keygen -o -t rsa -b 4096 -C "youremail@example.com"
```

### 2) id_rsa.pub 파일 생성 확인

1번 절차를 성공적으로 수행했다면, 홈 디렉토리에 `id_rsa.pub`라는 파일이 생겼을텐데, 이를 확인하는 절차를 거치는 것이 좋다.

```bash
cd ~
ls -a
.ssh
ls
```

![image](https://user-images.githubusercontent.com/93081720/206493756-4d263522-4987-4f9a-ba26-de1bcac84330.png)

![image](https://user-images.githubusercontent.com/93081720/206494146-e18988c4-1392-41ee-8d9b-72f765b43c4b.png)

### 3) public key값 복사

아래 명령어를 입력하여 터미널에 나오는 public key 값을 복사해준다. 이때 정상적인 키 값이라면 암호화된 키 내용 맨 뒤에 아까 입력했던 이메일 주소가 들어가 있을 것이다.

```bash
cat id_rsa.pub
```

### 4) 복사한 키 등록

git clone 해오고자 하는 private repository에 들어가서 `settings` - `Deploy keys` - `Add deploy key`에 들어가서 방금 복사했던 키를 등록해준다.

![image](https://user-images.githubusercontent.com/93081720/206495761-9b147c80-394d-431c-b7fe-80914de45ad0.png)

### 5) Clone with SSH

Clone 항목에서 `SSH`탭을 눌러서 나오는 주소를 복사하여 `git clone`해주면 끝!

![image](https://user-images.githubusercontent.com/93081720/206496328-0616467b-c585-4148-82d7-697ed0ce9828.png)

위의 작업을 순차적으로 잘 진행하면 EC2 인스턴스에 private repository를 연동할 수 있다.