---
    layout: post
---

### 1. phoneFormatter
전화번호 형식에 맞게 dash(-)를 추가합니다.

```javascript
export const phoneFormatter = (num) => {
  let formatNum = '';
  const numLength = num.length;
  switch (numLength) {
    case 11:
      formatNum = num.replace(/(\d{3})(\d{4})(\d{4})/, '$1-$2-$3');
      break;
    case 10:
      formatNum = num.startsWith('02') ?
          num.replace(/(\d{2})(\d{4})(\d{4})/, '$1-$2-$3') :
          num.replace(/(\d{3})(\d{3})(\d{4})/, '$1-$2-$3');
      break;
    case 8:
      formatNum = num.replace(/(\d{4})(\d{4})/, '$1-$2');
      break;
    default:
      formatNum = num;
      break;
  }
  return formatNum;
};
```
### 2. 숫자에 천 단위로 comma 찍기

```javascript
export const addComma = (num) => {
  num = num.toString();
  const reg = /(^[+-]?\d+)(\d{3})/;
  while (reg.test(num)) num = num.replace(reg, '$1' + ',' + '$2');
  return num;
};
```

### 3. timestamp 형식 바꾸기

```javascript
export const getDateFromTimestamp = (timestamp) => {
  const date = new Date(timestamp);
  const year = date.getFullYear();
  const month = date.getMonth() + 1;
  const day = date.getDate();
  return `${year}-${month}-${day}`;
};

```

### 4. Date객체의 월, 일이 한자리 일때 0 더하기
```javascript
export const addZ = (n) => { return n<10 ? '0'+n : ''+n };
```