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
   - `/...` root플래그 열람 성공
     
![image](https://github.com/user-attachments/assets/9535e57e-bb8e-474e-b591-3532b33bc980)
![image](https://github.com/user-attachments/assets/536e403d-e372-4c37-b3e3-61a2aafae967)

---

### 🕵️‍♂️ 웹 취약점 워게임 (2025)
- SQL Injection, XSS, LFI 등 웹 보안 위주 팀 워게임 문제 제작
- 사용자 세션, 인증 우회, 로그 추적 등 실제 상황을 반영
- PHP + MariaDB 기반 문제 60개 구현
- 🏆 학원 내 보안과정 wargame 대회 우승

### 문제 요약 (Problem 01 ~ 10)
| 번호 | 제목 | 도구 | 설명 | 보안 포인트 |
|------|------|------|------|--------------|
| 01 | 이미지 메타데이터 분석 | `exiftool`, `strings` | 이미지(EXIF) 메타데이터에 삽입된 flag 추출 | 은닉 정보 분석 |
| 02 | LocalStorage & JS 분석 | DevTools, JS 분석, `Base64` | 클라이언트 저장소와 JS 내부에 숨겨진 플래그 추적 | 클라이언트 저장소 위험성 |
| 03 | 디스크 이미지 포렌식 | `foremost`, `strings`, `base64` | 파일 복원 후 문자열 추출 | 삭제 정보 복구 가능성 |
| 04 | QR 이미지 복원 | 그림판, 온라인 QR 스캐너 | 손상된 QR 이미지 복원 후 스캔 | 시각적 복원과 데이터 은닉 |
| 05 | 텍스트 비교 기반 인코딩 | `sort`, `comm`, CyberChef | 공통 문자열 추출 후 인코딩 | 문자열 유사성과 인코딩 조작 |
| 06 | 로그 분석 | `access.log`, `grep`, JSON 파싱 | 로그 기반 사용자 활동 추적 | 서버 로그 통한 유출 위험 |
| 07 | SQL Injection | SQL 문법 (`' or 1=1#`) | 로그인 우회 SQLi | 입력 필터링 부재 취약성 |
| 08 | Reflected XSS | `<script>` 삽입 | 입력값 즉시 출력 구조 악용 | 출력 이스케이프 누락 위험 |
| 09 | Broken Authentication | DevTools, `document.cookie` | `is_admin=1`로 관리자 권한 획득 | 인증정보 클라이언트 저장 위험성 |
| 10 | URL 인코딩 기반 코드 실행 | URL 디코딩, 콘솔 실행 | 숨겨진 코드 실행 후 flag 획득 | 콘솔 실행 및 은닉 코드 취약점 |
  
![image](https://github.com/user-attachments/assets/da6ee63a-e661-41cf-9a06-7ae1880cdda8)
![image](https://github.com/user-attachments/assets/8bfe7c44-30b9-4d94-befe-66b1bd344b93)
 

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
