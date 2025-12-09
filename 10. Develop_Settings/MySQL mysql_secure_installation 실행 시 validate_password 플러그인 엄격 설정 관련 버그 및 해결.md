---
link: "[[_Clipping]]"
title: MySQL mysql_secure_installation 실행 시 validate_password 플러그인 엄격 설정 관련 버그 및 해결
source: https://www.perplexity.ai/search/mysql-mysql-secure-installatio-AHL8D630RnyQdB9_TNbd.g
created: 2025-10-26
tags:
  - MySQL
  - DB
---
[MySQL:: MySQL 8.4 Reference Manual:: 6.4.2 mysql\_secure\_installation](https://dev.mysql.com/doc/refman/8.4/en/mysql-secure-installation.html)

[

Improve MySQL Installation Security

](https://dev.mysql.com/doc/refman/8.4/en/mysql-secure-installation.html)[dev.mysql.com](https://dev.mysql.com/doc/mysql-secure-deployment-guide/5.7/en/secure-deployment-password-validation.html)

[

Chapter 6, Installing the MySQL Password Validation Plugin

](https://dev.mysql.com/doc/mysql-secure-deployment-guide/5.7/en/secure-deployment-password-validation.html)[bugs.mysql.com](https://bugs.mysql.com/bug.php?id=80480)

[

Validate Password Plugin throws error if installed in my.cnf

](https://bugs.mysql.com/bug.php?id=80480)[GitHub](https://github.com/Homebrew/homebrew-core/issues/180063)

[

Homebrew MySQL brew upgrade broke mysql

](https://github.com/Homebrew/homebrew-core/issues/180063)

어시스턴트 단계

MySQL에서 `mysql_secure_installation` 실행 시 `validate_password` 플러그인이 엄격(STRONG)하게 설정되어 비밀번호 정책 관련 오류나 비정상적인 동작이 발생하는 경우는 MySQL 8.0 이상 버전에서 자주 보고된 문제다. 특히 `FORCE_PLUS_PERMANENT` 나 `STRONG` 정책이 활성화된 경우 내부 비밀번호 검증 단계가 비정상 종료되거나, 사용자 입력이 제한되는 버그가 존재한다.[mysql +2](https://dev.mysql.com/doc/refman/8.4/en/mysql-secure-installation.html)

## 주요 원인

- `mysql_secure_installation` 스크립트가 `validate_password` 모듈 로드 순서 문제로 인해 정책을 중복 적용하거나, 비밀번호 검증 시 예기치 못한 종료를 일으킴.[bugs.mysql](https://bugs.mysql.com/bug.php?id=80480)
- `validate_password_policy` 기본값이 **STRONG** 또는 **MEDIUM** 으로 되어 있으며, 이에 따라 `dictionary` 파일 미설정이나 `validate_password_check_user_name` 변수가 활성화된 상태에서 오류가 발생함.[mysql](https://dev.mysql.com/doc/mysql-secure-deployment-guide/5.7/en/secure-deployment-password-validation.html)
- 특정 Homebrew 기반 MySQL 8.0~9.0 환경에서 `plugin-load-add=validate_password.so` 가 중복 선언된 경우 서비스가 비정상 종료되는 보고가 있음.[github](https://github.com/Homebrew/homebrew-core/issues/180063)

## 해결 방법

1. **엄격 정책 완화**  
	아래 명령어로 정책 완화:
	```
	sql
	SHOW VARIABLES LIKE 'validate_password%';
	SET GLOBAL validate_password.policy = LOW;
	SET GLOBAL validate_password.length = 4;
	```
	이 설정은 보안 강도를 낮추지만, 개발용 환경(Local, Test 등)에서는 문제 해결에 효과적이다.[msm1307.tistory +2](https://msm1307.tistory.com/131)
2. **임시로 플러그인 비활성화**  
	`mysql_secure_installation` 실행 전 콘솔에서 다음 수행:
	```
	sql
	UNINSTALL PLUGIN validate_password;
	```
	이후 설치 완료 후 재활성화:
	```
	sql
	INSTALL PLUGIN validate_password SONAME 'validate_password.so';
	```
	— 이 방법은 비밀번호 확인 단계에서의 버그를 우회할 때 사용된다.[gcore +1](https://gcore.com/learning/how-to-fix-password-error-mysql)
3. **my.cnf 설정 수정**  
	`/etc/my.cnf` 또는 `/opt/homebrew/etc/my.cnf` 경로에서 `[mysqld]` 섹션에 아래를 추가 또는 조정:
	```
	text
	plugin-load-add=validate_password.so
	validate-password=FORCE_PLUS_PERMANENT
	validate_password_policy=LOW
	validate_password_check_user_name=0
	```
	— 이 설정은 서버 재시작 후 자동으로 정책이 완화된 상태로 유지된다.[percona +1](https://www.percona.com/blog/improving-mysql-password-security-with-validation-plugin/)
4. **스크립트 상 Bug 대응**  
	MySQL 공식 Bug DB(80480, 79305)에 따르면 `mysql_secure_installation` 이 플러그인 실행 중 강제 STRONG 정책을 적용하려다 실패하는 케이스가 존재하며, **MySQL 8.0.36** 이상에서는 이 부분이 개선되었으므로 최신 버전으로의 업그레이드가 권장된다.[bugs.mysql +1](https://bugs.mysql.com/79305)

요약하면, `mysql_secure_installation` 실행 시 발생하는 `validate_password` 관련 엄격 설정 버그는 일시적으로 플러그인을 제거하거나 정책을 LOW로 완화하는 방식으로 우회 가능하며, 완전한 해결은 MySQL 8.0.36 이상으로 업그레이드하거나 `my.cnf` 에서 정책을 사전에 조정하는 것이 가장 안정적이다.