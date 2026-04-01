# aws-nuke

# aws nuke

aws nuke는 리소스를 삭제하는 것을 지칭하는 것이다.

별칭 생성 : `aws iam create-account-alias --account-alias [원하는-별칭-이름]`

별칭 확인 :  `aws iam list-account-aliases`

- **nuke-config.yml을 생성한다.**

```jsx
regions:
  - ap-northeast-2  # 서울 리전 (주로 사용하는 리전만 넣으면 빨라집니다)
  - global          # IAM 등 글로벌 리소스 삭제를 위해 필수

account-blocklist:  # 절대 지우면 안 되는 계정 ID (필수)
  - "999999999999" 

accounts:
  "781729906178": # 지한 님의 계정 ID
    filters:
      IAMUser:
        - "admin" # 본인 관리자 계정은 삭제 제외 설정 권장
```

- 실제로 삭제하는건 아니고 삭제할 목록을 확인한다.

```jsx
aws-nuke nuke --config nuke-config.yml --no-alias-check
```

- 진짜로 aws 리소스를 삭제한다.

```jsx
**aws-nuke nuke --config nuke-config.yml --no-alias-check --no-dry-run**
```

리소스 삭제하는 커멘드를 입력하면 아마도 “ > ”가 뜰건데 여기에다가 이 텍스트를 입력하면 복구할 수 없다.

```jsx
aws-nuke-target-<<계정 ID>>
```
