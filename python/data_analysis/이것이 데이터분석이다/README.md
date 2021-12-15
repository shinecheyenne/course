# SUMMARY


```python
# 단순 상관 분석 - 상관계수(r) 구하기  ** 결정계수: r^2
# 두 변수 간 선형적 관계를 표현(인과관계 설명x), 1에 가까울수록 강한 양의 상관관계가 있음
# -1 < 피어슨 상관계수 < 1
# pandas - corr() : 피처 간 상관 계수를 matrix 형태로 출력
```


```python
# t-test
# scipy - ttest_ind()로 검정 결과 확인
# 두 집단 간 평균 차에 대한 검정 : 모집단의 평균 모를 때 (두 집단의 데이터가 정규 분포를 보일 때 신뢰도가 높은 검정 방식)
# p-value: 귀무 가설이 맞다는 전제 하에 현재 나온 통계값 이상이 나올 확률 : 기준보다 낮으면 귀무가설 기각, 결과 차이는 통계적으로 유의미
# -> 두 집단의 평균이 다르다.
```

# # Numpy

random.seed() : 랜덤 추출 시드 고정

random.rand() : 넘파이 배열 타입 난수 생성

arange() : 넘파이 배열 생성

reshpae() :행, 열 지정

shape : 넘파이 배열 정보 (행, 열) 확인

zeros() : 0으로 채워진 넘파이 배열 생성




# # Pandas

### (1) 데이터 프레임 기본 정보 출력

dtypes : 데이터 프레임 열 타입 정보 출력

index : 인덱스 정보

shape : (행, 열) 의 개수 출력

info() : 행과 열의 구성 정보

columns: 열의 형태 정보

head() : 상단 부분 출력

describe() : 수치형 피처의 기초 통계량 출력(평균, 표준편차, 최대값 등)


### (2) 데이터 불러오기

read_csv(file_path) : 데이터를 데이터 프레임 형태로 불러옴

### (3) 탐색

unique() : 데이터 범주 반환

value_counts() : series 객체의 모든 데이터의 범주를 개수와 함께 반환

groupby() : 특정 피처 기준으로 그룹 생성

sum(), count() : 총량, 개수

tolist() : 값을 리스트화

apply() : 시리즈 단위의 연산을 처리
 


```python
# apply() 사용 예
df['column_name'].apply(lambda x: float(x[1:]))
```

sort_values(by="", ascending=False): series 데이터를 정렬

drop_duplicates([a,b]) : b내 중복 집계된 a 아이템을 제거

astype() : 데이터 형 변환

loc() / iloc() : 특정 행 지정하여 출력

corr(method='pearson') : 피어슨 상관계수 구하기

isna() : 결측데이터값을 True로 반환

fillna() : 결측데이터 값(NAN) 지정하기

agg() : 여러 연산 결과를 동시에 얻을 수 있음 ex) .agg(['mean','min','sum'])


# # Matplotlib

bar()

scatter()

hist()

legend()

pie()

# # Seaborn

heatmap() : 히트맵

pairplot() : 산점도 그래프

# # Scipy

ttest_ind() : 두 집단의 시리즈 데이터를 넣어 t-test 검정 통계량과 p-value(유의확률) 반환 --> equal_var=True (두 집단의 분산이 같은 경우)


```python

```
