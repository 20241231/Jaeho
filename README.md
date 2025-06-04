<h1 align="center">보안전문가가 되고싶은 이재호 입니다.</h1>
<p align="center">보안 엔지니어 / 모의해킹 / 시스템 취약점 분석</p>

---

## 📌 About Me
- 🔍 보안 구축 엔지니어 양성과정 수료
- 🎯 화이트 해커를 꿈꾸며, 다양한 취약점을 탐구하는 중
- 🧠 늦게 시작했지만 복습과 실습으로 끊임없이 성장 중

---

## 🛠 Tech Stack

| 분야 | 기술 |
|------|------|
| Language | `Python`, `Bash`, `JavaScript`, `PHP` |
| Web | `HTML`, `CSS`, `Mariadb`, `Apache` |
| Tools | `Burp Suite`, `Wireshark`, `Metasploit`, `Hydra`, `Gobuster 등` |
| OS | `Rocky Linux`, `Ubuntu Linux` `Kali Linux`, `Windows` |

---

## 🧩 Projects

### 🔍 주요정보통신기반시설 취약점 분석 스크립트 제작 (2025)
- 기준 문서: "주요정보통신기반시설 기술적 취약점 분석 평가 방법 상세가이드"
- 팀 프로젝트로 진행되었으며, 본인은 **U-49 ~ U-72 항목 진단 스크립트 개발** 담당
- Bash 기반 자동화 스크립트 작성
- 리눅스 시스템 내에서 실시간 결과 리포트 자동 출력
- **로그, 권한, 계정 관리, 서비스 설정 등** 다양한 보안 점검 항목 포함
![result1](https://github.com/user-attachments/assets/a5cf77e2-f818-4c9c-9cfa-cc7be2ffa9ff)
![jaeho](https://github.com/user-attachments/assets/5b2cb4a1-dce1-4e41-a11f-83d3ce3fd833)

---

### 🔐 ESG CTF 머신 제작 (2025)
- 학원 내 보안과정 수강생 대상 CTF 대회를 위한 팀 CTF 구축
- [🔗 문제 페이지 GitHub 링크](https://20241231.github.io/sunglass-ctf)
- 주요 담당:
  - 취약한 WordPress 서버를 Docker로 구축
  - SSH 계정 권한 상승 트랩 설계
  - 문제 해결 시 엔딩 크레딧 출력 페이지 구현
  - GitHub Pages를 통한 다운로드/배포 환경 구축
- 🏆 학원 내 보안과정 CTF 대회 우승

- CTF의 전체 흐름 요약
1. **정보 수집 및 스캐닝**
   - `nmap`으로 IP, 열린 포트 식별
   - 익명 로그인 가능한 FTP 서버에서 단서 파일(`sunglass`) 확보

2. **웹 포트 분석**
   - `7979` 포트 페이지의 소스코드에서 **Base64, ROT47, ROT8000** 조합으로 디코딩 수행
   - 숨겨진 디렉토리(`hidden.txt`)에서 `sunglass90.com` 도메인 발견
   - 낚시용 로그인 페이지 구분 및 유저 힌트(`admin`)

3. **8000번 포트 – Hansel & Alibaba 시나리오**
   - 로그인 후 힌트를 통한 디코딩 → `alibaba` 경로 진입
   - 콘솔 입력 및 `/api/access` 접근으로 암호 획득
   - 암호 `open_sesame` 쿠키 설정 → 새 페이지 진입
   - Burp Suite로 `GET → POST` 변경하여 플래그 획득

4. **8080 포트 – WordPress 취약점**
   - `wpscan`으로 사용자(admin1~5) 열거
   - `hydra`로 패스워드 크랙 → 관리자 로그인
   - 테마 설정을 통한 리버스 쉘 삽입 (`404.php`)
   - Kali에서 `nc` 리스닝 후 셸 획득
   - `.hint` 파일 확인 → 문자열 수집

5. **수집된 문자열 조합**
   - 다운로드 페이지, Apache, WordPress, Alibaba 페이지 힌트 조합
   - Base64 디코딩 → SSH 패스워드 획득

6. **SSH 계정 순차적 권한 상승**
   - `sunglass` → `jaeho` → `smyoo` → `gilhyeong` 순으로 이동
   - 스테가노그래피(`password.jpg`), 숨겨진 파일, 힌트 텍스트, `.bash_login`, `.bash_logout` 등을 활용
   - 힌트: `한 글자를 0.8초 간격으로 11회 반복 타이핑` → 리듬 기반 로그인

7. **setuid 기반 루트 권한 탈취**
   - 의심스러운 바이너리 분석: `strings`, `chmod`, `ss`, `cat`, `echo` 등 활용
   - `setuid` 가능한 실행파일 추출 → `root` 권한 획득
   - `/root/access.txt`, `/root/system.info` 등의 정보 열람 성공
---

### 🕵️‍♂️ 웹 취약점 워게임 (2025)
- SQL Injection, XSS, LFI 등 웹 보안 위주 팀 워게임 문제 제작
- 사용자 세션, 인증 우회, 로그 추적 등 실제 상황을 반영
- PHP + MariaDB 기반 문제 60개 구현
- 🏆 학원 내 보안과정 wargame 대회 우승

- 제작한 wargame 문제 요약
### Problem 01 – 이미지 메타데이터 분석
- **도구**: exiftool, strings
- **설명**: 이미지(EXIF) 메타데이터에 삽입된 flag 추출
- **보안 포인트**: 일반 사용자가 인식하기 어려운 은닉 정보 분석 기법

### Problem 02 – LocalStorage & JS 소스 분석
- **도구**: Developer Tools, JavaScript 분석, Base64 디코딩
- **설명**: 클라이언트 저장소와 JS 내부에 숨겨진 플래그 추적
- **보안 포인트**: 클라이언트에 중요한 정보를 저장하는 위험성

### Problem 03 – 디스크 이미지 포렌식
- **도구**: foremost, strings, base64
- **설명**: 디스크 이미지에서 파일 복원 후 문자열 추출
- **보안 포인트**: 삭제된 정보도 복구 가능하다는 포렌식 시각

### Problem 04 – QR 이미지 복원
- **도구**: 그림판, 온라인 QR 스캐너
- **설명**: 손상된 QR 이미지 시각적으로 복원 후 스캔
- **보안 포인트**: 시각적 복원력과 데이터 은닉의 위험성 강조

### Problem 05 – 텍스트 비교 기반 인코딩 문제
- **도구**: sort, comm, CyberChef
- **설명**: 공통 문자열 추출 후 base64 인코딩
- **보안 포인트**: 문자열 유사성, 인코딩 조작 이해

### Problem 06 – 로그 분석 및 사용자 추적
- **도구**: access.log, grep, JSON 파싱
- **설명**: 로그 기반 특정 사용자 활동 추적 및 정보 확인
- **보안 포인트**: 서버 로그를 통한 정보 유출 가능성 경고

### Problem 07 – SQL Injection
- **도구**: SQL 문법 (`' or 1=1#`)
- **설명**: 로그인 우회 SQLi 시도
- **보안 포인트**: 필터링 없는 입력 값의 치명적 취약성

### Problem 08 – Reflected XSS
- **도구**: script 태그 삽입
- **설명**: 사용자 입력값이 바로 출력되는 구조를 악용한 XSS
- **보안 포인트**: 출력 이스케이프 누락 시 발생하는 취약점

### Problem 09 – Broken Authentication (Cookie 조작)
- **도구**: document.cookie, Developer Tools
- **설명**: 쿠키값 `is_admin=1` 변경 후 관리자 권한 획득
- **보안 포인트**: 인증 정보가 클라이언트에 저장될 때의 위험성

### Problem 10 – URL 인코딩 기반 코드 실행
- **도구**: URL decoding, 콘솔 실행
- **설명**: 주석에 숨겨진 URL-encoded 코드 실행으로 flag 획득
- **보안 포인트**: 눈에 보이지 않는 코드 은닉 및 콘솔 실행의 위험
---

### 🧠 기타 프로젝트
- 보안 인프라 전체 구축 (방화벽, IDS, WAF, VPN, NMS, DB, CTF 등 통합 설계)
- 실습 기반 OWASP Juice Shop 공격/분석
- 시스템 기반 DDoS 탐지 / Suricata, Snort 룰 설계 및 실전 적용
- 로그 분석 플랫폼 (LogAnalyzer, Wazuh, OSSEC) 구성 및 테스트
- 네트워크 토폴로지 설계 및 실제 VM 기반 운영 환경 구성
![networksecurity-portfolio-202502](https://github.com/user-attachments/assets/267eb52c-90ae-4bda-af9a-734a7518a633)
![20250304-s-n](https://github.com/user-attachments/assets/556c0343-29f8-4362-9077-d7d6995f6ab3)
![network-security-lab정보시스템구축추가완료](https://github.com/user-attachments/assets/1aed3825-3d69-40ef-ba9b-51a55151aef0)
![db-software-application-20250404](https://github.com/user-attachments/assets/60bc8d9a-c9d8-47cb-b5d4-bf3bbab453da)
![full_security_portfolio](https://github.com/user-attachments/assets/554a68a9-fbfc-44aa-be2a-5c18a4584607)

---

<p align="center">"공격자의 시선으로 방어를 설계하는 보안 엔지니어가 되겠습니다." 💡</p>
