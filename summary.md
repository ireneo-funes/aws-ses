# Summary of AWS SES Best Practices

This is a summary of [AWS](https://aws.amazon.com/)
[SES](https://aws.amazon.com/ses/)
[Best Practices](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/best-practices.html).

AWS SES로 이메일 서비스를 할때 주의할 사항을 정리한다.

## region

- AWS SES 는 한국 리전은 지원하지 않아서 US West (Oregon) 리전을 사용

## 신뢰도

- 메일 서버의 신뢰도를 높게 유지해야 나중에 메일 보낼 때 불이익을 받지 않음.
- 신뢰도를 유지하는 방법: **bounce**는 5% 이하,  **complaint**는 0.1% 이하로 유지하는 것이 최선.

- Bounce의 종류
  - hard bounce: **영구적** 반송 (예: 메일 주소가 잘못됨)
  - soft bounce: **일시적** 반송 (예: 메일함이 가득 차서 우편을 못받음)

- Complaint: 메일을 받은 사람이 '스팸'으로 등록하면 발신자에게 전달됨.

## Double Opt-in

- 사용자가 이메일 주소를 아무거나 넣는 경우도 많음.
- double opt-in: 제대로 된 이메일 주소만 추리는 방식
  - 사용자가 입력한 주소로 메일을 보낼 때 '확인 링크'를 본문에 넣고
  - 그 링크를 클릭한 경우만 주소록에 추가함.

## 보내는 주소

- 사용자에게 알려준 주소 그대로 보낸다.  
  `alice.net` 에서 보낸 메일의 double opt-in 으로 주소를 수집했으면 `bob.com` 에서 보내지 말고 `alice.net` 에서 보낸다.
- 사용자는 도메인 정보도 확인한다. whois 정보도 언제나 최신으로 유지.
- [Domain Key Identified Mail (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail)을 적극적으로 활용한다.

