# Gulp
자동화 빌드 시스템

<br>
## Nodejs 설치
[nodejs 다운로드](https://nodejs.org/)<br>
- 설치 후 운영체제를 재시작 해야 정상 작동한다.<br>
![nodejs Download](./Resources/images/node-msi.jpg)

### Node 버전확인
- cmd : `node --version` 입력

### npm (Node Package Manager) 버전확인
- cmd : `npm --version` 입력

<br>
## Gulp 전역설치
[gulp 패키지] (https://www.npmjs.com/package/gulp)

### 참조 
![Documentation documentation for the current release!](./Resources/images/gulp-documentation.jpg)
![Getting Started](/Resources/images/gulp-documentation_start.jpg)

### 설치 
- cmd : `npm install --global gulp` 입력

### 버전확인 
- cmd : `gulp -v` 입력

<br>
## Gulp 프로젝트
### 설치 
1) cmd : `cd Desktop/Gulp` 해당 프로젝트 디렉토리 입력 <br>
2) cmd : `npm init` : package.json 생성 <br>
3) cmd : `npm install --save-dev gulp` 입력 : [node_modules] 생성 <br>
4) package.json 위치에 gulpfile.js 작성 <br>

### 기본(Default) 테스크  
```md
gulp.task('default', function(){
	// 콘솔 (Console)에 메시지 기록(Log)
	console.log('gulp default 수행되었습니다.');
});
```

### 명령어
- **Javascript** ([instruction : javascript](instruction/javascript/README.md))



