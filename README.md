# 별점 리뷰 기반 음식점 순위
Introduction
---------
우리는 별점의 평균을 보고 음식점을 판단할 때가 많다. 하지만 별점의 평균은 두 가지 문제가 있다. 1) 별점은 continuous variable이 아닌 ordinal variable이기 때문에 평균은 의미가 없다. ex: '별점 5점 음식점' - '별점 4점 음식점' = '별점 3점 음식점' - '별점 2점 음식점' 이 성립될까? 2) 별점의 평균은 sample size를 고려하지 않는다. ex: 5점 리뷰만 3번 받은 음식점과 4점, 5점 리뷰를 100번씩 받은 음식점이 있을 때 어느 음식점을 방문하겠는가? 이를 보안하기 위해 별점을 categorical variable로 다루고, sample size도 고려하는 디리클레 (dirichlet) 분포의 사후확률을 (posterior probability) 이용하여 음식점을 방문했을 때 5점짜리 경험을 하게될 확률을 계산할 것이다.

Process
---------
1. `selenium`을 활용하여 내 주변 음식점의 캐치테이블 고유 코드를 획득한다.
2. `requests`의 `get` 함수로 리뷰 데이터를 가져온다.
3. 디리클레 분포의 사후확률분포를 적용해서 5점 리뷰의 기댓값을 구한다.
4. 5점짜리 경험을 할 기댓값이 가장 높은 음식점을 방문한다!!

Results
---------
5점 별점을 많이 받으면 평균과 5점 별점 기댓값이 동시에 증가하기 때문에 어느정도 correlation이 보인다. 하지만, 스시초심과 포레스트우드의 경우, 4.8점 별점 음식점의 5점 별점 기댓값이 5점 별점 음식점의 5점 별점 기댓값보다 더 높은 경우도 볼 수 있다.

![별점과 디리클레 사후확률 비교](https://user-images.githubusercontent.com/39905872/236180365-2c2f87de-0828-40da-9cd2-151f176d992d.png)

디리클레 분포의 접근도 단점도 있다. 1점 리뷰만 받은 음식점에서 5점짜리 경험을 할 확률이 높을까? 아니면 4점 리뷰만 받은 음식점에서 5점짜리 경험을 할 확률이 높을까? 당연히 4점만 받은 음식점이 더 높을 것이다. 하지만 두 음식점 다 5점의 기댓값은 같다. 5점 기댓값을 계산할 때 1, 2, 3, 4점의 정보가 쓰이지 않기 때문이다. 즉, 별점을 categorical variable로 다루었기 때문에 별점의 ordinality를 무시한다는 뜻이다. 평균값과 디리클레 사후확률 중 무엇이 더 좋다고 확정지어 말할 수는 없지만 별점의 평균이 가진 문제를  해결했다고 생각한다.
