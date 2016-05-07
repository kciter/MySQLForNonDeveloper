###### 비개발자를 위한 MySQL
# 설치

MySQL을 배우기 위해서는 MySQL을 설치해야 합니다. 그리고 MySQL을 쉽게 다루기 위한 툴도 같이 설치해봅시다.

## MySQL 설치
MySQL 설치는 [이곳](http://dev.mysql.com/downloads/mysql/)에서 하시면 됩니다. MySQL의 GPL 라이센스 버전인 MySQL Community Server를 설치하시면 됩니다. 다운로드 페이지에서 본인이 사용하는 운영체제를 선택 후 다운로드 받으면 됩니다. 윈도우의 경우는 MSI 파일을 이용하여 설치하고 맥의 경우에는 DMG 파일을 이용하여 설치하면 편합니다.
<p align="center">
  <sub>참고 이미지</sub>
  <img src='https://github.com/kciter/MySQLForNonDeveloper/blob/master/Images/mysql_download.png?raw=true'>
</p>

다운로드 할 때 로그인 혹은 회원가입해달라는 화면이 나옵니다. 이때 두 가지 모두 하기 싫다면 하단에 'No thanks, just start my download.' 버튼을 누르면 생략 됩니다.

설치할 때 무엇을 설치할 것인지 나타납니다. 이때 MySQL Server와 MySQL Workbench만 설치하면 됩니다. 그리고 설치가 마무리된 후에는 환경설정을 하게 됩니다. 이때 중요한 것은 Password를 설정하는 부분인데 가장 상위 권한을 가지고 있는 Root의 비밀번호를 설정하는 것이기 때문에 까먹지 않도록 조심합시다. 이후에는 설명에 맞춰서 설정한 후 Finish 버튼을 누르시면 설치가 완료됩니다.

## MySQL Workbench
MySQL Workbench는 MySQL을 좀 더 쉽게 사용할 수 있도록 도와주는 툴입니다. 버그도 종종 있지만 편리한 기능이 많으므로 사용하면 좋습니다. 만약 MySQL Workbench를 MySQL 설치하며 하지 못했다면 [이곳](http://dev.mysql.com/downloads/workbench/)에서 설치 할 수 있습니다.

[다음 장](BASIC.md)에서는 MySQL을 이용하여 기본적인 문법을 배워봅시다.

## 지적, 수정사항에 대해서
Github 계정이 있으신 분들은 Issue에 지적사항을 등록해주시거나 직접 수정하여 Pull request를 주시면 반영하도록 하겠습니다. <br>Github 계정이 없으신 분들은 kciter@naver.com를 통해 지적사항을 보내주세요. :smile:

## 라이센스
<a rel="license" href="http://creativecommons.org/publicdomain/mark/1.0/">
<img src="https://licensebuttons.net/p/mark/1.0/88x31.png" alt="Public Domain Mark" />
</a>

이 문서는 [CC0 라이센스](LICENSE)를 따릅니다.

특허권 또는 상표권은 CC0에 의해 영향을 받지 않으며, 퍼블리시티권 및 프라이버시권 등 저작물 자체에 대해 또는 저작물 이용에 대해 타인이 갖는 권리 또한 영향을 받지 않습니다.

달리 정하지 않은 한, 본 저작물의 인증자는 관련법에서 허용하는 최대 한도 내에서 저작물에 대해 아무런 보증도 하지 않으며 저작물의 모든 이용에 관한 어떠한 책임도 지지 않습니다.

저작물을 사용하거나 인용할 때 저자나 인증자로부터 승인을 받았다는 뜻을 시사하여서는 안됩니다.
