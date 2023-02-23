# Article_summary
 Summarization Task를 수행하기 위해 KoBART를 네이버 뉴스 요약 데이터셋으로 fine-tuning하여 성능을 확인한다.<br>
 데이터셋은 2022년 7원 1일부터 2022년 7월 10일까지의 기사들이며, train, validation, test 데이터로 나누어져 있다. 데이터셋과 약 6개월 정도의 시간차이로 이슈가 다른 점도 생각하여 최근의 기사도 요약해보도록 할 것이다..

## 1. 알고리즘 순서도 <br><br>
![Article_Summary](https://user-images.githubusercontent.com/86700191/220829629-8c6bef99-31b4-40c4-9cce-b62d63a1f975.png)

## 2. 결과
- Test 데이터셋에 대한 ROUGE 점수<br>
<table border ="0">
    <tr align="center">
      <th></th><th>ROUGE-1</th><th>ROUGE-2</th><th>ROUGE-L</th>
    </tr>
    <tr align="center">
      <th>Precision</th><td>0.658</td><td>0.418</td><td>0.633</td>
    </tr>
    <tr align="center">
      <th >Recall</th><td>0.620</td><td>0.393</td><td>0.597</td>
    </tr>
</table>

- 최근 기사 요약<br>
<table border ="0">
    <tr align="center">
      <th>기사 원본</th><td><a href="https://news.mt.co.kr/mtview.php?no=2023021415450614652">https://news.mt.co.kr/mtview.php?no=2023021415450614652</a></td>
    </tr>
    <tr align="left">
      <th>KoBART 요약</th><td>정필모 더불어민주당 의원은 14일 정보통신방송법안심사소위원회를 통과한 '인공지능산업 육성 및 신뢰 기반 조성 등에 관한 법률안' 이 통과했다고 이날 밝혔으며 이 제정안에 따르면 과학기술정보통신부는 투자 및 인력양성 등 AI 정책 기본 방향을 담은 'AI 기본계획'을 3년마다 수립해야 하고 정책과 예산 등을 심의하기 위한 AI위원회도 구성해야 한다.</td>
    </tr>
</table>
<table border ="0">
    <tr align="center">
      <th>기사 원본</th><td><a href="http://www.womennews.co.kr/news/articleView.html?idxno=232737">http://www.womennews.co.kr/news/articleView.html?idxno=232737</a></td>
    </tr>
    <tr align="left">
      <th>KoBART 요약</th><td>지난 7일 정부는 튀르키예 지진 피해 지역에 110여명 규모의 한국 해외긴급구호대(KDRT)를 급파하여 건물에 깔린 생존자를 찾는 구조견들이 눈부신 활약을 보이고 있다고 밝혔다.</td>
    </tr>
</table>
<table border ="0">
    <tr align="center">
      <th>기사 원본</th><td><a href="https://www.yna.co.kr/view/AKR20230214013600504">https://www.yna.co.kr/view/AKR20230214013600504</a></td>
    </tr>
    <tr align="left">
      <th>KoBART 요약</th><td>미 11월 북한 대륙간탄도미사일(ICBM) 발사에 대응해 미국이 추진해온 유엔 안전보장이사회(안보리) 의장성명이 최종 무산됐다고 미국의소리(VOA) 방송이 14일 보도했으며 안보리의 단합을 촉구하며 안보리의 단합을 촉구했다.</td>
    </tr>
</table>

## 3. 주의점
- 모델 install 후 Hugging Face의 Transformers 사용 문제
  - 해결법 1 (채택) <br>
  Hugging Face Hub를 통해 [Hugging Face에 업로드 되어있는 모델](https://huggingface.co/gogamza/kobart-base-v2) 을 직접 install한다.
  KoBART의 공식 install 방법은 아니지만 같은 모델이라는 [Contributor의 언급](https://github.com/SKT-AI/KoBART/issues/17) 이 있었다.
  <br><br>
  - 해결법 2 <br>
  여러 requirements를 처리하는데에 생긴 [transformers 구 버전의 issue](https://github.com/huggingface/transformers/issues/20799) 이다.
  [해결 방법](https://github.com/CompVis/latent-diffusion/issues/207) 으로는 packaging을 21.3버전으로 재설치, KoBART를 다운 후 transformers를 업그레이드 시켜야 한다.
  ```
  pip install packaging==21.3    # KoBART는 21.0버전으로 설치
  pip install git+https://github.com/SKT-AI/KoBART#egg=kobart
  pip install transformers -U    # KoBART는 4.3.3버전으로 설치, 문제해결을 위해서는 4.6버전 이상의 transformers 필요
  ```

## 4. 사용 모델과 데이터 및 참고링크
- [KoBART](https://github.com/SKT-AI/KoBART)
- [네이버 뉴스 요약 데이터셋](https://huggingface.co/datasets/daekeun-ml/naver-news-summarization-ko)
- [KoBART Summarization Example](https://github.com/seujung/KoBART-summarization)
- [ROUGE score 설명](https://huffon.github.io/2019/12/07/rouge/)
- [TorchMetrics의 ROUGE score](https://torchmetrics.readthedocs.io/en/stable/text/rouge_score.html)