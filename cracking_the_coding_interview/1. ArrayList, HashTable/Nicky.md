🧐 해시테이블로 풀어라, 라고 하면.. 못풀거같기도.. 

### 1
🧐 자료구조를 추가로 사용하지 않고 풀 수 있는 알고리즘 또한 고민하라 가 뭔말?
- True/False만 반환
- Case-sensitive
```js
const solution = (str) => {
  const len = str.length;
  for (let i = 0; i < len - 1; i++) {
    for (let j = i + 1; j < len; j++) {
      if (str[i] === str[j]) {
        console.log(str[i]);
        return true;
      }
    }
  }

  return false;
};

console.log(solution("Mr John Smith"));
```

### 2
🧐 해설에 'dog'와 'god'가 다르다 가 뭔말?
- `순열관계`? 문자열을 정렬했을때 동일한 문자가 되는 관계
```js
const solution = (str1, str2) => {
  const len1 = str1.length;
  const len2 = str2.length;
  if (len1 !== len2) return false;

  return str1.split("").sort().join() === str2.split("").sort().join();
};

console.log(solution("dog", "ogd"));

```

### 3
```js
const solution = (str, len) => {
  let resultStr = "";
  for (let i = 0; i < len; i++) {
    if (str[i] === " ") {
      resultStr += "%20";
    } else {
      resultStr += str[i];
    }
  }

  return resultStr;
};

console.log(solution("Mr John Smith", 13));
```

### 4
- 회문의 순열..
- 예시로 보아 띄어쓰기는 취급안하는것같음, case-sensitive 아님
```js
const solution = (str) => {
  const target = str.toLowerCase().replace(" ", "");
  const len = target.length;
  let status = {};

  for (let i = 0; i < len; i++) {
    if (status[target[i]]) {
      status[target[i]]++;
    } else {
      status[target[i]] = 1;
    }
  }

  //is 회문
  let numberOfOdds = 0;
  Object.values(status).forEach((val) => {
    if (val % 2 !== 0) numberOfOdds++;
  });

  if (numberOfOdds > 1) return false;

  return true;
};

console.log(solution("Tact Coa"));
```

### 5
- 다른게 1개 이하인지?
- 해설참고함
```js
const solution = (str1, str2) => {
  if (str1.length === str2.length) {
    return checkReplace(str1, str2);
  } else if (str1.length + 1 === str2.length) {
    return checkInsert(str1, str2);
  } else if (str1.length - 1 === str2.length) {
    return checkInsert(str2, str1);
  }

  return false;
};

const checkReplace = (str1, str2) => {
  let foundDifference = false;
  for (let i = 0; i < str1.length; i++) {
    if (str1[i] !== str2[i]) {
      if (foundDifference) {
        return false;
      }
      foundDifference = true;
    }
  }

  return true;
};
const checkInsert = (shortStr, longStr) => {
  let shortIndex = 0;
  let longIndex = 0;
  while (shortIndex < shortStr.length && longIndex < longStr.length) {
    if (shortStr[shortIndex] === longStr[longIndex]) {
      shortIndex++;
      longIndex++;
    } else {
      if (shortIndex !== longIndex) {
        return false;
      }

      longIndex++;
    }
  }

  return true;
};

console.log(solution("bake", "ake"));
```

### 6
🧐 책 오타인가.. c가 네갠데
```js
const solution = (str) => {
  let resultStr = "";
  const len = str.length;

  for (let i = 0; i < len; i++) {
    resultStr += str[i];
    let count = 1;
    const iCopy = i;
    for (let j = iCopy + 1; j < len; j++) {
      if (str[i] === str[j]) {
        count++;
        i++;
      } else {
        break;
      }
    }
    resultStr += count;
  }

  return resultStr.length > str.length ? str : resultStr;
};

console.log(solution("aabcccccaaa"));
```

### 7
```js

```

### 8
- 처음엔 이렇게 풀었다가
```js
const solution = (arr) => {
  const N = arr.length;
  const M = arr[0].length;
  let i,
    j = 0;
  for (let iii = 0; iii < N; iii++) {
    for (let jjj = 0; jjj < M; jjj++) {
      if (arr[iii][jjj] === 0) {
        i = iii;
        j = jjj;
        break;
      }
    }
  }

  const resultArr = arr;
  for (let ii = 0; ii < N; ii++) {
    console.log("ii", i);
    if (ii === i) {
      resultArr[ii] = new Array(M).fill(0);
      continue;
    }
    for (let jj = 0; jj < M; jj++) {
      if (jj === j) {
        console.log(ii + " " + jj);
        resultArr[ii][jj] = 0;
      }
    }
  }

  return resultArr;
};

console.log(
  solution([
    [1, 1, 1, 1, 1],
    [1, 1, 1, 1, 1],
    [1, 0, 1, 1, 1]
  ])
);
```

### 9
```js

```