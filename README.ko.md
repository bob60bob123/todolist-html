# 할 일 목록 ToDo List

[中文](README.md) / [English](README.en.md) / [日本語](README.ja.md) / [한국어](README.ko.md) / [Deutsch](README.de.md) / [Français](README.fr.md)

---

## 개요

싱글 파일 HTML 할 일 목록 애플리케이션 (중국어 UI). 빌드 시스템이나 프레임워크 의존성 없음.

**데모**: `ToDoList.html`을 브라우저에서 직접 열으세요.

## 기능

- 우선순위 수준 (十分紧急 / 较为紧急 / 一般)을 지원하는 CRUD 작업
- 사용자 정의 카테고리
- 기간 통계 (오늘, 이번 주, 이번 달, 이번 분기, 올해)
- 필터: 전체, 활성, 완료, 생성 시간순, 완료 시간순, 카테고리별
- 실시간 검색
- DOCX / Excel 내보내기
- Excel에서 가져오기
- 작업 보고서 생성
-音效
- 반응형 디자인
- **다중 언어 UI** (중국어, 영어, 일본어, 한국어, 독일어, 프랑스어)

## 시작하기

```bash
# macOS
open ToDoList.html

# Windows
start ToDoList.html

# Linux
xdg-open ToDoList.html
```

## 데이터 저장

- 모든 데이터는 브라우저 localStorage에 저장
- 키: `todos`, `todoCategories`

## 기술 스택

- Vanilla JavaScript
- docx@8.5.0 (DOCX 내보내기)
- xlsx@0.18.5 (Excel 가져오기/내보내기)
- Google Fonts: Outfit, JetBrains Mono

## 라이선스

MIT License

```
MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
