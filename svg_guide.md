# SVG (Scalable Vector Graphics) 문법 가이드

## 1. 기본 구조

```xml
<svg width="400" height="600" xmlns="http://www.w3.org/2000/svg">
  <!-- SVG 내용이 여기에 들어갑니다 -->
</svg>
```

- `width`, `height`: SVG 캔버스의 크기 지정
- `xmlns`: SVG 네임스페이스 선언

## 2. 기본 도형 요소

### 사각형 (rect)

```xml
<rect
  x="20" y="120"           /* 시작 위치 */
  width="360" height="360" /* 크기 */
  fill="#d3d3d3"          /* 채우기 색상 */
  stroke="#a9a9a9"        /* 테두리 색상 */
  stroke-width="10"       /* 테두리 두께 */
  rx="20" ry="20"         /* 모서리 둥글기 */
/>
```

### 원 (circle)

```xml
<circle
  cx="120" cy="260"  /* 중심점 */
  r="3"              /* 반지름 */
  fill="#cd853f"     /* 채우기 색상 */
/>
```

### 다각형 (polygon)

```xml
<polygon
  points="120,180 123,190 130,190"  /* 꼭지점 좌표들 */
  fill="#d2691e"                    /* 채우기 색상 */
/>
```

## 3. 패스 (path)

### 기본 이동

- `M/m`: 시작점 이동 (Move to)
  ```xml
  M x y   /* 절대 좌표 */
  m dx dy /* 상대 좌표 */
  ```

### 직선 그리기

- `L/l`: 직선 그리기 (Line to)
- `H/h`: 수평선 그리기 (Horizontal line)
- `V/v`: 수직선 그리기 (Vertical line)
  ```xml
  L x y    /* 절대 좌표로 직선 */
  l dx dy  /* 상대 좌표로 직선 */
  H x      /* 절대 x좌표로 수평선 */
  h dx     /* 상대 거리로 수평선 */
  V y      /* 절대 y좌표로 수직선 */
  v dy     /* 상대 거리로 수직선 */
  ```

### 곡선 그리기

- `C/c`: 3차 베지어 곡선
- `S/s`: 매끄러운 3차 베지어 곡선
- `Q/q`: 2차 베지어 곡선
- `T/t`: 매끄러운 2차 베지어 곡선
  ```xml
  C x1 y1, x2 y2, x y  /* 3차 베지어 곡선 */
  S x2 y2, x y         /* 매끄러운 3차 베지어 곡선 */
  Q x1 y1, x y         /* 2차 베지어 곡선 */
  T x y                /* 매끄러운 2차 베지어 곡선 */
  ```

### 호 그리기

```xml
<path d="A rx ry rotation large-arc sweep-flag x y" />
```

- `rx, ry`: 타원의 반지름
- `rotation`: 회전각
- `large-arc`: 큰 호(1) 또는 작은 호(0)
- `sweep-flag`: 시계방향(1) 또는 반시계방향(0)
- `x, y`: 종점 좌표

## 4. 특수 효과

### 애니메이션

```xml
<animate
  attributeName="opacity"    /* 애니메이션을 적용할 속성 */
  values="1;0.5;1"          /* 변화값 */
  dur="2s"                  /* 지속시간 */
  repeatCount="indefinite"  /* 반복횟수 */
/>
```

### 필터 효과

```xml
<filter id="glow">
  <!-- 흐림 효과 -->
  <feGaussianBlur in="SourceGraphic" stdDeviation="2" />

  <!-- 색상 매트릭스 -->
  <feColorMatrix
    type="matrix"
    values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 18 -7"
  />

  <!-- 효과 병합 -->
  <feMerge>
    <feMergeNode in="glow" />
    <feMergeNode in="SourceGraphic" />
  </feMerge>
</filter>
```

## 5. 텍스트 및 변환

### 텍스트

```xml
<text
  x="270" y="405"           /* 위치 */
  font-size="14"            /* 글자 크기 */
  text-anchor="middle"      /* 정렬 방식 */
  fill="black"              /* 글자 색상 */
  transform="rotate(-90)"   /* 회전 변환 */
>
  텍스트 내용
</text>
```

### 변환 (Transform)

```xml
transform="rotate(-90, 200, 400)"  /* 회전 변환 */
transform="scale(0.5)"             /* 크기 변환 */
transform="translate(10, 20)"      /* 이동 변환 */
```

## 예시: 글로우 효과가 있는 도형

```xml
<!-- 필터 정의 -->
<defs>
  <filter id="glow">
    <feGaussianBlur stdDeviation="2" />
    <feColorMatrix type="matrix" values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 18 -7" />
    <feMerge>
      <feMergeNode in="glow" />
      <feMergeNode in="SourceGraphic" />
    </feMerge>
  </filter>
</defs>

<!-- 글로우 효과가 적용된 도형 -->
<circle cx="200" cy="200" r="50" fill="yellow" filter="url(#glow)">
  <animate attributeName="opacity" values="1;0.5;1" dur="2s" repeatCount="indefinite" />
</circle>
```
