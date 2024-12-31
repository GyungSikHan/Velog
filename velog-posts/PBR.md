<h2 id="pbrphysically-based-rendering">PBR(Physically Based Rendering)</h2>
<hr />
<h3 id="정의">정의</h3>
<p>표면의 재질에 따른 빛의 반사가 물리적으로 어떻게 이뤄지는지 시뮬레이션하여 그래픽을 표현하는 기법
빛의 물리적 현상을 기존 방식에 비해 조금 더 과학적인 관점으로 분석한 개념을 기반으로 한 텍스쳐와  셰이딩을 사용한다는 의미</p>
<h3 id="레거시-렌더링-vs-pbr">레거시 렌더링 VS PBR</h3>
<p>기존 렌더링 방식은 레거시 렌더링(Legacy Rendering)이라 구분함
PBR은 레거시 렌더링과 비교해 개념이나 특정 고난도 기술, 새로운 엔진을 요하는 방식이 아니라 그래픽 리소스를 줄이면서 더 사실적으로 구현 가능하고, 최적화에 더 용리함</p>
<table>
<thead>
<tr>
<th>구분</th>
<th>레거시 렌더링</th>
<th>물리기반 렌더링</th>
</tr>
</thead>
<tbody><tr>
<td>재질의기본색</td>
<td>난반사(Diffuse)텍스처</td>
<td>기본색(Base Color)</td>
</tr>
<tr>
<td>재질의 반사광</td>
<td>정반사(Specular) 텍스처(또는 값)</td>
<td>금속성(Metallic) 값</td>
</tr>
<tr>
<td>재질의 거칠기</td>
<td>반사(Reflection) 텍스처(또는 값)</td>
<td>거칠기(ROughness) 텍스처(또는 값)</td>
</tr>
</tbody></table>
<h3 id="1-난반사광diffuse-lighthing--컬러를-만드는-반사">1. 난반사광(Diffuse Lighthing) : 컬러를 만드는 반사</h3>
<p>레거시 렌더링은 추상적인 관점으로 난반사광을 별도로 분리해서 구현하는 데 보이는 이미지를 그대로 텍스처로 사용하며, 이것을 난반사(Diffuse) 텍스처라 부름
PBR에선 재질이 반사하는 순수한 색(Color)의 파장만 고려해 기본색(Base Color) 텍스처를 제작해 사용<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/b6656b6a-9940-4e90-8958-534fbe657b54/image.png" /></p>
<h3 id="2-정반사광specular-lighting--표면의-각도에-따른-반사">2. 정반사광(Specular Lighting) : 표면의 각도에 따른 반사</h3>
<p>레거시 렌더링에서 회색조(Graysc;ae)의 환경 맵(Environment Map)을 이용해 정반사광을 구현하거나, 마스크 맵(Marsk Map)을 이용해 정반사 텍스처를 제작하고 픽셀 단위 라이팅을 적용해 구현하는 방식이 존재
또는 별도의 텍스처를 사용하지 않고 광원의 위치와 표면 각에 따라 광원이 반사되는 수치를 입력하는 방법으 구현
PBR에선 재질이 금속(Metallic)을 가진 빛 자체를 더 많이 반사하게 된다는 현상에 입각해, 재질의 금속성 값이 어느 정도인지 수치로 입력하는 방법을 사용<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/020b375b-f373-4893-85dd-6374602aba26/image.png" /></p>
<h3 id="3전반사광total-reflection--표면의-거칠기에-따른-반사의-선명도">3.전반사광(Total Reflection) : 표면의 거칠기에 따른 반사의 선명도</h3>
<p>레거시 렌더링에선 실제 표면의 거칠기와는 무관하게 작엊바가 반사 재질을 지니게 만들고 싶은 파트에 해당 표면의 전반사 속성을 적용/비적용으로 구분하여 주변 환경을 맵으로 이용해 주변이 오브젝트에 반사되는 것처럼 눈속임을 하거나, 반사될 장면을 한번 더 렌더링해 실시간 반사를 구현하는 방법을 사용
PBR에선 전반사의 구현 방식은 동일하나, 표면의 거칠기 정도에 따라 해당 표면의 전반사성이 반비례되는 값을 조절하는 방식 사용<img alt="" src="https://velog.velcdn.com/images/gksrudtlr2/post/13a8492a-86bc-4159-80f7-74cd0aa0d8ac/image.png" /></p>
<h3 id="외의것">외의것</h3>
<p>위의 3가지는 기본적인 재질에 대한 빛의 물리적 반사 현상을 시뮬레이션 하는 부분으로 변경된 것으로, 재질과 질감에 관련된 핵심 요소가 됨
이 외에 굴절(Refraction), 외곡(Distortion), 프레넬(Fresnel)과 같은 옵션이 추가로 들어갈 수 있으나, 이는 레거시와 PBR 모두 적용이 가능</p>