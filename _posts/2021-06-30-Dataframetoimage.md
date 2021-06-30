---
title: "데이터프레임 이미지 파일로 변환하기"
date: "2021-06-30"
---

내가 필요해서 작성하는 데이터프레임을 캡쳐가 아닌 이미지 파일로 저장하여 사용하는 두 가지 방법.

- dataframe_to_image 라이브러리
- 함수 사용 

포스트의 내용 및 코드는 코랩(Colab) 환경을 기준으로 작성하였음.


[Colab Full code](https://colab.research.google.com/drive/17lC2LbUbjuasV7AKdtdZhaqyYa6w8c_U?usp=sharing)
<br><br>

# 1. 공통부분
##  1) 폰트 설치

데이터프레임에 한글을 사용하면 반드시 한글 폰트 설치를 해준다. 본인은 나눔폰트를 사용하였다. 
<br>
밑의 코드를 실행 후 **런타임 다시 시작**을 반드시 해준다.
```
!sudo apt-get install -y fonts-nanum
!sudo fc-cache -fv
!rm ~/.cache/matplotlib -rf
```
<br>

## 2) 폰트 지정
필요 라이브러리를 불러온 후 폰트 지정을 해준다.
```
import pandas as pd
import matplotlib.pyplot as plt

plt.rc('font', family='NanumBarunGothic') 
```
<br>

## 3) 데이터 프레임 생성

```
data = {'포지션':['GK', 'DF', 'MF', 'FW'], '등번호':['19', '3', '22', '29'], '이름':['노동건', '양상민', '권창훈', '정상빈']}
df = pd.DataFrame(data)
```
<br>

# 2. `dataframe_to_image` 사용
## 1) `dataframe_to_image`를 설치하고 임포트 해준다.
```
!pip install dataframe_to_image

from dataframe_to_image import dataframe_to_image
```
<br>

## 2) `dataframe_to_image` 사용

```
dataframe_to_image.convert(df, visualisation_library='matplotlib')
```
![dataframetoimage-01](https://github.com/chxijihxxn/chxijihxxn.github.io/blob/main/_posts/post-images/dataframetoimage-01.png?raw=true)

<br>

# 3. 함수 사용
## 1) 필요 라이브러리 임포트 
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import six
```
<br>

## 2) 함수 사용
`font_size`, `header_color`등 수정하고 싶은 부분을 수정해서 사용한다.
```
def render_mpl_table(data, col_width=3.0, row_height=0.625, font_size=14,
                     header_color='#184A96', row_colors=['#f1f1f2', 'w'], edge_color='w',
                     bbox=[0, 0, 1, 1], header_columns=0,
                     ax=None, **kwargs):
    if ax is None:
        size = (np.array(data.shape[::-1]) + np.array([0, 1])) * np.array([col_width, row_height])
        fig, ax = plt.subplots(figsize=size)
        ax.axis('off')

    mpl_table = ax.table(cellText=data.values, bbox=bbox, colLabels=data.columns, **kwargs)

    mpl_table.auto_set_font_size(False)
    mpl_table.set_fontsize(font_size)

    for k, cell in  six.iteritems(mpl_table._cells):
        cell.set_edgecolor(edge_color)
        if k[0] == 0 or k[1] < header_columns:
            cell.set_text_props(weight='bold', color='w')
            cell.set_facecolor(header_color)
        else:
            cell.set_facecolor(row_colors[k[0]%len(row_colors) ])
    return ax

render_mpl_table(df, header_columns=0, col_width=2.0)
```
![dataframetoimage-02](https://github.com/chxijihxxn/chxijihxxn.github.io/blob/main/_posts/post-images/dataframetoimage-02.png?raw=true)

<br>

---
Reference :
- [dataframe-to-image](https://pypi.org/project/dataframe-to-image/)
- [코랩 한글 깨짐 현상 방지](https://velog.io/@dk99521/%EC%BD%94%EB%9E%A9%EC%97%90%EC%84%9C-matplotlib-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC%EC%9D%98-%ED%95%9C%EA%B8%80-%EA%B9%A8%EC%A7%90-%ED%98%84%EC%83%81%EC%9D%84-%EB%B0%A9%EC%A7%80%ED%95%98%EB%8A%94-%EB%B2%95)
- [Pandas 데이터 프레임을 테이블 이미지로 내보내기](https://pythonq.com/so/python/163592)
