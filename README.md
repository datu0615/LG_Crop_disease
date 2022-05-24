# LG_Crop_disease
![20220524_105615](https://user-images.githubusercontent.com/84311270/169933015-d79ba179-fd21-4d79-aa1f-104cdaf3474d.png)  
"작물 환경 데이터"와 "작물 병해 이미지"를 이용해 "작물의 종류", "병해의 종류", "병해의 진행 정도"를 진단하는 AI 모델 개발하는 것이 목적이였습니다. 

## Dataset
1. train : 학습용 데이터셋  
	├ 10001 : 데이터 고유 아이디  
	│	├ 10001.jpg : 이미지 파일  
	│	├ 10001.csv : 환경 데이터  
	│		└ 촬영 전 48 시간의 "측정 시각", "내부 온도", "내부 습도", "내부 이슬점", "내부 CO2", "외부 풍속", "외부 누적일사" 등의 환경 정보  
	│	└ 10001.json :  
	│		├ description   
	│		│	├ image : 이미지 파일 이름  
	│		│	├ date : 촬영 날짜  
	│		│	├ time : 촬영 시간  
	│		│	├ region : 촬영 지역  
	│		│	├ height : 이미지 높이  
	│		│	├ width : 이미지 너비  
	│		│	└  task : 데이터 종류 (질병/해충/병해/정상 구분)  
	│		└ annotations  
	│				├ disease : 작물 상태 코드  
	│				├ crop : 작물 코드  
	│				├ area : 작물 촬영 부위  
	│				├ grow : 작물의 생육 단계   
	│				├ risk : 질병 피해 정도  
	│				├ bbox : 주목 객체 바운딩 박스 (x, y, w, h 형태)  
	│				└ part : 병해 부위 바운딩 박스 (x, y, w, h 형태)  
	│  
	├ 10002  
	├ 10003  
	└ ...  
	[추가] train.csv : train set에 대한 정답 파일  
 image : 이미지 파일 이름  
 label : "{작물 코드}_{작물 상태 코드}_{질병 피해 정도}" 형태의 문자열  
 "{crop}_{disease}_{risk}"  

2. test : 평가용 데이터셋  
	├ 10001 : 데이터 고유 아이디  
	│	├ 10001.csv : 환경 데이터  
	│		└ 촬영 전 48 시간의 "측정 시각", "내부 온도", "내부 습도", "내부 이슬점", "내부 CO2", "외부 풍속", "외부 누적일사" 등의 환경 정보  
	│	└ 10001.jpg : 이미지 파일  
	│  
	├ 10002  
	├ 10003  
	└ ...  

3. sample_submission.csv : 제출용 양식  
 image : 이미지 파일 이름  
 label : "{작물 코드}_{작물 상태 코드}_{질병 피해 정도}" 형태의 문자열  
 "{crop}_{disease}_{risk}"  
 
## Model
최대한 이미지 scale과 pixel value가 변하지 않는 data augmentation과 data imbalanced 문제를 해결하는 방향으로 접근하였고 최종 모델로는 tf_efficientnet_b4_ns를 사용하였습니다.

