### 함수

- `CEIL(값)` : (올림) 소수점이 있으면 올림하여 가장 가까운 정수 반환
    ~~~
    SELECT CEIL(7.1) FROM DUAL; // 8
    ~~~
- `FLOOR(값)` : (내림) 소수점이 있으면 내림하여 가장 가까운 정수 반환
    ~~~
    SELECT FLOOR(7.45) FROM DUAL; // 7
    ~~~
- `ROUND(값, [반올림위치])` : 반올림위치 바로 뒷자리에서 반올림하여 소수점 처리
    ~~~
    SELECT ROUND(7.45, 1) FROM DUAL; // 7.5 (소수 두번째 자리에서 반올림)
    SELECT ROUND(7.45) FROM DUAL; // 7.4 (소수 첫번째 자리에서 반올림)
    ~~~
- `ABS(값)` : 주어진 값의 절대값 반환
    ~~~
    SELECT ABS(7.45) FROM DUAL; // 7.45
    SELECT ABS(-7.45) FROM DUAL; // 7.45
    ~~~
- `TRUNC(값, [절삭위치])` : 절삭위치 바로 뒷자리부터 소수점을 버림 처리
    ~~~
    SELECT TRUNC(7.45) FROM DUAL; // 7 (소수 첫번째 자리부터 소수점 버림)
    SELECT TRUNC(7.45, 1) FROM DUAL; // 7.4 (소수 두번째 자리부터 소수점 버림)
    ~~~