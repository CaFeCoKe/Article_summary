# Article_summary
 Summarization Task를 수행하기 위해 KoBART를 네이버 뉴스 요약 데이터셋으로 fine-tuning하여 성능을 확인한다.<br>
 데이터셋은 2022년 7원 1일부터 2022년 7월 10일까지의 기사들이며, train, validation, test 데이터로 나누어져 있다. 데이터셋에 존재하는 test 데이터 외 시기에 따른 이슈가 다른 점도 생각하여 최근의 기사도 요약 해볼 것이다.

## 1. 알고리즘 순서도
## 2. 결과
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