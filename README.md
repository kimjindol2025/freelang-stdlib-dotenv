# freelang-stdlib-dotenv

FreeLang v2 stdlib - dotenv (npm dotenv 완전 대체)

외부 npm 의존성 0개로 `.env` 파일 파싱 및 환경변수 로딩을 구현합니다.

## 설치

```
import "stdlib/dotenv"
```

## 사용

```
// 기본 .env 로드
load()

// 경로 지정
loadFromPath("/app/.env.production")

// 필수 변수 검증 (없으면 exit(1))
requireVars(["DB_HOST", "DB_PORT", "JWT_SECRET"])

// 타입 변환 접근자
let port    = getInt("PORT", 3000)
let isDebug = getBool("DEBUG", false)
let tags    = getList("TAGS", ",")   // "api,web" → ["api","web"]
```

## 파싱 규칙

```
# 주석 무시
KEY=VALUE
KEY="VALUE WITH SPACES"
KEY='single quotes'
KEY=                    # 빈 값 허용
EXPORT KEY=VALUE        # export 키워드 무시
  KEY = VALUE           # 앞뒤 공백 trim
BASE=/home/user
PATH=${BASE}/bin        # 변수 참조 (expand:true 시 치환)
```

## 네이티브 함수 (src/stdlib/dotenv.ts)

| 함수 | 설명 |
|---|---|
| `dotenv_load_file(path)` | 파일 읽기 |
| `dotenv_parse_content(content)` | 내용 파싱 → map |
| `dotenv_apply(parsed, override)` | process.env 적용 |
| `dotenv_expand_map(parsed)` | `${VAR}` 확장 |
| `dotenv_validate_vars(vars)` | 필수 변수 검증 |
| `dotenv_load(path, override, debug, expand)` | 원스톱 로드 |
