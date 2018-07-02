---
layout: post
title:  "[Reversing.kr] Easy Crack"
date:   2018-07-02
excerpt: "Reversing.kr 1번"
image: "/images/post1_ (2).png"
---
<hr />
<img src="../images/post1_ (1).png" />
<br>Easy_CrackMe.exe 실행화면
<br><br>
프로그램을 실행해보면 무언가 값을 입력 가능하고, 확인 버튼을 누르면 Incorrect Password라는 문구를 띄운다.<br>아마도 이 문제의 정답은 저 패스워드를 구하는게 아닐까?<br>바로 IDA로 열어보자.<br><br>

<img src="../images/post1_ (2).png" style="width:100%;"/>
<br>
sub_401080을 열어보면 아래와 같이 변수가 선언되어있다.
<br>
```
int result;
CHAR String; // [sp+4h]
char v3; // [sp+5h]
char v4; // [sp+6h]
char v5; // [sp+8h]
__int16 v6;
char v7;
```
쉽게 말해서 메모리를 표현하자면 아래와 같다.<br>
```string | v3 | v4 | v5```<br><br>
다음은 16번째 줄의 if문을 보자<br>
```
if ( v3 == 97 && !strncmp(&v4, a5y, 2u) && !strcmp(&v5, aR3versing) && String == 69 )
```
v3가 97(ASCII로 a), v4가 변수 a5y, v5가 변수 aR3versing, String이 69(ASCII로 E)라는 조건을 가지고 있는 if문이다.
<br>
그러면 a5y와 aR3versing에는 어떤 값이 저장되어있는지 확인해보자.<br><br>
<img src="https://raw.githubusercontent.com/sqrtrev/sqrtrev.github.io/master/images/post1_%20(3).PNG" style="width:100%;"/>
aR3versing에는 R3versing이라는 값이, a5y에는 5y라는 값이 저장되어있다.<br>
위 내용을 기반으로 값들을 조합하면 Password가 나오게된다.<br>
<img src="../images/post1_ (4).png"/><br>
Clear!
<br>
키값은 따로 공유하지 않도록 하겠다.