# PlantUML Server - Korean PDF Output Solution

## Project Overview & Environment

- This project is based on [plantuml/plantuml-server](https://github.com/plantuml/plantuml-server/).
- Server environment: Tomcat 10 + JDK 17 (Java 11 used for compilation).

## Korean PDF Output Issue & Solution

1. **Problem**
   - On both Windows 10 and Ubuntu 22.04 (Docker) with Tomcat 10, Korean text in PDF output was broken and displayed as `#`.
   - The Tomcat log repeatedly showed messages like:
     ```
     WARNING: Glyph "..." not available in font "Helvetica"
     ```
   - This indicates that the required Korean font was missing during PDF generation.

2. **Solution**
   - Using Apache FOP version 2.2 or 2.3 resolved the Korean text issue.
   - In the Ubuntu Docker environment, installing the `fonts-nanum` package provided the necessary Korean fonts.
   - Example Dockerfile snippet:
     ```dockerfile
     RUN apt-get update && \
         apt-get install -y fonts-nanum && \
         rm -rf /var/lib/apt/lists/* && \
         fc-cache -fv
     ```

3. **Result**
   - After these changes, Korean text in PDF output was rendered correctly.

---

## 프로젝트 개요 및 환경

- 본 프로젝트는 [plantuml/plantuml-server](https://github.com/plantuml/plantuml-server/)를 기반으로 합니다.
- 서버 환경: Tomcat 10 + JDK 17 (컴파일은 Java 11 사용)

## 한글 PDF 출력 문제 및 해결 과정

1. **문제**
   - Windows 10과 Ubuntu 22.04(Docker) 환경의 Tomcat 10에서 PDF 변환 시 한글이 깨지고 `#` 문자로 표시됨
   - Tomcat 로그에 아래와 같은 메시지가 반복적으로 출력됨:
     ```
     WARNING: Glyph "..." not available in font "Helvetica"
     ```
   - 이는 PDF 생성 시 한글 폰트가 없어서 발생하는 현상임

2. **해결 방법**
   - Apache FOP 2.2 또는 2.3 버전을 사용하면 한글이 정상적으로 출력됨을 확인
   - Ubuntu Docker 환경에서는 `fonts-nanum` 패키지를 설치하여 한글 폰트를 제공
   - Dockerfile 예시:
     ```dockerfile
     RUN apt-get update && \
         apt-get install -y fonts-nanum && \
         rm -rf /var/lib/apt/lists/* && \
         fc-cache -fv
     ```

3. **결과**
   - 위와 같이 설정 후 한글 PDF가 정상적으로 출력됨을 확인
