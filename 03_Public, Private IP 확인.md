# 03_ Public / Private IP 주소 확인

![image](https://user-images.githubusercontent.com/93081720/210489205-bba8e020-4ed2-451f-909e-10c391aeb328.png)

EC2 인스턴스에 접근하기 위한 툴을 사용할 때 맨 처음 상단에 Public, Private IP주소가 노출되긴해서 확인할 수 있지만, 다음과 같이 명령어를 사용해서 확인을 할 수도 있다.

## 1. Public

```bash
curl ifconfig.me
```

<br>

## 2. Private

```bash
ifconfig -a
```

